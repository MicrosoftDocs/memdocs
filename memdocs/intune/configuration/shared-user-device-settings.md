---
# required metadata

title: Shared or multi-user device settings in Microsoft Intune - Azure | Microsoft Docs
description: Add and use Windows 10 and Windows Holographic for Business devices that are shared, or used by multiple users in Microsoft Intune. See a list of all the settings and what they do on the devices, including Microsoft HoloLens. Control guest accounts, manage accounts and delete inactive accounts, allow or prevent saving to local storage, set power and sleep options, choose when updates are installed, and use devices in education environments in a device configuration profile.
keywords:
author: MandiOhlinger

ms.author: mandia
manager: dougeby
ms.date: 11/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
---

# Control access, accounts, and power features on shared PC or multi-user devices using Intune

Devices that have multiple users are called shared devices, and are a common part of mobile device management (MDM) solutions. Using Microsoft Intune, you can customize shared devices running the following platforms:

- Windows 10 Professional and newer
- Windows 10 Enterprise and newer
- Windows Holographic for Business, such as the HoloLens

For example, schools have devices that are typically used by many students. With this setting, the school Intune administrator can turn on the Shared PC feature to allow one user at a time. Students can't switch between different signed-in accounts on the device. When the student signs out, you also choose to remove all user-specific settings.

End users can sign in to these shared devices with a guest account. After users sign in, the credentials are cached. As they use the device, end-users only get access to features you allow. For example, you choose when the device goes in to sleep mode, if users can see and save files locally, enable or disable power management settings, and more. You also control if the guest account deletes when the user signs-off, or delete inactive accounts when a threshold is reached.

This article shows you how to create a configuration profile, and includes links to the available settings with their descriptions.

When the profile is created in Intune, you deploy or assign the profile to device groups in your organization. You can also assign this profile to device groups with mixed device types and operating system (OS) versions.

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

   - **Name**: Enter a descriptive name for the new profile.
   - **Description**: Enter a description for the profile. This setting is optional, but recommended.
   - **Platform**: Select **Windows 10 and later**.
   - **Profile type**: Select **Shared multi-user device**.

4. Configure the settings for [Windows 10 and later](shared-user-device-settings-windows.md) or [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md).

5. Select **OK** > **Create** to save your changes.

Your profile is created and shown in the list, but it's not doing anything yet. Be sure to [assign the profile](device-profile-assign.md) to device groups in your organization.

## Next steps

- See all the settings for [Windows 10 and newer](shared-user-device-settings-windows.md) and [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md).
- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
