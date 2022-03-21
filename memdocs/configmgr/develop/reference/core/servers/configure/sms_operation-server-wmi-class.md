---
title: "SMS_Operation Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ea1053c7-f7e8-4641-8328-2e4c4d6bb93c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_Operation Server WMI Class
The `SMS_Operation` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that is embedded by `SMS_RbacSecuredObject` and describes the various operations.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Operation :    
{  
    UInt32 BitFlag;  
    Boolean IsTypeWideOperation;  
    UInt32 ObjectTypeID;  
    String OperationName;  
};  
```  

## Methods  
 The `SMS_Operation` class does not define any methods.  

## Properties  
 `BitFlag`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The bit flag of the operation. Possible values are:  

|N|2^N|Operation|  
|-|-|-|  
|0|1|Read|  
|1|2|Modify|  
|2|4|Delete|  
|3|8|Copy to Distribution Point|  
|4|16|Set Security Scope|  
|5|32|Remote Control|  
|6|64|Not Used|  
|7|128|Modify Resource|  
|8|256|Not Used|  
|9|512|Delete Resource|  
|10|1024|Create<br /><br /> Admin.Add|  
|11|2048|View Collected File<br /><br /> Application.Approve|  
|12|4096|Read Resource|  
|13|8192|Manage Folder Item|  
|14|16384|Meter Site<br /><br /> Collection.Deploy Packages|  
|15|32768|Not Used|  
|16|65536|Manage Status Filters<br /><br /> Collection.Deploy Client Settings|  
|17|131072|Manage Folder|  
|18|262144|ConfigurationItem.Network Access<br /><br /> Site.Modify CH Settings<br /><br /> Collection.EnforceSecurity<br /><br /> SMS_AntimalwareSettings.ReadDefault|  
|19|524288|Site.Import Machine<br /><br /> Collection.Deploy Antimalware Settings|  
|20|1048576|SequencePackage.Create<br /><br /> Task Sequence Media<br /><br /> SMS_DistributionPointGroup.Associate<br /><br /> SMS_BoundaryGroup.AssociateSiteSystem<br /><br /> SMS_SettingsDefinition.ModifyPolicy<br /><br /> Collection.Deploy Applications|  
|21|2097152|Collection.Modify Collection Settings<br /><br /> Site.ModifyConnectorPolicy<br /><br /> SMS_AntimalwareSettings.ModifyDefault|  
|22|4194304|Site.Manage OSD Certificate<br /><br /> MigrationJob.Manage<br /><br /> MigrationSiteMapping.SpecifySourceHierarchy<br /><br /> Collection.Deploy Configuration Items|  
|23|8388608|StateMigration.Recover User State<br /><br /> Collection.Deploy Task Sequences|  
|24|16777216|Collection.Manage BMC|  
|25|33554432|Collection.View BMC|  
|26|67108864|AISoftwareList.Manage AI<br /><br /> Collection.Deploy Software Updates|  
|27|134217728|AISoftwareList.View AI<br /><br /> Collection.Deploy Firewall Policies|  
|28|268435456|RunReport|  
|29|536870912|ModifyReport|  

 `IsTypeWideOperation`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true`, if the operation is type wide.  

 If the operation is type wide, the user will have the permission against all objects of this type, if the user has this operation against any RBA security category. If the operation is not type wide, then user will have the permission against the objects which are assigned to the related RBA security category.  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Type ID of the object.  

 `OperationName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [sizelimit("256")]  

 Name of the operation.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
