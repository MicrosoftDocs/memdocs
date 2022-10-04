---
title: SMS_TaskSequence_SoftwareConditionExpression Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that represents a condition expression to verify if a specified product is installed on the destination computer.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: c7881ad7-e3c8-4c67-ae69-2f8615343f5f
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_TaskSequence_SoftwareConditionExpression Server WMI Class
The `SMS_TaskSequence_SoftwareConditionExpression` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a condition expression to verify if a specified product is installed on the destination computer. If the software exists, the action is run; otherwise it is not run.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_SoftwareConditionExpression : SMS_TaskSequence_ConditionExpression  
{  
      String Operator;  
      String ProductCode;  
      String ProductName;  
      String UpgradeCode;  
      String Version  
};  
```  

## Methods  
 The `SMS_TaskSequence_SoftwareConditionExpression` class does not define any methods.  

## Properties  
 `Operator`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 The condition operator to use for the comparison. Possible values are:  

- AnyVersion  

- ThisVersion  

  `ProductCode`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: [Not_Null]  

  The Windows Installer package product code to be compared.  

  `ProductName`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: None  

  The product name.  

  `UpgradeCode`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: None  

  The upgrade code for the product to be compared.  

  `Version`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: None  

  The version of the software.

## Remarks  
 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Using this condition, you can do the following:  

 Check for the existence of a specific product.  

- `Operator` should be ThisVersion.  

- `ProductCode` should the product code.  

  Check for existence of a product family.  

- `Operator` should be AnyVersion  

- `UpgradeCode` should be the upgrade code.  

  Either the product code or upgrade code must be specified, otherwise an error will occur.  

  The software on the destination computer must be installed using a Windows Installer package for this expression to work. In usage, the class properties are obtained from the Windows Installer package of the software that is to be compared against. For more information, see [Windows Installer](/windows/desktop/Msi/windows-installer-portal).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
