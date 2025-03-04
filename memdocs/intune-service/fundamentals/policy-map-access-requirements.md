---
# required metadata

title: Access requirements policy mapping from Basic Mobility and Security to Intune
description: A detailed list of the policy map between Basic Mobility and Security access requirements and Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/02/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier2
- M365-identity-device-management
---

# Access requirements policy mapping from Basic Mobility and Security to Intune

This article provides mapping details between Basic Mobility and Security to Intune. Specifically, this page maps the Microsoft Purview compliance portal Access Requirement policies to the equivalent policies in Microsoft Intune. Intune offers more policy flexibility. So, each Office policy translates into multiple Intune and Microsoft Entra policies to achieve the same result.

If you're migrating from Basic Mobility and Security to Intune, you can use the [Migration evaluation tool](migrate-to-intune.md) to automate much of this mapping.

To see these settings in the Microsoft Purview compliance portal, sign in to the [Purview compliance portal](https://protection.office.com/devicev2). Then, go to the **Device security policies** list, select your policy name > **Edit policy** > **Access Requirements**.

## Before you begin

To configure the settings in an Intune policy, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md) lists and describes the built-in roles that can create policies.

## If a device doesn't meet the requirements above, then...

This setting determines if you should use Intune compliance policies or configuration profiles for all the access requirement settings. Make sure to review the details for this setting first.

> [!NOTE]
> Basic Mobility and Security never supported enforcing Conditional Access on Windows.

### Allow access and report violation (one-time enrollment is still enforced)

All Access Requirements are deployed in an Intune device configuration profile.

### Block access and report violation

All Access Requirements are deployed in an Intune compliance policy. The groups assigned are assigned to classic Conditional Access policies:

- [GraphAggregatorService] Device policy
- [Office 365 Exchange Online] Device policy
- [Outlook Service for Exchange] Device policy
- [Office 365 SharePoint Online] Device policy
- [Outlook Service for OneDrive] Device policy

## Require a password

> [!NOTE]
> All password-related settings impact only local accounts on Windows. User accounts sourced from Microsoft Entra ID are not managed by these policies.

[!INCLUDE [blockorallow](../includes/block-or-allow.md)]

Three compliance policies:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Compliance** > policy name_O365_W > **Properties** >  **Compliance settings Edit** > **System Security** > **Require a password to unlock mobile devices**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Compliance** > policy name_O365_i > **Properties** > **Compliance settings Edit** > **System Security** > **Require a password to unlock mobile devices**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Compliance** > policy name_O365_A > **Properties** > **Compliance settings Edit** > **System Security** > **Require a password to unlock mobile devices**

## Prevent simple passwords

For Android devices, this setting and multiple other Office settings are covered by one Android compliance setting. So this setting alone doesn't determine a specific Android compliance value.

[!INCLUDE [blockorallow](../includes/block-or-allow.md)]

Three compliance policies:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Compliance** > policy name_O365_W > **Properties** >  **Compliance settings Edit** > **System Security** > **Simple passwords**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Compliance** > policy name_O365_i > **Properties** > **Compliance settings Edit** > **System Security** > **Simple passwords**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Compliance** > policy name_O365_A > **Properties** > **Compliance settings Edit** > **System Security** > **Required password type**.

  - If **Prevent simple passwords** is selected, choose **Numeric complex**, **Alphabetic**, **Alphanumeric**, or **Alphanumeric with symbols** (based on other Office settings).
  - If **Prevent simple passwords** isn't selected, choose **Numeric** or a higher type in the list (based on other Office settings).

## Require an alphanumeric password

For Android devices, this setting and multiple other Office settings are covered by one Android compliance setting. So this setting alone doesn't determine a specific Android compliance value.

[!INCLUDE [blockorallow](../includes/block-or-allow.md)]

Three compliance policies:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Compliance** > policy name_O365_W > **Properties** >  **Compliance settings Edit** > **System Security** > **Required password type**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Compliance** > policy name_O365_i > **Properties** > **Compliance settings Edit** > **System Security** > **Required password type**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Compliance** > policy name_O365_A > **Properties** > **Compliance settings Edit** > **System Security** > **Required password type**.

  - If **Prevent simple passwords** is selected, choose **Numeric complex**, **Alphabetic**, **Alphanumeric**, or **Alphanumeric with symbols** (based on other Office settings).
  - If **Prevent simple passwords** isn't selected, choose **Numeric** or a higher type in the list (based on other Office settings).

## Password must include at least [1-4] character sets

[!INCLUDE [blockorallow](../includes/block-or-allow.md)]

