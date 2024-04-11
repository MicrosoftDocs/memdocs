---
title: Common Education tenant configuration
description: Learn about common tenant configuration used by Education organizations in Intune.
ms.date: 04/09/2024
ms.topic: overview
author: scottbreenmsft
ms.author: scbree
---

# Initial Tenant Configuration

## Microsoft 365 admin center

Settings described in this section are located in the Microsoft 365 admin center: <a href="https://admin.microsoft.com/" target="_blank"><b>https://admin.microsoft.com</b></a>.

Custom domain should be configured and validated to be able to create users and groups with organization-specific email.

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| [Setup](https://admin.microsoft.com/#/featureexplorer) | Sign-in and security | Get your custom domain setup | Follow the configuration wizard |

Entra:
## Tenant settings (review)

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| Settings | Domain names | custom domain | Set your custom domain as the default. |

## Microsoft Entra admin center

Settings described in this section are located in the Microsoft Entra admin center: <a href="https://entra.microsoft.com" target="_blank"><b>https://entra.microsoft.com</b></a>

### Dynamic security groups examples

Here are examples of queries commonly used for dynamic security groups.

Additional information:

- [Learn about groups and access rights in Microsoft Entra ID](/entra/fundamentals/concept-learn-about-groups)
- [Create or update a dynamic group in Microsoft Entra ID](/entra/fundamentals/concept-learn-about-groups)
- [Dynamic membership rules for groups in Microsoft Entra ID](/entra/fundamentals/concept-learn-about-groups)
- [Create simpler, more efficient rules for dynamic groups in Microsoft Entra ID](/entra/fundamentals/concept-learn-about-groups)

| Name | Type | Query |
| --- | --- | --- |
| All Windows devices | Dynamic membership rules | (device.deviceOSType -startsWith \"Windows\") |
| All Autopilot devices | Dynamic membership rules | (device.devicePhysicalIDs -any _ -startsWith \"[ZTDId]\") |
| All non-Autopilot devices | Dynamic membership rules | (device.deviceOSType -startsWith \"Windows\") -and (device.deviceOwnership -eq \"Company\") -and -not(device.devicePhysicalIds -any (_ -startsWith \"[ZTDId]\")) |
