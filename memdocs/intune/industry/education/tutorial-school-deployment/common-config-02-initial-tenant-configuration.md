---
author: Yusuke Shinoki (HE/HIM)
ms.date: 04/10/2024
---
## Initial Tenant Configuration

This article describes organization-wide settings within Microsoft Entra ID and Microsoft Intune that affect device management. Microsoft Intune relies on Microsoft Entra ID for identity, license assignment and for devices and users grouping.

### Network prerequisites

Confirm all required network endpoint can access without SSL inspection or any type of filtering - <https://learn.microsoft.com/mem/intune/fundamentals/intune-endpoints>

### Microsoft 365 admin center

Settings described in this section are located in the Microsoft 365 admin center: <https://admin.microsoft.com>

Custom domain should be configured and validated to be able to create users and groups with organization-specific email.

| **Blade** | **Configuration group** | **Setting** | **Value** |
|---|---|---|---|
| [**Setup**](https://admin.microsoft.com/) | Sign-in and security | Get your custom domain set up | Follow the configuration wizard |

### Microsoft Entra admin center

Settings described in this section are located in the Microsoft Entra admin center: <https://entra.microsoft.com>

#### Licenses assignment

Please make sure all of your users are properly assigned with Microsoft Entra ID and Microsoft Intune licenses to be able to fully utilize Microsoft cloud services.

Additional information:

- [Assign or remove licenses in the Azure portal](https://learn.microsoft.com/entra/fundamentals/license-users-groups)
- [Assign licenses to users by group membership using the Microsoft 365 admin center](https://learn.microsoft.com/entra/identity/users/licensing-admin-center)
- [Assign licenses to users by group membership in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/users/licensing-groups-assign)

#### Tenant settings

| **Blade** | **Configuration group** | **Setting** | **Value** |
|---|---|---|---|
| **Settings** | [Mobility](https://entra.microsoft.com/) | Microsoft Intune\MDM user scope | All |
| **Settings** | [Mobility](https://entra.microsoft.com/) | Microsoft Intune\MAM user scope | None |
| **Settings** | [Domain names](https://entra.microsoft.com/) | _custom domain_ | Set your custom domain as the default. |
| **User experiences** | [Company branding](https://entra.microsoft.com/) | | Configure according to organization policies.Company branding is a prerequisite for several Intune workflows, e.g. Windows Autopilot.[Configure your company branding](https://learn.microsoft.com/entra/fundamentals/how-to-customize-branding). |
| [**Overview**](https://entra.microsoft.com/) | Properties | Security defaults | Review Security defaults and adjust if necessary |

#### Users

Basic set of settings to restrict users’ access to administrative actions.

| **Blade** | **Configuration group** | **Setting** | **Value** |
|---|---|---|---|
| [**User settings**](https://entra.microsoft.com/) | Default user role permissions | Users can register applications | No |
| [**User settings**](https://entra.microsoft.com/) | Default user role permissions | Restrict non-admin users from creating tenants | Yes |
| [**User settings**](https://entra.microsoft.com/) | Default user role permissions | Users can create security groups | No |
| [**User settings**](https://entra.microsoft.com/) | Guest user access | Guest user access restrictions | Guest user access is restricted to properties and memberships of their own directory objects (most restrictive) |
| [**User settings**](https://entra.microsoft.com/) | Administration portal | Restrict access to Microsoft Entra ID administration portal | Yes |
| [**User settings**](https://entra.microsoft.com/) | LinkedIn account connections | Allow users to connect their work or school account with LinkedIn | No |
| [**User settings**](https://entra.microsoft.com/) | Show keep user signed in | Show keep user signed in | Yes |

#### Groups

A set of settings to limit users’ ability to create groups.

| **Blade** | **Configuration group** | **Setting** | **Value** |
|---|---|---|---|
| [**Group settings**](https://entra.microsoft.com/) | General\Self Service Group Management | Owners can manage group membership requests in My Groups | Yes |
| [**Group settings**](https://entra.microsoft.com/) | General\Self Service Group Management | Restrict user ability to access groups features in My Groups | Yes |
| [**Group settings**](https://entra.microsoft.com/) | General\Security Groups | Users can create security groups in Azure portals, API or PowerShell | No |
| [**Group settings**](https://entra.microsoft.com/) | General\Microsoft 365 Groups | Users can create Microsoft 365 groups in Azure portals, API or PowerShell | No |

#### Devices

| **Blade** | **Configuration group** | **Setting** | **Value** |
|---|---|---|---|
| [**All devices\Device settings**](https://entra.microsoft.com/) | Microsoft Entra join and registration settings | Users may join devices to Microsoft Entra | All |
| [**All devices\Device settings**](https://entra.microsoft.com/) | Microsoft Entra join and registration settings | Max number of devices per user | Unlimited |
| [**All devices\Device settings**](https://entra.microsoft.com/) | Local administrator settings | Enable Microsoft Entra Local Administrator Password Solution (LAPS) (Preview) | Yes |
| [**All devices\Device settings**](https://entra.microsoft.com/) | Other settings | Restrict users from recovering the BitLocker key(s) for their owned devices | No |
| [**All devices\Enterprise State Roaming**](https://entra.microsoft.com/) | Users may sync settings and app data across devices | Users may sync settings and app data across devices | None |

### Dynamic security groups examples

Below are examples of queries commonly used for dynamic security groups.

Additional information:

- [Learn about groups and access rights in Microsoft Entra ID](https://learn.microsoft.com/entra/fundamentals/concept-learn-about-groups)
- [Create or update a dynamic group in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/users/groups-create-rule)
- [Dynamic membership rules for groups in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/users/groups-dynamic-membership)
- [Create simpler, more efficient rules for dynamic groups in Microsoft Entra ID](https://learn.microsoft.com/entra/identity/users/groups-dynamic-rule-more-efficient)

  | **Name** | **Type** | **Query** |
  |---|---|---|
  | **All Windows devices** | Dynamic membership rules | (device.deviceOSType -startsWith "Windows") |
  | **All Autopilot devices** | Dynamic membership rules | (device.devicePhysicalIDs -any _ -startsWith "[ZTDId]") |
  | **All non-Autopilot devices** | Dynamic membership rules | (device.deviceOSType -startsWith "Windows") -and (device.deviceOwnership -eq "Company") -and -not(device.devicePhysicalIds -any (\_ -startsWith "[ZTDId]")) |

### Microsoft Intune admin center

Settings described in this section are located in the Microsoft Intune admin center: <https://intune.microsoft.com>

#### [Tenant administration](https://intune.microsoft.com/)

| **Configuration group** | **Setting** | **Value** |
|---|---|---|
| [**Customization**](https://intune.microsoft.com/) | Customize branding according to organization policies.Additional information: | |
| [**Remote Help**](https://intune.microsoft.com/)**\Settings\Configure** | Enable Remote Help | Enabled |
| [**Remote Help**](https://intune.microsoft.com/)**\Settings\Configure** | Allow Remote Help to unenrolled devices | Not allowed |
| [**Device diagnostics**](https://intune.microsoft.com/) | Device diagnostics are available for corporate-managed devices running Windows 10, version 1909 and later, or Windows 11. Diagnostics may include user identifiable information such as user or device name | Enabled |
| [**Device diagnostics**](https://intune.microsoft.com/) | Automatically capture diagnostics when devices experience a failure during the Autopilot process on Windows 10 version 1909 or later and Windows 11. Diagnostics may include user identifiable information such as user or device name. | Enabled |
| [**Terms and conditions**](https://intune.microsoft.com/) | Create Terms and conditions according to organization policies.Additional information: | |

- [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](https://learn.microsoft.com/mem/intune/apps/company-portal-app)

- [Terms and conditions for user access](https://learn.microsoft.com/mem/intune/enrollment/terms-and-conditions-create)
- [Choosing the right Terms solution for your organization](https://aka.ms/intune/TOU/AadToulearnMore)

#### [Devices enrollment settings](https://intune.microsoft.com/)

| **Blade** | **Configuration group** | **Setting** | **Value** |
|---|---|---|---|
| [**Enrollment device platform restriction**](https://intune.microsoft.com/) | Android restrictions\Device type restrictions | Default\Android Enterprise (work profile) | Personally owned: Block |
| [**Enrollment device platform restriction**](https://intune.microsoft.com/) | Android restrictions\Device type restrictions | Default\Android device administrator | Platform: Block |
| [**Enrollment device platform restriction**](https://intune.microsoft.com/) | iOS restriction\Device type restrictions | Default\iOS/iPadOS | Personally owned: Block |
| [**Enrollment device platform restriction**](https://intune.microsoft.com/) | macOS restriction\Device type restrictions | Default\macOS | Personally owned: Block |
| [**Enrollment device platform restriction**](https://intune.microsoft.com/) | Windows restriction\Device type restrictions | Default\Windows (MDM) | Personally owned: Block |
| [**Windows enrollment**](https://intune.microsoft.com/) | General\Windows Hello for Business | Configure Windows Hello for Business | Disabled |

#### Intune data collection policy

{description}

| **Blade** | **Policy type** | **Setting** | **Value** |
|---|---|---|---|
| **Windows Configuration profiles** | Windows health monitoring | Health monitoring | Enable |
| **Windows Configuration profiles** | | Scope | Windows updatesEndpoint analytics |
| | | | |

#### (Optional) Enrollment Status Page

Consider enabling the Enrollment Status Page if planning to use Windows Autopilot to enroll Windows devices in Intune.

The enrollment status page (ESP) displays the provisioning status to people enrolling Windows devices and signing in for the first time. You can configure the ESP to block device use until all required policies and applications are installed. Device users can look at the ESP to track how far along their device is in the setup process.

Additional information:

- [Windows Autopilot Enrollment Status Page](https://learn.microsoft.com/autopilot/enrollment-status)
- [Set up the Enrollment Status Page](https://learn.microsoft.com/mem/intune/enrollment/windows-enrollment-status)

  | **Blade** | **Configuration group** | **Setting** | **Value** |
  |---|---|---|---|
  | [**Windows enrollment**](https://intune.microsoft.com/) | General\Enrollment Status Page | Default\Show app and profile configuration progress | Yes |
  | [**Windows enrollment**](https://intune.microsoft.com/) | General\Enrollment Status Page | Default\Show an error when installation takes longer than specified number of minutes | 120 |
  | [**Windows enrollment**](https://intune.microsoft.com/) | General\Enrollment Status Page | Default\Show custom message when time limit or error occurs | Yes |
  | [**Windows enrollment**](https://intune.microsoft.com/) | General\Enrollment Status Page | Default\Turn on log collection and diagnostics page for end users | Yes |
  | [**Windows enrollment**](https://intune.microsoft.com/) | General\Enrollment Status Page | Default\Only show page to devices provisioned by out-of-box experience (OOBE) | Yes |
  | [**Windows enrollment**](https://intune.microsoft.com/) | General\Enrollment Status Page | Enrollment Status Page\Default\Block device use until all apps and profiles are installed | Yes |
  | [**Windows enrollment**](https://intune.microsoft.com/) | Windows Autopilot Deployment Program\Deployment Profiles | Create Windows Autopilot deployment profiles according to organization policies.Additional information: | |

- [Overview of Windows Autopilot](https://learn.microsoft.com/autopilot/windows-autopilot)
- [Windows Autopilot scenarios and capabilities](https://learn.microsoft.com/autopilot/windows-autopilot-scenarios)
- [Manually register devices with Windows Autopilot](https://learn.microsoft.com/autopilot/add-devices)
- [Configure Autopilot profiles](https://learn.microsoft.com/autopilot/profiles)
- [YouTube: Windows Autopilot Fundamentals](https://www.youtube.com/watch?v=wNmLvqZ21AE&list=PLMuDtq95SdKvpS9zPyFt9fc9HgepQxaw9&index=7)

