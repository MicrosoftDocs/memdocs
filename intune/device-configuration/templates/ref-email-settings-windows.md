---
title: Email settings for Windows devices in Microsoft Intune
description: Create a device configuration email profile that that uses Exchange servers, and retrieves attributes from Microsoft Entra ID. You can also enable SSL, and synchronize email and schedules on Windows 10/11 client devices using Microsoft Intune.
ms.date: 06/23/2026
ms.topic: reference
ms.reviewer: sheetg
ms.collection:
- M365-identity-device-management
---

# Email profile settings for Windows devices in Microsoft Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

In Microsoft Intune, you can create and configure an email profile to connect to an Exchange email server, choose how users authenticate, use S/MIME for encryption, and more. The email profile uses the native or built-in email app on the device, and users can connect to their organization email.

This article describes some of the settings you can configure. You can create a device configuration profile to assign or deploy these email settings to your iOS/iPadOS devices.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]
:::column-end:::
:::column span="3":::
> This feature supports the following platform:
> - Windows
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To configure this policy and start collecting inventory data from devices, use an account with at least one of the following roles:
> - [!INCLUDE [minimum-rbac-role-policy-profile-manager](../../includes/minimum-rbac-role-policy-profile-manager.md)]
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
> - Deploy your [email app](./configure-email.md).
> - Create a [Windows e-mail device configuration profile](./configure-email.md).
:::column-end:::
:::row-end:::

## Email settings

- **Email server**: Enter the host name of your Exchange server. For example, enter `outlook.office365.com`.
- **Account name**: Enter the display name for the email account. This name is shown to users on their devices. For example, enter `Contoso corporate email`.
- **Username attribute from Microsoft Entra ID**: This name is the attribute Intune gets from Microsoft Entra ID. Intune dynamically generates the username that this profile uses. Your options:
  - **User Principal Name**: Gets the name, such as `user1` or `user1@contoso.com`.
  - **Primary SMTP address**: Gets the name in email address format, such as `user1@contoso.com`.
  - **sAM Account Name**: Requires the domain, such as `domain\user1`. Also enter:
    - **User domain name source**: Select **Microsoft Entra ID** or **Custom**.

      When getting the attributes from Microsoft Entra ID, also enter:
      - **User domain name attribute from Microsoft Entra ID**: Choose to get the **Full domain name** or the **NetBIOS name** Microsoft Entra attribute of the user.

      When using **Custom** attributes, also enter:
      - **Custom domain name to use**: Enter a value that Intune uses for the domain name, such as `contoso.com` or `contoso`.

- **Email address attribute from Microsoft Entra ID**: Intune gets this attribute from Microsoft Entra ID. Choose how the email address for the user is generated. Make sure your users have email addresses that match the attribute you select. Your options:
  - **User principal name**: Uses the full principal name as the email address, such as `user1@contoso.com` or `user1`.
  - **Primary SMTP address**: Uses the primary SMTP address to sign in to Exchange, such as `user1@contoso.com`.

### Security

- **SSL**: **Enable** uses Secure Sockets Layer (SSL) communication when sending emails, receiving emails, and communicating with the Exchange server. **Disable** doesn't require SSL.

### Synchronization

- **Amount of email to synchronize**: Select the number of days of email that you want to synchronize. When set to **Not configured** (default), Intune doesn't change or update this setting. Select **Unlimited** to synchronize all available email.
- **Sync schedule**: Select the schedule for devices to synchronize data from the Exchange server. You can also select **As Messages arrive**, which synchronizes data as soon as it arrives. Or, select **Manual** so the device user starts the synchronization.

  When set to **Not configured** (default), Intune doesn't change or update this setting.

### Content type to sync

Select the content types that you want to synchronize to devices. Your options:

- **Contacts**: **On** syncs the contacts. **Off** doesn't automatically sync the contacts. Users manually sync.
- **Calendar**: **On** syncs the calendar. **Off** doesn't automatically sync the contacts. Users manually sync.
- **Tasks**: **On** syncs the tasks. **Off** doesn't automatically sync the tasks. Users manually sync.

## Related articles

- Configure the email settings on [Android Enterprise](./ref-email-settings-android-enterprise.md) and [iOS/iPadOS](./ref-email-settings-ios.md).
- [Learn more about the email settings in Intune](./configure-email.md).
- [Assign the profile](../assign-device-profile.md), and [monitor its status](../monitor-device-profile.md).
