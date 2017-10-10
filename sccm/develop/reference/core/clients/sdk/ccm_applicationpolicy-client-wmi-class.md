---
title: "CCM_ApplicationPolicy Class"
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
ms.assetid: b068007e-ee61-47ce-841d-d1f534b5aaffsearchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CCM_ApplicationPolicy Client WMI Class
The `CCM_ApplicationPolicy` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents application policy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_ApplicationPolicy : CCM_SoftwareBase  
{  
    String ApplicabilityState;  
    CCM_Application Apps[];  
    String ConfigureState;  
    UInt32 ContentSize;  
    String CurrentState;  
    DateTime Deadline;  
    String DeploymentReport;  
    String Description;  
    UInt32 ErrorCode;  
    UInt32 EstimatedInstallTime;  
    UInt32 EvaluationState;  
    String FullName;  
    String Id;  
    Boolean IsMachineTarget;  
    Boolean IsPreflightOnly;  
    DateTime LastEvalTime;  
    String Name;  
    DateTime NextUserScheduledTime;  
    UInt32 PercentComplete;  
    String ProgressState;  
    String Publisher;  
    String ResolvedState;  
    String Revision;  
    DateTime StartTime;  
    UInt32 Type;  
};  
```  

## Methods  
 The following table lists the methods in the `CCM_ApplicationPolicy` class.  

-   [EvaluateAllPolicies Method in Class CCM_ApplicationPolicy](../../../../../develop/reference/core/clients/sdk/evaluateallpolicies-method-in-class-ccm_applicationpolicy.md)  

-   [EvaluateAppPolicy Method in Class CCM_ApplicationPolicy](../../../../../develop/reference/core/clients/sdk/evaluateapppolicy-method-in-class-ccm_applicationpolicy.md)  

-   [GetEvaluationState Method in Class CCM_ApplicationPolicy](../../../../../develop/reference/core/clients/sdk/getevaluationstate-method-in-class-ccm_applicationpolicy.md)  

## Properties  
 `ApplicabilityState`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [values]  

 Applicability state. Possible values are:   

||  
|-|  
|Unknown|  
|Applicable|  
|Not Applicable|  

 `Apps`  
 Data type: `CCM_Application` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Applications.    

 `ConfigureState`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [values]  

 Configure state. Possible values are:    

||  
|-|  
|NotNeeded|  
|NotConfigured|  
|Configured|  

 `ContentSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Content size.    

 `CurrentState`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [values]  

 Current state. Possible values are:    

||  
|-|  
|NotInstalled|  
|Unknown|  
|Error|  
|Installed|  
|NotEvaluated|  
|NotUpdated|  
|NotConfigured|  

 `Deadline`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Deadline.    

 `DeploymentReport`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Deployment report.    

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description.    

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

 EvaluationState    

 `FullName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 FullName    

 `Id`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier.    

 `IsMachineTarget`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [key]  

 `true` if this is a client targeted application.    

 `IsPreflightOnly`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if this is a simulated deployment.    

 `LastEvalTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Last evaluation time.    

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

 `ProgressState`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [values]  

 Progress state. Possible values are:    

||  
|-|  
|Idle|  
|EvaluationStarted|  
|DownloadingDocuments|  
|Evaluating|  
|EvaluationFailure|  
|Reporting|  

 `Publisher`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Publisher.    

 `ResolvedState`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [values]  

 Resolved state. Possible values are:    

||  
|-|  
|None|  
|NotInstalled|  
|Installed|  
|Unknown|  

 `Revision`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Revision.    

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Start time.    

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

## See Also  
 [Configuration Manager Client SDK WMI Classes](../../../../../develop/reference/core/clients/sdk/client-sdk-wmi-classes.md)
