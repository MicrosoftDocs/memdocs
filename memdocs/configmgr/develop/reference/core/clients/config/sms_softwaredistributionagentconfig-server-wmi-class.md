---
description: Learn how to specify how client computers deploy software in Configuration Manager using SMS_SoftwareDistributionAgentConfig.
title: SMS_SoftwareDistributionAgentConfig Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: f8102cde-c2ac-4760-b97b-2f11f1624351
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SoftwareDistributionAgentConfig Server WMI Class
The `SMS_SoftwareDistributionAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies how client computers deploy software.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SoftwareDistributionAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    UInt32 CacheContentTimeout;  
    UInt32 CacheSpaceFailureRetryCount;  
    UInt32 CacheSpaceFailureRetryInterval;  
    UInt32 CacheTombstoneContentMinDuration;  
    UInt32 ContentLocationTimeoutInterval;  
    UInt32 ContentLocationTimeoutRetryCount;  
    UInt32 DefaultMaxDuration;  
    Boolean DisplayNewProgramNotification;  
    UInt32 DownloadModificationInterval;  
    UInt32 DownloadRetryInterval;  
    UInt32 ExecutionFailureRetryCount;  
    UInt32 ExecutionFailureRetryErrorCodes[];  
    UInt32 ExecutionFailureRetryInterval;  
    Boolean LockSettings;  
    UInt32 LogoffReturnCodes[];  
    UInt32 NetworkFailureRetryCount;  
    UInt32 NetworkFailureRetryInterval;  
    String NewProgramNotificationUI;  
    Boolean RebootLogoffNotification;  
    UInt32 RebootReturnCodes[];  
    Boolean RunNotification;  
    UInt32 RunNotificationCountdownDuration;  
    UInt32 SuccessReturnCodes[];  
    UInt32 UIContentLocationTimeoutInterval;  
    UInt32 UserPreemptionCountdown;  
    UInt32 UserPreemptionTimeout;  
    UInt32 WhatsNewDuration;  
};  
```  

## Methods  
 The `SMS_SoftwareDistributionAgentConfig` class doesn't define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Software Distribution Agent ID is 6.  

 `CacheContentTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Duration, in seconds, after which content can be deleted from the cache, even when referenced.  

 `CacheSpaceFailureRetryCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of times to retry for non-fatal cache errors (-1 = 4,294,967,295 retries).  

 `CacheSpaceFailureRetryInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Interval, in seconds, between retry attempts for non-fatal cache errors.  

 `CacheTombstoneContentMinDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Minimum duration, in seconds, that content must be kept in the cache. This value doesn't set any extra time for the content to be kept in the cache after being tombstoned.  

 `ContentLocationTimeoutInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Duration, in seconds, after which attempts to locate content should be failed.  

 `ContentLocationTimeoutRetryCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of times a content location request retries after recoverable failures have occurred.  

 `DefaultMaxDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is no longer used by the client.  

 `DisplayNewProgramNotification`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is no longer used by the client.  

 `DownloadModificationInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is no longer used by the client.  

 `DownloadRetryInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is no longer used by the client.  

 `ExecutionFailureRetryCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of times to retry for non-fatal execution errors (-1 = 4,294,967,295 retries).  

 `ExecutionFailureRetryErrorCodes`  
 Data type: `UInt32 Array`  

 Access type: Read/Write  

 Qualifiers: none  

 A list of the default program retry values from the site. If a program fails with one of these exit codes, the program will be retried.

 `ExecutionFailureRetryInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Interval, in seconds, between retry attempts for non-fatal execution errors.  

 `LockSettings`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 true if the site settings are locked and can't be overridden.  

 `LogoffReturnCodes`  
 Data type: `UInt32 Array`  

 Access type: Read/Write  

 Qualifiers: none  

 Array of program return codes that indicate a sign out is required.  

 `NetworkFailureRetryCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of times to retry for non-fatal network errors (-1 = 4,294,967,295 retries).  

 `NetworkFailureRetryInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Interval, in seconds, between retry attempts for non-fatal network errors.  

 `NewProgramNotificationUI`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [valuemap]  

 The console that should be shown when a user double-clicks a new program notification. Possible values are:  

|Value|Definition|  
|----|----|  
|ARP|Add/Remove Programs|  
|RAP|Run Advertised Programs|  

 `RebootLogoffNotification`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is no longer used by the client.  

 `RebootReturnCodes`  
 Data type: `UInt32 Array`  

 Access type: Read/Write  

 Qualifiers: none  

 Array of program return codes that indicate a restart is required.  

 `RunNotification`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is no longer used by the client.  

 `RunNotificationCountdownDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is no longer used by the client.  

 `SuccessReturnCodes`  
 Data type: `UInt32 Array`  

 Access type: Read/Write  

 Qualifiers: none  

 Array of program return codes that indicate success.  

 `UIContentLocationTimeoutInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Duration, in seconds, after which attempts to locate content should be failed.  

 `UserPreemptionCountdown`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Duration, in seconds, of the countdown displayed to the user before preemption.  

 `UserPreemptionTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The duration, in seconds, after which a pending mandatory program will run, if the user doesn't click Run on the Ready to Run dialog for their optional program. This timeout is used so that mandatory programs aren't blocked forever by users not clicking Run on the Download Completed/Ready to Run dialog for optional requests.  

 `WhatsNewDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is no longer used by the client.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
