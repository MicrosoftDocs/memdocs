---
# required metadata

title: Intune Graph API - Reports and properties | Microsoft Docs
description: Learn about Intune reports and properties provided via Graph API.
keywords: 
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/16/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

#ms.reviewer: spenspshumwa
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Intune reports and properties available using Graph API

Microsoft Intune provides many reports in the console that can be exported using Graph APIs. Microsoft Graph is a RESTful web API that enables you to access Microsoft Cloud service resources. To export Intune reports, you must use the Microsoft Graph API to make a set of HTTP calls. For more information about , see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

> [!NOTE]
> Intune reports that have been migrated to a new [Intune reporting infrastructure](https://techcommunity.microsoft.com/t5/intune-customer-success/new-reporting-framework-coming-to-intune/ba-p/1009553#:~:text=New%20Reporting%20Framework%20Coming%20to%20Intune%20%20,Device%20compliance%20logging%20%203%20more%20rows), will be available for export from a single top-level export Graph API.
> 
> For more information about making REST API calls, including tools for interacting with Microsoft Graph, see [Use the Microsoft Graph API](/graph/use-the-api).

Microsoft Endpoint Manager will export reports using the following Microsoft Graph API endpoint:

```http
https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs
```
The following table contains the possible values for the `reportName` parameter. These are the currently available reports for export.

|         ReportName (Export Parameter)  |            Associated   Report in Microsoft Endpoint Manager        |
|-|-|
|         DeviceCompliance  |            Device   Compliance Org        |
|         DeviceNonCompliance  |            Non-compliant   devices        |
|         Devices  |            All   devices list        |
|         DetectedAppsAggregate  |            Detected   Apps report        |
|         FeatureUpdatePolicyFailuresAggregate  |            Under   **Devices** > **Monitor** > **Failure for feature updates**       |
|         DeviceFailuresByFeatureUpdatePolicy  |            Under   **Devices** > **Monitor** > **Failure for feature updates** > *click   on error*        |
|         FeatureUpdateDeviceState  |            Under   **Reports** > **Window Updates** > **Reports** > **Windows   Feature Update Report**         |
|         UnhealthyDefenderAgents  |            Under   **Endpoint Security** > **Antivirus** > **Win10 Unhealthy   Endpoints**        |
|         DefenderAgents  |            Under   **Reports** > **MicrosoftDefender** > **Reports** > **Agent   Status**        |
|         ActiveMalware  |            Under   **Endpoint Security** > **Antivirus** > **Win10 detected   malware**        |
|         Malware  |            Under   **Reports** > **MicrosoftDefender** > **Reports** > **Detected   malware**        |

Each of the listed reports is described below.

## DeviceCompliance report

The following table contains the possible output when calling the `DeviceCompliance` report:

| Available properties |
|-|
| DeviceId |
| IntuneDeviceId |
| AadDeviceId |
| DeviceName |
| DeviceType |
| OSDescription |
| OSVersion |
| OwnerType |
| LastContact |
| InGracePeriodUntil |
| IMEI |
| SerialNumber |
| ManagementAgents |
| PrimaryUser |
| UserId |
| UPN |
| UserEmail |
| UserName |
| DeviceHealthThreatLevel |
| RetireAfterDatetime |
| PartnerDeviceId |
| ComplianceState |
| OS |

You can choose to filter the `DeviceCompliance` report's output based on the following columns:
- `ComplianceState`
- `OS` 
- `OwnerType`
- `DeviceType` 

## DeviceNonCompliance report

The following table contains the possible output when calling the `DeviceNonCompliance` report:

|     Available properties  |
|-|
|     DeviceId  |
|            IntuneDeviceId   |
| AadDeviceId   |
| DeviceName   |
| DeviceType   |
| OSDescription   |
|            OSVersion   |
| OwnerType   |
| LastContact   |
| InGracePeriodUntil   |
| IMEI   |
|            SerialNumber   |
| ManagementAgents   |
| PrimaryUser   |
| UserId     |
| UPN   |
|            UserEmail   |
| UserName   |
| DeviceHealthThreatLevel   |
| RetireAfterDatetime   |
| PartnerDeviceId   |
|            ComplianceState         |
| OS |

You can choose to filter the `DeviceNonCompliance` report's output based on the following columns:
- `OS` 
- `OwnerType`
- `DeviceType` 
- `UserId`
- `ComplianceState`

## Devices report

The following table contains the possible output when calling the `Devices` report:

|     Available properties |
|-|
|     DeviceId  |
| DeviceName  |
| DeviceType  |
| ClientRegistrationStatus  |
|            OwnerType  |
| CreatedDate  |
| LastContact  |
| ManagementAgents  |
| ManagementState  |
|            ReferenceId  |
| CategoryId  |
| EnrollmentType  |
| CertExpirationDate  |
| MDMStatus  |
|            OSVersion  |
| GraphDeviceIsManaged  |
| EasID  |
| SerialNumber  |
| EnrolledByUser  |
|            Manufacturer  |
| Model  |
| OSDescription  |
| IsManaged  |
| EasActivationStatus  |
|            IMEI  |
| EasLastSyncSuccessUtc  |
| EasStateReason  |
| EasAccessState  |
| EncryptionStatus  |
|            SupervisedStatus  |
| PhoneNumberE164Format  |
| InGracePeriodUntil  |
| AndroidPatchLevel  |
| WifiMacAddress  |
|            SCCMCoManagementFeatures  |
| MEID  |
| SubscriberCarrierNetwork  |
| StorageTotal  |
| StorageFree  |
|            ManagedDeviceName  |
| LastLoggedOnUserUPN  |
| MDMWinsOverGPStartTime  |
| StagedDeviceType  |
| UserApprovedEnrollment  |
|            ExtendedProperties  |
| EntitySource  |
| PrimaryUser  |
| CategoryName  |
| UserId  |
|            UPN  |
| UserEmail  |
| UserName  |
| RetireAfterDatetime  |
| PartnerDeviceId  |
|            HasUnlockToken  |
| CompliantState  |
| ManagedBy  |
| Ownership  |
| DeviceState  |
|            DeviceRegistrationState  |
| SupervisedStatusString  |
| EncryptionStatusString  |
| OS  |
| SkuFamily  |
|            JoinType  |
| PhoneNumber  |
| JailBroken  |
| EasActivationStatusString        |

You can choose to filter the `Devices` report's output based on the following columns:
- `OwnerType`
- `DeviceType` 
- `ManagementAgents`
- `CategoryName` 
- `ManagementState` 
- `CompliantState` 
- `JailBroken` 
- `LastContact` 
- `CreatedDate` 
- `EnrollmentType` 

## DetectedAppsAggregate report

The following table contains the possible output when calling the `DetectedAppsAggregate` report:

|     Available properties  |
|-|
|     ApplicationKey  |
| ApplicationName  |
|            ApplicationVersion  |
| DeviceCount  |
| BundleSize  |

You can choose to filter the `DetectedAppsAggregate` report's output based on the following column:
- `ApplicationName`

## FeatureUpdatePolicyFailuresAggregate report

The following table contains the possible output when calling the `FeatureUpdatePolicyFailuresAggregate` report:

| Available properties  |
|-|
|     PolicyId  |
|     PolicyName  |
|     FeatureUpdateVersion  |
|     NumberOfDevicesWithErrors     |

You cannot filter this report.

## DeviceFailuresByFeatureUpdatePolicy report

The following table contains the possible output when calling the `DeviceFailuresByFeatureUpdatePolicy` report:

| Available properties  |
|-|
|     PolicyId  |
|     PolicyName  |
|     FeatureUpdateVersion  |
|     DeviceId  |
|     AADDeviceId  |
|     AlertId  |
|     EventDateTimeUTC  |
|     LastUpdatedAlertStatusDateTimeUTC  |
|     AlertType  |
|     AlertStatus  |
|     AlertClassification  |
|     WindowsUpdateVersion  |
|     Build  |
|     AlertMessage  |
|     AlertMessageDescription  |
|     AlertMessageData  |
|     Win32ErrorCode  |
|     RecommendedAction  |
|     ExtendedRecommendedAction  |
|     StartDateTimeUTC  |
|     ResolvedDateTimeUTC  |
|     DeviceName  |
|     UPN     |

You can choose to filter the `DeviceFailuresByFeatureUpdatePolicy` report's output based on the following columns:
- `PolicyId` **(Required)** 
- `AlertMessage` 
- `RecommendedAction` 
- `WindowsUpdateVersion` 

## FeatureUpdateDeviceState report

The following table contains the possible output when calling the `FeatureUpdateDeviceState` report:

| Available properties  |
|-|
|     PolicyId  |
|     PolicyName  |
|     FeatureUpdateVersion  |
|     DeviceId  |
|     AADDeviceId  |
|     PartnerPolicyId  |
|     EventDateTimeUTC  |
|     LastSuccessfulDeviceUpdateStatus  |
|     LastSuccessfulDeviceUpdateSubstatus  |
|     LastSuccessfulDeviceUpdateStatusEventDateTimeUTC  |
|     CurrentDeviceUpdateStatus  |
|     CurrentDeviceUpdateSubstatus  |
|     CurrentDeviceUpdateStatusEventDateTimeUTC  |
|     LatestAlertMessage  |
|     LatestAlertMessageDescription  |
|     LatestAlertRecommendedAction  |
|     LatestAlertExtendedRecommendedAction  |
|     UpdateCategory  |
|     WindowsUpdateVersion  |
|     LastWUScanTimeUTC  |
|     Build  |
|     DeviceName  |
|     OwnerType  |
|     UPN  |
|     AggregateState     |

You can choose to filter the `FeatureUpdateDeviceState` report's output based on the following columns:
- `PolicyId` **(Required)**
- `AggregateState`
- `LatestAlertMessage`
- `OwnerType`

## UnhealthyDefenderAgents and DefenderAgents reports

The `UnhealthyDefenderAgents` and `DefenderAgents` reports are two distinct reports that have the same set of properties and filters. The following table contains the possible output when calling the `UnhealthyDefenderAgents` or `DefenderAgents` reports:

| Available   Columns  |
|-|
|     DeviceId  |
|     DeviceName  |
|     DeviceState  |
|     PendingFullScan  |
|     PendingReboot  |
|     PendingManualSteps  |
|     PendingOfflineScan  |
|     CriticalFailure  |
|     MalwareProtectionEnabled  |
|     RealTimeProtectionEnabled  |
|     NetworkInspectionSystemEnabled  |
|     SignatureUpdateOverdue  |
|     QuickScanOverdue  |
|     FullScanOverdue  |
|     RebootRequired  |
|     FullScanRequired  |
|     EngineVersion  |
|     SignatureVersion  |
|     AntiMalwareVersion  |
|     LastQuickScanDateTime  |
|     LastFullScanDateTime  |
|     LastQuickScanSignatureVersion  |
|     LastFullScanSignatureVersion  |
|     LastReportedDateTime  |
|     UPN  |
|     UserEmail  |
|     UserName     |

You can choose to filter the `UnhealthyDefenderAgents` and `DefenderAgents` report's output based on the following columns:
- `DeviceState` 
- `SignatureUpdateOverdue` 
- `MalwareProtectionEnabled`
- `RealTimeProtectionEnabled` 
- `NetworkInspectionSystemEnabled`

## ActiveMalware and Malware reports

The `ActiveMalware` and `Malware` reports are two distinct reports that have the same set of properties and filters. The following table contains the possible output when calling the `ActiveMalware` or `Malware` reports:

| Available   Columns  |
|-|
|     DeviceId  |
|     DeviceName  |
|     MalwareId  |
|     MalwareName  |
|     AdditionalInformationUrl  |
|     Severity  |
|     MalwareCategory  |
|     ExecutionState  |
|     State  |
|     InitialDetectionDateTime  |
|     LastStateChangeDateTime  |
|     DetectionCount  |
|     UPN  |
|     UserEmail  |
|     UserName     |

You can choose to filter the `ActiveMalware` and `Malware` report's output based on the following columns:
- `Severity` 
- `ExecutionState` 
- `State` 

## Next steps

- [Microsoft Graph documentation](/graph/)
- [Intune reports](./reports.md)
