---
# required metadata

title: Intune Graph API - Reports and properties | Microsoft Docs
description: Learn about Intune reports and properties provided via Graph API.
keywords: 
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/02/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
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
|         DiscoveredAppsRawData  |            Under **Apps** > **Monitor** > **Discoverd apps** > **Export**         |
|         FeatureUpdateDeviceState  |            Under   **Reports** > **Window Updates** > **Reports** > **Windows   Feature Update Report**         |
|         UnhealthyDefenderAgents  |            Under   **Endpoint Security** > **Antivirus** > **Win10 Unhealthy   Endpoints**        |
|         DefenderAgents  |            Under   **Reports** > **MicrosoftDefender** > **Reports** > **Agent   Status**        |
|         ActiveMalware  |            Under   **Endpoint Security** > **Antivirus** > **Win10 detected   malware**        |
|         Malware  |            Under   **Reports** > **MicrosoftDefender** > **Reports** > **Detected   malware**        |
|         AllAppsList  |            Under   **Apps** > **All Apps**        |
|         AppInstallStatusAggregate  |             Under **Apps** > **Monitor** > **App install status**         |
|         DeviceInstallStatusByApp  |            Under **Apps** > **All Apps** > *Select an individual app*       |
|         UserInstallStatusAggregateByApp  |            Under **Apps** > **All Apps** > *Select an individual app*         |
|         ComanagedDeviceWorkloads  |            Under **Reports** > **Cloud attached devices** > **Reports** > **Co-Managed Workloads**        |
|         ComanagementEligibilityTenantAttachedDevices  |            Under **Reports** > **Cloud attached devices** > **Reports** > **Co-Management Eligibility**        |
|         DeviceRunStatesByProactiveRemediation  |            Under **Reports** > **Endpoint Analytics** > **Proactive remediations** > *Select a remediation* > **Device status**        |
|         DevicesWithInventory  |            Under **Devices** > **All Devices** > **Export**        |
|         FirewallStatus  |            Under **Reports** > **Firewall** > **MDM Firewall status for Windows 10 and later**        |
|         GPAnalyticsSettingMigrationReadiness  |            Under **Reports** > **Group policy analytics** > **Reports** > **Group policy migration readiness**        |
|         QualityUpdateDeviceErrorsByPolicy  |            Under **Devices** > **Monitor** > **Windows Expedited update failures** > *Select a profile*        |
|         QualityUpdateDeviceStatusByPolicy  |            Under **Reports** > **Windows updates** > **Reports** > **Windows Expedited Update Report**        |
|         MAMAppProtectionStatus  |            Under **Apps** > **Monitor** > **App protection status** > **App protection report: iOS, Android**       |
|         MAMAppConfigurationStatus  |            Under **Apps** > **Monitor** > **App protection status** > **App configuration report**        |



Each of the listed reports is described below.

## AllAppsList

The following table contains the possible output when calling the `AllAppsList` report:

| Available   properties |
|-|
|     AppIdentifier |
| Name |
| Publisher |
| Platform |
| Status |
| Type |
| Version |
| Description |
| Developer |
| FeaturedApp |
| Notes |
| Owner |
| DateCreated |
| LastModified |
| ExpirationDate |
| MoreInformationURL |
| PrivacyInformationURL |
| StoreURL |
| Assigned    |

There are no filters for this report.

## AppInstallStatusAggregate

The following table contains the possible output when calling the `AppInstallStatusAggregate` report:

| Available   properties |
|-|
|     ApplicationId |
| DisplayName |
| Publisher |
| Platform |
| Platform_loc |
| AppVersion |
| InstalledDeviceCount |
| InstalledUserCount |
| FailedDeviceCount |
| FailedUserCount |
| PendingInstallDeviceCount |
| PendingInstallUserCount |
| NotApplicableDeviceCount |
| NotApplicableUserCount |
| NotInstalledDeviceCount |
| NotInstalledUserCount |
| FailedDevicePercentage    |

