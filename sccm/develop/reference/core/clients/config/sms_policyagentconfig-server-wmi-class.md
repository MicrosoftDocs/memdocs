---
title: "SMS_PolicyAgentConfig Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 56f1a21f-3f6d-47b9-924a-ebb47ff49bd5
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_PolicyAgentConfig Server WMI Class
The `SMS_PolicyAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents how the client policy system is configured. These settings affect which policies are retrieved, when and how often they are retrieved, and how the client policy processing component takes action on policy updates.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PolicyAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    String PolicyDownloadMethod;  
    Boolean PolicyEnableUserAuthForAllUserPolicies;  
    Boolean PolicyEnableUserGroupSupport;  
    Boolean PolicyEnableUserPolicyOnInternet;  
    Boolean PolicyEnableUserPolicyPolling;  
    UInt32 PolicyRequestAssignmentTimeout;  
    UInt32 PolicyTimeDelayBeforeUserPolicyRefreshAtLogonOrUnlock;  
    UInt32 PolicyTimeUntilAck;  
    UInt32 PolicyTimeUntilExpire;  
    UInt32 PolicyTimeUntilUpdateActualConfig;  
};  
```  

## Methods  
 The `SMS_PolicyAgentConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Policy Agent ID is 13.  

 `PolicyDownloadMethod`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Method used by the Policy Agent to download policy files. Possible values are listed below. This value can only be NULL if PolicyRequestTarget is NULL. This value should not be changed.  

|||  
|-|-|  
|FILECOPY|Copy policy files using standard file copy operations. Policy paths must be local or Universal Naming Convention (UNC) file paths. This value is intended for testing only.|  
|HTTP|Download policy files synchronously by using direct HTTP. Policy paths must be HTTP URLs.|  
|BITS|Drizzle policy files asynchronously by using the Data Transfer Service. Policy paths must be HTTP URLs.|  

 `PolicyEnableUserAuthForAllUserPolicies`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` when the policy agent requests policies specific for users on the computer and enforces user authentication with the management point.  

 `PolicyEnableUserGroupSupport`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the Policy Agent sends user group information when requesting a user policy.  

 `PolicyEnableUserPolicyOnInternet`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to enable user policy requests from internet clients.  

 `PolicyEnableUserPolicyPolling`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to enable user policy polling.  

 `PolicyRequestAssignmentTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Timeout for the policy request assignment.  

 `PolicyTimeDelayBeforeUserPolicyRefreshAtLogonOrUnlock`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The amount of time in milliseconds before the policy agent will automatically retrieve new user policies after unlocking the desktop, or after log on.  

 `PolicyTimeUntilAck`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The time that must elapse before the policy is acknowledged.  

 `PolicyTimeUntilExpire`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of days that the Policy Agent should wait since it last received a ReplyAssignments message from the authority before removing its policy. At half this time, the Policy Agent begins requesting acknowledgments. If this value is NULL, the policy never expires.  

 `PolicyTimeUntilUpdateActualConfig`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The time that must elapse before the actual configuration is updated.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
