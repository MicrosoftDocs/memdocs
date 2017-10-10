---
title: "SMS_AIHardwareRequirements Class"
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
ms.assetid: f158f87a-3607-4a5e-8c2a-2e8da8997c60searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_AIHardwareRequirements Server WMI Class
The `SMS_AIHardwareRequirements` Windows Management Instrumentation (WMI) class, in System Center Configuration Manager, associates a software title with hardware requirements.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AIHardwareRequirements : SMS_BaseClass   
{   
      boolean IsLocal;   
      uint32 MinCPU;   
      sint64 MinDiskFree;   
      sint64 MinDiskSize;   
      sint64 MinRAM;   
      string Product;   
      uint32 State;   
};  
```  

## Methods  
 The following table lists the methods in the `SMS_AIHardwareRequirements` class.  

|Method|Description|  
|------------|-----------------|  
|[GetSummary Method in Class SMS_AIHardwareRequirements](../../../../../develop/reference/core/clients/asset-intelligence/getsummary-method-in-class-sms_aihardwarerequirements.md)|Retrieves a summary of all class instances based on the State property of the class.|  

## Properties  
 `IsLocal`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` when this entry has been created locally. Local entries are editable.  

 `MinCPU`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Minimum CPU in megahertz.  

 `MinDiskFree`  
 Data type: `SInt64`  

 Access type: Read/Write  

 Qualifiers: None  

 Minimum free disk space in KB.  

 `MinDiskSize`  
 Data type: `SInt64`  

 Access type: Read/Write  

 Qualifiers: None  

 Minimum total disk size in KB.  

 `MinRAM`  
 Data type: `SInt64`  

 Access type: Read/Write  

 Qualifiers: None  

 Minimum total RAM in KB.  

 `Product`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: key  

 The software title.  

 `State`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

|Value|Description|  
|-----------|-----------------|  
|0|Validated, defined by Microsoft through System Center Online.|  
|1|User-defined.|  

## Remarks  
 Class qualifiers for this class include:  

-   DisplayName("AI Hardware Requirements")  

-   Dynamic  

-   Provider("ExtnProv")  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Asset Intelligence](../../../../../develop/core/clients/asset-intelligence/asset-intelligence.md)
