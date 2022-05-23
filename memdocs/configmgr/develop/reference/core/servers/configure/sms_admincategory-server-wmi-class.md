---
description: Learn how to represent an association between the admin account and an RBA secured category in Configuration Manager using SMS_AdminCategory.
title: "SMS_AdminCategory Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: faf9793b-abb7-4a69-8277-5b7190dc435e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_AdminCategory Server WMI Class
The `SMS_AdminCategory` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an association between the admin account and an RBA secured category.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AdminCategory : SMS_BaseClass  
{  
    UInt32 AdminID;  
    String CategoryID;  
};  
```  

## Methods  
 The `SMS_AdminCategory` class does not define any methods.  

## Properties  
 `AdminID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the associated account.  

 `CategoryID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the associated RBA secured category.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
