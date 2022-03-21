---
title: "GetAvailableScopes Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0deba515-ebef-44c8-8059-8480d536f9b3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GetAvailableScopes Method in Class SMS_RbacSecuredObject
The `GetAvailableScopes` Windows Management Instrumentation (WMI) class method, in Configuration Manager, returns the secured scopes, which current user has the permission to grant to other accounts.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 GetAvailableScopes(  
     String RoleIDs[],  
     UInt32 ScopeTypeID,  
     String ScopeIDs[],  
     String ScopeNames[]  
);  
```  

#### Parameters  
 `RoleIDs`  
 Data type: `String` Array  

 Qualifiers: [in]  

 The role ID list which user uses to grant permissions to other accounts.  

 `ScopeTypeID`  
 Data type: `UInt32`  

 Qualifiers: [in, optional]  

 Type of scope, could be RBA security category (29) or collection(1). The default value is 29.  

|Value|Scope type|  
|-|-|  
|1|Collection|  
|29|Secured scope.|  

 `ScopeIDs`  
 Data type: `String` Array  

 Qualifiers: [out]  

 IDs of collections for which the user has the specified permissions.  

 `ScopeNames`  
 Data type: `String` Array  

 Qualifiers: [out]  

 The name of the scopes.  

## Return Values  
 A `UInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
