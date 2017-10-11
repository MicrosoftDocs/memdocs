---
title: "SMS_MDMDeviceCategory Class"
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
ms.assetid: 2369dea2-a365-48d8-8450-1629059f8fa9searchScope: - ConfigMgr SDK
caps.latest.revision: 3
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_MDMDeviceCategory Server WMI Class
The `SMS_MDMDeviceCategory` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an On-premises Mobile Device Management (MDM) device category.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MDMDeviceCategory : SMS_BaseClass  
{  
    String CategoryID;  
    String Name;  
};  

```  

## Methods  
 The `SMS_MDMDeviceCategory` class does not define any methods.  

## Properties  
 `CategoryID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key]  

 Category ID.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Category name.  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Mobile Device Management Server WMI Classes](../../../develop/reference/mdm/mobile-device-management-server-wmi-classes.md)   
 [Configuration Manager Hybrid Server WMI Classes](../../../develop/reference/mdm/hybrid-server-wmi-classes.md)
