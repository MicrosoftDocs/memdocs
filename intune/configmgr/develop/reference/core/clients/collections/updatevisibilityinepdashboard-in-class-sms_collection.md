---
title: UpdateVisibilityInEPDashBoard Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the UpdateVisibilityInEPDashBoard Windows Management Instrumentation class method that shows this collection in the Endpoint Protection dashboard.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 1adf0ff2-437e-486d-b548-3470b5246641
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# UpdateVisibilityInEPDashBoard Method in Class SMS_Collection
The `UpdateVisibilityInEPDashBoard` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that shows this collection in the Endpoint Protection dashboard.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 UpdateVisibilityInEPDashBoard   
{  
    [IN]    Boolean Visible  
};  
```  

## Parameters  
 `Visible`  
 Data type: `Boolean`  

 Qualifiers: [id("0"), in]  

 `true` if this collection should show in the Endpoint Protection dashboard.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
