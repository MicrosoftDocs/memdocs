---
# required metadata

title: Add preference file settings to macOS devices in Microsoft Intune
titleSuffix:
description: Add an xml or plist file that includes key information about your app. Use a preference file device configuration profile to change key information in the property list file, and assign it to your macOS devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/29/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: beflamm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add a property list file to macOS devices using Microsoft Intune

Using Microsoft Intune, you can add a property list file (.plist) for macOS devices, or apps on macOS devices.

This feature applies to:

- macOS 10.7 and newer

Property list files include information about macOS applications. For more information, see [About Information Property List Files](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (Apple's website) and [Custom payload settings](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1).

This article describes the different property list file settings you can add to macOS devices. As part of your mobile device management (MDM) solution, use these settings to add the app bundle ID (`com.company.application`), and add the app's `.plist` file.

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your macOS devices.

## What you need to know

- These settings aren't validated. Be sure to test your changes before assigning the profile to your devices.
- If you're not sure how to enter an app key, change the setting within the app. Then, review the app's preference file using [Xcode](https://developer.apple.com/xcode/) to see how the setting is configured. Apple recommends removing non-manageable settings using Xcode before importing the file.
- Only some apps work with managed preferences, and might not allow you to manage all settings.
- Be sure you upload property list files that target device channel settings, not user channel settings. Property list files target the entire device.
- If you're configuring the Microsoft Edge version 77 and newer app, then use the [Settings catalog](settings-catalog.md). For a list of the settings you can configure, see [Microsoft Edge - Policies](/DeployEdge/microsoft-edge-policies) (opens another Microsoft website).

  Be sure macOS is listed as a supported platform. If some settings aren't available in the settings catalog, then it's recommended to continue using the preference file.

## Create the profile

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]
>
> [Tasks you can complete using the Settings Catalog in Intune](settings-catalog-common-features.md) is also a good resource.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **macOS**
    - **Profile**: Select **Templates** > **Preference file**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **macOS: Add preference file that configures Microsoft Defender for Endpoint on devices**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, configure your settings:

    - **Preference domain name**: Enter the bundle ID, such as `com.company.application`. For example, enter `com.Contoso.applicationName`, `com.Microsoft.Edge`, or `com.microsoft.wdav`.

      Property list files are typically used for web browsers (Microsoft Edge), [Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac), and custom apps. When you create a preference domain, a bundle ID is also created.

      > [!TIP]
      > For Microsoft Edge version 77 and newer, you can use the settings catalog. You don't have to use a preference file. For more information, see [Settings catalog](settings-catalog.md).

    - **Property list file**: Select the property list file associated with your app. Be sure it's a `.plist` or `.xml` file. For example, upload a `YourApp-Manifest.plist` or `YourApp-Manifest.xml` file.

      The key information in the property list file is shown. If you need to change the key information, open the list file in another editor, and then reupload the file in Intune.

    Be sure your file is formatted correctly. The file should only have key value pairs, and shouldn't be wrapped in `<dict>`, `<plist>`, or `<xml>` tags. For example, your property list file should be similar to the following file:

    ```xml
    <key>SomeKey</key>
    <string>someString</string>
    <key>AnotherKey</key>
    <false/>
    ...
    ```

    To see some property list file examples, go to [Set preferences for Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/mac-preferences).

8. Select **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

For more information on preference files for Microsoft Edge, see [Configure Microsoft Edge policy settings on macOS](/deployedge/configure-microsoft-edge-on-mac).
