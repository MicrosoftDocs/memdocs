---
title: "GetCollectionsWithResourcePermissions Method"
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
ms.assetid: 815a36d8-7681-4a33-921f-69268b0663afsearchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetCollectionsWithResourcePermissions Method in Class SMS_RbacSecuredObject
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

 Unique ID, supplied by System Center Configuration Manager, for the resource.  

 `Permissions`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Set of user permissions for the collections that contain the resource.  

 `CollectionIDs`  
 Data type: `String` Array  

 Qualifiers: [out]  

 IDs of collections for which the user has the specified permissions.  

## Return Values  
 A `UInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_RbacSecuredObject Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_rbacsecuredobject-server-wmi-class.md)
