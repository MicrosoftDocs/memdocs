---
title: "SMS_WindowsServicingStates Class"
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
ms.assetid: 34c629ca-b0c6-4e58-9c5f-cb03f54759dbsearchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_WindowsServicingStates Server WMI Class
For internal use only.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_WindowsServicingStates : SMS_BaseClass  
{  
    String Branch;  
    String Build;  
    String Name;  
    UInt32 State;  
};  

```  

## Methods  
 The `SMS_WindowsServicingStates` class does not define any methods.  

## Properties  
 `Branch`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 Reserved for internal use.  

 `Build`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 Reserved for internal use.  

 `Name`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Reserved for internal use.  

 `State`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 Reserved for internal use.  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

-   Read (read-only)  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Windows 10 Servicing Server WMI Classes](../../../develop/reference/misc/windows-10-servicing-server-wmi-classes.md)
