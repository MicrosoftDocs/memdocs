---
# required metadata

title: Microsoft Intune email settings for Windows Phone 8.1
titleSuffix:
description: Learn about the Intune settings you can use to configure email connections on devices running Windows Phone 8.1.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/19/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

ROBOTS: NOINDEX
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Email profile settings in Microsoft Intune for devices running Windows Phone 8.1

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

This article shows you the email profile settings you can configure for your devices running Windows Phone 8.1.

>[!IMPORTANT]
>Windows Phone 8.1 email profiles are also applied to Windows 10/11 devices.

## Before you begin

[Create a Windows Phone 8.1 email profile](email-settings-configure.md).

## Email settings

- **Email server**: Enter the host name of your Exchange server. For example, enter `outlook.office365.com`.
- **Account name**: Enter the display name for the email account. This name is shown to users on their devices.
- **Username attribute from AAD**: This name is the attribute Intune gets from Azure Active Directory (AAD). Intune dynamically generates the username that's used by this profile. Your options:
  - **User Principal Name**: Gets the name, such as `user1` or `user1@contoso.com`.
  - **Primary SMTP address**: Gets the name in email address format, such as `user1@contoso.com`.
  - **sAM Account Name**: Requires the domain, such as `domain\user1`. Also enter:
    - **User domain name source**: Your options:
      - **AAD** (Azure Active Directory): Enter **User domain name attribute from AAD**. Choose to get the **Full domain name** or the **NetBIOS name** attribute of the user.
      - **Custom**: Enter **Custom domain name to use**. Enter a value that Intune uses for the domain name, such as `contoso.com` or `contoso`.

- **Email address attribute from AAD**: Intune gets this attribute from Azure Active Directory (AAD). Choose how the email address for the user is generated. Your options:
  - **User principal name**: Uses the full principal name as the email address, such as `user1@contoso.com` or `user1`.
  - **Primary SMTP address**: Uses the primary SMTP address to sign in to Exchange, such as `user1@contoso.com`.

## Security settings

- **SSL**: **Enable** uses Secure Sockets Layer (SSL) communication when sending emails, receiving emails, and communicating with the Exchange server. **Disable** doesn't require SSL.

## Synchronization settings

- **Amount of email to synchronize**: Choose the number of days of email that you want to synchronize. When set to **Not configured** (default), Intune doesn't change or update this setting. Select **Unlimited** to synchronize all available email.
- **Sync schedule**: Select the schedule for devices to synchronize data from the Exchange server. You can also select **As Messages arrive**, which synchronizes data as soon as it arrives. Or, select **Manual** so the device user starts the synchronization.

## Content sync settings

- **Content type to sync**: Select the content types that you want to synchronize to devices:
  - **Contacts**: **On** syncs the contacts. **Off** doesn't automatically sync the contacts. Users manually sync.
  - **Calendar**: **On** syncs the calendar. **Off** doesn't automatically sync the contacts. Users manually sync.
  - **Tasks**: **On** syncs the tasks. **Off** doesn't automatically sync the tasks. Users manually sync.

## Next steps

You can also configure the email settings on [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md), [iOS/iPadOS](email-settings-ios.md), and [Windows 10/11](email-settings-windows-10.md).

[Configure email settings in Intune](email-settings-configure.md).
