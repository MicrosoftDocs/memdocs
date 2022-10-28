---
description: Learn how to retrieve a list of client editions and whether the DeviceOwner property may be edited using CLientEditions class method.
title: ClientEditions Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 030dee48-575c-40fe-b402-920426271329
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ClientEditions Method in Class SMS_Collection
The `ClientEditions` Windows Management Instrumentation (WMI) class method, in Configuration Manager, retrieves a list of client editions and whether the `DeviceOwner` property may be edited.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ClientEditions(  
     UInt32 ClientEdition[],  
     Boolean Editable[]  
);  
```  

#### Parameters  
 `ClientEdition`  
 Data type: `UInt32` Array  

 Qualifiers: [out]  

 Edition of the client. Possible values are:  

| Value | Client edition |
| ----- | -------------- |
|0|Desktop|  
|1|Windows RT|  
|2|Windows Mobile 6|  
|3|Nokia Symbian|  
|4|Windows Phone|  
|5|Mac|  
|6|Windows CE|  
|7|Windows Embedded|  
|8|iOS|  
|9|iPad|  
|10|iPodTouch|  
|11|Andriod|  
|12|iSocConsumer|  
|13|Unix/Linux|  

 `Editable`  
 Data type: `Boolean` Array  

 Qualifiers: [out]  

 `true` if the `DeviceOwner` property may be edited.  

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
