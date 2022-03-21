---
# required metadata

title: See device profiles with Microsoft Intune
description: See and manage the device configuration profile details in Microsoft Intune. Look at a graphical chart of the number of devices assigned to a profile, and see which devices have profiles assigned or deployed. Can also troubleshoot profiles that have conflict settings. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/21/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid: 9deaed87-fb4b-4689-ba88-067bc61686d7

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Monitor device configuration profiles in Microsoft Intune

Intune includes some features to help monitor and manage your device configuration profiles. For example, you can check the status of a profile, see which devices are assigned, and update the properties of a profile.

## View existing profiles

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles**.

All of your profiles are shown. You also see the platform, the type of profile, and if the profile is assigned.

> [!NOTE]
> For additional reporting information about device configuration profiles, see [Intune reports](../fundamentals/reports.md).

## View details on a profile

After you create your device profile, Intune provides graphical charts. These charts display the status of a profile, such as it being successfully assigned to devices, or if the profile shows a conflict.

1. In **Devices** > **Configuration profiles**, select an existing profile. For example, select a macOS profile.
2. Select the **Overview** tab. In this view, the **Profile assignment status** includes the following statuses:

    - **Succeeded**: Policy is applied successfully.
    - **Error**: The policy failed to apply. The message typically displays with an error code that links to an explanation.
    - **Conflict**: Two settings are applied to the same device, and Intune can't sort out the conflict. An administrator should review.
    - **Pending**: The device hasn't checked in with Intune to receive the policy yet.
    - **Not applicable**: The device can't receive the policy. For example, the policy updates a setting specific to iOS 11.1, but the device is using iOS 10.

3. The top graphical chart shows the number of devices assigned to the device profile. For example, if the configuration device profile applies to macOS devices, the chart lists the count of the macOS devices.

    When you monitor a Windows profile, the count in the **Profile assignment status** is per device per user. So, if two users sign in to the same device, then that device is counted twice.

4. Select the top graphical chart. Or, select **Device status**. **Device status** opens.

    The devices assigned to the profile are listed, and it shows the deployment status. Also note that it only lists the devices with the specific platform (for example, macOS).

    Close the **Device status** details.

5. Select the circle in the bottom graphical chart. Or, select **User status**. **User status** opens.

    The users assigned to the profile are listed, and it shows the deployment status. Also note that it only lists the users with the specific platform (for example, macOS).

    Close the **User status** details.

6. Back in the **Profiles** list, select a specific profile.

    - **Properties**: Change the policy name, or update any existing configuration settings. You can also update:

      - **Scope tags**: See any existing [scope tags](../fundamentals/scope-tags.md) used in the policy. Select **Edit** to add or remove a scope tag.
      - **Assignments**: See the users and groups that receive policy, and see any existing [filters](../fundamentals/filters.md) in the policy. Select **Edit** to update the policy assignment, and add or remove a filter.
      - **Applicability Rules**: On your Windows devices, see the [applicability rules](device-profile-create.md#applicability-rules) used in the policy. Select **Edit** to add or remove an applicability rule.

    - **Device status**: The devices assigned to the profile are listed, and it shows if the profile is successfully deployed. You can select a specific device to get even more details, including the installed apps.
    - **User status**: Lists the user names with devices affected by this profile, and if the profile successfully deployed. You can select a specific user to get even more details.
    - **Per-setting status**: Filters the output by showing the individual settings within the profile, and shows if the setting is successfully applied.

> [!TIP]
> [Intune reports](../fundamentals/reports.md) is a great resource, and describes all the reporting features you can use.

## View conflicts

In **Devices** > **All devices**, you can see any settings that are causing a conflict. When there's a conflict, you also see all the configuration profiles that contain this setting. Administrators can use this feature to help troubleshoot, and fix any discrepancies with the profiles.

1. In Intune, select **Devices** > **All Devices** > select an existing device in the list. An end user can get the device name from their Company Portal app.
2. Select **Device configuration**. All configuration policies that apply to the device are listed.
3. Select the policy. It shows you all the settings in that policy that apply to the device. If a device has a **Conflict** state, select that row. In the new window, you see all the profiles, and the profile names that have the setting causing the conflict.

Now that you know the conflicting setting, and the policies that include that setting, it should be easier to resolve the conflict.

> [!TIP]
> In **Devices** > **Monitor**, a list of all policies are shown. The **Assignment failures (preview)** report helps troubleshoot errors and conflicts for configuration profiles that are assigned. For more information on the available reporting data, see [Intune reports](../fundamentals/reports.md).

## Device Firmware Configuration Interface profile reporting

DFCI profiles are reported on a per-setting basis, just like other device configuration profiles. Depending on the manufacturer's support of DFCI, some settings may not apply.

With your DFCI profile settings, you may see the following states:

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
  - The device wasn't registered to Autopilot by a Microsoft CSP, or registered directly by the OEM.

## Next steps

[Common questions, issues, and resolutions with device profiles](device-profile-troubleshoot.md)  
[Troubleshoot policies and profiles and in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
