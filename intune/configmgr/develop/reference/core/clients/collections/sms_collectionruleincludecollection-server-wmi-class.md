---
title: SMS_CollectionRuleIncludeCollection Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that represents an inclusion rule that's added as a rule to the `SMS_Collection` instance.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 27193c49-d811-4f93-b119-f2faf39fffea
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CollectionRuleIncludeCollection Server WMI Class
The `SMS_CollectionRuleIncludeCollection` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an inclusion rule that's added as a rule to the `SMS_Collection` instance. Any members of a collection defined by this rule will be included in the collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ CollectionRuleIncludeCollection : SMS_BaseClass  
{  
      String IncludeCollectionID;  
      String RuleName;  
};  
```  

## Methods  
 The `SMS_ CollectionRuleIncludeCollection` class doesn't define any methods.  

## Properties  
 `IncludeCollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The ID of the collection to include in the membership results.  

 `RuleName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CollectionRule Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionrule-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Abstract  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
