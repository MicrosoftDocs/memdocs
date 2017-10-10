---
title: "SMS_DPStatus Class"
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
ms.assetid: 9ed95bb1-02b9-4e49-953a-af312f64cce9searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_DPStatus Server WMI Class
> [!WARNING]
>  This class is obsolete. Use [SMS_ObjectContentInfo Server WMI Class](../../../develop/reference/core/servers/console/sms_objectcontentinfo-server-wmi-class.md) instead.  

 The `SMS_DPStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that shows the distribution status for a given package or application.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DPStatus : SMS_BaseClass  
{  
    UInt32 AppCI;  
    UInt32 Failed;  
    UInt32 Installed;  
    DateTime LastUpdated;  
    String PkgID;  
    UInt32 Retrying;  
    String SoftwareName;  
};  
```  

## Methods  
 The `SMS_DPStatus` class does not define any methods.  

## Properties  
 `AppCI`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of the application configuration items.  

 `Failed`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of the application configuration items that failed to install.  

 `Installed`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of the application configuration items that installed.  

 `LastUpdated`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The last update time.  

 `PkgID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Identifier for the package.  

 `Retrying`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of application configuration items that are retrying.  

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
