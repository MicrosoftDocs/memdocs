---
description: The GetTotalNumResults Windows Management Instrumentation class method gets a count of all members in a collection, including subcollections.
title: GetTotalNumResults Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 2398cf48-ce19-4c12-8008-04501f3f8a11
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetTotalNumResults Method in Class SMS_Collection
The `GetTotalNumResults` Windows Management Instrumentation (WMI) class method gets a count of all members in a collection, including subcollections.  

 The following syntax is simplified from Managed Object Format (MOF) code and is intended to show the definition of the method.  

## Syntax  

```  
SInt32 GetTotalNumResults(  
     ref:SMS_Collection Collection,  
     UInt32 Result  
);  
```  

#### Parameters  
 `Collection`  
 Data type: `ref:SMS_Collection`  

 Qualifiers: [in]  

 Collection ID or object path of the collection. The collection ID is the value of the `CollectionID` property of [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md).  

 `Result`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Number of collection members, including subcollections.  

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
