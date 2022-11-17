---
# required metadata

title: Configure email settings in Microsoft Intune | Microsoft Docs
titleSuffix:
description: Create an email profile in Microsoft Intune, and deploy this profile to Android device administrator, Android Enterprise, iOS, iPadOS, and Windows devices. Use email profiles to configure common email settings, including a Microsoft Exchange email server. Add authentication methods to connect to corporate email on devices you manage.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/17/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast, japoehlm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add email settings to devices using Intune

Microsoft Intune includes different email settings you can deploy to devices in your organization. Email device configuration profiles include the connection settings used by your email app to access organization email.

Most platforms have a native or built-in email app on the device. Using Intune, you can configure the built-in email app or deploy another email app that connects to Microsoft Exchange. End users then connect, authenticate, and synchronize their organizational email accounts on their mobile devices. By creating and deploying an email profile, you can confirm settings are standard across many devices. And, help reduce support calls from end users who don't know the correct email settings.

You can use email profiles to configure the built-in email settings for the following devices:

- Android device administrator on Samsung Knox Standard 5.0 and newer
- Android Enterprise personally owned devices with a work profile
- iOS 11.0 and newer
- iPadOS 13.0 and newer
- Windows 11
- Windows 10

This article shows you how to create an email profile in Microsoft Intune. It also includes links to the different platforms for more specific settings.

## Before you begin

- Email profiles are deployed for the user who enrolled the device. To configure the email profile, Intune uses the Azure Active Directory (AD) properties in the email profile of the user during enrollment.

- Email is based on identity and user settings. Email profiles are typically assigned to user groups, not device groups. Some considerations:

  - If the email profile includes user certificates, then assign the email profile to user groups. You may have multiple user certificate profiles that are assigned. These multiple profiles create a chain of profile deployments. Deploy this profile chain to user groups.

    If one profile in this chain is deployed to a device group, users may be continuously prompted to enter their password.

  - Device groups are typically used when there's not a primary user, or if you don't know who the user will be. Email profiles targeted to device groups (not user groups) may not be delivered to the device.

    For example, your email profile targets an all iOS/iPadOS devices group. Be sure all these devices have a user.

    - If any device doesn't have a user, then the email profile may not deploy. You limit the profile, and could miss some devices.
    - If the device has a primary user, then deploying to device groups should work.

    For more information on possible issues with using device groups, see [Common issues with email profiles](/troubleshoot/mem/intune/troubleshoot-email-profiles-in-microsoft-intune).

## Choose your email app

On user devices, you decide the email apps that can connect to and access organization email. You need to determine the email apps your organization will allow, and then deploy the email app to your users.

After the email app is deployed, then you can create and deploy an email device configuration profile, if it's needed.

This section describes some of the common email apps you can use and what you need to do.

### Android Enterprise

There are two types of Android Enterprise devices:

- **Android Enterprise organization-owned devices**: These devices are owned by the organization, are enrolled in Intune, and are fully managed by you.

  These devices don't have a built-in email app.

