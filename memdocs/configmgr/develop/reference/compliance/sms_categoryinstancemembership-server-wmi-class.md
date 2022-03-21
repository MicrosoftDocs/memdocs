---
title: "SMS_CategoryInstanceMembership Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 5df040f8-ff76-440e-95c4-663be1869b9c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_CategoryInstanceMembership Server WMI Class
The `SMS_CategoryInstanceMembership` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, which represents the relationship between categories and configuration item objects.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CategoryInstanceMembership   
{  
    UInt32 CategoryInstanceID;  
    String ObjectKey;  
    UInt32 ObjectTypeID;  
};  
```  

## Methods  
 The `SMS_CategoryInstanceMembership` class does not define any methods.  

## Properties  
 `CategoryInstanceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md)  

 `ObjectKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, sizelimit]  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 [SMS_ObjectContentInfo Server WMI Class](../../../develop/reference/core/servers/console/sms_objectcontentinfo-server-wmi-class.md)  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
