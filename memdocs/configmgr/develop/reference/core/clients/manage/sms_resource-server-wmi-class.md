---
title: "SMS_Resource Class"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, the SMS_Resource WMI class is an SMS Provider server class that serves as an abstract base class for all discovery resource classes."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d123b9ea-bfde-4b95-9678-7f7820de7635
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_Resource Server WMI Class
The `SMS_Resource` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that serves as an abstract base class for all discovery resource classes, for example, [SMS_R_IPNetwork Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_r_ipnetwork-server-wmi-class.md).  

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

 Configuration Manager-supplied ID that uniquely identifies a Configuration Manager client resource. This ID is not unique across sites. The default value is ''".  

## Remarks  
 Class qualifiers for this class include:  

- Abstract  

- Read:ToSubClass  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ResourceMap Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resourcemap-server-wmi-class.md)
