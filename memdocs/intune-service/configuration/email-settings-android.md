---
# required metadata

title: Android email settings in Microsoft Intune
description: Create device configuration email profiles that use Exchange servers, and retrieve attributes from Microsoft Entra ID. Enable SSL or SMIME, authenticate users with certificates or username/password, and synchronize email and schedules on Android Samsung Knox devices using Microsoft Intune.
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
ms.collection:
- tier3
- M365-identity-device-management
---

# Android device settings to configure email, authentication, and synchronization in Intune

This article describes the different email settings you can control on Android Samsung Knox devices in Intune. As part of your mobile device management (MDM) solution, use these settings to configure an Exchange email server, use SSL to encrypt emails, and more. The email profile uses the native or built-in email app on the device, and allows users to connect to their organization email.

This feature applies to:

- Android device administrator (DA)

As an Intune administrator, you can create and assign email settings to Android Samsung Knox Standard devices. To learn more about email profiles in Intune, go to [configure email settings](email-settings-configure.md).

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

## Before you begin

- Create an [Android device administrator Email device configuration profile](email-settings-configure.md).

## Android (Samsung Knox)

- **Email server**: Enter the host name of your Exchange server. For example, enter `outlook.office365.com`.
- **Account name**: Enter the display name for the email account. This name is shown to users on their devices.
- **Username attribute from Microsoft Entra ID**: This name is the attribute Intune gets from Microsoft Entra ID. Intune dynamically generates the username that this profile uses. Your options:
  - **User principal name**: Gets the name, like `user1` or `user1@contoso.com`.
  - **User name**: Gets only the name, like `user1`.
  - **sAM Account Name**: Requires the domain, like `domain\user1`. sAM account name is only used with Android devices. Also enter:  
    - **User domain name source**: Select **Microsoft Entra ID** or **Custom**.

      When choosing to get the attributes from Microsoft Entra ID, enter:
      - **User domain name attribute from Microsoft Entra ID**: Select to get the **Full domain name** or the **NetBIOS name** attribute of the user.

      When choosing to use **Custom** attributes, enter:
      - **Custom domain name to use**: Enter a value that Intune uses for the domain name, like `contoso.com` or `contoso`.

- **Email address attribute from Microsoft Entra ID**: This name is the email attribute Intune gets from Microsoft Entra ID. Intune dynamically generates the email address that this profile uses. Make sure your users have email addresses that match the attribute you select. Your options:
  - **User principal name**: Uses the full principal name, like `user1@contoso.com` or `user1`, as the email address.
  - **Primary SMTP address**: Uses the primary Simple Mail Transfer Protocol (SMTP) address, like `user1@contoso.com`, to sign in to Exchange.

- **Authentication method**: Select **Username and Password** or **Certificate** as the authentication method used by the email profile.
  - If you select **Certificate**, select a client [SCEP](../protect/certificates-profile-scep.md) or [PKCS](../protect/certificates-pfx-configure.md) certificate profile that you previously created to authenticate the Exchange connection.

### Security settings

- **SSL**: **Enable** uses Secure Sockets Layer (SSL) communication when sending emails, receiving emails, and communicating with the Exchange server. **Disable** does use SSL.
- **S/MIME**: **Disable S/MIME** (default): Doesn't use an S/MIME email certificate to sign, encrypt, or decrypt emails. **Enable S/MIME** sends outgoing email using S/MIME encryption. Also enter:
  - Select a client [SCEP](../protect/certificates-profile-scep.md) or [PKCS](../protect/certificates-pfx-configure.md) certificate profile that you previously created to authenticate the Exchange connection.

### Synchronization settings

- **Amount of email to synchronize**: Select the number of days of email that you want to synchronize, or select **Unlimited** to synchronize all available email.
- **Sync schedule**: Select the schedule for devices to synchronize data from the Exchange server. You can also select **As Messages arrive**, which synchronizes data when it arrives, or **Manual**, where the user of the device must initiate the synchronization.

### Content type to sync

Select the content types that you want to synchronize on the devices.

**Not configured** disables the setting. When set to **Not configured**, if an end user enables synchronization on the device, synchronization is disabled again when the device syncs with Intune, as the policy is reinforced.

- **Contacts**: **Enable** allows end users to sync contacts to their devices.
- **Calendar**: **Enable** allows end users to sync the calendar to their devices.
- **Tasks**: **Enable** allows end users to sync any tasks to their devices.

## Related articles

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

- Create email profiles for [Android Enterprise](email-settings-android-enterprise.md), [iOS/iPadOS](email-settings-ios.md), and [Windows 10 and later](email-settings-windows-10.md).
