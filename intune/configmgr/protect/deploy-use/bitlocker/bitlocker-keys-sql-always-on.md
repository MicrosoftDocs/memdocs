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

When you encrypt the BitLocker information using the instructions at [Encrypt recovery data in the database](encrypt-recovery-data.md), there are additional steps required to ensure that all AlwaysOn nodes can automatically open the Database Master Key (DMK) when a failover event occurs. This allows seamless retrieval of BitLocker keys without manual intervention.

## Why is is this necessary with SQL AlwaysOn?

SQL Server encrypts data using a hierarchical infrastructure and is described in depth at [Encryption Hierarchy](/sql/relational-databases/security/encryption/encryption-hierarchy)

- Site Master Key (SMK) - this key is a *per instance* key that is unique to each SQL Server AlwaysOn node and is not replicated. It is used to encrypt the database master key.
- Database Master Key (DMK) - this key is stored in the database and is replicated. It is used to encrypt the BitLockerManagement_CERT
- BitLockerManagement_CERT - this certificate is stored in the database and is replicated. It is used to encrypt some BitLocker-related data like recovery keys.

The DMK password is encrypted by the SMK. Because the SMK is node-specific, when a failover event occurs the new primary node will be unable to decrypt the DMK password because it was encrypted by a different SMK. Setting the DMK password on each node allows the node to decrypt the password on failover.

> [!NOTE]
>
> The BitlockerManagemnt_CERT performs the encryption of the columns. If this certificate is lost or deleted, or the DMK that encrypted it is lost or deleted, BitLocker keys will have to be escrowed and re-encrypted again.

> [!IMPORTANT]
>
> - Replace `password` everywhere below with a strong password of your choosing.
> - Replace `CM_XXX` with the name of your Configuration Manager (CM) database.

---

## If the Database Master Key password is known

Execute the following command on each node in the Availability Group that hosts the Configuration Manager database. This wll register the DMK password with the local Service Master Key (SMK), allowing SQL Server to automatically open the DMK when a failover event occurs.

```sql
EXEC sp_control_dbmasterkey_password
    @db_name = N'CM_XXX',
    @password = N'password',
    @action = N'add';
```

This ensures the DMK can be decrypted automatically on that node after failovers or restarts.

---

## If the existing Database Master Key password is unknown

If the existing DMK password is unknown, the existing DMK must be dropped and a new one created with a known password. These steps document how perform this procedure.

### How to find a valid DMK

If you don't know which node has a valid DMK, running this query will help you determine where the existing DMK is open.

```sql
select RecoveryAndHardwareCore.DecryptString(RecoveryKey, DEFAULT) from RecoveryAndHardwareCore_Keys
```

If the DMK is open, the query will return plaintext values for any rows that have a valid key in them.
If the DMK is not open, it will return NULL values for all rows.

Run the query on the primary node, and if that returns all NULL values, failover to each secondary node until you find a node that can decrypt the RecoveryAndHardwareCore_Keys successfully. This is the node you will start on.

(1) **Export the BitLockerManagement_CERT certificate with its private key** (using a strong password):

```sql
BACKUP CERTIFICATE BitLockerManagement_CERT
TO FILE = 'C:\Windows\Temp\BitLockerManagement_CERT'
WITH PRIVATE KEY
(
    FILE = 'C:\Windows\Temp\BitLockerManagement_CERT_KEY',
    ENCRYPTION BY PASSWORD = 'password'
);
```

(1b) **Export the existing DMK** (for backup):

```sql
BACKUP MASTER KEY
TO FILE = 'C:\Windows\Temp\DMK'
ENCRYPTION BY PASSWORD = 'password';
```

(2) **Drop the existing certificate and DMK** (this removes the old keys):

```sql
DROP CERTIFICATE BitLockerManagement_CERT;
DROP MASTER KEY;
```

(3) **Create a new DMK** (using a strong password):

```sql
CREATE MASTER KEY
ENCRYPTION BY PASSWORD = 'password';
```

(3b) **Register the new DMK password with the local SMK** (once on the active node):

```sql
EXEC sp_control_dbmasterkey_password
    @db_name = N'CM_XXX',
    @password = N'password',
    @action = N'add';
```

(4) **Import the previously exported BitLockerManagement_CERT certificate**:

```sql
CREATE CERTIFICATE BitLockerManagement_CERT
FROM FILE = 'C:\Windows\Temp\BitLockerManagement_CERT'
WITH PRIVATE KEY
(
    FILE = 'C:\Windows\Temp\BitLockerManagement_CERT_KEY',
    DECRYPTION BY PASSWORD = 'password'
);
```

(5) **Grant required control permissions on the certificate**:

```sql
GRANT CONTROL ON CERTIFICATE::BitLockerManagement_CERT TO RecoveryAndHardwareCore;
GRANT CONTROL ON CERTIFICATE::BitLockerManagement_CERT TO RecoveryAndHardwareRead;
GRANT CONTROL ON CERTIFICATE::BitLockerManagement_CERT TO RecoveryAndHardwareWrite;
```

(6) **Fail over to the next node.**

(7) **Register the DMK password with the local SMK** (execute once per replica):

```sql
EXEC sp_control_dbmasterkey_password
    @db_name = N'CM_XXX',
    @password = N'password',
    @action = N'add';
```

(8) Perform steps 6 and 7 on any remaining nodes.

(9) **Fail over to the original node.**

(10) To verify that all nodes will automatically open the Database Master Key and can decrypt the data failover to each node and run the query in the [How to find a valid DMK](#how-to-find-a-valid-dmk) section.

> [!TIP]
> For improved security:** Store the strong DMK password securely (e.g., in Azure Key Vault or another secure secret store) and avoid hardcoding it in scripts or configuration files.
