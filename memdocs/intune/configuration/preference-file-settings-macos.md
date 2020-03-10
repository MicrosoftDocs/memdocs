---
# required metadata

title: Add preference file settings to macOS devices in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Add an xml or plist file that includes key information about your app. Use a preference file device configuration profile to change key information in the property list file, and assign it to your macOS devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add a property list file to macOS devices using Microsoft Intune

Using Microsoft Intune, you can add a property list file (.plist) for macOS devices, or apps on macOS devices.

This feature applies to:

- macOS devices running 10.7 and newer

Property list files typically include information about macOS applications. For more information, see [About Information Property List Files](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (Apple's website) and [Custom payload settings](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1).

This article lists and describes the different property list file settings you can add to macOS devices. As part of your mobile device management (MDM) solution, use these settings to add the app bundle ID (`com.company.application`), and add its .plist file.

These settings are added to a device configuration profile in Intune, and then assigned or deployed to your macOS devices.

## Before you begin

[Create the profile](device-profile-create.md).

## What you need to know

- These settings aren't validated. Be sure to test your changes before assigning the profile to your devices.
- If you’re not sure how to enter an app key, change the setting within the app. Then, review the app's preference file using [Xcode](https://developer.apple.com/xcode/) to see how the setting is configured. Apple recommends removing non-manageable settings using Xcode before importing the file.
- Only some apps work with managed preferences, and might not allow you to manage all settings.
- Be sure you upload property list files that target device channel settings, not user channel settings. Property list files target the entire device.

## Preference file

- **Preference domain name**: Property list files are typically used for web browsers (Microsoft Edge), [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac), and custom apps. When you create a preference domain, a bundle ID is also created. Enter the bundle ID, such as `com.company.application`. For example, enter `com.Contoso.applicationName`, `com.Microsoft.Edge`, or `com.microsoft.wdav`.
- **Property list file**: Select the property list file associated with your app. Be sure it's a `.plist` or `.xml` file. For example, upload a `YourApp-Manifest.plist` or `YourApp-Manifest.xml` file.
- **File contents**: The key information in the property list file is shown. If you need to change the key information, open the list file in another editor, and then reupload the file in Intune.

Be sure your file is formatted correctly. The file should only have key value pairs, and shouldn't be wrapped in `<dict>`, `<plist>`, or `<xml>` tags. For example, your property list file should be similar to the following file:

```xml
<key>SomeKey</key>
<string>someString</string>
<key>AnotherKey</key>
<false/>
...
```

Select **OK** > **Create** to save your changes. The profile is created and shown in the profiles list.

## Next steps

The profile is created, but it's not doing anything yet. Next, [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

For more information on preference files for Microsoft Edge, see [Configure Microsoft Edge policy settings on macOS](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
