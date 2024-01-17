---
description: Learn how to get the list of users who have been granted permission to this object with the GetUserList method.
title: GetUserList Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 817f73f8-0573-41a5-92a4-b2a18fdfa1b9
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetUserList Method in Class SMS_RbacSecuredObject
The `GetUserList` Windows Management Instrumentation (WMI) class method, in Configuration Manager, returns the list of users who have been granted permission to this object.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 GetUserList(  
     SMS_BaseClass ref ObjectPath,  
     String UserNames[],  
     Uint32 PermittedOperations[]  
);  
```  

#### Parameters  
 `ObjectPath`  
 Data type: `SMS_BaseClass`  

 Qualifiers: [in]  

 The path of the object.  

 `UserNames`  
 Data type: `String` Array  

 Qualifiers: [out]  

 Logon names of the users.  

 `PermittedOperations`  
 Data type: `UInt32` Array  

 Qualifiers: [out]  

 Granted permissions.  

## Return Values  
 A `UInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_RbacSecuredObject Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_rbacsecuredobject-server-wmi-class.md)
