---
title: GetSiteID Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the GetSiteID WMI class method gets the unique ID of the installed Configuration Manager site.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 9e36aa9b-b824-4ea1-9d70-db562f46d212
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetSiteID Method in Class SMS_Identification
The `GetSiteID` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the unique ID of the installed Configuration Manager site.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetSiteID(  
   String SiteID  
);  
```  

#### Parameters  
 `SiteID`  
 Data type: `String`  

 Qualifiers: [out]  

 Site ID of the Configuration Manager site.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Identification Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md)
