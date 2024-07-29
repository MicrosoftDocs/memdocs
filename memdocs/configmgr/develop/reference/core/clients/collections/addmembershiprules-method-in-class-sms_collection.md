---
title: AddMembershipRules Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the AddMembershipRules WMI class method adds multiple new rules to the CollectionRules property of the SMS_Collection Server WMI Class object.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 882de2be-1f2f-49e2-b105-37a3b8152002
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# AddMembershipRules Method in Class SMS_Collection
The `AddMembershipRules` (WMI) class method, in Configuration Manager, adds multiple new rules to the `CollectionRules` property of the [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) object.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AddMembershipRules(  
     SMS_CollectionRule collectionRules[],  
     UInt32 QueryIDs[]  
);  
```  

#### Parameters  
 `collectionRules`  
 Data type: `SMS_CollectionRule` Array  

 Qualifiers: [in]  

 [SMS_CollectionRule Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionrule-server-wmi-class.md) objects to add.  

 `QueryIDs`  
 Data type: `UInt32` Array  

 Qualifiers: [out]  

 IDs corresponding to the rules. These are Configuration Manager-generated query IDs for query rules. The IDs for direct rules are set to 0. Use `QueryID` to modify or delete a query membership rule.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 The `AddMembershipRules` method does not validate a query rule, but simply adds it to the rules list. This can create debugging issues when the collection does not contain the intended membership. Your application should always validate the query rule before adding it to the collection rules by using the [ValidateQuery Method in Class SMS_CollectionRuleQuery](../../../../../develop/reference/core/clients/collections/validatequery-method-in-class-sms_collectionrulequery.md).  

 The `AddMembershipRules` method can also be used to modify membership rules. Only query rules can be modified.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see Configuration Manager Server Development Requirements.  

## See Also  
 [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)
