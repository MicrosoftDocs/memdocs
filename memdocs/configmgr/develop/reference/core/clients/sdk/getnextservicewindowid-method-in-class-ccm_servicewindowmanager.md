---
title: GetNextServiceWindowID Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the GetNextServiceWindowID WMI class method gets the identifier of the next service window instance closest to the current time.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0d183452-3798-4ac8-a210-25368c575ddf
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetNextServiceWindowID Method in Class CCM_ServiceWindowManager
The `GetNextServiceWindowID` WMI class method, in Configuration Manager, gets the identifier of the next service window instance closest to the current time.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetNextServiceWindowID(  
     [OUT] String NextServiceWindowID  
);  
```  

#### Parameters  
 `NextServiceWindowID`  
 Data type: `String`  

 Qualifiers: [out]  

 Identifier of the next service window instance closest to the current time.  

## Return Values  
 A `UInt32` data type that is 0 to indicate success or nonzero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [CCM_ServicewindowManager Client WMI Class](../../../../../develop/reference/core/clients/sdk/ccm_servicewindowmanager-client-wmi-class.md)
