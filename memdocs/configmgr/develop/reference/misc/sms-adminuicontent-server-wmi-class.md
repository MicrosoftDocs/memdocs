---
title: "SMS_AdminUIContent Class"
description: Learn how to use the SMS_AdminUIContent class although it has no defined methods.
titleSuffix: "Configuration Manager"
ms.date: "02/15/2017"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: c4bb10ba-7fad-4307-afc2-b0b4c7db7658
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
descriptions: Learn about the simplified syntax, methods, properties, and requirements of the SMS_AdminUIContent server class.

---
# SMS_AdminUIContent Server WMI Class
For internal use only.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AdminUIContent : SMS_BaseClass
{
    DateTime CreationDate;
    String Data;
    String Name;
};

```  

## Methods  
 The `SMS_AdminUIContent` class does not define any methods.  

## Properties  
 `CreationDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: None  

 Reserved for internal use.  

 `Data`  
 Data type: `String`  

 Access type: Read-only

 Qualifiers: None  

 Reserved for internal use.

 `Name`  
 Data type:  `String`  

 Access type: Read-only  

 Qualifiers: [unique, not_null, key]

 Reserved for internal use.

## Remarks  
  Class qualifiers for this class include:  

- Read  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
