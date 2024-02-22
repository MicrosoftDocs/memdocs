---
title: SMS_CN_ClientStatus Class
titleSuffix: Configuration Manager
description: The SMS_CN_ClientStatus Windows Management Instrumentation class is an SMS Provider server class, in Configuration Manager, that represents client notification of agent status.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 3d52902c-630b-4450-8cf5-3f58852c057c
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CN_ClientStatus Server WMI Class
The `SMS_CN_ClientStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents client notification of agent status.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CN_ClientStatus : SMS_BaseClass  
{  
    UInt32 ChannelType;  
    DateTime LastStatusTime;  
    UInt32 OnlineStatus;  
    UInt32 ResourceID;  
    UInt32 ServerID;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_CN_ClientStatus` class.  

|Method|Description|  
|------------|-----------------|  
|[GetOnlineCount Method in Class SMS_CN_ClientStatus](../../../../../develop/reference/core/clients/status/getonlinecount-method-in-class-sms_cn_clientstatus.md)|Gets an online count of the selected clients of the target collection.|  

## Properties  
 `ChannelType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Channel type. Possible values are:  

|Value|Channel type|  
|-|-|  
|0|TCP|  
|1|HTTP|  

 `LastStatusTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Last online time.  

 `OnlineStatus`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Online status. Possible values are:  

|Value|Online status|  
|-|-|  
|0|Offline|  
|1|Online|  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Client resource identifier.  

 `ServerID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Client notification server identifier.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
