---
title: "SMS_LocalizedNameLookup Class"
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
ms.assetid: 550b49ed-d2f8-4bdf-bac6-26b1c6de9ffdsearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_LocalizedNameLookup Server WMI Class
The `SMS_LocalizedNameLookup` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents a localized name lookup.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_LocalizedNameLookup : SMS_BaseClass  
{  
      String ColumnName;  
      String ResourceDLL;  
      UInt32 ResourceID;  
};  
```  

## Methods  
 The `SMS_LocalizedNameLookup` class does not define any methods.  

## Properties  
 `ColumnName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 English language version of the view column as it appears in the database.  

 `ResourceDLL`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the resource DLL where the localized version of the name appears.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 ID of the string in the resource DLL that contains the localized version of the name.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 The localized name lookup represented by this class is used by Web reports to match an English view column name to a string resource in a resource DLL that contains the localized version of the name. It can be manipulated through the provider so that custom property names and resource DLLs can be defined.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Reporting Server WMI Classes](../../../develop/reference/core/servers/reporting/configuration-manager-reporting-server-wmi-classes.md)
