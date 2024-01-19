---
title: SMS_CIAllCategories Class
titleSuffix: Configuration Manager
description: Lists all SMS_CategoryInstance Server WMI Class or SMS_UpdateCategoryInstance Server WMI Class object instances for a given SMS_ConfigurationItem object.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 57b6120e-a157-4bd4-8b52-8ebc31b4b41f
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CIAllCategories Server WMI Class
The `SMS_CIAllCategories` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that lists all of the SMS_CategoryInstance Server WMI Class or [SMS_UpdateCategoryInstance Server WMI Class](../../../develop/reference/sum/sms_updatecategoryinstance-server-wmi-class.md) object instances for a given SMS_ConfigurationItem object.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CIAllCategories : SMS_BaseClass  
{  
    UInt32 CategoryInstanceID;  
    String CategoryInstance_UniqueID;  
    String CategoryTypeName;  
    UInt32 CI_ID;  
    String CI_UniqueID;  
    String LocalizedCategoryInstanceName;  
    UInt32 LocalizedPropertyLocaleID;  
    String ModelName;  
    UInt32 ObjectTypeID;  
};  
```  

## Methods  
 The `SMS_CIAllCategories` class does not define any methods.  

## Properties  
 `CategoryInstanceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read, Not_null]  

 Configuration Manager-generated, site-specific ID for the category instance. This ID is defined by the `CategoryInstanceID` property of SMS_CategoryInstanceBase Server WMI Class for the specific configuration item.  

 `CategoryInstance_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique, SizeLimit("512")]  

 The unique ID for the category instance. This string can have a maximum of 512 characters. This ID is defined by the `CategoryInstance_UniqueID` property of SMS_CategoryInstanceBase Server WMI Class for the specific configuration item.  

 `CategoryTypeName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md).  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read, Not_null]  

 The unique ID of the configuration item. This ID is unique only for the site. The ID is defined by the `CI_ID` property of SMS_ConfigurationItemBaseClass Server WMI Class for the specific configuration item.  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LocalizedCategoryInstanceName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LocalizedPropertyLocaleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `ModelName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class is applicable to all types of configuration items, not just software updates. For a discussion of configuration item types, see the `CIType_ID` property of SMS_ConfigurationItemBaseClass Server WMI Class.  

  Use this class to query for all categories associated with a configuration item, or all configuration items associated with a category.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_UpdateCategoryInstance Server WMI Class](../../../develop/reference/sum/sms_updatecategoryinstance-server-wmi-class.md)   
 [About software update deployments](../../sum/about-software-updates-deployments.md)
