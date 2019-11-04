---
title: Enroll devices in Desktop Analytics
titleSuffix: Configuration Manager
description: Learn how to enroll devices in Desktop Analytics.
ms.date: 10/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# How to enroll devices in Desktop Analytics

When you [connect Configuration Manager](/sccm/desktop-analytics/connect-configmgr) to Desktop Analytics, you configure settings to enroll devices to Desktop Analytics. You can change these settings at any time. Also make sure the devices are up to date.



## Update devices

There are two main Windows components that Desktop Analytics uses:

- **Compatibility component**. The compatibility component (Appraiser) runs diagnostics on the Windows device to evaluate its compatibility status with the latest versions of the Windows 10. 

- **Connected User Experiences and Telemetry service**. With Windows diagnostic data enabled, the Connected User Experience and Telemetry service (DiagTrack) collects system, application, and driver data. Microsoft analyzes this data, and shares it back to you via Desktop Analytics.

Windows 10 already includes these components, but Windows 7 SP1 and Windows 8.1 require specific updates to be installed. Regardless of the operating system version, Microsoft recommends having a recent version of these components to get the best experience with Desktop Analytics.

The following table shows the minimum and recommended updates for each operating system to use Desktop Analytics:

| OS Version    | Minimum Update | Recommended update |
| --------------| -----------------------  | -------------------|
| Windows 10 1903   | Included  | [Latest cumulative update](https://support.microsoft.com/help/4498140) |
| Windows 10 1809   | Included  | [Latest cumulative update](https://support.microsoft.com/help/4464619) |
| Windows 10 1803   | Included  | [Latest cumulative update](https://support.microsoft.com/en-us/help/4099479), or at least [September 26, 2018 Cumulative Update (KB 4458469)](https://support.microsoft.com/help/4458469) |
| Windows 10 1709   | Included | [Latest cumulative update](https://support.microsoft.com/en-us/help/4043454), or at least [September 26, 2018 Cumulative Update (KB 4457136)](https://support.microsoft.com/help/4457136) |
| Windows 8.1   | [KB 2976978](https://support.microsoft.com/help/2976978) | [Latest monthly rollup](https://support.microsoft.com/en-us/help/4009470), or at least [October 9, 2018 Monthly Rollup (KB 4462926)](https://support.microsoft.com/help/4462926) |
| Windows 7 SP1 | [KB 2952664](https://support.microsoft.com/help/2952664) | [Latest monthly rollup](https://support.microsoft.com/en-us/help/4009469), or at least [October 9, 2018 monthly rollup (KB 4462923)](https://support.microsoft.com/help/4462923) |


> [!Note]  
> When you install the September 26, 2018 Cumulative Update or later on Windows 10 1803 or earlier devices, or the October 9, 2018 Monthly Rollup or later on Windows 7 SP1 or Windows 8.1 devices, you will get the following benefits on those operating systems:
> 
> - Devices that you enroll to Desktop Analytics show up in the service in less than an hour  
> - Devices quickly report the status on Windows feature and quality updates  
>
> Without these updates, these processes can take over 48 hours for a device to report to Desktop Analytics.  

> [!Note]  
> For Windows 7 SP1 and Windows 8.1, there's a related optional update, [KB 3150513](https://support.microsoft.com/help/3150513) on top of either [KB 2952664](https://support.microsoft.com/help/2952664) or [KB 2976978](https://support.microsoft.com/help/2976978) respectively. This update provides updated configuration and definitions for older compatibility updates. This update is not needed if you install October 9, 2018 Monthly Rollup or later.

> [!Note]
> If your organization does not apply "Monthly Quality Rollup" updates to Windows 7 devices, and only applies "Security Only" updates, you will find some "Security Only" updates in the [list of updates superseding KB 2952664](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=ad3652cd-2689-4726-b3ef-b086ded23c7c), that you can install instead of KB 2952664. This is not the case for Windows 8.1, where updates to KB 2976978 are only provided as part of "Monthly Quality Rollup" updates.

> [!Tip]  
> Use Configuration Manager to automatically install these updates, and restart devices after you install the compatibility updates for the first time. For more information, see [Deploy software updates](/sccm/sum/deploy-use/deploy-software-updates).  


## Device enrollment

The Desktop Analytics service has no agents to install. Device enrollment requires configuring settings on the devices you want it to monitor. These settings control to which Desktop Analytics instance the device should send its data, and other configuration options.

> [!Note]  
> If you're already using Windows Analytics, use that same workspace for Desktop Analytics. You need to reenroll devices to Desktop Analytics that you previously enrolled in Windows Analytics.
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


### Windows settings

Configuration Manager sets Windows policies in one or both of the following registry keys:

- **IT policy**: `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- **User** preference: `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| Policy   | Path | Value  | 
|----------|------|--------|
| **CommercialId** | User | *Applies to Windows 7, Windows 8.1, and Windows 10*: In order for a device to show up in Desktop Analytics, configure it with your organization’s Commercial ID. | 
| **AllowTelemetry**  | IT policy | *Applies to Windows 10*: Set `1` for **Basic**, `2` for **Enhanced**, or `3` for **Full** diagnostic data. Desktop Analytics requires at least basic diagnostic data. Microsoft recommends that you use the Enhanced (Limited) level with Desktop Analytics. For more information, see [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | IT Policy | *Applies to Windows 10, version 1803 and later*: This setting only applies when the AllowTelemetry setting is `2`. It limits the Enhanced diagnostic data events sent to Microsoft to just those events needed by Desktop Analytics. For more information, see [Windows 10 diagnostic data events and fields collected through the limit enhanced diagnostic data policy](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields).|
| **AllowDeviceNameInTelemetry** | IT policy | *Applies to Windows 10, version 1803 and later*: A separate opt-in is required to enable devices to continue to send the device name.<br> <br>Note: The device name isn't sent to Microsoft by default. If you don't send the device name, it appears in Desktop Analytics as "Unknown". This behavior can make it difficult to identify and assess devices. For more information, see [Device name](#device-name). | 
| **CommercialDataOptIn** | User |*Applies to Windows 7 and Windows 8.1*: A value of `1` is required for Desktop Analytics. For more information, see [Commercial Data Opt-in in Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |
| **RequestAllAppraiserVersions** | Both |*Applies to all Windows versions*: A value of `1` is required for Desktop Analytics for data collection to work correctly. | 
| **DisableEnterpriseAuthProxy** | IT policy |*Applies to all Windows versions*: A value of `0` is required for Desktop Analytics for data collection to work correctly. | 

> [!Important]  
> In most circumstances, only use Configuration Manager to configure these settings. Don't also apply these settings in domain group policy objects. For more information, see [Conflict resolution](#conflict-resolution).<!-- SCCMDocs-pr 3120 -->

### Device name

Starting in Windows 10, version 1803, the device name is no longer collected by default. Collecting the device name with the diagnostic data requires a separate opt-in. Without the device name, it's more difficult for you to identify what devices require attention while evaluating an upgrade to a new version of Windows.

If you don't send the device name, it appears in Desktop Analytics as "Unknown".

![Desktop Analytics device list showing "unknown" names](media/unknown-device-name.png)

There's an option in the Configuration Manager settings for Desktop Analytics to configure this option: **Allow Device Name in diagnostic data**. This Configuration Manager setting controls the Windows policy setting, AllowDeviceNameInTelemetry.
 

### Conflict resolution

In general, use Configuration Manager collections to target Desktop Analytics settings and enrollment. Use direct membership or queries to include or exclude devices from the collection. For more information, see [How to create collections](/sccm/core/clients/manage/collections/create-collections).

Configuration Manager only configures the Windows settings if a value doesn't already exist. If you need to configure different settings for a unique group of devices, you can use [group policy](#windows-settings). 

View these settings in the group policy editor at the following path: **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Data Collection and Preview Builds**. Settings targeted by group policy take precedence over Configuration Manager settings.

If you target Configuration Manager clients with both Windows Analytics and Desktop Analytics settings, the settings for Desktop Analytics take precedence.

When you configure the diagnostic data level, you set the upper boundary for the device. By default in Windows 10, version 1803 and later, users can choose to set a lower level. You can control this behavior using the group policy setting, **Configure telemetry opt-in setting user interface**. For more information, see [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).



## Next steps

Advance to the next article to create deployment plans in Desktop Analytics.
> [!div class="nextstepaction"]  
> [Create deployment plans](/sccm/desktop-analytics/create-deployment-plans)  
