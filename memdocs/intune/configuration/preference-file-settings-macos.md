---
# required metadata

title: Add preference file settings to macOS devices in Microsoft Intune
titleSuffix:
description: Add an xml or plist file that includes key information about your app. Use a preference file device configuration profile to change key information in the property list file, and assign it to your macOS devices in Microsoft Intune.
keywords: preference file, property list file, plist, macOS, microsoft intune, endpoint management
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/22/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:
ms.reviewer: beflamm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Add a property list file to macOS devices using Microsoft Intune

Using Microsoft Intune, you can add a property list file (`.plist`) for macOS devices, or apps on macOS devices.

This feature applies to:

- macOS 10.7 and newer

Property list files, also called preference files, include information about your macOS apps. You define app properties or settings that you want to preconfigure. When the file is ready, you can use Intune to deploy the file to your devices and configure the app settings in your file.

Property list files are typically used for web browsers, like Google Chrome, [Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint-mac), and custom apps.

> ![WARNING]
> There are sample `.plist` files at [ManagedPreferencesApplications examples on GitHub](https://github.com/ProfileCreator/ProfileManifests/tree/master/Manifests/ManagedPreferencesApplications). This GitHub repository is not owned, not maintained, and not created by Microsoft. Use the information at your own risk.

> [!TIP]
> For Microsoft Edge version 77 and newer, you can use the settings catalog. You don't have to use a preference file. For more information, go to [Settings catalog](settings-catalog.md).

For more information on `plist` files, go to [About Information Property List Files](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (Apple's website) and [Custom payload settings](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1) (Apple's website).

This article describes the different property list file settings you can add to macOS devices. As part of your mobile device management (MDM) solution, use these settings to add the app bundle ID (`com.company.application`), and add the app's `.plist` file.

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your macOS devices.

## Prerequisites

- [!INCLUDE [minimum-rbac-role-policy-profile-manager](../includes/minimum-rbac-role-policy-profile-manager.md)]
- The device must be enrolled and MDM managed by Intune. For information on the enrollment options for macOS devices, go to [macOS enrollment guide for Microsoft Intune](../fundamentals/deployment-guide-enrollment-macos.md).

## What you need to know

- Test your changes before assigning the profile to your devices. Intune doesn't validate the settings in the property list file.
- Review the app's preference file using [Xcode](https://developer.apple.com/xcode/) to see how the setting is configured. If you're not sure how to enter an app key, change the setting within the app. Then, review the app's preference file using [Xcode](https://developer.apple.com/xcode/).

  Apple recommends removing nonmanageable settings using Xcode before importing the file.

- Only some apps work with managed preferences, and might not allow you to manage all settings.
- Be sure you upload property list files that target device channel settings, not user channel settings. Property list files target the entire device.
- Use the [Settings catalog](settings-catalog.md) to configure Microsoft Edge version 77 and newer. For a list of the settings you can configure, go to [Microsoft Edge - Policies](/DeployEdge/microsoft-edge-policies) (opens another Microsoft website).

  Be sure macOS is listed as a supported platform. If some settings aren't available in the settings catalog, then use the preference file.

## Create the profile

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]
>
> [Tasks you can complete using the Settings Catalog in Intune](settings-catalog-common-features.md) is also a good resource.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **macOS**
    - **Profile type**: Select **Templates** > **Preference file**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **macOS-plist file for Microsoft Defender for Endpoint**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, configure your settings:

    - **Preference domain name**: Enter the bundle ID for your app, like `com.company.application`. For example, enter `com.Contoso.applicationName`, `com.Microsoft.Edge`, or `com.microsoft.wdav`.

      When you create a preference domain, a bundle ID is also created.

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
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, go to [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Resources

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

For more information on preference files for Microsoft Edge, go to [Configure Microsoft Edge policy settings on macOS](/deployedge/configure-microsoft-edge-on-mac).
