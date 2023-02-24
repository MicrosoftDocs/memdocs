---
# required metadata

title: Android email settings in Microsoft Intune
description: Create device configuration email profiles that use Exchange servers, and retrieve attributes from Azure Active Directory. Enable SSL or SMIME, authenticate users with certificates or username/password, and synchronize email and schedules on Android Samsung Knox devices using Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/07/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection:
- tier3
- M365-identity-device-management
---

# Android device settings to configure email, authentication, and synchronization in Intune

This article describes the different email settings you can control on Android Samsung Knox devices in Intune. As part of your mobile device management (MDM) solution, use these settings to configure an Exchange email server, use SSL to encrypt emails, and more. The email profile uses the native or built-in email app on the device, and allows users to connect to their organization email.

This feature applies to:

- Android device administrator (DA)

As an Intune administrator, you can create and assign email settings to Android Samsung Knox Standard devices. To learn more about email profiles in Intune, see [configure email settings](email-settings-configure.md).

## Before you begin

Create an [Android device administrator Email device configuration profile](email-settings-configure.md).

## Android (Samsung Knox)

- **Email server**: Enter the host name of your Exchange server. For example, enter `outlook.office365.com`.
- **Account name**: Enter the display name for the email account. This name is shown to users on their devices.
- **Username attribute from AAD**: This name is the attribute Intune gets from Azure Active Directory (Azure AD). Intune dynamically generates the username that's used by this profile. Your options:
  - **User Principal Name**: Gets the name, such as `user1` or `user1@contoso.com`.
  - **User name**: Gets only the name, such as `user1`.
  - **sAM Account Name**: Requires the domain, such as `domain\user1`. sAM account name is only used with Android devices. Also enter:  
    - **User domain name source**: Choose **AAD** (Azure Active Directory) or **Custom**.

      When choosing to get the attributes from **AAD**, enter:
      - **User domain name attribute from AAD**: Choose to get the **Full domain name** or the **NetBIOS name** attribute of the user.

      When choosing to use **Custom** attributes, enter:
      - **Custom domain name to use**: Enter a value that Intune uses for the domain name, such as `contoso.com` or `contoso`.

- **Email address attribute from AAD**: This name is the email attribute Intune gets from Azure AD. Intune dynamically generates the email address that's used by this profile. Make sure your users have email addresses that match the attribute you select. Your options:
  - **User principal name**: Uses the full principal name, such as `user1@contoso.com` or `user1`, as the email address.
  - **Primary SMTP address**: Uses the primary SMTP address, such as `user1@contoso.com`, to sign in to Exchange.

- **Authentication method**: Select either **Username and Password** or **Certificates** as the authentication method used by the email profile.
  - If you select **Certificate**, select a client SCEP or PKCS certificate profile that you previously created to authenticate the Exchange connection.

### Security settings

- **SSL**: Use Secure Sockets Layer (SSL) communication when sending emails, receiving emails, and communicating with the Exchange server.
- **S/MIME**: Send outgoing email using S/MIME encryption.
  - If you select **Certificate**, select a client SCEP or PKCS certificate profile that you previously created to authenticate the Exchange connection.

### Synchronization settings

- **Amount of email to synchronize**: Choose the number of days of email that you want to synchronize, or select **Unlimited** to synchronize all available email.
- **Sync schedule**: Select the schedule for devices to synchronize data from the Exchange server. You can also select **As Messages arrive**, which synchronizes data when it arrives, or **Manual**, where the user of the device must initiate the synchronization.

### Content sync settings

- **Content type to sync**: Select the content types that you want to synchronize on the devices. **Not configured** disables this setting. When set to **Not configured**, if an end user enables synchronization on the device, synchronization is disabled again when the device syncs with Intune, as the policy is reinforced. 

  You can sync the following content:  
  - **Contacts**: Choose **Enable** to allow end users to sync contacts to their devices.
  - **Calendar**: Choose **Enable** to allow end users to sync the calendar to their devices.
  - **Tasks**: Choose **Enable** to allow end users to sync any tasks to their devices.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

You can also create email profiles for [Android Enterprise](email-settings-android-enterprise.md), [iOS/iPadOS](email-settings-ios.md), and [Windows 10 and later](email-settings-windows-10.md).
