---
title: SMS_ClientActionStatus Class
titleSuffix: Configuration Manager
description: An SMS Provider server class, in Configuration Manager, that summarize the status of a client action.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: ecd42432-ceb8-4d0d-9445-3fc6752eedef
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ClientActionStatus Server WMI Class
The `SMS_ClientActionStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that summarize the status of a client action.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientActionStatus : SMS_BaseClass  
{  
    UInt32 ActionID;  
    UInt32 ActionState;  
    UInt32 ActionType;  
    String ActionUniqueID;  
    UInt32 CompletedClients;  
    UInt32 FailedClients;  
    UInt32 OfflineClients;  
    UInt32 OperationID;  
    String OperationUniqueID;  
    UInt32 State;  
    DateTime TimeLastUpdated;  
    UInt32 TotalClients;  
    UInt32 UnknownClients;  
};  
```  

## Methods  
 The `SMS_ClientActionStatus` class does not define any methods.  

## Properties  
 `ActionID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier for the client action.  

 `ActionState`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 State of the client action.  Possible values are:  

| Value | Action state |  
| ----- | ------------ |  
|0|Inactive|  
|1|Active|  
|2|Decommission|  

 `ActionType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Action type. Possible values are:  

| Value | Action type |  
| ----- | ----------- |  
|1|Full Scan|  
|2|Quick Scan|  
|3|Download Definition|  
|4|Evaluate Software Update|  
|5|Exclude Scan Path|  
|6|Override Default Action|  
|7|Restore Quarantine Items|  
|8|Request Policy Now|  

 `ActionUniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Unique identifier for the client action.  

 `CompletedClients`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients returned completed result.  

 `FailedClients`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients returned failed result.  

 `OfflineClients`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients which are always offline when the client operation is performed.  

 `OperationID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier of the client operation.  

 `OperationUniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Unique identifier of the client operation.  

 `State`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Client operation state.   

 `TimeLastUpdated`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Last update time of the client operation.  

 `TotalClients`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of all clients targeted with this client action.  

 `UnknownClients`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients that have not yet reported any result.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
