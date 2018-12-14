---
title: "SMS_CategoryInstanceBase Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 9981a2ee-d1aa-46c0-8043-ebfaa8c82cd7
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_CategoryInstanceBase Server WMI Class
The `SMS_CategoryInstanceBase` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that serves as an abstract base class for the [SMS_CategoryInstance Server WMI Class](../../../develop/reference/compliance/sms_categoryinstance-server-wmi-class.md) and [SMS_UpdateCategoryInstance Server WMI Class](../../../develop/reference/sum/sms_updatecategoryinstance-server-wmi-class.md) classes.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CategoryInstanceBase : SMS_BaseClass  
{  
      String CategoryInstance_UniqueID;  
      UInt32 CategoryInstanceID;  
      String CategoryTypeName;  
      String LocalizedCategoryInstanceName;  
      SMS_Category_LocalizedProperties LocalizedInformation[];  
      UInt32 LocalizedPropertyLocaleID;  
      UInt32 ParentCategoryInstanceID;  
      String SourceSite;  
};  
```  

## Methods  
 The `SMS_CategoryInstanceBase` class does not define any methods.  

## Properties  
 `CategoryInstance_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique, SizeLimit("512")  

 Unique ID of the category instance. This ID is unique across sites. The string length can be up to 512 characters.  

 `CategoryInstanceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 ID of the category instance. This ID is not unique across sites.  

 `CategoryTypeName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The type of category represented by the category instance. Possible values are:  

- Product  

- Locale  

- Classification  

- Company  

- Product Family  

- User  

  `LocalizedCategoryInstanceName`  
  Data type: `String`  

  Access type: Read-only  

  Qualifiers: [read]  

  The localized name of the category instance.  

  `LocalizedInformation`  
  Data type: `SMS_Category_LocalizedProperties` Array  

  Access type: Read/Write  

  Qualifiers: [lazy]  

  Localized properties associated with the category instance.  

  `LocalizedPropertyLocaleID`  
  Data type: `UInt32`  

  Access type: Read-only  

  Qualifiers: [read]  

  ID of the locale applying to the localized properties.  

  `ParentCategoryInstanceID`  
  Data type: `UInt32`  

  Access type: Read-only  

  Qualifiers: [read]  

  ID of the parent for the category instance.  

  `SourceSite`  
  Data type: `String`  

  Access type: Read-only  

  Qualifiers: [read]  

  The site code for the site where the category instance is created.  

## Remarks  
 Class qualifiers for this class include:  

- Abstract  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)
