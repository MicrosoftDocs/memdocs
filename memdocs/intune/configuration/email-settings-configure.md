---
# required metadata

title: Configure email settings in Microsoft Intune | Microsoft Docs
titleSuffix:
description: Create an email device configuration profile in Microsoft Intune, and deploy this profile to Android device administrator, Android Enterprise, iOS, iPadOS, and Windows devices. Use email profiles to configure common email settings, including a Microsoft Exchange email server. Add authentication methods to connect to corporate email on devices you manage.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/04/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
# optional metadata

#ROBOTS:
#audience:

ms.reviewer: sheetg
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
---

# Add email settings to devices using Intune

Microsoft Intune includes different email settings you can deploy to devices in your organization. Email device configuration profiles include the connection settings used by your email app to access organization email.

Most platforms have a native or built-in email app on the device. Using Intune, you can configure the built-in email app or deploy other email apps that connect to your email system, like Microsoft Exchange. End users then connect, authenticate, and synchronize their organizational email accounts on their devices.

By creating and deploying an email profile, you can confirm settings are standard across many devices. And, help reduce support calls from end users who don't know the correct email settings.

You can use email profiles to configure email settings for the following devices:

- Android device administrator on Samsung Knox Standard 5.0 and newer
- Android Enterprise personally owned devices with a work profile
- iOS 11.0 and newer
- iPadOS 13.0 and newer
- Windows 11
- Windows 10

