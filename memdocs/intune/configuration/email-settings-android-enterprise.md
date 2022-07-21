---
# required metadata

title: Android Enterprise email settings in Microsoft Intune
description: Create device configuration email profiles that use Exchange servers, and retrieve attributes from Azure Active Directory. Enable SSL or SMIME, authenticate users with certificates or username/password, and synchronize email and schedules on Android Enterprise personally owned devices with a work profile using Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/21/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
ms.reviewer: maholdaa
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Android Enterprise device settings to configure email, authentication, and synchronization in Intune

This article describes the different email settings you can control on Android Enterprise personally owned devices with a work profile. As part of your mobile device management (MDM) solution, use these settings to configure an Exchange email server, use SSL to encrypt emails, and more. The email profile uses the email app on the device, and allows users to connect to their organization email.

This feature applies to:

- Android Enterprise personally owned devices with a work profile (BYOD)

On Android Enterprise Fully Managed, Dedicated, and Corporate-owned Work Profiles, use [app configuration policies](../apps/app-configuration-policies-use-android.md). For Android device administrator, see [Android device settings to configure email](email-settings-android.md).

As an Intune administrator, you can create and assign email settings to Android Enterprise personally owned devices with a work profile. To learn more about email profiles in Intune, see [configure email settings](email-settings-configure.md).

## Before you begin

- Create an [Android Enterprise email device configuration profile](email-settings-configure.md) > **Personally-owned work profile**.
- Or, create an [app configuration policy](../apps/app-configuration-policies-use-android.md).
- If your profile will use Gmail and you want to use modern authentication, then you may have to deploy the Google Chrome app to the work profile.

  For more specific information, go to [Add Android store apps to Microsoft Intune](../apps/store-apps-android.md) and [Assign apps to groups with Microsoft Intune](../apps/apps-deploy.md).

## Android Enterprise

- **Email app**: Select **Gmail** or **Nine Work**. This app is the client app that connects to the email server you enter.
- **Email server**: Enter the host name of your Exchange server. For example, enter `outlook.office365.com`.
- **Username attribute from AAD**: This name is the attribute Intune gets from Azure Active Directory (Azure AD). Intune dynamically generates the username that's used by this profile. Make sure your users have email addresses that match the attribute you select. Your options:

  - **User Principal Name**: Gets the name, such as `user1` or `user1@contoso.com`.
  - **User name**: Gets only the name, such as `user1`.

- **Email address attribute from AAD**: This name is the email attribute Intune gets from Azure AD. Intune dynamically generates the email address that's used by this profile. Your options:
  - **User principal name**:  Uses the full principal name, such as `user1@contoso.com` or `user1`, as the email address.
  - **Primary SMTP address**: Uses the primary SMTP address, such as `user1@contoso.com`, to sign in to Exchange.

- **Authentication method**: Select **Username and Password** or **Certificates** as the authentication method used by the email profile.
  - If you select **Certificate**, select a client SCEP or PKCS certificate profile that you previously created to authenticate the Exchange connection.
- **SSL**: Choose **Enable** to use Secure Sockets Layer (SSL) communication when sending emails, receiving emails, and communicating with the Exchange server.
- **Amount of email to synchronize**: Choose the amount of time of email you want to synchronize. Or, select **Unlimited** to synchronize all available email.
- **Content type to sync** (Nine Work only): Choose which data you want to synchronize on the devices. Your options:
  - **Contacts**: Choose **Enable** to allow end users to sync contacts to their devices.
  - **Calendar**: Choose **Enable** to allow end users to sync the calendar to their devices.
  - **Tasks**: Choose **Enable** to allow end users to sync any tasks to their devices.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

You can also create email profiles for [Android Samsung Knox](email-settings-android.md), [iOS/iPadOS](email-settings-ios.md), and [Windows 10 and later](email-settings-windows-10.md) devices.
