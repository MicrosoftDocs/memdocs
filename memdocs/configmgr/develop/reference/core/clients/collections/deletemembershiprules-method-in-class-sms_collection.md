---
title: "DeleteMembershipRules Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 2744b35e-fe64-4224-86c1-ba09168f5190
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# DeleteMembershipRules Method in Class SMS_Collection
The `DeleteMembershipRules` Windows Management Instrumentation (WMI) class method, in Configuration Manager, is used to delete multiple membership rules from the collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 DeleteMembershipRules(  
      SMS_CollectionRule collectionRules[]  
);  
```  

#### Parameters  
 `collectionRules`  
 Data type: `SMS_CollectionRule` Array  

 Qualifiers: [in]  

 [SMS_CollectionRule Server WMI Class](sms_collectionrule-server-wmi-class.md) objects to delete.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Collection Server WMI Class](sms_collection-server-wmi-class.md)   
 [SMS_Site Server WMI Class](../../servers/configure/sms_site-server-wmi-class.md)
