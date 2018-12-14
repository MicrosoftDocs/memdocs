---
title: "CCM_SoftwareUpdate Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: dd1a5ba5-b611-4b28-888f-7918fcd1d869
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# CCM_SoftwareUpdate Client WMI Class
The `CCM_SoftwareUpdate` WMI class is a client class, in Configuration Manager, that represents a software update.  

 Enumerating this class gives all the updates that are applicable and need to be installed.  You can use `GetObject` to query for an individual update based on the `UpdateID` property. Each update object has properties equivalent to the old COM interface `ICCMTargetedUpdate`. For more details on individual properties you can refer to Configuration Manager 2007 ICCMTargetedUpdate interface. We have listed here only the differences between `ICCMTargetedUpdate` and `CCM_SoftwareUpdate` classes.  

> [!IMPORTANT]
>  The software update client side SDK will only return set of updates which are deployed to client from Configuration Manager site server, and are applicable, and are yet to be installed on the client.  

 The following syntax is simplified from the Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
class CCM_SoftwareUpdate : CCM_SoftwareBase  
{  
     String ArticleID;  
     String BulletinID;  
     UInt32 ComplianceState;  
     UInt32 ContentSize;  
     Datetime Deadline  
     String Description;  
     UInt32 ErrorCode;  
     UInt32 EvaluationState;  
     Boolean ExclusiveUpdate;  
     String FullName;  
     Boolean IsUpgrade;  
     UInt32 MaxExecutionTime;  
     String Name;  
     Datetime NextUserScheduledTime;  
     Boolean NotifyUser;  
     Boolean OverrideServiceWindows;  
     UInt32 PercentComplete;  
     String Publisher;  
     Boolean RebootOutsideServiceWindows;  
     Datetime RestartDeadline;  
     Datetime StartTime;  
     String UpdateID;  
     String URL;  
     Boolean UserUIExperience;  
};  
```  

## Methods  
 The `CCM_SoftwareUpdate` class does not define any methods.  

## Properties  
 `ArticleID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Identifier of the knowledge base article for the software update. The maximum length for this value is 64 characters.  

 `BulletinID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Identifier of the bulletin for security updates released by Microsoft. The maximum length for this value is 64 characters. The default value is `None`.  

 `ComplianceState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Compliance state of the software update that indicates if the software update is missing and needs to be installed. The `ciNotPresent` state indicates missing updates. The following table shows other possible values for the **ComplianceState** property for software updates. Only values 0, 1, and 2 are used by software update management.  

|Value|State|  
|-----------|-----------|  
|0|ciNotPresent|  
|1|ciPresent|  
|2|ciPresenceUnknown (also used for not applicable)|  
|3|ciEvaluationError|  
|4|ciNotEvaluated|  
|5|ciNotUpdated|  
|6|ciNotConfigured|  

 `ContentSize`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Size of the software update content.  

> [!NOTE]
>  This property is only available after the software update is downloaded into Configuration Manager cache, not before.  

 `Deadline`  
 Data type: `Datetime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when the software update is installed.  

 `Description`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the software update.  

 `ErrorCode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Error code, if any, associated with the software update.  

 `EvaluationState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Evaluation state of the software update. Once the **InstallUpdates** method in the `CCM_SoftwareUpdatesManager` class is called to trigger installation of software updates, the **EvaluationState**, **PercentComplete** and **ErrorCode** properties can be used to monitor update progress.  

> [!NOTE]
>  The **EvaluationState** property is only meant to evaluate progress, not to find the compliance state of a software update. When a software update is not in a progress state, the value of **EvaluationState** is `none` or `available`, depending on whether there was any progress at any point in the past. This is not related to compliance state. Also, if a software update was downloaded at activation time, the value of **EvaluationState** is `none`. This value only changes once an install is attempted on the software update.  

 The following table shows the values for the **EvaluationState**property for software updates.  

|||  
|-|-|  
|**Value**|**State**|  
|0|ciJobStateNone|  
|1|ciJobStateAvailable|  
|2|ciJobStateSubmitted|  
|3|ciJobStateDetecting|  
|4|ciJobStatePreDownload|  
|5|ciJobStateDownloading|  
|6|ciJobStateWaitInstall|  
|7|ciJobStateInstalling|  
|8|ciJobStatePendingSoftReboot|  
|9|ciJobStatePendingHardReboot|  
|10|ciJobStateWaitReboot|  
|11|ciJobStateVerifying|  
|12|ciJobStateInstallComplete|  
|13|ciJobStateError|  
|14|ciJobStateWaitServiceWindow|  
|15|ciJobStateWaitUserLogon|  
|16|ciJobStateWaitUserLogoff|  
|17|ciJobStateWaitJobUserLogon|  
|18|ciJobStateWaitUserReconnect|  
|19|ciJobStatePendingUserLogoff|  
|20|ciJobStatePendingUpdate|  
|21|ciJobStateWaitingRetry|  
|22|ciJobStateWaitPresModeOff|  
|23|ciJobStateWaitForOrchestration|  

 `ExclusiveUpdate`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if software update is EXCLUSIVE; otherwise, `false`. An exclusive update cannot be installed at the same time as other updates.  

 `FullName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 This property is not used.  

 `IsUpgrade`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates whether the software update is an upgrade.  

 `MaxExecutionTime`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Maximum time required for the software update to run.  

 `Name`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the software update.  

 `NextUserScheduledTime`  
 Data type: `Datetime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when a user postpones specific software updates to non-business hours (NBH). This property shows the next NBH to be used.  

 `NotifyUser`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if notifications for the software update are shown to the user; otherwise, `false`.  

> [!NOTE]
>  If `UserUIExperience` is set to `false`, `NotifyUser` is ignored.  

 `OverrideServiceWindows`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the software update can be installed outside of maintenance windows; otherwise, `false`.  

 `PercentComplete`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Percentage of completion of the installation of the software update.  

 `Publisher`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Publisher of the software update.  

 `RebootOutsideServiceWindows`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the software update can restart outside maintenance windows; otherwise, `false`.  

 `RestartDeadline`  
 Data type: `Datetime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when a computer is restarted after the installation of the software update.  

 `StartTime`  
 Data type: `Datetime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when the software update is made available to the user.  

 `UpdateID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Identifier of the software update.  

 `URL`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 URL for a software update.  

 `UserUIExperience`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the software update is visible in software center; otherwise, `false`.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Configuration Manager Client SDK WMI Classes](../../../../../develop/reference/core/clients/sdk/client-sdk-wmi-classes.md)
