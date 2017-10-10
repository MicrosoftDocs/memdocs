---
title: "GetCollectionsWithResourcePermissions Method"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 31656a08-313b-4a42-a53c-6d9c97050fdfsearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetCollectionsWithResourcePermissions Method in Class SMS_SecuredObject
The `GetCollectionsWithResourcePermissions` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the list of collection identifiers for which the user has the specified permissions. The collection must contain the specified resource.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 GetCollectionsWithResourcePermissions(  
     UInt32 ResourceID,  
     UInt32 Permissions,  
     String CollectionIDs[]  
);  
```  

#### Parameters  
 `ResourceID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Unique ID, supplied by Configuration Manager, for the resource.  

 `Permissions`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Set of user permissions for the collections that contain the resource.  

 `CollectionIDs`  
 Data type: `String` Array  

 Qualifiers: [out]  

 IDs of collections for which the user has the specified permissions.  

## Return Values  
 A `UInt32` data type.  

## Example Code  
 The following example shows how to call the `GetCollectionsWithResourcePermissions` method to get the list of collections that contain the resource to which the user has permissions to delete resources.  

```  
Dim Security As SWbemObject  
Dim Collections() As Variant  
Set Security = GetObject("winmgmts:root\sms\site_<sitecode>:SMS_SecuredObject")  
Security.GetCollectionsWithResourcePermissions <resourceid>, 512, Collections  
```  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SecuredObject](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md)   
 [UserHasPermissions Method in Class SMS_SecuredObject](../../../develop/reference/misc/userhaspermissions-method-in-class-sms_securedobject.md)