- **Android Enterprise personally owned devices with a work profile**: These devices are owned by end users. Users enroll their devices and a work profile is automatically created. You manage the work profile, including apps and data in the work profile.

  For more information on the enrollment options for personal devices, go to [Deployment guide: Enroll Android devices in Microsoft Intune - BYOD: Android Enterprise personally owned devices with a work profile](../fundamentals/deployment-guide-enrollment-android.md#byod-android-enterprise-personally-owned-devices-with-a-work-profile).

  These personal devices have a built-in email app, but these built-in email apps aren't typically used for organization email. Organizations that use conditional access (CA) typically create CA policies to block native mail apps, or only allow specific apps.

  If you don't have CA, then users can use the built-in email app or any other personal email app to connect to organization email. They'll need to know what to enter.

On both types of Android Enterprise devices, you can add and deploy an email app that supports Microsoft Exchange. Your options:

- **Gmail**: The Gmail app is available in the managed Play Store. In Intune, you connect to your Managed Google Play account. Then, you add the Gmail app and deploy this app to your Android Enterprise devices.

  After the app is deployed, you [create an email device configuration profile](#create-the-profile) (in this article), and deploy this profile to your devices. The profile includes the settings that connect the Gmail app to your Microsoft Exchange.

  If your profile uses Gmail and you want to use modern authentication, then you may have to deploy the Google Chrome app to the work profile.

- **Nine Work**: The Nine Work app is available in the managed Play Store. In Intune, you connect to your Managed Google Play account. Then, you add the Nine Work app and deploy this app to your Android Enterprise devices.

  After the app is deployed, you [create an email device configuration profile](#create-the-profile) (in this article), and deploy this profile to your devices. The profile includes the settings that connect the Nine work app to your Microsoft Exchange.

- **Microsoft Outlook**: The Outlook app is available in the managed Play Store. If you have a Microsoft 365 license, then use the Outlook app included with your license; don't use the version in the Play Store.

  To use Outlook as the email app, you add the Outlook app, create an app configuration policy with your organization settings, and deploy this app configuration policy to your Android Enterprise devices.

  Since the Outlook app configuration policy already includes your organization settings, don't create and deploy an email device configuration profile.

  To summarize:

  ✔️ Microsoft Outlook app requires an app configuration policy on Android Enterprise  
  ✔️ Don't create an email device configuration profile

  If you don't want to customize Outlook or preconfigure it for your users, you don't have to. You still need to deploy your licensed Outlook app using an app configuration policy. After Outlook is installed, users will need to know what to enter to connect to their work or school account.

- **Other email apps**: Other enterprise level emails apps are available in the managed Play Store. Remember, they must support Microsoft Exchange.

  To use any of these other apps, you add the app, create an app configuration policy with your organization settings, and deploy this app configuration policy to your Android Enterprise devices.

  Since the app configuration policy already includes your organization settings, don't create and deploy an email device configuration profile for these app users.

  To summarize:

  ✔️ The app requires an app configuration policy on Android Enterprise  
  ✔️ Don't create an email device configuration profile

For more information on app configuration policies, go to:

- [App configuration policies in Microsoft Intune](../apps/app-configuration-policies-overview.md)
- [Add app configuration policies for managed Android Enterprise devices](../apps/app-configuration-policies-use-android.md)
- [Manage messaging collaboration access by using Outlook for iOS and Android with Microsoft Intune](../apps/app-configuration-policies-outlook.md)
- [Deploying Outlook for iOS and Android app configuration settings in Exchange Online](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

### iOS/iPadOS

In Intune, you can use organization owned devices and personally owned devices:

- **Organization owned devices**: These devices are owned by the organization, are enrolled in Intune, and are fully managed by you.

- **Personally owned devices**: These devices are owned by end users. Users can enroll their entire devices in Intune to be fully managed by you, Or, they can enroll only the apps that will access organization data.

  For more information on the enrollment options for personal devices, go to [Deployment guide: Enroll iOS and iPadOS devices in Microsoft Intune: BYOD User and Device enrollment](../fundamentals/deployment-guide-enrollment-ios-ipados.md#byod-user-and-device-enrollment).

  Depending on the enrollment method for personal devices, it's also recommended to use [app protection policies](../apps/app-protection-policy-settings-ios.md) on the email app.

On all iOS/iPadOS devices, you can add and deploy an email app that supports Microsoft Exchange ActiveSync. Your options:

- **Built-in Mail app**: This app is preinstalled with the OS and can be used to access personal email and organization email. For organization email, you need to [create an email device configuration profile](#create-the-profile) (in this article), and deploy this profile to your devices. The profile includes the settings that connect the Mail app to your Microsoft Exchange ActiveSync.

  If you don't want to use the built-in Mail app, then organizations that use conditional access (CA) typically create CA policies to block native mail apps. Or, use CA to only allow specific apps.

  If you don't have CA, then users can use the built-in email app or any other personal email app to connect to organization email. They'll need to know what to enter.

- **Microsoft Outlook**: The Outlook app is available in the App Store. If you have a Microsoft 365 license, then use the Outlook app included with your license; don't use the version in the App Store.

  To use Outlook as the email app, you add the Outlook app, create an app configuration policy with your organization settings, and deploy this app configuration policy to your iOS/iPadOS devices.

  Since the Outlook app configuration policy already includes your organization settings, don't create and deploy an email device configuration profile.

  To summarize:

  ✔️ Microsoft Outlook app requires an app configuration policy on Android Enterprise  
  ✔️ Don't create an email device configuration profile

  If you don't want to customize Outlook or preconfigure it for your users, you don't have to. You still need to deploy your licensed Outlook app using an app configuration policy. After Outlook is installed, users will need to know what to enter to connect to their work or school account.

- **Other email apps**: Other enterprise level emails apps are available the App Store. Remember, they must support Microsoft Exchange ActiveSync.

  To use any of these other apps, you add the app, create an app configuration policy with your organization settings, and deploy this app configuration policy to your iOS/iPadOS devices.

  Since the app configuration policy already includes your organization settings, don't create and deploy an email device configuration profile for these app users.

  To summarize:

  ✔️ The app requires an app configuration policy on Android Enterprise  
  ✔️ Don't create an email device configuration profile

For more information on app configuration policies, go to:

- [App configuration policies in Microsoft Intune](../apps/app-configuration-policies-overview.md)
- [Add app configuration policies for managed iOS/iPadOS devices](../apps/app-configuration-policies-use-ios.md)
- [Deploying Outlook for iOS and Android app configuration settings in Exchange Online](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

### Windows client

In Intune, you can use organization owned devices and personally owned devices:

- **Organization owned devices**: These devices are owned by the organization, are enrolled in Intune, and are fully managed by you.

- **Personally owned devices**: These devices are owned by end users. Users can enroll their entire devices in Intune to be fully managed by you.

  For more information on the enrollment options for personal devices, go to [Deployment guide: Enroll Windows devices in Microsoft Intune: BYOD: User enrollment](../fundamentals/deployment-guide-enrollment-windows.md#byod-user-enrollment).

On all Windows devices, you can add and deploy an email app that supports Microsoft Exchange. Your options:

- **Built-in Mail app**: This app is preinstalled with the OS and can be used to access personal email and organization email. For organization email, you need to [create an email device configuration profile](#create-the-profile) (in this article), and deploy this profile to your devices. The profile includes the settings that connect the Mail app to your Microsoft Exchange.

  If you don't want to use the built-in Mail app, then organizations that use conditional access (CA) typically create CA policies to block native mail apps. Or, use CA to only allow specific apps.

  If you don't have CA, then users can use the built-in email app or any other personal email app to connect to organization email. They'll need to know what to enter.

- **Microsoft Outlook**: The Outlook app is available in the Microsoft 365 Apps suite. If you have a Microsoft 365 license, then use the Outlook app included with your license; don't use the version in the Microsoft Store.

  To use Outlook as the email app, you add the Outlook app and deploy this app to your Windows devices. After the app is deployed, you [create an email device configuration profile](#create-the-profile) (in this article), and deploy this profile to your devices. The profile includes the settings that connect the Outlook app to your Microsoft Exchange.

- **Other email apps**: Other enterprise level emails apps are available in the Microsoft Store. Remember, they must support Microsoft Exchange. In Intune, you connect to your organization store of apps. Then, you add the app and deploy this app to your Windows devices.

  After the app is deployed, you [create an email device configuration profile](#create-the-profile) (in this article), and deploy this profile to your devices. The profile includes the settings that connect the email app to your Microsoft Exchange.

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Choose the platform of your devices. Your options:  

        - **Android device administrator** (Samsung Android Knox Standard only)
        - **Android Enterprise** personally owned work profiles
        - **iOS/iPadOS**
        - **Windows 10 and later**

    - **Profile**: Select **Email**. Or, select **Templates** > **Email**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **Windows 10/11: Email settings for all Windows 10/11 devices**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, depending on the platform you chose, the settings you can configure are different. Choose your platform for detailed settings:

    - [Android device administrator (Samsung Knox Standard)](email-settings-android.md)
    - [Android Enterprise](email-settings-android-enterprise.md)
    - [iOS/iPadOS](email-settings-ios.md)
    - [Windows 10/11](email-settings-windows-10.md)

8. Select **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or device groups that will receive your profile. For more information on assigning profiles, see [Before you begin](#before-you-begin) (in this article). [Assign user and device profiles](device-profile-assign.md) also some guidance.

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Remove an email profile

There are different ways to remove an email profile from devices, even when there's only one email profile on the device:

- **Option 1**: Open the email profile (**Devices** > **Configuration profiles** > select your profile), and choose **Assignments**. The **Include** tab shows the groups that are assigned the profile. Right-click the group > **Remove**. Be sure to **Save** your changes.

- **Option 2**: [Wipe or retire the device](../remote-actions/devices-wipe.md). You can use these actions to selectively or fully remove data and settings.

## Secure email access

You can help secure email profiles using the following options:

- **Certificates**: When you create the email profile, you choose a certificate profile previously created in Intune. This certificate is known as the identity certificate. It authenticates against a trusted certificate profile or a root certificate to confirm a user's device is allowed to connect. The trusted certificate is assigned to the computer that authenticates the email connection. Typically, this computer is the native mail server.

  If you use certificate-based authentication for your email profile, then deploy the email profile, certificate profile, and trusted root profile to the same groups. This deployment makes sure each device can recognize the legitimacy of your certificate authority.

  For more information about how to create and use certificate profiles in Intune, see [How to configure certificates with Intune](../protect/certificates-configure.md).

- **User name and password**: The end user authenticates to the native mail server by entering a user name and password. The password doesn't exist in the email profile. So, the end user enters the password when connecting to email.

## How Intune handles existing email accounts

If the user already configured an email account, then the email profile is assigned differently, depending on the platform.

- **Android device administrator Samsung Knox Standard**: An existing, duplicate email profile is detected based on the email address, and overwrites it with the Intune profile. Android doesn't use the host name to identify the profile. Don't create multiple email profiles using the same email address on different hosts. The profiles overwrite each other.

- **Android Enterprise personally owned work profiles**: Intune provides two Android work email apps that you can configure: Gmail and Nine Work. These apps are available in the Google Play Store, and install in the personally owned work profile. These apps don't create duplicate profiles. To use email connectivity, deploy one of these email apps to your user devices. Then, create and deploy the email profile.

  You can also use certificate profiles on Gmail and Nine Work. Any Gmail or Nine Work device configuration policies that you create continue to apply to the device. It's not necessary to move them to app configuration policies. Email apps, such as Nine Work, may not be free. Review the app's licensing details, or contact the app company with any questions.

- **iOS/iPadOS**: An existing, duplicate email profile is detected based on host name and email address. The duplicate email profile blocks the assignment of an Intune profile. In this case, the Company Portal app notifies the user that they aren't compliant, and prompts the end user to manually remove the configured profile. To help prevent this scenario, tell your end users to enroll *before* installing an email profile, which allows Intune to set up the profile.

- **Windows:** An existing, duplicate email profile is detected based on host name and email address. Intune overwrites the existing email profile created by the end user.

## Changes to assigned email profiles

If you make changes to an email profile you previously assigned, end users may see a message asking them to approve the reconfiguration of their email settings.

## Next steps

Once the profile is created, it isn't doing anything yet. Next, [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
