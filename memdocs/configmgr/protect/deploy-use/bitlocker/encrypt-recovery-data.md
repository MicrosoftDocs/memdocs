---
title: Encrypt recovery data in the database
titleSuffix: Configuration Manager
description: Encrypt BitLocker recovery keys, recovery packages, and TPM password hashes in the Configuration Manager database.
ms.date: 11/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Encrypt recovery data in the database

*Applies to: Configuration Manager (current branch)*

<!--3601034-->

When you create a BitLocker management policy, Configuration Manager deploys the recovery service to a management point. On the **Client Management** page of the BitLocker management policy, when you **Configure BitLocker Management Services**, the client backs up key recovery information to the site database. This information includes BitLocker recovery keys, recovery packages, and TPM password hashes. When users are locked out of their protected device, you can use this information to help them recover access to the device.

Given the sensitive nature of this information, you need to protect it. Configuration Manager requires an HTTPS connection between the client and the recovery service to encrypt the data in transit across the network. For more information, see [Encrypt recovery data over the network](encrypt-recovery-data-transit.md).

Consider also encrypting this data when stored in the site database. If you install a SQL Server certificate, Configuration Manager encrypts your data in SQL.

If you don't want to create a BitLocker management encryption certificate, opt-in to plain-text storage of the recovery data. When you create a BitLocker management policy, enable the option to **Allow recovery information to be stored in plain text**.

> [!NOTE]
> Another layer of security is to encrypt the entire site database. If you enable encryption on the database, there aren't any functional issues in Configuration Manager.
>
> Encrypt with caution, especially in large-scale environments. Depending upon the tables you encrypt and the version of SQL, you may notice up to a 25% performance degradation. Update your backup and recovery plans, so that you can successfully recover the encrypted data.

> [!NOTE]
> Configuration Manager never removes or deletes recovery information for devices from the database, even if the client is inactive or deleted. This behavior is for security reasons. It helps with scenarios where a device is stolen but later recovered. For large environments, the impact to the database size is about 9 KB of data per encrypted volume.

## SQL Server encryption certificate

Use this SQL Server certificate for Configuration Manager to encrypt BitLocker recovery data in the site database. You can create a self-signed certificate using a script in SQL Server.

Alternatively, you can use your own process to create and deploy this certificate, as long as it meets the following requirements:

- The name of the BitLocker management encryption certificate must be `BitLockerManagement_CERT`.

- Encrypt this certificate with a database master key.

- The following SQL Server users need **Control** permissions on the certificate:
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- Deploy the same certificate at every site database in your hierarchy.

- Create the certificate with the latest version of SQL Server in your environment. For example:
  - Certificates created with SQL Server 2016 or later are compatible with SQL Server 2014 or earlier.
  - Certificates created with SQL Server 2014 or earlier aren't compatible with SQL Server 2016 or later.

## Example scripts

These SQL scripts are examples to create and deploy a BitLocker management encryption certificate in the Configuration Manager site database.

### Create certificate

This sample script does the following actions:

- Creates a certificate
- Sets the permissions
- Creates a database master key

Before you use this script in a production environment, change the following values:

- Site database name (`CM_ABC`)
- Password to create the master key (`MyMasterKeyPassword`)
- Certificate expiry date (`20391022`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

> [!NOTE]
> The certificate expiration date is not checked or enforced by SQL Server when the certificate is used for database encryption as is the case here.

### Back up certificate

This sample script backs up a certificate. When you save the certificate to a file, you can then [restore](#restore-certificate) it to other site databases in the hierarchy.

Before you use this script in a production environment, change the following values:

- Site database name (`CM_ABC`)
- File path and name (`C:\BitLockerManagement_CERT_KEY`)
- Export key password (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'MyExportKeyPassword')
```

> [!IMPORTANT]
> Store the exported certificate file and associated password in a secure location.

### Restore certificate

This sample script restores a certificate from a file. Use this process to deploy a certificate that you created on another site database.

Before you use this script in a production environment, change the following values:

- Site database name (`CM_ABC`)
- Master key password (`MyMasterKeyPassword`)
- File path and name (`C:\BitLockerManagement_CERT_KEY`)
- Export key password (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'MyExportKeyPassword')

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### Verify certificate

Use this SQL script to verify that SQL Server successfully created the certificate with the required permissions.

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

If the certificate is valid, the script returns a value of `1`.

## See also

For more information on these SQL commands, see the following articles:

- [SQL Server and database encryption keys](/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [Create certificate](/sql/t-sql/statements/create-certificate-transact-sql)
- [Backup certificate](/sql/t-sql/statements/backup-certificate-transact-sql)
- [Create master key](/sql/t-sql/statements/create-master-key-transact-sql)
- [Backup master key](/sql/t-sql/statements/backup-master-key-transact-sql)
- [Grant certificate permissions](/sql/t-sql/statements/grant-certificate-permissions-transact-sql)

## Next steps

[Deploy BitLocker management client](deploy-management-agent.md)
