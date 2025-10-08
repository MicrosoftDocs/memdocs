---
title: See device configuration policies with Microsoft Intune
description: See and manage the device configuration policy details in Microsoft Intune. Look at a graphical chart of the number of devices assigned to a policy, and see which devices have policies assigned or deployed. Can also troubleshoot policies that have conflict settings.
author: MandiOhlinger
ms.author: mandia
ms.date: 09/17/2025
ms.update-cycle: 180-days
ms.topic: how-to
ms.reviewer: laarrizz
ms.collection:
- M365-identity-device-management
- msec-ai-copilot
---

# View and monitor device configuration policies in Microsoft Intune

Intune includes some features to help monitor and manage your device configuration policies. For example, you can check the status of a policy, view the devices assigned to the policy, and update the properties of an existing policy. These capabilities extend to the profiles for your [endpoint security policies](../protect/endpoint-security-manage-devices.md#review-your-profiles-for-endpoint-security-policies) for macOS and Windows devices.

You can also use [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md) to get more information about your policies and the settings configured in your policies.

This article shows you how to check the assignment status of existing device configuration policies, make changes, troubleshoot conflicts, and how to use Copilot for some of these features.

This feature applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

## Prerequisites

At a minimum, sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with one of the following roles, depending on your task:

- **Read Only Operator**: This role can view existing policies and view reports. It can't make any changes.
- **Policy and Profile manager**: This role can view existing policies and reports, and can make any changes.

For information on the built-in roles in Intune, and what they can do, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

## View and filter existing policies

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Policies** tab. All of your policies are shown. You also see the platform, the type of policy, and more properties.

    :::image type="content" source="./media/device-profile-monitor/configuration-policy-list.png" alt-text="Screenshot that shows all the device configuration profiles, their profile type, and the last modified date in Microsoft Intune and Intune admin center." lightbox="./media/device-profile-monitor/configuration-policy-list.png":::

3. If you have many policies, you can filter by the policy type, like the settings catalog or software updates. Select **Add filters** > **Policy type** > **Apply**:

    :::image type="content" source="./media/device-profile-monitor/filter-policies.png" alt-text="Screenshot that shows the Add filter option to filter existing policies in Microsoft Intune and Intune admin center.":::

> [!NOTE]
> For more in-depth reporting information about device configuration policies, go to [Intune reports](../fundamentals/reports.md).

## View details on a policy

After you create your device configuration policy, Intune provides reporting data. These reports show the status of a policy, like it being successfully assigned to devices, or if the policy shows a conflict.

# [By policy](#tab/policy)

1. In **Devices** > **Manage devices** > **Configuration** > **Policies** tab, select an existing policy.

2. **Device and user check-in status** shows the number of all users or devices that checked-in with the policy. If one device has multiple users, this report shows the status for each user. When the user or device checks in with Intune, they receive the settings in your policy.

    The following statuses are shown:

    - **Succeeded**: The policy is applied successfully.
    - **Error**: The policy failed to apply. The message typically displays with an error code that links to an explanation.
    - **Conflict**: Two settings are applied to the same device, and Intune can't sort out the conflict. An administrator should review.
    - **Pending**: The device hasn't checked in with Intune to receive the policy yet.
    - **Not applicable**: The device can't receive the policy. For example, the policy updates a setting specific to iOS 11.1, but the device is using iOS 10.

3. Select **Device assignment status**:

    :::image type="content" source="./media/device-profile-monitor/device-assignment-status.png" alt-text="Screenshot that shows the device assignment status report in Microsoft Intune and Intune admin center.":::

    This report shows information about the user that last checked-in. Select **Generate report** to see the latest policy assignment states for the devices that received the policy. You can also filter the assignment status to see only errors, conflicts, and more.

    It's normal for the numbers in the **Device and user check-in status** and **Device assignment status** reports to be different.

4. Go back to **Device and user check-in status** and select **Per setting status**:

    :::image type="content" source="./media/device-profile-monitor/per-setting-status.png" alt-text="Screenshot that shows the per setting status report in Microsoft Intune and Intune admin center.":::

    This report shows the individual settings in the policy, and their status.

5. Go back to **Device and user check-in status** and select **View report**:

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

# [Copilot](#tab/copilot-devices)

1. Go to **Devices** > **Manage devices** > **Configuration** > **Policies** tab > select an existing policy.

2. Select **Summarize with Copilot**:

    :::image type="content" source="./media/device-profile-monitor/copilot-summarize-policy.png" alt-text="Screenshot that shows you can select Summarize with Copilot on a device configuration policy in Microsoft Intune and Intune admin center.":::

    The summary describes what the policy does, the users and groups assigned to the policy, and the settings in the policy. This feature can help you understand the effect of a policy and its settings on your users and devices.

    For more information on the different ways you can use Copilot in Intune, go to [Copilot in Intune overview](../copilot/copilot-intune-overview.md).

3. Go to **Devices** > **All devices** > select an existing device.

4. Select **Summarize with Copilot**. Copilot shows device-specific information, like the device properties, group membership, and more.

    For information on using Copilot to troubleshoot devices, go to [Use Copilot in Intune to troubleshoot devices](../copilot/copilot-devices.md).

---

## View details on all device configuration policies

1. Go to **Devices** > **Manage devices** > **Configuration** > **Monitor** tab:

    :::image type="content" source="./media/device-profile-monitor/device-configuration-monitor-tab.png" alt-text="Screenshot that shows to select the monitor tab in device configuration profiles in Microsoft Intune and Intune admin center.":::

2. In this area, you have access to the **Configuration policy assignment failures** report. This report helps troubleshoot errors and conflicts for configuration policies that are assigned.

    This area also provides quick access to the following reports:

    - Devices with restricted apps
    - Device encryption status
    - Certificates

> [!TIP]
> In **Devices**, select **Monitor**. This area lists all reports you can use, including reports for device configuration, compliance, enrollment, and software updates. For more information on all the Intune reports, go to [Intune reports](../fundamentals/reports.md).

## View conflicts

To help with conflicts, there are features in Intune to help you troubleshoot any discrepancies with the policies. When there's a conflict, you also see all the configuration policies that contain this setting.

# [By device](#tab/devices)

In **Devices** > **All devices**, you can see any settings that are causing a conflict.

1. In Intune, select **Devices** > **All Devices** > select an existing device in the list. An end user can get the device name from their Company Portal app.
2. Select **Device configuration**. All configuration policies that apply to the device are listed.
3. Select a policy. It shows you all the settings in that policy that apply to the device.

    If a device has a **Conflict** state, select that row. In the new window, you see all the policies, and the profile names that have the setting causing the conflict.

Now that you know the conflicting setting, and the policies that include that setting, it should be easier to resolve the conflict.

# [Copilot](#tab/copilot-setting)

You can use Copilot to help troubleshoot conflicts at the setting level.

1. Select **Devices** > **Manage devices** > **Configuration** > select an existing policy in the list.

2. Scroll to the **Configuration settings** area and expand a setting category:

    :::image type="content" source="./media/device-profile-monitor/copilot-configuration-settings-expand-category.png" alt-text="Screenshot that shows how to expand a category to see the Copilot tooltip in Microsoft Intune and Intune admin center.":::

3. For each setting, there's a Copilot tooltip:

    :::image type="content" source="./media/device-profile-monitor/copilot-tooltip.png" alt-text="Screenshot that shows the Copilot tooltip for a setting in Microsoft Intune and Intune admin center.":::

    Select the tooltip to get more information about setting. In Copilot Chat, enter `conflicts`. In suggestions, there are some sample prompts you can select, like **Show me policies that contain conflicting settings**.

---

## Device Firmware Configuration Interface (DFCI) profile reporting

DFCI policies are reported on a per-setting basis, just like other device configuration policies. Depending on the manufacturer's support of DFCI, some settings might not apply.

With your DFCI profile settings, you might see the following states:

- **Compliant**: This state shows when a setting value in the profile matches the setting on the device. This state can happen in the following scenarios:

  - The DFCI profile successful configured the setting in the profile.
  - The device doesn't have the hardware feature controlled by the setting, and the profile setting is **Disabled**.
  - Unified Extensible Firmware Interface (UEFI) doesn't allow DFCI to disable the feature, and the profile setting is **Enabled**.
  - The device lacks the hardware to disable the feature, and the profile setting is **Enabled**.

- **Not Applicable**: This state shows when a setting value in the profile is **Enabled** or **Allowed**, and the matching setting on the device isn't found. This state can happen if the device hardware doesn't have the feature.

- **Noncompliant**: This state shows when a setting value in the profile doesn't match the setting on the device. This state can happen in the following scenarios:

  - UEFI doesn't allow DFCI to disable a setting, and the profile setting is **Disabled**.
  - The device lacks the hardware to disable the feature, and the profile setting is **Disabled**.
  - The device doesn't have the latest DFCI firmware version.
  - DFCI was disabled before being enrolled in Intune using a local "opt-out" control in the UEFI menu.
  - The device was enrolled to Intune outside of Windows Autopilot enrollment.
  - The device isn't registered to Windows Autopilot by a Microsoft CSP, or registered directly by the OEM.

## Related content

- [Common questions, issues, and resolutions with device configuration policies](device-profile-troubleshoot.md)
- [Troubleshoot device configuration policies in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
