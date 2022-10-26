---
title: SMS_AmPolicySummary Class
titleSuffix: Configuration Manager
description: The SMS_AmPolicySummary Windows Management Instrumentation class is an SMS Provider server class in Configuration Manager.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: adfce640-adc5-48d7-a723-5be5c9f40206
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_AmPolicySummary Server WMI Class
The `SMS_AmPolicySummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the endpoint protection client antimalware policy status.  

> [!IMPORTANT]
>  This class is only for customized antimalware policy summary.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AmPolicySummary : SMS_BaseClass  
{  
    UInt32 AppliedCount;  
    DateTime AssignmentTime;  
    UInt32 ClientSettingsID;  
    String CollectionID;  
    String CollectionName;  
    UInt32 FailureCount;  
    UInt32 ID;  
    DateTime LastClientUpdateTime;  
    UInt32 NotAppliedCount;  
    UInt32 TotalCount;  
    UInt32 UnknownCount;  
};  
```  

## Methods  
 The `SMS_AmPolicySummary` class does not define any methods.  

## Properties  
 `AppliedCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of clients that applied this particular antimalware policy  

 `AssignmentTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Local time the customized setting is deployed.  

 `ClientSettingsID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Unique identifier of the antimalware setting.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Collection identifier.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Collection name.  

 `FailureCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of clients that failed to apply this particular antimalware policy.  

 `ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier of the antimalware setting assignment.  

 `LastClientUpdateTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Last update from all assigned clients.  

 `NotAppliedCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of clients that are not applicable to apply the policy.  

 `TotalCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Total number of clients assigned the policy.  

 `UnknownCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of unknown clients.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
