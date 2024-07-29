---
description: Learn how to use Configuration Manager RequestWipe Windows Management Instrumentation (WMI) class method to remove Microsoft Exchange and Configuration Manager software from the mobile device or Exchange ActiveSync device.
title: RequestWipe Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 0035a1ee-f788-4f2d-b122-05f8d390f3c6
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# RequestWipe Method in Class SMS_DeviceMethods
The `RequestWipe` Windows Management Instrumentation (WMI) class method, in Configuration Manager, removes Microsoft Exchange and Configuration Manager software from the mobile device or Exchange ActiveSync device.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RequestWipe(  
   UInt32 ResourceId  
   String EASIdentities[]  
);  
```  

#### Parameters  
 `ResourceId`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 ID of the resource to remove software from.  

 `EASIdentities`  
 Data type: `String` Array  

 Qualifiers: [in]  

 Array of Exchange ActiveSync identities.  

## Return Values  
 An `SInt32`data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## See Also  
 [SMS_DeviceMethods Server WMI Class](../../../develop/reference/mdm/sms_devicemethods-server-wmi-class.md)
