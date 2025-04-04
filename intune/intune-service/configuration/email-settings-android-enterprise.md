---
# required metadata

title: Android Enterprise email settings in Microsoft Intune
description: Create device configuration email profiles that use Exchange servers, and retrieve attributes from Microsoft Entra ID. Enable SSL or SMIME, authenticate users with certificates or username/password, and synchronize email and schedules on Android Enterprise personally owned devices with a work profile using Microsoft Intune.
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

ms.suite: ems
search.appverid: MET150
ms.reviewer: sheetg
#ms.tgt_pltfrm:
ms.collection:
- tier3
- M365-identity-device-management
---

# Android Enterprise device settings to configure email, authentication, and synchronization in Intune

This article describes the different email settings you can control on Android Enterprise personally owned devices with a work profile. As part of your mobile device management (MDM) solution, use these settings to configure an Exchange email server, use SSL to encrypt emails, and more. The email profile uses the email app on the device, and allows users to connect to their organization email.

This feature applies to:

- Android Enterprise personally owned devices with a work profile (BYOD)

On Android Enterprise Fully Managed, Dedicated, and Corporate-owned Work Profiles, use [app configuration policies](../apps/app-configuration-policies-use-android.md). For Android device administrator, go to [Android device settings to configure email](email-settings-android.md).

As an Intune administrator, you can create and assign email settings to Android Enterprise personally owned devices with a work profile. To learn more about email profiles in Intune, go to [configure email settings](email-settings-configure.md).

## Before you begin

- Deploy your email app. For more information, go to [Configure email apps](email-settings-configure.md).

  - If your profile uses Gmail and you want to use modern authentication, then you might have to deploy the Google Chrome app to the work profile.

- Create an [Android Enterprise email device configuration profile](email-settings-configure.md) > **Personally-owned work profile**.

## Android Enterprise

- **Email app**: Select **Gmail** or **Nine Work**. This client app connects to the email server you enter.
- **Email server**: Enter the host name of your Exchange server. For example, enter `outlook.office365.com`.
- **Username attribute from Microsoft Entra ID**: This name is the attribute Intune gets from Microsoft Entra ID. Intune dynamically generates the username that this profile uses. Make sure your users have email addresses that match the attribute you select. Your options:

  - **User Principal Name**: Gets the name, like `user1` or `user1@contoso.com`.
  - **User name**: Gets only the name, like `user1`.

- **Email address attribute from Microsoft Entra ID**: This name is the email attribute Intune gets from Microsoft Entra ID. Intune dynamically generates the email address this profile uses. Your options:
  - **User principal name**:  Uses the full principal name, like `user1@contoso.com` or `user1`, as the email address.
  - **Primary SMTP address**: Uses the primary Simple Mail Transfer Protocol (SMTP) address, like `user1@contoso.com`, to sign in to Exchange.

- **Authentication method**: Select **Username and Password** or **Certificates** as the authentication method used by the email profile.
  - If you select **Certificate**, select a client [SCEP](../protect/certificates-profile-scep.md) or [PKCS](../protect/certificates-pfx-configure.md) certificate profile that you previously created to authenticate the Exchange connection.
- **SSL**: **Enable** uses Secure Sockets Layer (SSL) communication when sending emails, receiving emails, and communicating with the Exchange server. **Disable** doesn't use SSL.
- **Amount of email to synchronize**: Select the amount of time of email you want to synchronize. Or, select **Unlimited** to synchronize all available email.
- **Content type to sync** (Nine Work only): Select the data you want to synchronize on the devices. Your options:
  - **Contacts**: **Enable** allows end users to sync contacts to their devices.
  - **Calendar**: **Enable** allows end users to sync the calendar to their devices.
  - **Tasks**: **Enable** allows end users to sync any tasks to their devices.

## Related articles

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

- Create email profiles for [Android Samsung Knox](email-settings-android.md), [iOS/iPadOS](email-settings-ios.md), and [Windows 10 and later](email-settings-windows-10.md) devices.
