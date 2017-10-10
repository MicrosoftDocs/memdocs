---
title: "SMS_ObjectToClassPermissions_a Class"
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
ms.assetid: da62ef7d-7f4e-4606-b659-7ad5510598f8searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ObjectToClassPermissions_a Server WMI Class
The `SMS_ObjectToClassPermissions_a` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that relates a secured object with various users that have class permissions on it.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ObjectToClassPermissions_a : SMS_BaseAssociation  
{  
      ref:SMS_UserClassPermissions classPermissions;  
      ref:SMS_SecuredObject object;  
};  
```  

## Properties  
 `classPermissions`  
 Data type: `ref:SMS_UserClassPermissions`  

 Access type: Read  

 Qualifiers: [key]  

 Reference to an [SMS_UserClassPermissions Server WMI Class](../../../develop/reference/misc/sms_userclasspermissions-server-wmi-class.md) object path uniquely identifying the location of the permissions object class instance.  

 `Object`  
 Data type: `ref:SMS_SecuredObject`  

 Access type: Read  

 Qualifiers: [key]  

 Reference to an [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md) object path uniquely identifying the location of the secured object class instance.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

-   Association: ToInstance  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class relates an instance of [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md) with an instance of [SMS_UserClassPermissions Server WMI Class](../../../develop/reference/misc/sms_userclasspermissions-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SecuredObject Server WMI Class](../../../develop/reference/misc/sms_securedobject-server-wmi-class.md)   
 [SMS_UserClassPermissions Server WMI Class](../../../develop/reference/misc/sms_userclasspermissions-server-wmi-class.md)
