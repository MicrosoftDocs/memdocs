---
description: Learn how to specify how client computers retrieve software inventory in Configuration Manager using SMS_SoftwareInventoryAgentConfig.
title: SMS_SoftwareInventoryAgentConfig Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: cd15f059-a89a-4990-8048-b8976237128a
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SoftwareInventoryAgentConfig Server WMI Class
The `SMS_SoftwareInventoryAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies how client computers retrieve software inventory.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SoftwareInventoryAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    String CollectableFileExclude[];  
    String CollectableFileMaxSize[];  
    String CollectableFilePaths[];  
    String CollectableFiles[];  
    String CollectableFileSubdirectories[];  
    Boolean Enabled;  
    String Exclude[];  
    String ExcludeWindirAndSubfolders[];  
    String InventoriableTypes[];  
    String Path[];  
    UInt32 QueryTimeout;  
    UInt32 ReportOptions;  
    UInt32 ReportTimeout;  
    UInt32 ScanInterval;  
    String Schedule;  
    String Subdirectories[];  
};  
```  

## Methods  
 The `SMS_SoftwareInventoryAgentConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Software Updates Agent ID is 2.  

 `CollectableFileExclude`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if encrypted and compressed files are excluded in the file collection settings. The value in the array should be `true` or `false`.  

 `CollectableFileMaxSize`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 Maximum size for all collected files (KB).  

 `CollectableFilePaths`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 The list of file paths to collect.  

 `CollectableFiles`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 The list of files to collect.  

 `CollectableFileSubdirectories`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if files in subfolders are collected in the file collection settings. The value in the array should be `true` or `false`.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the agent is enabled.  

 `Exclude`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if encrypted and compressed files are excluded in the file inventory settings. The value in the array should be `true` or `false`.  

 `ExcludeWindirAndSubfolders`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if files in the Windows folder are excluded in the file inventory settings. The value in the array should be `true` or `false`.  

 `InventoriableTypes`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 The list of file types to inventory.  

 `Path`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 The list of file path to be inventoried in the file inventory settings.  

 `QueryTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The maximum time, in seconds, for querying file information on the client. The default value is 1 week.  

 `ReportOptions`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The reporting details. Possible values are:  

|Value|Report options|  
|-|-|  
|1|Product Only|  
|2|File Only|  
|7|Full Details|  

 `ReportTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Maximum time, in seconds, that the client messaging framework attempts to transmit the report, if the destination endpoint is unreachable. The default value is 1 week.  

 `ScanInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Delay, in milliseconds, to pass to the software inventory provider for the software scan.  

 `Schedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Software inventory and file collection schedule.  

 `Subdirectories`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if files in subfolders are inventoried in the file inventory settings. The value in the array should be `true` or `false`.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
