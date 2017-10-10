---
title: "SMS_NAPSystemInfo Class"
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
ms.assetid: 1601051a-73a6-4ac2-8f03-8d4558f658a0searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_NAPSystemInfo Server WMI Class
The `SMS_NAPSystemInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents Network Access Protection (NAP) related system information.  

> [!NOTE]
>  The logic used to populate `NAPIncapableCount` does not take Windows XP Professional SP2 x64 Edition into consideration. Client computers running this operating system will not appear under this property.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_NAPSystemInfo : SMS_BaseClass  
{  
      UInt32 NAPEnabledCount;  
      UInt32 NAPIncapableCount;  
      UInt32 NAPRestrictedCount;  
      UInt32 NAPUpgradeableCount;  
      UInt32 TotalCount;  
};  
```  

## Methods  
 The `SMS_NAPSystemInfo` class does not define any methods.  

## Properties  
 `NAPEnabledCount`  
 Data type: UInt32  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of NAP-enabled computers. The default value is 0.  

 `NAPIncapableCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of computers not enabled for NAP. The default value is 0.  

 `NAPRestrictedCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of computers restricted from running NAP. The default value is 0.  

 `NAPUpgradeableCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of computers that can be upgraded to NAP. The default value is 0.  

 `TotalCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, key]  

 Total number of computers. The default value is 0.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [NAP Server WMI Classes](../../../develop/reference/misc/nap-server-wmi-classes.md)
