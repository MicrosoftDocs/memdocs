---
title: SMS_PolicyAgentConfig class
titleSuffix: Configuration Manager
description: Details of the SMS_PolicyAgentConfig server WMI class
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 56f1a21f-3f6d-47b9-924a-ebb47ff49bd5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# SMS_PolicyAgentConfig server WMI class

The `SMS_PolicyAgentConfig` WMI class is an SMS Provider server class in Configuration Manager. It represents how the client policy system is configured. These settings affect which policies are retrieved, when and how often they're retrieved, and how the client policy processing component takes action on policy updates.  

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```MOF
Class SMS_PolicyAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    String PolicyDownloadMethod;  
    Boolean PolicyEnableUserAuthForAllUserPolicies;  
    Boolean PolicyEnableUserGroupSupport;  
    Boolean PolicyEnableUserPolicyOnInternet;  
    Boolean PolicyEnableUserPolicyOnTS;  
    Boolean PolicyEnableUserPolicyPolling;  
    UInt32 PolicyRequestAssignmentTimeout;  
    UInt32 PolicyTimeDelayBeforeUserPolicyRefreshAtLogonOrUnlock;  
    UInt32 PolicyTimeUntilAck;  
    UInt32 PolicyTimeUntilExpire;  
    UInt32 PolicyTimeUntilUpdateActualConfig;  
};  
```  

## Methods

The `SMS_PolicyAgentConfig` class doesn't define any methods.  

## Properties

### `AgentID`

Data type: `UInt32`  

Access type: Read-only  

Qualifiers: [key, read]  

Identifies the client agent component. The policy agent ID is 13.  

### `PolicyDownloadMethod`

Data type: `String`  

Access type: Read/Write  

Qualifiers: none  

Method used by the policy agent to download policy files. Possible values are listed below. This value can only be NULL if PolicyRequestTarget is NULL. This value shouldn't be changed.  

|Value|Policy download method|  
|-|-|  
|FILECOPY|Copy policy files using standard file copy operations. Policy paths must be local or Universal Naming Convention (UNC) file paths. This value is intended for testing only.|  
|HTTP|Download policy files synchronously by using direct HTTP. Policy paths must be HTTP URLs.|  
|BITS|Drizzle policy files asynchronously by using the Data Transfer Service. Policy paths must be HTTP URLs.|  

### `PolicyEnableUserAuthForAllUserPolicies`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` when the policy agent requests policies specific for users on the computer and enforces user authentication with the management point.  

### `PolicyEnableUserGroupSupport`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` if the Policy Agent sends user group information when requesting a user policy.  

### `PolicyEnableUserPolicyOnInternet`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` to enable user policy requests from internet clients.  

### `PolicyEnableUserPolicyOnTS`

<!--3556025-->
Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

Set to `true` to enable user policy on a terminal server, such as Azure Virtual Desktop. User policy is disabled by default on these devices to help client performance. If you enable this property, you accept any potential performance impact to these devices.

If PolicyEnableUserPolicyPolling is false, this property is ignored.

### `PolicyEnableUserPolicyPolling`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: none  

`true` to enable user policy polling.  

### `PolicyRequestAssignmentTimeout`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: none  

Timeout for the policy request assignment.  

### `PolicyTimeDelayBeforeUserPolicyRefreshAtLogonOrUnlock`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: none  

The amount of time in milliseconds before the policy agent automatically retrieves new user policies after the user signs in or unlocks the desktop.  

### `PolicyTimeUntilAck`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: none  

The time that must elapse before the policy is acknowledged.  

### `PolicyTimeUntilExpire`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: none  

The number of days that the policy agent should wait since it last received a ReplyAssignments message from the authority before removing its policy. At half this time, the policy agent begins requesting acknowledgments. If this value is NULL, the policy never expires.  

### `PolicyTimeUntilUpdateActualConfig`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: none  

The time that must elapse before the actual configuration is updated.  

## Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../../core/reqs/server-runtime-requirements.md).  

## Development requirements

For more information, see [Configuration Manager server development requirements](../../../../core/reqs/server-development-requirements.md).
