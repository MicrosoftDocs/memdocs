---
title: "SMS_SecuredCategoryMembership Class"
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
ms.assetid: 918f15b3-ce2a-408b-b83f-949e5a4f1369searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SecuredCategoryMembership Server WMI Class
The `SMS_SecuredCategoryMembership` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents object to security category assignment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SecuredCategoryMembership : SMS_BaseClass  
{  
    String CategoryID;  
    String ObjectKey;  
    UInt32 ObjectTypeID;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_SecuredCategoryMembership` class.  

|Method|Description|  
|------------|-----------------|  
|[AddMemberships Method in Class SMS_SecuredCategoryMembership](../../../../../develop/reference/core/servers/configure/addmemberships-method-in-class-sms_securedcategorymembership.md)|Batch operation to assign objects to a security category.|  
|[RemoveMemberships Method in Class SMS_SecuredCategoryMembership](../../../../../develop/reference/core/servers/configure/removememberships-method-in-class-sms_securedcategorymembership.md)|Batch operation to remove objects from a security category|  

## Properties  
 `CategoryID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The ID of security category.  

 `ObjectKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, sizelimit(“256��?)]  

 The key of object.  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The type id of the object. See the `SMS_RbacSecuredObject` class for details.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Role Based Administration Server WMI Classes](../../../../../develop/reference/core/servers/configure/role-based-administration-server-wmi-classes.md)
