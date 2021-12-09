---
title: "SMS_SoftwareUpdatesAgentConfig Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: efb91a02-0377-479d-ae95-a135ff57e901
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SoftwareUpdatesAgentConfig Server WMI Class
The `SMS_SoftwareUpdatesAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the settings and properties used by the software updates client agent.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SoftwareUpdatesAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    String AlternateContentProviders;  
    UInt32 AssignmentBatchingTimeout;  
    String BrandingSubTitle;  
    String BrandingTitle;  
    UInt32 ContentDownloadTimeout;  
    UInt32 ContentLocationTimeout;  
    UInt32 DayReminderInterval;  
    Boolean Enabled;  
    String EvaluationSchedule;  
    UInt32 HourReminderInterval;  
    UInt32 MaxRandomDelayMinutes;  
    UInt32 MaxScanRetryCount;  
    UInt32 PerDPInactivityTimeout;  
    UInt32 ReminderInterval;  
    UInt32 ScanRetryDelay;  
    String ScanSchedule;  
    UInt32 TotalInactivityTimeout;  
    UInt32 UpdateStatusRefreshIntervalDays;  
    Boolean UserExperience;  
    UInt32 UserJobPerDPInactivityTimeout;  
    UInt32 UserJobTotalInactivityTimeout;  
    UInt32 WSUSLocationTimeout;  
    String WSUSScanRetryCodes[];  
    UInt32 WUAMaxRebootsWhenOnInternet;  
    String WUASuccessCodes[];  
};  
```  

## Methods  
 The `SMS_SoftwareUpdatesAgentConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Software Updates Agent ID is 9.  

 `AlternateContentProviders`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 An XML string to set alternate content provider settings.  

 `AssignmentBatchingTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The maximum number of seconds between two or more required deployments before those deployments are considered to be a single batch of deployed updates. The default value is 0 (no batching).  

 `BrandingSubTitle`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is deprecated in Configuration Manager.  

 `BrandingTitle`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is deprecated in Configuration Manager.  

 `ContentDownloadTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates the timeout value for downloading the content.  

 `ContentLocationTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates the timeout value for accessing the content location.  

 `DayReminderInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The day reminder interval. This value is not used by the software updates management feature.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the agent is enabled.  

 `EvaluationSchedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Deployment re-evaluation schedule.  

 `HourReminderInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The hour reminder interval. This value is not used by the software updates management feature.  

 `MaxRandomDelayMinutes`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The maximum interval in minutes added to the available after time to prevent a large number of computers from simultaneously downloading the software. This value is not used by the software updates management feature.  

 `MaxScanRetryCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 When a software update scan returns any error in the array `WSUSScanRetryCodes`, the scan is retried every  `ScanRetryDelay` minutes for  `MaxScanRetryCount` times.  

 `PerDPInactivityTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The time before the agent no longer attempts to communicate with an inactive or non-responsive distribution point. If 0 is specified, the timeout value is configured as 8 hours. The default value is 1 hour.  

 `ReminderInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The reminder interval. This value is not used by the software updates management feature.  

 `ScanRetryDelay`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 When a software update scan returns any error in the array `WSUSScanRetryCodes`, the scan is retried every `ScanRetryDelay` minutes for `MaxScanRetryCount` times.  

 `ScanSchedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Software update scan schedule.  

 `TotalInactivityTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The time before the agent no longer attempts to communicate with an inactive or non-responsive distribution point from all distribution points supplied for system initiated downloads. The agent attempts to communicate with each distribution point supplied for the `PerDPInactivityTimeout` before attempting to communicate with next distribution point supplied.  

 `UpdateStatusRefreshIntervalDays`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 This value is not used by the software updates management client.  

 `UserExperience`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is deprecated in Configuration Manager.  

 `UserJobPerDPInactivityTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The time before the agent no longer attempts to communicate with an inactive or non-responsive distribution point from all distribution points supplied for user initiated downloads. The agent attempts to communicate with each distribution point supplied for the `PerDPInactivityTimeout` before attempting to communicate with next distribution point supplied. The default timeout is one hour.  

 `UserJobTotalInactivityTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The time before the agent no longer attempts to communicate with an inactive or non-responsive distribution point from all distribution points supplied for user initiated downloads. The agent attempts to communicate with each distribution point supplied for the `PerDPInactivityTimeout` before attempting to communicate with next distribution point supplied. The default timeout is one hour.  

 `WSUSLocationTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of seconds before the agent no longer waits to receive a list of Windows Software Update Services servers used to perform a software update scan.  

 `WSUSScanRetryCodes`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 An array of error code values. When a software update scan returns any error in the array `WSUSScanRetryCodes`, the scan is retried every `ScanRetryDelay` minutes for `MaxScanRetryCount` times.  

 `WUAMaxRebootsWhenOnInternet`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is reserved for internal use.  

 `WUASuccessCodes`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is reserved for internal use.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
