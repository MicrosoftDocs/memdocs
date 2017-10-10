---
title: "SMS_MobileDeviceAgentConfig Class"
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
ms.assetid: 9eabac3a-3186-48b2-bd71-482163b7f83csearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_MobileDeviceAgentConfig Server WMI Class
The `SMS_MobileDeviceAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies general settings for mobile devices.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MobileDeviceAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    UInt32 DeviceEnrollmentProfileID;  
    UInt32 EnableDeviceEnrollment;  
    Boolean EnableFileCollection;  
    Boolean EnableHardwareInventory;  
    UInt32 EnableModernDeviceEnrollment;  
    Boolean EnableSoftwareDistribution;  
    Boolean EnableSoftwareInventory;  
    UInt32 FailureRetryCount;  
    String FailureRetryInterval;  
    String FileCollectionExcludeCompressed[];  
    String FileCollectionExcludeEncrypted[];  
    String FileCollectionFilter[];  
    String FileCollectionInterval;  
    String FileCollectionPath[];  
    String FileCollectionSubdirectories[];  
    String HardwareInventoryInterval;  
    UInt32 MDMPollInterval;  
    UInt32 ModernDeviceEnrollmentProfileID;  
    String PollingInterval;  
    String PollServer;  
    String SoftwareInventoryExcludeCompressed[];  
    String SoftwareInventoryExcludeEncrypted[];  
    String SoftwareInventoryFilter[];  
    String SoftwareInventoryInterval;  
    String SoftwareInventoryPath[];  
    String SoftwareInventorySubdirectories[];  
};  
```  

## Methods  
 The `SMS_MobileDeviceAgentConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Mobile Device Agent ID is 12.  

 `DeviceEnrollmentProfileID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Mobile device enrollment profile ID.  

 `EnableDeviceEnrollment`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Allow users to enroll mobile devices.  

 `EnableFileCollection`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to enable file collection.  

 `EnableHardwareInventory`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to enable hardware inventory.  

 `EnableModernDeviceEnrollment`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Enables enrollment for modern devices.  

 `EnableSoftwareDistribution`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to enable software distribution on devices.  

 `EnableSoftwareInventory`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to enable software inventory on devices.  

 `FailureRetryCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 FailureRetryCount description.   

 `FailureRetryInterval`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 FailureRetryInterval.   

 `FileCollectionExcludeCompressed`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 When collecting files, exclude compressed files.  

 `FileCollectionExcludeEncrypted`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 When collecting files, exclude encrypted files.  

 `FileCollectionFilter`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 FileCollectionFilter.   

 `FileCollectionInterval`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 FileCollectionInterval.   

 `FileCollectionPath`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 FileCollectionPath.   

 `FileCollectionSubdirectories`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 FileCollectionSubdirectories.   

 `HardwareInventoryInterval`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 HardwareInventoryInterval.   

 `MDMPollInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Polling interval for mobile device management.  

 `ModernDeviceEnrollmentProfileID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 ID of the enrollment profile that allows users to enroll modern devices.  

 `PollingInterval`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Policy polling interval, in minutes.  

 `PollServer`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 PollServer.   

 `SoftwareInventoryExcludeCompressed`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 When inventorying files, exclude compressed files.  

 `SoftwareInventoryExcludeEncrypted`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 When inventorying files, exclude encrypted files.  

 `SoftwareInventoryFilter`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 SoftwareInventoryFilter.   

 `SoftwareInventoryInterval`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 SoftwareInventoryInterval.   

 `SoftwareInventoryPath`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 SoftwareInventoryPath.   

 `SoftwareInventorySubdirectories`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 SoftwareInventorySubdirectories.   

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
