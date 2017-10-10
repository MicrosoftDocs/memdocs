---
title: "SMS_DPGroupDistributionStatus Class"
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
ms.assetid: 72e07914-d83b-48b2-a637-828f3af05f17searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_DPGroupDistributionStatus Server WMI Class
The `SMS_DPGroupDistributionStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that describes distribution information for a given distribution point group.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DPGroupDistributionStatus : SMS_BaseClass  
{  
    UInt32 Assets;  
    UInt32 ContentCount;  
    String GroupID;  
    UInt32 MessageCategory;  
    UInt32 MessageType;  
    DateTime StatusTime;  
};  
```  

## Methods  
 The `SMS_DPGroupDistributionStatus` class does not define any methods.  

## Properties  
 `Assets`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of distribution points.  

 `ContentCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of packages or applications distributed to this distribution point group.  

 `GroupID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique identifier for the distribution point group.  

 `MessageCategory`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Status message category.  

 `MessageType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 See [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md).  

 `StatusTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time, in Universal Coordinated Time (UTC), when the status message was created.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Content Server WMI Classes](../../../../../develop/reference/core/servers/configure/content-server-wmi-classes.md)
