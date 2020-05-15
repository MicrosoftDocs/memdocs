---
# required metadata

title: Configure email settings in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Create an email profile in Microsoft Intune, and deploy this profile to Android device administrator, Android Enterprise, iOS, iPadOS, and Windows devices. Use email profiles to configure common email settings, including an email server and authentication methods to connect to corporate email on devices you manage.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
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

# Add email settings to devices using Intune

Microsoft Intune includes different email settings you can deploy to devices in your organization. An IT administrator creates email profiles with specific settings to connect to a mail server, such as Office 365 and Gmail. End users then connect, authenticate, and synchronize their organizational email accounts on their mobile devices. By creating and deploying an email profile, you can confirm settings are standard across many devices. And, help reduce support calls from end users who don't know the correct email settings.

You can use email profiles to configure the built-in email settings for the following devices:

- Android device administrator on Samsung Knox Standard 4.0 and newer
- Android Enterprise
- iOS 8.0 and newer
- iPadOS 13.0 and newer
- Windows Phone 8.1 and newer
- Windows 10 (desktop) and Windows 10 Mobile

This article shows you how to create an email profile in Microsoft Intune. It also includes links to the different platforms for more specific settings.

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Choose the platform of your devices. Your options:  

        - **Android device administrator** (Samsung Android Knox Standard only)
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **Windows 10 and later**
        - **Windows Phone 8.1**

    - **Profile**: Select **Email**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **Windows 10: Email settings for all Windows 10 devices**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, depending on the platform you chose, the settings you can configure are different. Choose your platform for detailed settings:

    - [Android device administrator (Samsung Knox Standard)](email-settings-android.md)
    - [Android Enterprise](email-settings-android-enterprise.md)
    - [iOS/iPadOS](email-settings-ios.md)
    - [Windows 10](email-settings-windows-10.md)
    - [Windows Phone 8.1](email-settings-windows-phone-8-1.md)

8. Select **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Remove an email profile

Email profiles are assigned to device groups, not user groups. There are different ways to remove an email profile from a device, even when there's only one email profile on the device:

- **Option 1**: Open the email profile (**Devices** > **Configuration profiles** > select your profile), and choose **Assignments**. The **Include** tab shows the groups that are assigned the profile. Right-click the group > **Remove**. Be sure to **Save** your changes.

- **Option 2**: [Wipe or retire the device](../remote-actions/devices-wipe.md). You can use these actions to selectively or fully remove data and settings.

## Secure email access

You can help secure email profiles using the following options:

- **Certificates**: When you create the email profile, you choose a certificate profile previously created in Intune. This certificate is known as the identity certificate. It authenticates against a trusted certificate profile or a root certificate to confirm a user's device is allowed to connect. The trusted certificate is assigned to the computer that authenticates the email connection. Typically, this computer is the native mail server.

  If you use certificate based authentication for your email profile, deploy the email profile, certificate profile, and trusted root profile to the same groups to ensure that each device can recognize the legitimacy of your certificate authority.

  For more information about how to create and use certificate profiles in Intune, see [How to configure certificates with Intune](../protect/certificates-configure.md).

- **User name and password**: The end user authenticates to the native mail server by entering a user name and password. The password doesn't exist in the email profile. So, the end user enters the password when connecting to email.

## How Intune handles existing email accounts

If the user already configured an email account, then the email profile is assigned differently, depending on the platform.

- **iOS/iPadOS**: An existing, duplicate email profile is detected based on host name and email address. The duplicate email profile blocks the assignment of an Intune profile. In this case, the Company Portal app notifies the user that they aren't compliant, and prompts the end user to manually remove the configured profile. To help prevent this scenario, tell your end users to enroll *before* installing an email profile, which allows Intune to set up the profile.

- **Windows:** An existing, duplicate email profile is detected based on host name and email address. Intune overwrites the existing email profile created by the end user.

- **Android Samsung Knox Standard**: An existing, duplicate email profile is detected based on the email address, and overwrites it with the Intune profile. Android doesn't use host name to identify the profile. Don't create multiple email profiles using the same email address on different hosts. The profiles overwrite each other.

- **Android work profiles**: Intune provides two Android work email profiles: one for the Gmail app, and one for the Nine Work app. These apps are available in the Google Play Store, and install in the device work profile. These apps don't create duplicate profiles. Both apps support connections to Exchange. To use email connectivity, deploy one of these email apps to your users' devices. Then create and deploy the appropriate email profile. You can use Gmail and Nine email configuration profiles that will work for both Work Profile and Device Owner enrollment types, including the use of certificate profiles on both email configuration types. Any Gmail or Nine policies that you have created under Device Configuration for Work Profiles will continue to apply to the device and it is not necessary to move them to app configuration policies. Email apps such as Nine Work may not be free. Review the app's licensing details, or contact the app company with any questions. 

## Changes to assigned email profiles

If you make changes to an email profile you previously assigned, end users may see a message asking them to approve the reconfiguration of their email settings.

## Next steps

Once the profile is created, it isn't doing anything yet. Next, [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
