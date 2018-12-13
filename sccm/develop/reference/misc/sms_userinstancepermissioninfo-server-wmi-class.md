---
title: "SMS_UserInstancePermissionInfo Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 79cfa07c-c7ca-4bc9-9f2a-00ff01779aaf
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_UserInstancePermissionInfo Server WMI Class
The `SMS_UserInstancePermissionInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents information about a user's instance-level permissions for a secured object.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UserInstancePermissionInfo : SMS_BaseClass  
{  
      String DisplayName;  
      String InstanceKey;  
      UInt32 InstancePermissions;  
      UInt32 ObjectKey;  
      Boolean ReadFlag;  
      String UserName;  
};  
```  

## Methods  
 The `SMS_UserInstancePermissionInfo` class does not define any methods.  

## Properties  
 `DisplayName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 Friendly name of the secured object. The default value is "".  

 `InstanceKey`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Unique ID of the secured object. The default value is "".  

 `InstancePermissions`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Permissions granted to a user for a specific secured object. See the `InstancePermissions` property of [SMS_UserInstancePermissions Server WMI Class](../../../develop/reference/misc/sms_userinstancepermissions-server-wmi-class.md).  

 `ObjectKey`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 Numeric key describing the type of secured object. See the `ObjectKey` property of [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md).  

 `ReadFlag`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: None  

 `true` if the user has read permission to the specified secured object.  

 `UserName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Name of the user, including the domain name. The default value is "".  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md)
