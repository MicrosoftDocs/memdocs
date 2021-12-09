---
# required metadata

title: Add custom settings to Android Enterprise devices in Microsoft Intune
description: Add or create a custom profile for Android Enterprise devices to create  in Microsoft Intune
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:
ms.assetid: 4724d6e5-05e5-496c-9af3-b74f083141f8

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use custom settings for Android Enterprise devices in Microsoft Intune

Using Microsoft Intune, you can add or create custom settings for your Android Enterprise personally owned devices with a work profile using a "custom profile". Custom profiles are a feature in Intune. They are designed to add device settings and features that aren't built in to Intune.

This feature applies to:

- Android Enterprise personally owned devices with a work profile (BYOD)

Android Enterprise custom profiles use Open Mobile Alliance Uniform Resource Identifier (OMA-URI) settings to control features on Android Enterprise devices. These settings are typically used by mobile device manufacturers to control these features.

Intune supports the following limited number of Android Enterprise custom profiles:

- ./Vendor/MSFT/WiFi/Profile/SSID/Settings: [Create a Wi-Fi profile with a pre-shared key](wi-fi-profile-shared-key.md) has some examples.
- ./Vendor/MSFT/VPN/Profile/Name/PackageList: [Create a per-app VPN profile](android-pulse-secure-per-app-vpn.md) has some examples.
- ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste: See the [example](#example) in this article. This setting is also available in the user interface. For more information, see [Android Enterprise device settings to allow or restrict features](device-restrictions-android-for-work.md).

If you need additional settings, see [OEMConfig for Android Enterprise](android-oem-configuration-overview.md).

This article shows you how to create a custom profile for Android Enterprise devices. It also provides an example of a custom profile that blocks copy-and-paste.

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following settings:

    - **Platform**: Select **Android Enterprise**.
    - **Profile**: Select **Personally-owned work profile** > **Custom**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Android Enterprise custom profile**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings** > **OMA-URI Settings**, select **Add**. Enter the following settings:

    - **Name**: Enter a unique name for the OMA-URI setting so you can easily find it.
    - **Description**: Enter a description that gives an overview of the setting, and any other important details.
    - **OMA-URI**: Enter the OMA-URI you want to use as a setting.
    - **Data type**: Select the data type you'll use for this OMA-URI setting. Your options:

      - String
      - String (XML file)
      - Date and time
      - Integer
      - Floating point
      - Boolean
      - Base64 (file)

    - **Value**: Enter the data value you want to associate with the OMA-URI you entered. The value depends on the data type you selected. For example, if you select **Date and time**, select the value from a date picker.

    After you add some settings, you can select **Export**. **Export** creates a list of all the values you added in a comma-separated values (.csv) file.

8. Select **Save** to save your changes. Continue to add more settings as needed.

    Select **Next**.

9. In **Scope tags** (optional) > **Select scope tags**, choose your scope tags to assign to the profile. For more information, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, when you're done, choose **Create**. The profile is created, and shown in the list.

    You can also [monitor its status](device-profile-monitor.md).

## Example

In this example, you create a custom profile that restricts copy and paste actions between work and personal apps on Android Enterprise devices.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following settings:

    - **Platform**: Select **Android Enterprise**.
    - **Profile**: Select **Personally-owned work profile** > **Custom**.

4. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, enter **AE block copy paste custom profile**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

5. Select **Next**.
6. In **Configuration settings** > **OMA-URI Settings**, select **Add**. Enter the following settings:

    - **Name**: Enter something like `Block copy and paste`.
    - **Description**: Enter something like `Blocks copy/paste between work and personal apps`.
    - **OMA-URI**: Enter `./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste`.
    - **Data type**: Select **Boolean** so the value for this OMA-URI is **True** or **False**.
    - **Value**: Select **True**.

    Your settings look similar to the following image:

    :::image type="content" source="./media/custom-settings-android-for-work/custom-oma-uri-android-enterprise.png" alt-text="Block copy and paste for Android Enterprise personally owned devices with a work profile in Microsoft Intune.":::

7. Select **Save** to save your changes. Continue to add more settings as needed. After you add some settings, you can select **Export**. **Export** creates a list of all the values you added in a comma-separated values (.csv) file.

    After you enter the settings, your environment looks similar to the following image:

    :::image type="content" source="./media/custom-settings-android-for-work/custom-policy-afw-copy-paste.png" alt-text="You can add more OMA-URI values, and export the values for Android Enterprise personally owned devices with a work profile in Microsoft Intune.":::

8. Select **Next**.
9. In **Scope tags** (optional) > **Select scope tags**, choose your scope tags to assign to the profile. For more information, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, when you're done, choose **Create**. The profile is created and is shown in the list.

    When you assign this profile to Android Enterprise devices you manage, copy and paste is blocked between apps in the work and personal profiles.

    You can also [monitor its status](device-profile-monitor.md).

## Next steps

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
- Create a [custom profile on Android device administrator devices](custom-settings-android.md).