Four compliance policies:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Compliance** > policy name_O365_W > **Properties** >  **Compliance settings Edit** > **System Security** > **Password complexity**.

  | Office value | Intune value |
  | --- | --- |
  | 1 | **Require digits and lowercase letters**. The Windows compliance policy doesn't allow only one character set, so an Office setting of **1** translates to **Require digits and lowercase letters**. |
  | 2 | **Require digits and lowercase letters** |
  | 3 | **Require digits, lowercase and uppercase letters** |
  | 4 | **Require digits, lowercase, uppercase, and special characters** |

- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Compliance** > policy name_O365_i > **Properties** > **Compliance settings Edit** > **System Security** > **Number of non-alphanumeric characters in password**.

  The iOS compliance policy doesn't enforce the number of character sets but only the number of non-alphanumeric characters that must be used. So Office values are translated to the same number of non-alphanumeric characters required.

  | Office value | Intune value |
  | --- | --- |
  | Disabled (0) | Not configured |
  | 1 | 1 |
  | 2 | 2 |
  | 3 | 3 |
  | 4 | 4 |

- **Devices** > **By platform** > **Android** > **Manage devices** > **Compliance** > policy name_O365_A > **Properties** > **Compliance settings Edit** > **System Security** > **Required password type**.

  Android doesn't support distinguishing lowercase and uppercase as different character sets, and so the Office value of 4 can't be enforced. Instead it translates to at least **Alphanumeric with symbols**.

  | Office value | Intune value |
  | --- | --- |
  | 1 | At least **Numeric** or **Numeric complex** (based on other Office settings) |
  | 2 | At least **Alphanumeric** |
  | 3 | At least **Alphanumeric with symbols** |
  | 4 | At least **Alphanumeric with symbols** |

- policy-name_OfficeMDM > **Access controls** > **Grant** > **Require device to be marked as compliant**

## Minimum password length

[!INCLUDE [blockorallow](../includes/block-or-allow.md)]

Three compliance policies:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Compliance** > policy name_O365_W > **Properties** >  **Compliance settings Edit** > **System Security** > **Minimum password length**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Compliance** > policy name_O365_i > **Properties** > **Compliance settings Edit** > **System Security** > **Minimum password length**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Compliance** > policy name_O365_A > **Properties** > **Compliance settings Edit** > **System Security** > **Required password type** and **Minimum password length**.

  | Office value for **Require an alphanumeric password** | Intune value for **Required password type** |
  | --- | --- |
  | Selected | At least **Numeric** (based on other Office settings) |
  | Not selected | At least **Numeric** (based on other Office settings) |

## Number of sign-in failures before the device is wiped

Although this setting is listed under **Access requirements** in Basic Mobility and Security, access is still allowed. It's allowed even if this setting isn't enabled on the device yet, and this setting isn't a device compliance criterion.

[!INCLUDE [blockorallow](../includes/block-or-allow.md)]

Three configuration profiles:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > policy name_O365_W > **Properties** >  **Compliance settings Edit** > **Password** > **Number of sign-in failures before wiping device**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration** > policy name_O365_i > **Properties** >  **Compliance settings Edit** > **Password** > **Number of sign-in failures before wiping device**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Configuration** > policy name_O365_A > **Properties** >  **Compliance settings Edit** > **Password** > **Number of sign-in failures before wiping device**

## Lock devices if they are inactive for this many minutes

The Windows, iOS/iPadOS, and Android compliance policies don't offer the same granularity of values, so the Office setting range is mapped to fewer Intune values.

Three compliance policies:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Compliance** > policy name_O365_W > **Properties** >  **Compliance settings Edit** > **System Security** > **Maximum minutes of inactivity before password is required**

  | Office value | Intune value |
  | --- | --- |
  | 1 through 4 | 1 minute |
  | 5 through 14 | 5 minutes |
  | 15 or more | 15 minutes |

- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Compliance** > policy name_O365_i > **Properties** > **Compliance settings Edit** > **System Security** > **Maximum minutes of inactivity before password is required**

  | Office value | Intune value |
  | --- | --- |
  | 1  | 1 minute |
  | 2  | 2 minutes |
  | 3  | 3 minutes |
  | 4  | 4 minutes |
  | 5 through 9 | 5 minutes (maximum for iOS) |
  | 10 through 14 | 10 minutes (iPadOS only) |
  | 15 or more | 15 minutes (iPadOS only) |

- **Devices** > **By platform** > **Android** > **Manage devices** > **Compliance** > policy name_O365_A > **Properties** > **Compliance settings Edit** > **System Security** > **Required password type**.

  | Office value | Intune value |
  | --- | --- |
  | 1 through 4 | 1 minute |
  | 5 through 14 | 5 minutes |
  | 15 through 29 | 15 minutes |
  | 30 through 59 | 30 minutes |
  | 60 | 60 minutes |

## Password expiration

[!INCLUDE [blockorallow](../includes/block-or-allow.md)]

