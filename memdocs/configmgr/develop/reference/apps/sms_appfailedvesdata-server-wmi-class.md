---
description: The SMS_AppFailedVEsData Windows Management Instrumentation (WMI) class is an SMS Provider server class in Configuration Manager.
title: "SMS_AppFailedVEsData Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 22eb79c4-c169-4a91-a478-78ce2cd7ba27
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# SMS_AppFailedVEsData Server WMI Class

The `SMS_AppFailedVEsData` Windows Management Instrumentation (WMI) class is an SMS Provider server class in Configuration Manager.

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax  

```  
Class SMS_AppFailedVEsData : SMS_BaseClass  
{  
    UInt32 AssignmentID;  
    String AssignmentUniqueID;  
    String CollectionID;  
    UInt32 ComplianceState;  
    UInt32 DTCI;  
    UInt64 DTResultID;  
    UInt32 EnforcementState;  
    UInt32 ErrorValue;  
    String MachineName;  
    String UserName;  
    String VEDisplayName;  
};  
```  

## Methods  
 The `SMS_AppFailedVEsData` class does not define any methods.  

## Properties  
 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 AssignmentID    

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 AssignmentUniqueID    

 `CollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 CollectionID    

 `ComplianceState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 ComplianceState    

 `DTCI`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 DTCI    

 `DTResultID`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 DTResultID    

 `EnforcementState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 EnforcementState    

 `ErrorValue`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 ErrorValue    

 `MachineName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 MachineName    

 `UserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 UserName    

 `VEDisplayName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 VEDisplayName    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
