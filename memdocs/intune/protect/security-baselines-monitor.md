---
# required metadata

title: Check the success or failure of security baselines in Microsoft Intune - Azure | Microsoft Docs
description: Check the error, conflict, and success status when deploying security baselines to users and devices in Microsoft Intune MDM. See how to troubleshoot using client logs, and the report features in Intune.
keywords:
author: brenduns 
ms.author: brenduns
manager: dougeby
ms.date: 09/21/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: laarrizz
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Monitor security baselines and profiles in Microsoft Intune

Intune provides several options to monitor security baselines. You can:

- Monitor a security baseline, and any devices that match (or don't match) the recommended values.
- Monitor the security baselines profile that applies to your users and devices.
- View how the settings from a selected profile are set on a selected device.

You can also view the *Endpoint security configurations* that apply to individual devices, which include security baselines.

For more information about the feature, see [Security baselines in Intune](security-baselines.md).

## Monitor the baseline and your devices

When you monitor a baseline, you get insight into the security state of your devices based on Microsoft's recommendations. To view these insights, sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Endpoint security** > **Security baselines** and select a security baseline type like the *MDM Security Baseline*. Then, from the *Versions* pane, select the profile instance for which you want to view details to open its *Overview* pane. The *Overview* pane displays the **Security baseline posture** chart for that baseline, which includes a high-level status for the baseline instance your viewing. <!-- The following image shows an instance of MDM Security baseline that hasn’t been assigned to any devices yet: -->

<!-- Not available yet:
For each baseline, you’ll see the number of devices assigned the baseline, and the following information about them: 
-->

When you drill-in past the *Security baseline posture* view for a baseline, you can view the following details for the setting status and the device status list views:

- **Succeeded**: Policy is applied.
- **Error**: The policy failed to apply. The message typically displays with an error code that links to an explanation.
- **Conflict**: Two settings are applied to the same device, and Intune can't sort out the conflict. An administrator should review.
- **Pending**: The device hasn't checked in with Intune to receive the policy yet.
- **Not applicable**: The device can't receive the policy. For example, the policy updates a setting specific to the latest version of Windows, but the device runs an older (earlier) version that doesn’t support that setting.

It takes up to 24 hours for data to appear after you first assign a baseline. Later changes take up to six hours to appear.

## Monitor the profile

Monitoring the profile gives insight into the deployment state of your devices, but not the security state based on the baseline recommendations.

1. In Intune, select **Endpoint security** > **Security baselines**, *select a security baseline type like the MDM Security Baseline* > *select an instance of that baseline* > **Properties**.

2. In the *Properties* of the baseline, expand **Settings** to drill-in and view all the settings categories and individual settings in the baseline, including  their configuration for this instance of the baseline.

   ![Screen image showing the settings view](./media/security-baselines-monitor/manage-settings.png)

3. Use the options for **Monitor** to view the deployment status of the profile on individual devices, the status for each user, and the status for the settings from the instance of the baseline:

   ![See the different monitor options for a security baselines profile](./media/security-baselines-monitor/monitor-status-options.png)

## View settings from profiles that apply to a device

You can select a profile for a Security Baseline, and drill-in to view a list of settings from that profile as they apply to an individual device.  To view that list, drill into **Endpoint security** > **Security baselines** > *select the security baseline type* > *select the Profile you want to view* > **Device status**. You can also view the list by going to **Endpoint Security** > **All devices** > *select a device* > **Endpoint security configuration** > *select a baseline version*.

After selecting a device, Microsoft Endpoint Manager admin center displays a list of the settings from that profile that includes the category the setting is from and the configuration state on the device. Configuration states include the following values:

- **Success** – The setting on the device matches the value as configured in the profile. This is either the baselines default and recommended value, or a custom value specified by an administrator when the profile was configured.
- **Conflict** – The setting is in conflict with another policy, has an error, or is pending an update.
- **Not applicable** – The setting is not applied by the profile.

> [!NOTE]
> The status values for settings will update in a future release to provide more granular details.

## View Endpoint security configurations per device

View details about the security configurations that apply to an individual device, which can help you isolate settings that  are misconfigured.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to  **Devices** > **All devices** and select the device you want to view.

3. In the *Monitor* category, select **Endpoint security configuration** to view the list of security configurations that apply to that device.

4. You can select an Endpoint security configuration to drill in and view additional details about the evaluation of that security configuration on the device.

## Troubleshoot using per-setting status

You deployed a security baseline, but the deployment status shows an error. The following steps give you some guidance on troubleshooting the error.

1. In Intune, select **Security Baselines** > select a baseline > **Profiles**.

2. Select a profile > Under **Monitor** > **Per-setting status**.

3. The table shows all the settings, and the status of each setting. Select the **Error** column or the **Conflict** column to see the setting causing the error.

### MDM diagnostic information

Now you know the problematic setting. The next step is to find out why this setting is causing an error or conflict.

On Windows 10 devices, there's a built-in MDM diagnostic information report. This report includes default values, current values, lists the policy, shows if it's deployed to the device or the user, and more. Use this report to help determine why the setting is causing a conflict or error.

1. On the device, go to **Settings** > **Accounts** > **Access work or school**.

2. Select the account > **Info** > **Advanced Diagnostic Report** > **Create report**.

3. Choose **Export**, and open the generated file.

4. In the report, look for the error or conflict setting in the different sections of the report.

  For example, look in the **Enrolled configuration sources and target resources** section or the **Unmanaged policies** section. You may get an idea of why it's causing an error or conflict.

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
- [Troubleshoot policies and profiles in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)