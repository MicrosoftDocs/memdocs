---
title: "SMS_SUPSyncStatus Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 2ed724a6-b660-4d71-9580-901814bec745
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SUPSyncStatus Server WMI Class
The `SMS_SUPSyncStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that lists sync and replication status for SUM data for participating site/SUP.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SUPSyncStatus : SMS_BaseClass  
{  
    DateTime LastReplicationLinkCheckTime;  
    DateTime LastSuccessfulSyncTime;  
    UInt32 LastSyncErrorCode;  
    UInt32 LastSyncState;  
    DateTime LastSyncStateTime;  
    UInt32 ReplicationLinkStatus;  
    String SiteCode;  
    UInt32 SyncCatalogVersion;  
    String WSUSServerName;  
    String WSUSSourceServer;  
};  
```  

## Methods  
 The `SMS_SUPSyncStatus` class does not define any methods.  

## Properties  
 `LastReplicationLinkCheckTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last time the replication link status was checked.  

 `LastSuccessfulSyncTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last synchronization success time.  

 `LastSyncErrorCode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Last synchronization error code.  

 `LastSyncState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last synchronization state.  

 `LastSyncStateTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last time the synchronization state was reported.  

 `ReplicationLinkStatus`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Replication link status.  

| Value | Status |  
| ----- | ------ |  
|0|Healthy|  
|1|Degraded|  
|2|Error|  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Site code.  

 `SyncCatalogVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Synchronization catalog version.  

 `WSUSServerName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 WSUS server name.  

 `WSUSSourceServer`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 WSUS source server.  

## Remarks  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [About software update deployments](../../sum/about-software-updates-deployments.md)
