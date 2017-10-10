---
title: "CreateRelationship Method"
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
ms.assetid: 17717f11-feaa-413c-aeae-948c1492c836searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CreateRelationship Method in Class SMS_UserMachineRelationship
The `CreateRelationship` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, creates a relationship between a user and a device.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 CreateRelationship (  
     uint32 MachineResourceId,  
     string UserAccountName,  
     uint32 SourceId,  
     uint32 TypeId  
);  
```  

#### Parameters  
 `MachineResourceId`  
 Data type: `UInt32`  

 Qualifiers: `[in]`  

 Unique Configuration Manager-supplied identifier for the resource.  

 `UserAccountName`  
 Data type: `String`  

 Qualifiers: `[in]`  

 User account name.  

 `SourceId`  
 Data type: `UInt32`  

 Qualifiers: `[in]`  

 Source object identifier for dependency.  

|||  
|-|-|  
|Software Catalog|The end user enabled the relationship by selecting the option in the AppCatalog Web page.|  
|Administrator|An administrator created the relationship manually in the UI.|  
|User|Unused/deprecated.|  
|Usage Agent|The threshold of activity triggered a relationship to be created.|  
|Device Management|The user/device were tied together during enrollment.|  
|OSD|The user/device were tied together as part of OSD imaging.|  
|Fast Install|The user/device were tied together temporarily to enable an on-demand install from the catalog if no UDA relationship installed before the Install was triggered.|  
|Exchange Server connector|The device was provisioned through EAS.|  

 `TypeId`  
 Data type: `UInt32`  

 Qualifiers: `[in, optional]`  

 Type identifier.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)   
 [Application Model Server WMI Classes](../../../../../develop/reference/apps/application-management-server-wmi-classes.md)
