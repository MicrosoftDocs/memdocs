---
title: "AddMemberships Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: f4ffae17-c05e-409f-84c5-f3919664fa60
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# AddMemberships Method in Class SMS_SecuredCategoryMembership
The `AddMemberships` Windows Management Instrumentation (WMI) class method, in Configuration Manager, is a batch operation to assign objects to security categories.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AddMemberships(  
     String ObjectIDs[],  
     UInt32 ObjectTypeIDs[],  
     String CategoryIDs[],  
);  
```  

#### Parameters  
 `ObjectIDs`  
 Data type: `String` Array  

 Qualifiers: [in]  

 Array of object IDs.  

 `ObjectTypeIDs`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 Array of object type ids.  

 `CategoryIDs`  
 Data type: `String` Array  

 Qualifiers: [in]  

 The security category IDs which the objects will be assigned to.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SecuredCategoryMembership Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_securedcategorymembership-server-wmi-class.md)
