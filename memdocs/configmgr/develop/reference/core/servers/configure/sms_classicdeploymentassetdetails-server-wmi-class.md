---
description: Learn how to represent asset level details about classic software distribution deployments using SMS_ClassicDeploymentAssetDetails class.
title: SMS_ClassicDeploymentAssetDetails Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ea789cfb-050d-4901-a79d-2a0df24efaa1
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ClassicDeploymentAssetDetails Server WMI Class
The `SMS_ClassicDeploymentAssetDetails` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents asset level details about classic software distribution deployments.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClassicDeploymentAssetDetails : SMS_BaseClass  
{  
    String CollectionID;  
    String CollectionName;  
    String DeploymentID;  
    UInt32 DeviceID;  
    String DeviceName;  
    Boolean IsMachineAssignedToUser;  
    Boolean IsMachineChangesPersisted;  
    Boolean IsVM;  
    UInt32 MessageID;  
    String PackageID;  
    String PackageName;  
    String ProgramName;  
    String StatusDescription;  
    UInt32 StatusType;  
    DateTime SummarizationTime;  
    String UserName;  
    String VMHostName;  
};  
```  

## Methods  
 The `SMS_ClassicDeploymentAssetDetails` class does not define any methods.  

## Properties  
 `CollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Existing collection to which the advertisement is targeted.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the collection to which the advertisement is advertising.  

 `DeploymentID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 A unique auto-generated key.  

 `DeviceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Resource identifier.  

 `DeviceName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Computer NetBIOS name.  

 `IsMachineAssignedToUser`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the computer is assigned to a user.  

 `IsMachineChangesPersisted`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if changes made to the virtual machine have been persisted.  

 `IsVM`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if this is a virtual machine.  

 `MessageID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Software distribution or software update message ID.  

 `PackageID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 ID for an existing package associated with the advertisement.  

 `PackageName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the advertised package.  

 `ProgramName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The program name of the program related to the package that the advertisement will advertise.  

 `StatusDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Status description.  

 `StatusType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Status type.  

|Value|Status type|  
|-|-|  
|1|Success|  
|2|InProgress|  
|4|Unknown|  
|5|Error|  

 `SummarizationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The last time the summarization task was run for this application or current time in UTC if it is missing.  

 `UserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the user to last log in to this client.  

 `VMHostName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Virtual machine host name.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
