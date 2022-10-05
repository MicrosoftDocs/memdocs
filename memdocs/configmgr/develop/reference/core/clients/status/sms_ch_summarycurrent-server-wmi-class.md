---
title: SMS_CH_SummaryCurrent Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_CH_SummaryCurrent Windows Management Instrumentation class is an SMS Provider server class that represents client summary.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 72003aea-633b-47c1-8817-3fca1da8d0a8
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CH_SummaryCurrent Server WMI Class
The `SMS_CH_SummaryCurrent` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents client summary.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CH_SummaryCurrent : SMS_BaseClass  
{  
    UInt32 ClientsActive;  
    UInt32 ClientsHealthUnknown;  
    UInt32 ClientsHealthy;  
    UInt32 ClientsHealthyActive;  
    UInt32 ClientsHealthyInactive;  
    UInt32 ClientsInactive;  
    UInt32 ClientsRemediationSuccess;  
    UInt32 ClientsRemediationTotal;  
    UInt32 ClientsTotal;  
    UInt32 ClientsUnhealthy;  
    UInt32 ClientsUnhealthyActive;  
    UInt32 ClientsUnhealthyInactive;  
    String CollectionID;  
};  
```  

## Methods  
 The `SMS_CH_SummaryCurrent` class does not define any methods.  

## Properties  
 `ClientsActive`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of active clients.  

 `ClientsHealthUnknown`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of healthy unknown clients.  

 `ClientsHealthy`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of healthy clients.  

 `ClientsHealthyActive`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of health and active clients.  

 `ClientsHealthyInactive`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of healthy and inactive clients.  

 `ClientsInactive`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of inactive clients.  

 `ClientsRemediationSuccess`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of successfully remediated clients.  

 `ClientsRemediationTotal`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Total count of remediated clients (successful and unsuccessful).  

 `ClientsTotal`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients.  

 `ClientsUnhealthy`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of unhealthy clients.  

 `ClientsUnhealthyActive`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of unhealthy and active clients.  

 `ClientsUnhealthyInactive`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of unhealthy and inactive clients.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique auto-generated ID containing eight characters that identifies the collection.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