You can choose to filter the `AppInstallStatusAggregate` report's output based on the following columns:
- `Platform`
- `FailedDevicePercentage`

## DeviceInstallStatusByApp

The following table contains the possible output when calling the `DeviceInstallStatusByApp` report:

| Available   properties |
|-|
|     DeviceName |
| UserPrincipalName |
| Platform |
| AppVersion |
| DeviceId |
| AssignmentFilterIdsExist |
| LastModifiedDateTime |
| AppInstallState |
| AppInstallState_loc |
| AppInstallStateDetails |
| AppInstallStateDetails_loc |
| HexErrorCode    |

You can choose to filter the `DeviceInstallStatusByApp` report's output based on the following columns:
- `ApplicationId`
- `AppInstallState`
- `HexErrorCode` (Used as ErrorCode)

## UserInstallStatusAggregateByApp

The following table contains the possible output when calling the `UserInstallStatusAggregateByApp` report:

| Available   properties |
|-|
|     UserName |
| UserPrincipalName |
| FailedCount |
| InstalledCount |
| PendingInstallCount |
| NotInstalledCount |
| NotApplicableCount    |

You can choose to filter the `UserInstallStatusAggregateByApp` report's output based on the following column:
- `ApplicationId`

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

## DiscoveredAppsRawData report

The following table contains the possible output when calling the `DiscoveredAppsRawData` report:

| Available   properties |
|-|
| ApplicationKey |
| ApplicationName |
| ApplicationPublisher |
| ApplicationShortVersion |
| ApplicationSize |
| ApplicationVersion |
| DeviceId |
| DeviceName |
| ImeiNumber |
| OSDescription |
| OSVersion |
| Platform |
| UserId |
| EmailAddress |
| UserName |

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

## ComanagedDeviceWorkloads 

The following table contains the possible output when calling the `ComanagedDeviceWorkloads` report:

| Available   properties |
|-|
|   DeviceName  |
|   DeviceId    | 
|   CompliancePolicy    | 
|   ResourceAccess   |
|   DeviceConfiguration  |
|   WindowsUpdateforBusiness     |
|   EndpointProtection   |
|   ModernApps   |
|   OfficeApps   |

You can choose to filter the `ComanagedDeviceWorkloads` report's output based on the following columns:
- `CompliancePolicy`
- `ResourceAccess`
- `DeviceConfiguration`
- `WindowsUpdateforBusiness`
- `EndpointProtection`
- `ModernApps`
- `OfficeApps`

## ComanagementEligibilityTenantAttachedDevices 

The following table contains the possible output when calling the `ComanagementEligibilityTenantAttachedDevices` report:

| Available   properties |
|-|
|   DeviceName   |
|   DeviceId   |
|   Status   |
|   OSDescription   |
|   OSVersion   |

You can choose to filter the `ComanagementEligibilityTenantAttachedDevices` report's output based on the following columns:
- `Status` 

## DeviceRunStatesByProactiveRemediation 

The following table contains the possible output when calling the `DeviceRunStatesByProactiveRemediation` report:

| Available   properties |
|-|
|   PolicyId   | 
|   DeviceId   | 
|   UserId   | 
|   InternalVersion   | 
|   ModifiedTime   | 
|   PostRemediationDetectionScriptError   | 
|   PostRemediationDetectionScriptOutput   | 
|   PreRemediationDetectionScriptError   | 
|   PreRemediationDetectionScriptOutput   | 
|   RemediationScriptErrorDetails   | 
|   RemediationStatus   | 
|   DeviceName   | 
|   OSVersion   | 
|   UPN   | 
|   UserEmail   | 
|   UserName   | 
|   DetectionStatus   | 
|   UniqueKustoKey   | 
|   DetectionScriptStatus   | 
|   RemediationScriptStatus   | 
|   PolicyId   | 

You can choose to filter the `DeviceRunStatesByProactiveRemediation` report's output based on the following columns:
- `PolicyId` **(required)**
- `RemediationStatus`
- `DetectionStatus`

