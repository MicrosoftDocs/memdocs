---
title: "SMS_UserInstancePermissionNames Class"
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
ms.assetid: 33c8bbff-a969-4e93-bacc-54d0b7d0734csearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_UserInstancePermissionNames Server WMI Class
The `SMS_UserInstancePermissionNames` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that lists all the users and the permissions granted to each user for a secured object.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UserInstancePermissionNames : SMS_BaseClass  
{  
      String InstanceKey;  
      UInt32 ObjectKey;  
      UInt32 Permission;  
      String PermissionName;  
      String UserName;  
};  
```  

## Methods  
 The `SMS_UserInstancePermissionNames` class does not define any methods.  

## Properties  
 `InstanceKey`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Unique ID for a secured object. The ID is the value of the key field for that object. The default value is "".  

 `ObjectKey`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 Numeric key describing the type of secured object. See the `ObjectKey` property of [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md).  

 `Permission`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Access permission for the secured object. The default value is 0.  

 There is a separate instance of `SMS_UserInstancePermissionNames` for each right granted to a user.  

 `PermissionName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Text description of the named permission, for example, Read. The default value is "".  

 `UserName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Name of the user, including the domain name. The default value is "".  

## Remarks  
 This class is read-only.  

 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_UserInstancePermissions Server WMI Class](../../../develop/reference/misc/sms_userinstancepermissions-server-wmi-class.md)   
 [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md)
