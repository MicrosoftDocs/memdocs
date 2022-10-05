---
title: CCM_AppDeploymentType Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that represents an application deployment type.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: bf386bdb-7161-47f8-94c9-3b2613be2354
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CCM_AppDeploymentType Client WMI Class
The `CCM_AppDeploymentType` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an application deployment type.   

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_AppDeploymentType : CCM_SoftwareBase  
{  
    String AllowedActions[];  
    String ApplicabilityState;  
    String ConfigureState;  
    UInt32 ContentSize;  
    DateTime Deadline;  
    Object Dependencies[];  
    String DeploymentReport;  
    String Description;  
    UInt32 ErrorCode;  
    UInt32 EstimatedInstallTime;  
    UInt32 EvaluationState;  
    String FullName;  
    String Id;  
    String InstallState;  
    DateTime LastEvalTime;  
    UInt32 MaxExecuteTime;  
    String Name;  
    DateTime NextUserScheduledTime;  
    UInt32 PercentComplete;  
    String PostInstallAction;  
    String Publisher;  
    Boolean RequiresUserInteraction;  
    String ResolvedState;  
    UInt32 RetriesRemaining;  
    String Revision;  
    String SupersessionState;  
    UInt32 Type;  
};  
```  

## Methods  
 The following table lists the methods in the `CCM_AppDeploymentType` class.  

-   [GetDeploymentTypeForUser Method in Class CCM_AppDeploymentType](../../../../../develop/reference/core/clients/sdk/getdeploymenttypeforuser-method-in-class-ccm_appdeploymenttype.md)  

-   [GetProperty Method in Class CCM_AppDeploymentType](../../../../../develop/reference/core/clients/sdk/getproperty-method-in-class-ccm_appdeploymenttype.md)  

-   [GetTargetedUsers Method in Class CCM_AppDeploymentType](../../../../../develop/reference/core/clients/sdk/gettargetedusers-method-in-class-ccm_appdeploymenttype.md)  

## Properties  
 `AllowedActions`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 Allowed actions.    

 `ApplicabilityState`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [values]  

 Applicability state. Possible values are:    

|Value|
|-|  
|Unknown|  
|Applicable|  
|NotApplicable|  

 `ConfigureState`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [values]  

 Configure state.    

 `ContentSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Content size.    

 `Deadline`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Deadline.    

 `Dependencies`  
 Data type: `Object Array`  

 Access type: Read/Write  

 Qualifiers: none  

 Dependencies.    

 `DeploymentReport`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Deployment report.    

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Deployment type description.    

 `ErrorCode`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Error code.    

 `EstimatedInstallTime`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Estimated installation time.   

 `EvaluationState`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Evaluation state.    

 `FullName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Full name.    

 `Id`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier.    

 `InstallState`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [values]  

 Installation state. Possible values are:    

|Value|
|-|  
|NotInstalled|  
|Unknown|  
|Error|  
|Installed|  
|NotEvaluated|  
|NotUpdated|  

 `LastEvalTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Last evaluation time.    

 `MaxExecuteTime`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Maximum execution time.    

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name.    

 `NextUserScheduledTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Next user scheduled time.    

 `PercentComplete`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Percent complete.    

 `PostInstallAction`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [values]  

 Post installation action. Possible values are:   

|Value|
|-|  
|NoAction|  
|BasedOnExitCode|  
|ProgramReboot|  
|ForceReboot|  
|ForceLogOff|  

 `Publisher`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Publisher.    

 `RequiresUserInteraction`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Requires user interaction.    

 `ResolvedState`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [values]  

 Resolved state. Possible values are:    

|Value|
|-|  
|None|  
|NotInstalled|  
|Installed|  
|Unknown|  

 `RetriesRemaining`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Retries remaining.    

 `Revision`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Revision.    

 `SupersessionState`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [values]  

 Supersession state. Possible values are:    

|Value|
|-|  
|Unknown|  
|None|  
|Superseded|  
|Superseding|  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Type.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
