---
description: Learn how to use SMS_SoftwareConversionRules to describe rules to convert the company or product name resource string into a standard name.
title: SMS_SoftwareConversionRules Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: b7b38ebe-43cf-496a-8cec-0fbef9b99ef9
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SoftwareConversionRules Server WMI Class
The `SMS_SoftwareConversionRules` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that describes the rules to convert the company or product name resource string into a standard name for software inventory. For example, different Microsoft products might contain variations of the Microsoft company name, for example, "Microsoft Corporation" or "Microsoft."  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SoftwareConversionRules : SMS_BaseClass  
{  
     String ConvertType;  
     String NewName;  
     String OriginalName;  
     UInt32 RuleId;   
};  
```  

## Methods  
 The `SMS_SoftwareConversionRules` class does not define any methods.  

## Properties  
 `ConvertType`  
 Data type: **String**  

 Access type: Read/Write  

 Type of resource string to convert. Possible values are:  

- Manufacturer (default)  

- Product  

  `NewName`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: [Not_Null]  

  Name reported to software inventory. The default value is "".  

  `OriginalName`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: [Not_Null]  

  Original company or product name. The default value is "".  

  The original name can contain SQL wildcard characters (&, _, [], and [^]), but the `OriginalName` and `ConvertType`combination must be unique.  

  `RuleId`  
  Data type: **UInt32**  

  Access type: Read-only  

  Qualifiers: [key, read, Not_Null]  

  Unique ID of the rule. The default value is 0.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
