---
title: "SMS_StateMigration Class"
titleSuffix: "Configuration Manager"
description:" "An SMS Provider that contains all the state migration information for a specific computer association and exposes methods for managing an association."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 04fc39cc-e229-4bd1-8382-9d5b78af2867
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_StateMigration Server WMI Class
The `SMS_StateMigration` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that contains all the state migration information for a specific computer association and exposes methods for managing an association.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_StateMigration : SMS_BaseClass  
{  
   UInt32 MigrationBehavior;  
   String MigrationID;  
   UInt32 MigrationStatus;  
   UInt32 MigrationType;  
   UInt32 RestoreClientResourceID;  
   String RestoreLastLogonUserDomain;  
   String RestoreLastLogonUserName;  
   String RestoreMACAddresses;  
   String RestoreName;  
   String SiteCode;  
   UInt32 SourceClientResourceID;  
   String SourceLastLogonUserDomain;  
   String SourceLastLogonUserName;  
   String SourceMACAddresses;  
   String SourceName;  
   DateTime StoreCreationDate;  
   DateTime StoreDeletionDate;  
   String StorePath;  
   DateTime StoreReleaseDate;  
   SMS_StateMigrationUserNames UserNames[];  
};  
```  

## Methods  
 The following table shows the methods in `SMS_StateMigration`.  

|Method|Description|  
|------------|-----------------|  
|[AddAssociation Method in Class SMS_StateMigration](../../../develop/reference/osd/addassociation-method-in-class-sms_statemigration.md)|Adds the association between two system resources.|  
|[DeleteAssociation Method in Class SMS_StateMigration](../../../develop/reference/osd/deleteassociation-method-in-class-sms_statemigration.md)|Deletes the association between two system resources.|  
|[GetEncryptDecryptKey Method in Class SMS_StateMigration](../../../develop/reference/osd/getencryptdecryptkey-method-in-class-sms_statemigration.md)|Retrieves the symmetric key that is used to encrypt and decrypt the user state.|  
|[AddAssociationEx Method in Class SMS_StateMigration](../../../develop/reference/osd/addassociationex-method-in-class-sms_statemigration.md)|Adds the association with a specified migration behavior between two system resources.|  

## Properties  
 `MigrationBehavior`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Migration behavior. Possible values are:  

| Value | Migration behavior |  
| ----- | ------------------ |  
|0|CAPTUREANDRESTOREALL|  
|1|CAPTUREALLRESTORESPECIFIED|  
|2|CAPTUREANDRESTORESPECIFIED|  

 `MigrationID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Unique migration ID. The default value is "".  

 `MigrationStatus`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Migration status. Possible values are:  

| Value | Migration status |  
| ----- | ---------------- |  
|0|NOTSTARTED|  
|1|INPROGRESS|  
|2|COMPLETED|  

 `MigrationType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The migration type used to store the user state. Possible values are:  

| Value | Migration type |  
| ----- | -------------- |  
|1|SIDEBYSIDE|  
|2|INPLACE|  

 `RestoreClientResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique resource ID of the restore client.  

 `RestoreLastLogonUserDomain`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last logon user domain of the user on the restore client.  

 `RestoreLastLogonUserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last logon user name on the restore client.  

 `RestoreMACAddresses`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Media access controller (MAC) addresses of the restore client.  

 `RestoreName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the restore client.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Site code.  

 `SourceClientResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of the source client.  

 `SourceLastLogonUserDomain`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last logon user domain of the user on the source client.  

 `SourceLastLogonUserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last logon user name on the source client.  

 `SourceMACAddresses`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 MAC addresses of the source client.  

 `SourceName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the source client.  

 `StoreCreationDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when the state was saved. The default value is "00000000000000.000000+***".  

 `StoreDeletionDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when the state was deleted. The default value is "00000000000000.000000+***".  

 `StorePath`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The UNC path indicating the location of the state store.  

 `StoreReleaseDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when the state was migrated. The default value is "00000000000000.000000+***".  

 `UserNames`  
 Data type: `SMS_StateMigrationUserNames` Array  

 Access type: Read-only  

 Qualifiers: [read, lazy]  

 [SMS_StateMigrationUserNames Server WMI Class](../../../develop/reference/osd/sms_statemigrationusernames-server-wmi-class.md) objects representing the user names to be migrated.  

## Remarks  
 Class qualifiers for this class include:  

- Secured  

  For more information about both the class qualifiers and the property qualifiers that are included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class represents state migration that is used in configuring sites for operating system deployment. State migration primarily affects resources, for example, memory, for the state migration point. During migration, user state and settings are copied from one computer to another as part of operating system deployment.  

> [!NOTE]
>  The state migration point requires Internet Information Services (IIS) to be installed.  

 For an example of the use of this class, see How to Create an Association Between Two Computers in Configuration Manager.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See also

[SMS_StateMigrationUserNames server WMI class](sms_statemigrationusernames-server-wmi-class.md)
