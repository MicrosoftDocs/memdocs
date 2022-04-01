---
description: "Learn how to use the CCM_SoftwareBase class to represent the base class for management entities like software updates, applications and more."
title: "CCM_SoftwareBase Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d01a7ab7-5edd-4534-926d-161ec05d813d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# CCM_SoftwareBase Client WMI Class
The `CCM_SoftwareBase` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the base class for management entities like software updates, applications, and so on. This class contains the common properties across these management entities. This class is listed here for completeness and to show the base class properties which derived classes would inherit. Client SDK users will always use the specific derived classes of interest to achieve the functionality.  

> [!IMPORTANT]
>  The software update client side SDK will only return set of updates which are deployed to client from Configuration Manager site server, and are applicable, and are yet to be installed on the client.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_SoftwareBase :    
{  
    UInt32 ContentSize;  
    DateTime Deadline;  
    String Description;  
    UInt32 ErrorCode;  
    UInt32 EstimatedInstallTime;  
    UInt32 EvaluationState;  
    String FullName;  
    String Name;  
    DateTime NextUserScheduledTime;  
    UInt32 PercentComplete;  
    String Publisher;  
    UInt32 Type;  
};  
```  

## Methods  
 The `CCM_SoftwareBase` class does not define any methods.  

## Properties  
 `ContentSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Represents the content size. Populated only if the managed entity has binary content associated with it.  

 `Deadline`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The deadline specified by the administrator to deploy this managed entity on a client computer.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The description of the managed entity.  

 `ErrorCode`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Error code.    

 `EstimatedInstallTime`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 EstimatedInstallTime    

 `EvaluationState`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Software enforcement state, such as downloading content, waiting servicewindow, and so on.  

|Value|Software enforcement state|State description|  
|-|-|-|  
|0|Unknown|No state information is available.|  
|1|Enforced|Application is enforced to desired/resolved state.|  
|2|NotRequired|Application is not required on the client.|  
|3|ApplicationForEnforcement|Application is available for enforcement (install or uninstall based on resolved state). Content may or may not have been downloaded.|  
|4|EnforcementFailed|Application last failed to enforce (install/uninstall).|  
|5|Evaluating|Application is currently waiting for content download to complete. |  
|6|DownloadingContent|Application is currently waiting for content download to complete.|  
|7|WaitingforDependenciesDownload|Application is currently waiting for its dependencies to download.|  
|8|WaitingforServiceWindow|Application is currently waiting for a service window.|  
|9|WaitingforReboot|Application is currently waiting for a previously pending reboot.|  
|10|WaitingToEnforce|Application is currently waiting for serialized enforcement.|  
|11|EnforcingDependencies|Application is currently enforcing dependencies.|  
|12|Enforcing|Application is currently enforcing.|  
|13|SoftRebootPending|Application install/uninstall enforced and a soft reboot is pending.|  
|14|HardRebootPending|Application installed/uninstalled and a hard reboot is pending.|  
|15|PendingUpdate|Update is available but pending installation.|  
|16|EvaluationFailed|Application failed to evaluate.|  
|17|WaitingUserReconnect|Application is currently waiting for an active user session to enforce.|  
|18|WaitingforUserLogoff|Application is currently waiting for all users to logoff.|  
|19|WaitingforUserLogon|Application is currently waiting for a user logon.|  
|20|InProgressWaitingRetry|Application is in progress awaiting retry.|  
|21|WaitingforPresModeOff|Application  is waiting for presentation mode to be switched off.|  
|22|AdvanceDownloadingContent|Application is pre-downloading content (downloading outside of the install job).|  
|23|AdvanceDependenciesDownload|Application is pre-downloading dependent content (downloading outside of the install job).|  
|24|DownloadFailed|Application is download failed (downloading during the install job).|  
|25|AdvanceDownloadFailed|Application is pre-downloading failed (downloading outside of the install job).|  
|26|DownloadSuccess|Download success (downloading during the install job).|  
|27|PostEnforceEvaluation|Post enforce evaluation. |  

 `FullName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The complete name of the managed entity, such as software update, application and so on.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The name of the actual managed entity like software update, application and so on.  

 `NextUserScheduledTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Next scheduled time when end user would like to deploy this managed entity.  

 `PercentComplete`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Percent complete.    

 `Publisher`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The publisher that published the managed entity, such as Microsoft for software updates coming from Windows Updates.  

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
