---
title: Enroll devices in Desktop Analytics
titleSuffix: Configuration Manager
description: Learn how to enroll devices in Desktop Analytics.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to enroll devices in Desktop Analytics

When you [connect Configuration Manager](/sccm/desktop-analytics/connect-configmgr) to Desktop Analytics, you configure settings to enroll devices to Desktop Analytics. You can change these settings at any time. Also make sure the devices are up to date.

## Update devices

Desktop Analytics uses two main Windows components:

- **Compatibility component**: The compatibility component (**Appraiser**) runs diagnostics on the Windows device to evaluate its compatibility status with the latest versions of Windows 10.

- **Connected User Experiences and Telemetry service**: With Windows diagnostic data enabled, the Connected User Experience and Telemetry service (**DiagTrack**) collects system, application, and driver data. Microsoft analyzes this data, and shares it back to you via Desktop Analytics.

Install the latest version of these components to get the best experience with Desktop Analytics.

The following table lists the updates for each component on supported OS versions:

| OS version | Appraiser | DiagTrack |
| --------------| ----------------------- | -------------------|
| Windows 10 1909 | Included <sup>[Note 1](#bkmk_note1)</sup> | [Latest cumulative update](https://support.microsoft.com/help/4529964) |
| Windows 10 1903 | Included | [Latest cumulative update](https://support.microsoft.com/help/4498140) |
| Windows 10 1809 | Included | [Latest cumulative update](https://support.microsoft.com/help/4464619) |
| Windows 10 1803 | Included | [Latest cumulative update](https://support.microsoft.com/help/4099479) |
| Windows 10 1709 | Included | [Latest cumulative update](https://support.microsoft.com/help/4043454) |
| Windows 8.1 | [KB 2976978](https://support.microsoft.com/help/2976978) <sup>[Note 2](#bkmk_note2)</sup> | [Latest monthly rollup](https://support.microsoft.com/help/4009470) |
| Windows 7 SP1 | [KB 2952664](https://support.microsoft.com/help/2952664) <sup>[Note 3](#bkmk_note3)</sup> | [Latest monthly rollup](https://support.microsoft.com/help/4009469) |

> [!TIP]
> Use Configuration Manager to automatically install these updates. For more information, see [Deploy software updates](/sccm/sum/deploy-use/deploy-software-updates).
>
> Restart devices after you install the compatibility updates for the first time.

### <a name="bkmk_note1"></a> Note 1: Windows 10

While Windows 10 includes these components by default, Windows 10 devices require the latest cumulative update to get the full functionality of Desktop Analytics. For example, to assess the device for compatibility against the latest OS version, and to get the near real-time information for deployments and enrollment status.

### <a name="bkmk_note2"></a> Note 2: Windows 8.1

Microsoft regularly increments the updates for this component, but the associated KB number doesn't change. Make sure that you always have the latest version of the update.

This component runs diagnostics on Windows 8.1 systems that participate in the Windows Customer Experience Improvement Program. These diagnostics help determine whether you might have compatibility issues when upgrading to Windows 10.

### <a name="bkmk_note3"></a> Note 3: Windows 7

If your organization doesn't apply "Monthly Quality Rollup" updates to Windows 7 devices, and only applies "Security Only" updates, you'll find some "Security Only" updates in the [list of updates superseding KB 2952664](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=ad3652cd-2689-4726-b3ef-b086ded23c7c). You can install these newer updates instead of KB 2952664.

> [!NOTE]
> For Windows 8.1, Microsoft only revises KB 2976978 as part of "Monthly Quality Rollup" updates.

## Device enrollment

The Desktop Analytics service has no agents to install. Device enrollment requires configuring settings on the devices you want it to monitor. These settings control to which Desktop Analytics instance the device should send its data, and other configuration options.

> [!Note]  
> If you previously used Windows Analytics, use that same workspace for Desktop Analytics. You need to reenroll devices to Desktop Analytics that you previously enrolled in Windows Analytics.
>
> You can only have one Desktop Analytics workspace per Azure AD tenant. Devices can only send diagnostic data to one workspace.  

Configuration Manager provides an integrated experience for managing and deploying these settings to clients. For the best experience, use Configuration Manager.

When you connect Configuration Manager to Desktop Analytics, you configure the settings to enroll devices. For more information, see [How to connect Configuration Manager with Desktop Analytics](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

To change these settings, use the following procedure:

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node. Select the connection to Desktop Analytics, and choose **Properties** in the ribbon.

2. On the **Diagnostic Data** page, make changes as needed to the following settings:  

    - **Commercial ID**: this value should automatically populate with your organization's ID. If it doesn't, make sure your proxy server is configured to allow all required [endpoints](/sccm/desktop-analytics/enable-data-sharing#endpoints) before continuing. Alternatively, retrieve your Commercial ID manually from the [Desktop Analytics portal](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID).   

    - **Windows 10 diagnostic data level**: For more information, see [Diagnostic data levels](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

    - **Allow Device Name in diagnostic data**: For more information, see [Device name](#device-name).  

    When you make changes to this page, the **Available functionality** page shows a preview of the Desktop Analytics functionality with the selected diagnostic data settings.  

3. On the **Desktop Analytics Connection** page, make changes as needed to the following settings:

    - **Display name**: The Desktop Analytics portal displays this Configuration Manager connection using this name.  

    - **Target collection**: This collection includes all devices that Configuration Manager configures with your commercial ID and diagnostic data settings. It's the full set of devices that Configuration Manager connects to the Desktop Analytics service.  

    - **Devices in the target collection use a user-authenticated proxy for outbound communication**: By default, this value is **No**. If needed in your environment, set to **Yes**. For more information, see [Proxy server authentication](/sccm/desktop-analytics/enable-data-sharing#proxy-server-authentication).  

    - **Select specific collections to synchronize with Desktop Analytics**: Select **Add** to include additional collections from your **Target collection** hierarchy. These collections are available in the Desktop Analytics portal for grouping with deployment plans. Make sure to include pilot and pilot exclusion collections.  <!-- 4097528 -->

        > [!Important] 
        > These collections continue to sync as their membership changes. For example, your deployment plan uses a collection with a Windows 7 membership rule. As those devices upgrade to Windows 10, and Configuration Manager evaluates the collection membership, those devices drop out of the collection and deployment plan.  


## Windows settings

When enrolling devices into Desktop Analytics, Configuration Manager sets Windows policies in one or both of the following registry keys:

- **GPO**: `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- **Local Policy** preference: `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| Policy   | Path | Value  | 
|----------|------|--------|
| **CommercialId** | Local Policy | *Applies to Windows 7, Windows 8.1, and Windows 10*: In order for a device to show up in Desktop Analytics, configure it with your organization’s Commercial ID. | 
| **AllowTelemetry**  | GPO | *Applies to Windows 10*: Set `1` for **Basic**, `2` for **Enhanced**, or `3` for **Full** diagnostic data. Desktop Analytics requires at least basic diagnostic data. Microsoft recommends that you use the Enhanced (Limited) level with Desktop Analytics. For more information, see [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO | *Applies to Windows 10, version 1803 and later*: This setting only applies when the AllowTelemetry setting is `2`. It limits the Enhanced diagnostic data events sent to Microsoft to just those events needed by Desktop Analytics. For more information, see [Windows 10 diagnostic data events and fields collected through the limit enhanced diagnostic data policy](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields).|
| **AllowDeviceNameInTelemetry** | GPO | *Applies to Windows 10, version 1803 and later*: A separate opt-in is required to enable devices to continue to send the device name.<br> <br>Note: The device name isn't sent to Microsoft by default. If you don't send the device name, it appears in Desktop Analytics as "Unknown". This behavior can make it difficult to identify and assess devices. For more information, see [Device name](#device-name). | 
| **CommercialDataOptIn** | Local Policy |*Applies to Windows 7 and Windows 8.1*: A value of `1` is required for Desktop Analytics. For more information, see [Commercial Data Opt-in in Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |
| **RequestAllAppraiserVersions** | Both |*Applies to Windows 7 and Windows 8.1*: A value of `1` is required for Desktop Analytics for data collection to work correctly. | 
| **DisableEnterpriseAuthProxy** | GPO |*Applies to all Windows versions*: A value of `0` is required for Desktop Analytics for data collection to work correctly when using a user-authenticated proxy (using Windows Integrated Authentication) for Internet access.| 

> [!Important]  
> Under most circumstances, it is recommended to only use Configuration Manager to configure these settings. Applying these settings through local or domain group policy objects could potentially cause configuration problems. For more information, see [Group Policy settings](#group-policy-settings).

> [!Tip]
> The predecessor of Desktop Analytics, Windows Analytics Upgrade Readiness, also set the following policies through the Upgrade Readiness script: *CommercialId*, *AllowDeviceNameInTelemetry*, *CommercialDataOptIn* and *RequestAllAppraiserVersions*. If you have these policies in a device not enrolled in Desktop Analytics, most probably the device was targeted with Upgrade Readiness script in the past. In such case, ensure Upgrade Readiness script does not run on the device and remove these policies before enrolling it into  Desktop Analytics.
>


### Device name

Starting in Windows 10, version 1803, the device name is no longer collected by default. Collecting the device name with the diagnostic data requires a separate opt-in. Without the device name, it's more difficult for you to identify what devices require attention while evaluating an upgrade to a new version of Windows.

If you don't send the device name, it appears in Desktop Analytics as "Unknown".

![Desktop Analytics device list showing "unknown" names](media/unknown-device-name.png)

There's an option in the Configuration Manager settings for Desktop Analytics to configure this option: **Allow Device Name in diagnostic data**. This Configuration Manager setting controls the Windows policy setting, AllowDeviceNameInTelemetry.
 


## Group Policy settings

In general, is recommended to only use Configuration Manager collections to target Desktop Analytics settings and enrollment. Use direct membership or queries to include or exclude devices from the collection. For more information, see [How to create collections](/sccm/core/clients/manage/collections/create-collections).

Configuration Manager only allows you to use only one target collection to configure commercial ID and diagnostic data settings. 
If you need to configure different diagnostic data settings for different group of devices (i.e. using "Enhanced (Limited)" level for some devices and "Basic" or "Full" for others, or different proxy authentication settings), you can use group policy settings to override Configuration Manager settings in order to implement such scenarios.

There are a number of policy settings available through group policy editor at the following path: **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Data Collection and Preview Builds**. 

As opposed to Configuration Manager, group policy settings only modify registry settings in the following location:

- **GPO**: `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

> [!Important]  
> When using Group Policy settings to enable complex scenarios, pay special attention to policies that can cause configuration conflicts. Configuration Manager only configures [Windows settings](#windows-settings) **if the value doesn't already exist**, and Group Policy settings take precedence over Configuration Manager settings, so certain group policy configurations could cause issues with Desktop Analytics.


### Group Policy settings that could cause collisions

From the group policy settings available, there are some that could cause isues with Desktop Analytics if not set carefully, due to  configuration conflicts with settings defined in Configuration Manager:

| Policy   | Display Name | Effect on devices enrolled in Desktop Analytics | 
|----------|--------------|-------------------------------------------------|
| **CommercialId** | *Configure the Commercial ID* | If you set this policy to a different value, it will override the Commercial ID set by through Configuration Manager and prevent affected devices to show up in Desktop Analytics.|
| **AllowTelemetry** | *Allow Telemetry* | If you set this policy to a different value that the one set in Configuration Manager, it will override diagnostic data level set globally in Configuration Manager for specific devices.|
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | *Limit Enhanced diagnostic data to the minimum required by Windows Analytics* | If you set "Enhanced Limited" or "Enhanced" in Configuration Manager, setting this policy could cause the device to limit or not limit enhanced diagnostic level depending on configured setting. If AllowTelemetry in either Configuration Manager or Group Policy is set a value other than 2 (Enhanced), setting this policy will have no effect.|
| **AllowDeviceNameInTelemetry** | *Allow device name to be sent in Windows diagnostic data* | If you opted-in to send device names in Configuration Manager, setting this policy to Disabled will override such setting, causing device names appear as "Unknown" in Desktop Analytics. For more information, see [Device name](#device-name).|
| **DisableEnterpriseAuthProxy** | *Configure Authenticated Proxy usage for the Connected User Experience and Telemetry service* | If you set in Configuration Manager to use user-authenticated proxy (0), setting this policy to "Disable Authenticated Proxy usage" (1) will cause the device to use system context instead of user context to send diagnostic data. If the device has no proxy configured in system context or cannot authenticate against it as device, Windows will not be able to send diagnostic data to Desktop Analytics.|
| **TelemetryProxy** | *Configure Connected User Experiences and Telemetry* | This legacy policy allows Windows to forward diagnostic data to a dedicated proxy, instead of using user (WinINET) or device (WinHTTP) proxy. While not specifically a colliding setting, is included here because **its use is not recommended**. Because not all Windows components involved in diagnostic data collection are aware of this configuration, using this setting causes data quality issues in Desktop Analytics. Use only as last resort.|


> [!Important]  
> Settings these group policy settings to "Disabled" have different effects on system behavior.
> For **CommercialId**, if you set the policy to "Disabled", the registry value will be removed, and Configuration Manager Commercial ID setting, set in local policy registry path, will take effect.
>
> For the rest of policies, because Configuration Manager sets registry settings in the same registry location that group policy, if you set the policy to "Disabled", the registry value will be removed, causing Configuration Manager to set it in next processing cycle, and be removed again on hext GPO refresh, causing a configuration conflict.
>
> Setting policies previously configured back to "Not configured" (within the same group policy object) will remove previously set value only once, letting Configuration Manager to apply its values as expected.


### Group Policy settings to customize user experience

There is another set of of group policy settings that help administrators configure diagnostic data experience for end users. Unlike previous policies, these policies does not collide with settings configured in Configuration Manager for Desktop Analytics:

| Policy   | Display Name | Effect on devices enrolled in Desktop Analytics | 
|----------|--------------|-------------------------------------------------|
| **DisableTelemetryOptInChangeNotification** | *Configure telemetry opt-in change notifications* | Starting Windows 10 1803, users get notified when diagnostic data level changes. Administrators can use this policy to disable notifications.|
| **DisableTelemetryOptInSettingsUx** | *Configure telemetry opt-in setting user interface* | When you configure the diagnostic data level, you set the upper boundary for the device. Starting Windows 10 1803, users can choose to set a lower level. Administrators can use this policy to prevent users from lower the diagnostic level. For more information, see [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).|
| **DisableDeviceDelete** | *Disable deleting diagnostic data* | Starting Windows 10 1809, users can delete diagnostic data from Diagnostic & Feedback Settings page. Administrators can use this policy to preventing the deletion of diagnostic data collected by Microsoft from the device.|
| **DisableDiagnosticDataViewer** | *Disable diagnostic data viewer* | Starting Windows 10 1809, users can enable and launch the Diagnostic Data Viewer from the Diagnostic & Feedback Settings page. Administrators can use this policy to disable the Diagnostic Data Viewer in Settings page, and prevent the viewer from showing diagnostic data collected by Microsoft from the device.|


## Proxy settings

Proxy settings are one of the most common sources of issues with Desktop Analytics device enrollment experience.
When using user-authenticated proxies (Windows Integrated Authentication) to reach the Internet, administrators have the option to configure user-authenticated proxy in Configuration Manager (DisableEnterpriseAuthProxy=0).
When doing so, Windows will use logged-on user's Internet proxy settings (typically set in Internet Explorer or Settings/Network & Internet/Proxy) to send diagnostic data to Desktop Analytics, and also use logged-on user's context to authenticate against the proxy server.

However, there are circumstances where user-authenticated proxy might not work as expected, and a device-based proxy configuration could be helpful to enroll devices in Desktop Analytics, like:

- Using Desktop Analytics together with Microsoft Defender Advanced Threat Protection.
- Using Desktop Analytics for devices where there is no logged on user or when the logged on user does not have Internet access.
- Using Desktop Analytics with authenticated proxies that don't use Windows Integrated Authentication. 

When user-authenticated proxy is not configured (DisableEnterpriseAuthProxy not set to 0), Windows will use system context's proxy settings, and use device identity to authenticate against the proxy server to send diangnostic data. 

[!Important]
> Using user-authenticated proxy (DisableEnterpriseAuthProxy=0) is incompatible with Microsoft Defender Advanced Threat Protection, that enforces DisableEnterpriseAuthProxy=1. For more information see [Configure machine proxy and Internet connectivity settings](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).
>
>When using Desktop Analytics together with Defender ATP, if system-wide proxy settings are not properly configured or the device identity cannot be properly authenticated by the proxy server, Windows will not be able to send diagnostic data to Desktop Analytics.

When a user-authenticated proxy does not work as expected, administrators can use different techniques to configure a system-wide proxy, including the use of transparent proxies, web-proxy auto discovery (WPAD), setting WinHTTP default proxy (through "netsh winhttp" context), or configuring machine-wide WinINET proxy using *Make proxy settings per-machine (rather than per-user)* group policy setting (ProxySettingsPerUser=1). TelemetryProxy policy could also be used for this purpose as last resort, due to data quality issues in Desktop Analytics.

If your proxy server uses a custom authentication mechanism (not Windows integrated authentication) or cannot authenticate device identities, you might also need to whitelist [Desktop Analytics endpoints](https://docs.microsoft.com/en-us/configmgr/desktop-analytics/enable-data-sharing#endpoints) in order to send diagnostic data.



## Next steps

Advance to the next article to create deployment plans in Desktop Analytics.
> [!div class="nextstepaction"]  
> [Create deployment plans](/sccm/desktop-analytics/create-deployment-plans)  