## DevicesWithInventory 

> [!NOTE]
> To maintain backwards compatibility, there are mappings that take place. You can map column names that the export API will allow you to select, to what you will receive back.
>
> The column alias can only be accepted by the select parameter, and can not be accepted by the filter parameter.
>
> The values for `EnrollmentType`, `PartnerFeaturesBitmask`, `ManagementAgents`, `CertExpirationDate`, and `IsManaged` will only be exported when they are included in the select parameter. These columns will not be exported by default.

The following table contains the possible output when calling the `DevicesWithInventory` report:

| Requestable Columns  | Columns received  |
|---|---|
| DeviceId  | Device ID  |
| DeviceName  | Device name  |
| CreatedDate  | Enrollment date  |
| LastContact  | Last check-in  |
| ReferenceId  | Azure AD Device ID  |
| OSVersion  | OS version  |
| GraphDeviceIsManaged  | Azure AD registered  |
| EasID  | EAS activation ID  |
| SerialNumber  | Serial number  |
| Manufacturer  | Manufacturer  |
| Model  | Model  |
| EasActivationStatus  | EAS activated  |
| IMEI  | IMEI  |
| EasLastSyncSuccessUtc  | Last EAS sync time  |
| EasStateReason  | EAS reason  |
| EasAccessState  | EAS status  |
| InGracePeriodUntil  | Compliance grace period expiration  |
| AndroidPatchLevel  | Security patch level  |
| WifiMacAddress  | Wi-Fi MAC  |
| MEID  | MEID  |
| SubscriberCarrierNetwork  | Subscriber carrier  |
| StorageTotal  | Total storage  |
| StorageFree  | Free storage  |
| ManagedDeviceName  | Management name  |
| CategoryName  | Category  |
| UserId  | UserId  |
| UPN  | Primary user UPN  |
| UserEmail  | Primary user email address  |
| UserName  | Primary user display name  |
| WiFiIPv4Address  | WiFiIPv4Address  |
| WiFiSubnetID  | WiFiSubnetID  |
| CompliantState *(alias: ComplianceState)*  | Compliance  |
| ManagementAgent  | Managed by  |
| OwnerType  | Ownership  |
| ManagementState  | Device state  |
| DeviceRegistrationState  | Intune registered  |
| IsSupervised  | Supervised  |
| IsEncrypted  | Encrypted  |
| DeviceType *(alias: OS)*  | OS  |
| SkuFamily  | SkuFamily  |
| JoinType  | JoinType  |
| PhoneNumber  | Phone number  |
| JailBroken  | Jailbroken  |
| ICCID  | ICCID  |
| EthernetMAC  | EthernetMAC  |
| CellularTechnology  | CellularTechnology  |
| ProcessorArchitecture  | ProcessorArchitecture  |
| EID  | EID  |
| EnrollmentType  | EnrollmentType  |
| PartnerFeaturesBitmask  | PartnerFeaturesBitmask  |
| ManagementAgents  | ManagementAgents  |
| CertExpirationDate  | CertExpirationDate  |
| IsManaged  | IsManaged  |
| SystemManagementBIOSVersion  | SystemManagementBIOSVersion  |
| TPMManufacturerId  | TPMManufacturerId  |
| TPMManufacturerVersion  | TPMManufacturerVersion  |

You can choose to filter the `DevicesWithInventory` report's output based on the following columns:
- `CreatedDate`
- `LastContact`
- `CategoryName` 
- `CompliantState` 
- `ManagementAgents` 
- `OwnerType`
- `ManagementState`
- `DeviceType`
- `JailBroken` 
- `EnrollmentType` 
- `PartnerFeaturesBitmask` 

`ProcessorArchitecture` mappings:

Windows 10+:
- 9 = x64
- 5 = ARM
- 12 = ARM64
- 0 = x86
- default = Unknown

Mac:
- 9 = x64
- 12 = ARM64
- default = unknown

