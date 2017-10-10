---
title: "SMS_RbacSecuredObject Class"
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
ms.assetid: 5e6e53ef-623c-479d-91d3-35b5710a0541searchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_RbacSecuredObject Server WMI Class
The `SMS_RbacSecuredObject` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the RBAC Security Object.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_RbacSecuredObject : SMS_BaseClass  
{  
    UInt32 AvailableInstanceOperations;  
    UInt32 AvailableTypeOperations;  
    UInt32 GrantedOperations;  
    UInt32 ObjectTypeID;  
    String ObjectTypeName;  
    SMS_Operation Operations[];  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_RbacSecuredObject` class.  

|Method|Description|  
|------------|-----------------|  
|[UserHasPermissions Method in Class SMS_RbacSecuredObject](../../../../../develop/reference/core/servers/configure/userhaspermissions-method-in-class-sms_rbacsecuredobject.md)|Returns `true` if the current user has all the requested rights to the given object.|  
|[GetCollectionsWithResourcePermissions Method in Class SMS_RbacSecuredObject](../../../../../develop/reference/core/servers/configure/getcollectionswithresourcepermissions-method-in-class-sms_rbacsecuredobject.md)|Retrieves the collections that the given resource is a member of and the requested permissions.|  
|[GetAvailableScopes Method in Class SMS_RbacSecuredObject](../../../../../develop/reference/core/servers/configure/getavailablescopes-method-in-class-sms_rbacsecuredobject.md)|Returns the secured scopes which current user has all the specified roles associated.|  
|[GetUserList Method in Class SMS_RbacSecuredObject](../../../../../develop/reference/core/servers/configure/getuserlist-method-in-class-sms_rbacsecuredobject.md)|Returns the secured scopes which current user has all the specified roles associated.|  

## Properties  
 `AvailableInstanceOperations`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Available instance level permissions. Detail at Operations.  

 `AvailableTypeOperations`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Available permissions. Detail at Operations.  

 `GrantedOperations`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The operations which are granted to the current user for this type of object.  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The type of object.  

 `ObjectTypeName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [sizelimit(“256��?)]  

 Name of the object type.  

 `Operations`  
 Data type: `SMS_Operation` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The list of operations which belong to this type.   

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Role Based Administration Server WMI Classes](../../../../../develop/reference/core/servers/configure/role-based-administration-server-wmi-classes.md)
