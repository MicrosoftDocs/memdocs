---
description: Learn how to represent the database link status between the child and parent site for each replication group with SMS_ReplicationLinkStatus.
title: "SMS_ReplicationLinkStatus Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: eb30cf7e-c3dc-4d9f-b70b-453dbf059896
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ReplicationLinkStatus Server WMI Class
The `SMS_ReplicationLinkStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the database link status between the child and parent site for each replication group.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ReplicationLinkStatus : SMS_BaseClass  
{  
    DateTime ChildLastReceived;  
    DateTime ChildLastSent;  
    String ChildSite;  
    UInt32 DegradedSyncs;  
    UInt32 FailedSyncs;  
    UInt32 InitializationPercent;  
    UInt32 InitializationStatus;  
    DateTime ParentLastReceived;  
    DateTime ParentLastSent;  
    String ParentSite;  
    UInt32 RecoveryStatus;  
    String ReplicationGroup;  
    String ReplicationPattern;  
    UInt32 SyncInterval;  
};  
```  

## Methods  
 The `SMS_ReplicationLinkStatus` class does not define any methods.  

## Properties  
 `ChildLastReceived`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The time of last received message for this replication group on the child site.  

 `ChildLastSent`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The time of last message for this replication group sent from the child site.  

 `ChildSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Site code of the child site.  

 `DegradedSyncs`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 If the link status is degraded, this will show the synchronization intervals from the last synchronization finish time.  

 `FailedSyncs`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 If the link status is status is failed, this will show the synchronization intervals from last synchronization finish time.  

 `InitializationPercent`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Re-initialization progress for this replication group.  

 `InitializationStatus`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Re-initialization status.  

 `ParentLastReceived`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Time of the last received message for this replication group on the parent site.  

 `ParentLastSent`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Time of the last message for this replication group sent from the parent site.  

 `ParentSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Site code of the parent site.  

 `RecoveryStatus`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Recovery status.  

 `ReplicationGroup`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Name of the replication group. See [SMS_ReplicationGroup Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_replicationgroup-server-wmi-class.md).  

 `ReplicationPattern`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Replication pattern. See [SMS_ReplicationGroup Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_replicationgroup-server-wmi-class.md).  

 `SyncInterval`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Synchronization interval, in minutes, for the replication group.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
