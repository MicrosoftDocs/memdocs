---
title: "SMS_UINAL_ResourceInfo Class"
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
ms.assetid: 01f37e13-395e-4648-af97-525d95bfe7absearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_UINAL_ResourceInfo Server WMI Class
The `SMS_UINAL_ResourceInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents network abstraction layer (NAL) data specific to the Configuration Manager console.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UINAL_ResourceInfo   
{  
     String ChmFile;  
     String ConfigUnit;  
     UInt32 DisplayNameIconID;  
     UInt32 DisplayNameResID;  
     String GUID;  
     String HtmFile;  
     String ResourceDLL;  
     String ResourceType;  
};  
```  

## Methods  
 The `SMS_UINAL_ResourceInfo` class does not define any methods.  

## Properties  
 `ChmFile`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the compressed .chm file for the resource type.  

 `ConfigUnit`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the unit that is being configured.  

 `DisplayNameIconID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Resource ID of the display name icon for the resource type.  

 `DisplayNameResID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Resource ID of the display name for the resource type.  

 `GUID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 GUID representing the Microsoft Management Console node for the property page.  

 `HtmFile`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Help file (.htm) for the property page.  

 `ResourceDLL`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the resource DLL containing the resource strings for `DisplayNameResID` and `DisplayNameIconID`.  

 `ResourceType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Supported resource type.  

## Remarks  
 Class qualifiers for this class include:  

-   Embedded  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class is used in the `ResourceInfo` parameter of [SMS_SIIB_UINALProvider Server WMI Class](../../../develop/reference/misc/sms_siib_uinalprovider-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SIIB_UINALProvider Server WMI Class](../../../develop/reference/misc/sms_siib_uinalprovider-server-wmi-class.md)
