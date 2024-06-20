---
# required metadata

title: Email settings for Windows 10/11 devices in Microsoft Intune
description: Create a device configuration email profile that that uses Exchange servers, and retrieves attributes from Microsoft Entra ID. You can also enable SSL, and synchronize email and schedules on Windows 10/11 client devices using Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/15/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: sheetg
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
---

# Email profile settings for devices running Windows 10/11 in Microsoft Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

In Microsoft Intune, you can create and configure email to connect to an Exchange email server, choose how users authenticate, use S/MIME for encryption, and more. The email profile uses the native or built-in email app on the device, and allows users to connect to their organization email.

This feature applies to:

- Windows 11
- Windows 10

This article describes some of the settings you can configure. You can create a device configuration profile to assign or deploy these email settings to your iOS/iPadOS devices.

## Before you begin

- Deploy your email app. For more information, go to [Configure email apps](email-settings-configure.md).
- Create a [Windows 10/11 Email device configuration profile](email-settings-configure.md).

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

- Configure the email settings on [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md), and [iOS/iPadOS](email-settings-ios.md).

- [Learn more about the email settings in Intune](email-settings-configure.md).

- [Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).
