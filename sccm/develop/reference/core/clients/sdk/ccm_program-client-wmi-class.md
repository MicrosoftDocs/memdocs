---
title: "CCM_Program Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: 2c024101-cb8e-4185-b3b2-6b9c509f7919searchScope: - ConfigMgr SDK
caps.latest.revision: 24
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CCM_Program Client WMI Class
The `CCM_Program` WMI class is a client class, in Configuration Manager, that represents a legacy software distribution program on the client.  

 The following syntax is simplified from the Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
class CCM_Program : CCM_SoftwareBase  
{  
     Datetime ActivationTime;  
     Boolean AdvertisedDirectly;  
     String Categories[];  
     UInt32 CompletionAction;  
     CCM_Program Dependencies[];  
     String DependentPackageID;  
     String DependentProgramID;  
     String DiskSpaceRequired;  
     UInt32 Duration;  
     Datetime ExpirationTime;  
     Boolean ForceDependencyToRun;  
     Boolean HighImpact;   
     UInt32 LastExitCode;  
     String LastRunStatus;  
     Datetime LastRunTime;  
     UInt32 Level;  
     Boolean NotifyUser;  
     String PackageID;  
     String PackageLanguage;  
     String PackageName;  
     Boolean Published;  
     String ProgramID;  
     String RepeatRunBehavior;  
     Boolean RequiresUserInput;  
     Boolean RunAtLogoff;  
     Boolean RunAtLogon;  
     Boolean RunDependent;   
     Boolean TaskSequence;  
     String Version;  
};  
```  

## Methods  
 The `CCM_Program` class does not define any methods.  

## Properties  
 `ActivationTime`  
 Data type: `Datetime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Date and time the specified software distribution program is activated.  

 `AdvertisedDirectly`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if the specified software distribution program is advertised directly, otherwise, `false`.  

 `Categories[]`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Array of categories associated with the software distribution program.  

 `CompletionAction`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Controls the action Configuration Manager takes after a successful installation. The following table shows the list of possible values.  

|Value|Action|  
|-----------|------------|  
|0|Reboot|  
|1|LogOff|  
|2|ProgramReboot|  
|3|No action|  

 `Dependencies[]`  
 Data type: `CCM_Program`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Array of software distribution program dependencies.  

 `DependentPackageID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Identifier of the package on which the software distribution program depends.  

 `DependentProgramID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Identifier of the program on which the specified software distribution program depends.  

 `DiskSpaceRequired`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Amount of disk space required.  

 `Duration`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Duration time of the software distribution program.  

 `ExpirationTime`  
 Data type: `Datetime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Date and time the specified software distribution program expires.  

 `ForceDependencyToRun`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if the dependent program is forced to run; otherwise, `false.`  

 `HighImpact`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if the specified software distribution program has a high impact, otherwise, `false`.  

 `LastExitCode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Code value of last exit.  

 `LastRunStatus`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Status of the last run software distribution program.  

 `LastRunTime`  
 Data type: `Datetime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Date and time that the software distribution program was last run.  

 `Level`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Level of the specified software distribution program.  

 `NotifyUser`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if notifications for the software distribution program are shown to the user; otherwise, `false`.  

 `PackageID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Identifier of the software distribution package.  

 `PackageLanguage`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Language specified in the software distribution package.  

 `PackageName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Name of the software distribution package.  

 `Published`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if the specified software distribution program is published, otherwise, `false`.  

 `ProgramID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Identifier of the software distribution program.  

 `RepeatRunBehavior`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Response of the client when a software distribution program is run more than once on a computer. The following table shows the list of possible values.  

|Value|Description|  
|-----------|-----------------|  
|RerunAlways|Rerun the program regardless of previous execution condition.|  
|RerunIfFail|Rerun the program if the previous attempt to run failed. If there was no previous attempt, do not run.|  
|RerunIfSuccess|Rerun the program if the previous attempt to run succeeded. If there was no previous attempt, do not run.|  
|RerunNever|Do not rerun the program.|  

 `RequiresUserInput`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if user input is required; otherwise, `false`.  

 `RunAtLogoff`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if the specified software distribution program runs when user logs off, otherwise, `false`.  

 `RunAtLogon`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if the specified software distribution program runs when user logs on, otherwise, `false`.  

 `RunDependent`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if software distribution program is dependent on another program, otherwise, `false`.  

 `TaskSequence`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if the specified software distribution program uses a task sequence, otherwise, `false`.  

 `Version`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Version of the software distribution program.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Configuration Manager Client SDK WMI Classes](../../../../../develop/reference/core/clients/sdk/client-sdk-wmi-classes.md)