## FirewallStatus  

The following table contains the possible output when calling the `FirewallStatus` report:

| Available   properties |
|-|
| DeviceName  | 
| FirewallStatus  | 
| FirewallStatus_loc   |
| _ManagedBy   |
| _ManagedBy_loc   |
| UPN   |

You can choose to filter the `FirewallStatus` report's output based on the following columns:
- `FirewallStatus` 

## GPAnalyticsSettingMigrationReadiness

The following table contains the possible output when calling the `GPAnalyticsSettingMigrationReadiness` report:

| Available   properties |
|-|
| SettingName   | 
| SettingCategory   | 
| MigrationReadiness   | 
| OSVersion   | 
| Scope   | 
| ProfileType   | 
| CSPName   | 
| MdmMapping   | 

You can choose to filter the `GPAnalyticsSettingMigrationReadiness` report's output based on the following columns:
- `MigrationReadiness` 
- `ProfileType` 
- `CSPName` 

## QualityUpdateDeviceErrorsByPolicy 

The following table contains the possible output when calling the `QualityUpdateDeviceErrorsByPolicy` report:

| Available   properties |
|-|
| PolicyId   | 
| DeviceName   |  
| AlertMessage   |  
| AlertMessage_loc   |  
| Win32ErrorCode   |  
| UPN   |  
| ExpediteQUReleaseDate   |  
| DeviceId   |  

You can choose to filter the `QualityUpdateDeviceErrorsByPolicy` report's output based on the following columns:
- `PolicyId` **(required)** 
- `AlertMessage` 

## QualityUpdateDeviceStatusByPolicy 

The following table contains the possible output when calling the `QualityUpdateDeviceStatusByPolicy` report:

| Available   properties |
|-|
| PolicyId   |  
| DeviceName   |  
| UPN   |  
| DeviceId   |  
| AADDeviceId   |  
| EventDateTimeUTC   |  
| CurrentDeviceUpdateStatus   |  
| CurrentDeviceUpdateStatus_loc   |  
| CurrentDeviceUpdateSubstatus   |  
| CurrentDeviceUpdateSubstatus_loc   |  
| AggregateState   |  
| AggregateState_loc   |  
| LatestAlertMessage   |  
| LatestAlertMessage_loc   |  
| LastWUScanTimeUTC   |  
| OwnerType   |  

You can choose to filter the `QualityUpdateDeviceStatusByPolicy` report's output based on the following columns:
- `PolicyId` **(required)** 
- `AggregateState`
- `OwnerType`

## MAMAppProtectionStatus 

The following table contains the possible output when calling the `MAMAppProtectionStatus` report:

| Available   properties |
|-|
| User   | 
| Email   | 
| App   | 
| AppVersion   | 
| SdkVersion   | 
| AppInstanceId   | 
| DeviceName   | 
| DeviceHealth   | 
| DeviceType   | 
| DeviceManufacturer   | 
| DeviceModel   | 
| AndroidPatchVersion   | 
| AADDeviceID   | 
| MDMDeviceID   | 
| Platform   | 
| PlatformVersion   | 
| ManagementType   |
| AppProtectionStatus   | 
| Policy   | 
| LastSync   |
| ComplianceState   | 

There are no filters for this report.

## MAMAppConfigurationStatus 

The following table contains the possible output when calling the `MAMAppConfigurationStatus` report:

| Available   properties |
|-|
| User   | 
| Email   | 
| App   | 
| AppVersion   | 
| SdkVersion   | 
| AppInstanceId   | 
| DeviceName   | 
| DeviceHealth   | 
| DeviceType   | 
| DeviceManufacturer   | 
| DeviceModel   | 
| AndroidPatchVersion   | 
| AADDeviceID   | 
| MDMDeviceID    |
| Platform   | 
| PlatformVersion   | 
| Policy   | 
| LastSync   | 

There are no filters for this report.

## Next steps

- [Microsoft Graph documentation](/graph/)
- [Intune reports](./reports.md)
