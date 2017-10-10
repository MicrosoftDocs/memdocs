---
title: "SMS_Resource Class"
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
ms.assetid: d123b9ea-bfde-4b95-9678-7f7820de7635searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_Resource Server WMI Class
The `SMS_Resource` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that serves as an abstract base class for all discovery resource classes, for example, [SMS_R_IPNetwork Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_r_ipnetwork-server-wmi-class.md).  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Resource : SMS_BaseClass  
{  
     UInt32 ResourceID;  
};  
```  

## Methods  
 The `SMS_Resource` class does not define any methods.  

## Properties  
 `ResourceID`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: [key]  

 System Center Configuration Manager-supplied ID that uniquely identifies a System Center Configuration Manager client resource. This ID is not unique across sites. The default value is ''".  

## Remarks  
 Class qualifiers for this class include:  

-   Abstract  

-   Read:ToSubClass  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Resource Management Server WMI Classes](../../../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)   
 [SMS_ResourceMap Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resourcemap-server-wmi-class.md)
