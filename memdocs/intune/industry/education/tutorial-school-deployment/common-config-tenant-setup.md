---
title: Common Education tenant configuration
description: Learn about common tenant configuration used by Eduation organizations in Intune
ms.date: 04/09/2024
ms.topic: overview
author: scottbreenmsft
ms.author: scbree
---

# Initial Tenant Configuration

This article describes organization-wide settings within Microsoft Entra ID and Microsoft Intune that affect device management. Microsoft Intune relies on Microsoft Entra ID for identity, license assignment and for devices and users grouping.

#### Network prerequisites

Confirm all required network endpoint can access without SSL inspection or any type of filtering - https://learn.microsoft.com/mem/intune/fundamentals/intune-endpoints

#### Microsoft 365 admin center

Settings described in this section are located in the Microsoft 365 admin center: https://admin.microsoft.com

Custom domain should be configured and validated to be able to create users and groups with organization-specific email.

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| Setup | Sign-in and security | Get your custom domain set up | Follow the configuration wizard |

#### Microsoft Entra admin center

Settings described in this section are located in the Microsoft Entra admin center: https://entra.microsoft.com

##### Licenses assignment

Please make sure all of your users are properly assigned with Microsoft Entra ID and Microsoft Intune licenses to be able to fully utilize Microsoft cloud services.

Additional information:

- Assign or remove licenses in the Azure portal
- Assign licenses to users by group membership using the Microsoft 365 admin center
- Assign licenses to users by group membership in Microsoft Entra ID

##### Tenant settings

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| Settings | Mobility | Microsoft Intune\\MDM user scope | All |
| Settings | Mobility | Microsoft Intune\\MAM user scope | None |
| Settings | Domain names | custom domain | Set your custom domain as the default. |
| User experiences | Company branding | Configure according to organization policies. | Company branding is a prerequisite for several Intune workflows, e.g. Windows Autopilot. |

Configure your company branding .

| Overview | Properties | Security defaults | Review Security defaults and adjust if necessary |

##### Users

Basic set of settings to restrict users’ access to administrative actions.

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| User settings | Default user role permissions | Users can register applications | No |
| User settings | Default user role permissions | Restrict non-admin users from creating tenants | Yes |
| User settings | Default user role permissions | Users can create security groups | No |
| User settings | Guest user access | Guest user access restrictions | Guest user access is restricted to properties and memberships of their own directory objects (most restrictive) |
| User settings | Administration portal | Restrict access to Microsoft Entra ID administration portal | Yes |
| User settings | LinkedIn account connections | Allow users to connect their work or school account with LinkedIn | No |
| User settings | Show keep user signed in | Show keep user signed in | Yes |

##### Groups

A set of settings to limit users’ ability to create groups.

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| Group settings | General\\Self Service Group Management | Owners can manage group membership requests in My Groups | Yes |
| Group settings | General\\Self Service Group Management | Restrict user ability to access groups features in My Groups | Yes |
| Group settings | General\\Security Groups | Users can create security groups in Azure portals, API or PowerShell | No |
| Group settings | General\\Microsoft 365 Groups | Users can create Microsoft 365 groups in Azure portals, API or PowerShell | No |

##### Devices

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| All devices | Device settings | Microsoft Entra join and registration settings | Users may join devices to Microsoft Entra | All |
| All devices | Device settings | Microsoft Entra join and registration settings | Max number of devices per user | Unlimited |
| All devices | Device settings | Local administrator settings | Enable Microsoft Entra Local Administrator Password Solution (LAPS) (Preview) | Yes |
| All devices | Device settings | Other settings | Restrict users from recovering the BitLocker key(s) for their owned devices | No |
| All devices | Enterprise State Roaming | Users may sync settings and app data across devices | Users may sync settings and app data across devices | None |

##### Dynamic security groups examples

Below are examples of queries commonly used for dynamic security groups.

Additional information:

- Learn about groups and access rights in Microsoft Entra ID
- Create or update a dynamic group in Microsoft Entra ID
- Dynamic membership rules for groups in Microsoft Entra ID
- Create simpler, more efficient rules for dynamic groups in Microsoft Entra ID

| Name | Type | Query |
| --- | --- | --- |
| All Windows devices | Dynamic membership rules | (device.deviceOSType -startsWith \"Windows\") |
| All Autopilot devices | Dynamic membership rules | (device.devicePhysicalIDs -any _ -startsWith \"[ZTDId]\") |
| All non-Autopilot devices | Dynamic membership rules | (device.deviceOSType -startsWith \"Windows\") -and (device.deviceOwnership -eq \"Company\") -and -not(device.devicePhysicalIds -any (_ -startsWith \"[ZTDId]\")) |

### Microsoft Intune admin center

Settings described in this section are located in the Microsoft Intune admin center: https://intune.microsoft.com

#### Tenant administration

| Configuration group | Setting | Value |
| --- | --- | --- |
| Customization | Customize branding according to organization policies. | |

Additional information:

- How to configure the Intune Company Portal apps, Company Portal website, and Intune app

| Remote Help | Settings\\Configure | Enable Remote Help | Enabled |
| Remote Help | Settings\\Configure | Allow Remote Help to unenrolled devices | Not allowed |

##### Device diagnostics

Device diagnostics are available for corporate-managed devices running Windows 10, version 1909 and later, or Windows 11. Diagnostics may include user identifiable information such as user or device name

| Device diagnostics | Automatically capture diagnostics when devices experience a failure during the Autopilot process on Windows 10 version 1909 or later and Windows 11. Diagnostics may include user identifiable information such as user or device name. | Enabled |

##### Terms and conditions

Create Terms and conditions according to organization policies.

Additional information:

- Terms and conditions for user access
- Choosing the right Terms solution for your organization

##### Devices enrollment settings

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| Enrollment device platform restriction | Android restrictions\\Device type restrictions | Default\\Android Enterprise (work profile) | Personally owned: Block |
| Enrollment device platform restriction | Android restrictions\\Device type restrictions | Default\\Android device administrator | Platform: Block |
| Enrollment device platform restriction | iOS restriction\\Device type restrictions | Default\\iOS/iPadOS | Personally owned: Block |
| Enrollment device platform restriction | macOS restriction\\Device type restrictions | Default\\macOS | Personally owned: Block |
| Enrollment device platform restriction | Windows restriction\\Device type restrictions | Default\\Windows (MDM) | Personally owned: Block |

##### Windows enrollment

| General | Windows Hello for Business | Configure Windows Hello for Business | Disabled |

#### Intune data collection policy

{description}

| Policy type | Setting | Value |
| --- | --- | --- |
| Windows Configuration profiles | Windows health monitoring | Health monitoring | Enable |
| Windows Configuration profiles | Scope | Windows updates | Endpoint analytics |

##### (Optional) Enrollment Status Page

Consider enabling the Enrollment Status Page if planning to use Windows Autopilot to enroll Windows devices in Intune.