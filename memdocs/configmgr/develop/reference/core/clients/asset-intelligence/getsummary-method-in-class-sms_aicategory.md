---
title: GetSummary Method in Class SMS_AICategory
titleSuffix: Configuration Manager
description: The GetSummary Windows Management Instrumentation class method provides a summary count of all the categories, families, and tags used by Asset Intelligence.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: c912603e-0480-4518-a1df-fd4a9664ea3b
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetSummary Method in Class SMS_AICategory
The `GetSummary` Windows Management Instrumentation (WMI) class method, in Configuration Manager, provides a summary count of all the categories, families, and tags used by Asset Intelligence.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetSummary(      
     UInt32 ValidatedCategory,  
     UInt32 UserDefinedCategory,  
     UInt32 ValidatedFamily,  
     UInt32 UserDefinedFamily,  
     UInt32 UserDefinedTags  
);  
```  

#### Parameters  
 `ValidatedCategory`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Count of Microsoft-defined categories.  

 `UserDefinedCategory`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Count of user-defined categories.  

 `ValidatedFamily`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Count of Microsoft-defined families.  

 `UserDefinedFamily`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Count of user-defined families.  

 `UserDefinedTags`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Count of all tags defined by the user.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_AICategory Server WMI Class](../../../../../develop/reference/core/clients/asset-intelligence/sms_aicategory-server-wmi-class.md)
