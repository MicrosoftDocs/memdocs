---
description: Learn how to take two collections as arguments and verify that no circular dependencies form using VerifyNoCircularDependencies.
title: VerifyNoCircularDependencies Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 233501a5-2b33-4394-8732-e77e46331871
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# VerifyNoCircularDependencies Method in Class SMS_Collection
In Configuration Manager, the `VerifyNoCircularDependencies` Windows Management Instrumentation (WMI) class method takes two collections as arguments and verifies that no circular dependencies would be formed if one collection were the parent of another.  

 The following syntax is simplified from Managed Object Format (MOF) code and is intended to show the definition of the method.  

## Syntax  

```  
sint32 VerifyNoCircularDependencies(  
        SMS_Collection ref parentCollection,   
        SMS_Collection ref subCollection,   
        boolean Result);  

```  

#### Parameters  
 `parentCollection`  
 Data type: `ref:SMS_Collection`  

 Qualifiers: [in]  

 Reference to an [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) object path for the parent collection.  

 `subCollection`  
 Data type: `ref:SMS_Collection`  

 Qualifiers: [in]  

 Reference to an [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) object path for the child collection.  

 `Result`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 true if there are no circular dependencies, false if there are circular dependencies.  

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
