---
title: "SMS_CollectionRuleIncludeCollection Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 27193c49-d811-4f93-b119-f2faf39fffea
searchScope:
 - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_CollectionRuleIncludeCollection Server WMI Class
The `SMS_CollectionRuleIncludeCollection` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, represents an inclusion rule that is added as a rule to the `SMS_Collection` instance. Any members of a collection defined by this rule will be included in the collection.  

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
 The `SMS_ CollectionRuleIncludeCollection` class does not define any methods.  

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

-   Abstract  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Collections Server WMI Classes](../../../../../develop/reference/core/clients/collections/collections-server-wmi-classes.md)
