---
title: "SMS_DPGroupInfo Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 9e558edd-a5c6-44db-9283-e4edff42dcb6searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_DPGroupInfo Server WMI Class
The `SMS_DPGroupInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that describes a distribution point group.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DPGroupInfo : SMS_BaseClass  
{  
    UInt32 AssignedContentCount;  
    String Description;  
    UInt32 FeatureType;  
    String GroupID;  
    UInt32 MembersCount;  
    String Name;  
    UInt32 NumberErrors;  
    UInt32 NumberInProgress;  
    UInt32 NumberSuccess;  
    UInt32 NumberUnknown;  
};  
```  

## Methods  
 The `SMS_DPGroupInfo` class does not define any methods.  

## Properties  
 `AssignedContentCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of the packages or applications targeted to this distribution point group.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description for this distribution point group.  

 `FeatureType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Deployment type for monitoring.  

 `GroupID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique identifier for the distribution point group.  

 `MembersCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of the distribution point members.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the distribution point group.  

 `NumberErrors`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of the number of packages or applications with failed to be distributed to this distribution point.  

 `NumberInProgress`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of the number of packages or applications being distributed to this distribution point.  

 `NumberSuccess`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of the number of packages or applications successfully distributed to this distribution point group.  

 `NumberUnknown`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of the number of packages or applications that are in an unknown state.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Content Server WMI Classes](../../../../../develop/reference/core/servers/configure/content-server-wmi-classes.md)
