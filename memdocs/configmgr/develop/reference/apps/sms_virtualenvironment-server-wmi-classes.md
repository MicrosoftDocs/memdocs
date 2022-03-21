---
title: "SMS_VirtualEnvironment Classes"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: b6e5fec6-6d2f-442e-8f06-ac9269165a23
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_VirtualEnvironment Server WMI Classes
The `SMS_VirtualEnvironment` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents   

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UserApplicationRequestHistoryItem :    
{  
    boolean IsReadOnly;;  
    SMS_CI_LocalizedProperties LocalizedInformation[];  
    uint32 NumReferringApplications;  
    uint32 NumReferringDeploymentTypes;  
    uint32 ReferringDeploymentTypes[];  
};  
```  

## Methods  
 The `SMS_UserApplicationRequestHistoryItem` class does not define any methods.  

## Properties  
 `IsReadOnly`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Flag to indicate the virtual environment is read-only.  

 `LocalizedInformation`  
 Data type: `SMS_CI_LocalizedProperties` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Localized information.  

 `NumReferringApplications`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [read, not_null]  

 The number of referring applications.  

 `NumReferringDeploymentTypes`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [read, not_null]  

 The number of referring deployment types.  

 `ReferringDeploymentTypes`  
 Data type: `UInt32` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 A list of CI_IDs of the referring deployment types.  

## Remarks  

## Requirements  
 Each time a request is updated, an instance of this class is created to track the history of the request.  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
