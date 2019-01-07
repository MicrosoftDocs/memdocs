---
title: "SMS_CollectionRuleQuery Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 66ce9c02-42f9-441b-ae63-0c8862c2bc12
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_CollectionRuleQuery Server WMI Class
The `SMS_CollectionRuleQuery` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents a member of a collection based on the results of a query.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CollectionRuleQuery : SMS_CollectionRule  
{  
      String QueryExpression;  
      UInt32 QueryID;  
      String RuleName;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_CollectionRuleQuery` class.  

|Method|Description|  
|------------|-----------------|  
|[ValidateQuery Method in Class SMS_CollectionRuleQuery](../../../../../develop/reference/core/clients/collections/validatequery-method-in-class-sms_collectionrulequery.md)|Validates the collection rule query.|  

## Properties  
 `QueryExpression`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 WQL SELECT statement having results that are used to populate the collection. The statement must specify a resource class name. The default value is "".  

 Your application can use the `LimitToCollectionID` property to further limit the results. Note that the SMS Provider might alter the text of the query to make it more amenable to collection evaluation.  

 `QueryID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Auto-generated ID that is only useful when deleting a rule.  

 `RuleName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CollectionRule Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionrule-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Collections Server WMI Classes](../../../../../develop/reference/core/clients/collections/collections-server-wmi-classes.md)
