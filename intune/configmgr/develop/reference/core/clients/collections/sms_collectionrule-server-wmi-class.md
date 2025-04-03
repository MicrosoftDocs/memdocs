---
description: Learn how to represent a collection rule using SMS_CollectionRule class in Configuration Manager.
title: SMS_CollectionRule Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 43c23dda-0881-44b0-ac6b-65428b0c68c3
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CollectionRule Server WMI Class
The `SMS_CollectionRule` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a collection rule in a collection and serves as an abstract base class for [SMS_CollectionRuleDirect Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionruledirect-server-wmi-class.md) and [SMS_CollectionRuleQuery Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionrulequery-server-wmi-class.md).  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CollectionRule  
{  
      String RuleName;  
};  
```  

## Methods  
 The `SMS_CollectionRule` class does not define any methods.  

## Properties  
 `RuleName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Descriptive name that identifies the rule. The default value is "".  

## Remarks  
 Class qualifiers for this class include:  

- Abstract  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
