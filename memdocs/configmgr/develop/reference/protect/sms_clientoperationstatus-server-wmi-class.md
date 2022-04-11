---
title: "SMS_ClientOperationStatus Class"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, the SMS_ClientOperationStatus WMI class is an SMS Provider server class that summarizes the client operation."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d24f7db3-271b-46dd-af80-b2362781bf0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ClientOperationStatus Server WMI Class
The `SMS_ClientOperationStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that summarizes the client operation.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientOperationStatus : SMS_BaseClass  
{  
    String CollectionID;  
    UInt32 CompletedClients;  
    String CreatedBy;  
    UInt32 FailedClients;  
    UInt32 ID;  
    UInt32 IsExpired;  
    DateTime LastSummaryTime;  
    UInt32 OfflineClients;  
    String PrimaryActionTargetObjectID;  
    String PrimaryActionTargetObjectName;  
    UInt32 PrimaryActionTargetObjectType;  
    UInt32 PrimaryActionType;  
    UInt32 Priority;  
    DateTime RequestedTime;  
    UInt32 State;  
    String TargetCollectionName;  
    DateTime TimeLastUpdated;  
    UInt32 TotalClients;  
    UInt32 Type;  
    String UniqueID;  
    UInt32 UnknownClients;  
};  
```  

## Methods  
 The `SMS_ClientOperationStatus` class does not define any methods.  

## Properties  
 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Target collection identifier of this operation.  

 `CompletedClients`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients that returned a completed result.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 User who created this operation.  

 `FailedClients`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients that returned a failed result.  

 `ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier for the client operation.  

 `IsExpired`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Whether the client operation is expired.   

 `LastSummaryTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Last summary time of the client operation.  

 `OfflineClients`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients which are always offline when the client operation is performed.  

 `PrimaryActionTargetObjectID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Object ID of the target object of the primary action.  

 `PrimaryActionTargetObjectName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the target object of the primary action.  

 `PrimaryActionTargetObjectType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Target object type of the primary action. Possible values are:  

| Value | Object type |  
| ----- | ----------- |  
|1|Threat|  
|8|RequestPolicyNow|  

 `PrimaryActionType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 "Action type of the primary action. Possible values are:  

| Value | Action type |  
| ----- | ----------- |  
|1|Full Scan|  
|2|Quick Scan|  
|3|Download Definition|  
|4|Evaluate Software Update|  
|5|Exclude Scan Path|  
|6|Override Default Action|  
|7|Restore Quarantine Items|  

 `Priority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Operation priority (1 highest, 10 lowest).  

 `RequestedTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Creation time of this operation.  

 `State`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 State of this EndPoint Protection client operation. Possible values are:  

| Value | State |  
| ----- | ----- |  
|0|Action Unknown|  
|1|Action Not Applicable|  
|2|Action Failed|  
|3|Action Succeeded|  

 `TargetCollectionName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Target collection name of this operation.  

 `TimeLastUpdated`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Latest update time of this client operation.  

 `TotalClients`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of all clients targeted with this client action.  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Operation type.   

 `UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Unique identifier for this client operation.  

 `UnknownClients`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients that have not yet reported any result.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
