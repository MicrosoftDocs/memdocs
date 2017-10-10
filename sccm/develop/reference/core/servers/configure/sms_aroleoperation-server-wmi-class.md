---
title: "SMS_ARoleOperation Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 0631a5e5-4f9c-4e14-b662-684439588b55searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ARoleOperation Server WMI Class
The `SMS_ARoleOperation` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that is embedded by SMS_Role and describes the operation that is granted to this role.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ARoleOperation : SMS_BaseClass  
{  
    UInt32 GrantedOperations;  
    UInt32 ObjectTypeID;  
};  
```  

## Methods  
 The `SMS_ARoleOperation` class does not define any methods.  

## Properties  
 `GrantedOperations`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 A bit mask representing the granted operations. Possible values are:  

||||  
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

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 ID of the object type ID. See `SMS_RbacSecuredObject` for a list of secured object types.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Role Based Administration Server WMI Classes](../../../../../develop/reference/core/servers/configure/role-based-administration-server-wmi-classes.md)
