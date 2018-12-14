---
title: "SMS_ObjectToInstancePermissions_a Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e8f74f9a-352c-419d-82b7-3f78070bebe4
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_ObjectToInstancePermissions_a Server WMI Class
The `SMS_ObjectToInstancePermissions_a` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that relates a secured object with users that have permissions for an instance of the secured object.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ObjectToInstancePermissions_a : SMS_BaseAssociation  
{  
      ref:SMS_UserInstancePermissions instancePermissions;  
      ref:SMS_SecuredObject object;  
};  
```  

## Properties  
 `instancePermissions`  
 Data type: `ref;SMS_UserInstancePermissions`  

 Access type: Read  

 Qualifiers: [key]  

 Reference to an [SMS_UserInstancePermissions Server WMI Class](../../../develop/reference/misc/sms_userinstancepermissions-server-wmi-class.md) object path uniquely identifying the location of the permissions object.  

 `object`  
 Data type: `ref:SMS_SecuredObject`  

 Access type: Read  

 Qualifiers: [key]  

 Reference to an [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md) object path uniquely identifying the location of the secured object.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

- Association: ToInstance  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class relates an instance of [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md) with an instance of [SMS_UserInstancePermissions Server WMI Class](../../../develop/reference/misc/sms_userinstancepermissions-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md)   
 [SMS_UserInstancePermissions Server WMI Class](../../../develop/reference/misc/sms_userinstancepermissions-server-wmi-class.md)
