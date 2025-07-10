---
# required metadata

title: Intune Graph API - Reports and properties | Microsoft Docs
description: Learn about Intune reports and properties provided via Graph API.
keywords:
author: nicholasswhite
ms.author: nwhite
manager: laurawi
ms.date: 07/10/2024
ms.topic: article
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: davidra
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier2
- M365-identity-device-management
---

# Intune reports and properties available using Graph API

Microsoft Intune provides many reports in the Microsoft Intune admin center that can be exported using Graph APIs. Microsoft Graph is a RESTful web API that enables you to access Microsoft Cloud service resources. To export Intune reports, you must use the Microsoft Graph API to make a set of HTTP calls. For more information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

> [!NOTE]
> Intune reports that have been migrated to a new [Intune reporting infrastructure](https://techcommunity.microsoft.com/t5/intune-customer-success/new-reporting-framework-coming-to-intune/ba-p/1009553#:~:text=New%20Reporting%20Framework%20Coming%20to%20Intune%20%20,Device%20compliance%20logging%20%203%20more%20rows), will be available for export from a single top-level export Graph API.
>
> For more information about making REST API calls, including tools for interacting with Microsoft Graph, see [Use the Microsoft Graph API](/graph/use-the-api).

Microsoft Intune will export reports using the following Microsoft Graph API endpoint:

```http
https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs
```

The following table contains the possible values for the `reportName` parameter. These are the currently available reports for export.

| ReportName (Export Parameter) | Associated Report in Microsoft Intune |
|------------------------------|----------------------------------------|
| ActiveMalware | Under **Endpoint Security** > **Antivirus** > **Win10 detected malware** |
| ADMXSettingsByDeviceByPolicy | |
| AllAppsList | Under **Apps** > **All Apps** |
| AllDeviceCertificates | |
| AppInstallStatusAggregate | Under **Apps** > **Monitor** > **App install status** |
| AppInvAggregate | Under **Apps** > **Monitor** > **Discovered apps** > **Export**  |
| AppInvByDevice | Under **Devices** > **All Devices** > **Device** > **Discovered Apps**  |
| AppInvRawData | Under **Apps** > **Monitor** > **Discovered apps** > **Export**  |
<!-- | AppleDDMDeviceOSUpdateStatus | | -->
<!-- | AppleDDMOSUpdateFailures | | -->
<!-- | AppleDDMOSVersionReport | | -->
<!-- | AppleDDMSoftwareUpdatesSummary | | -->
| AutopilotV1DeploymentStatus | |
| AutopilotV2DeploymentStatus | |
| AutopilotV2DeploymentStatusDetailedAppInfo | |
| AutopilotV2DeploymentStatusDetailedScriptInfo | |
| BRBatteryByModel | |
| BRBatteryByOs | |
| BRDeviceBatteryAgg | |
| BREnergyUsage | |
| CatalogAppsUpdateList | |
| CertificatesByRAPolicy | |
| ComanagedDeviceWorkloads | Under **Reports** > **Cloud attached devices** > **Reports** > **Co-Managed Workloads** |
| ComanagementEligibilityTenantAttachedDevices | Under **Reports** > **Cloud attached devices** > **Reports** > **Co-Management Eligibility** |
| ConfigurationPolicyAggregate | |
| ConfigurationPolicyAggregateV3 | |
| ConfigurationPolicyDeviceAggregates | |
| ConfigurationPolicyDeviceAggregatesV3 | |
| ConfigurationPolicyDeviceAggregatesWithPF | |
| ConfigurationPolicyDeviceAggregatesWithPFV3 | |
| DefenderAgents | Under **Reports** > **MicrosoftDefender** > **Reports** > **Agent Status** |
| DependentAppsInstallStatus | |
| DeviceAssignmentStatusByConfigurationPolicy | |
| DeviceAssignmentStatusByConfigurationPolicyForAC | |
| DeviceAssignmentStatusByConfigurationPolicyForASR | |
| DeviceAssignmentStatusByConfigurationPolicyForEDR | |
| DeviceAssignmentStatusByConfigurationPolicyV3 | |
| DeviceCompliance | Device Compliance Org |
| DeviceComplianceTrend | |
| DeviceConfigurationPolicyStatuses | |
| DeviceConfigurationPolicyStatusesV3 | |
| DeviceConfigurationPolicyStatusesWithPF | |
| DeviceConfigurationPolicyStatusesWithPFV3 | |
| DeviceEnrollmentFailures | |
| DeviceFailuresByFeatureUpdatePolicy | Under **Devices** > **Monitor** > **Failure for feature updates** > *click on error* |
| DeviceInstallStatusByApp | Under **Apps** > **All Apps** > *Select an individual app* |
| DeviceIntentPerSettingStatus | |
| DeviceInventoryPolicyStatusesV3 | |
| DeviceInventoryPolicyStatusesWithPF | |
| DeviceNonCompliance | Non-compliant devices |
| DevicePoliciesComplianceReport | |
| DevicePoliciesComplianceReportV3 | |
| DevicePolicySettingsComplianceReport | |
| DevicePolicySettingsComplianceReportV3 | |
| DeviceRunStatesByProactiveRemediation | Under **Reports** > **Endpoint Analytics** > **Proactive remediations** > *Select a remediation* > **Device status** |
| DeviceRunStatesByScript | |
| Devices | All devices list |
| DevicesByAppInv | Under **Apps** > **Monitor** > **Discovered apps** > **Discovered app**> **Export**  |
| DevicesStatusByPolicyPlatformComplianceReport | |
| DevicesStatusByPolicyPlatformComplianceReportV3 | |
| DevicesStatusBySettingReport | |
| DevicesStatusBySettingReportV3 | |
| DeviceStatusByCompliacePolicyReport | |
| DeviceStatusByCompliacePolicyReportV3 | |
| DeviceStatusByCompliancePolicySettingReport | |
| DeviceStatusByCompliancePolicySettingReportV3 | |
| DeviceStatusesByConfigurationProfile | |
| DeviceStatusesByConfigurationProfileForAppControl | |
| DeviceStatusesByConfigurationProfileForASR | |
| DeviceStatusesByConfigurationProfileForEDR | |
| DeviceStatusesByConfigurationProfileV3 | |
| DeviceStatusesByConfigurationProfileWithPF | |
| DeviceStatusesByConfigurationProfileWithPFV3 | |
| DeviceStatusesByInventoryPolicyWithPF | |
| DeviceStatusesByInventoryPolicyWithPFV3 | |
| DeviceStatusSummaryByCompliacePolicyReport | |
| DeviceStatusSummaryByCompliacePolicyReportV3 | |
| DeviceStatusSummaryByCompliancePolicySettingsReport | |
| DeviceStatusSummaryByCompliancePolicySettingsReportV3 | |
| DevicesWithInventory | Under **Devices** > **All Devices** > **Export** |
| DevicesWithoutCompliancePolicy | |
| DevicesWithoutCompliancePolicyV3 | |
| DriverUpdatePolicyStatusSummary | |
| EAAnomalyAsset | |
| EAAnomalyAssetV2 | |
| EAAnomalyDeviceAsset | |
| EAAnomalyDeviceAssetV2 | |
| EAAppPerformance | |
| EADeviceModelPerformance | |
| EADeviceModelPerformanceV2 | |
| EADevicePerformance | |
| EADevicePerformanceV2 | |
| EADeviceScoresV2 | |
| EAModelScoresV2 | |
| EAOSVersionsPerformance | |
| EAResourcePerfAggByDevice | |
| EAResourcePerfAggByModel | |
| EAResourcePerfCpuSpikeProcess | |
| EAResourcePerfRamSpikeProcess | |
| EAStartupPerfDevicePerformance | |
| EAStartupPerfDevicePerformanceV2 | |
| EAStartupPerfDeviceProcesses | |
| EAStartupPerfModelPerformance | |
| EAStartupPerfModelPerformanceV2 | |
| EAWFADeviceList | |
| EAWFAModelPerformance | |
| EAWFAPerDevicePerformance | |
| EnrollmentActivity | |
| EnrollmentConfigurationPoliciesByDevice | |
| EpmAggregationReportByApplication | |
| EpmAggregationReportByApplicationV2 | |
| EpmAggregationReportByPublisher | |
| EpmAggregationReportByPublisherV2 | |
| EpmAggregationReportByUser | |
| EpmAggregationReportByUserAppByMonth | |
| EpmAggregationReportByUserV2 | |
| EpmDeniedReport | |
| EpmElevationReportByUserAppByDayToReporting | |
| EpmElevationReportElevationEvent | |
| EpmInsightsElevationTrend | |
| EpmInsightsMostFrequentElevations | |
| EpmInsightsReport | |
| FeatureUpdateDeviceState | Under **Reports** > **Window Updates** > **Reports** > **Windows Feature Update Report**  |
| FeatureUpdatePolicyFailuresAggregate | Under **Devices** > **Monitor** > **Failure for feature updates** |
| FeatureUpdatePolicyStatusSummary | |
| FilteredAppsList | |
| FirewallStatus | Under **Reports** > **Firewall** > **MDM Firewall status for Windows 10 and later** |
| FirewallUnhealthyStatus | |
| GPAnalyticsSettingMigrationReadiness | Under **Reports** > **Group policy analytics** > **Reports** > **Group policy migration readiness** |
| InventoryPolicyDeviceAggregatesV3 | |
| InventoryPolicyDeviceAggregatesWithPF | |
| MAMAppConfigurationStatus | Under **Apps** > **Monitor** > **App protection status** > **App configuration report** |
| MAMAppConfigurationStatusScopedV2 | |
| MAMAppConfigurationStatusV2 | |
| MAMAppProtectionStatus | Under **Apps** > **Monitor** > **App protection status** > **App protection report: iOS, Android** |
| MAMAppProtectionStatusScopedV2 | |
| MAMAppProtectionStatusV2 | |
| Malware | Under **Reports** > **MicrosoftDefender** > **Reports** > **Detected malware** |
| MEMUpgradeReadinessOrgAsset | |
| NonCompliantCompliancePoliciesAggregate | |
| NonCompliantCompliancePoliciesAggregateV3 | |
| NonCompliantConfigurationPoliciesAggregateWithPF | |
| NonCompliantConfigurationPoliciesAggregateWithPFV3 | |
| NoncompliantDevicesAndSettings | |
| NoncompliantDevicesAndSettingsV3 | |
| NonCompliantDevicesByCompliancePolicy | |
| NonCompliantDevicesByCompliancePolicyV3 | |
| NoncompliantDevicesToBeRetired | |
| OrgAppsInstallStatus | |
| OrgDeviceInstallStatus | |
| PerSettingDeviceSummaryByConfigurationPolicy | |
| PerSettingDeviceSummaryByConfigurationPolicyForAppControl | |
| PerSettingDeviceSummaryByConfigurationPolicyForEDR | |
| PerSettingDeviceSummaryByInventoryPolicy | |
| PerSettingDeviceSummaryByInventoryPolicyV3 | |
| PerSettingSummaryByDeviceConfigurationPolicy | |
| Policies | |
| PolicyComplianceAggReport | |
| PolicyComplianceAggReportV3 | |
| PolicyNonComplianceAgg | |
| PolicyNonComplianceAggVer3 | |
| PolicyNonComplianceNew | |
| PolicyNonComplianceNewV3 | |
| PolicyRunStatesByProactiveRemediation | |
| QualityUpdateDeviceErrorsByPolicy | Under **Devices** > **Monitor** > **Windows Expedited update failures** > *Select a profile* |
| QualityUpdateDeviceStatusByPolicy | Under **Reports** > **Windows updates** > **Reports** > **Windows Expedited Update Report** |
| QualityUpdatePolicyStatusSummary | |
| RemoteAssistanceSessions | |
| ResourcePerformanceAggregateByDevice | |
| ResourcePerformanceAggregateByModel | |
| SettingComplianceAggReport | |
| SettingComplianceAggReportV3 | |
| TicketingSecurityTaskAppsList | |
| TpmAttestationStatus | |
| UnhealthyDefenderAgents | Under **Endpoint Security** > **Antivirus** > **Win10 Unhealthy Endpoints** |
| UserInstallStatusAggregateByApp | Under **Apps** > **All Apps** > *Select an individual app* |
| Users | |
| UserScaleTest | |
| WindowsDeviceHealthAttestationReport | |
| WindowsUpdatePerPolicyPerDeviceStatus | |
| WorkFromAnywhereDeviceList | |


Each of the listed reports is described below.

## ActiveMalware

The following table contains the possible output when calling the `ActiveMalware` report:

| Available   Columns  |
|-|
|     AdditionalInformationUrl  |
|     DetectionCount  |
|     DeviceId  |
|     DeviceName  |
|     ExecutionState  |
|     InitialDetectionDateTime  |
|     LastStateChangeDateTime  |
|     MalwareCategory  |
|     MalwareId  |
|     MalwareName  |
|     Severity  |
|     State  |
|     UPN  |
|     UserEmail  |
|     UserName     |
|     _ManagedBy  |

You can choose to filter the `ActiveMalware` and `Malware` report's output based on the following columns:
- `Severity`
- `ExecutionState`
- `State`

## ADMXSettingsByDeviceByPolicy

The following table contains the possible output when calling the `ADMXSettingsByDeviceByPolicy` report:

| Available properties |
|-|
| CreationSource |
| DeviceId |
| ErrorCode |
| ErrorType |
| PolicyId |
| PolicyName |
| PolicyVersion |
| SettingId |
| SettingInstanceId |
| SettingInstancePath |
| SettingName |
| SettingNameStringId |
| SettingStatus |
| UserId |

You can choose to filter the `ADMXSettingsByDeviceByPolicy` report's output based on the following columns:
- `PolicyId`
- `UserId`
- `DeviceId`

## AllAppsList

The following table contains the possible output when calling the `AllAppsList` report:

| Available   properties |
|-|
| AppIdentifier |
| Assigned |
| DateCreated |
| Description |
| Developer |
| ExpirationDate |
| FeaturedApp |
| LastModified |
| MoreInformationURL |
| Name |
| Notes |
| Owner |
| Platform |
| PrivacyInformationURL |
| Publisher |
| Status |
| StoreURL |
| Type |
| Version |

There are no filters for this report.

## AllDeviceCertificates

The following table contains the possible output when calling the `AllDeviceCertificates` report:

| Available properties |
|-|
| CertificateStatus |
| DeviceId |
| DeviceName |
| EnhancedKeyUsage |
| IssuerName |
| KeyUsage |
| PolicyId |
| SerialNumber |
| SubjectName |
| Thumbprint |
| UPN |
| UserId |
| ValidFrom |
| ValidTo |

There are no filters for this report.

## AppInstallStatusAggregate

The following table contains the possible output when calling the `AppInstallStatusAggregate` report:

| Available   properties |
|-|
| AppPlatform |
| ApplicationId |
| AppVersion |
| DisplayName |
| FailedDeviceCount |
| FailedDevicePercentage |
| FailedUserCount |
| InstalledDeviceCount |
| InstalledUserCount |
| NotApplicableDeviceCount |
| NotApplicableUserCount |
| NotInstalledDeviceCount |
| NotInstalledUserCount |
| PendingInstallDeviceCount |
| PendingInstallUserCount |
| Platform |
| Publisher |

You can choose to filter the `AppInstallStatusAggregate` report's output based on the following columns:
- `Platform`
- `FailedDevicePercentage`

## AppInvAggregate

The following table contains the possible output when calling the `AppInvAggregate` report:

|     Available properties  |
|-|
| ApplicationId  |
| ApplicationKey  |
| ApplicationName  |
| ApplicationPublisher  |
| ApplicationShortVersion  |
| ApplicationVersion  |
| DeviceCount  |
| Platform  |

There are no filters for this report.

## AppInvByDevice

The following table contains the possible output when calling the `AppInvByDevice` report:

|     Available properties  |
|-|
|     ApplicationId  |
|     ApplicationKey  |
|     ApplicationName  |
|     ApplicationPublisher  |
|     ApplicationShortVersion  |
|     ApplicationVersion  |
|     DeviceId  |
|     DeviceName  |
|     EmailAddress  |
|     OSDescription  |
|     OSVersion  |
|     Platform  |
|     UserId  |
|     UserName  |

You can choose to filter the `AppInvByDevice` report's output based on the following column:
- `DeviceId` **(Required)**

## AppInvRawData report

The following table contains the possible output when calling the `AppInvRawData` report:

|     Available properties  |
|-|
|     ApplicationKey  |
|     ApplicationName  |
|     ApplicationPublisher  |
|     ApplicationShortVersion  |
|     ApplicationVersion  |
|     DeviceId  |
|     DeviceName  |
|     EmailAddress  |
|     OSDescription  |
|     OSVersion  |
|     Platform  |
|     UserId  |
|     UserName  |

You can filter the `AppInvRawData` report using the `eq` comparison operator on the following properties: 
- ApplicationName
- ApplicationPublisher
- ApplicationShortVersion
- ApplicationVersion
- DeviceId
- DeviceName
- OSDescription
- OSVersion
- Platform
- UserId
- EmailAddress
- UserName

<!-- ## AppleDDMDeviceOSUpdateStatus

The following table contains the possible output when calling the `AppleDDMDeviceOSUpdateStatus` report:

| Available properties |
|-|
| CurrentBuildVersion |
| CurrentOSVersion |
| DeviceId |
| FailureCount |
| FailureReason |
| InstallReason |
| InstallState |
| LastReportedTime |
| LatestAvailableOSVersion |
| PendingBuildVersion |
| PendingOSVersion |
| TargetLocalDateTime |

There are no filters for this report. -->

<!-- ## AppleDDMOSUpdateFailures

The following table contains the possible output when calling the `AppleDDMOSUpdateFailures` report:

| Available properties |
|-|
| CurrentBuildVersion |
| CurrentOSVersion |
| DeclarationId |
| DeviceFamily |
| DeviceId |
| DeviceModelMarketingName |
| DeviceName |
| FailureCount |
| FailureReason |
| InstallReason |
| InstallState |
| LastFailureTime |
| LastReportedTime |
| LatestAvailableOSVersion |
| PendingBuildVersion |
| PendingOSVersion |
| SupplementalBuildVersion |
| SupplementalExtraVersion |
| TargetLocalDateTime |
| UserEmail |
| UserName |

There are no filters for this report. -->

<!-- ## AppleDDMOSVersionReport

The following table contains the possible output when calling the `AppleDDMOSVersionReport` report:

| Available properties |
|-|
| CurrentBuildVersion |
| CurrentOSVersion |
| DeclarationId |
| DeviceFamily |
| DeviceId |
| DeviceName |
| FailureCount |
| FailureReason |
| InstallReason |
| InstallState |
| IsDeviceUpToDate |
| IsRSRUpdateAvailable |
| LastReportedTime |
| LatestAvailableOSVersion |
| PendingBuildVersion |
| PendingOSVersion |
| SupplementalBuildVersion |
| SupplementalExtraVersion |
| TargetLocalDateTime |

There are no filters for this report. -->

<!-- ## AppleDDMSoftwareUpdatesSummary

The following table contains the possible output when calling the `AppleDDMSoftwareUpdatesSummary` report:

| Available properties |
|-|
| CountDevicesDownloading |
| CountDevicesFailed |
| CountDevicesInstalling |
| CountDevicesNotAssigned |
| CountDevicesPrepared |
| CountDevicesUpToDate |
| CountDevicesWaiting |
| DeviceFamily |

There are no filters for this report. -->

## AutopilotV1DeploymentStatus

The following table contains the possible output when calling the `AutopilotV1DeploymentStatus` report:

| Available properties |
|-|
| AccountSetupDuration |
| AutopilotProfileName |
| DeploymentDuration |
| DeploymentEndDateTime |
| DeploymentStartDateTime |
| DeploymentState |
| DeploymentTotalDuration |
| DeviceId |
| DeviceName |
| DeviceRegisteredDateTime |
| DeviceSerialNumber |
| DeviceSetupDuration |
| DeviceSetupStatus |
| EnrollmentDateTime |
| EnrollmentMethod |
| EnrollmentStatus |
| ESPPolicyId |
| ESPPolicyName |
| EspDeviceSetupFailureDetails |
| EspUserSetupFailureDetails |
| FailureDetails |
| FailureReason |
| OS |
| OSVersion |
| UPN |
| UserId |
| UserSetupStatus |

There are no filters for this report.

## AutopilotV2DeploymentStatus

The following table contains the possible output when calling the `AutopilotV2DeploymentStatus` report:

| Available properties |
|-|
| CurrentProvisioningPhase |
| DeploymentDurationTimeInSeconds |
| DeploymentStatus |
| DeviceId |
| DeviceName |
| EnrollmentTimeInUtc |
| Phase |
| ResultCode |
| SerialNumber |
| UPN |

There are no filters for this report.

## AutopilotV2DeploymentStatusDetailedAppInfo

The following table contains the possible output when calling the `AutopilotV2DeploymentStatusDetailedAppInfo` report:

| Available properties |
|-|
| ApplicationId |
| ApplicationName |
| AppType |
| DeviceId |
| IsAdminSelected |
| PolicyInstallStatus |

There are no filters for this report.

## AutopilotV2DeploymentStatusDetailedScriptInfo

The following table contains the possible output when calling the `AutopilotV2DeploymentStatusDetailedScriptInfo` report:

| Available properties |
|-|
| DeviceId |
| DisplayName |
| PolicyId |
| PolicyInstallStatus |

There are no filters for this report.

## BRBatteryByModel

The following table contains the possible output when calling the `BRBatteryByModel` report:

| Available properties |
|-|
| ActiveDevices |
| DeviceManufacturer |
| DeviceScopeId |
| InsertedDate |
| MemaTimeGeneratedTimeStamp |
| Model |
| ModelBatteryAge |
| ModelBatteryHealthScore |
| ModelCycleCount |
| ModelMaximumCapacity |
| ModelMedianCapacity |
| ModelMedianCycleCount |
| ModelMedianRuntime |
| ModelRuntime |
| NeedsAttention |
| PartnerFeaturesBitmask |
| RowCountInSnapshot |
| SchemaVersion |

You can choose to filter the `BRBatteryByModel` report's output based on the following columns:
- `DeviceScopeId`
- `PartnerFeaturesBitmask`
- `ActiveDevices`
- `ModelMaximumCapacity`
- `ModelRuntime`
- `ModelBatteryAge`
- `ModelCycleCount`
- `ModelMedianCapacity`
- `ModelMedianRuntime`
- `ModelMedianCycleCount`
- `ModelBatteryHealthScore`
- `NeedsAttention`

## BRBatteryByOs

The following table contains the possible output when calling the `BRBatteryByOs` report:

| Available properties |
|-|
| ActiveDevices |
| DeviceScopeId |
| InsertedDate |
| MemaTimeGeneratedTimeStamp |
| NeedsAttention |
| OsBatteryAge |
| OsBatteryHealthScore |
| OsBuildNumber |
| OsCycleCount |
| OsMaximumCapacity |
| OsMedianCapacity |
| OsMedianCycleCount |
| OsMedianRuntime |
| OsRuntime |
| OsVersion |
| PartnerFeaturesBitmask |
| RowCountInSnapshot |
| SchemaVersion |

You can choose to filter the `BRBatteryByOs` report's output based on the following columns:
- `DeviceScopeId`
- `PartnerFeaturesBitmask`
- `ActiveDevices`
- `OsMaximumCapacity`
- `OsRuntime`
- `OsBatteryAge`
- `OsCycleCount`
- `OsMedianCapacity`
- `OsMedianRuntime`
- `OsMedianCycleCount`
- `OsBatteryHealthScore`
- `NeedsAttention`

## BRDeviceBatteryAgg

The following table contains the possible output when calling the `BRDeviceBatteryAgg` report:

| Available properties |
|-|
| BatteryCapacityScore |
| BatteryHealthScore |
| BatteryId |
| BatteryManufacturer |
| BatteryRuntimeScore |
| Chemistry |
| CycleCount |
| DesignActiveRuntime |
| DesignCapacity |
| DesignConnectedStandByRuntime |
| DeviceBatteryCount |
| DeviceId |
| DeviceInsights |
| DeviceManufacturer |
| DeviceModel |
| DeviceName |
| DeviceOs |
| DeviceOsBuild |
| DeviceProperties |
| DeviceScopeIds |
| DeviceTags |
| EstimatedBatteryAge |
| FullChargeActiveRuntime |
| FullChargeCapacity |
| FullChargeStandByRuntime |
| InsertedDate |
| MaximumCapacity |
| MemaTimeGeneratedTimeStamp |
| NeedsAttention |
| PartnerFeaturesBitmask |
| RowCountInSnapshot |
| SchemaVersion |

You can choose to filter the `BRDeviceBatteryAgg` report's output based on the following columns:
- `DeviceScopeIds`
- `PartnerFeaturesBitmask`
- `MaximumCapacity`
- `FullChargeActiveRuntime`
- `EstimatedBatteryAge`
- `CycleCount`
- `DeviceBatteryCount`
- `BatteryHealthScore`
- `NeedsAttention`

## BREnergyUsage

The following table contains the possible output when calling the `BREnergyUsage` report:

| Available properties |
|-|
| ActiveDevices |
| AppFriendlyName |
| AppName |
| AppPublisher |
| BatteryUsageInPercentage |
| DeviceScopeId |
| InsertedDate |
| IsForeground |
| MemaTimeGeneratedTimeStamp |
| PartnerFeaturesBitmask |
| RowCountInSnapshot |
| SchemaVersion |
| TotalAppUsageDuration |

You can choose to filter the `BREnergyUsage` report's output based on the following columns:
- `DeviceScopeId`
- `PartnerFeaturesBitmask`
- `ActiveDevices`
- `IsForeground`
- `BatteryUsageInPercentage`

## CatalogAppsUpdateList

The following table contains the possible output when calling the `CatalogAppsUpdateList` report:

| Available properties |
|-|
| ApplicationId |
| ApplicationName |
| CurrentAppVersion |
| CurrentRevisionId |
| IsSuperseded |
| LatestAvailableVersion |
| LatestRevisionId |
| Publisher |
| UpdateAvailable |
| UpdateEligible |

There are no filters for this report.

## CertificatesByRAPolicy

The following table contains the possible output when calling the `CertificatesByRAPolicy` report:

| Available properties |
|-|
| CaConfiguration |
| CertificateStatus |
| DeviceId |
| DeviceName |
| EnhancedKeyUsage |
| IssuerName |
| KeyUsage |
| PolicyId |
| SerialNumber |
| SubjectName |
| Thumbprint |
| UPN |
| UserId |
| ValidFrom |
| ValidTo |

There are no filters for this report.

## ChromeOSDevices report

The following table contains the possible output when calling the `ChromeOSDevices` report:

|     Available properties  |
|-|
|     AutoUpdateExpiration  |
|     ChromeOSDeviceStatus  |
|     IntuneDeviceId  |
|     IntuneDeviceName  |
|     LastEnrollmentTime  |
|     LastOSUpdateTime  |
|     LastRebootTime  |
|     LastSyncFromGoogle  |
|     Model  |
|     MostRecentLogin  |
|     MostRecentUserEmail  |
|     OrganizationalUnitPath  |
|     OSVersion  |
|     SerialNumber  |
|     WifiMacAddress  |

To call this report, you'll need a minimum RBAC permission of **Read** for **Managed Devices**. The minimum Microsoft Graph Application required permission is `DeviceManagementManagedDevices.Read.All`.

> [!NOTE]
> The reporting data for this report is updated at a minimum of once per day.

The properties `LastOSUpdateTime` and `LastRebootTime` will only populate in the report when the **OS Update Status** setting is enabled in the Google Admin Console. This setting can be found in the Google Admin Console under **Devices** > **Chrome** **Settings**.

You can filter the `ChromeOSDevices` report using the following properties: 
- IntuneDeviceId
- MostRecentUserEmail
- MostRecentLogin
- OrganizationalUnitPath
- ChromeOSDeviceStatus

### Generate the ChromeOSDevices report

You can generate the ChromeOSDevices report using the Microsoft Graph API to make the HTTP call. Microsoft Graph is a RESTful web API that enables you to access Microsoft Cloud service resources.

| Microsoft Graph API Endpoint | Method | Body examples |
|---|---|---|
| `https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs` | POST | The following examples show different types of calls you can make based on the data you need to retrieve. This list is not comprehensive.<ul><li>Return all devices using CSV format:<br>`{ 'reportName': 'ChromeOSDevices', 'format': 'csv' }`</li><li>Return all devices using JSON format:<br>`{ 'reportName': 'ChromeOSDevices', 'format': 'json' }`</li><li>Use a filter:<br>`{ 'reportName': 'ChromeOSDevices', 'filter':'(ChromeOSDeviceStatus eq  'ACTIVE') ', 'format': 'csv' }`</li><li>Select which columns are included in the report:<br>`{ 'reportName': 'ChromeOSDevices', 'select':['IntuneDeviceId','IntuneDeviceName','MostRecentUserEmail']}`</li></ul>  |

### Check the status of the ChromeOSDevices report

You can check whether the ChromeOSDevices report has completed by using the Microsoft Graph API. 

| Microsoft Graph API Endpoint | Method | 
|---|---|
| `https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs('id') ` | GET |

Use the output from the above call to determine the status of the ChromeOSDevices report. An example call will look similar to the following:
`https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs('ChromeOSDevices_1223a321-4bcd-5432-efg1-0hi9876h1234') `

You can continue to run your call to check the status of the report. When the report shows a status of `complete`, your report is ready to be downloaded.

### Download the completed ChromeOSDevices report

You can download the completed ChromeOSDevices report by retrieving the `url` provided based on the same call you used to check the ChromeOSDevices report status. The download contains a zip file with the requested data that is formatted as CSV or JSON based on your selected format.

For more information about generating Intune reports, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

## ComanagedDeviceWorkloads

The following table contains the possible output when calling the `ComanagedDeviceWorkloads` report:

| Available   properties |
|-|
|   ClientRegistrationStatus    |
|   ComplianceState  |
|   DeviceId    |
|   DeviceName  |
|   DeviceType   |
|   IsDeviceActive   |
|   LastContact   |
|   OS   |
|   ReferenceId   |
|   SCCMCoManagementFeatures   |
|   UPN   |
|   UserEmail   |
|   UserName     |

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
|   ClientRegistrationStatus   |
|   CompliantState   |
|   DeviceId   |
|   DeviceName   |
|   DeviceRegistrationState   |
|   DeviceState   |
|   DeviceType   |
|   EntitySource   |
|   ManagedBy   |
|   ManagementAgents   |
|   ManagementState   |
|   Manufacturer   |
|   MDMStatus   |
|   Model   |
|   OS   |
|   OSDescription   |
|   OSVersion   |
|   OwnerType   |
|   Ownership   |
|   ReferenceId   |
|   SerialNumber   |
|   Status   |
|   UPN   |
|   UserEmail   |
|   UserId   |
|   UserName   |
|   _ComputedComplianceState   |

You can choose to filter the `ComanagementEligibilityTenantAttachedDevices` report's output based on the following columns:
- `Status`

## ConfigurationPolicyAggregate

The following table contains the possible output when calling the `ConfigurationPolicyAggregate` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| PolicyType |
| UnifiedPolicyType |
| PolicyBaseTypeName |
| PolicyPlatformType |
| NumberOfNotApplicableDevices |
| NumberOfCompliantDevices |
| NumberOfNonCompliantDevices |
| NumberOfErrorDevices |
| NumberOfConflictDevices |
| NumberOfNonCompliantOrErrorDevices |
| UnifiedPolicyPlatformType |
| TemplateVersion |

You can choose to filter the `ConfigurationPolicyAggregate` report's output based on the following columns:
- `UnifiedPolicyPlatformType`
- `UnifiedPolicyType`

## ConfigurationPolicyAggregateV3

The following table contains the possible output when calling the `ConfigurationPolicyAggregateV3` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| PolicyType |
| UnifiedPolicyType |
| PolicyBaseTypeName |
| PolicyPlatformType |
| NumberOfNotApplicableDevices |
| NumberOfCompliantDevices |
| NumberOfNonCompliantDevices |
| NumberOfErrorDevices |
| NumberOfConflictDevices |
| NumberOfNonCompliantOrErrorDevices |
| UnifiedPolicyPlatformType |
| TemplateVersion |

You can choose to filter the `ConfigurationPolicyAggregateV3` report's output based on the following columns:
- `UnifiedPolicyPlatformType`
- `UnifiedPolicyType`

## ConfigurationPolicyDeviceAggregates

The following table contains the possible output when calling the `ConfigurationPolicyDeviceAggregates` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| PolicyType |
| UnifiedPolicyType |
| PolicyBaseTypeName |
| PolicyPlatformType |
| NumberOfNotApplicableDevices |
| NumberOfCompliantDevices |
| NumberOfNonCompliantDevices |
| NumberOfErrorDevices |
| NumberOfConflictDevices |
| NumberOfNonCompliantOrErrorDevices |
| NumberOfInProgressDevices |
| NumberOfRemovedDevices |
| UnifiedPolicyPlatformType |
| TemplateVersion |
| ProfileSource |

You can choose to filter the `ConfigurationPolicyDeviceAggregates` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`

## ConfigurationPolicyDeviceAggregatesV3

The following table contains the possible output when calling the `ConfigurationPolicyDeviceAggregatesV3` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| PolicyType |
| UnifiedPolicyType |
| PolicyBaseTypeName |
| PolicyPlatformType |
| NumberOfNotApplicableDevices |
| NumberOfCompliantDevices |
| NumberOfNonCompliantDevices |
| NumberOfErrorDevices |
| NumberOfConflictDevices |
| NumberOfNonCompliantOrErrorDevices |
| NumberOfInProgressDevices |
| NumberOfRemovedDevices |
| UnifiedPolicyPlatformType |
| TemplateVersion |
| ProfileSource |

You can choose to filter the `ConfigurationPolicyDeviceAggregatesV3` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`

## ConfigurationPolicyDeviceAggregatesWithPF

The following table contains the possible output when calling the `ConfigurationPolicyDeviceAggregatesWithPF` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| PolicyType |
| UnifiedPolicyType |
| PolicyBaseTypeName |
| PolicyPlatformType |
| NumberOfNotApplicableDevices |
| NumberOfCompliantDevices |
| NumberOfNonCompliantDevices |
| NumberOfErrorDevices |
| NumberOfConflictDevices |
| NumberOfNonCompliantOrErrorDevices |
| NumberOfInProgressDevices |
| NumberOfRemovedDevices |
| UnifiedPolicyPlatformType |
| TemplateVersion |
| ProfileSource |

You can choose to filter the `ConfigurationPolicyDeviceAggregatesWithPF` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`

## ConfigurationPolicyDeviceAggregatesWithPFV3

The following table contains the possible output when calling the `ConfigurationPolicyDeviceAggregatesWithPFV3` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| PolicyType |
| UnifiedPolicyType |
| PolicyBaseTypeName |
| PolicyPlatformType |
| NumberOfNotApplicableDevices |
| NumberOfCompliantDevices |
| NumberOfNonCompliantDevices |
| NumberOfErrorDevices |
| NumberOfConflictDevices |
| NumberOfNonCompliantOrErrorDevices |
| NumberOfInProgressDevices |
| NumberOfRemovedDevices |
| UnifiedPolicyPlatformType |
| TemplateVersion |
| ProfileSource |

You can choose to filter the `ConfigurationPolicyDeviceAggregatesWithPFV3` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`

## DefenderAgents

The following table contains the possible output when calling the `DefenderAgents` report:

| Available properties |
|-|
| DeviceId |
| DeviceName |
| DeviceState |
| IsVirtualMachine |
| LastReportedDateTime |
| MalwareProtectionEnabled |
| NetworkInspectionSystemEnabled |
| ProductStatus |
| RealTimeProtectionEnabled |
| SignatureUpdateOverdue |
| TamperProtectionEnabled |
| UPN |
| UserEmail |
| UserName |
| _ManagedBy |

You can choose to filter the `DefenderAgents` report's output based on the following columns:
- `DeviceState`
- `SignatureUpdateOverdue`
- `MalwareProtectionEnabled`
- `RealTimeProtectionEnabled`
- `NetworkInspectionSystemEnabled`

## DependentAppsInstallStatus

The following table contains the possible output when calling the `DependentAppsInstallStatus` report:

| Available properties |
|-|
| ApplicationId |
| AppVersion |
| DeviceId |
| DisplayName |
| ErrorCode |
| InstallState |
| InstallStateDetail |
| LastModifiedDateTime |
| Relationship |
| Replaced |
| SourceIds |
| UserId |
| UserPrincipalName |

There are no filters for this report.

## DeviceAssignmentStatusByConfigurationPolicy

The following table contains the possible output when calling the `DeviceAssignmentStatusByConfigurationPolicy` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| IntuneDeviceId |
| DeviceName |
| AadDeviceId |
| UPN |
| AssignmentStatus |
| PspdpuLastModifiedTimeUtc |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| AssignmentFilterIds |
| TemplateVersion |
| ReportStatus |

You can choose to filter the `DeviceAssignmentStatusByConfigurationPolicy` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `UnifiedPolicyPlatformType`
- `AssignmentStatus`

## DeviceAssignmentStatusByConfigurationPolicyForAC

The following table contains the possible output when calling the `DeviceAssignmentStatusByConfigurationPolicyForAC` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| IntuneDeviceId |
| DeviceName |
| AadDeviceId |
| UPN |
| AssignmentStatus |
| PspdpuLastModifiedTimeUtc |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| AssignmentFilterIds |
| TemplateVersion |
| ReportStatus |

You can choose to filter the `DeviceAssignmentStatusByConfigurationPolicyForAC` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `UnifiedPolicyPlatformType`
- `AssignmentStatus`

## DeviceAssignmentStatusByConfigurationPolicyForASR

The following table contains the possible output when calling the `DeviceAssignmentStatusByConfigurationPolicyForASR` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| IntuneDeviceId |
| DeviceName |
| AadDeviceId |
| UPN |
| AssignmentStatus |
| PspdpuLastModifiedTimeUtc |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| AssignmentFilterIds |
| TemplateVersion |
| ReportStatus |

You can choose to filter the `DeviceAssignmentStatusByConfigurationPolicyForASR` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `UnifiedPolicyPlatformType`
- `AssignmentStatus`

## DeviceAssignmentStatusByConfigurationPolicyForEDR

The following table contains the possible output when calling the `DeviceAssignmentStatusByConfigurationPolicyForEDR` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| IntuneDeviceId |
| DeviceName |
| AadDeviceId |
| UPN |
| AssignmentStatus |
| PspdpuLastModifiedTimeUtc |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| AssignmentFilterIds |
| TemplateVersion |
| ReportStatus |

You can choose to filter the `DeviceAssignmentStatusByConfigurationPolicyForEDR` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `UnifiedPolicyPlatformType`
- `AssignmentStatus`

## DeviceAssignmentStatusByConfigurationPolicyV3

The following table contains the possible output when calling the `DeviceAssignmentStatusByConfigurationPolicyV3` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| IntuneDeviceId |
| DeviceName |
| AadDeviceId |
| UPN |
| AssignmentStatus |
| PspdpuLastModifiedTimeUtc |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| AssignmentFilterIds |
| TemplateVersion |
| ReportStatus |

You can choose to filter the `DeviceAssignmentStatusByConfigurationPolicyV3` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `UnifiedPolicyPlatformType`
- `AssignmentStatus`

## DeviceCompliance

The following table contains the possible output when calling the `DeviceCompliance` report:

| Available properties |
|-|
| AadDeviceId |
| ComplianceState |
| DeviceHealthThreatLevel |
| DeviceId |
| DeviceName |
| DeviceType |
| IMEI |
| InGracePeriodUntil |
| IntuneDeviceId |
| LastContact |
| OS |
| OSDescription |
| OSVersion |
| OwnerType |
| PartnerDeviceId |
| PrimaryUser |
| RetireAfterDatetime |
| SerialNumber |
| UPN |
| UserEmail |
| UserId |
| UserName |

You can choose to filter the `DeviceCompliance` report's output based on the following columns:
- `ComplianceState`
- `OS`
- `OwnerType`
- `DeviceType`

## DeviceComplianceTrend

The following table contains the possible output when calling the `DeviceComplianceTrend` report:

| Available properties |
|-|
| ComplianceState |
| Count |
| Date |
| DeviceType |
| OSFamily |
| OwnerType |

There are no filters for this report.

## DeviceConfigurationPolicyStatuses

The following table contains the possible output when calling the `DeviceConfigurationPolicyStatuses` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| IntuneDeviceId |
| DeviceName |
| Manufacturer |
| Model |
| UPN |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| AssignmentFilterIds |
| TemplateVersion |
| ReportStatus |

You can choose to filter the `DeviceConfigurationPolicyStatuses` report's output based on the following columns:
- `IntuneDeviceId`
- `PolicyBaseTypeName`

## DeviceConfigurationPolicyStatusesV3

The following table contains the possible output when calling the `DeviceConfigurationPolicyStatusesV3` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| IntuneDeviceId |
| DeviceName |
| Manufacturer |
| Model |
| UPN |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| AssignmentFilterIds |
| TemplateVersion |
| ReportStatus |

You can choose to filter the `DeviceConfigurationPolicyStatusesV3` report's output based on the following columns:
- `IntuneDeviceId`
- `PolicyBaseTypeName`

## DeviceConfigurationPolicyStatusesWithPF

The following table contains the possible output when calling the `DeviceConfigurationPolicyStatusesWithPF` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| IntuneDeviceId |
| DeviceName |
| Manufacturer |
| Model |
| UPN |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| AssignmentFilterIds |
| TemplateVersion |
| ReportStatus |

You can choose to filter the `DeviceConfigurationPolicyStatusesWithPF` report's output based on the following columns:
- `IntuneDeviceId`
- `PolicyBaseTypeName`

## DeviceConfigurationPolicyStatusesWithPFV3

The following table contains the possible output when calling the `DeviceConfigurationPolicyStatusesWithPFV3` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |
| IntuneDeviceId |
| DeviceName |
| Manufacturer |
| Model |
| UPN |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| AssignmentFilterIds |
| TemplateVersion |
| ReportStatus |

You can choose to filter the `DeviceConfigurationPolicyStatusesWithPFV3` report's output based on the following columns:
- `IntuneDeviceId`
- `PolicyBaseTypeName`

## DeviceEnrollmentFailures

The following table contains the possible output when calling the `DeviceEnrollmentFailures` report:

| Available properties |
|-|
| EnrollmentFailureDateTime |
| EnrollmentMethod |
| FailureGuid |
| FailureReason |
| OS |
| OSVersion |
| UPN |
| UserId |

You can choose to filter the `DeviceEnrollmentFailures` report's output based on the following columns:
- `EnrollmentFailureDateTime`
- `OS`
- `FailureReason`
- `EnrollmentMethod`
- `UserId`

## DeviceFailuresByFeatureUpdatePolicy

The following table contains the possible output when calling the `DeviceFailuresByFeatureUpdatePolicy` report:

| Available properties  |
|-|
|     AADDeviceId  |
|     AlertClassification  |
|     AlertId  |
|     AlertMessage  |
|     AlertMessageData  |
|     AlertMessageDescription  |
|     AlertStatus  |
|     AlertType  |
|     Build  |
|     DeviceId  |
|     DeviceName  |
|     EventDateTimeUTC  |
|     ExtendedRecommendedAction  |
|     FeatureUpdateVersion  |
|     LastUpdatedAlertStatusDateTimeUTC  |
|     PolicyId  |
|     PolicyName  |
|     RecommendedAction  |
|     ResolvedDateTimeUTC  |
|     StartDateTimeUTC  |
|     UPN  |
|     Win32ErrorCode  |
|     WindowsUpdateVersion     |

You can choose to filter the `DeviceFailuresByFeatureUpdatePolicy` report's output based on the following columns:
- `PolicyId` **(Required)**
- `AlertMessage`
- `RecommendedAction`
- `WindowsUpdateVersion`

## DeviceInstallStatusByApp

The following table contains the possible output when calling the `DeviceInstallStatusByApp` report:

| Available   properties |
|-|
| AppInstallState |
| AppInstallStateDetails |
| ApplicationId |
| AppVersion |
| AssignmentFilterIdsExist |
| DeviceId |
| DeviceName |
| ErrorCode |
| HexErrorCode |
| InstallState |
| InstallStateDetail |
| LastModifiedDateTime |
| Platform |
| UserId |
| UserName |
| UserPrincipalName |

You can choose to filter the `DeviceInstallStatusByApp` report's output based on the following columns:
- `ApplicationId` **(Required)**
- `AppInstallState`
- `HexErrorCode` (Used as ErrorCode)

## DeviceIntentPerSettingStatus

The following table contains the possible output when calling the `DeviceIntentPerSettingStatus` report:

| Available properties |
|-|
| LocalizedSettingName |
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| NumberOfNonCompliantDevices |
| NumberOfNotApplicableDevices |
| NumberOfRemediatedDevices |
| NumberOfUnknownDevices |
| PolicyId |
| SettingId |
| SettingName |

You can choose to filter the `DeviceIntentPerSettingStatus` report's output based on the following columns:
- `PolicyId`

## DeviceInventoryPolicyStatusesV3

The following table contains the possible output when calling the `DeviceInventoryPolicyStatusesV3` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `DeviceInventoryPolicyStatusesV3` report's output based on the following columns:
- `IntuneDeviceId`
- `PolicyBaseTypeName`

## DeviceInventoryPolicyStatusesWithPF

The following table contains the possible output when calling the `DeviceInventoryPolicyStatusesWithPF` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `DeviceInventoryPolicyStatusesWithPF` report's output based on the following columns:
- `IntuneDeviceId`
- `PolicyBaseTypeName`

## DeviceNonCompliance

The following table contains the possible output when calling the `DeviceNonCompliance` report:

|     Available properties  |
|-|
| AadDeviceId   |
| ComplianceState |
| DeviceHealthThreatLevel   |
| DeviceId  |
| DeviceName   |
| DeviceType   |
| IMEI   |
| InGracePeriodUntil   |
| IntuneDeviceId   |
| LastContact   |
| OS |
| OSDescription   |
| OSVersion   |
| OwnerType   |
| PartnerDeviceId   |
| PrimaryUser   |
| RetireAfterDatetime   |
| SerialNumber   |
| UPN   |
| UserEmail   |
| UserId     |
| UserName   |

You can choose to filter the `DeviceNonCompliance` report's output based on the following columns:
- `OS`
- `OwnerType`
- `DeviceType`
- `UserId`
- `ComplianceState`

## DevicePoliciesComplianceReport

The following table contains the possible output when calling the `DevicePoliciesComplianceReport` report:

| Available properties |
|-|
| DeviceId |
| LastContact |
| PolicyId |
| PolicyName |
| PolicyPlatformType |
| PolicyStatus |
| PolicyVersion |
| UPN |
| UserEmail |
| UserId |
| UserName |

There are no filters for this report.

## DevicePoliciesComplianceReportV3

The following table contains the possible output when calling the `DevicePoliciesComplianceReportV3` report:

| Available properties |
|-|
| DeviceId |
| LastContact |
| PolicyId |
| PolicyName |
| PolicyPlatformType |
| PolicyStatus |
| PolicyVersion |
| UPN |
| UserEmail |
| UserId |
| UserName |

There are no filters for this report.

## DevicePolicySettingsComplianceReport

The following table contains the possible output when calling the `DevicePolicySettingsComplianceReport` report:

| Available properties |
|-|
| DeviceId |
| ErrorCode |
| ErrorType |
| PolicyId |
| PolicyVersion |
| SettingId |
| SettingInstanceId |
| SettingName |
| SettingNm |
| SettingStatus |
| SettingValue |
| StateDetails |
| UserId |

There are no filters for this report.

## DevicePolicySettingsComplianceReportV3

The following table contains the possible output when calling the `DevicePolicySettingsComplianceReportV3` report:

| Available properties |
|-|
| DeviceId |
| ErrorCode |
| ErrorType |
| PolicyId |
| PolicyVersion |
| SettingId |
| SettingInstanceId |
| SettingName |
| SettingNm |
| SettingStatus |
| SettingValue |
| StateDetails |
| UserId |

There are no filters for this report.

## DeviceRunStatesByProactiveRemediation

The following table contains the possible output when calling the `DeviceRunStatesByProactiveRemediation` report:

| Available   properties |
|-|
|   DetectionScriptStatus   |
|   DetectionStatus   |
|   DeviceId   |
|   DeviceName   |
|   DisplayName   |
|   FilterIdsCSV   |
|   InternalVersion   |
|   JoinType   |
|   LastAgentUpdateTime   |
|   Model   |
|   ModifiedTime   |
|   NextExecutionDateTime   |
|   OSDescription   |
|   OSVersion   |
|   PolicyId   |
|   PostRemediationDetectionScriptError   |
|   PostRemediationDetectionScriptOutput   |
|   PreRemediationDetectionScriptError   |
|   PreRemediationDetectionScriptOutput   |
|   PrimaryUser   |
|   RemediationScriptErrorDetails   |
|   RemediationScriptOutputDetails   |
|   RemediationScriptStatus   |
|   RemediationStatus   |
|   UniqueKustoKey   |
|   UPN   |
|   UserEmail   |
|   UserId   |
|   UserName   |

You can choose to filter the `DeviceRunStatesByProactiveRemediation` report's output based on the following columns:
- `PolicyId` **(required)**
- `RemediationStatus`
- `DetectionStatus`

## DeviceRunStatesByScript

The following table contains the possible output when calling the `DeviceRunStatesByScript` report:

| Available properties |
|-|
| DeviceId |
| DeviceName |
| ErrorCode |
| ErrorDescription |
| ModifiedTime |
| OSVersion |
| PolicyId |
| PolicyResultDetail |
| PolicyResultState |
| PolicyVersion |
| RunState |
| UPN |
| UserEmail |
| UserId |
| UserName |

There are no filters for this report.

## Devices

The following table contains the possible output when calling the `Devices` report:

|     Available properties |
|-|
| AndroidPatchLevel  |
| CategoryId  |
| CategoryName  |
| CertExpirationDate  |
| ClientRegistrationStatus  |
| CompliantState  |
| CreatedDate  |
| DeviceEnrollmentType  |
| DeviceId  |
| DeviceName  |
| DeviceRegistrationState  |
| DeviceState  |
| DeviceType  |
| EasAccessState  |
| EasActivationStatus  |
| EasID  |
| EasLastSyncSuccessUtc  |
| EasStateReason  |
| EncryptionStatus  |
| EncryptionStatusString  |
| EnrolledByUser  |
| EnrollmentType  |
| EntitySource  |
| ExtendedProperties  |
| GraphDeviceIsManaged  |
| HasUnlockToken  |
| IMEI  |
| InGracePeriodUntil  |
| IsManaged  |
| JailBroken  |
| JoinType  |
| LastContact  |
| LastLoggedOnUserUPN  |
| ManagedBy  |
| ManagedDeviceName  |
| ManagementAgents  |
| ManagementState  |
| Manufacturer  |
| MDMStatus  |
| MDMWinsOverGPStartTime  |
| MEID  |
| Model  |
| OS  |
| OSVersion  |
| Ownership  |
| OwnerType  |
| PhoneNumber  |
| PrimaryUser  |
| ReferenceId  |
| RetireAfterDatetime  |
| SCCMCoManagementFeatures  |
| SerialNumber  |
| SkuFamily  |
| SkuNumber  |
| StagedDeviceType  |
| StorageFree  |
| StorageTotal  |
| SubscriberCarrierNetwork  |
| SupervisedStatus  |
| SupervisedStatusString  |
| UPN  |
| UserApprovedEnrollment  |
| UserEmail  |
| UserId  |
| UserName  |
| WifiMacAddress        |

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

## DevicesByAppInv

The following table contains the possible output when calling the `DevicesByAppInv` report:

|     Available properties  |
|-|
|     ApplicationId  |
|     ApplicationKey  |
|     ApplicationName  |
|     ApplicationPublisher  |
|     ApplicationShortVersion  |
|     ApplicationVersion  |
|     DeviceId  |
|     DeviceName  |
|     EmailAddress  |
|     OSDescription  |
|     OSVersion  |
|     Platform  |
|     UserId  |
|     UserName  |

You can choose to filter the `DevicesByAppInv` report's output based on the following column:
- `ApplicationKey` **(Required)**

## DevicesStatusByPolicyPlatformComplianceReport

The following table contains the possible output when calling the `DevicesStatusByPolicyPlatformComplianceReport` report:

| Available properties |
|-|
| AadDeviceId |
| ComplianceState |
| DeviceId |
| DeviceName |
| InGracePeriodUntil |
| LastContact |
| Model |
| OS |
| PolicyId |
| PolicyPlatformType |
| PolicyStatus |
| UPN |

There are no filters for this report.

## DevicesStatusByPolicyPlatformComplianceReportV3

The following table contains the possible output when calling the `DevicesStatusByPolicyPlatformComplianceReportV3` report:

| Available properties |
|-|
| AadDeviceId |
| ComplianceState |
| DeviceId |
| DeviceName |
| InGracePeriodUntil |
| LastContact |
| Model |
| OS |
| PolicyId |
| PolicyPlatformType |
| PolicyStatus |
| UPN |

There are no filters for this report.

## DevicesStatusBySettingReport

The following table contains the possible output when calling the `DevicesStatusBySettingReport` report:

| Available properties |
|-|
| AadDeviceId |
| ComplianceState |
| DeviceId |
| DeviceName |
| InGracePeriodUntil |
| Model |
| OS |
| PolicyPlatformType |
| PrimaryUser |
| SettingId |
| SettingName |
| SettingNm |
| SettingStatus |
| UPN |

There are no filters for this report.

## DevicesStatusBySettingReportV3

The following table contains the possible output when calling the `DevicesStatusBySettingReportV3` report:

| Available properties |
|-|
| AadDeviceId |
| ComplianceState |
| DeviceId |
| DeviceName |
| InGracePeriodUntil |
| Model |
| OS |
| PolicyPlatformType |
| PrimaryUser |
| SettingId |
| SettingName |
| SettingNm |
| SettingStatus |
| UPN |

There are no filters for this report.

## DeviceStatusByCompliacePolicyReport

The following table contains the possible output when calling the `DeviceStatusByCompliacePolicyReport` report:

| Available properties |
|-|
| AadDeviceId |
| DeviceId |
| DeviceName |
| LastContact |
| ManagementAgents |
| OS |
| PolicyId |
| PolicyStatus |
| UPN |
| UserId |
| UserName |

There are no filters for this report.

## DeviceStatusByCompliacePolicyReportV3

The following table contains the possible output when calling the `DeviceStatusByCompliacePolicyReportV3` report:

| Available properties |
|-|
| AadDeviceId |
| DeviceId |
| DeviceName |
| LastContact |
| ManagementAgents |
| OS |
| PolicyId |
| PolicyStatus |
| UPN |
| UserId |
| UserName |

There are no filters for this report.

## DeviceStatusByCompliancePolicySettingReport

The following table contains the possible output when calling the `DeviceStatusByCompliancePolicySettingReport` report:

| Available properties |
|-|
| AadDeviceId |
| ComplianceState |
| DeviceId |
| DeviceName |
| ManagementAgents |
| Model |
| OS |
| PolicyId |
| SettingId |
| SettingName |
| SettingNm |
| SettingStatus |
| UPN |

There are no filters for this report.

## DeviceStatusByCompliancePolicySettingReportV3

The following table contains the possible output when calling the `DeviceStatusByCompliancePolicySettingReportV3` report:

| Available properties |
|-|
| AadDeviceId |
| ComplianceState |
| DeviceId |
| DeviceName |
| ManagementAgents |
| Model |
| OS |
| PolicyId |
| SettingId |
| SettingName |
| SettingNm |
| SettingStatus |
| UPN |

There are no filters for this report.

## DeviceStatusesByConfigurationProfile

The following table contains the possible output when calling the `DeviceStatusesByConfigurationProfile` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `DeviceStatusesByConfigurationProfile` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `PolicyStatus`
- `PolicyTypeName`

## DeviceStatusesByConfigurationProfileForAppControl

The following table contains the possible output when calling the `DeviceStatusesByConfigurationProfileForAppControl` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `DeviceStatusesByConfigurationProfileForAppControl` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `PolicyStatus`
- `PolicyTypeName`

## DeviceStatusesByConfigurationProfileForASR

The following table contains the possible output when calling the `DeviceStatusesByConfigurationProfileForASR` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `DeviceStatusesByConfigurationProfileForASR` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `PolicyStatus`
- `PolicyTypeName`

## DeviceStatusesByConfigurationProfileForEDR

The following table contains the possible output when calling the `DeviceStatusesByConfigurationProfileForEDR` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `DeviceStatusesByConfigurationProfileForEDR` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `PolicyStatus`
- `PolicyTypeName`

## DeviceStatusesByConfigurationProfileV3

The following table contains the possible output when calling the `DeviceStatusesByConfigurationProfileV3` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `DeviceStatusesByConfigurationProfileV3` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `PolicyStatus`
- `PolicyTypeName`

## DeviceStatusesByConfigurationProfileWithPF

The following table contains the possible output when calling the `DeviceStatusesByConfigurationProfileWithPF` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `DeviceStatusesByConfigurationProfileWithPF` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `PolicyStatus`
- `PolicyTypeName`

## DeviceStatusesByConfigurationProfileWithPFV3

The following table contains the possible output when calling the `DeviceStatusesByConfigurationProfileWithPFV3` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `DeviceStatusesByConfigurationProfileWithPFV3` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `PolicyStatus`
- `PolicyTypeName`

## DeviceStatusesByInventoryPolicyWithPF

The following table contains the possible output when calling the `DeviceStatusesByInventoryPolicyWithPF` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `DeviceStatusesByInventoryPolicyWithPF` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `PolicyStatus`
- `PolicyTypeName`

## DeviceStatusesByInventoryPolicyWithPFV3

The following table contains the possible output when calling the `DeviceStatusesByInventoryPolicyWithPFV3` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `DeviceStatusesByInventoryPolicyWithPFV3` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`
- `PolicyStatus`
- `PolicyTypeName`

## DeviceStatusSummaryByCompliacePolicyReport

The following table contains the possible output when calling the `DeviceStatusSummaryByCompliacePolicyReport` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfNonCompliantDevices |
| NumberOfOtherDevices |
| OS |
| PolicyId |

There are no filters for this report.

## DeviceStatusSummaryByCompliacePolicyReportV3

The following table contains the possible output when calling the `DeviceStatusSummaryByCompliacePolicyReportV3` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfNonCompliantDevices |
| NumberOfOtherDevices |
| OS |
| PolicyId |

There are no filters for this report.

## DeviceStatusSummaryByCompliancePolicySettingsReport

The following table contains the possible output when calling the `DeviceStatusSummaryByCompliancePolicySettingsReport` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfErrorDevices |
| NumberOfNonCompliantDevices |
| NumberOfNotApplicableDevices |
| NumberOfNotEvaluatedDevices |
| NumberOfOtherDevices |
| PolicyId |
| SettingId |
| SettingName |
| SettingNm |

There are no filters for this report.

## DeviceStatusSummaryByCompliancePolicySettingsReportV3

The following table contains the possible output when calling the `DeviceStatusSummaryByCompliancePolicySettingsReportV3` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfErrorDevices |
| NumberOfNonCompliantDevices |
| NumberOfNotApplicableDevices |
| NumberOfNotEvaluatedDevices |
| NumberOfOtherDevices |
| PolicyId |
| SettingId |
| SettingName |
| SettingNm |

There are no filters for this report.

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
| ReferenceId  | Microsoft Entra Device ID  |
| OSVersion  | OS version  |
| GraphDeviceIsManaged  | Microsoft Entra registered  |
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

The `ProcessorArchitecture` mappings for Windows 10+ are the following:
- 9 = x64
- 5 = ARM
- 12 = ARM64
- 0 = x86
- default = Unknown

The `ProcessorArchitecture` mappings for macOS are the following:
- 9 = x64
- 12 = ARM64
- default = unknown

## DevicesWithoutCompliancePolicy

The following table contains the possible output when calling the `DevicesWithoutCompliancePolicy` report:

| Available properties |
|-|
| AadDeviceId |
| ComplianceState |
| DeviceId |
| DeviceModel |
| DeviceName |
| DeviceType |
| LastContact |
| LastContactedUserId |
| ManagementAgents |
| OS |
| OSDescription |
| OSVersion |
| OwnerType |
| PrimaryUser |
| UPN |
| UserEmail |
| UserId |
| UserName |

There are no filters for this report.

## DevicesWithoutCompliancePolicyV3

The following table contains the possible output when calling the `DevicesWithoutCompliancePolicyV3` report:

| Available properties |
|-|
| AadDeviceId |
| ComplianceState |
| DeviceId |
| DeviceModel |
| DeviceName |
| DeviceType |
| LastContact |
| LastContactedUserId |
| ManagementAgents |
| OS |
| OSDescription |
| OSVersion |
| OwnerType |
| PrimaryUser |
| UPN |
| UserEmail |
| UserId |
| UserName |

There are no filters for this report.

## DriverUpdatePolicyStatusSummary

The following table contains the possible output when calling the `DriverUpdatePolicyStatusSummary` report:

| Available properties |
|-|
| CountDevicesCancelledStatus |
| CountDevicesErrorStatus |
| CountDevicesInProgressStatus |
| CountDevicesSuccessStatus |
| CountOfNeedsReviewDrivers |
| CountOfPausedDrivers |
| PolicyId |
| PolicyName |

There are no filters for this report.

## EAAnomalyAsset

The following table contains the possible output when calling the `EAAnomalyAsset` report:

| Available properties |
|-|
| AnomalyFirstOccurrenceDateTime |
| AnomalyId |
| AnomalyLatestOccurrenceDateTime |
| AnomalyName |
| AnomalyType |
| AssetName |
| AssetPublisher |
| AssetVersion |
| DetectionModelId |
| DeviceImpactedCount |
| IssueId |
| Severity |
| State |

You can choose to filter the `EAAnomalyAsset` report's output based on the following columns:
- `Severity`
- `State`
- `DeviceImpactedCount`
- `AnomalyFirstOccurrenceDateTime`
- `AnomalyLatestOccurrenceDateTime`

## EAAnomalyAssetV2

The following table contains the possible output when calling the `EAAnomalyAssetV2` report:

| Available properties |
|-|
| AnomalyFirstOccurrenceDateTime |
| AnomalyId |
| AnomalyLatestOccurrenceDateTime |
| AnomalyName |
| AnomalyType |
| AssetName |
| AssetPublisher |
| AssetVersion |
| DetectionModelId |
| DeviceImpactedCount |
| IssueId |
| Severity |
| State |

You can choose to filter the `EAAnomalyAssetV2` report's output based on the following columns:
- `Severity`
- `State`
- `DeviceImpactedCount`
- `AnomalyFirstOccurrenceDateTime`
- `AnomalyLatestOccurrenceDateTime`

## EAAnomalyDeviceAsset

The following table contains the possible output when calling the `EAAnomalyDeviceAsset` report:

| Available properties |
|-|
| AnomalyId |
| AnomalyOnDeviceFirstOccurrenceDateTime |
| AnomalyOnDeviceLatestOccurrenceDateTime |
| DeviceId |
| DeviceManufacturer |
| DeviceModel |
| DeviceName |
| OsName |
| OsVersion |

You can choose to filter the `EAAnomalyDeviceAsset` report's output based on the following columns:
- `AnomalyId`
- `AnomalyOnDeviceFirstOccurrenceDateTime`
- `AnomalyOnDeviceLatestOccurrenceDateTime`

## EAAnomalyDeviceAssetV2

The following table contains the possible output when calling the `EAAnomalyDeviceAssetV2` report:

| Available properties |
|-|
| AnomalyId |
| AnomalyOnDeviceFirstOccurrenceDateTime |
| AnomalyOnDeviceLatestOccurrenceDateTime |
| CohortId |
| DeviceId |
| DeviceManufacturer |
| DeviceModel |
| DeviceName |
| DeviceStatus |
| OsName |
| OsVersion |

You can choose to filter the `EAAnomalyDeviceAssetV2` report's output based on the following columns:
- `AnomalyId`
- `AnomalyOnDeviceFirstOccurrenceDateTime`
- `AnomalyOnDeviceLatestOccurrenceDateTime`
- `CohortId`

## EAAppPerformance

The following table contains the possible output when calling the `EAAppPerformance` report:

| Available properties |
|-|
| ActiveDevices |
| AllOrgsHealthScore |
| AllOrgsMeanTimeToFailure |
| AppFriendlyName |
| AppHealthScore |
| AppHealthStatus |
| AppName |
| AppPublisher |
| DeviceScopeId |
| MeanTimeToFailure |
| MemaTimeGenerated |
| PartnerFeaturesBitmask |
| RowCountInSnapshot |
| SchemaVersion |
| TotalAppCrashes |
| TotalAppHangs |
| TotalAppUsageDuration |

You can choose to filter the `EAAppPerformance` report's output based on the following columns:
- `DeviceScopeId`
- `PartnerFeaturesBitmask`
- `ActiveDevices`
- `TotalAppUsageDuration`
- `TotalAppCrashes`
- `MeanTimeToFailure`
- `AppHealthScore`

## EADeviceModelPerformance

The following table contains the possible output when calling the `EADeviceModelPerformance` report:

| Available properties |
|-|
| ActiveDevices |
| DeviceManufacturer |
| DeviceModel |
| DeviceScopeId |
| HealthStatus |
| MeanTimeToFailure |
| MemaTimeGenerated |
| ModelAppHealthScore |
| ModelAppHealthStatus |
| PartnerFeaturesBitmask |
| RowCountInSnapshot |
| SchemaVersion |
| TargetSnapshotId |

You can choose to filter the `EADeviceModelPerformance` report's output based on the following columns:
- `DeviceScopeId`
- `PartnerFeaturesBitmask`
- `ActiveDevices`
- `MeanTimeToFailure`
- `ModelAppHealthScore`
- `HealthStatus`

## EADeviceModelPerformanceV2

The following table contains the possible output when calling the `EADeviceModelPerformanceV2` report:

| Available properties |
|-|
| ActiveDevices |
| DeviceManufacturer |
| DeviceModel |
| DeviceScopeId |
| HealthStatus |
| MeanTimeToFailure |
| MemaTimeGenerated |
| ModelAppHealthScore |
| ModelAppHealthStatus |
| PartnerFeaturesBitmask |
| RowCountInSnapshot |
| SchemaVersion |
| TargetSnapshotId |

You can choose to filter the `EADeviceModelPerformanceV2` report's output based on the following columns:
- `DeviceScopeId`
- `PartnerFeaturesBitmask`
- `ActiveDevices`
- `MeanTimeToFailure`
- `ModelAppHealthScore`
- `HealthStatus`

## EADevicePerformance

The following table contains the possible output when calling the `EADevicePerformance` report:

| Available properties |
|-|
| DeviceAppHealthScore |
| DeviceAppHealthStatus |
| DeviceId |
| DeviceManufacturer |
| DeviceModel |
| DeviceName |
| DeviceScopeIds |
| DistinctAppsWithCrashes |
| HealthStatus |
| MeanTimeToFailure |
| MemaTimeGenerated |
| PartnerFeaturesBitmask |
| ProcessedDateTime |
| RowCountInSnapshot |
| SchemaVersion |
| TargetSnapshotId |
| TotalAppCrashes |
| TotalAppHangs |

You can choose to filter the `EADevicePerformance` report's output based on the following columns:
- `DeviceScopeIds`
- `PartnerFeaturesBitmask`
- `DeviceId`
- `TotalAppCrashes`
- `MeanTimeToFailure`
- `DeviceAppHealthScore`
- `HealthStatus`

## EADevicePerformanceV2

The following table contains the possible output when calling the `EADevicePerformanceV2` report:

| Available properties |
|-|
| DeviceAppHealthScore |
| DeviceAppHealthStatus |
| DeviceId |
| DeviceManufacturer |
| DeviceModel |
| DeviceName |
| DeviceScopeIds |
| DistinctAppsWithCrashes |
| HealthStatus |
| MeanTimeToFailure |
| MemaTimeGenerated |
| PartnerFeaturesBitmask |
| ProcessedDateTime |
| RowCountInSnapshot |
| SchemaVersion |
| TargetSnapshotId |
| TotalAppCrashes |
| TotalAppHangs |

You can choose to filter the `EADevicePerformanceV2` report's output based on the following columns:
- `DeviceScopeIds`
- `PartnerFeaturesBitmask`
- `DeviceId`
- `TotalAppCrashes`
- `MeanTimeToFailure`
- `DeviceAppHealthScore`
- `HealthStatus`

## EADeviceScoresV2

The following table contains the possible output when calling the `EADeviceScoresV2` report:

| Available properties |
|-|
| AppReliabilityScore |
| DeviceId |
| DeviceName |
| DeviceScopeIds |
| EndpointAnalyticsScore |
| HealthStatus |
| Manufacturer |
| Model |
| OverviewBatteryHealthScore |
| PartnerFeaturesBitmask |
| ResourcePerfScore |
| StartupPerformanceScore |
| WorkFromAnywhereScore |

You can choose to filter the `EADeviceScoresV2` report's output based on the following columns:
- `PartnerFeaturesBitmask`
- `HealthStatus`
- `EndpointAnalyticsScore`
- `StartupPerformanceScore`
- `AppReliabilityScore`
- `WorkFromAnywhereScore`
- `DeviceScopeIds`
- `OverviewBatteryHealthScore`
- `ResourcePerfScore`

## EAModelScoresV2

The following table contains the possible output when calling the `EAModelScoresV2` report:

| Available properties |
|-|
| AppReliabilityScore |
| DeviceScopeId |
| EndpointAnalyticsScore |
| HealthStatus |
| Manufacturer |
| Model |
| ModelDeviceCount |
| OverviewBatteryHealthScore |
| PartnerFeaturesBitmask |
| ResourcePerfScore |
| StartupPerformanceScore |
| WorkFromAnywhereScore |

You can choose to filter the `EAModelScoresV2` report's output based on the following columns:
- `PartnerFeaturesBitmask`
- `ModelDeviceCount`
- `HealthStatus`
- `EndpointAnalyticsScore`
- `StartupPerformanceScore`
- `AppReliabilityScore`
- `WorkFromAnywhereScore`
- `DeviceScopeId`
- `OverviewBatteryHealthScore`
- `ResourcePerfScore`

## EAOSVersionsPerformance

The following table contains the possible output when calling the `EAOSVersionsPerformance` report:

| Available properties |
|-|
| ActiveDevices |
| DeviceScopeId |
| MeanTimeToFailure |
| MemaTimeGenerated |
| OSBuildNumber |
| OSVersion |
| OSVersionAppHealthScore |
| OSVersionAppHealthStatus |
| PartnerFeaturesBitmask |
| RowCountInSnapshot |
| SchemaVersion |

You can choose to filter the `EAOSVersionsPerformance` report's output based on the following columns:
- `DeviceScopeId`
- `PartnerFeaturesBitmask`
- `ActiveDevices`
- `MeanTimeToFailure`
- `OSVersionAppHealthScore`

## EAResourcePerfAggByDevice

The following table contains the possible output when calling the `EAResourcePerfAggByDevice` report:

| Available properties |
|-|
| ClockSpeed |
| Cores |
| CpuSpikeScore |
| CpuSpikeTimePercentage |
| CpuSpikeTimePercentageThreshold |
| CpuSpikeTimeScore |
| DeviceId |
| DeviceMake |
| DeviceModel |
| DeviceName |
| DeviceScopeIds |
| DiskType |
| HealthStatus |
| IsPhysical |
| MachineType |
| OSVersion |
| PartnerFeaturesBitmask |
| ProcessorName |
| RamSpikeScore |
| RamSpikeTimePercentage |
| RamSpikeTimePercentageThreshold |
| RamSpikeTimeScore |
| ResourcePerfScore |
| TotalRamInMB |

You can choose to filter the `EAResourcePerfAggByDevice` report's output based on the following columns:
- `PartnerFeaturesBitmask`
- `DeviceId`
- `CpuSpikeTimePercentage`
- `RamSpikeTimePercentage`
- `CpuSpikeTimeScore`
- `RamSpikeTimeScore`
- `ResourcePerfScore`
- `HealthStatus`
- `MachineType`
- `ProcessorName`
- `DiskType`
- `TotalRamInMB`
- `Cores`
- `ClockSpeed`
- `DeviceScopeIds`

## EAResourcePerfAggByModel

The following table contains the possible output when calling the `EAResourcePerfAggByModel` report:

| Available properties |
|-|
| CpuSpikeScore |
| CpuSpikeTimePercentage |
| CpuSpikeTimePercentageThreshold |
| CpuSpikeTimeScore |
| DeviceMake |
| DeviceModel |
| DeviceScopeId |
| HealthStatus |
| IsPhysical |
| MachineType |
| ModelId |
| PartnerFeaturesBitmask |
| ProcessorName |
| RamSpikeScore |
| RamSpikeTimePercentage |
| RamSpikeTimePercentageThreshold |
| RamSpikeTimeScore |
| ResourcePerfScore |
| TotalDeviceCount |
| TotalRamInMB |

You can choose to filter the `EAResourcePerfAggByModel` report's output based on the following columns:
- `PartnerFeaturesBitmask`
- `ModelId`
- `CpuSpikeTimePercentage`
- `RamSpikeTimePercentage`
- `CpuSpikeTimeScore`
- `RamSpikeTimeScore`
- `ResourcePerfScore`
- `TotalDeviceCount`
- `HealthStatus`
- `MachineType`
- `ProcessorName`
- `TotalRamInMB`
- `DeviceScopeId`

## EAResourcePerfCpuSpikeProcess

The following table contains the possible output when calling the `EAResourcePerfCpuSpikeProcess` report:

| Available properties |
|-|
| CpuSpikeCount |
| Description |
| DeviceId |
| DeviceScopeId |
| DisplayName |
| EventDateTime |
| Publisher |

You can choose to filter the `EAResourcePerfCpuSpikeProcess` report's output based on the following columns:
- `DeviceId`
- `DisplayName`
- `Description`
- `Publisher`
- `CpuSpikeCount`
- `EventDateTime`

## EAResourcePerfRamSpikeProcess

The following table contains the possible output when calling the `EAResourcePerfRamSpikeProcess` report:

| Available properties |
|-|
| Description |
| DeviceId |
| DeviceScopeId |
| DisplayName |
| EventDateTime |
| Publisher |
| RamUsageInMb |

You can choose to filter the `EAResourcePerfRamSpikeProcess` report's output based on the following columns:
- `DeviceId`
- `DisplayName`
- `Description`
- `Publisher`
- `RamUsageInMb`
- `EventDateTime`

## EAStartupPerfDevicePerformance

The following table contains the possible output when calling the `EAStartupPerfDevicePerformance` report:

| Available properties |
|-|
| BlueScreenCount |
| BootScore |
| CoreBootTime |
| CoreLogonTime |
| DesktopUsableTime |
| DeviceId |
| DeviceName |
| DeviceScopeIds |
| Disktype |
| GPBootTime |
| GPLogonTime |
| HealthStatus |
| IsAnomalous |
| LogonScore |
| Manufacturer |
| MemaTimeGenerated |
| Model |
| OSVersion |
| PartnerFeaturesBitmask |
| RestartCount |
| StartupPerformanceScore |
| TargetSnapshotId |

You can choose to filter the `EAStartupPerfDevicePerformance` report's output based on the following columns:
- `DeviceScopeIds`
- `PartnerFeaturesBitmask`
- `DeviceId`
- `Disktype`
- `CoreBootTime`
- `GPBootTime`
- `CoreLogonTime`
- `GPLogonTime`
- `DesktopUsableTime`
- `RestartCount`
- `BlueScreenCount`
- `StartupPerformanceScore`
- `BootScore`
- `LogonScore`
- `HealthStatus`

## EAStartupPerfDevicePerformanceV2

The following table contains the possible output when calling the `EAStartupPerfDevicePerformanceV2` report:

| Available properties |
|-|
| BlueScreenCount |
| BootScore |
| CoreBootTime |
| CoreLogonTime |
| DesktopUsableTime |
| DeviceId |
| DeviceName |
| DeviceScopeIds |
| Disktype |
| GPBootTime |
| GPLogonTime |
| HealthStatus |
| IsAnomalous |
| LogonScore |
| Manufacturer |
| MemaTimeGenerated |
| Model |
| OSVersion |
| PartnerFeaturesBitmask |
| RestartCount |
| StartupPerformanceScore |
| TargetSnapshotId |

You can choose to filter the `EAStartupPerfDevicePerformanceV2` report's output based on the following columns:
- `DeviceScopeIds`
- `PartnerFeaturesBitmask`
- `DeviceId`
- `Disktype`
- `CoreBootTime`
- `GPBootTime`
- `CoreLogonTime`
- `GPLogonTime`
- `DesktopUsableTime`
- `RestartCount`
- `BlueScreenCount`
- `StartupPerformanceScore`
- `BootScore`
- `LogonScore`
- `HealthStatus`

## EAStartupPerfDeviceProcesses

The following table contains the possible output when calling the `EAStartupPerfDeviceProcesses` report:

| Available properties |
|-|
| DeviceScopeId |
| FileDescription |
| InsertedDate |
| Median |
| PartnerFeaturesBitmask |
| ProcessName |
| ProductName |
| Publisher |
| TimePerProcess |
| TotalDeviceCount |

You can choose to filter the `EAStartupPerfDeviceProcesses` report's output based on the following columns:
- `DeviceScopeId`
- `PartnerFeaturesBitmask`
- `TotalDeviceCount`
- `Median`
- `TimePerProcess`

## EAStartupPerfModelPerformance

The following table contains the possible output when calling the `EAStartupPerfModelPerformance` report:

| Available properties |
|-|
| AverageBlueScreens |
| AverageRestarts |
| BootDeviceCount |
| CoreBootTime |
| CoreLogonTime |
| DeviceBootTimeAverage |
| DeviceScopeId |
| Disktype |
| GPBootTime |
| GPLogonTime |
| HealthStatus |
| IsAnomalous |
| LogonDeviceCount |
| Manufacturer |
| MemaTimeGenerated |
| Model |
| ModelId |
| PartnerFeaturesBitmask |
| StartupPerformanceScore |
| TargetSnapshotId |
| TotalDeviceRecordCount |

You can choose to filter the `EAStartupPerfModelPerformance` report's output based on the following columns:
- `DeviceScopeId`
- `PartnerFeaturesBitmask`
- `ModelId`
- `Disktype`
- `TotalDeviceRecordCount`
- `CoreBootTime`
- `GPBootTime`
- `CoreLogonTime`
- `GPLogonTime`
- `AverageRestarts`
- `AverageBlueScreens`
- `StartupPerformanceScore`
- `HealthStatus`

## EAStartupPerfModelPerformanceV2

The following table contains the possible output when calling the `EAStartupPerfModelPerformanceV2` report:

| Available properties |
|-|
| AverageBlueScreens |
| AverageRestarts |
| BootDeviceCount |
| CoreBootTime |
| CoreLogonTime |
| DeviceBootTimeAverage |
| DeviceScopeId |
| Disktype |
| GPBootTime |
| GPLogonTime |
| HealthStatus |
| IsAnomalous |
| LogonDeviceCount |
| Manufacturer |
| MemaTimeGenerated |
| Model |
| ModelId |
| PartnerFeaturesBitmask |
| StartupPerformanceScore |
| TargetSnapshotId |
| TotalDeviceRecordCount |

You can choose to filter the `EAStartupPerfModelPerformanceV2` report's output based on the following columns:
- `DeviceScopeId`
- `PartnerFeaturesBitmask`
- `ModelId`
- `Disktype`
- `TotalDeviceRecordCount`
- `CoreBootTime`
- `GPBootTime`
- `CoreLogonTime`
- `GPLogonTime`
- `AverageRestarts`
- `AverageBlueScreens`
- `StartupPerformanceScore`
- `HealthStatus`

## EAWFADeviceList

The following table contains the possible output when calling the `EAWFADeviceList` report:

| Available properties |
|-|
| AutoPilotProfileAssigned |
| AutoPilotRegistered |
| CompliancePolicySetToIntune |
| DeviceId |
| DeviceName |
| DeviceScopeIds |
| GraphDeviceIsManaged |
| IsCloudManagedGatewayEnabled |
| JoinType |
| ManagedBy |
| Manufacturer |
| Model |
| OSCheckFailed |
| OSDescription |
| OSVersion |
| OtherWorkloadsSetToIntune |
| Ownership |
| PartnerFeaturesBitmask |
| Processor64BitCheckFailed |
| ProcessorCoreCountCheckFailed |
| ProcessorFamilyCheckFailed |
| ProcessorSpeedCheckFailed |
| RamCheckFailed |
| ReferenceId |
| SecureBootCheckFailed |
| SerialNumber |
| StorageCheckFailed |
| TenantAttached |
| TPMCheckFailed |
| UpgradeEligibility |

You can choose to filter the `EAWFADeviceList` report's output based on the following columns:
- `DeviceScopeIds`
- `PartnerFeaturesBitmask`
- `DeviceId`
- `ManagedBy`
- `Ownership`
- `GraphDeviceIsManaged`
- `JoinType`
- `TenantAttached`
- `CompliancePolicySetToIntune`
- `OtherWorkloadsSetToIntune`
- `AutoPilotRegistered`
- `AutoPilotProfileAssigned`
- `UpgradeEligibility`
- `IsCloudManagedGatewayEnabled`

## EAWFAModelPerformance

The following table contains the possible output when calling the `EAWFAModelPerformance` report:

| Available properties |
|-|
| CloudIdentityScore |
| CloudManagementScore |
| CloudProvisioningScore |
| DeviceScopeId |
| HealthStatus |
| Manufacturer |
| MemaTimeGenerated |
| Model |
| ModelDeviceCount |
| PartnerFeaturesBitmask |
| RowCountInSnapshot |
| SchemaVersion |
| TargetSnapshotId |
| WindowsScore |
| WorkFromAnywhereScore |

You can choose to filter the `EAWFAModelPerformance` report's output based on the following columns:
- `DeviceScopeId`
- `PartnerFeaturesBitmask`
- `HealthStatus`
- `ModelDeviceCount`
- `WindowsScore`
- `CloudIdentityScore`
- `CloudManagementScore`
- `CloudProvisioningScore`
- `WorkFromAnywhereScore`

## EAWFAPerDevicePerformance

The following table contains the possible output when calling the `EAWFAPerDevicePerformance` report:

| Available properties |
|-|
| CloudIdentityScore |
| CloudManagementScore |
| CloudProvisioningScore |
| DeviceId |
| DeviceName |
| DeviceScopeIds |
| HealthStatus |
| Manufacturer |
| MemaTimeGenerated |
| Model |
| PartnerFeaturesBitmask |
| RowCountInSnapshot |
| SchemaVersion |
| TargetSnapshotId |
| WindowsScore |
| WorkFromAnywhereScore |

You can choose to filter the `EAWFAPerDevicePerformance` report's output based on the following columns:
- `DeviceScopeIds`
- `PartnerFeaturesBitmask`
- `DeviceId`
- `HealthStatus`
- `WindowsScore`
- `CloudIdentityScore`
- `CloudManagementScore`
- `CloudProvisioningScore`
- `WorkFromAnywhereScore`

## EnrollmentActivity

The following table contains the possible output when calling the `EnrollmentActivity` report:

| Available properties |
|-|
| AadDeviceId |
| Context |
| DeviceId |
| DeviceName |
| EnrollmentActivityId |
| EnrollmentDateTime |
| EnrollmentMethod |
| Failure |
| FailureDetails |
| FailureReason |
| OS |
| OSVersion |
| OwnerType |
| Remediation |
| SerialNumber |
| UPN |
| UserId |

You can choose to filter the `EnrollmentActivity` report's output based on the following columns:
- `EnrollmentDateTime`
- `OS`
- `FailureReason`
- `EnrollmentMethod`
- `UserId`

## EnrollmentConfigurationPoliciesByDevice

The following table contains the possible output when calling the `EnrollmentConfigurationPoliciesByDevice` report:

| Available properties |
|-|
| DeviceId |
| PolicyId |
| Target |
| PolicyType |
| ProfileName |
| UserId |
| UserPrincipalName |
| State |
| Priority |
| FilterIds |
| LastAppliedTime |

You can choose to filter the `EnrollmentConfigurationPoliciesByDevice` report's output based on the following columns:
- `State`
- `DeviceId`

## EpmAggregationReportByApplication

The following table contains the possible output when calling the `EpmAggregationReportByApplication` report:

| Available properties |
|-|
| CompanyName |
| ElevationCount |
| ElevationType |
| FileName |
| FileVersion |
| Hash |
| InternalName |
| IsBackgroundProcess |

You can choose to filter the `EpmAggregationReportByApplication` report's output based on the following columns:
- `ElevationType`
- `CompanyName`
- `FileName`
- `FileVersion`

## EpmAggregationReportByApplicationV2

The following table contains the possible output when calling the `EpmAggregationReportByApplicationV2` report:

| Available properties |
|-|
| CompanyName |
| ElevationCount |
| ElevationType |
| FileName |
| FileVersion |
| Hash |
| InternalName |
| IsBackgroundProcess |

There are no filters for this report.

## EpmAggregationReportByPublisher

The following table contains the possible output when calling the `EpmAggregationReportByPublisher` report:

| Available properties |
|-|
| CompanyName |
| ElevationCount |
| ElevationType |

There are no filters for this report.

## EpmAggregationReportByPublisherV2

The following table contains the possible output when calling the `EpmAggregationReportByPublisherV2` report:

| Available properties |
|-|
| CompanyName |
| ElevationCount |
| ElevationType |

There are no filters for this report.

## EpmAggregationReportByUser

The following table contains the possible output when calling the `EpmAggregationReportByUser` report:

| Available properties |
|-|
| ManagedCount |
| TotalCount |
| UnmanagedCount |
| Upn |

There are no filters for this report.

## EpmAggregationReportByUserAppByMonth

The following table contains the possible output when calling the `EpmAggregationReportByUserAppByMonth` report:

| Available properties |
|-|
| DeviceId |
| DeviceName |
| ElevationType |
| FileDescription |
| FileInternalName |
| FileName |
| FileProductName |
| FileVersion |
| HashValue |
| MonthElevationCount |
| Publisher |
| UserName |

There are no filters for this report.

## EpmAggregationReportByUserV2

The following table contains the possible output when calling the `EpmAggregationReportByUserV2` report:

| Available properties |
|-|
| ManagedCount |
| TotalCount |
| UnmanagedCount |
| Upn |

There are no filters for this report.

## EpmDeniedReport

The following table contains the possible output when calling the `EpmDeniedReport` report:

| Available properties |
|-|
| UserName |
| DeviceId |
| DeviceName |
| FileName |
| FileProductName |
| FileDescription |
| FileInternalName |
| FileVersion |
| HashValue |
| Publisher |
| ElevationType |
| MonthElevationCount |

There are no filters for this report.

## EpmElevationReportByUserAppByDayToReporting

The following table contains the possible output when calling the `EpmElevationReportByUserAppByDayToReporting` report:

| Available properties |
|-|
| DateCreated |
| DeviceId |
| ElevationCount |
| ElevationType |
| FileName |
| FileVersion |
| HashValue |
| Publisher |
| UserName |

There are no filters for this report.

## EpmElevationReportElevationEvent

The following table contains the possible output when calling the `EpmElevationReportElevationEvent` report:

| Available properties |
|-|
| CompanyName |
| DeviceId |
| DeviceName |
| ElevationType |
| EventDateTime |
| FileDescription |
| FilePath |
| FileVersion |
| Hash |
| Id |
| InternalName |
| IsSystemInitiated |
| Justification |
| ParentProcessName |
| PolicyId |
| PolicyName |
| ProcessType |
| ProductName |
| Result |
| RuleId |
| Upn |
| UserType |

You can choose to filter the `EpmElevationReportElevationEvent` report's output based on the following columns:
- `ElevationType`
- `Result`
- `EventDateTime`

## EpmInsightsElevationTrend

The following table contains the possible output when calling the `EpmInsightsElevationTrend` report:

| Available properties |
|-|
| DateCreated |
| ElevationType |
| DailyElevationCount |

There are no filters for this report.

## EpmInsightsMostFrequentElevations

The following table contains the possible output when calling the `EpmInsightsMostFrequentElevations` report:

| Available properties |
|-|
| ElevationType |
| FileInternalName |
| FileName |
| FileVersion |
| HashValue |
| MonthElevationCount |
| Publisher |

There are no filters for this report.

## EpmInsightsReport

The following table contains the possible output when calling the `EpmInsightsReport` report:

| Available properties |
|-|
| Green |
| Yellow |
| Red |

There are no filters for this report.

## FeatureUpdateDeviceState report

The following table contains the possible output when calling the `FeatureUpdateDeviceState` report:

| Available properties  |
|-|
|     AADDeviceId  |
|     AggregateState     |
|     Build  |
|     CurrentDeviceUpdateStatus  |
|     CurrentDeviceUpdateStatusEventDateTimeUTC  |
|     CurrentDeviceUpdateSubstatus  |
|     DeviceId  |
|     DeviceName  |
|     EventDateTimeUTC  |
|     FeatureUpdateVersion  |
|     LastSuccessfulDeviceUpdateStatus  |
|     LastSuccessfulDeviceUpdateStatusEventDateTimeUTC  |
|     LastSuccessfulDeviceUpdateSubstatus  |
|     LastWUScanTimeUTC  |
|     LatestAlertExtendedRecommendedAction  |
|     LatestAlertMessage  |
|     LatestAlertMessageDescription  |
|     LatestAlertRecommendedAction  |
|     OwnerType  |
|     PartnerPolicyId  |
|     PolicyId  |
|     PolicyName  |
|     UpdateCategory  |
|     UPN  |
|     WindowsUpdateVersion  |

You can choose to filter the `FeatureUpdateDeviceState` report's output based on the following columns:
- `PolicyId` **(Required)**
- `AggregateState`
- `LatestAlertMessage`
- `OwnerType`

## FeatureUpdatePolicyFailuresAggregate report

The following table contains the possible output when calling the `FeatureUpdatePolicyFailuresAggregate` report:

| Available properties  |
|-|
|     FeatureUpdateVersion  |
|     NumberOfDevicesWithErrors     |
|     PolicyId  |
|     PolicyName  |

You cannot filter this report.

## FeatureUpdatePolicyStatusSummary

The following table contains the possible output when calling the `FeatureUpdatePolicyStatusSummary` report:

| Available properties |
|-|
| CountDevicesErrorStatus |
| CountDevicesInProgressStatus |
| CountDevicesSuccessStatus |
| FeatureUpdateVersion |
| PolicyId |
| PolicyName |

There are no filters for this report.

## FilteredAppsList

The following table contains the possible output when calling the `FilteredAppsList` report:

| Available properties |
|-|
| ApplicationId |
| ApplicationName |
| AppLastModifiedTime |
| AppStatus |
| AppType |
| AppVersion |
| Assigned |
| CreationTime |
| Description |
| Developer |
| ExpirationTime |
| IsFeaturedApp |
| MoreInformationLink |
| Notes |
| Owner |
| Platform |
| PrivacyLink |
| Publisher |
| StoreUrl |

There are no filters for this report.

## FirewallStatus

The following table contains the possible output when calling the `FirewallStatus` report:

| Available   properties |
|-|
| DeviceId  |
| DeviceName  |
| FirewallStatus  |
| LastReportedDateTime  |
| ReferenceId  |
| UPN   |
| UserName  |
| _ManagedBy   |
| _OS  |

You can choose to filter the `FirewallStatus` report's output based on the following columns:
- `FirewallStatus`

## FirewallUnhealthyStatus

The following table contains the possible output when calling the `FirewallUnhealthyStatus` report:

| Available properties |
|-|
| DeviceId |
| DeviceName |
| FirewallStatus |
| LastReportedDateTime |
| UPN |
| UserName |
| _OS |
| _ManagedBy |
| ReferenceId |

You can choose to filter the `FirewallUnhealthyStatus` report's output based on the following columns:
- `FirewallStatus`

## GPAnalyticsSettingMigrationReadiness

The following table contains the possible output when calling the `GPAnalyticsSettingMigrationReadiness` report:

| Available   properties |
|-|
| CSPName   |
| Key   |
| MdmMapping   |
| MigrationReadiness   |
| OSVersion   |
| ProfileType   |
| Scope   |
| SettingCategory   |
| SettingName   |

You can choose to filter the `GPAnalyticsSettingMigrationReadiness` report's output based on the following columns:
- `MigrationReadiness`
- `ProfileType`
- `CSPName`

## InventoryPolicyDeviceAggregatesV3

The following table contains the possible output when calling the `InventoryPolicyDeviceAggregatesV3` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| NumberOfInProgressDevices |
| NumberOfNonCompliantDevices |
| NumberOfNonCompliantOrErrorDevices |
| NumberOfNotApplicableDevices |
| NumberOfRemovedDevices |
| PolicyBaseTypeName |
| PolicyId |
| PolicyName |
| PolicyPlatformType |
| PolicyType |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |

You can choose to filter the `InventoryPolicyDeviceAggregatesV3` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`

## InventoryPolicyDeviceAggregatesWithPF

The following table contains the possible output when calling the `InventoryPolicyDeviceAggregatesWithPF` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| NumberOfInProgressDevices |
| NumberOfNonCompliantDevices |
| NumberOfNonCompliantOrErrorDevices |
| NumberOfNotApplicableDevices |
| NumberOfRemovedDevices |
| PolicyBaseTypeName |
| PolicyId |
| PolicyName |
| PolicyPlatformType |
| PolicyType |
| ProfileSource |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |

You can choose to filter the `InventoryPolicyDeviceAggregatesWithPF` report's output based on the following columns:
- `PolicyId`
- `PolicyBaseTypeName`

## Malware

The following table contains the possible output when calling the `Malware` report:

| Available properties |
|-|
| AdditionalInformationUrl |
| DetectionCount |
| DeviceId |
| DeviceName |
| ExecutionState |
| InitialDetectionDateTime |
| LastStateChangeDateTime |
| MalwareCategory |
| MalwareId |
| MalwareName |
| Severity |
| State |
| UPN |
| UserEmail |
| UserName |
| _ManagedBy |

You can choose to filter the `Malware` report's output based on the following columns:
- `Severity`
- `ExecutionState`
- `State`

## MAMAppConfigurationStatus

The following table contains the possible output when calling the `MAMAppConfigurationStatus` report:

| Available   properties |
|-|
| AADDeviceID   |
| AndroidMamSdkVersion   |
| AndroidPatchVersion   |
| App   |
| AppInstanceId   |
| AppVersion   |
| DeviceHealth   |
| DeviceManufacturer   |
| DeviceModel   |
| DeviceName   |
| DeviceType   |
| Email   |
| LastSync   |
| MDMDeviceID    |
| Platform   |
| PlatformVersion   |
| Policy   |
| SdkVersion   |
| User   |

There are no filters for this report.

## MAMAppConfigurationStatusScopedV2

The following table contains the possible output when calling the `MAMAppConfigurationStatusScopedV2` report:

| Available properties |
|-|
| AADDeviceID |
| AndroidMamSdkVersion |
| AndroidSecurityPatchVersion |
| App |
| AppInstanceId |
| AppVersion |
| DeviceManufacturer |
| DeviceModel |
| DeviceName |
| DeviceType |
| Email |
| iOSSdkVersion |
| LastSync |
| MDMDeviceID |
| _Platform |
| PlatformVersion |
| Policy |
| User |

There are no filters for this report.

## MAMAppConfigurationStatusV2

The following table contains the possible output when calling the `MAMAppConfigurationStatusV2` report:

| Available properties |
|-|
| AADDeviceID |
| AndroidMamSdkVersion |
| AndroidSecurityPatchVersion |
| App |
| AppInstanceId |
| AppVersion |
| DeviceManufacturer |
| DeviceModel |
| DeviceName |
| DeviceType |
| Email |
| iOSSdkVersion |
| LastSync |
| MDMDeviceID |
| _Platform |
| PlatformVersion |
| Policy |
| User |

There are no filters for this report.

## MAMAppProtectionStatus

The following table contains the possible output when calling the `MAMAppProtectionStatus` report:

| Available   properties |
|-|
| AADDeviceID   |
| AndroidMamSdkVersion   |
| AndroidPatchVersion   |
| App   |
| AppInstanceId   |
| AppProtectionStatus   |
| AppVersion   |
| ComplianceState   |
| DeviceHealth   |
| DeviceManagmentType   |
| DeviceManufacturer   |
| DeviceModel   |
| DeviceName   |
| DeviceType   |
| Email   |
| LastSync   |
| ManagementType   |
| MDMDeviceID   |
| Platform   |
| PlatformVersion   |
| Policy   |
| SdkVersion   |
| User   |

There are no filters for this report.

## MAMAppProtectionStatusScopedV2

The following table contains the possible output when calling the `MAMAppProtectionStatusScopedV2` report:

| Available properties |
|-|
| AADDeviceID |
| AndroidMamSdkVersion |
| AndroidSecurityPatchVersion |
| App |
| AppInstanceId |
| AppProtectionStatus |
| AppVersion |
| ComplianceState |
| DeviceManufacturer |
| DeviceModel |
| DeviceName |
| DeviceType |
| Email |
| iOSSdkVersion |
| LastSync |
| ManagementType |
| MDMDeviceID |
| _Platform |
| PlatformVersion |
| Policy |
| User |

There are no filters for this report.

## MAMAppProtectionStatusV2

The following table contains the possible output when calling the `MAMAppProtectionStatusV2` report:

| Available properties |
|-|
| AADDeviceID |
| AndroidMamSdkVersion |
| AndroidSecurityPatchVersion |
| App |
| AppInstanceId |
| AppProtectionStatus |
| AppVersion |
| ComplianceState |
| DeviceManufacturer |
| DeviceModel |
| DeviceName |
| DeviceType |
| Email |
| iOSSdkVersion |
| LastSync |
| ManagementType |
| MDMDeviceID |
| _Platform |
| PlatformVersion |
| Policy |
| User |

There are no filters for this report.

## MEMUpgradeReadinessOrgAsset

The following table contains the possible output when calling the `MEMUpgradeReadinessOrgAsset` report:

| Available properties |
|-|
| AadDeviceId |
| AadTenantId |
| AssetId |
| AssetName |
| AssetType |
| AssetVendor |
| AssetVersion |
| ConfigMgrId |
| DeviceId |
| DeviceManufacturer |
| DeviceModel |
| DeviceName |
| InventoryCompleteness |
| IssueTypes |
| ManagedBy |
| MemaTimeGenerated |
| OSVersion |
| Ownership |
| PartnerFeaturesBitmask |
| ReadinessStatus |
| RowCountInSnapshot |
| SCCMObjectId |
| SchemaVersion |
| TargetOS |

There are no filters for this report.

## NonCompliantCompliancePoliciesAggregate

The following table contains the possible output when calling the `NonCompliantCompliancePoliciesAggregate` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| NumberOfNonCompliantDevices |
| NumberOfNonCompliantOrErrorDevices |
| NumberOfNotApplicableDevices |
| PolicyBaseTypeName |
| PolicyId |
| PolicyName |
| PolicyPlatformType |
| PolicyType |
| ProfileSource |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |

You can choose to filter the `NonCompliantCompliancePoliciesAggregate` report's output based on the following columns:
- `PolicyName`
- `PolicyType`
- `UnifiedPolicyType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyPlatformType`
- `UnifiedPolicyPlatformType`

## NonCompliantCompliancePoliciesAggregateV3

The following table contains the possible output when calling the `NonCompliantCompliancePoliciesAggregateV3` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| NumberOfNonCompliantDevices |
| NumberOfNonCompliantOrErrorDevices |
| NumberOfNotApplicableDevices |
| PolicyBaseTypeName |
| PolicyId |
| PolicyName |
| PolicyPlatformType |
| PolicyType |
| ProfileSource |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |

You can choose to filter the `NonCompliantCompliancePoliciesAggregateV3` report's output based on the following columns:
- `PolicyName`
- `PolicyType`
- `UnifiedPolicyType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyPlatformType`
- `UnifiedPolicyPlatformType`

## NonCompliantConfigurationPoliciesAggregateWithPF

The following table contains the possible output when calling the `NonCompliantConfigurationPoliciesAggregateWithPF` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| NumberOfInProgressDevices |
| NumberOfNonCompliantDevices |
| NumberOfNonCompliantOrErrorDevices |
| NumberOfNotApplicableDevices |
| NumberOfRemovedDevices |
| PolicyBaseTypeName |
| PolicyId |
| PolicyName |
| PolicyPlatformType |
| PolicyType |
| ProfileSource |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |

You can choose to filter the `NonCompliantConfigurationPoliciesAggregateWithPF` report's output based on the following columns:
- `PolicyName`
- `PolicyType`
- `UnifiedPolicyType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyPlatformType`
- `UnifiedPolicyPlatformType`
- `NumberOfErrorDevices`
- `NumberOfNonCompliantDevices`

## NonCompliantConfigurationPoliciesAggregateWithPFV3

The following table contains the possible output when calling the `NonCompliantConfigurationPoliciesAggregateWithPFV3` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| NumberOfInProgressDevices |
| NumberOfNonCompliantDevices |
| NumberOfNonCompliantOrErrorDevices |
| NumberOfNotApplicableDevices |
| NumberOfRemovedDevices |
| PolicyBaseTypeName |
| PolicyId |
| PolicyName |
| PolicyPlatformType |
| PolicyType |
| ProfileSource |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |

You can choose to filter the `NonCompliantConfigurationPoliciesAggregateWithPFV3` report's output based on the following columns:
- `PolicyName`
- `PolicyType`
- `UnifiedPolicyType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyPlatformType`
- `UnifiedPolicyPlatformType`
- `NumberOfErrorDevices`
- `NumberOfNonCompliantDevices`

## NoncompliantDevicesAndSettings

The following table contains the possible output when calling the `NoncompliantDevicesAndSettings` report:

| Available properties |
|-|
| DeviceId |
| DeviceName |
| ErrorCode |
| OS |
| OSVersion |
| PolicyName |
| SettingName |
| SettingNm |
| SettingStatus |
| UPN |

There are no filters for this report.

## NoncompliantDevicesAndSettingsV3

The following table contains the possible output when calling the `NoncompliantDevicesAndSettingsV3` report:

| Available properties |
|-|
| DeviceId |
| DeviceName |
| ErrorCode |
| OS |
| OSVersion |
| PolicyName |
| SettingName |
| SettingNm |
| SettingStatus |
| UPN |

There are no filters for this report.

## NonCompliantDevicesByCompliancePolicy

The following table contains the possible output when calling the `NonCompliantDevicesByCompliancePolicy` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `NonCompliantDevicesByCompliancePolicy` report's output based on the following columns:
- `PolicyName`
- `PolicyType`
- `DeviceType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyPlatformType`
- `PolicyStatus`

## NonCompliantDevicesByCompliancePolicyV3

The following table contains the possible output when calling the `NonCompliantDevicesByCompliancePolicyV3` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `NonCompliantDevicesByCompliancePolicyV3` report's output based on the following columns:
- `PolicyName`
- `PolicyType`
- `DeviceType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyPlatformType`
- `PolicyStatus`

## NoncompliantDevicesToBeRetired

The following table contains the possible output when calling the `NoncompliantDevicesToBeRetired` report:

| Available properties |
|-|
| ComplianceState |
| DeviceId |
| DeviceName |
| ManagementAgents |
| OS |
| OwnerType |
| PolicyId |
| PolicyName |
| RetireAfterDatetime |
| ScheduledRetireState |

There are no filters for this report.

## OrgAppsInstallStatus

The following table contains the possible output when calling the `OrgAppsInstallStatus` report:

| Available properties |
|-|
| ApplicationId |
| AppVersion |
| DisplayName |
| FailedDeviceCount |
| FailedDevicePercentage |
| FailedUserCount |
| InstalledDeviceCount |
| InstalledUserCount |
| NotApplicableDeviceCount |
| NotApplicableUserCount |
| NotInstalledDeviceCount |
| NotInstalledUserCount |
| PendingInstallDeviceCount |
| PendingInstallUserCount |
| Platform |
| Publisher |

There are no filters for this report.

## OrgDeviceInstallStatus

The following table contains the possible output when calling the `OrgDeviceInstallStatus` report:

| Available properties |
|-|
| ApplicationId |
| AppVersion |
| DeviceId |
| DeviceName |
| ErrorCode |
| InstallState |
| InstallStateDetail |
| LastModifiedDateTime |
| Platform |
| UserName |
| UserPrincipalName |

There are no filters for this report.

## PerSettingDeviceSummaryByConfigurationPolicy

The following table contains the possible output when calling the `PerSettingDeviceSummaryByConfigurationPolicy` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| SettingName |

You can choose to filter the `PerSettingDeviceSummaryByConfigurationPolicy` report's output based on the following columns:
- `PolicyId`

## PerSettingDeviceSummaryByConfigurationPolicyForAppControl

The following table contains the possible output when calling the `PerSettingDeviceSummaryByConfigurationPolicyForAppControl` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| SettingName |

You can choose to filter the `PerSettingDeviceSummaryByConfigurationPolicyForAppControl` report's output based on the following columns:
- `PolicyId`

## PerSettingDeviceSummaryByConfigurationPolicyForEDR

The following table contains the possible output when calling the `PerSettingDeviceSummaryByConfigurationPolicyForEDR` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| SettingName |

You can choose to filter the `PerSettingDeviceSummaryByConfigurationPolicyForEDR` report's output based on the following columns:
- `PolicyId`

## PerSettingDeviceSummaryByInventoryPolicy

The following table contains the possible output when calling the `PerSettingDeviceSummaryByInventoryPolicy` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| SettingName |

You can choose to filter the `PerSettingDeviceSummaryByInventoryPolicy` report's output based on the following columns:
- `PolicyId`

## PerSettingDeviceSummaryByInventoryPolicyV3

The following table contains the possible output when calling the `PerSettingDeviceSummaryByInventoryPolicyV3` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| SettingName |

You can choose to filter the `PerSettingDeviceSummaryByInventoryPolicyV3` report's output based on the following columns:
- `PolicyId`

## PerSettingSummaryByDeviceConfigurationPolicy

The following table contains the possible output when calling the `PerSettingSummaryByDeviceConfigurationPolicy` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| SettingId |
| SettingName |

You can choose to filter the `PerSettingSummaryByDeviceConfigurationPolicy` report's output based on the following columns:
- `PolicyId`

## Policies

The following table contains the possible output when calling the `Policies` report:

| Available properties |
|-|
| PolicyId |
| PolicyName |

There are no filters for this report.

## PolicyComplianceAggReport

The following table contains the possible output when calling the `PolicyComplianceAggReport` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| NumberOfNonCompliantDevices |
| NumberOfNotApplicableDevices |
| NumberOfNotEvaluatedDevices |
| PolicyId |
| PolicyName |
| PolicyPlatform |
| PolicyPlatformType |

There are no filters for this report.

## PolicyComplianceAggReportV3

The following table contains the possible output when calling the `PolicyComplianceAggReportV3` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| NumberOfNonCompliantDevices |
| NumberOfNotApplicableDevices |
| NumberOfNotEvaluatedDevices |
| PolicyId |
| PolicyName |
| PolicyPlatform |
| PolicyPlatformType |

There are no filters for this report.

## PolicyNonComplianceAgg

The following table contains the possible output when calling the `PolicyNonComplianceAgg` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| NumberOfNonCompliantDevices |
| NumberOfNonCompliantOrErrorDevices |
| NumberOfNotApplicableDevices |
| PolicyBaseTypeName |
| PolicyId |
| PolicyName |
| PolicyPlatformType |
| PolicyType |
| ProfileSource |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |

You can choose to filter the `PolicyNonComplianceAgg` report's output based on the following columns:
- `PolicyName`
- `PolicyType`
- `UnifiedPolicyType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyPlatformType`
- `UnifiedPolicyPlatformType`
- `NumberOfErrorDevices`
- `NumberOfNonCompliantDevices`

## PolicyNonComplianceAggVer3

The following table contains the possible output when calling the `PolicyNonComplianceAggVer3` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfErrorDevices |
| NumberOfNonCompliantDevices |
| NumberOfNonCompliantOrErrorDevices |
| NumberOfNotApplicableDevices |
| PolicyBaseTypeName |
| PolicyId |
| PolicyName |
| PolicyPlatformType |
| PolicyType |
| ProfileSource |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |

You can choose to filter the `PolicyNonComplianceAggVer3` report's output based on the following columns:
- `PolicyName`
- `PolicyType`
- `UnifiedPolicyType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyPlatformType`
- `UnifiedPolicyPlatformType`
- `NumberOfErrorDevices`
- `NumberOfNonCompliantDevices`

## PolicyNonComplianceNew

The following table contains the possible output when calling the `PolicyNonComplianceNew` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `PolicyNonComplianceNew` report's output based on the following columns:
- `PolicyName`
- `PolicyType`
- `DeviceType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyPlatformType`
- `PolicyStatus`

## PolicyNonComplianceNewV3

The following table contains the possible output when calling the `PolicyNonComplianceNewV3` report:

| Available properties |
|-|
| AssignmentFilterIds |
| DeviceName |
| IntuneDeviceId |
| Manufacturer |
| Model |
| PolicyId |
| PolicyName |
| PolicyStatus |
| PspdpuLastModifiedTimeUtc |
| ReportStatus |
| TemplateVersion |
| UnifiedPolicyPlatformType |
| UnifiedPolicyType |
| UPN |

You can choose to filter the `PolicyNonComplianceNewV3` report's output based on the following columns:
- `PolicyName`
- `PolicyType`
- `DeviceType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyPlatformType`
- `PolicyStatus`

## PolicyRunStatesByProactiveRemediation

The following table contains the possible output when calling the `PolicyRunStatesByProactiveRemediation` report:

| Available properties |
|-|
| DetectionScriptStatus |
| DetectionStatus |
| DeviceId |
| DeviceName |
| FilterIdsCSV |
| InternalVersion |
| JoinType |
| LastAgentUpdateTime |
| Model |
| ModifiedTime |
| NextExecutionDateTime |
| OSDescription |
| OSVersion |
| PolicyId |
| PolicyName |
| PostRemediationDetectionScriptError |
| PostRemediationDetectionScriptOutput |
| PreRemediationDetectionScriptError |
| PreRemediationDetectionScriptOutput |
| PrimaryUser |
| RemediationScriptErrorDetails |
| RemediationScriptOutputDetails |
| RemediationScriptStatus |
| RemediationStatus |
| UniqueKustoKey |
| UPN |
| UserEmail |
| UserId |
| UserName |

There are no filters for this report.

## QualityUpdateDeviceErrorsByPolicy

The following table contains the possible output when calling the `QualityUpdateDeviceErrorsByPolicy` report:

| Available   properties |
|-|
| AlertMessage   |
| AlertMessage_loc   |
| DeviceId   |
| DeviceName   |
| ExpediteQUReleaseDate   |
| PolicyId   |
| UPN   |
| Win32ErrorCode   |

You can choose to filter the `QualityUpdateDeviceErrorsByPolicy` report's output based on the following columns:
- `PolicyId` **(required)**
- `AlertMessage`

## QualityUpdateDeviceStatusByPolicy

The following table contains the possible output when calling the `QualityUpdateDeviceStatusByPolicy` report:

| Available   properties |
|-|
| AADDeviceId   |
| AggregateState   |
| AggregateState_loc   |
| CurrentDeviceUpdateStatus   |
| CurrentDeviceUpdateStatus_loc   |
| CurrentDeviceUpdateSubstatus   |
| CurrentDeviceUpdateSubstatus_loc   |
| DeviceId   |
| DeviceName   |
| EventDateTimeUTC   |
| LastWUScanTimeUTC   |
| LatestAlertMessage   |
| LatestAlertMessage_loc   |
| OwnerType   |
| PolicyId   |
| UPN   |

You can choose to filter the `QualityUpdateDeviceStatusByPolicy` report's output based on the following columns:
- `PolicyId` **(required)**
- `AggregateState`
- `OwnerType`

## QualityUpdatePolicyStatusSummary

The following table contains the possible output when calling the `QualityUpdatePolicyStatusSummary` report:

| Available properties |
|-|
| CountDevicesErrorStatus |
| CountDevicesInProgressStatus |
| CountDevicesSuccessStatus |
| ExpediteQUReleaseDate |
| PolicyId |
| PolicyName |

There are no filters for this report.

## RemoteAssistanceSessions

The following table contains the possible output when calling the `RemoteAssistanceSessions` report:

| Available properties |
|-|
| Attribute |
| Date |
| DateDifference |
| HelperDeviceAadId |
| HelperDeviceName |
| HelperEmail |
| HelperFirstName |
| HelperLastName |
| Sessionend |
| SessionId |
| Sessionstart |
| SharerDeviceAadId |
| SharerDeviceName |
| SharerDeviceOS |
| SharerDeviceSerialNumber |
| SharerEmail |
| SharerFirstName |
| SharerLastName |

You can choose to filter the `RemoteAssistanceSessions` report's output based on the following columns:
- `ProviderID`
- `Recipient ID`
- `RecipientName`
- `DeviceName`
- `OS`

## ResourcePerformanceAggregateByDevice

The following table contains the possible output when calling the `ResourcePerformanceAggregateByDevice` report:

| Available properties |
|-|
| CpuSpikeScore |
| CpuSpikeTimePercentage |
| CpuSpikeTimePercentageThreshold |
| CpuSpikeTimeScore |
| DeviceId |
| DeviceMake |
| DeviceModel |
| DeviceName |
| OSVersion |
| PartnerFeaturesBitmask |
| RamSpikeScore |
| RamSpikeTimePercentage |
| RamSpikeTimePercentageThreshold |
| RamSpikeTimeScore |
| ResourcePerfScore |

You can choose to filter the `ResourcePerformanceAggregateByDevice` report's output based on the following columns:
- `PartnerFeaturesBitmask`
- `DeviceId`
- `CpuSpikeTimePercentage`
- `RamSpikeTimePercentage`
- `CpuSpikeTimeScore`
- `RamSpikeTimeScore`
- `ResourcePerfScore`
- `CpuSpikeTimePercentageThreshold`
- `RamSpikeTimePercentageThreshold`

## ResourcePerformanceAggregateByModel

The following table contains the possible output when calling the `ResourcePerformanceAggregateByModel` report:

| Available properties |
|-|
| CpuSpikeScore |
| CpuSpikeTimePercentage |
| CpuSpikeTimePercentageThreshold |
| CpuSpikeTimeScore |
| DeviceMake |
| DeviceModel |
| ModelId |
| PartnerFeaturesBitmask |
| RamSpikeScore |
| RamSpikeTimePercentage |
| RamSpikeTimePercentageThreshold |
| RamSpikeTimeScore |
| ResourcePerfScore |
| TotalDeviceCount |

You can choose to filter the `ResourcePerformanceAggregateByModel` report's output based on the following columns:
- `PartnerFeaturesBitmask`
- `ModelId`
- `CpuSpikeTimePercentage`
- `RamSpikeTimePercentage`
- `CpuSpikeTimeScore`
- `RamSpikeTimeScore`
- `ResourcePerfScore`
- `TotalDeviceCount`
- `CpuSpikeTimePercentageThreshold`
- `RamSpikeTimePercentageThreshold`

## SettingComplianceAggReport

The following table contains the possible output when calling the `SettingComplianceAggReport` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfNonCompliantDevices |
| NumberOfNotApplicableDevices |
| NumberOfNotEvaluatedDevices |
| PolicyPlatform |
| PolicyPlatformType |
| SettingId |
| SettingName |
| SettingNm |

There are no filters for this report.

## SettingComplianceAggReportV3

The following table contains the possible output when calling the `SettingComplianceAggReportV3` report:

| Available properties |
|-|
| NumberOfCompliantDevices |
| NumberOfConflictDevices |
| NumberOfNonCompliantDevices |
| NumberOfNotApplicableDevices |
| NumberOfNotEvaluatedDevices |
| PolicyPlatform |
| PolicyPlatformType |
| SettingId |
| SettingName |
| SettingNm |

There are no filters for this report.

## TicketingSecurityTaskAppsList

The following table contains the possible output when calling the `TicketingSecurityTaskAppsList` report:

| Available properties |
|-|
| ApplicationId |
| ApplicationName |
| AppLastModifiedTime |
| AppType |
| CurrentAppVersion |
| InstalledDeviceCount |
| IsSuperseded |
| LatestAvailableVersion |
| UpdateAvailable |

There are no filters for this report.

## TpmAttestationStatus

The following table contains the possible output when calling the `TpmAttestationStatus` report:

| Available properties |
|-|
| AttestationStatus |
| AttestationStatusDetail |
| DeviceId |
| DeviceName |
| EnrolledByUser |
| EnrollmentDate |
| LastCheckin |
| Model |
| OS |
| OSVersion |
| Ownership |
| TpmManufacturer |
| TpmVersion |
| UPN |

You can choose to filter the `TpmAttestationStatus` report's output based on the following columns:
- `AttestationStatus`
- `Ownership`
- `OSDescription`

## UnhealthyDefenderAgents

The following table contains the possible output when calling the `UnhealthyDefenderAgents` report:

| Available properties |
|-|
| DeviceId |
| DeviceName |
| DeviceState |
| IsVirtualMachine |
| LastReportedDateTime |
| MalwareProtectionEnabled |
| NetworkInspectionSystemEnabled |
| ProductStatus |
| RealTimeProtectionEnabled |
| SignatureUpdateOverdue |
| TamperProtectionEnabled |
| UPN |
| UserEmail |
| UserName |
| _ManagedBy |

You can choose to filter the `UnhealthyDefenderAgents` report's output based on the following columns:
- `DeviceState`
- `SignatureUpdateOverdue`
- `MalwareProtectionEnabled`
- `RealTimeProtectionEnabled`
- `NetworkInspectionSystemEnabled`

## UserInstallStatusAggregateByApp

The following table contains the possible output when calling the `UserInstallStatusAggregateByApp` report:

| Available   properties |
|-|
| ApplicationId |
| FailedCount |
| InstalledCount |
| NotApplicableCount    |
| NotInstalledCount |
| PendingInstallCount |
| UserId |
| UserName |
| UserPrincipalName |

You can choose to filter the `UserInstallStatusAggregateByApp` report's output based on the following column:
- `ApplicationId` **(Required)**

## Users

The following table contains the possible output when calling the `Users` report:

| Available properties |
|-|
| UPN |
| UserEmail |
| UserId |
| UserName |

There are no filters for this report.

## UserScaleTest

The following table contains the possible output when calling the `UserScaleTest` report:

| Available properties |
|-|
| UPN |
| UserEmail |
| UserId |
| UserName |

You can choose to filter the `UserScaleTest` report's output based on the following columns:
- `UserId`
- `UPN`
- `UserEmail`
- `UserName`

## WindowsDeviceHealthAttestationReport

The following table contains the possible output when calling the `WindowsDeviceHealthAttestationReport` report:

| Available properties |
|-|
| AIKKey |
| AttestationError |
| BitlockerStatus |
| BootDebuggingStatus |
| CodeIntegrityStatus |
| DEPPolicy |
| DeviceId |
| DeviceName |
| DeviceOS |
| ELAMDriverLoadedStatus |
| FirmwareProtectionStatus |
| HealthCertIssuedDate |
| MemoryAccessProtectionStatus |
| MemoryIntegrityProtectionStatus |
| OSKernelDebuggingStatus |
| PrimaryUser |
| SafeModeStatus |
| SecuredCorePCStatus |
| SecureBootStatus |
| SystemManagementMode |
| TpmVersion |
| UPN |
| VSMStatus |
| WinPEStatus |

There are no filters for this report.

## WindowsUpdatePerPolicyPerDeviceStatus

The following table contains the possible output when calling the `WindowsUpdatePerPolicyPerDeviceStatus` report:

| Available properties |
|-|
| AggregateState |
| CurrentDeviceUpdateStatus |
| DeviceId |
| DeviceName |
| LatestAlertMessage |
| PolicyId |
| UPN |

There are no filters for this report.

## WorkFromAnywhereDeviceList

The following table contains the possible output when calling the `WorkFromAnywhereDeviceList` report:

| Available properties |
|-|
| AutoPilotProfileAssigned |
| AutoPilotRegistered |
| CompliancePolicySetToIntune |
| DeviceId |
| DeviceName |
| GraphDeviceIsManaged |
| JoinType |
| ManagedBy |
| Manufacturer |
| Model |
| OSCheckFailed |
| OSDescription |
| OSVersion |
| OtherWorkloadsSetToIntune |
| Ownership |
| PartnerFeaturesBitmask |
| Processor64BitCheckFailed |
| ProcessorCoreCountCheckFailed |
| ProcessorFamilyCheckFailed |
| ProcessorSpeedCheckFailed |
| RamCheckFailed |
| ReferenceId |
| SecureBootCheckFailed |
| SerialNumber |
| StorageCheckFailed |
| TenantAttached |
| TPMCheckFailed |
| UpgradeEligibility |

You can choose to filter the `WorkFromAnywhereDeviceList` report's output based on the following columns:
- `PartnerFeaturesBitmask`
- `DeviceId`
- `ManagedBy`
- `Ownership`
- `GraphDeviceIsManaged`
- `JoinType`
- `TenantAttached`
- `CompliancePolicySetToIntune`
- `OtherWorkloadsSetToIntune`
- `AutoPilotRegistered`
- `AutoPilotProfileAssigned`
- `UpgradeEligibility`


## Next steps

- [Microsoft Graph documentation](/graph/)
- [Intune reports](./reports.md)
