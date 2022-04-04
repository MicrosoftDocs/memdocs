---
# required metadata

title: Manage disk encryption with endpoint security policies in Microsoft Intune | Microsoft Docs
description: Configure and deploy policies for devices you manage with endpoint security disk encryption policy in Microsoft Endpoint Manager. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/04/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: aanavath

---

# Disk encryption policy for endpoint security in Intune

Endpoint security Disk encryption profiles focus on only the settings that are relevant for a devices built-in encryption method, like FileVault or BitLocker. This focus makes it easy for security admins to manage disk encryption settings without having to navigate a host of unrelated settings.

While you can configure the same device settings by using *Endpoint Protection* profiles for device configuration, the device configuration profiles include additional categories of settings. These additional settings are unrelated to disk encryption and can complicate the task of configuring only disk encryption.

Find the endpoint security policies for disk encryption under *Manage* in the **Endpoint security** node of the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

## Prerequisites for disk encryption policy

- **macOS** - macOS 10.13 or later
- **Windows** - Windows 10/11

## Disk encryption profiles

**macOS profiles**:

- **FileVault** - FileVault provides built-in Full Disk Encryption for macOS devices.

  Manage [FileVault settings](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) for macOS.

  To create a FileVault profile, see [Use FileVault disk encryption for macOS](../protect/encrypt-devices-filevault.md).

**Windows profiles**:

> [!NOTE]  
> Beginning in April 2022, the *BitLocker* profile for the *Windows 10 and later* platform was replaced by by a new profile instance. This new profile use the settings format as found in the Settings Catalog. The new profile template includes the same settings as the older profile template it replaces. With this change you can no longer create new versions of the old profile. Your existing instances of the old profile remain available to use and edit.

- **BitLocker** - BitLocker Drive Encryption is a data protection feature that integrates with the operating system and addresses the threats of data theft or exposure from lost, stolen, or inappropriately decommissioned computers


  To create a BitLocker profile, see [Use BitLocker disk encryption for Windows](../protect/encrypt-devices.md).

## Manage device encryption

After you deploy policy to encrypt a device disk, see the following articles for information on managing encryption:

- [Manage BitLocker](../protect/encrypt-devices.md#manage-bitlocker)
- [Manage FileVault](../protect/encrypt-devices-filevault.md#manage-filevault)
- [Monitor device encryption](../protect/encryption-monitor.md)

## Next steps

- [To create a FileVault profile](../protect/encrypt-devices-filevault.md#create-endpoint-security-policy-for-filevault)
- [To create a BitLocker profile](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker)

View details for the Windows settings in the deprecated profile for Windows BitLocker:

- [BitLocker settings](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker)