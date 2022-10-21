---
title: SMS_ApplicationManagementAgentConfig Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_ApplicationManagementAgentConfig WMI class is an SMS Provider server class that contains the configuration of Application Management client agent settings.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: b84aafbf-df61-4324-a39f-3b50c4eb14ce
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ApplicationManagementAgentConfig Server WMI Class
The `SMS_ApplicationManagementAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that contains the configuration of Application Management client agent settings.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ApplicationManagementAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    String AlternateContentProviders;  
    Boolean AppXInplaceUpgradeEnabled;  
    Boolean Enabled;  
    String EvaluationSchedule;  
};  
```  

## Methods  
 The `SMS_ApplicationManagementAgentConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Application Management Agent ID is 17.  

 `AlternateContentProviders`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 An XML string to set alternate content provider settings. This property does not apply to a software update package or a driver package.  

```  
<AlternateDownloadSettings SchemaVersion="1.0">    <Provider Name="logical name here">        <Data>provider specific data here</Data>    </Provider>    <Provider Name="logical name here">         <Data>provider specific data here</Data>    </Provider></AlternateDownloadSettings>  
```  

 `AppXInplaceUpgradeEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates whether Windows app package (.appx files)  in-place upgrade is enabled.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the agent is enabled.  

 `EvaluationSchedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Evaluation schedule for deployments.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