Three compliance policies:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Compliance** > policy name_O365_W > **Properties** >  **Compliance settings Edit** > **System Security** > **Password expiration (days)**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Compliance** > policy name_O365_i > **Properties** > **Compliance settings Edit** > **System Security** > **Password expiration (days)**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Compliance** > policy name_O365_A > **Properties** > **Compliance settings Edit** > **System Security** > **Number of days until password expires**.

## Remember password history and prevent reuse

[!INCLUDE [blockorallow](../includes/block-or-allow.md)]

Three compliance policies:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Compliance** > policy name_O365_W > **Properties** >  **Compliance settings Edit** > **System Security** > **Number of previous passwords to prevent reuse**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Compliance** > policy name_O365_i > **Properties** > **Compliance settings Edit** > **System Security** > **Number of previous passwords to prevent reuse**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Compliance** > policy name_O365_A > **Properties** > **Compliance settings Edit** > **System Security** > **Number of previous passwords to prevent reuse** and **Required password type**

  | Office value for **Require an alphanumeric password** | Intune value for **Required password type** |
  | --- | --- |
  | Selected | At least **Numeric** (based on other Office settings) |
  | Not selected | At least **Numeric** (based on other Office settings) |

## Require data encryption on devices

This setting was never configurable for Windows or iOS/iPadOS in Basic Mobility and Security.

[!INCLUDE [blockorallow](../includes/block-or-allow.md)]

One compliance policy:

- **Devices** > **By platform** > **Android** > **Manage devices** > **Compliance** > policy name_O365_A > **Properties** > **Compliance settings Edit** > **System Security** > **Encryption of data storage on device**

## Prevent jail broken or rooted devices from connecting

This setting was never configurable for Windows in Basic Mobility and Security.

For Android devices, Intune only supports this setting for Android device administrator devices.

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

[!INCLUDE [blockorallow](../includes/block-or-allow.md)]

Two compliance policies:

- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Compliance** > policy name_O365_i > **Properties** > **Compliance settings Edit** > **Device Health** > **Jailbroken devices**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Compliance** > policy name_O365_A > **Properties** > **Compliance settings Edit** > **Device Health** > **Rooted devices**

## Require managing email profile (required for selective wipe on iOS)

Requiring this setting was never supported for Windows or Android compliance in Basic Mobility and Security.
Windows email was never supported for Windows 10 in Basic Mobility and Security.

For Android, this setting was only supported on Samsung Knox devices in Basic Mobility and Security.

Intune requires more settings be configured when deploying email that weren't available in device security policies. For more information, see [More settings required by Intune for email profiles](#more-settings-required-by-intune-for-email-profiles).

[!INCLUDE [blockorallow](../includes/block-or-allow.md)]

Three configuration profiles and one compliance policy:

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > policy name_O365_W_Email > **Properties** > **Configuration settings Edit**

  | Setting | Value |
  | --- | --- |
  | Email server | outlook.office365.com |
  | Account name | Office 365 email |
  | Username attribute from Microsoft Entra ID | User Principal Name |
  | Email address attribute from Microsoft Entra ID | User Principal Name |
  | SSL | Enable |

- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration** > policy name_O365_i_Email > **Properties** > **Configuration settings Edit**

  | Setting | Value |
  | --- | --- |
  | Email server | outlook.office365.com |
  | Account name | Office 365 email |
  | Username attribute from Microsoft Entra ID | User Principal Name |
  | Email address attribute from Microsoft Entra ID | User Principal Name |
  | Authentication name | Username and password |
  | SSL | Enable |

- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Compliance** > policy name_O365_i > **Properties** > **Compliance settings Edit** > **Email** > **Unable to set up email on the device** > **Require**
- **Devices** > **Android ** > **Configuration profiles** > policy name_O365_A_Email > **Properties** > ** Configuration settings Edit**

  | Setting | Value |
  | --- | --- |
  | Email server | outlook.office365.com |
  | Account name | Office 365 email |
  | Username attribute from Microsoft Entra ID | User Principal Name |
  | Email address attribute from Microsoft Entra ID | User Principal Name |
  | Authentication name | Username and password |
  | SSL | Enable |

### More settings required by Intune for email profiles

The following settings aren't deployed by device security policies. But when deploying email profiles, Intune requires the settings have a value.

| Platform | Setting | Value in migration |
| --- | --- | --- |
| Android | Require S/mime | false |
| Android | Sync Contacts | true |
| Android | Sync Calendar | true |
| Android | Sync Tasks | true |
| Android | Sync Notes | false |
| iOS | Block moving messages to other email accounts | false |
| iOS | Block sending Email from third party addresses | false |
| iOS | Block syncing recently used email addresses | false |
| iOS | Require S/mime | false |
| Windows 10 | Sync Contacts | true |
| Windows 10 | Sync Calendar | true |
| Windows 10 | Sync Tasks | true |

## Related articles

[Migration evaluation tool](migrate-to-intune.md)
