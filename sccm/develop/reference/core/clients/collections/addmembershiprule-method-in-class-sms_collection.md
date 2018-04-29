---
title: "AddMembershipRule Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 6d32daa3-13ce-4aef-a3da-820c6fbe21e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# AddMembershipRule Method in Class SMS_Collection
The `AddMembershipRule` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, adds a new rule to the `CollectionRules` property of the [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md).  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AddMembershipRule(  
     SMS_CollectionRule collectionRule,  
     UInt32 QueryID  
);  
```  

#### Parameters  
 `collectionRule`  
 Data type: `SMS_CollectionRule`  

 Qualifiers: [in]  

 [SMS_CollectionRule Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionrule-server-wmi-class.md) object to add.  

 `QueryID`  
 Data type: `UInt32`  

 Qualifiers: `[out]`  

 Configuration Manager-generated query ID if the rule is a query rule. If the rule is direct, this ID is 0. Use `QueryID` to modify or delete a query membership rule.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
