---
title: Intune Graph API - Reports and Properties | Microsoft Docs
description: Learn about Intune reports and properties provided via Graph API.
author: nicholasswhite
ms.author: nwhite
ms.date: 09/08/2025
ms.topic: article
ms.reviewer: davidra
#ms.custom:
ms.collection:
- M365-identity-device-management
---

# Intune Reports and Properties Available Using Graph API

Microsoft Intune provides many reports in the Microsoft Intune admin center that can be exported using Graph APIs. Microsoft Graph is a RESTful web API that enables you to access Microsoft Cloud service resources. To export Intune reports, you must use the Microsoft Graph API to make a set of HTTP calls. For more information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

> [!NOTE]
> Intune reports that are migrated to a new [Intune reporting infrastructure](https://techcommunity.microsoft.com/t5/intune-customer-success/new-reporting-framework-coming-to-intune/ba-p/1009553#:~:text=New%20Reporting%20Framework%20Coming%20to%20Intune%20%20,Device%20compliance%20logging%20%203%20more%20rows), are available for export from a single top-level export Graph API.
>
> For more information about making REST API calls, including tools for interacting with Microsoft Graph, see [Use the Microsoft Graph API](/graph/use-the-api).

Microsoft Intune exports reports through the following Microsoft Graph API endpoint:

```http
https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs
```

The following table contains the possible values for the `reportName` parameter and the corresponding reports you can export.

| ReportName (Export Parameter) | Associated Report in Microsoft Intune |
|------------------------------|----------------------------------------|
| ActiveMalware | Under **Endpoint Security** > **Antivirus** > **Win10 detected malware** |
| ADMXSettingsByDeviceByPolicy | Under **Reports** > **Device management** > **Device Configuration** |
| AllAppsList | Under **Apps** > **All Apps** |
| AllDeviceCertificates | Under **Devices** > **Monitor** > **Certificates** |
| AppInstallStatusAggregate | Under **Apps** > **Monitor** > **App install status** |
| AppInvAggregate | Under **Apps** > **Monitor** > **Discovered apps** > **Export**  |
| AppInvByDevice | Under **Devices** > **All Devices** > **Device** > **Discovered Apps**  |
| AppInvRawData | Under **Apps** > **Monitor** > **Discovered apps** > **Export**  |
| AutopilotV1DeploymentStatus | Under **Devices** > **Windows** > **Enrollment** > **Windows Autopilot** |
| AutopilotV2DeploymentStatus | Under **Devices** > **Windows** > **Enrollment** > **Windows Autopilot** |
| AutopilotV2DeploymentStatusDetailedAppInfo | Under **Devices** > **Windows** > **Enrollment** > **Windows Autopilot** |
| AutopilotV2DeploymentStatusDetailedScriptInfo | Under **Devices** > **Windows** > **Enrollment** > **Windows Autopilot** |
| BRBatteryByModel | Under **Reports** > **Endpoint analytics** > **Battery health** > *select model performance* |
| BRBatteryByOs | Under **Reports** > **Endpoint analytics** > **Battery health** > *select OS performance* |
| BRDeviceBatteryAgg | Under **Reports** > **Endpoint analytics** > **Battery health** > *select device performance* |
| BREnergyUsage | Under **Reports** > **Endpoint analytics** > **Battery health** |
| CatalogAppsUpdateList | Under **Apps** > **Monitor** > **Enterprise App Catalog apps with updates** |
| CertificatesByRAPolicy | Under **Devices** > **Monitor** > **Certificates** |
| ComanagedDeviceWorkloads | Under **Reports** > **Cloud attached devices** > **Reports** > **Co-Managed Workloads** |
| ComanagementEligibilityTenantAttachedDevices | Under **Reports** > **Cloud attached devices** > **Reports** > **Co-Management Eligibility** |
| ConfigurationPolicyAggregate | Under **Devices** > **Manage devices** > **Configuration** |
| ConfigurationPolicyAggregateV3 | Under **Devices** > **Manage devices** > **Configuration** |
| ConfigurationPolicyDeviceAggregates | Under **Devices** > **Manage devices** > **Configuration** > *select specific policy* |
| ConfigurationPolicyDeviceAggregatesV3 | Under **Devices** > **Manage devices** > **Configuration** > *select specific policy* |
| ConfigurationPolicyDeviceAggregatesWithPF | Under **Devices** > **Manage devices** > **Configuration** > *select specific policy* |
| ConfigurationPolicyDeviceAggregatesWithPFV3 | Under **Devices** > **Manage devices** > **Configuration** > *select specific policy* |
| DefenderAgents | Under **Reports** > **MicrosoftDefender** > **Reports** > **Agent Status** |
| DependentAppsInstallStatus | Under **Apps** > **All Apps** > *select the dependent app* > **Device install status** |
| DeviceAssignmentStatusByConfigurationPolicy | Under **Devices** > **Manage devices** > **Configuration** > *select specific policy* > **Device assignment status** |
| DeviceAssignmentStatusByConfigurationPolicyForAC | Under **Devices** > **Manage devices** > **Configuration** > *select specific policy* > **Device assignment status** |
| DeviceAssignmentStatusByConfigurationPolicyForASR | Under **Devices** > **Manage devices** > **Configuration** > *select specific policy* > **Device assignment status** |
| DeviceAssignmentStatusByConfigurationPolicyForEDR | Under **Devices** > **Manage devices** > **Configuration** > *select specific policy* > **Device assignment status** |
| DeviceAssignmentStatusByConfigurationPolicyV3 | Under **Devices** > **Manage devices** > **Configuration** > *select specific policy* > **Device assignment status** |
| DeviceCompliance | Device Compliance Org |
| DeviceComplianceTrend | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceConfigurationPolicyStatuses | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceConfigurationPolicyStatusesV3 | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceConfigurationPolicyStatusesWithPF | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceConfigurationPolicyStatusesWithPFV3 | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceEnrollmentFailures | Under **Devices** > **Device onboarding** > **Enrollment** > **Monitor** |
| DeviceFailuresByFeatureUpdatePolicy | Under **Devices** > **Monitor** > **Failure for feature updates** > *click on error* |
| DeviceInstallStatusByApp | Under **Apps** > **All Apps** > *Select an individual app* |
| DeviceIntentPerSettingStatus | Under **Devices** > **All Devices** > *select specific device* |
| DeviceInventoryPolicyStatusesV3 | Under **Devices** > **Manage devices** > **Configuration** > *select specific policy* > **Device assignment status** |
| DeviceInventoryPolicyStatusesWithPF | Under **Devices** > **Manage devices** > **Configuration** > *select specific policy* > **Device assignment status** |
| DeviceNonCompliance | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DevicePoliciesComplianceReport | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DevicePoliciesComplianceReportV3 | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DevicePolicySettingsComplianceReport | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DevicePolicySettingsComplianceReportV3 | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceRunStatesByProactiveRemediation | Under **Reports** > **Endpoint Analytics** > **Proactive remediations** > *Select a remediation* > **Device status** |
| DeviceRunStatesByScript | Under **Devices** > **Manage devices** > **Scripts and remediations** > *select specific script* > **Device status** |
| Devices | All devices list |
| DevicesByAppInv | Under **Apps** > **Monitor** > **Discovered apps** > **Discovered app**> **Export**  |
| DevicesStatusByPolicyPlatformComplianceReport | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DevicesStatusByPolicyPlatformComplianceReportV3 | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DevicesStatusBySettingReport | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DevicesStatusBySettingReportV3 | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceStatusByCompliacePolicyReport | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceStatusByCompliacePolicyReportV3 | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceStatusByCompliancePolicySettingReport | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceStatusByCompliancePolicySettingReportV3 | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceStatusesByConfigurationProfile | Under **Devices** > **Manage devices** > **Configuration** > **Policies** > *select specific policy* > **Device and user check-in status** |
| DeviceStatusesByConfigurationProfileForAppControl | Under **Devices** > **Manage devices** > **Configuration** > **Policies** > *select specific policy* > **Device and user check-in status** |
| DeviceStatusesByConfigurationProfileForASR | Under **Devices** > **Manage devices** > **Configuration** > **Policies** > *select specific policy* > **Device and user check-in status** |
| DeviceStatusesByConfigurationProfileForEDR | Under **Devices** > **Manage devices** > **Configuration** > **Policies** > *select specific policy* > **Device and user check-in status** |
| DeviceStatusesByConfigurationProfileV3 | Under **Devices** > **Manage devices** > **Configuration** > **Policies** > *select specific policy* > **Device and user check-in status** |
| DeviceStatusesByConfigurationProfileWithPF | Under **Devices** > **Manage devices** > **Configuration** > **Policies** > *select specific policy* > **Device and user check-in status** |
| DeviceStatusesByConfigurationProfileWithPFV3 | Under **Devices** > **Manage devices** > **Configuration** > **Policies** > *select specific policy* > **Device and user check-in status** |
| DeviceStatusesByInventoryPolicyWithPF | Under **Devices** > **Manage devices** > **Compliance** |
| DeviceStatusesByInventoryPolicyWithPFV3 | Under **Devices** > **Manage devices** > **Compliance** |
| DeviceStatusSummaryByCompliacePolicyReport | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceStatusSummaryByCompliacePolicyReportV3 | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceStatusSummaryByCompliancePolicySettingsReport | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DeviceStatusSummaryByCompliancePolicySettingsReportV3 | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DevicesWithInventory | Under **Devices** > **All Devices** > **Export** |
| DevicesWithoutCompliancePolicy | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DevicesWithoutCompliancePolicyV3 | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| DriverUpdatePolicyStatusSummary | Under **Devices** > **Manage updates** > **Windows updates** > **Driver updates** |
| EAAnomalyAsset | Under **Reports** > **Endpoint analytics** > **Anomalies** |
| EAAnomalyAssetV2 | Under **Reports** > **Endpoint analytics** > **Anomalies** |
| EAAnomalyDeviceAsset | Under **Reports** > **Endpoint analytics** > **Anomalies** |
| EAAnomalyDeviceAssetV2 | Under **Reports** > **Endpoint analytics** > **Anomalies** |
| EAAppPerformance | Under **Reports** > **Endpoint analytics** > **Application reliability** > **App performance** |
| EADeviceModelPerformance | Under **Reports** > **Endpoint analytics** |
| EADeviceModelPerformanceV2 | Under **Reports** > **Endpoint analytics** |
| EADevicePerformance | Under **Reports** > **Endpoint analytics** |
| EADevicePerformanceV2 | Under **Reports** > **Endpoint analytics** |
| EADeviceScoresV2 | Under **Reports** > **Endpoint analytics** > **Device scores** |
| EAModelScoresV2 | Under **Reports** > **Endpoint analytics** > **Model scores** |
| EAOSVersionsPerformance | Under **Reports** > **Endpoint analytics** > **Application reliability** > **OS versions performance** |
| EAResourcePerfAggByDevice | Under **Reports** > **Endpoint analytics** > **Resource performance** > **Device performance** |
| EAResourcePerfAggByModel | Under **Reports** > **Endpoint analytics** > **Resource performance** > **Model performance** |
| EAResourcePerfCpuSpikeProcess | Under **Reports** > **Endpoint analytics** > **Resource performance** > **Resource performance score** |
| EAResourcePerfRamSpikeProcess | Under **Reports** > **Endpoint analytics** > **Resource performance** > **Resource performance score** |
| EAStartupPerfDevicePerformance | Under **Reports** > **Endpoint analytics** > **Startup performance** > **Device performance** |
| EAStartupPerfDevicePerformanceV2 | Under **Reports** > **Endpoint analytics** > **Startup performance** > **Device performance** |
| EAStartupPerfDeviceProcesses | Under **Reports** > **Endpoint analytics** > **Startup performance** > **Startup processes** |
| EAStartupPerfModelPerformance | Under **Reports** > **Endpoint analytics** > **Startup performance** > **Model performance** |
| EAStartupPerfModelPerformanceV2 | Under **Reports** > **Endpoint analytics** > **Startup performance** > **Model performance** |
| EAWFADeviceList | Under **Reports** > **Endpoint analytics** > **Work from anywhere** > **Device performance** |
| EAWFAModelPerformance | Under **Reports** > **Endpoint analytics** > **Work from anywhere** > **Model performance** |
| EAWFAPerDevicePerformance | Under **Reports** > **Endpoint analytics** > **Work from anywhere** > **Device performance** |
| EnrollmentActivity | Under **Dashboard** > **Device enrollment** and/or **Intune enrolled devices** |
| EnrollmentConfigurationPoliciesByDevice | Under **Devices** > **Device onboarding** > **Enrollment** |
| EpmAggregationReportByApplication | Under **Endpoint security** > **Manage** > **Endpoint Privilege Management** > **Elevation report by applications** |
| EpmAggregationReportByApplicationV2 | Under **Endpoint security** > **Manage** > **Endpoint Privilege Management** > **Elevation report by applications** |
| EpmAggregationReportByPublisher | Under **Endpoint security** > **Manage** > **Endpoint Privilege Management** > **Elevation report by publisher** |
| EpmAggregationReportByPublisherV2 | Under **Endpoint security** > **Manage** > **Endpoint Privilege Management** > **Elevation report by publisher** |
| EpmAggregationReportByUser | Under **Endpoint security** > **Manage** > **Endpoint Privilege Management** > **Elevation report by user** |
| EpmAggregationReportByUserAppByMonth | Under **Endpoint security** > **Manage** > **Endpoint Privilege Management** > **Elevation report by user** |
| EpmAggregationReportByUserV2 | Under **Endpoint security** > **Manage** > **Endpoint Privilege Management** > **Elevation report by user** |
| EpmDeniedReport | Under **Endpoint security** > **Manage** > **Endpoint Privilege Management** > **Elevation report** |
| EpmElevationReportByUserAppByDayToReporting | Under **Endpoint security** > **Manage** > **Endpoint Privilege Management** > **Elevation report** |
| EpmElevationReportElevationEvent | Under **Endpoint security** > **Manage** > **Endpoint Privilege Management** > **Elevation report** |
| EpmInsightsElevationTrend | Under **Endpoint security** > **Manage** > **Endpoint Privilege Management** > **Elevation report** |
| EpmInsightsMostFrequentElevations | Under **Endpoint security** > **Manage** > **Endpoint Privilege Management** > **Elevation report** |
| EpmInsightsReport | Under **Endpoint security** > **Manage** > **Endpoint Privilege Management** > **Elevation report** |
| FeatureUpdateDeviceState | Under **Reports** > **Window Updates** > **Reports** > **Windows Feature Update Report**  |
| FeatureUpdatePolicyFailuresAggregate | Under **Devices** > **Monitor** > **Failure for feature updates** |
| FeatureUpdatePolicyStatusSummary | Under **Devices** > **Manage updates** > **Windows updates** > **Feature updates** |
| FilteredAppsList | Under **Apps** > **All Apps** |
| FirewallStatus | Under **Reports** > **Firewall** > **MDM Firewall status for Windows 10 and later** |
| FirewallUnhealthyStatus | Under **Reports** > **Endpoint security** > **Firewall** |
| GPAnalyticsSettingMigrationReadiness | Under **Reports** > **Group policy analytics** > **Reports** > **Group policy migration readiness** |
| InventoryPolicyDeviceAggregatesV3 | Under **Devices** > **Monitor** |
| InventoryPolicyDeviceAggregatesWithPF | Under **Devices** > **Monitor** |
| MAMAppConfigurationStatus | Under **Apps** > **Monitor** > **App protection status** > **App configuration report** |
| MAMAppConfigurationStatusScopedV2 | Under **Apps** > **Monitor** |
| MAMAppConfigurationStatusV2 | Under **Apps** > **Monitor** |
| MAMAppProtectionStatus | Under **Apps** > **Monitor** > **App protection status** > **App protection report: iOS, Android** |
| MAMAppProtectionStatusScopedV2 | Under **Apps** > **Monitor** |
| MAMAppProtectionStatusV2 | Under **Apps** > **Monitor** |
| Malware | Under **Reports** > **MicrosoftDefender** > **Reports** > **Detected malware** |
| MEMUpgradeReadinessOrgAsset | Under **Devices** |
| NonCompliantCompliancePoliciesAggregate | Under **Reports** > **Device management** > **Device compliance** |
| NonCompliantCompliancePoliciesAggregateV3 | Under **Reports** > **Device management** > **Device compliance** |
| NonCompliantConfigurationPoliciesAggregateWithPF | Under **Reports** > **Device management** > **Device compliance** |
| NonCompliantConfigurationPoliciesAggregateWithPFV3 | Under **Reports** > **Device management** > **Device compliance** |
| NoncompliantDevicesAndSettings | Under **Reports** > **Device management** > **Device compliance** |
| NoncompliantDevicesAndSettingsV3 | Under **Reports** > **Device management** > **Device compliance** |
| NonCompliantDevicesByCompliancePolicy | Under **Reports** > **Device management** > **Device compliance** |
| NonCompliantDevicesByCompliancePolicyV3 | Under **Reports** > **Device management** > **Device compliance** |
| NoncompliantDevicesToBeRetired | Under **Reports** > **Device management** > **Device compliance** |
| OrgAppsInstallStatus | Under **Apps** > **Monitor** > **App install status** |
| OrgDeviceInstallStatus | Under **Devices** > **Monitor** |
| PerSettingDeviceSummaryByConfigurationPolicy | Under **Devices** > **Monitor** > **Configuration profiles** |
| PerSettingDeviceSummaryByConfigurationPolicyForAppControl | Under **Devices** > **Monitor** > **Configuration profiles** |
| PerSettingDeviceSummaryByConfigurationPolicyForEDR | Under **Devices** > **Monitor** > **Configuration profiles** |
| PerSettingDeviceSummaryByInventoryPolicy | Under **Devices** > **Monitor** > **Configuration profiles** |
| PerSettingDeviceSummaryByInventoryPolicyV3 | Under **Devices** > **Monitor** > **Configuration profiles** |
| PerSettingSummaryByDeviceConfigurationPolicy | Under **Devices** > **Monitor** > **Configuration profiles** |
| Policies | Under **Devices** > **Manage Device** > *select specific policy type* |
| PolicyComplianceAggReport | Under **Reports** > **Device management** > **Device compliance** |
| PolicyComplianceAggReportV3 | Under **Reports** > **Device management** > **Device compliance** |
| PolicyNonComplianceAgg | Under **Reports** > **Device management** > **Device compliance** |
| PolicyNonComplianceAggVer3 | Under **Reports** > **Device management** > **Device compliance** |
| PolicyNonComplianceNew | Under **Reports** > **Device management** > **Device compliance** |
| PolicyNonComplianceNewV3 | Under **Reports** > **Device management** > **Device compliance** |
| PolicyRunStatesByProactiveRemediation | Under **Reports** > **Endpoint analytics** |
| QualityUpdateDeviceErrorsByPolicy | Under **Devices** > **Monitor** > **Windows Expedited update failures** > *Select a profile* |
| QualityUpdateDeviceStatusByPolicy | Under **Reports** > **Windows updates** > **Reports** > **Windows Expedited Update Report** |
| QualityUpdatePolicyStatusSummary | Under **Reports** > **Device management** > **Windows updates** |
| RemoteAssistanceSessions | Under **Reports** > **Endpoint analytics** |
| ResourcePerformanceAggregateByDevice | Under **Reports** > **Endpoint analytics** |
| ResourcePerformanceAggregateByModel | Under **Reports** > **Endpoint analytics** |
| SettingComplianceAggReport | Under **Reports** > **Device management** > **Device compliance** |
| SettingComplianceAggReportV3 | Under **Reports** > **Device management** > **Device compliance** |
| TicketingSecurityTaskAppsList | Under **Endpoint security** > **Security tasks** |
| TpmAttestationStatus | Under **Devices** > **Manage devices** > **Configuration** > **Monitor** > **Device encryption status** |
| UnhealthyDefenderAgents | Under **Endpoint Security** > **Antivirus** > **Win10 Unhealthy Endpoints** |
| UserInstallStatusAggregateByApp | Under **Apps** > **All Apps** > *Select an individual app* |
| Users | Under **Users** |
| UserScaleTest | Under **Reports** > **Endpoint analytics** |
| WindowsDeviceHealthAttestationReport | Under **Reports** > **Device management** > **Device Compliance** > **Reports** |
| WindowsUpdatePerPolicyPerDeviceStatus | Under **Devices** > **Manage updates** > **Windows updates** |
| WorkFromAnywhereDeviceList | Under **Reports** > **Endpoint analytics** > **Work from anywhere** |

The following sections describe each listed report.

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
- `ExecutionState`
- `Severity`
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
- `DeviceId`
- `PolicyId`
- `UserId`

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
- `FailedDevicePercentage`
- `Platform`

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
- `ActiveDevices`
- `DeviceScopeId`
- `ModelBatteryAge`
- `ModelBatteryHealthScore`
- `ModelCycleCount`
- `ModelMaximumCapacity`
- `ModelMedianCapacity`
- `ModelMedianCycleCount`
- `ModelMedianRuntime`
- `ModelRuntime`
- `NeedsAttention`
- `PartnerFeaturesBitmask`

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
- `ActiveDevices`
- `DeviceScopeId`
- `NeedsAttention`
- `OsBatteryAge`
- `OsBatteryHealthScore`
- `OsCycleCount`
- `OsMaximumCapacity`
- `OsMedianCapacity`
- `OsMedianCycleCount`
- `OsMedianRuntime`
- `OsRuntime`
- `PartnerFeaturesBitmask`

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
- `BatteryHealthScore`
- `CycleCount`
- `DeviceBatteryCount`
- `DeviceScopeIds`
- `EstimatedBatteryAge`
- `FullChargeActiveRuntime`
- `MaximumCapacity`
- `NeedsAttention`
- `PartnerFeaturesBitmask`

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
- `ActiveDevices`
- `BatteryUsageInPercentage`
- `DeviceScopeId`
- `IsForeground`
- `PartnerFeaturesBitmask`

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

To call this report, you need a minimum role-based access control permission of **Read** for **Managed Devices**. The minimum Microsoft Graph Application required permission is `DeviceManagementManagedDevices.Read.All`.

> [!NOTE]
> The reporting data for this report is updated at a minimum of once per day.

The properties `LastOSUpdateTime` and `LastRebootTime` only populate in the report when the **OS Update Status** setting is enabled in the Google Admin Console. This setting can be found in the Google Admin Console under **Devices** > **Chrome** **Settings**.

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
| `https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs` | POST | The following examples show different types of calls you can make based on the data you need to retrieve. This list isn't comprehensive.<ul><li>Return all devices using CSV format:<br>`{ 'reportName': 'ChromeOSDevices', 'format': 'csv' }`</li><li>Return all devices using JSON format:<br>`{ 'reportName': 'ChromeOSDevices', 'format': 'json' }`</li><li>Use a filter:<br>`{ 'reportName': 'ChromeOSDevices', 'filter':'(ChromeOSDeviceStatus eq  'ACTIVE') ', 'format': 'csv' }`</li><li>Select which columns are included in the report:<br>`{ 'reportName': 'ChromeOSDevices', 'select':['IntuneDeviceId','IntuneDeviceName','MostRecentUserEmail']}`</li></ul>  |

### Check the status of the ChromeOSDevices report

You can check whether the ChromeOSDevices report is complete by using the Microsoft Graph API.

| Microsoft Graph API endpoint | Method |
|---|---|
| `https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs('id')` | GET |

Use the output from this call to check the report status. The following example shows a typical request:
`https://graph.microsoft.com/beta/deviceManagement/reports/exportJobs('ChromeOSDevices_1223a321-4bcd-5432-efg1-0hi9876h1234')`

Repeat the call until the response includes a status of `complete`. When the report is complete, you can download it.

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
- `DeviceConfiguration`
- `EndpointProtection`
- `ModernApps`
- `OfficeApps`
- `ResourceAccess`
- `WindowsUpdateforBusiness`

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
- `MalwareProtectionEnabled`
- `NetworkInspectionSystemEnabled`
- `RealTimeProtectionEnabled`
- `SignatureUpdateOverdue`

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
- `AssignmentStatus`
- `PolicyBaseTypeName`
- `PolicyId`
- `UnifiedPolicyPlatformType`

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
- `AssignmentStatus`
- `PolicyBaseTypeName`
- `PolicyId`
- `UnifiedPolicyPlatformType`

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
- `AssignmentStatus`
- `PolicyBaseTypeName`
- `PolicyId`
- `UnifiedPolicyPlatformType`

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
- `AssignmentStatus`
- `PolicyBaseTypeName`
- `PolicyId`
- `UnifiedPolicyPlatformType`

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
- `AssignmentStatus`
- `PolicyBaseTypeName`
- `PolicyId`
- `UnifiedPolicyPlatformType`

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
- `DeviceType`
- `OS`
- `OwnerType`

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
- `EnrollmentMethod`
- `FailureReason`
- `OS`
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
- `AlertMessage`
- `PolicyId` **(Required)**
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
- `AppInstallState`
- `ApplicationId` **(Required)**
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
- `ComplianceState`
- `DeviceType`
- `OS`
- `OwnerType`
- `UserId`

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
- `DetectionStatus`
- `PolicyId` **(required)**
- `RemediationStatus`

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

[!INCLUDE [platform-scripts-column-mappings](../includes/platform-scripts-column-mappings.md)]

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
- `CategoryName`
- `CompliantState`
- `CreatedDate`
- `DeviceType`
- `EnrollmentType`
- `JailBroken`
- `LastContact`
- `ManagementAgents`
- `ManagementState`
- `OwnerType`

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
> To maintain backwards compatibility, there are mappings that take place. You can map column names that the export API allows you to select, to what you receive back.
>
> The select parameter accepts column aliases, but the filter parameter doesn't.
>
> The values for `EnrollmentType`, `PartnerFeaturesBitmask`, `ManagementAgents`, `CertExpirationDate`, and `IsManaged` are only exported when they're included in the select parameter. These columns aren't exported by default.

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
- `CategoryName`
- `CompliantState`
- `CreatedDate`
- `DeviceType`
- `EnrollmentType`
- `JailBroken`
- `LastContact`
- `ManagementAgents`
- `ManagementState`
- `OwnerType`
- `PartnerFeaturesBitmask`

The following `ProcessorArchitecture` mappings apply to Windows:
- 9 = x64
- 5 = ARM
- 12 = ARM64
- 0 = x86
- default = Unknown

The following `ProcessorArchitecture` mappings apply to macOS:
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
- `AnomalyFirstOccurrenceDateTime`
- `AnomalyLatestOccurrenceDateTime`
- `DeviceImpactedCount`
- `Severity`
- `State`

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
- `AnomalyFirstOccurrenceDateTime`
- `AnomalyLatestOccurrenceDateTime`
- `DeviceImpactedCount`
- `Severity`
- `State`

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
- `ActiveDevices`
- `AppHealthScore`
- `DeviceScopeId`
- `MeanTimeToFailure`
- `PartnerFeaturesBitmask`
- `TotalAppCrashes`
- `TotalAppUsageDuration`

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
- `ActiveDevices`
- `DeviceScopeId`
- `HealthStatus`
- `MeanTimeToFailure`
- `ModelAppHealthScore`
- `PartnerFeaturesBitmask`

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
- `ActiveDevices`
- `DeviceScopeId`
- `HealthStatus`
- `MeanTimeToFailure`
- `ModelAppHealthScore`
- `PartnerFeaturesBitmask`

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
- `DeviceAppHealthScore`
- `DeviceId`
- `DeviceScopeIds`
- `HealthStatus`
- `MeanTimeToFailure`
- `PartnerFeaturesBitmask`
- `TotalAppCrashes`

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
- `DeviceAppHealthScore`
- `DeviceId`
- `DeviceScopeIds`
- `HealthStatus`
- `MeanTimeToFailure`
- `PartnerFeaturesBitmask`
- `TotalAppCrashes`

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
- `AppReliabilityScore`
- `DeviceScopeIds`
- `EndpointAnalyticsScore`
- `HealthStatus`
- `OverviewBatteryHealthScore`
- `PartnerFeaturesBitmask`
- `ResourcePerfScore`
- `StartupPerformanceScore`
- `WorkFromAnywhereScore`

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
- `AppReliabilityScore`
- `DeviceScopeId`
- `EndpointAnalyticsScore`
- `HealthStatus`
- `ModelDeviceCount`
- `OverviewBatteryHealthScore`
- `PartnerFeaturesBitmask`
- `ResourcePerfScore`
- `StartupPerformanceScore`
- `WorkFromAnywhereScore`

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
- `ActiveDevices`
- `DeviceScopeId`
- `MeanTimeToFailure`
- `OSVersionAppHealthScore`
- `PartnerFeaturesBitmask`

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
- `ClockSpeed`
- `Cores`
- `CpuSpikeTimePercentage`
- `CpuSpikeTimeScore`
- `DeviceId`
- `DeviceScopeIds`
- `DiskType`
- `HealthStatus`
- `MachineType`
- `PartnerFeaturesBitmask`
- `ProcessorName`
- `RamSpikeTimePercentage`
- `RamSpikeTimeScore`
- `ResourcePerfScore`
- `TotalRamInMB`

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
- `CpuSpikeTimePercentage`
- `CpuSpikeTimeScore`
- `DeviceScopeId`
- `HealthStatus`
- `MachineType`
- `ModelId`
- `PartnerFeaturesBitmask`
- `ProcessorName`
- `RamSpikeTimePercentage`
- `RamSpikeTimeScore`
- `ResourcePerfScore`
- `TotalDeviceCount`
- `TotalRamInMB`

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
- `CpuSpikeCount`
- `Description`
- `DeviceId`
- `DisplayName`
- `EventDateTime`
- `Publisher`

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
- `Description`
- `DeviceId`
- `DisplayName`
- `EventDateTime`
- `Publisher`
- `RamUsageInMb`

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
- `BlueScreenCount`
- `BootScore`
- `CoreBootTime`
- `CoreLogonTime`
- `DesktopUsableTime`
- `DeviceId`
- `DeviceScopeIds`
- `Disktype`
- `GPBootTime`
- `GPLogonTime`
- `HealthStatus`
- `LogonScore`
- `PartnerFeaturesBitmask`
- `RestartCount`
- `StartupPerformanceScore`

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
- `BlueScreenCount`
- `BootScore`
- `CoreBootTime`
- `CoreLogonTime`
- `DesktopUsableTime`
- `DeviceId`
- `DeviceScopeIds`
- `Disktype`
- `GPBootTime`
- `GPLogonTime`
- `HealthStatus`
- `LogonScore`
- `PartnerFeaturesBitmask`
- `RestartCount`
- `StartupPerformanceScore`

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
- `Median`
- `PartnerFeaturesBitmask`
- `TimePerProcess`
- `TotalDeviceCount`

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
- `AverageBlueScreens`
- `AverageRestarts`
- `CoreBootTime`
- `CoreLogonTime`
- `DeviceScopeId`
- `Disktype`
- `GPBootTime`
- `GPLogonTime`
- `HealthStatus`
- `ModelId`
- `PartnerFeaturesBitmask`
- `StartupPerformanceScore`
- `TotalDeviceRecordCount`

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
- `AverageBlueScreens`
- `AverageRestarts`
- `CoreBootTime`
- `CoreLogonTime`
- `DeviceScopeId`
- `Disktype`
- `GPBootTime`
- `GPLogonTime`
- `HealthStatus`
- `ModelId`
- `PartnerFeaturesBitmask`
- `StartupPerformanceScore`
- `TotalDeviceRecordCount`

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
- `AutoPilotProfileAssigned`
- `AutoPilotRegistered`
- `CompliancePolicySetToIntune`
- `DeviceId`
- `DeviceScopeIds`
- `GraphDeviceIsManaged`
- `IsCloudManagedGatewayEnabled`
- `JoinType`
- `ManagedBy`
- `OtherWorkloadsSetToIntune`
- `Ownership`
- `PartnerFeaturesBitmask`
- `TenantAttached`
- `UpgradeEligibility`

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
- `CloudIdentityScore`
- `CloudManagementScore`
- `CloudProvisioningScore`
- `DeviceScopeId`
- `HealthStatus`
- `ModelDeviceCount`
- `PartnerFeaturesBitmask`
- `WindowsScore`
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
- `CloudIdentityScore`
- `CloudManagementScore`
- `CloudProvisioningScore`
- `DeviceId`
- `DeviceScopeIds`
- `HealthStatus`
- `PartnerFeaturesBitmask`
- `WindowsScore`
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
- `EnrollmentMethod`
- `FailureReason`
- `OS`
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
- `DeviceId`
- `State`

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
- `CompanyName`
- `ElevationType`
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
| ID |
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
- `EventDateTime`
- `Result`

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
- `AggregateState`
- `LatestAlertMessage`
- `OwnerType`
- `PolicyId` **(Required)**

## FeatureUpdatePolicyFailuresAggregate report

The following table contains the possible output when calling the `FeatureUpdatePolicyFailuresAggregate` report:

| Available properties  |
|-|
|     FeatureUpdateVersion  |
|     NumberOfDevicesWithErrors     |
|     PolicyId  |
|     PolicyName  |

You can't filter this report.

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
- `CSPName`
- `MigrationReadiness`
- `ProfileType`

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
- `ExecutionState`
- `Severity`
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
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyName`
- `PolicyPlatformType`
- `PolicyType`
- `UnifiedPolicyPlatformType`
- `UnifiedPolicyType`

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
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyName`
- `PolicyPlatformType`
- `PolicyType`
- `UnifiedPolicyPlatformType`
- `UnifiedPolicyType`

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
- `NumberOfErrorDevices`
- `NumberOfNonCompliantDevices`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyName`
- `PolicyPlatformType`
- `PolicyType`
- `UnifiedPolicyPlatformType`
- `UnifiedPolicyType`

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
- `NumberOfErrorDevices`
- `NumberOfNonCompliantDevices`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyName`
- `PolicyPlatformType`
- `PolicyType`
- `UnifiedPolicyPlatformType`
- `UnifiedPolicyType`

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
- `DeviceType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyName`
- `PolicyPlatformType`
- `PolicyStatus`
- `PolicyType`

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
- `DeviceType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyName`
- `PolicyPlatformType`
- `PolicyStatus`
- `PolicyType`

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
- `NumberOfErrorDevices`
- `NumberOfNonCompliantDevices`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyName`
- `PolicyPlatformType`
- `PolicyType`
- `UnifiedPolicyPlatformType`
- `UnifiedPolicyType`

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
- `NumberOfErrorDevices`
- `NumberOfNonCompliantDevices`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyName`
- `PolicyPlatformType`
- `PolicyType`
- `UnifiedPolicyPlatformType`
- `UnifiedPolicyType`

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
- `DeviceType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyName`
- `PolicyPlatformType`
- `PolicyStatus`
- `PolicyType`

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
- `DeviceType`
- `PolicyBaseTypeName`
- `PolicyId`
- `PolicyName`
- `PolicyPlatformType`
- `PolicyStatus`
- `PolicyType`

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
- `AlertMessage`
- `PolicyId` **(required)**

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
- `AggregateState`
- `OwnerType`
- `PolicyId` **(required)**

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
- `DeviceName`
- `OS`
- `ProviderID`
- `Recipient ID`
- `RecipientName`

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
- `CpuSpikeTimePercentage`
- `CpuSpikeTimePercentageThreshold`
- `CpuSpikeTimeScore`
- `DeviceId`
- `PartnerFeaturesBitmask`
- `RamSpikeTimePercentage`
- `RamSpikeTimePercentageThreshold`
- `RamSpikeTimeScore`
- `ResourcePerfScore`

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
- `CpuSpikeTimePercentage`
- `CpuSpikeTimePercentageThreshold`
- `CpuSpikeTimeScore`
- `ModelId`
- `PartnerFeaturesBitmask`
- `RamSpikeTimePercentage`
- `RamSpikeTimePercentageThreshold`
- `RamSpikeTimeScore`
- `ResourcePerfScore`
- `TotalDeviceCount`

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
- `MalwareProtectionEnabled`
- `NetworkInspectionSystemEnabled`
- `RealTimeProtectionEnabled`
- `SignatureUpdateOverdue`

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
- `UPN`
- `UserEmail`
- `UserId`
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
- `AutoPilotProfileAssigned`
- `AutoPilotRegistered`
- `CompliancePolicySetToIntune`
- `DeviceId`
- `GraphDeviceIsManaged`
- `JoinType`
- `ManagedBy`
- `OtherWorkloadsSetToIntune`
- `Ownership`
- `PartnerFeaturesBitmask`
- `TenantAttached`
- `UpgradeEligibility`


## Next steps

- [Microsoft Graph documentation](/graph/)
- [Intune reports](./reports.md)
