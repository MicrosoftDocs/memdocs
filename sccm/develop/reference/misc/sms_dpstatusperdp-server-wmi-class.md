---
title: "SMS_DPStatusPerDP Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: 00d2b5d3-1b24-4d22-91ce-a5238931f95fsearchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_DPStatusPerDP Server WMI Class
> [!WARNING]
>  This class is obsolete. Use [SMS_DPStatusInfo Server WMI Class](../../../develop/reference/core/servers/configure/sms_dpstatusinfo-server-wmi-class.md) instead.  

 The `SMS_DPStatusPerDP` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents distribution point status per distribution point.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DPStatusPerDP : SMS_BaseClass  
{  
    String DPName;  
    UInt32 Failed;  
    UInt32 Installed;  
    DateTime LastUpdated;  
    UInt32 Retrying;  
    String SoftwareName;  
};  
```  

## Methods  
 The `SMS_DPStatusPerDP` class does not define any methods.  

## Properties  
 `DPName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Name of the distribution point.  

 `Failed`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of the failed package or application installations.  

 `Installed`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of the installed package or application installations.  

 `LastUpdated`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Time  status was last updated.  

 `Retrying`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of the retrying package or application installations.  

 `SoftwareName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Name of the software.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Content Server WMI Classes](../../../develop/reference/core/servers/configure/content-server-wmi-classes.md)
