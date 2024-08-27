---
# required metadata

title: Deploy policy for Windows Hello to groups of Windows 10 and Windows 11 devices in Microsoft Intune
description: Use a Microsoft Intune profile for Identity protection configure Windows Hello for Business on Windows devices.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/23/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- identity-protection
- sub-secure-endpoints
---

# Use identity protection profiles to manage Windows Hello for Business in Microsoft Intune

> [!IMPORTANT]
>
> In July 2024, the following Intune profiles for identity protection and account protection were deprecated and replaced by a new consolidated profile named *Account protection*. This newer profile is found in the account protection policy node of endpoint security, and is the only profile template that remains available to create new policy instances for identity and account protection. The settings from this new profile are also available through the settings catalog. 
>
> Any instances of the following older profiles that you have created remain available to use and edit:
>
> - *Identity protection* – previously available from  *Devices* > *Configuration* > *Create* >  *New Policy* > *Windows 10 and later* > *Templates* > *Identity Protection*
> - *Account protection (Preview)* – previously available from *Endpoint Security* > *Account protection* > *Windows 10 and later* > *Account protection ( Preview)*

Microsoft Intune supports use of *Account protection* profiles to manage Windows Hello for Business on your managed Windows devices. [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-overview) is a method for signing in to Windows devices by replacing passwords, smart cards, and virtual smart cards.

Applies to:

- Windows 10
- Windows 11

When you use Intune Account protection profiles to manage Windows Hello for Business settings, you can:

- Enable Windows Hello for Business for devices and users
- Set device PIN requirements, including a minimum or maximum PIN length
- Allow gestures, such as a fingerprint, that users can (or can't use) to sign in to devices

In addition to Account protection profiles, Intune supports the following options to manage settings for Windows Hello for Business:

- [During device enrollment](../protect/windows-hello.md): Configure tenant-wide policy that applies Windows Hello settings to devices at the time the device enrolls with Intune.
- [Security baselines](../protect/security-baselines.md): Some settings for Windows Hello can be managed through Intune's security baselines, like the baselines for *Microsoft Defender for Endpoint security* or *Security Baseline for Windows 10 and later*.
- [Settings catalog](../configuration/settings-catalog.md): The settings from endpoint security Account protection profiles are available in the Intune settings catalog.

> [!NOTE]
> For customers looking to configure Windows Holographic for Business, please use [DeviceLock CSP](/windows/client-management/mdm/policy-csp-devicelock)

## Next steps

- [Configure Account protection profiles to manage Windows Hello for Business settings](../protect/endpoint-security-account-protection-policy.md)
- [Review settings, and what they do](identity-protection-windows-settings.md)
- [Monitor the profile status](../configuration/device-profile-monitor.md)
