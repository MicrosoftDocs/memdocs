---
title: "SMS_Group Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 6fcacb73-c71f-4300-9d29-eaeae91e2532
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_Group Server WMI Class
The `SMS_Group` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents a resource group and serves as the abstract base class for [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md).  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Group : SMS_BaseClass  
{  
     UInt32 ResourceID;  
};  
```  

## Methods  
 The `SMS_Group` class does not define any methods.  

## Properties  
 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 System Center Configuration Manager-supplied ID that uniquely identifies a client resource. The default value is 0. This ID is unique only for the site.  

 Inventory items with the same `ResourceID` property are all found on the same client.  

## Remarks  
 Class qualifiers for this class include:  

- Abstract  

- Read:ToSubClass  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Resource Management Server WMI Classes](../../../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)   
 [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md)
