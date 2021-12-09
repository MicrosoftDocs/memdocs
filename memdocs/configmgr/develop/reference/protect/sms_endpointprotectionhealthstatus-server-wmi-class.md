---
title: "SMS_EndpointProtectionHealthStatus Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: dd7b5aad-be22-4052-bdd4-55c082bf2324
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_EndpointProtectionHealthStatus Server WMI Class
The `SMS_EndpointProtectionHealthStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents health status of Endpoint Protection.   

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_EndpointProtectionHealthStatus : SMS_BaseClass  
{  
    UInt32 ApplyPolicyFailedCount;  
    UInt32 ApplyPolicySucceededCount;  
    String CollectionID;  
    UInt32 InstallFailedCount;  
    UInt32 InstallRebootPendingCount;  
    UInt32 NoSignatureCount;  
    UInt32 OverallNotClientCount;  
    UInt32 OverallStatusAtRiskCount;  
    UInt32 OverallStatusInactiveCount;  
    UInt32 OverallStatusNotSupportedCount;  
    UInt32 OverallStatusNotYetInstalledCount;  
    UInt32 OverallStatusProtectedCount;  
    UInt32 SignaturesOlderThan7DaysCount;  
    UInt32 SignaturesUpTo1DayOldCount;  
    UInt32 SignaturesUpTo3DaysOldCount;  
    UInt32 SignaturesUpTo7DaysOldCount;  
    DateTime TimeLastUpdated;  
    UInt32 TotalMemberCount;  
    UInt32 TotalOperationalIssueCount;  
    UInt32 UnhealthyCount;  
};  
```  

## Methods  
 The `SMS_EndpointProtectionHealthStatus` class does not define any methods.  

## Properties  
 `ApplyPolicyFailedCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients failed to apply policy.  

 `ApplyPolicySucceededCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients succeeded to apply policy.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier of collection summarized.  

 `InstallFailedCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients failed to install the Endpoint Protection client.  

 `InstallRebootPendingCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients pending restart to complete Endpoint Protection client installation.  

 `NoSignatureCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients without definitions.  

 `OverallNotClientCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of non-client members.  

 `OverallStatusAtRiskCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients with deficient status (agent health, malware, signatures, agent deployment).  

 `OverallStatusInactiveCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of inactive clients.  

 `OverallStatusNotSupportedCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients not supported by Endpoint Protection agent.  

 `OverallStatusNotYetInstalledCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients without Endpoint Protection client installed yet.  

 `OverallStatusProtectedCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients with good overall status (agent health, malware, signatures, agent deployment).  

 `SignaturesOlderThan7DaysCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients with definitions that are 7 days old or older.  

 `SignaturesUpTo1DayOldCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients with definitions less than 24 hours old.  

 `SignaturesUpTo3DaysOldCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients with definitions between 1 and 2 days old.  

 `SignaturesUpTo7DaysOldCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients with definitions between 3 and 6 days old.  

 `TimeLastUpdated`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Time the statistics were last updated.

 `TotalMemberCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Total count of members in the collection.  

 `TotalOperationalIssueCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients with any of 5 types of operational issues.   

 `UnhealthyCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of clients with unhealthy agents.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
