---
# required metadata

title: Email settings for Windows 10 devices in Microsoft Intune - Azure | Microsoft Docs
description: Create a device configuration email profile that that uses Exchange servers, and retrieves attributes from Azure Active Directory. You can also enable SSL, and synchronize email and schedules on Windows 10 devices using Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Email profile settings for devices running Windows 10 in Microsoft Intune

Use the email profile settings to configure the Mail app on your devices running Windows 10 and newer.

## Before you begin

[Create the profile](email-settings-configure.md).

## Email settings

- **Email server**: Enter the host name of your Exchange server. For example, enter `outlook.office365.com`.
- **Account name**: Enter the display name for the email account. This name is shown to users on their devices.
- **Username attribute from AAD**: This name is the attribute Intune gets from Azure Active Directory (AAD). Intune dynamically generates the username that's used by this profile. Your options:
  - **User Principal Name**: Gets the name, such as `user1` or `user1@contoso.com`.
  - **Primary SMTP address**: Gets the name in email address format, such as `user1@contoso.com`.
  - **sAM Account Name**: Requires the domain, such as `domain\user1`. Also enter:  
    - **User domain name source**: Choose **AAD** (Azure Active Directory) or **Custom**.

      When choosing to get the attributes from **AAD**, enter:
      - **User domain name attribute from AAD**: Choose to get the **Full domain name** or the **NetBIOS name** attribute of the user.

      When choosing to use **Custom** attributes, enter:
      - **Custom domain name to use**: Enter a value that Intune uses for the domain name, such as `contoso.com` or `contoso`.

- **Email address attribute from AAD**: Intune gets this attribute from Azure Active Directory (AAD). Choose how the email address for the user is generated. Your options:
  - **User principal name**: Uses the full principal name as the email address, such as `user1@contoso.com` or `user1`.
  - **Primary SMTP address**: Uses the primary SMTP address to sign in to Exchange, such as `user1@contoso.com`.

### Security

- **SSL**: **Enable** uses Secure Sockets Layer (SSL) communication when sending emails, receiving emails, and communicating with the Exchange server. **Disable** doesn't require SSL.

### Synchronization

- **Amount of email to synchronize**: Choose the number of days of email that you want to synchronize. When set to **Not configured** (default), Intune doesn't change or update this setting. Select **Unlimited** to synchronize all available email.
- **Sync schedule**: Select the schedule for devices to synchronize data from the Exchange server. You can also select **As Messages arrive**, which synchronizes data as soon as it arrives. Or, select **Manual** so the device user starts the synchronization.

### Content sync

- **Content type to sync**: Select the content types that you want to synchronize to devices:
  - **Contacts**: **On** syncs the contacts. **Off** doesn't automatically sync the contacts. Users manually sync.
  - **Calendar**: **On** syncs the calendar. **Off** doesn't automatically sync the contacts. Users manually sync.
  - **Tasks**: **On** syncs the tasks. **Off** doesn't automatically sync the tasks. Users manually sync.

## Next steps

You can also configure the email settings on [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md), and [iOS/iPadOS](email-settings-ios.md). 

[Configure email settings in Intune](email-settings-configure.md).
