---
# required metadata

title: See device configuration policies with Microsoft Intune
description: See and manage the device configuration policy details in Microsoft Intune. Look at a graphical chart of the number of devices assigned to a policy, and see which devices have policies assigned or deployed. Can also troubleshoot policies that have conflict settings. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/22/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.assetid: 9deaed87-fb4b-4689-ba88-067bc61686d7

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Monitor device configuration policies in Microsoft Intune

Intune includes some features to help monitor and manage your device configuration policies. For example, you can check the status of a policy, go to the devices are assigned to the policy, and update the properties of an existing policy.

This article shows you how to view existing device configuration policies for assignment status, making changes, and how to troubleshoot any conflicts.

## View existing policies

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration** > **Policies** tab.

All of your policies are shown. You also see the platform, the type of policy, and if the policy is assigned.

> [!NOTE]
> For more in-depth reporting information about device configuration policies, go to [Intune reports](../fundamentals/reports.md).

## View details on a policy

After you create your device configuration policy, Intune provides reporting data. These reports show the status of a policy, such as it being successfully assigned to devices, or if the policy shows a conflict.

1. In **Devices** > **Configuration** > **Policies** tab, select an existing policy.

2. The **Device and user check-in status** shows the number of all users or devices that checked-in with the policy. If one device has multiple users, this report shows the status for each user. When the user or device checks in with Intune, they receive the settings in your policy.

    The following statuses are shown:

    - **Succeeded**: The policy is applied successfully.
    - **Error**: The policy failed to apply. The message typically displays with an error code that links to an explanation.
    - **Conflict**: Two settings are applied to the same device, and Intune can't sort out the conflict. An administrator should review.
    - **Pending**: The device hasn't checked in with Intune to receive the policy yet.
    - **Not applicable**: The device can't receive the policy. For example, the policy updates a setting specific to iOS 11.1, but the device is using iOS 10.

3. **Device assignment status** shows information for the user that last checked-in. Select **Generate report** to see the latest policy assignment states for the devices that received the policy. You can also filter the assignment status to see only errors, conflicts, and more.

    It's normal for the numbers in the **Device and user check-in status** and **Device assignment status** reports to be different.

4. **Per setting status** shows the individual settings in the policy, and their status.

5. Back in **Device and user check-in status**, select **View report**:

    :::image type="content" source="./media/device-profile-monitor/device-user-check-in-status-view-report.png" alt-text="Screenshot that shows to select view report on a device configuration policy to get the device and user check-in status in Microsoft Intune and Intune admin center.":::

    **View report** shows more information on the devices assigned to that specific device configuration policy, including:

    - The devices that received the policy
    - The user names with devices that received the policy
    - The check-in status and the last time the user/device checked in with the policy

    You can also select a specific device to get more details and use the filter column to see the assignment filter options.

6. Back in **Device and user check-in status**, the following property information for the specific policy is available for you to view and edit:

    - **Basics**: See the policy name and description.
    - **Assignments**: See the users and groups that receive policy, and see any existing [filters](../fundamentals/filters.md) in the policy.
    - **Scope tags**: See any existing [scope tags](../fundamentals/scope-tags.md) used in the policy.
    - **Configuration settings**: See the settings you configured in the policy.
    - **Applicability Rules**: On your Windows devices, go to the [applicability rules](device-profile-create.md#applicability-rules) used in the policy.

## View details on all device configuration policies

1. Go to **Devices** > **Configuration** > **Monitor** tab:

    :::image type="content" source="./media/device-profile-monitor/device-configuration-monitor-tab.png" alt-text="Screenshot that shows to select the monitor tab in device configuration profiles in Microsoft Intune and Intune admin center.":::

2. In this area, you have access to the **Configuration policy assignment failures** report. This report helps troubleshoot errors and conflicts for configuration policies that are assigned.

    This area also provides quick access to the following reports:

    - Devices with restricted apps
    - Device encryption status
    - Certificates

> [!TIP]
> In **Devices**, select **Monitor**. This area lists all reports you can use, including reports for device configuration, compliance, enrollment, and software updates. For more information on all the Intune reports, go to [Intune reports](../fundamentals/reports.md).

## View conflicts

In **Devices** > **All devices**, you can see any settings that are causing a conflict. When there's a conflict, you also see all the configuration policies that contain this setting.

Administrators can use this feature to help troubleshoot, and fix any discrepancies with the policies.

1. In Intune, select **Devices** > **All Devices** > select an existing device in the list. An end user can get the device name from their Company Portal app.
2. Select **Device configuration**. All configuration policies that apply to the device are listed.
3. Select the policy. It shows you all the settings in that policy that apply to the device. If a device has a **Conflict** state, select that row. In the new window, you see all the policies, and the profile names that have the setting causing the conflict.

Now that you know the conflicting setting, and the policies that include that setting, it should be easier to resolve the conflict.

## Device Firmware Configuration Interface (DFCI) profile reporting

DFCI policies are reported on a per-setting basis, just like other device configuration policies. Depending on the manufacturer's support of DFCI, some settings might not apply.

With your DFCI profile settings, you might see the following states:

- **Compliant**: This state shows when a setting value in the profile matches the setting on the device. This state can happen in the following scenarios:

  - The DFCI profile successful configured the setting in the profile.
  - The device doesn't have the hardware feature controlled by the setting, and the profile setting is **Disabled**.
  - UEFI doesn't allow DFCI to disable the feature, and the profile setting is **Enabled**.
  - The device lacks the hardware to disable the feature, and the profile setting is **Enabled**.

- **Not Applicable**: This state shows when a setting value in the profile is **Enabled** or **Allowed**, and the matching setting on the device isn't found. This state can happen if the device hardware doesn't have the feature.

- **Noncompliant**: This state shows when a setting value in the profile doesn't match the setting on the device. This state can happen in the following scenarios:

  - UEFI doesn't allow DFCI to disable a setting, and the profile setting is **Disabled**.
  - The device lacks the hardware to disable the feature, and the profile setting is **Disabled**.
  - The device doesn't have the latest DFCI firmware version.
  - DFCI was disabled before being enrolled in Intune using a local "opt-out" control in the UEFI menu.
  - The device was enrolled to Intune outside of Autopilot enrollment.
  - The device isn't registered to Windows Autopilot by a Microsoft CSP, or registered directly by the OEM.

## Related content

- [Common questions, issues, and resolutions with device configuration policies](device-profile-troubleshoot.md)
- [Troubleshoot device configuration policies in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
