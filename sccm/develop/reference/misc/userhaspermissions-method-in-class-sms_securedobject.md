---
title: "UserHasPermissions Method"
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
ms.assetid: c2742668-beeb-4993-81bb-698db57512a6searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# UserHasPermissions Method in Class SMS_SecuredObject
The `UserHasPermissions` Windows Management Instrumentation (WMI) class method, in Configuration Manager, determines whether the current user has the requested permissions for the specified object.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
Boolean UserHasPermissions(  
     ref:SMS_BaseClass ObjectPath,  
     UInt32 Permissions,  
);  
```  

#### Parameters  
 `ObjectPath`  
 Data type: `ref:SMS_BaseClass`  

 Qualifiers: [in]  

 Object being checked for access permissions, which can be a class name or instance path.  

 `Permissions`  
 Data type: `UInt32`  

 Qualifiers: [in,out]  

 The permission the user has on the object specified by `ObjectPath`.  

 Possible values are defined by the properties of [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md).  

## Return Values  
 Returns a `Boolean` data type that is `true` if the user has permissions.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md)   
 [GetCollectionsWithResourcePermissions Method in Class SMS_SecuredObject](../../../develop/reference/misc/getcollectionswithresourcepermissions-method-in-class-sms_securedobject.md)   
 [RefreshNTGroupMembership Method in Class SMS_SecuredObject](../../../develop/reference/misc/refreshntgroupmembership-method-in-class-sms_securedobject.md)
