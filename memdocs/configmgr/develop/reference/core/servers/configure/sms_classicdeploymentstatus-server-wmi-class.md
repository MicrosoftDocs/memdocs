---
title: "SMS_ClassicDeploymentStatus Class"
titleSuffix: "Configuration Manager"
description: "The SMS_ClassicDeploymentStatus WMI class is an SMS Provider server class that represents classic software distribution deployment status."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: e20290e5-6bcd-4b77-a4c2-9d72fe420206
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ClassicDeploymentStatus Server WMI Class
The `SMS_ClassicDeploymentStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents classic software distribution deployment status.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClassicDeploymentStatus : SMS_BaseClass  
{  
    UInt32 Assets;  
    String CollectionID;  
    String CollectionName;  
    String DeploymentID;  
    DateTime DeploymentTime;  
    Boolean IsDeviceDeployment;  
    String MessageDescription;  
    UInt32 MessageID;  
    String PackageID;  
    String PackageName;  
    String ProgramName;  
    UInt32 Purpose;  
    UInt32 StatusType;  
    DateTime SummarizationTime;  
};  
```  

## Methods  
 The `SMS_ClassicDeploymentStatus` class does not define any methods.  

## Properties  
 `Assets`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Number of assets related to the status.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

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

 `DeploymentTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The time of the deployment.  

 `IsDeviceDeployment`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if the deployment is for mobile devices.  

 `MessageDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Message description.  

 `MessageID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

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

 `Purpose`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Purpose.   

 `StatusType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Status Type.  

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

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
