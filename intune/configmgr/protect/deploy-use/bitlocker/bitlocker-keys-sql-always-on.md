---
title: Using BitLocker Management with SQL Always On
titleSuffix: Configuration Manager
description: Describes how to use BitLocker Management with SQL Always On
ms.date: 06/10/2025
ms.service: configuration-manager
ms.subservice: protect
ms.topic: how-to
author: frankroj
ms.author: frankroj
manager: bpardi
ms.localizationpriority: medium
ms.reviewer: frankroj,mstewart
ms.collection: tier3
---

# BitLocker Encryption with SQL AlwaysOn

For SQL AlwaysOn, additional steps are required when the BitLocker information is encrypted using the instructions at [Encrypt recovery data in the database](encrypt-recovery-data.md). The additional steps ensure that all AlwaysOn nodes can automatically open the Database Master Key (DMK) when a failover event occurs. Following steps allows seamless retrieval of BitLocker keys without manual intervention.

## Overview of BitLocker Encryption with SQL AlwaysOn

SQL Server encrypts data using a hierarchical infrastructure and is described in depth at [Encryption Hierarchy](/sql/relational-databases/security/encryption/encryption-hierarchy).

- **Site Master Key (SMK)** - this key is a *per instance* key that is unique to each SQL Server AlwaysOn node and isn't replicated. It's used to encrypt the database master key.
- **Database Master Key (DMK)** - this key is stored in the database and is replicated. It's used to encrypt the BitLockerManagement_CERT.
- **BitLockerManagement_CERT** - this certificate is stored in the database and is replicated. It's used to encrypt some BitLocker-related data like recovery keys.

The SMK encrypts the DMK password. SMKs are node-specific. When a failover event occurs, the new primary node can't decrypt the DMK password since it was encrypted with a different SMK. Setting the DMK password on each node allows the node to decrypt the password on failover.

> [!NOTE]
>
> The BitlockerManagemnt_CERT performs the encryption of the columns. If this certificate is lost or deleted, or the DMK that encrypted is lost or deleted, BitLocker keys have to be escrowed and re-encrypted again.

## If the Database Master Key (DMK) password is known

Execute the following command on each node in the Availability Group that hosts the Configuration Manager database.

> [!IMPORTANT]
>
> In the following command:
>
> - Replace `password` everywhere with a strong password of your choosing. Make sure to securely store the password for future reference.
> - Replace `CM_XXX` with the name of the Configuration Manager (CM) database.

```sql
EXEC sp_control_dbmasterkey_password
    @db_name = N'CM_XXX',
    @password = N'password',
    @action = N'add';
```

This command registers the DMK password with the local Service Master Key (SMK) allowing SQL Server to automatically open the DMK when a failover event occurs. This process ensures the DMK can be decrypted automatically on that node after a failover or a restart.

## If the existing Database Master Key (DMK) password is unknown

If the existing DMK password is unknown, the existing DMK must be dropped and a new one created with a known password. These steps document how to perform this procedure.

### Find a valid DMK

If it's unknown which node has a valid DMK, follow these steps to determine where the existing DMK is open:

> [!IMPORTANT]
>
> In the following queries and commands:
>
> - Replace `password` everywhere with a strong password of your choosing. Make sure to securely store the password in a known location for future reference.
> - Replace `CM_XXX` with the name of the Configuration Manager (CM) database.

1. Run the following query on the primary node:

    ```sql
    select RecoveryAndHardwareCore.DecryptString(RecoveryKey, DEFAULT) from RecoveryAndHardwareCore_Keys
    ```

1. In the resultant query:

   - If the DMK is open, the query returns plaintext values for any rows that have a valid key in them. This node is the node to start on and the next step can be skipped.
   - If the DMK isn't open, the query returns NULL values for all rows. The current node isn't the node where the DMK is open. Follow the next step to find the node where the DMK is open.

1. If the query returns all NULL values, then failover to each secondary node and repeat the previous steps until the node that can successfully decrypt **RecoveryAndHardwareCore_Keys** is found. This node is the node to start on.

### Create a new Database Master Key (DMK)

Once the proper node with the open DMK is identified, follow these steps:

1. On the node that was identified in the previous steps, run the following query to export the BitLockerManagement_CERT certificate with its private key. Make sure to use a strong password:

    ```sql
    BACKUP CERTIFICATE BitLockerManagement_CERT
    TO FILE = 'C:\Windows\Temp\BitLockerManagement_CERT'
    WITH PRIVATE KEY
    (
        FILE = 'C:\Windows\Temp\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'password'
    );
    ```

1. Backup the existing Database Master Key (DMK) by running the following query to export the existing DMK:

    ```sql
    BACKUP MASTER KEY
    TO FILE = 'C:\Windows\Temp\DMK'
    ENCRYPTION BY PASSWORD = 'password';
    ```

    > [!NOTE]
    >
    > This step is optional but recommended. Make sure to keep the backup in a secure known location.

1. Run the following query to drop the existing certificate and DMK:

    ```sql
    DROP CERTIFICATE BitLockerManagement_CERT;
    DROP MASTER KEY;
    ```

    This step removes the old keys.

1. Run the following query to create a new DMK. Make sure to use a strong password:

    ```sql
    CREATE MASTER KEY
    ENCRYPTION BY PASSWORD = 'password';
    ```

1. Run the following query to register the new DMK password with the local SMK:

    ```sql
    EXEC sp_control_dbmasterkey_password
        @db_name = N'CM_XXX',
        @password = N'password',
        @action = N'add';
    ```

1. Run the following query to import the previously exported BitLockerManagement_CERT certificate:

    ```sql
    CREATE CERTIFICATE BitLockerManagement_CERT
    FROM FILE = 'C:\Windows\Temp\BitLockerManagement_CERT'
    WITH PRIVATE KEY
    (
        FILE = 'C:\Windows\Temp\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'password'
    );
    ```

1. Run the following query to grant required control permissions on the certificate:

    ```sql
    GRANT CONTROL ON CERTIFICATE::BitLockerManagement_CERT TO RecoveryAndHardwareCore;
    GRANT CONTROL ON CERTIFICATE::BitLockerManagement_CERT TO RecoveryAndHardwareRead;
    GRANT CONTROL ON CERTIFICATE::BitLockerManagement_CERT TO RecoveryAndHardwareWrite;
    ```

1. Fail over to the next node.

1. Run the following query to register the DMK password with the local SMK. Execute once per replica:

    ```sql
    EXEC sp_control_dbmasterkey_password
        @db_name = N'CM_XXX',
        @password = N'password',
        @action = N'add';
    ```

1. Perform the previous two steps on any remaining nodes.

1. Fail over to the original node.

### Verify all nodes can automatically open the Database Master Key (DMK) and can decrypt the data

1. To verify that all nodes automatically open the Database Master Key (DMK) and can decrypt the data:

   1. Failover to a node.

   1. Run the following query:

    ```sql
    select RecoveryAndHardwareCore.DecryptString(RecoveryKey, DEFAULT) from RecoveryAndHardwareCore_Keys
    ```

   1. If the query returns plaintext values for any rows that have a valid key in them, then the node can automatically open the Database Master Key (DMK) and can decrypt the data.

   1. Repeat the previous three steps for each additional node.

> [!TIP]
>
> For improved security, store the strong DMK password securely. For example, in Azure Key Vault or another secure secret store. Additionally, avoid hardcoding the DMK password in plain text in scripts or configuration files.
