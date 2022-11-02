---
title: SMS_CollectionRuleExcludeCollection Class
description: The SMS_CollectionRuleExcludeCollection class is an SMS Provider server class represents an exclusion rule that is added as a rule to the SMS_Collection instance.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a624418d-40f9-46b8-a079-d6776c2f3132
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CollectionRuleExcludeCollection Server WMI Class
The `SMS_CollectionRuleExcludeCollection` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, represents an exclusion rule which is added as a rule to the `SMS_Collection` instance. Any members of a collection defined by this rule will be excluded from the collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ CollectionRuleExcludeCollection : SMS_BaseClass  
{  
      String ExcludeCollectionID;  
      String RuleName;  
};  
```  

## Methods  
 The `SMS_ CollectionRuleExcludeCollection` class does not define any methods.  

## Properties  
 `ExcludeCollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The ID of the collection to exclude from the membership results.  

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
