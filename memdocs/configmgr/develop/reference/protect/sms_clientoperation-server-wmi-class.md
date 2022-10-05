---
title: SMS_ClientOperation Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that represents a set of client actions.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f523822e-1638-42bc-8997-c52ac4d53a82
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ClientOperation Server WMI Class
The `SMS_ClientOperation` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a set of client actions.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientOperation : SMS_BaseClass  
{  
    SMS_ClientAction Actions[];  
    String CollectionID;  
    String CreatedBy;  
    UInt32 DependentClientOperations[];  
    String Filter;  
    UInt32 FilterType;  
    UInt32 ID;  
    Boolean IsActionsDependent;  
    String PrimaryActionTargetObjectID;  
    String PrimaryActionTargetObjectName;  
    UInt32 PrimaryActionTargetObjectType;  
    UInt32 PrimaryActionType;  
    UInt32 Priority;  
    DateTime RequestedTime;  
    String SourceSite;  
    UInt32 State;  
    String TargetCollectionName;  
    UInt32 TargetResourceIDs[];  
    UInt32 TargetType;  
    String UniqueID;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_ClientOperation` class.  

|Method|Description|  
|------------|-----------------|  
|[AllowThreat Method in Class SMS_ClientOperation](../../../develop/reference/protect/allowthreat-method-in-class-sms_clientoperation.md)|Allow the specified threat (identified by ID) to all members in a specific collection.|  
|[CancelClientOperation Method in Class SMS_ClientOperation](../../../develop/reference/protect/cancelclientoperation-method-in-class-sms_clientoperation.md)|Cancels a client operation.|  
|[DeleteClientOperation Method in Class SMS_ClientOperation](../../../develop/reference/protect/deleteclientoperation-method-in-class-sms_clientoperation.md)|Deletes a client operation.|  
|[ExcludeScanPaths Method in Class SMS_ClientOperation](../../../develop/reference/protect/excludescanpaths-method-in-class-sms_clientoperation.md)|Excludes scan paths from all members in specified collection.|  
|[IsClientOperationAllowed Method in Class SMS_ClientOperation](../../../develop/reference/protect/isclientoperationallowed-method-in-class-sms_clientoperation.md)|Checks whether a user has permission to execute an operation.|  
|[IsClientOperationUpdateAllowed Method in Class SMS_ClientOperation](../../../develop/reference/protect/isclientoperationupdateallowed-method-in-class-sms_clientoperation.md)|Checks whether a user has permission to update an operation.|  
|[InitiateClientOperation Method in Class SMS_ClientOperation](../../../develop/reference/protect/initiateclientoperation-method-in-class-sms_clientoperation.md)|Initiates a client operation.|  
|[RestoreQuarantinedItem Method in Class SMS_ClientOperation](../../../develop/reference/protect/restorequarantineditem-method-in-class-sms_clientoperation.md)|Restores quarantined items to all members in a collection infected by specified threat.|  

## Properties  
 `Actions`  
 Data type: `SMS_ClientAction` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 A set of embedded client actions to be executed on target clients.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Target collection identifier of this operation.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 User who created this operation.  

 `DependentClientOperations`  
 Data type: `UInt32 Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Embedded IDs of dependent client operations.  

 `Filter`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Thread identifier filter.  

 `FilterType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Filter type of the target members, applicable only when the `TargetType` is 3. Possible values are:  

| Value | Filter type |  
| ----- | ----------- |  
|0|No filter.|  
|1|Infected by given threat (Filter).|  

 `ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier for this instance.  

 `IsActionsDependent`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the actions within this operation depend on a previous one.  

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
|8|RequestPolicyNow|  

 `Priority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Operation priority (1 Highest, 50 Lowest).  

 `RequestedTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Creation time of this operation.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Side code of the site from which the operation was initiated.  

 `State`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Operation state. Possible values are:  

| Value | Operation state |  
| ----- | --------------- |  
|0|Inactive|  
|1|Active|  
|2|Decommission|  

 `TargetCollectionName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Target collection name of this operation.  

 `TargetResourceIDs`  
 Data type: `UInt32 Array`  

 Access type: Read/Write  

 Qualifiers: none  

 The embedded Resource IDs of target clients.  

 `TargetType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Operation target type. Possible values are:  

| Value | Target type |  
| ----- | ----------- |  
|0|Current members of a specified collection.|  
|1|Specific clients in a specified collection.|  
|2|Members of a specified collection.|  
|3|Members of a specific collection matching specified criteria.|  

 `UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Unique identifier for this instance.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
