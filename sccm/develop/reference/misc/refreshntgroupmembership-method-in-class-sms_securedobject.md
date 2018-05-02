---
title: "RefreshNTGroupMembership Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: b3971d0d-0cf8-4778-a564-812d767eb3b1
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# RefreshNTGroupMembership Method in Class SMS_SecuredObject
The `RefreshNTGroupMembership` Windows Management Instrumentation (WMI) class method, in Configuration Manager, refreshes the information that is stored about the user's Windows NT group membership.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 RefreshNTGroupMembership(  
    String GroupMembership[]  
);  
```  

#### Parameters  
 `GroupMembership`  
 Data type: `String`  

 Qualifiers: [out]  

 List of Windows NT group memberships for the user.  

## Return Values  
 A `UInt32` data type.  

## Remarks  
 The provider typically caches information about the current user's membership in Windows user groups and refreshes the user's membership information approximately every 10 minutes. Calling this method causes the provider to refresh this information.  

## Example Code  
 The following example shows how to call the `RefreshNTGroupMembership` method to refresh the Windows NT group membership list.  

```  
Dim Security As SWbemObject  
Dim Groups() As Variant  
Set Security = GetObject("winmgmts:root\sms\site_<sitecode>:SMS_SecuredObject")  
Security.RefreshNTGroupMembership Groups  
```  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SecuredObject](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md)   
 [GetCollectionsWithResourcePermissions Method in Class SMS_SecuredObject](../../../develop/reference/misc/getcollectionswithresourcepermissions-method-in-class-sms_securedobject.md)   
 [UserHasPermissions Method in Class SMS_SecuredObject](../../../develop/reference/misc/userhaspermissions-method-in-class-sms_securedobject.md)
