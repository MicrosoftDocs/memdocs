---
description: Learn how to use the SMS_FeatureExtension class to represent feature extensions.  
title: "SMS_FeatureExtension Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0a40d370-575f-480d-b998-9fd3c8cf7f1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_FeatureExtension Server WMI Class
The `SMS_FeatureExtension` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents feature extensions.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_FeatureExtension : SMS_BaseClass  
{  
    String FeatureId;  
    String Name;  
    String Description;  
    Boolean IsExposed;  
};  

```  

## Methods  
 The `SMS_FeatureExtension` class does not define any methods.  

## Properties  
 `FeatureId`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The feature ID.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The name of the feature extension.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 A description of the feature extension.  

 `IsExposed`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates whether the feature extension is exposed.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
