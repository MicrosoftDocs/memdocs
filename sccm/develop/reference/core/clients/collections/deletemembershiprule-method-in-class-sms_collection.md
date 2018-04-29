---
title: "DeleteMembershipRule Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 7efdeb19-a509-454a-af9b-dec12ea9a155
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# DeleteMembershipRule Method in Class SMS_Collection
The `DeleteMembershipRule` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, deletes a membership rule from the collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 DeleteMembershipRule(  
     SMS_CollectionRule collectionRule  
);  
```  

#### Parameters  
 `collectionRule`  
 Data type: `SMS_CollectionRule`  

 Qualifiers: [in]  

 [SMS_CollectionRule Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collectionrule-server-wmi-class.md) object to delete.  

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
