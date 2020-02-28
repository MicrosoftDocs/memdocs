---
# required metadata

title: Configure email settings in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Create an email profile in Microsoft Intune, and deploy this profile to Android Enterprise, iOS, iPadOS, and Windows devices. Use an email profile to configure common email settings, including an email server and authentication method to connect to corporate email on devices you manage.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add email settings to devices using Intune

Microsoft Intune includes different email settings you can deploy to devices in your organization. An IT administrator creates email profiles with specific settings to connect to a mail server, such as Office 365 and Gmail. End users then connect, authenticate, and synchronize their organizational email accounts on their mobile devices. By creating and deploying an email profile, you can confirm settings are standard across many devices. And, help reduce support calls from end users who don't know the correct email settings.

You can use email profiles to configure the built-in email settings for the following devices:

- Android Samsung Knox Standard 4.0 and newer
- Android Enterprise
- iOS 8.0 and newer
- iPadOS 13.0 and newer
- Windows Phone 8.1 and newer
- Windows 10 (desktop) and Windows 10 Mobile

This article shows you how to create an email profile in Microsoft Intune. It also includes links to the different platforms for more specific settings.

## Create a device profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **Email settings for all Windows devices**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
    - **Platform**: Choose the platform of your devices. Your options:

        - **Android** (Samsung Android Knox Standard only)
        - **Android enterprise**
        - **iOS/iPadOS**
        - **Windows Phone 8.1**
        - **Windows 10 and later**

    - **Profile type**: Select **Email**.

4. Depending on the platform you chose, the settings you can configure are different. Choose your platform for detailed settings:

    - [Android Samsung Knox Standard settings](../email-settings-android.md)
    - [Android Enterprise settings](../email-settings-android-enterprise.md)
    - [iOS/iPadOS settings](email-settings-ios.md)
    - [Windows Phone 8.1 settings](email-settings-windows-phone-8-1.md)
    - [Windows 10 settings](email-settings-windows-10.md)

5. When you're done, select **OK** > **Create** to save your changes.

After you enter your settings, and create the profile, your profile is shown in the profiles list. Next, [assign this profile to some groups](../device-profile-assign.md).

## Remove an email profile

Email profiles are assigned to device groups, not user groups. There are different ways to remove an email profile from a device, even when there's only one email profile on the device:

- **Option 1**: Open the email profile (**Devices** > **Configuration profiles** > select your profile), and choose **Assignments**. The **Include** tab shows the groups that are assigned the profile. Right-click the group > **Remove**. Be sure to **Save** your changes.

- **Option 2**: [Wipe or retire the device](../remote-actions/devices-wipe.md). You can use these actions to selectively or fully remove data and settings.

## Secure email access

You can help secure email profiles using the following options:

- **Certificates**: When you create the email profile, you choose a certificate profile previously created in Intune. This certificate is known as the identity certificate. It authenticates against a trusted certificate profile or a root certificate to confirm a user’s device is allowed to connect. The trusted certificate is assigned to the computer that authenticates the email connection. Typically, this computer is the native mail server.

  For more information about how to create and use certificate profiles in Intune, see [How to configure certificates with Intune](../protect/certificates-configure.md).

- **User name and password**: The end user authenticates to the native mail server by entering a user name and password. The password doesn't exist in the email profile. So, the end user enters the password when connecting to email.

## How Intune handles existing email accounts

If the user already configured an email account, then the email profile is assigned differently, depending on the platform.

- **iOS/iPadOS**: An existing, duplicate email profile is detected based on host name and email address. The duplicate email profile blocks the assignment of an Intune profile. In this case, the Company Portal app notifies the user that they aren't compliant, and prompts the end user to manually remove the configured profile. To help prevent this scenario, tell your end users to enroll *before* installing an email profile, which allows Intune to set up the profile.

- **Windows:** An existing, duplicate email profile is detected based on host name and email address. Intune overwrites the existing email profile created by the end user.

- **Android Samsung Knox Standard**: An existing, duplicate email profile is detected based on the email address, and overwrites it with the Intune profile. Android doesn't use host name to identify the profile. Don't create multiple email profiles using the same email address on different hosts. The profiles overwrite each other.

- **Android work profiles**: Intune provides two Android work email profiles: one for the Gmail app, and one for the Nine Work app. These apps are available in the Google Play Store, and install in the device work profile. These apps don't create duplicate profiles. Both apps support connections to Exchange. To use email connectivity, deploy one of these email apps to your users' devices. Then create and deploy the appropriate email profile. Email apps such as Nine Work may not be free. Review the app’s licensing details, or contact the app company with any questions.

## Changes to assigned email profiles

If you make changes to an email profile you previously assigned, end users may see a message asking them to approve the reconfiguration of their email settings.

## Next steps

Once the profile is created, it isn't doing anything yet. Next, [assign the profile](../device-profile-assign.md).
