---
title: Application reliability in endpoint analytics
description: Get details about application reliability in endpoint analytics
titleSuffix: Microsoft Endpoint Manager
ms.date: 03/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: high
---

# Application reliability in endpoint analytics
<!--IN5653073-->
The application reliability report provides insight into potential issues for desktop applications on managed devices. You can quickly identify the top applications that are impacting end-user productivity, and see aggregate app usage along with app failure metrics for these applications. From the report, drill into specific device data and view a timeline of app reliability events to troubleshoot end-user impacting issues.

:::image type="content" source="media/5659073-application-reliability.png" alt-text="Application reliability report in endpoint analytics" lightbox="media/5659073-application-reliability.png":::

## Prerequisites

- Devices are enrolled in endpoint analytics.
   - [Enroll Configuration Manager devices](enroll-configmgr.md)
   - [Enroll Intune devices](enroll-intune.md)
   - After enrollment, client devices require a restart to fully enable all analytics. <!--7698085-->
- Devices enrolled from Configuration Manager need client version 2006, or later installed

## App reliability score

The **App reliability score** provides a high-level view of desktop application robustness across your environment. As with other endpoint analytics scores, the **App reliability score** is a number between 0 and 100. The score is calculated from the app reliability scores of each desktop application in your environment that's found in the **App performance** tab.

Each application on the **App performance** tab is assigned an **App reliability score** based on:

- **Crash frequency**: For each of app, the total number of crashes and the total usage duration over a 14 day rolling window is used to calculate the **Mean time to failure** value. This calculation normalizes the crash rate allowing for direct comparison of the relative frequency of crash events across different applications. This value is the primary contributor to an app's reliability score.
- **Total usage duration**: Factoring in the usage duration across all enrolled devices helps ensure the most disruptive application issues are prioritized.

## App performance tab

The **App performance** tab uses data from the past 14 days to show reliability insights for each desktop application in your organization. The following applications are included in the report:

- Foreground applications with a measurable amount of usage in your organization. This ensures that the report is focused on end-user impacting issues.
- Applications with either an active device count that's greater than 5, or a count greater than 2% of the total number of your tenant's enrolled devices, whichever is larger. This helps filter out noise and ensures that calculations are made across a sufficient number of devices to be meaningful.

:::image type="content" source="media/5659073-app-performance-tab.png" alt-text="Application performance tab in endpoint analytics" lightbox="media/5659073-app-performance-tab.png":::

For each application in the report, the following data is provided:

**App name**: The app identifier in the file manifest provided by your client devices. The app name is typically in executable (or .exe) format.

**App display name**: The `friendly name` of the application reported in the file manifest. This column is hidden by default since the data isn't always available.

**App publisher**: The publisher of the executable reported in the file manifest. Limited cleanup occurs on the app publisher. For instance, `Microsoft Corporation` and `microsoft corporation` are collapsed during cleanup. However, app metadata isn't added or modified in cases where it's unavailable, null, or potentially inaccurate.

**Active devices (14 days)**: The total number of your tenant's enrolled devices that have launched this app at least once in the past 14 days.

**Total usage duration (14 days)**: The cumulative usage duration of the application across all your tenant's enrolled devices over the past 14 days. **Engagement time** is used to determine usage duration. **Engagement time** is composed of both:
   -  Interactive time: The time when the user is actively engaging with an application, such as browsing the web
   - Keep-alive time: Time when the application is requesting a keep-alive from the OS, such as when  presenting a PowerPoint or watching a video.

**Total crashes (14 days)**: The total number of application crash events reported across all enrolled devices in your tenant over the past 14 days.

**Mean time to failure**: The average amount of engagement time that an end user is able to use the application before a crash occurs over the past 14 days. This value is calculated by dividing **Total usage duration (14 days)** by **Total crashes (14 days)**. By relating usage duration and crash counts, the frequency of crashes across different applications is normalized. Applications without crash events in your tenant over the past 14 days are given a mean time to failure value of `No crash events`.

**App reliability score**: A score between 0 and 100 that represents the relative reliability of the application in your tenant. This score is calculated based on **Mean time to failure** and **Total usage duration (14 days)**. A score of 0 represents an unreliable app that is likely hampering end-user productivity. A score of 100 represents a reliable app that is likely contributing to end-user productivity.

