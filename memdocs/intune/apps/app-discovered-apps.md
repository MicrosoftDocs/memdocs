---
# required metadata

title: Discovered apps
titleSuffix: Microsoft Intune
description: Understand details about the detected apps that Intune found on a device.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/13/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 07dd262f-13e7-4cb2-9cc2-b755d1c276cf

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier1
- M365-identity-device-management
---

# Intune discovered apps

Intune **discovered apps** is a list of detected apps on the Intune enrolled devices in your tenant. It acts as a software inventory for your tenant. **Discovered apps** is a separate report from the [app installation](apps-monitor.md) reports. For personal devices, Intune never collects information on applications that are unmanaged. On corporate devices, any app whether it is a managed app or not is collected for this report. Below is the table mapping the expected behavior. In general, the report refreshes every 7 days from the time of enrollment (not a weekly refresh for the entire tenant). The only exception to this refresh cycle for the **Discovered apps** report is application information collected through the Intune Management Extension for Win32 Apps, which is collected every 24 hours.

## Monitor discovered apps with Intune

Intune provides an aggregated list of detected apps on the Intune enrolled devices in your tenant.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **Monitor** > **Discovered apps**.

>[!NOTE]
>You can export the list of discovered apps to a .csv file by selecting **Export** from the **Discovered apps** pane.
>
>For discovered Win32 apps, there currently is no aggregate count. This type of data can only be viewed on a per-device basis.

Intune also provides the list of discovered apps for the individual device in your tenant.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All Devices**.
3. Select a device.
4. To view detected apps for this device, select **Discovered Apps** in the **Monitor** section.

## Details of discovered apps

The following list provides the app platform type, the apps that are monitored for personal devices, the apps that are monitored for company-owned devices, and the refresh cycle. For more information about app types supported by Intune, see [App types in Microsoft Intune](apps-add.md#app-types-in-microsoft-intune).

| Platform | For personally-owned devices | For company-owned devices | Refresh cycle |
|------------------------------------------------------------------------|----------------------------------|--------------------------------------------------|---------------------------------------|
| Windows 10/11 (Win32 Apps) NOTE: [Requires Intune Management Extension](intune-management-extension.md) on device | Not Applicable | MSI installed apps on the device | Every 24 hours from device enrollment |
| Windows 10/11 (Modern Apps) | Only managed modern apps | All modern apps installed on the device | Every 7 days from device enrollment |
| Windows 8.1 | Only managed apps | Only managed apps | Every 7 days from device enrollment |
| Windows RT | Only managed apps | Only managed apps | Every 7 days from device enrollment |
| iOS/iPadOS | Only managed apps | All apps installed on the device | Every 7 days from device enrollment |
| macOS | Only managed apps | All apps installed on the device | Every 7 days from device enrollment |
| Android device administrator | Only managed apps | All apps installed on the device | Every 7 days from device enrollment |
| Android Enterprise personally-owned enrollment | Only managed apps in the work profile | Not applicable | Every 7 days from device enrollment |
| Android Enterprise corporate-owned enrollments | Not applicable| Not yet supported | Not Applicable |
| AOSP enrollments | Not applicable | Not yet supported | Not applicable |

> [!NOTE]
> - Windows 10/11 co-managed devices, as shown in the [client apps](../../configmgr/comanage/workloads.md#client-apps) workload in Configuration Manager, do not currently collect app inventory through the Intune Management Extension (IME) as per the above schedule. To mitigate this issue, the [client apps](../../configmgr/comanage/workloads.md#client-apps) workload in Configuration Manager should be switched to Intune for the IME to be installed on the device (IME is required for Win32 inventory and PowerShell deployment). Note that any changes or updates on this behavior are announced in [in development](../fundamentals/in-development.md) and/or [what's new](../fundamentals/whats-new.md).
> - Personally-owned macOS devices enrolled before November 2019 may continue to show all apps installed on the device until the devices are enrolled again.
> - Android Enterprise corporate-owned enrollments (fully managed, dedicated, and corporate-owned work profile) do not display discovered apps. 
> - Android Open Source Project (AOSP) enrollments do not display discovered apps. 
> - For customers using a Mobile Threat Defense partner with Intune, [App Sync data](../protect/mtd-connector-enable.md) is sent to Mobile Threat Defense partners at an interval based on device check-in, and should not be confused with the refresh interval for the Discovered Apps report.

The number of discovered apps may not match the app install status count. Possibilities for inconsistencies include:

- A targeting change of an installed managed app can cause the install count in the status pane to decrement, but remain reported in the detected apps.
- Targeting multiple instances of the same app in a tenant will result in different counts due to potential overlap of users or devices. Each instance of the app will count overlapping users, but discovered apps will have duplicated counts.
- Discovered apps and app status are collected at different time intervals, which could cause a discrepancy in the app counts.

## Next steps

- [App types in Microsoft Intune](apps-add.md#app-types-in-microsoft-intune)
- [Monitor app information and assignments with Microsoft Intune](apps-monitor.md)
