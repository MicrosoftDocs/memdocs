---
title: Group policy settings
titleSuffix: Configuration Manager
description: Understand the local and group policy settings in Windows used by Configuration Manager and Desktop Analytics
ms.date: 07/07/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
ms.localizationpriority: medium
ms.collection: tier3
---

# Group policy settings for Desktop Analytics

*Applies to: Configuration Manager (current branch)*

This article details the local and group policy settings in Windows that Configuration Manager and Desktop Analytics use.

When Configuration Manager enrolls devices into Desktop Analytics, it sets Windows policies to configure the device. In most circumstances, only use Configuration Manager to configure these settings.

## Windows settings

Configuration Manager sets Windows policies in one or both of the following registry keys:

- Group policy object (**GPO**): `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- **Local** policy preference: `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| Policy | Path | Applies to | Value |
|--------|------|------------|-------|
| **CommercialId** | Local | All Windows versions | In order for a device to show up in Desktop Analytics, configure it with your organization's Commercial ID. |
| **AllowTelemetry**  | GPO | Windows 10 | Set `1` for **Basic** (Required), `2` for **Enhanced**, or `3` for **Full** (Optional) diagnostic data. Desktop Analytics requires at least basic diagnostic data. Microsoft recommends that you use the **Optional (limited)** (Enhanced (Limited)) level with Desktop Analytics. For more information, see [Configure Windows diagnostic data in your organization](/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO | Windows 10, version 1803 and later | This setting only applies when the AllowTelemetry setting is `2`. It limits the Enhanced diagnostic data events sent to Microsoft to just those events needed by Desktop Analytics. For more information, see [Windows 10 diagnostic data events and fields collected through the limit enhanced diagnostic data policy](/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields). |
| **AllowDeviceNameInTelemetry** | GPO | Windows 10, version 1803 and later | Enable devices to send the device name. The device name isn't sent to Microsoft by default. If you don't send the device name, it appears in Desktop Analytics as "Unknown". For more information, see [Device name](enroll-devices.md#device-name). |
| **CommercialDataOptIn** | Local | Windows 8.1 and earlier | Desktop Analytics requires a value of `1`. For more information, see [Commercial Data Opt-in in Windows 7](/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |
| **RequestAllAppraiserVersions** | Both | Windows 8.1 and earlier | Desktop Analytics requires a value of `1` for data collection to work correctly. |
| **DisableEnterpriseAuthProxy** | GPO | All Windows versions | If your environment requires a user-authenticated proxy with Windows Integrated Authentication for internet access, Desktop Analytics requires a value of `0` for data collection to work correctly. For more information, see [Proxy server authentication](enable-data-sharing.md#proxy-server-authentication). |

> [!IMPORTANT]
> When you configure the diagnostic data level, you set the upper boundary for the device. By default in Windows 10, version 1803 and later, users can choose to set a lower level. You can control this behavior using the group policy setting, [Configure telemetry opt-in setting user interface](#group-policy-settings-to-customize-the-user-experience).

Starting in version 2006, <!--8402852--> Configuration Manager sets the following Windows policies for the [Windows diagnostic data processor configuration](whats-new.md#support-for-the-windows-diagnostic-data-processor-configuration):

| Policy | Path | Applies to | Value |
|--------|------|------------|-------|
| **AllowDesktopAnalyticsProcessing** | GPO | Windows 10, version 1809 and later | Desktop Analytics requires a value of `2` for data collection to work correctly. |

Starting in version 2010, <!--6979470-->Configuration Manager can configure the **Optional (limited)** level on the devices running Windows build version 19577 or later. For more information, see [Changes to Windows diagnostic data collection](/windows/privacy/changes-to-windows-diagnostic-data-collection#behaviorial-changes). For this diagnostic data level, Configuration Manager sets the following settings:<!-- 8229653 -->

| Policy | Value |
|--------|-------|
| **AllowTelemetry** | `3` for **Optional (limited)** |
| **LimitDumpCollection** | `1` |
| **LimitDiagnosticLogCollection** | `1` |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | `1` |

> [!IMPORTANT]
> In most circumstances, only use Configuration Manager to configure these settings. Don't also apply these settings in domain group policy objects. For more information, see [Conflict resolution](#conflict-resolution).

### Settings from Upgrade Readiness

Windows Analytics also set the following policies through the Upgrade Readiness script:

- CommercialId
- AllowDeviceNameInTelemetry
- CommercialDataOptIn
- RequestAllAppraiserVersions

If you ran the Upgrade Readiness onboarding script on a device, these policy settings may still exist. Don't use the legacy script. Before you enroll the device to Desktop Analytics, remove these previous policy settings.

## Group policy settings

In general, use Configuration Manager collections to target Desktop Analytics settings and enrollment. Use direct membership or queries to include or exclude devices from the collection. For more information, see [How to create collections](../core/clients/manage/collections/create-collections.md).

Configuration Manager configures commercial ID and diagnostic data settings on your target collection. If you need to configure different diagnostic data settings for different group of devices, use group policy settings to override Configuration Manager settings. For example, you need to set **Optional (limited)** level for some devices and **Required** for others. Some devices may have different [proxy server authentication](enable-data-sharing.md#proxy-server-authentication) settings.

The relevant group policy settings are at the following path: **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Data Collection and Preview Builds**.

Group policy settings only modify registry settings in the following key: `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### Conflict resolution

When you use group policy settings to enable complex scenarios, pay special attention to policy settings that can cause configuration conflicts. Configuration Manager only configures [Windows settings](#windows-settings) *if the value doesn't already exist*. Mobile device management (MDM) policies and group policy settings take precedence over Configuration Manager settings, so certain policy configurations could cause issues with Desktop Analytics. Status for devices targeted with MDM and group policy settings may not be accurately reflected in the [Connection health](monitor-connection-health.md) dashboard.

The group policy settings in the following table have the greatest potential to cause conflict with the Windows settings that Configuration Manager sets on devices it enrolls to Desktop Analytics:

| Display name | Registry value | Effect on devices enrolled in Desktop Analytics |
|--------------|----------------|-------------------------------------------------|
| **Configure the Commercial ID** | CommercialId | If you set this policy to a different value, it overrides the Commercial ID set by Configuration Manager. If it's not the same ID, configured devices may not appear in Desktop Analytics. |
| **Allow telemetry** | AllowTelemetry | If you set this policy to a different value, it overrides the global diagnostic data level that you set in Configuration Manager for the target collection. |
| **Limit Enhanced diagnostic data to the minimum required by Windows Analytics** | LimitEnhancedDiagnosticDataWindowsAnalytics | This policy is dependent upon the prior AllowTelemetry setting. Depending upon the level you set in Configuration Manager or with group policy, this policy can change the diagnostic data level on the device to **Enhanced** or **Enhanced (Limited)**. This policy only applies if AllowTelemetry is set to `2` (**Enhanced**). |
| **Allow device name to be sent in Windows diagnostic data** | AllowDeviceNameInTelemetry | If you opt-in to send device names in Configuration Manager, you can override it by configuring this policy to Disabled. When you disable this setting, device names appear as "Unknown" in Desktop Analytics. For more information, see [Device name](enroll-devices.md#device-name). |
| **Configure Authenticated Proxy usage for the Connected User Experience and Telemetry service** | DisableEnterpriseAuthProxy | If you configure Configuration Manager devices to use user-authenticated proxy (`0`), if you then configure this policy to **Disable Authenticated Proxy usage** (`1`), then the device sends diagnostic data in the system context instead of the user's context. If you don't configure the device with a proxy in system context, or the device can't authenticate to the proxy, Windows can't send diagnostic data to Desktop Analytics. |
| **Allow Desktop Analytics Processing** | Allow Desktop Analytics Processing | If you configure this policy to **Disabled** (`0`), devices may not appear in Desktop Analytics. |

> [!NOTE]
> The legacy policy **Configure Connected User Experiences and Telemetry** (TelemetryProxy) allows Windows to forward diagnostic data to a dedicated proxy, instead of using the user (WinINET) or device (WinHTTP) proxy. Some Windows components don't support this policy. If you use this policy, it may cause data quality issues in Desktop Analytics.

#### Behavior of disabled settings

If you configure these group policy settings to **Disabled**, it has different effects on system behavior.

- When you disable the **CommercialId** policy, Windows removes the registry value. The Configuration Manager setting for the commercial ID, which is set in the local policy registry path, then applies to the device.

- For policies that Configuration Manager sets in the same registry location as group policy, when you disable the setting in group policy, Windows removes the registry value. Configuration Manager will set it again on its next policy processing cycle, and then Windows will remove it on the next group policy refresh. This constant change in configuration may cause undesired behaviors with Desktop Analytics.

  - If you set these group policy settings to **Not configured**, Windows removes the value once but doesn't continue to remove it. This configuration lets Configuration Manager apply its values as expected.

### Group policy settings to customize the user experience

These group policy settings aren't required by Configuration Manager or Desktop Analytics. You can configure them in group policy to configure your users' experience with Windows diagnostic data.

| Display name | Registry value | Effect on devices enrolled in Desktop Analytics |
|--------------|----------------|-------------------------------------------------|
| **Configure telemetry opt-in change notifications** | DisableTelemetryOptInChangeNotification | Starting in Windows 10, version 1803, Windows notifies users when the diagnostic data level changes. Use this policy to disable notifications. |
| **Configure telemetry opt-in setting user interface** | DisableTelemetryOptInSettingsUx | When you configure the diagnostic data level, you set the upper boundary for the device. Starting in Windows 10, version 1803, users can set a lower level. Use this policy to prevent users from changing the diagnostic level. For more information, see [Configure Windows diagnostic data in your organization](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management). |
| **Disable deleting diagnostic data** | DisableDeviceDelete | Starting in Windows 10, version 1809, users can delete diagnostic data from the **Diagnostic & feedback** settings page. Use this policy to prevent the deletion of diagnostic data that Microsoft collects from the device. |
| **Disable diagnostic data viewer** | DisableDiagnosticDataViewer | Starting in Windows 10, version 1809, users can enable and open the Diagnostic Data Viewer from the **Diagnostic & feedback** settings page. Use this policy to disable the Diagnostic Data Viewer in Windows settings, and prevent it from showing diagnostic data that Microsoft collects from the device.|
