---
title: Enroll devices in Desktop Analytics
titleSuffix: Configuration Manager
description: Learn how to enroll devices in Desktop Analytics.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
---

# How to enroll devices in Desktop Analytics 

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

When you [connect Configuration Manager](/sccm/desktop-analytics/connect-configmgr) to Desktop Analytics, you configure settings to enroll devices to Desktop Analytics. You can change these settings at any time. Also make sure the devices are up to date. 



## Update devices

There are two types of updates that you need to apply for the best experience with Desktop Analytics: 
- [Compatibility updates](#bkmk_appraiser)  
- [Connected User Experiences and Telemetry service](#bkmk_diagtrack)


### <a name="bkmk_appraiser"></a> Compatibility updates

The compatibility component (Appraiser) runs diagnostics on the Windows device to evaluate its compatibility status with the latest versions of the Windows 10.

Microsoft regularly increments the updates for this component, but the associated KB number doesn't change. Make sure that you always have the latest version of the update.

Restart devices after you install the compatibility updates for the first time.

> [!Tip]  
> Use Configuration Manager to automatically install the latest version of these updates. For more information, see [Deploy software updates](/sccm/sum/deploy-use/deploy-software-updates).  

> [!Note]  
> There's a related optional update, [KB 3150513](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=3150513). This update provides updated configuration and definitions for older compatibility updates. For more information, see [Latest compatibility definition update for Windows](https://support.microsoft.com/help/3150513).  

#### Windows 10
Windows 10 includes the compatibility component. To get the latest compatibility update, install the latest Windows 10 cumulative update.

#### Windows 8.1
Download the update: [KB 2976978](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2976978) 

Runs diagnostics on the Windows 8.1 systems that participate in the Windows Customer Experience Improvement Program. These diagnostics help determine whether you might have compatibility issues when upgrading to Windows 10.

For more information, see [Compatibility update for keeping Windows up-to-date in Windows 8.1](https://support.microsoft.com/help/2976978).

#### Windows 7 with Service Pack 1
Download the update: [KB 2952664](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2952664) 

Runs diagnostics on the Windows 7 with Service Pack 1 (SP1) systems that participate in the Windows Customer Experience Improvement Program. These diagnostics help determine whether you might have compatibility issues when upgrading to Windows 10.

For more information, see [Compatibility update for keeping Windows up-to-date in Windows 7](https://support.microsoft.com/help/2952664).


### <a name="bkmk_diagtrack"></a> Connected User Experiences and Telemetry service

With Windows diagnostic data enabled, the Connected User Experience and Telemetry service (DiagTrack) collects system, application, and driver data. Microsoft analyzes this data, and shares it back to you via Desktop Analytics.

For the best experience, install the following updates depending upon the OS version.

> [!Note]  
> When you install these updates, expect the following behaviors: 
> - Devices that you enroll to Desktop Analytics show up in the service in less than an hour  
> - Devices quickly report the status on feature and quality updates for Windows and Office  
> 
> Without these updates, these processes can take over 48 hours for a device to report to Desktop Analytics.  


#### Windows 10
Install the latest Windows 10 cumulative update.

<!-- 
- Windows 10 1809: Included in RTM build
- Windows 10 1803: [KB4458469](https://support.microsoft.com/help/4458469) (OS Build 17134.319)
- Windows 10 1709: [KB4457136](https://support.microsoft.com/help/4457136) (OS Build 16299.697)
- Windows 10 1703: [KB4457141](https://support.microsoft.com/help/4457141) (OS Build 15063.1358)
- Windows 10 1607: [KB4457127](https://support.microsoft.com/help/4457127) (OS Build 14393.2517)
 -->

#### Windows 8.1
Install the October 2018 monthly rollup, [KB4462926](https://support.microsoft.com/help/4462926)

#### Windows 7
Install the October 2018 monthly rollup, [KB4462923](https://support.microsoft.com/help/4462923)



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

    - **Commercial ID**: you shouldn't need to change or edit this value. For more information on troubleshooting issues with the commercial ID, see [Commercial ID configuration](/sccm/desktop-analytics/troubleshooting#commercial-id-configuration).  

    - **Windows 10 diagnostic data level**: For more information, see [Diagnostic data levels](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

    - **Allow Device Name in diagnostic data**: For more information, see [Device name](#device-name).  

    When you make changes to this page, the **Available functionality** page shows a preview of the Desktop Analytics functionality with the selected diagnostic data settings.  

3. On the **Microsoft 365 Analytics Connection** page, make changes as needed to the following settings:

    - **Display name**: The Desktop Analytics portal displays this Configuration Manager connection using this name.  

    - **Target collection**: This collection includes all devices that Configuration Manager configures with your commercial ID and diagnostic data settings. It's the full set of devices that Configuration Manager connects to the Desktop Analytics service.  

    - **Devices in the target collection use a user-authenticated proxy for outbound communication**: By default, this value is **No**. If needed in your environment, set to **Yes**. For more information, see [Proxy server authentication](/sccm/desktop-analytics/enable-data-sharing#proxy-server-authentication).  

    - **Select specific collections to synchronize with Desktop Analytics**: Select **Add** to include additional collections. These collections are available in the Desktop Analytics portal for grouping with deployment plans. Make sure to include pilot and pilot exclusion collections.  

        These collections continue to sync as their membership changes. For example, your deployment plan uses a collection with a Windows 7 membership rule. As those devices upgrade to Windows 10, and Configuration Manager evaluates the collection membership, those devices drop out of the collection and deployment plan.  


### Windows settings

Configuration Manager sets the following Windows settings under `Microsoft\Windows\DataCollection`:

| Policy   | Value  |
|----------|--------|
| **CommercialId** | In order for a device to show up in Desktop Analytics, configure it with your organization’s Commercial ID. |
| **AllowTelemetry**  |	Set `1` for **Basic**, `2` for **Enhanced**, or `3` for **Full** diagnostic data. Desktop Analytics requires at least basic diagnostic data. Microsoft recommends that you use the Enhanced (Limited) level with Desktop Analytics. For more information, see [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** |	*Applies to Windows 10, version 1709 and later*: This setting only applies when the AllowTelemetry setting is `2`. It limits the Enhanced diagnostic data events sent to Microsoft to just those events needed by Desktop Analytics. For more information, see [Windows 10, version 1709 enhanced diagnostic data events and fields used by Windows Analytics](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields).|
| **AllowDeviceNameInTelemetry** | *Applies to Windows 10, version 1803 and later*: A separate opt-in is required to enable devices to continue to send the device name.<br> <br>Note: The device name isn't sent to Microsoft by default. If you don't send the device name, it appears in Desktop Analytics as "Unknown". This behavior can make it difficult to identify and assess devices. For more information, see [Device name](#device-name). |
| **CommercialDataOptIn** | *Applies to Windows 7 and Windows 8.1*: A value of `1` is required for Desktop Analytics. For more information, see [Commercial Data Opt-in in Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |

View these settings in the group policy editor at the following path: **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Data Collection and Preview Builds**. 


### Device name

Starting in Windows 10, version 1803, the device name is no longer collected by default. Collecting the device name with the diagnostic data requires a separate opt-in. Without the device name, it's more difficult for you to identify what devices require attention while evaluating an upgrade to a new version of Windows or Office. 

If you don't send the device name, it appears in Desktop Analytics as "Unknown".

![Desktop Analytics device list showing "unknown" names](media/unknown-device-name.png)

There's an option in the Configuration Manager settings for Desktop Analytics to configure this option: **Allow Device Name in diagnostic data**. This Configuration Manager setting controls the Windows policy setting, AllowDeviceNameInTelemetry.
 

### Conflict resolution

In general, use Configuration Manager collections to target Desktop Analytics settings and enrollment. Use direct membership or queries to include or exclude devices from the collection. For more information, see [How to create collections](/sccm/core/clients/manage/collections/create-collections).

Configuration Manager only configures the Windows settings if a value doesn't already exist. If you need to configure different settings for a unique group of devices, you can use [group policy](#group-policy). Settings targeted by group policy take precedence over Configuration Manager settings.

If you target Configuration Manager clients with both Windows Analytics and Desktop Analytics settings, the settings for Desktop Analytics take precedence. 

When you configure the diagnostic data level, you set the upper boundary for the device. By default in Windows 10, version 1803 and later, users can choose to set a lower level. You can control this behavior using the group policy setting, **Configure telemetry opt-in setting user interface**. For more information, see [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).



## Next steps

Advance to the next article to create deployment plans in Desktop Analytics.
> [!div class="nextstepaction"]  
> [Create deployment plans](/sccm/desktop-analytics/create-deployment-plans)  
