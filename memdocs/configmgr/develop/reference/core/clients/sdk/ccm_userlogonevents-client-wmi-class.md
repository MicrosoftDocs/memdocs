---
title: CCM_UserLogonEvents Class
titleSuffix: Configuration Manager
description: A client class that represents a user logon event.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: e22cf0ef-08c1-41e7-9627-e3e19b15b664
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CCM_UserLogonEvents Client WMI Class
The `CCM_UserLogonEvents` Client WMI class is a client class, in Configuration Manager, that represents a user logon event.  

 The following syntax is simplified from the Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
class CCM_UserLogonEvents  
{  
    UInt64 LogoffTime;  
    UInt64 LogonTime;  
    String UserSID;  
};  

```  

## Methods  
 The `CCM_UserLogonEvents` class does not define any methods.  

## Properties  
 `LogoffTime`  
 Data type: `UInt64`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of seconds elapsed since midnight (00:00:00), January 1, 1970, Coordinated Universal Time (UTC).  

 `LogonTime`  
 Data type: `UInt64`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The number of seconds elapsed since midnight (00:00:00), January 1, 1970, Coordinated Universal Time (UTC).  

 `UserSID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The SID of the user.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  