> [!NOTE]
> A maximum of 10 application crash events per application, per device, per day is used. This prevents excessive data collections from devices with severe application issues and helps prevent outlier devices from having undue influence over the reliability scores for individual applications.
> 
> Applications with an insignificant amount of foreground usage (about 10 minutes or fewer) on a particular device may not be captured. 

### App performance details

Selecting an app name in the table from **App performance** opens **App performance details**. **App performance details** contain two tabs:

- **App versions**: This tab allows you to compare the number of **App crashes** and number of unique **Devices with crashes** across different versions of the application over the past 14 days. This information can be useful in determining which version of an application is the most reliable. The information can assist with troubleshooting a potential issue with certain versions of an application. You may also find these insights valuable when deciding which version of an application to deploy, whether to install an update or roll back an update.
- **OS versions**: This tab compares the **Mean time to failure** for the application across different versions of Windows. This information can be helpful for identifying potential correlations between OS version and application issues.

:::image type="content" source="media/5659073-app-performance-details.png" alt-text="Application performance details in endpoint analytics" lightbox="media/5659073-app-performance-details.png":::

## Device performance tab

The **Device performance** tab displays application reliability insights for each eligible, enrolled device in your tenant. The **Total app crashes (14 days)** column represents the total number of app crash events from any app reported by the device over the past 14 days. These crash events can be associated with any application installed on the device and aren't necessarily all from the same application.

> [!IMPORTANT]
> App crash events are limited to 10 app crash events per application, per device, per day.

Selecting a device name opens the **Application reliability** tab for that device. This tab displays a timeline of app crash and app unresponsive events for the device over a specified period of time, up to 14 days. Use the **Filter** option at the top of the timeline to select a custom time range.

## Known issues

### Some eligible, enrolled devices aren't appearing in the report due to a client certificate issue

**Scenario**: In certain uncommon situations, devices may be missing from the **Application reliability** report. You can determine how many devices are reporting application reliability data by looking at the number of records in the table on the **Device performance** tab of the **Application reliability** report.

**Impacted devices**: This issue affects devices enrolled in endpoint analytics from Configuration Manager that are unable to download a required ServiceCertificate policy. Without this policy, devices can't report application reliability data to endpoint analytics.

> [!IMPORTANT]
> This isn't a common issue. Before proceeding the mitigation, verify that your missing devices:
> - Meet the [prerequisites](#prerequisites) for the **Application reliability** report
> - Are actively being used
> - Have had sufficient time to start reporting data

Use the following script to determine if a device is impacted by this issue:

```powershell
$query = "SELECT * FROM CCM_PendingPolicyState WHERE PolicyID=""B27D9CFC-84AD-0AF8-9DF1-23EE05E8C05D"""
$obj = Get-WmiObject -Query $query -Namespace "root\ccm\policyagent"
 
foreach ($value in $obj)
{
    if ($value.State  -eq 1)
    {
        Write-Host "Found ServiceCertificate policy in the pending policy list."
    }
} 
```

**Mitigation**: Run the following script on affected devices to force a download of the updated ServiceCertificate policy state. This will resolve the issue, allowing the device to start uploading application reliability data. Allow up to 72 hours to start seeing data in the endpoint analytics portal.

```vbscript
On Error Resume Next

Set WshShell = WScript.CreateObject("WScript.Shell")

'First, find the pending policy object
Set wmiService = GetObject("winmgmts:\\.\root\ccm\policyagent")
Set wmiObjs = wmiService.ExecQuery("SELECT * FROM CCM_PendingPolicyState WHERE PolicyID=""B27D9CFC-84AD-0AF8-9DF1-23EE05E8C05D""")

For Each wmiPendingPolicy In wmiObjs
    If wmiPendingPolicy.State = 1 Then

        WScript.Echo "Found ServiceCertificate policy in the pending policy list. Resetting the state to force re-download"

        wmiPendingPolicy.State = 0
        wmiPendingPolicy.Put_

        If Err.Number <> 0 Then
            WScript.Echo "Failed to update ServiceCertificate policy state. Error code = " & Err.Number
        Else
            WScript.Echo "Successfully updated ServiceCertificate policy state."
        End If

    End If
Next
```
