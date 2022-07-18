---
description: Learn how to create a deployment template available to deploy a software update on the site directly versus using the Configuration Manager console.
title: "SMS_Template Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 29b71ea3-7470-4f58-a3fb-89dbbe98b386
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_Template Server WMI Class
The `SMS_Template` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a deployment template available on the site that you can use instead of the Configuration Manager console deployment wizard to deploy a software update.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Template : SMS_BaseClass  
{  
      String Data;  
      String Description;  
      DateTime LastModifiedDate;  
      String Name;  
      String SchemaGUID;  
      String TemplateUniqueID;  
      UInt32 Type;  
};  
```  

## Methods  
 The `SMS_Template` class does not define any methods.  

## Properties  
 `Data`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy, large]  

 Extended data for the template, in XML format.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 A comment describing the template.  

 `LastModifiedDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: read, not_null  

 The last modified date of the template.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 User-friendly display name for the template.  

 `SchemaGUID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [optional]  

 GUID that references the template schema.  

 `TemplateUniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, not_null]  

 GUID to represent the template. The default value is "".  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Not_null]  

 The type of the template. Currently the only possible value is:  

| Value | Template type |  
| ----- | ------------- |  
|0|SUM_DEPLOYMENT|  

## Remarks  
 Class qualifiers for this class include:  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Use of this class is optional. You can use an `SMS_Template` object instead of the console if required. In this case, the properties are populated for you, and you need to change only the ones that reflect information that has changed since the last software update deployment.  

> [!NOTE]
>  `SMS_Template` objects are not replicated to child sites.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [About software update deployments](../../sum/about-software-updates-deployments.md)
