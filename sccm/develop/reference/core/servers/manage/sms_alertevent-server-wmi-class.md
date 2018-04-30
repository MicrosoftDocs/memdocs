---
title: "SMS_AlertEvent Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e00ad156-746e-42da-97e1-e4ad0cdaca21
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_AlertEvent Server WMI Class
The `SMS_AlertEvent` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the event data for an alert.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AlertEvent : SMS_BaseClass  
{  
    UInt32 AlertID;  
    DateTime DateClosed;  
    String EventData;  
    UInt32 EventID;  
    String EventInstanceID;  
    UInt64 EventResourceID;  
    DateTime EventTime;  
    Boolean IsClosed;  
    String SiteCode;  
};  
```  

## Methods  
 The `SMS_AlertEvent` class does not define any methods.  

## Properties  
 `AlertID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Identifier of the alert.  

 `DateClosed`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Date on which the event was closed.  

 `EventData`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Additional data about the event in XML format.  

 `EventID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier of the event.  

 `EventInstanceID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Identifies the source of the alert.  

 `EventResourceID`  
 Data type: `UInt64`  

 Access type: Read/Write  

 Qualifiers: none  

 Resource identifier of an associated computer for computer based events. Another identifier for non-computer based alerts.  

 `EventTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The time the alert was raised.  

 `IsClosed`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true`, if this event has been closed.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Site code of the site at which the event was raised.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
