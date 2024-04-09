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

## Network pre-requisites

Confirm all the required network endpoints can access without SSL inspection or any type of filtering. See [Network endpoints for Microsoft Intune](/mem/intune/fundamentals/intune-endpoints) for a list of endpoints.

## Microsoft 365 admin center

Settings described in this section are located in the Microsoft 365 admin center: <a href="https://admin.microsoft.com/" target="_blank"><b>https://admin.microsoft.com</b></a>.

Custom domain should be configured and validated to be able to create users and groups with organization-specific email.

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| [Setup](https://admin.microsoft.com/#/featureexplorer) | Sign-in and security | Get your custom domain set up | Follow the configuration wizard |

## Microsoft Entra admin center

Settings described in this section are located in the Microsoft Entra admin center: <a href="https://entra.microsoft.com" target="_blank"><b>https://entra.microsoft.com</b></a>

### Licenses assignment

Please make sure all of your users are properly assigned with Microsoft Entra ID and Microsoft Intune licenses to be able to fully utilize Microsoft cloud services.

Additional information:

- Assign or remove licenses in the Azure portal
- Assign licenses to users by group membership using the Microsoft 365 admin center
- Assign licenses to users by group membership in Microsoft Entra ID

### Tenant settings

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| Settings | Mobility | Microsoft Intune\\MDM user scope | All |
| Settings | Mobility | Microsoft Intune\\MAM user scope | None |
| Settings | Domain names | custom domain | Set your custom domain as the default. |
| User experiences | Company branding | Configure according to organization policies. | Company branding is a prerequisite for several Intune workflows, e.g. Windows Autopilot. <br> [Configure your company branding](https://learn.microsoft.com/entra/fundamentals/how-to-customize-branding) |
| [Overview](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/TenantOverview.ReactView) | Properties | Security defaults | Review Security defaults and adjust if necessary |

### Users

Basic set of settings to restrict users’ access to administrative actions.

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| [User settings](https://entra.microsoft.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/UserSettings/menuId/UserSettings) | Default user role permissions | Users can register applications | No |
| [User settings](https://entra.microsoft.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/UserSettings/menuId/UserSettings) | Default user role permissions | Restrict non-admin users from creating tenants | Yes |
| [User settings](https://entra.microsoft.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/UserSettings/menuId/UserSettings) | Default user role permissions | Users can create security groups | No |
| [User settings](https://entra.microsoft.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/UserSettings/menuId/UserSettings) | Guest user access | Guest user access restrictions | Guest user access is restricted to properties and memberships of their own directory objects (most restrictive) |
| [User settings](https://entra.microsoft.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/UserSettings/menuId/UserSettings) | Administration portal | Restrict access to Microsoft Entra ID administration portal | Yes |
| [User settings](https://entra.microsoft.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/UserSettings/menuId/UserSettings) | LinkedIn account connections | Allow users to connect their work or school account with LinkedIn | No |
| [User settings](https://entra.microsoft.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/UserSettings/menuId/UserSettings) | Show keep user signed in | Show keep user signed in | Yes |

### Groups

A set of settings to limit users’ ability to create groups.

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| [Group settings](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/GroupsManagementMenuBlade/~/General/menuId/General) | General\\Self Service Group Management | Owners can manage group membership requests in My Groups | Yes |
| [Group settings](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/GroupsManagementMenuBlade/~/General/menuId/General) | General\\Self Service Group Management | Restrict user ability to access groups features in My Groups | Yes |
| [Group settings](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/GroupsManagementMenuBlade/~/General/menuId/General) | General\\Security Groups | Users can create security groups in Azure portals, API or PowerShell | No |
| [Group settings](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/GroupsManagementMenuBlade/~/General/menuId/General) | General\\Microsoft 365 Groups | Users can create Microsoft 365 groups in Azure portals, API or PowerShell | No |

### Devices

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| [All devices\Device settings](https://entra.microsoft.com/#view/Microsoft_AAD_Devices/DevicesMenuBlade/~/DeviceSettings/menuId/Devices) | Microsoft Entra join and registration settings | Users may join devices to Microsoft Entra | All |
| [All devices\Device settings](https://entra.microsoft.com/#view/Microsoft_AAD_Devices/DevicesMenuBlade/~/DeviceSettings/menuId/Devices) | Microsoft Entra join and registration settings | Max number of devices per user | Unlimited |
| [All devices\Device settings](https://entra.microsoft.com/#view/Microsoft_AAD_Devices/DevicesMenuBlade/~/DeviceSettings/menuId/Devices) | Local administrator settings | Enable Microsoft Entra Local Administrator Password Solution (LAPS) (Preview) | Yes |
| [All devices\Device settings](https://entra.microsoft.com/#view/Microsoft_AAD_Devices/DevicesMenuBlade/~/DeviceSettings/menuId/Devices) | Other settings | Restrict users from recovering the BitLocker key(s) for their owned devices | No |
| [All devices\Enterprise State Roaming](https://entra.microsoft.com/#view/Microsoft_AAD_Devices/DevicesMenuBlade/~/RoamingSettings/menuId/Devices) | Users may sync settings and app data across devices | Users may sync settings and app data across devices | None |

### Dynamic security groups examples

Below are examples of queries commonly used for dynamic security groups.

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

## Microsoft Intune admin center

Settings described in this section are located in the Microsoft Intune admin center: https://intune.microsoft.com

### Tenant administration

| Configuration group | Setting | Value |
| --- | --- | --- |
| Customization | Customize branding according to organization policies. For more information, see [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](https://learn.microsoft.com/mem/intune/apps/company-portal-app) | |
| [Remote Help](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/TenantAdminMenu/~/remote)\ Settings\Configure | Enable Remote Help | Enabled |
| [Remote Help](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/TenantAdminMenu/~/remote)\ Settings\Configure | Allow Remote Help to unenrolled devices | Not allowed |
| [Device diagnostics](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/TenantAdminMenu/~/termsAndConditions) | Device diagnostics are available for corporate-managed devices running Windows 10, version 1909 and later, or Windows 11. Diagnostics may include user identifiable information such as user or device name | Enabled |
| [Device diagnostics](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/TenantAdminMenu/~/termsAndConditions) | Automatically capture diagnostics when devices experience a failure during the Autopilot process on Windows 10 version 1909 or later and Windows 11. Diagnostics may include user identifiable information such as user or device name. | Enabled |
| [Terms and conditions](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/TenantAdminMenu/~/termsAndConditions) | Create Terms and conditions according to organization policies. For more information, see ]Terms and conditions for user access](/mem/intune/enrollment/terms-and-conditions-create) | |

### Devices enrollment settings

| Blade | Configuration group | Setting | Value |
| --- | --- | --- | --- |
| [Enrollment device platform restriction](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesEnrollmentMenu/~/deviceTypeEnrollmentRestrictions) | Android restrictions\\Device type restrictions | Default\\Android Enterprise (work profile) | Personally owned: Block |
| [Enrollment device platform restriction](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesEnrollmentMenu/~/deviceTypeEnrollmentRestrictions) | Android restrictions\\Device type restrictions | Default\\Android device administrator | Platform: Block |
| [Enrollment device platform restriction](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesEnrollmentMenu/~/deviceTypeEnrollmentRestrictions) | iOS restriction\\Device type restrictions | Default\\iOS/iPadOS | Personally owned: Block |
| [Enrollment device platform restriction](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesEnrollmentMenu/~/deviceTypeEnrollmentRestrictions) | macOS restriction\\Device type restrictions | Default\\macOS | Personally owned: Block |
| [Enrollment device platform restriction](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesEnrollmentMenu/~/deviceTypeEnrollmentRestrictions) | Windows restriction\\Device type restrictions | Default\\Windows (MDM) | Personally owned: Block |
| [Windows enrollment](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesEnrollmentMenu/~/windowsEnrollment) | General | Windows Hello for Business | Configure Windows Hello for Business | Disabled |

### Intune data collection policy

{description}

| Policy type | Setting | Value |
| --- | --- | --- |
| Windows Configuration profiles | Windows health monitoring | Health monitoring | Enable |
| Windows Configuration profiles | Scope | Windows updates | Endpoint analytics |

### (Optional) Enrollment Status Page

Consider enabling the Enrollment Status Page if planning to use Windows Autopilot to enroll Windows devices in Intune.
