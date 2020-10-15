---
# required metadata

title: Use Graph APIs to export Intune Reports | Microsoft Docs
description: Learn about exporting Intune reports using Graph APIs.
keywords: 
ms.author: erikre
author: Erikre
manager: dougeby
ms.date: 10/08/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

#ms.reviewer: [ALIAS]
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Export Intune reports using Graph APIs

All reports that have been migrated to the Intune reporting infrastructure will be available for export from a single top-level export API. You must use the Microsoft Graph API to make the HTTP call. Microsoft Graph is a RESTful web API that enables you to access Microsoft Cloud service resources. 

> [!NOTE]
> For information about making REST API calls, including tools for interacting with Microsoft Graph, see [Use the Microsoft Graph API](https://docs.microsoft.com/graph/use-the-api).

Microsoft Endpoint Manager will export reports based on the following Microsoft Graph API endpoint:

```http
https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs
```
## Example devices report request and response

When making the request, you must provide a `reportName` parameter as part of the request body based on the report that you would like to export. Below is an example of an export request for the **Devices** report. You must use the POST HTTP method on your request. The POST method is used to create a new resource or perform an action.

### Request example

The below request contains the HTTP method used on the request to Microsoft Graph.

```http
{ 
    "reportName": "Devices", 
    "filter": "", 
    "select": [ 
        "DeviceName", 
        "managementAgent", 
        "ownerType", 
        "complianceState", 
        "OS", 
        "OSVersion", 
        "LastContact", 
        "UPN", 
        "DeviceId" 
    ], 
    "localization": "true", 
    "ColumnName": "ui" 
} 
```
### Response example

Based on the above POST request, Graph returns a response message. The response message is the data that you requested or the result of the operation.

```http
{ 
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#deviceManagement/reports/exportJobs/$entity", 
    "id": "Devices_05e62361-783b-4cec-b635-0aed0ecf14a3", 
    "reportName": "Devices", 
    "filter": "", 
    "select": [ 
        "DeviceName", 
        "managementAgent", 
        "ownerType", 
        "complianceState", 
        "OS", 
        "OSVersion", 
        "LastContact", 
        "UPN", 
        "DeviceId" 
    ], 
    "format": "csv", 
    "snapshotId": null, 
    "status": "notStarted", 
    "url": null, 
    "requestDateTime": "2020-08-19T03:43:32.1405758Z", 
    "expirationDateTime": "0001-01-01T00:00:00Z" 
} 
```
You can then use the `id` field to query the status of the export with a GET request: 

For example:
```https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs('Devices_05e62361-783b-4cec-b635-0aed0ecf14a3') ```

You will need to continue calling this URL until you get a response with a `status: completed` attribute. It will look like the following example:

```http
{ 
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#deviceManagement/reports/exportJobs/$entity", 
    "id": "Devices_05e62361-783b-4cec-b635-0aed0ecf14a3", 
    "reportName": "Devices", 
    "filter": "", 
    "select": [ 
        "DeviceName", 
        "managementAgent", 
        "ownerType", 
        "complianceState", 
        "OS", 
        "OSVersion", 
        "LastContact", 
        "UPN", 
        "DeviceId" 
    ], 
    "format": "csv", 
    "snapshotId": null, 
    "status": "completed", 
    "url": "https://amsua0702repexpstorage.blob.core.windows.net/cec055a4-97f0-4889-b790-dc7ad0d12c29/Devices_05e62361-783b-4cec-b635-0aed0ecf14a3.zip?sv=2019-02-02&sr=b&sig=%2BP%2B4gGiZf0YzlQRuAV5Ji9Beorg4nnOtP%2F7bbFGH7GY%3D&skoid=1db6df02-4c8b-4cb3-8394-7ac2390642f8&sktid=72f988bf-86f1-41af-91ab-2d7cd011db47&skt=2020-08-19T03%3A48%3A32Z&ske=2020-08-19T09%3A44%3A23Z&sks=b&skv=2019-02-02&se=2020-08-19T09%3A44%3A23Z&sp=r", 
    "requestDateTime": "2020-08-19T03:43:32.1405758Z", 
    "expirationDateTime": "2020-08-19T09:44:23.8540289Z" 
} 
```
You can then directly download the compressed CSV from the `url` field.  

## Report parameters

There are three main parameters you can submit in your request body to define the export request: 

- `reportName`: Required. This parameter is the name of the report you want to specify.  
- `filter`: Not required for most reports. 
- `select`: Not required. If you don't specify a `select` value you will receive a default set of columns, which for most reports is the entire dataset. 

## Available reports

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

### DeviceCompliance report

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

### DeviceNonCompliance report

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

### Devices report

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

### DetectedAppsAggregate report

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

### FeatureUpdatePolicyFailuresAggregate report

The following table contains the possible output when calling the `FeatureUpdatePolicyFailuresAggregate` report:

| Available properties  |
|-|
|     PolicyId  |
|     PolicyName  |
|     FeatureUpdateVersion  |
|     NumberOfDevicesWithErrors     |

You cannot filter this report.

### DeviceFailuresByFeatureUpdatePolicy report

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

### FeatureUpdateDeviceState report

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

### UnhealthyDefenderAgents and DefenderAgents reports

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

### ActiveMalware and Malware reports

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

- [Microsoft Graph documentation](https://docs.microsoft.com/graph/)
- [Intune reports](https://docs.microsoft.com/mem/intune/fundamentals/reports)
