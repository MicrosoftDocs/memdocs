---
title: "SMS_ConfigMgrClientAgentConfig Class"
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
ms.assetid: 8f42cb66-ac17-444c-a93c-bd8af273437dsearchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ConfigMgrClientAgentConfig Server WMI Class
The `SMS_ConfigMgrClientAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies the general settings for communication between server and client.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ConfigMgrClientAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    Boolean AddPortalToTrustedSiteList;  
    Boolean AllowPortalToHaveElevatedTrust;  
    UInt32 AgentID;  
    String BrandingTitle;  
    UInt32 DayReminderInterval;  
    Boolean DisplayNewProgramNotification;  
    Boolean EnableHealthAttestation;  
    UInt32 EnableThirdPartyOrchestration;  
    UInt32 GracePeriodHours;  
    UInt32 HourReminderInterval;  
    UInt32 InstallRestriction;  
    String OnPremHAServiceUrl;  
    String OSDBrandingSubTitle;  
    String PortalUrl;  
    UInt32 PowerShellExecutionPolicy;  
    UInt32 ReminderInterval;  
    String SUMBrandingSubTitle;  
    UInt32 SuspendBitLocker;  
    String SWDBrandingSubTitle;  
    UInt32 SystemRestartTurnaroundTime;  
    Boolean UseNewSoftwareCenter;  
    Boolean UseOnPremHAService;  
};  
```  

## Methods  
 The `SMS_ConfigMgrClientAgentConfig` class does not define any methods.  

## Properties  
 `AddPortalToTrustedSiteList`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Add default Application Catalog website to the Internet Explorer trusted sites zone.  

 `AllowPortalToHaveElevatedTrust`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Allow Silverlight applications to run in elevated trust mode.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Configuration Manager Client Agent ID is 4.  

 `BrandingTitle`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Organization name displayed in Software Center.  

 `DayReminderInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Deployment deadline greater than 24 hours, remind user every (hours).  

 `DisplayNewProgramNotification`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if notifications are shown to a user when a new program is made available.  

 `EnableHealthAttestation`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates whether  [Windows 10 Device Health Attestation](https://technet.microsoft.com/itpro/windows/keep-secure/protect-high-value-assets-by-controlling-the-health-of-windows-10-based-devices) is enabled.  

 `EnableThirdPartyOrchestration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Enable third party orchestration.  

 `GracePeriodHours`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of hours in the enforcement grace period.  

 Define an enforcement grace period to give users more time to install required application deployments or software updates beyond any deadlines you configured.  

 `HourReminderInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Deployment deadline less than 24 hours, remind user every (hours).  

 `InstallRestriction`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Install permissions.  

|Possible values|
|----|
|All users|  
|Only administrators|  
|Only administrators and primary users|  
|No users|  

 `OnPremHAServiceUrl`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The URL for the on-premises Health Attestation Service.  

 `OSDBrandingSubTitle`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The operating system deployment branding subtitle.  

 `PortalUrl`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Default Application Catalog website point.  

 `PowerShellExecutionPolicy`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 PowerShell execution policy.  

|Value|Definition|
|----|----|
|0|Bypass|  
|1|Restricted|  

 `ReminderInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Deployment deadline less than 1 hour, remind user every (minutes).  

 `SUMBrandingSubTitle`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The software updates branding subtitle.  

 `SuspendBitLocker`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to disable PIN protector on the system volume if the reboot is initiated by CcmExec (not including the user explicitly rebooting from the reboot UI). After the reboot, the PIN protector is enabled. This enables a computer reboot without user intervention.  

|Value|Definition|
|----|----|
|0|Never disable PIN protection.|  
|1|Always disable PIN protection.|  

 `SWDBrandingSubTitle`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The software distribution branding subtitle.  

 `SystemRestartTurnaroundTime`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The estimated turnaround time for system reboot, in seconds.  

 `UseNewSoftwareCenter`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates whether the updated Software Center is used.  

 `UseOnPremHAService`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates whether the on-premises Health Attestation Service is used.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