This article shows you how to create an email profile in Microsoft Intune. It also includes links to the different platforms for more specific settings.

 [!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

## Before you begin

- Email profiles are deployed for the user who enrolled the device. To configure the email profile, Intune uses the Microsoft Entra properties in the email profile of the user during enrollment. The email app your organization uses must support Microsoft Entra identities.

- Email is based on identity and user settings. Email profiles are typically assigned to user groups, not device groups. Some considerations:

  - If the email profile includes user certificates, then assign the email profile to user groups. You can have multiple user certificate profiles that are assigned. These multiple profiles create a chain of profile deployments. Deploy this profile chain to user groups.

    If one profile in this chain is deployed to a device group, users can be continuously prompted to enter their password.

  - Device groups are typically used when there's not a primary user, or if you don't know who the user will be. Email profiles targeted to device groups (not user groups) might not be delivered to the device.

    For example, your email profile targets an all iOS/iPadOS devices group. Be sure all these devices have a user.

    - If any device doesn't have a user, then the email profile might not deploy. You limit the profile, and could miss some devices.
    - If the device has a primary user, then deploying to device groups should work.

    For more information on possible issues with using device groups, see [Common issues with email profiles](/troubleshoot/mem/intune/troubleshoot-email-profiles-in-microsoft-intune).

## Step 1 - Deploy your email app

On user devices, you decide the email apps that can connect to and access organization email. You also need to determine the email apps your organization allows, and then deploy the email app to your users.

After the email app is deployed, then you can create and deploy an email device configuration profile, if the profile is needed. Depending on the platform and email app you choose, you can use an app configuration policy **or** an email device configuration profile to preconfigure the email app with your organization settings.

This section describes some of the common email apps you can use, and the policy or profile type you can use for each platform.

### Android Enterprise

In Intune, you can use organization owned devices and personally owned devices:

- **Android Enterprise organization owned devices**: The organization owns these devices, they're enrolled in Intune, and are fully managed by you.

  These devices have a built-in email app that's typically hidden when the device enrolls in Intune. This behavior also depends on the OEM, so it can be different on your devices.

  The built-in email app is also considered a system app. For more information on system apps and Intune, go to [Manage Android Enterprise system apps in Microsoft Intune](../apps/apps-ae-system.md).

- **Android Enterprise personally owned devices with a work profile**: End users own these devices. Users enroll their devices and a work profile is automatically created. You manage the work profile, including apps and data in the work profile.

  For more information on the enrollment options for personal devices, go to [Deployment guide: Enroll Android devices - BYOD: Android Enterprise personally owned devices with a work profile](../fundamentals/deployment-guide-enrollment-android.md#byod-android-enterprise-personally-owned-devices-with-a-work-profile).

  These personal devices have a built-in email app that isn't typically used for organization email. Organizations that use Conditional Access (CA) can create CA policies to block native mail apps, or only allow specific apps.

#### Email app options for Android Enterprise

On both types of Android Enterprise devices, you can add and deploy an email app. Your options:

# [Outlook](#tab/outlook-android)

The **Microsoft Outlook** app is available in the managed Play Store. To use Outlook as the email app, add the Outlook app to Intune, and assign the app to your users or user groups. The app also installs.

After the app is deployed and installed:

- If you want to customize Outlook or preconfigure it with your organization settings, then you can [create an app configuration policy](../apps/app-configuration-policies-use-android.md) (opens another Microsoft article). When the policy is ready, deploy this app configuration policy to your users or user groups. App configuration policies are optional.

- If you don't want to customize Outlook or preconfigure it for your users, you don't have to. After Outlook is installed, users need to enter the information that connects to their work or school account, like the email server link and more.

# [Gmail](#tab/gmail)

The **Gmail** app is available in the managed Play Store. To use Gmail as the email app, add the Gmail app to Intune, and assign the app to your users or user groups. The app also installs.

> [!TIP]
> If your profile uses Gmail and you want to use modern authentication, then you might have to deploy the Google Chrome app to the work profile.

After the app is deployed and installed:

- On **Android Enterprise organization-owned devices**:

  - If you want to customize Gmail or preconfigure it with your organization settings, then you can [create an app configuration policy](../apps/app-configuration-policies-use-android.md) (opens another Microsoft article). When the policy is ready, deploy this app configuration policy to your users or user groups. App configuration policies are optional.

  - If you don't want to customize Gmail or preconfigure it for your users, you don't have to. After Gmail is installed, users need to enter the information that connects to their work or school account, like the email server link and more.

- On **Android Enterprise personally owned devices with a work profile**:

  - If you want to customize Gmail or preconfigure it with your organization settings, then you can [create an email device configuration profile](#step-2---create-the-profile) (in this article). When the profile is ready, deploy this email device configuration profile to your users or user groups. The profile includes the settings that connect the Gmail app to your email system, such as Microsoft Exchange. Email device configuration profiles are optional.

  - If you don't want to customize Gmail or preconfigure it for your users, you don't have to. After Gmail is installed, users need to enter the information that connects to their work or school account, like the email server link and more.

# [Nine Work](#tab/nine-work)

The **Nine Work** app is available in the managed Play Store. To use Nine Work as the email app, add the Nine Work app to Intune, and assign the app to your users or user groups. The app also installs.

After the app is deployed and installed:

- On **Android Enterprise organization-owned devices**:

  - If you want to customize Nine Work or preconfigure it with your organization settings, then you can [create an app configuration policy](../apps/app-configuration-policies-use-android.md) (opens another Microsoft article). When the policy is ready, deploy this app configuration policy to your users or user groups. App configuration policies are optional.

  - If you don't want to customize Nine Work or preconfigure it for your users, you don't have to. After Nine Work is installed, users need to enter the information that connects to their work or school account, like the email server link and more.

- On **Android Enterprise personally owned devices with a work profile**:

  - If you want to customize Nine Work or preconfigure it with your organization settings, then you can [create an email device configuration profile](#step-2---create-the-profile) (in this article). When the profile is ready, deploy this email device configuration profile to your users or user groups. The profile includes the settings that connect the Nine Work app to your email system, such as Microsoft Exchange. Email device configuration profiles are optional.

  - If you don't want to customize Nine Work or preconfigure it for your users, you don't have to. After Nine Work is installed, users need to enter the information that connects to their work or school account, like the email server link and more.

# [Other email apps](#tab/other-email-apps-android)

**Other email apps** that support Microsoft Entra identities are available in the managed Play Store. To use these email apps, add the app to Intune, and assign the app to your users or user groups. The app also installs.

After the app is deployed and installed:

- If you want to customize the app or preconfigure it with your organization settings, then you can [create an app configuration policy](../apps/app-configuration-policies-use-android.md) (opens another Microsoft article). When the policy is ready, deploy this app configuration policy to your users or user groups. App configuration policies are optional.

- If you don't want to customize the app or preconfigure it for your users, you don't have to. After the app is installed, users need to enter the information that connects to their work or school account, like the email server link and more.

---

For more information on app configuration policies, go to:

- [App configuration policies in Microsoft Intune](../apps/app-configuration-policies-overview.md)
- [Add app configuration policies for managed Android Enterprise devices](../apps/app-configuration-policies-use-android.md)
- [Manage messaging collaboration access by using Outlook for iOS and Android with Microsoft Intune](../apps/app-configuration-policies-outlook.md)
- [Deploying Outlook for iOS and Android app configuration settings in Exchange Online](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

> [!TIP]
> When you create an app configuration policy, you select the enrollment type – **Managed devices** or **Managed apps**. Be sure you know what to choose.
>
> For more information on these options, go to [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md).

### iOS/iPadOS

In Intune, you can use organization owned devices and personally owned devices:

- **Organization owned devices**: The organization owns these devices, they're enrolled in Intune, and are fully managed by you.

- **Personally owned devices**: End users own these devices. Users can enroll their entire devices in Intune to be fully managed by you. Or, they can enroll only the apps that access organization data.

  For more information on the enrollment options for personal devices, go to [Deployment guide: Enroll iOS and iPadOS devices - BYOD User and Device enrollment](../fundamentals/deployment-guide-enrollment-ios-ipados.md#byod-user-and-device-enrollment).

  Depending on the enrollment method for personal devices, it's also recommended to use [app protection policies](../apps/app-protection-policy-settings-ios.md) on the email app.

#### Email app options for iOS/iPadOS

On all iOS/iPadOS devices, you can add and deploy an email app. Your options:

# [Outlook](#tab/outlook-ios)

The **Microsoft Outlook** app is available in the App Store. To use Outlook as the email app, add the Outlook app to Intune, and assign the app to your users or user groups. The app also installs.

After the app is deployed and installed:

- If you want to customize Outlook or preconfigure it with your organization settings, then you can [create an app configuration policy](../apps/app-configuration-policies-use-ios.md) (opens another Microsoft article). When the policy is ready, deploy this app configuration policy to your users or user groups. App configuration policies are optional.

- If you don't want to customize Outlook or preconfigure it for your users, you don't have to. After Outlook is installed, users need to enter the information that connects to their work or school account, like the email server link and more.

# [Built-in Mail app](#tab/built-in-mail-app-ios)

The **Built-in Mail app** is preinstalled with the OS and can be used to access personal email and organization email. If you don't want to use the built-in Mail app, then organizations that use Conditional Access (CA) can create CA policies to block native mail apps. Or, use CA to only allow specific apps.

- If you want to customize the Mail app or preconfigure it with your organization settings, then you can [create an email device configuration profile](#step-2---create-the-profile) (in this article). When the profile is ready, deploy this email device configuration profile to your users or user groups. The profile includes the settings that connect the Mail app to your email system, such as Microsoft Exchange. Email device configuration profiles are optional.

- If you don't want to customize the Mail app or preconfigure it for your users, you don't have to. To use the Mail app for organization email, users need to enter the information that connects to their work or school account, like the email server link and more.

# [Other email apps](#tab/other-email-apps-ios)

**Other email apps** that support Microsoft Entra identities are available in the App Store. To use these email apps, add the app to Intune, and assign the app to your users or user groups. The app also installs.

After the app is deployed and installed:

- If you want to customize the app or preconfigure it with your organization settings, then you can [create an app configuration policy](../apps/app-configuration-policies-use-ios.md) (opens another Microsoft article). When the policy is ready, deploy this app configuration policy to your users or user groups. App configuration policies are optional.

- If you don't want to customize the app or preconfigure it for your users, you don't have to. After the app is installed, users need to enter the information that connects to their work or school account, like the email server link and more.

---

For more information on app configuration policies, go to:

- [App configuration policies in Microsoft Intune](../apps/app-configuration-policies-overview.md)
- [Add app configuration policies for managed iOS/iPadOS devices](../apps/app-configuration-policies-use-ios.md)
- [Deploying Outlook for iOS and Android app configuration settings in Exchange Online](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

> [!TIP]
> When you create an app configuration policy, you select the enrollment type – **Managed devices** or **Managed apps**. Be sure you know what to choose.
>
> For more information on these options, go to [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md).

### Windows client

In Intune, you can use organization owned devices and personally owned devices:

- **Organization owned devices**: The organization owns these devices, they're enrolled in Intune, and are fully managed by you.

- **Personally owned devices**: End users own these devices. Users can enroll their entire devices in Intune to be fully managed by you.

  For more information on the enrollment options for personal devices, go to [Deployment guide: Enroll Windows devices - BYOD: User enrollment](../fundamentals/deployment-guide-enrollment-windows.md#byod-user-enrollment).

#### Email app options for Windows client

On all Windows devices, you can add and deploy an email app. Your options:

# [Outlook](#tab/outlook-windows)

The **Microsoft Outlook** app is available in the Microsoft 365 Apps suite. To use Outlook as the email app, add the Outlook app to Intune, and assign the app to your users or user groups. The app also installs.

After the app is deployed and installed:

- If you want to customize Outlook or preconfigure it with your organization settings, then you can [create an email device configuration profile](#step-2---create-the-profile) (in this article). When the profile is ready, deploy this email device configuration profile to your users or user groups. The profile includes the settings that connect the Outlook app to your email system, such as Microsoft Exchange. Email device configuration profiles are optional.

- If you don't want to customize Outlook or preconfigure it for your users, you don't have to. After Outlook is installed, users need to enter the information that connects to their work or school account, like the email server link and more.

# [Built-in Mail app](#tab/built-in-mail-app-windows)

The **Built-in Mail app** is preinstalled with the OS and can be used to access personal email and organization email. If you don't want to use the built-in Mail app, then organizations that use Conditional Access (CA) can create CA policies to block native mail apps. Or, use CA to only allow specific apps.

- If you want to customize the Mail app or preconfigure it with your organization settings, then you can [create an email device configuration profile](#step-2---create-the-profile) (in this article). When the profile is ready, deploy this email device configuration profile to your users or user groups. The profile includes the settings that connect the Mail app to your email system, such as Microsoft Exchange. Email device configuration profiles are optional.

- If you don't want to customize the Mail app or preconfigure it for your users, you don't have to. To use the Mail app for organization email, users need to enter the information that connects to their work or school account, like the email server link and more.

# [Other email apps](#tab/other-email-apps-windows)

**Other email apps** that support Microsoft Entra identities are available in the Microsoft Store. To use these email apps, add the app to Intune, and assign the app to your users or user groups. The app also installs.

After the app is deployed and installed:

- If you want to customize the email app or preconfigure it with your organization settings, then you can [create an email device configuration profile](#step-2---create-the-profile) (in this article). When the profile is ready, deploy this email device configuration profile to your users or user groups. The profile includes the settings that connect the email app to your email system, such as Microsoft Exchange. Email device configuration profiles are optional.

- If you don't want to customize the app or preconfigure it for your users, you don't have to. After the app is installed, users need to enter the information that connects to their work or school account, like the email server link and more.

---

## Step 2 - Create the profile

After the email app is assigned to the device, this next step creates the device configuration policy that configures the email connection. If your email app uses an app configuration policy to configure the app, then skip this step.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select the platform of your devices. Your options:  

        - **Android device administrator** (Samsung Android Knox Standard only)
        - **Android Enterprise** personally owned work profiles
        - **iOS/iPadOS**
        - **Windows 10 and later**

    - **Profile type**: Select **Email**. Or, select **Templates** > **Email**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **Windows 10/11: Email settings for all Windows 10/11 devices**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, depending on the platform you chose, the settings you can configure are different. Select your platform for detailed settings:

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

- **Option 1**: Open the email profile (**Devices** > **Manage devices** > **Configuration** > select your profile), and select **Assignments**. The **Include** tab shows the groups that are assigned the profile. Right-click the group > **Remove**. Be sure to **Save** your changes.

- **Option 2**: [Wipe or retire the device](../remote-actions/devices-wipe.md). You can use these actions to selectively or fully remove data and settings.

## Secure email access

You can help secure email profiles using the following options:

- **Certificates**: When you create the email profile, you select a certificate profile previously created in Intune. This certificate is known as the identity certificate. It authenticates against a trusted certificate profile or a root certificate to confirm a user's device is allowed to connect. The trusted certificate is assigned to the computer that authenticates the email connection. Typically, this computer is the native mail server.

  If you use certificate-based authentication for your email profile, then deploy the email profile, certificate profile, and trusted root profile to the same groups. This deployment makes sure each device can recognize the legitimacy of your certificate authority.

  For more information about how to create and use certificate profiles in Intune, see [How to configure certificates with Intune](../protect/certificates-configure.md).

- **User name and password**: The end user authenticates to the native mail server by entering a user name and password. The password doesn't exist in the email profile. So, the end user enters the password when connecting to email.

## How Intune handles existing email accounts

If the user already configured an email account, then the email profile is assigned differently, depending on the platform.

- **Android device administrator Samsung Knox Standard**: An existing, duplicate email profile is detected based on the email address, and overwrites it with the Intune profile. Android doesn't use the host name to identify the profile. Don't create multiple email profiles using the same email address on different hosts. The profiles overwrite each other.

- **Android Enterprise personally owned work profiles**: Intune provides two Android work email apps that you can configure: Gmail and Nine Work. These apps are available in the Google Play Store, and install in the personally owned work profile. These apps don't create duplicate profiles. To use email connectivity, deploy one of these email apps to your user devices. Then, create and deploy the email profile.

  You can also use certificate profiles on Gmail and Nine Work. Any Gmail or Nine Work device configuration policies that you create continue to apply to the device. It's not necessary to move them to app configuration policies. Email apps, such as Nine Work, might not be free. Review the app's licensing details, or contact the app company with any questions.

- **iOS/iPadOS**: An existing, duplicate email profile is detected based on host name and email address. The duplicate email profile blocks the assignment of an Intune profile. In this case, the Company Portal app notifies the user that they aren't compliant, and prompts the end user to manually remove the configured profile. To help prevent this scenario, tell your end users to enroll *before* installing an email profile, which allows Intune to set up the profile.

- **Windows:** An existing, duplicate email profile is detected based on host name and email address. Intune overwrites the existing email profile created by the end user.

## Changes to assigned email profiles

If you make changes to an email profile you previously assigned, end users might see a message asking them to approve the reconfiguration of their email settings.

## Next steps

Once the profile is created, it isn't doing anything yet. Next, [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
