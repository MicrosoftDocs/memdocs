---
title: "SMS_G_System_EndpointProtectionStatus Class"
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
ms.assetid: 16d8b116-f852-48fb-9979-5d195397b0c5searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_G_System_EndpointProtectionStatus Server WMI Class
The `SMS_G_System_EndpointProtectionStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents status of Endpoint Protection.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_System_EndpointProtectionStatus : SMS_G_System  
{  
    Boolean AmFullscanRequired;  
    Boolean AmManualStepsRequired;  
    Boolean AmOfflineScanRequired;  
    Boolean AmRecentlyCleaned;  
    Boolean AmRemediationFailed;  
    Boolean AmRestartRequired;  
    Boolean AmThreatActivity;  
    Boolean AtRisk;  
    Boolean EnforcementFailed;  
    Boolean EnforcementSucceeded;  
    Boolean Inactive;  
    Boolean InstallFailed;  
    Boolean NoSignature;  
    Boolean NotClient;  
    Boolean NotYetInstalled;  
    Boolean PendingReboot;  
    Boolean Protected;  
    UInt32 ResourceID;  
    Boolean SignatureOlderThan7Days;  
    Boolean SignatureUpTo1DayOld;  
    Boolean SignatureUpTo3DaysOld;  
    Boolean SignatureUpTo7DaysOld;  
    Boolean Unhealthy;  
    Boolean Unsupported;  
};  
```  

## Methods  
 The `SMS_G_System_EndpointProtectionStatus` class does not define any methods.  

## Properties  
 `AmFullscanRequired`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client is pending a full scan due to threat action.  

 `AmManualStepsRequired`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client is pending manual steps due to threat action.  

 `AmOfflineScanRequired`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client is pending an offline scan due to threat action.  

 `AmRecentlyCleaned`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if a threat was detected and cleaned recently.  

 `AmRemediationFailed`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client failed to remediate the threat.  

 `AmRestartRequired`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client is pending a reboot due to threat action.  

 `AmThreatActivity`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if a threat was detected.  

 `AtRisk`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client has the policy to enable EndPoint Protection, however, the SCEP agent is not successfully installed (or pending a reboot to finish the installation), no signature is installed, the signature is too old, the client is inactive (from client status perspective) or the client failed to apply antimalware policy and so on.  

 `EnforcementFailed`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client failed to apply policy.  

 `EnforcementSucceeded`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client successfully applied policy.  

 `Inactive`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client is inactive.  

 `InstallFailed`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client failed to install the Endpoint Protection client.  

 `NoSignature`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if no signature is installed on this client.  

 `NotClient`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if this is not a Configuration Manager client.  

 `NotYetInstalled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the Endpoint Protection client is not installed.  

 `PendingReboot`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client is pending a restart to complete the Endpoint Protection installation.  

 `Protected`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client is well protected.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Client resource identifier.  

 `SignatureOlderThan7Days`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the signature is older than 7 days.  

 `SignatureUpTo1DayOld`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the signature is up to 1 day old.  

 `SignatureUpTo3DaysOld`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the signature is up from 1 to 3 days old.  

 `SignatureUpTo7DaysOld`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the signature is up from 3 to 7 days old.  

 `Unhealthy`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client is unhealthy from a client status perspective.  

 `Unsupported`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the Endpoint Protection client is not supported on this client platform.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
