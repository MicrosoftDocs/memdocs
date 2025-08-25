---
# required metadata

title: Intune endpoint security Account protection (Preview) policy settings
description: Endpoint security Account protection policy settings in Microsoft Intune
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2024
ms.topic: reference
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
- tier3
- M365-identity-device-management
- sub-secure-endpoints
ms.reviewer: juidaewo

---
# Account protection policy settings for endpoint security in Intune

> [!IMPORTANT]
>
> In July 2024, the following Intune profiles for identity protection and account protection were deprecated and replaced by a new consolidated profile named *Account protection*. This newer profile is found in the account protection policy node of endpoint security, and is the only profile template that remains available to create new policy instances for identity and account protection. The settings from this new profile are also available through the settings catalog. 
>
> Any instances of the following older profiles that you have created remain available to use and edit:
> 
> - **Identity protection** – previously available from  *Devices* > *Configuration* > *Create* >  *New Policy* > *Windows 10 and later* > *Templates* > *Identity Protection*
> - **Account protection (Preview)** – previously available from *Endpoint Security* > *Account protection* > *Windows 10 and later* > *Account protection ( Preview)*

This article describes settings that are available in profiles for *Account protection (preview)*, which is a profile type that was previously available through the *Account protection* policy for Intune [Endpoint security](../protect/endpoint-security-policy.md). Although you cannot create new instances of this profile, the information in this article applies to instances of the profile you might still have in use.

The settings in this article apply to:

- Windows 10
- Windows 11

Supported platforms and profiles:

- **Windows 10 and later**:
  - Profile: **Account protection (Preview)**

> [!TIP]
>
> For *Local user group membership* profiles, see [Manage local groups on Windows devices](../protect/endpoint-security-account-protection-policy.md#manage-local-groups-on-windows-devices).
>
> For *Local admin password solution (Windows LAPS)* profiles, see [Manage LAPS policy](../protect/windows-laps-policy.md).

## Account protection profile (Preview)

*The following settings details apply only to the endpoint security profile template for Account protection (Preview), which was deprecated in July 2024.*

- **Block Windows Hello for Business**

  Windows Hello for Business is an alternative method for signing into Windows by replacing passwords, Smart Cards, and Virtual Smart Cards.
  - **Not configured** (*default*) - Devices provision Windows Hello for Business.
  - **Disabled** - Devices provision Windows Hello for Business. With this configuration, more settings are available that support configurations for PIN, Trusted Platform Module (TPM), and more.
  - **Enabled** - Devices don't provision Windows Hello for Business for any user
  
> [!IMPORTANT]
>
> Due to how Intune determines the scope and applicability of Windows Hello for Business policy, the device may log **Event ID 454** as a result of applying policy. This can be safely ignored when policy is being successful applied (and enforced).

- **Enable to use security keys for sign-in**

  Enable Windows Hello security key as a sign-in credential for all PCs in the tenant.
  - **Not configured** (*default*)
  - **Yes**

- **Turn on Credential Guard**  
  [CSP: DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard uses Windows Hypervisor to provide protections. Credential Guard requires hardware support for Secure Boot and DMA protections. This setting is only successful on devices that meet the hardware requirements.
  - **Not configured** (*default*) - Disable the use of Credential Guard, which is the Windows default.
  - **Enable with UEFI lock** - Enable Credential Guard and block it from being turned off remotely, as the UEFI persisted configuration must be manually cleared.
  - **Enable without UEFI lock** - Enable Credential Guard and allow it to be turned off without physical access to the machine.

## Next steps

[Endpoint security policy for Account protection](../protect/endpoint-security-account-protection-policy.md)
