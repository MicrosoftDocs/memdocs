---
# required metadata

title: Add custom settings to Android DA devices in Microsoft Intune
description: Add or create a custom profile for Android devices in Microsoft Intune. Create a WiFi profile with a preshared key, create a per-app VPN profile, or allow/block apps for Samsung Knox Standard devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/16/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Use custom settings for Android devices in Microsoft Intune

Using Microsoft Intune, you can add or create custom settings for your Android devices using a "custom profile". Custom profiles are a feature in Intune. They're designed to add device settings and features that aren't built in to Intune.

This feature applies to:

- Android device administrator (DA)

Android custom profiles use Open Mobile Alliance Uniform Resource Identifier (OMA-URI) settings to configure different features on Android devices. These settings are typically used by mobile device manufacturers to control these features.

Using a custom profile, you can configure and assign the following Android settings. The following settings aren't built in to Intune:

- [Create a Wi-Fi profile with a pre-shared key](/intune/wi-fi-profile-shared-key)
- [Create a per-app VPN profile](/intune/android-pulse-secure-per-app-vpn)
- [Allow and block apps for Samsung Knox Standard devices](/intune/samsung-knox-apps-allow-block)
- [Configure web protection in Microsoft Defender for Endpoint for Android](../protect/advanced-threat-protection-manage-android.md)

> [!IMPORTANT]
> Only the settings listed can be configured by in a custom profile. Android devices don't expose a complete list of OMA-URI settings you can configure. If you'd like to see more settings, then vote for more settings at the [Feedback for Intune site](https://feedbackportal.microsoft.com/feedback/forum/ef1d6d38-fd1b-ec11-b6e7-0022481f8472).<!-- 10948264 -->

This article shows you how to create a custom profile for Android devices.

## Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following settings:

    - **Platform**: Select **Android device administrator**.
    - **Profile**: Select **Custom**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Android DA custom profile**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings** > **OMA-URI Settings**, select **Add**. Enter the following settings:

    - **Name**: Enter a unique name for the OMA-URI setting so you can easily find it.
    - **Description**: Enter a description that gives an overview of the setting, and any other important details.
    - **OMA-URI**: Enter the OMA-URI you want to use as a setting.
    - **Data type**: Select the data type for this OMA-URI setting. Your options:

      - String
      - String (XML file)
      - Date and time
      - Integer
      - Floating point
      - Boolean
      - Base64 (file)

    - **Value**: Enter the data value you want to associate with the OMA-URI you entered. The value depends on the data type you selected. For example, if you select **Date and time**, select the value from a date picker.

8. Select **Save** to save your changes. Continue to add more settings as needed. After you add some settings, you can select **Export**. **Export** creates a list of all the values you added in a comma-separated values (.csv) file.

    Select **Next**.

9. In **Scope tags** (optional) > **Select scope tags**, choose your scope tags to assign to the profile. For more information, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, when you're done, choose **Create**. The profile is created, and shown in the list.

    You can also [monitor its status](device-profile-monitor.md).

## Next steps

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
- Create a [custom profile on Android Enterprise devices](custom-settings-android-for-work.md).
