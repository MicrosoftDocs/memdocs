---
title: "SMS_EndpointProtectionAgentConfig Class"
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
ms.assetid: 6c5c8c61-9afc-481e-a288-04352a1e0614searchScope: - ConfigMgr SDK
caps.latest.revision: 13
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_EndpointProtectionAgentConfig Server WMI Class
The `SMS_EndpointProtectionAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies the settings for the Endpoint Protection client.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_EndpointProtectionAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    Boolean DisableFirstSignatureUpdate;  
    Boolean EnableBlueProvider;  
    Boolean EnableEP;  
    UInt32 ForceRebootPeriod;  
    UInt32 InstallRetryPeriod;  
    Boolean InstallSCEPClient;  
    Boolean LicenseAgreed;  
    Boolean OverrideMaintenanceWindow;  
    Boolean PersistInstallation;  
    UInt32 PolicyEnforcePeriod;  
    Boolean Remove3rdParty;  
    Boolean SuppressReboot;  
};  
```  

## Methods  
 The `SMS_EndpointProtectionAgentConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Endpoint Protection Agent ID is 20.  

 `DisableFirstSignatureUpdate`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Disable the first signature update on client from a remote source (Windows Update, WSUS, or UNC Path).  

 `EnableBlueProvider`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the Windows R2 provider is enabled. This value is not visible/available in the console. The default value is `true`.  

 `EnableEP`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the agent is enabled.  

 `ForceRebootPeriod`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Pending reboot window in hours.  

 `InstallRetryPeriod`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Client-side verify common client existence interval.  

 `InstallSCEPClient`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the client agent will install the common client.  

 `LicenseAgreed`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the Endpoint Protection License Agreement is approved.  

 `OverrideMaintenanceWindow`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if maintenance windows should not be respected.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `PersistInstallation`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if. EndPoint Protection should be installed on persisted storage. This only applied to embedded operating systems.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `PolicyEnforcePeriod`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Client-side enforce anti-malware policy interval.  

 `Remove3rdParty`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Remove existing 3rd party anti-malware solution when the Endpoint Protection client installs.  

 `SuppressReboot`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Suppress potential reboot after Endpoint Protection client installation.  

## Remarks  
 Enabling the Endpoint Protection client may uninstall existing antivirus solutions.  The Endpoint Protection client cannot be enabled until an Endpoint Protection role is added to the hierarchy.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
