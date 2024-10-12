---
# required metadata

title: Microsoft Intune endpoint security disk encryption policy
description: Configure and deploy Microsoft Intune endpoint security policy disk encryption policies for BitLocker and FileVault.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/23/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- sub-secure-endpoints
ms.reviewer: aanavath

---

# Disk encryption policy for endpoint security in Intune

Endpoint security Disk encryption profiles focus on only the settings that are relevant for a devices built-in encryption method, like FileVault, BitLocker, and Personal Data Encryption (for Windows). This focus makes it easy for security admins to manage disk encryption settings without having to navigate a host of unrelated settings.

While you can configure the same device settings by using *Endpoint Protection* profiles for device configuration, the device configuration profiles include other categories of settings. These other settings are unrelated to disk encryption and can complicate the task of configuring only disk encryption.

Find the endpoint security policies for disk encryption under *Manage* in the **Endpoint security** node of the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

## Prerequisites for disk encryption policy

- **macOS** - macOS 10.13 or later
- **Windows** - Windows 10
- **Windows** - Windows 11

## Role-based access controls (RBAC)

For guidance on assigning the right level of permissions and rights to manage Intune Disk encryption policy, see [Assign-role-based-access-controls-for-endpoint-security-policy](../protect/endpoint-security-policy.md#assign-role-based-access-controls-for-endpoint-security-policy).

## Disk encryption profiles

**macOS profiles**:

- **FileVault** - FileVault provides built-in Full Disk Encryption for macOS devices.

  Manage [FileVault settings](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) for macOS.

  To create a FileVault profile, see [Use FileVault disk encryption for macOS](../protect/encrypt-devices-filevault.md).

**Windows profiles**:

- **BitLocker** - BitLocker Drive Encryption is a data protection feature that integrates with the operating system and addresses the threats of data theft or exposure from lost, stolen, or inappropriately decommissioned computers.

  > [!NOTE]
  >
  > Beginning on June 19, 2023, the BitLocker profile for Windows was updated to use the settings format as found in the Settings Catalog. The new profile format includes the same settings as the older profile. With this change you can no longer create new versions of the old profiles. Your existing instances of the old profile remain available to use and edit.
  >
  > With the new profile format, we no longer publish a dedicated list of settings as found in the profile. Instead, use the *Learn more* link in the UI while viewing information for a setting, to open [BitLocker CSP](/windows/client-management/mdm/bitlocker-csp) in the Windows documentation, where the setting is detailed in full.
  >
  > You can continue to find a list of settings in the original BitLocker profiles created before June 19, 2023, at [BitLocker settings](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker) in the Intune documentation.

- **Personal Data Encryption** - Personal Data Encryption (PDE) encrypts data at the folder level and is available for devices that run Windows 11 version 22H2 or later. PDE differs from BitLocker in that it encrypts files instead of whole volumes and disks. PDE occurs in addition to other encryption methods such as BitLocker. Unlike BitLocker that releases data encryption keys at boot, PDE doesn't release data encryption keys until a user signs in using Windows Hello for Business. PDE uses the [PDE CSP](/windows/client-management/mdm/personaldataencryption-csp).

  For more information about PDE, including prerequisites, related requirements, and recommendations, see the following articles in the Windows security documentation:
  - [PDE overview](/windows/security/operating-system-security/data-protection/personal-data-encryption/)
  - [Configure PDE](/windows/security/operating-system-security/data-protection/personal-data-encryption/configure)
  - [PDE frequently asked questions (FAQ)](/windows/security/operating-system-security/data-protection/personal-data-encryption/faq)

To create a BitLocker or Personal Data Encryption profile, see [Use disk encryption for Windows](../protect/encrypt-devices.md).

## Manage device encryption

After you deploy policy to encrypt a device disk, see the following articles for information on managing encryption:

- [Manage encryption on Windows](../protect/encrypt-devices.md)
- [Manage encryption on macOS](../protect/encrypt-devices-filevault.md#manage-filevault)
- [Monitor device encryption](../protect/encryption-monitor.md)

## Next steps

- [To create a macOS encryption profile](../protect/encrypt-devices-filevault.md#create-endpoint-security-policy-for-filevault)
- [To create a Windows encryption profile](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-windows)
