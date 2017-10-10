---
title: "SMS_UserClassPermissionNames Class"
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
ms.assetid: 1fda87a6-197e-47d5-930c-0fa1f756f2e1searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_UserClassPermissionNames Server WMI Class
The `SMS_UserClassPermissionNames` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that lists all the users and the permissions granted to each user for each secured class.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UserClassPermissionNames : SMS_BaseClass  
{  
      UInt32 ObjectKey;  
      UInt32 Permission;  
      String PermissionName;  
      String UserName;  
};  
```  

## Methods  
 The `SMS_UserClassPermissionNames` class does not define any methods.  

## Properties  
 `ObjectKey`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 Numeric key that describes the type of secured object being specified. See the `ObjectKey` property of [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md).  

 `Permission`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Access permission for the class. The default value is 0.  

 There is a separate instance of `SMS_UserClassPermissionNames` for each right granted to a user.  

 `PermissionName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Text description of the permission, for example, Read. The default value is "".  

 `UserName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Name of the user, including the domain name. The default value is "".  

## Remarks  
 The class is read-only.  

 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_UserClassPermissions Server WMI Class](../../../develop/reference/misc/sms_userclasspermissions-server-wmi-class.md)
