---
# required metadata

title: Monitor security baselines deployed by Microsoft Intune
description: Monitor device and per-setting results of security baselines you deploy with Microsoft Intune, and identify conflicts for devices.
keywords:
author: brenduns 
ms.author: brenduns
manager: dougeby
ms.date: 08/22/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: juidaewo
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- sub-secure-endpoints
---

# Monitor security baselines and profiles in Microsoft Intune

Intune provides several options to monitor security baselines. You can:

- Monitor a security baseline, and any devices that match (or don't match) the recommended values.
- Monitor the security baselines profile that applies to your users and devices.
- View how the settings from a selected profile are set on a selected device.

You can also view the [Device configuration report](../fundamentals/reports.md#device-configuration-operational) to see which device configuration based policies apply to individual devices, which include security baselines.

For more information about the feature, see [Security baselines in Intune](security-baselines.md).

> [!NOTE]
>
> In May 2023, Intune began rollout of a new security baseline format that applies to new baseline types, like Microsoft 365 Apps, and to the newer versions of existing baselines, like Microsoft Edge baseline version 112. The new format updates the baseline settings to directly take their name and configuration options from the configuration service provider (CSP) that the baseline setting manages.
>
> Intune also introduced a new process to help you [*migrate an existing security baseline profile to the newer baseline version*](../protect/security-baselines-configure.md#update-a-baseline-to-the-new-format). This new behavior is a one-time process that replaces the normal update behavior when you move from the most recent version of an older profile to a newer version that became available in May 2023 or later.
>
> Baselines instances that use this new format also have an updated report and monitoring structure that aligns to other report improvements rolled out this year across Intune feature areas. The report view details for the [new format](#monitor-the-baseline-and-your-devices) are presented in this article separately from the [original details provided for the older baselines](#monitor-profiles-for-baseline-versions-released-before-may-2023), many of the concepts discussed for the older views remain relevant.

## Monitor the baseline and your devices

> [!TIP]
>
> The following information applies to profile versions released in May 2023 or later. To view information for profile versions released prior to May 2023, see [Monitor profiles for baseline versions released before May 2023](#monitor-profiles-for-baseline-versions-released-before-may-2023), later in this article.

When you select a security baseline profile that you've deployed, you can gain insights into the security state of devices that received that baseline. To view these insights, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Endpoint security** > **Security baselines** and select a security baseline type like the *Microsoft 365 Apps for Enterprise Security Baseline*. Then, from the *Profiles* pane, select the profile instance for which you want to view details to open the profiles dashboard view.

:::image type="content" source="./media/security-baselines-monitor/view-baseline-policy-details.png" alt-text="View the dashboard for a security baseline profile.":::

This dashboard view includes:

- A high-level summary of the default report, **Device and user check-in status**.
- A **View report** option to drill in for more details.
- Two additional report tiles:
  - Device assignment status
  - Per setting status
- A **Properties** list where you can review and edit the security baseline’s configuration.

### Summary view

This summary is a simple chart that presents a count of devices that report a specific status result for the baseline. The horizontal bar is divided into colors from the available categories in proportion to the count of devices in each category. In the preceding screen capture, a single device has processed the policy and reported success. As a result, the representational bar is entirely green.

### View report

When you select the *View report* button, Intune displays a more detailed view of the *Device and user check-in status* for this baseline instances. When you open the report for the first time, it will be empty until you select **Generate report**, after which it displays information.

:::image type="content" source="./media/security-baselines-monitor/device-assignment-status-report-with-results.png" alt-text="View the report details for Device and user check-in status.":::

The preceding image displays the initial *View report* results for the same baseline from the dashboard view. This view shows that there are two other devices that have an *Assignment status* of *Pending*, which means they haven't yet returned status for this baseline.

You can filter this report view for specific *Assignment status* values, and the select **Generate again** to update the visible results. You can also sort any of the available columns.

If you select the name of a device from the *Device name* column, Intune displays the *Profile Settings* view where you can view that devices status results for each setting in the security baseline. Next, from the Profile Settings page, you can select a setting to view more details, which is useful when a device reports a result for any setting other than *Succeeded*.

In the following image, we drill in on EAGLE003, the only device to show success for the baseline, and then selected the setting *Add-on Management*:

:::image type="content" source="./media/security-baselines-monitor/drill-in-for-setting-details-pane.png" alt-text="View a devices' reported status for each setting in the baseline.":::

On the settings Setting Details pane, we can see each profile that is assigned to this device that also configures this same setting.

For this device, there's only one source profile that manages the Add-on-management setting. If there were other profiles that configured this setting, those profiles would also be listed as a Source Profile.

Should this setting be in conflict, this view can help you identify the other profiles so you can then reconcile a consistent configuration, or later baseline profile assignments to remove the conflict.

### Device assignment status report

Select the *Device assignment status* tile to view this report. In this report:

- Results are a list of devices, similar to the *Device and user check-in status* report.
- Selecting a device on this page opens that devices Profile Settings view, which is the same view you can see from the main report drill-in you access from the View report button. However, devices that have an Assignment status of Pending don't have results to display.
- Selecting a setting from this view opens the Setting Details pane, same as via the main report-drill in.

### Per setting status report

Select the *Per setting status* tile to view this report. This report displays a list of the settings in the profile and for each, the count of results from devices for each status, like how many devices report Success, Error, or Conflict.

This view has no support to drill-in. Instead, to pursue settings that are in error or conflict you can use the other reports and view. For example, to find more about any devices that might have reported an Error or Conflict, you can then open the *Device assignment status* tile, and for that report, scope the report status to show only the status you're investigating. Then, with that report you can continue to drill-in to run-down the relevant details.

### Properties

Below the reports section of the dashboard, you can find the profiles *Properties* view. From Properties you can:

- View the configuration of each page of the profile.
- **Edit** the profiles configuration, like the friendly name you gave the profile, its *Assignments*, and any of the profile settings.

:::image type="content" source="./media/security-baselines-monitor/view-profile-configurations.png" alt-text="View the baselines configuration, where you can edit to make changes.":::

## Monitor profiles for baseline versions released before May 2023

> [!TIP]
>
> The following information applies to profile versions released before May 2023. To view information for profile versions released after May 2023, see [Monitor the baseline and your devices](#monitor-the-baseline-and-your-devices), earlier in this article.

When you monitor a baseline, you get insight into the security state of your devices based on Microsoft's recommendations. To view these insights, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Endpoint security** > **Security baselines** and select a security baseline type like the *Security Baseline for Windows 10 and later*. Then, from the *Versions* pane, select the profile instance for which you want to view details to open its *Overview* pane.

The *Overview* pane displays two status views for the selected baseline:

- **Security baseline posture** chart - This chart displays high-level details about device status for the baseline version. The available details:
  - **Matches default baseline** – This status identifies when a devices configuration matches the default (unmodified) baseline configuration.
  - **Matches custom settings** – This status identifies when a devices configuration matches the customized version of the baseline that you've deployed.
  - **Misconfigured** – This status is a roll-up that represents three status conditions from a device: *Error*, *Pending*, or *Conflict*. These separate states are available from other views, like the *Security baseline posture by category*, a list view that appears below this chart.
  - **Not applicable** - This status represents a device that can’t receive the policy. For example, the policy updates a setting specific to the latest version of Windows, but the device runs an older (earlier) version that doesn’t support that setting.

- **Security baseline posture by category** - A list view that displays device status by category. In this list view, the same details as the *Security baseline posture* chart are available. However, in place of *Misconfigured* there are three columns for the status states that make up Misconfigured:

  - **Error**: The policy failed to apply. The message typically displays with an error code that links to an explanation.
  - **Conflict**: Two settings are applied to the same device, and Intune can't sort out the conflict. An administrator should review.
  - **Pending**: The device hasn't checked in with Intune to receive the policy yet.

When you drill-in to the two preceding views, you can view the following details for the setting status and the device status list views:

- **Succeeded**: Policy is applied.
- **Error**: The policy failed to apply. The message typically displays with an error code that links to an explanation.
- **Conflict**: Two settings are applied to the same device, and Intune can't sort out the conflict. An administrator should review.
- **Pending**: The device hasn't checked in with Intune to receive the policy yet.
- **Not applicable**: The device can't receive the policy. For example, the policy updates a setting specific to the latest version of Windows, but the device runs an older (earlier) version that doesn’t support that setting.

From the *Version* view, you can select **Device Status**. The Device Status view displays a list of the devices that receive this baseline and includes the following details:

- *USER PRINCIPAL NAME* - The user profile associated with the baseline on the device.
- *SECURITY BASELINE POSTURE* - This column displays the devices state:
  - **Succeeded**: Policy is applied.
  - **Error**: The policy failed to apply. The message typically displays with an error code that links to an explanation.
  - **Conflict**: Two settings are applied to the same device, and Intune can't sort out the conflict. An administrator should review.
  - **Pending**: The device hasn't checked in with Intune to receive the policy yet.
  - **Not applicable**: The device can't receive the policy. For example, the policy updates a setting specific to the latest version of Windows, but the device runs an older (earlier) version that doesn’t support that setting
- *Last CHECK-IN* - When status was last received from the device.

> [!TIP]
>
> It takes up to 24 hours for data to appear after you first assign a baseline. Later changes take up to six hours to appear.

### Monitor the profile

Monitoring the profile gives insight into the deployment state of your devices, but not the security state based on the baseline recommendations.

1. In Intune, select **Endpoint security** > **Security baselines**, *select a security baseline type like the Security Baseline for Windows 10 and later* > *select an instance of that baseline* > **Properties**.

2. In the *Properties* of the baseline, expand **Settings** to drill-in and view all the settings categories and individual settings in the baseline, including their configuration for this instance of the baseline.

   ![Screen image showing the settings view](./media/security-baselines-monitor/manage-settings.png)

3. Use the options for **Monitor** to view the deployment status of the profile on individual devices, the status for each user, and the status for the settings from the instance of the baseline:

   ![See the different monitor options for a security baselines profile](./media/security-baselines-monitor/monitor-status-options.png)

### Resolve conflicts for security baselines

To help resolve a conflict or error for settings in your security baseline profiles or Endpoint security policies, view the [Device configuration report](../fundamentals/reports.md#device-configuration-operational) for a device. This report view helps you identify where your profiles and policies contain settings that drive a status of Conflict or Error.

You can also reach information about settings in conflict or error through two paths from within Microsoft Intune admin center:

- **Endpoint security** > **Security baselines** > *select a baseline type* > **Profiles** > *select a baseline instance* > **Device status**.
- **Devices** > **All devices** > *select a device* > **Device configuration** > *select a Policy* > *select a setting from the list of settings that shows a Conflict or Error*.

#### Drill in to identify and resolve conflicts

1. While viewing the [Device configuration report](../fundamentals/reports.md#device-configuration-operational) for a device, select a policy to drill-in to learn more about the issue that results in a conflict or error status.

   When you drill-in, Intune displays a list of settings for that policy that includes each setting that wasn’t set as *Not configured*, and the status of that setting.

2. To view details about a specific setting, select it to open the **Settings details** pane. In this pane you can view:

   - Setting – The name of the setting.
   - State – The status of the setting on the device.
   - Source Profiles – A list of each conflicting profile that configures the same setting but with a different value.

3. To reconfigure conflicting profiles, select a record from the **Source Profile** list to open *Overview* for that profile. Select the profiles **Properties** and you can then review and edit settings in that profile to remove the conflict.

### View settings from profiles that apply to a device

You can select a profile for a security baseline, and drill-in to view a list of settings from that profile as they apply to an individual device. To drill in:

- **Endpoint Security** > **All devices** > *select a device* > Device configuration > *select a baseline policy instance*.

After you drill in, the admin center displays a list of the settings from that profile and the settings status. Status states include:

- **Succeeded** – The setting on the device matches the value as configured in the profile. This is either the baselines default and recommended value, or a custom value specified by an administrator when the profile was configured.
- **Conflict** – The setting is in conflict with another policy, has an error, or is pending an update.
- **Error** - The settings failed to apply.

### Troubleshoot using per-setting status

You deployed a security baseline, but the deployment status shows an error. The following steps give you some guidance on troubleshooting the error.

1. In Intune, select **Endpoint security** > **Security baselines** > select a baseline > **Profiles**.

2. Select a profile > Under **Monitor** > **Per-setting status**.

3. The table shows all the settings, and the status of each setting. Select the **Error** column or the **Conflict** column to see the setting causing the error.

#### MDM diagnostic information

Now you know the problematic setting. The next step is to find out why this setting is causing an error or conflict.

On Windows 10/11 devices, there's a built-in MDM diagnostic information report. This report includes default values, current values, lists the policy, shows if it's deployed to the device or the user, and more. Use this report to help determine why the setting is causing a conflict or error.

1. On the device, go to **Settings** > **Accounts** > **Access work or school**.

2. Select the account > **Info** > **Advanced Diagnostic Report** > **Create report**.

3. Choose **Export**, and open the generated file.

4. In the report, look for the error or conflict setting in the different sections of the report.

  For example, look in the **Enrolled configuration sources and target resources** section or the **Unmanaged policies** section. You might get an idea of why it's causing an error or conflict.

[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10) provides more information on this built-in report.

> [!TIP]
>
> - Some settings also list the GUID. You can search for this GUID in the local registry (regedit) for any set values.
> - The Event Viewer logs may also include some error information on the problematic setting (**Event viewer** > **Applications and Services Logs** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider** > **Admin**).

## Next steps

- [Learn about security baselines](security-baselines.md)
- [Avoid conflicts](security-baselines.md#avoid-conflicts)
- [Monitor device profiles](../configuration/device-profile-monitor.md) 
- [Common issues and resolutions](../configuration/device-profile-troubleshoot.md).
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
