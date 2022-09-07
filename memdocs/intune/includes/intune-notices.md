---
title: include file
description: include file
author: ErikjeMS  
ms.service: microsoft-intune
ms.topic: include
ms.date: 08/09/2022
ms.author: erikje
ms.custom: include file
---

These notices provide important information that can help you prepare for future Intune changes and features.  

### Plan for Change: Ending support for Windows Information Protection

Microsoft Windows [announced](https://go.microsoft.com/fwlink/?linkid=2202124) they are ending support for Windows Information Protection (WIP), Microsoft Endpoint Manager will be discontinuing future investments in managing and deploying WIP. In addition to limiting future investments, we will remove support for WIP *without enrollment* scenario by the end of calendar year 2022.

### How does this affect you or your users?

If you have enabled WIP policies, you should turn off or disable these policies.

### How can you prepare?

We recommend that you take action to disable WIP to ensure users in your organization do not lose access to documents that have been protected by WIP policy. Read the blog [Support tip: End of support guidance for Windows Information Protection](https://aka.ms/Intune-WIP-support) for more details and options for removing WIP from your devices.

### Plan for Change: Ending support for Windows 8.1 <!-- 14740233 -->

Microsoft Intune will be ending support for devices running Windows 8.1 on **October 21, 2022**. Additionally, the sideloading key scenario for line-of-business apps will stop being supported since it is only applicable to Windows 8.1 devices. 

Microsoft strongly recommends that you move to a supported version of Windows 10 or Windows 11, to avoid a scenario where you need service or support that is no longer available.

### How does this affect you or your users?

If you are managing Windows 8.1 devices those devices should be upgraded to a supported version of Windows 10 or Windows 11. There is no impact to existing devices and polices, however, you will not be able to enroll new devices if they are running Windows 8.1.

### How can you prepare?

Upgrade your Windows 8.1 devices, if applicable. To determine which users’ devices are running Windows 8.1 navigate to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows** > **Windows devices**, and filter by OS.

**Additional information**
- [Manage operating system versions with Intune](../fundamentals/manage-os-versions.md)

### Update your certificate connector for Microsoft Intune

As of June 1, 2022, Intune certificate connectors earlier than version 6.2101.13.0 may no longer work as expected and stop connecting to the Intune service. See [Certificate Connectors for Microsoft Intune](../protect/certificate-connector-overview.md) for additional information on the certificate connector lifecycle and support.

#### How does this affect you or your users?

If you're impacted by this change, see MC393815 in the Message center.

#### How can you prepare?

Download, install, and configure the latest certificate connector. For more information see, [Install the Certificate Connector for Microsoft Intune](../protect/certificate-connector-install.md).

To check which version of the certificate connector you are using follow these steps:

1. On a Windows Server running the Intune Certificate Connector, launch "Add or Remove programs".
2. A list of installed programs and applications will be displayed.
3. Look for an entry related to the Microsoft Intune Certificate Connector. There will be a "Version" associated with the connector. **Note:** Names for older connectors may vary.

### Plan for Change: New APP biometrics settings and authorization requirements for Android devices<!--9740832-->

Currently, our biometric settings do not distinguish between [Class 2 and Class 3 Biometrics](https://source.android.com/security/biometric). Expected with Intune’s July (2207) service release, we are modifying fingerprint and biometric settings for Intune app protection policies (APP) that apply to Android devices to accommodate [Class 3 Biometrics](https://developer.android.com/reference/android/hardware/biometrics/BiometricManager.Authenticators#BIOMETRIC_STRONG).

When you create or modify an app protection policy, you will see the following changes on the [Access requirements](/mem/intune/apps/app-protection-policy-settings-android#access-requirements) page:

- The setting **Fingerprint instead of PIN for access** will be rolled into the existing setting **Biometrics instead of PIN for access**. This setting will apply to all biometrics (Class 2 and Class 3).
- The setting **Override fingerprint with PIN after timeout** will be modified to **Override Biometrics with PIN after timeout**. This setting will apply to all biometrics (Class 2 and Class 3).
- There is a new setting: **Class 3 Biometrics (Android 9.0+)** with a new sub-setting: **Override Biometrics with PIN after biometric updates**. This sub-setting applies only to Class 3 Biometrics, when selected.

> [!NOTE]
> Support for Class 3 Biometrics depends on the device, so you may need to contact your device manufacturers to understand device-specific limitations.

#### How does this affect you or your users?

Existing policies that allow fingerprints or biometrics for authentication will be migrated with no user impact.

After this change, if you configure the policy to require **Class 3 Biometrics (Android 9.0+)**, the following will occur:

- For users with Android devices that support Class 3 Biometrics, the user will be prompted to enter their APP PIN the first time they sign in to the APP-protected app. Subsequent sign-ins will use Class 3 Biometrics for authentication. However, if a user does not configure biometrics that satisfy the Class 3 requirements, they will be prompted to enter their PIN with each subsequent sign-in.
- For users with Android devices that do not support Class 3 Biometrics, the user will be prompted to enter their PIN each time they sign in to the APP-protected app.

If **Override Biometrics with PIN after biometric updates** is also required, users who update their stored Class 3 Biometrics will be prompted to enter their APP PIN the next time they sign in to the APP-protected app.

#### How can you prepare?

Admins should be aware of the combined settings for fingerprints and Class 2 Biometrics. If your existing policy allows for fingerprint authentication but not other biometrics, it will allow for *both* once migrated. Also, if you had previously required an APP PIN after fingerprint timeout, this timeout setting will apply to all biometrics.

> [!NOTE]
> If you are using the Microsoft Graph API’s FingerprintBlocked and BiometricAuthenticationBlocked, plan to update your APIs to use the new combined FingerprintAndBiometricEnabled API. The current APIs will retain their values for existing policies and the new FingerprintAndBiometricEnabled API will be defaulted to Null for these policies, until the policy has been updated.

### Plan for change: Intune is moving to support macOS 11.6 and higher later this year<!--14766663-->

Apple is expected to release macOS 13 (Ventura) later this year, Microsoft Intune, the Company Portal app and the Intune mobile device management agent will be moving to support macOS 11.6 (Big Sur) and later. Since the Company Portal app for iOS and macOS are a unified app, this change will occur shortly after the release of iOS/iPadOS 16.

#### How does this affect you or your users?

This change will affect you only if you currently manage, or plan to manage, macOS devices with Intune. This change might not affect you because your users have likely already upgraded their macOS devices. For a list of supported devices, see [macOS Big Sur is compatible with these computers](https://support.apple.com/HT211238).

> [!NOTE]
> Devices that are currently enrolled on macOS 10.15 or earlier will continue to remain enrolled even when those versions are no longer supported. New devices will be unable to enroll if they are running macOS 10.15 or earlier.

#### How can you prepare?

Check your Intune reporting to see what devices or users might be affected. Go to **Devices** > **All devices** and filter by macOS. You can add more columns to help identify who in your organization has devices running macOS 10.15 or earlier. Ask your users to upgrade their devices to a supported OS version.

### Plan for change: Intune is moving to support iOS/iPadOS 14 and later<!--14778947-->

Later this year, we expect iOS 16 to be released by Apple. Microsoft Intune, including the Intune Company Portal and Intune app protection policies (APP, also known as MAM), will require [iOS 14/iPadOS 14 and higher](../fundamentals/supported-devices-browsers.md) shortly after iOS 16’s release.

#### How does this affect you or your users?

If you're managing iOS/iPadOS devices, you might have devices that won't be able to upgrade to the minimum supported version (iOS/iPadOS 14). 

Because Office 365 mobile apps are supported on iOS/iPadOS 14.0 and later, this change might not affect you. You've likely already upgraded your OS or devices. 

To check which devices support iOS 14 or iPadOS 14 (if applicable), see the following Apple documentation:

- [Supported iPhone models](https://support.apple.com/guide/iphone/supported-models-iphe3fa5df43/14.0/ios/14.0)
- [Supported iPad models](https://support.apple.com/guide/ipad/supported-models-ipad213a25b2/14.0/ipados/14.0)

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. See [https://aka.ms/ADE_userless_support](https://aka.ms/ADE_userless_support) for more information.

#### How can you prepare?

Check your Intune reporting to see what devices or users might be affected. For devices with mobile device management, go to **Devices** > **All devices** and filter by OS. For devices with app protection policies, go to **Apps** > **Monitor** > **App protection status** > **App Protection report: iOS, Android**.

To manage the supported OS version in your organization, you can use Microsoft Endpoint Manager controls for both mobile device management and APP. For more information, see [Manage operating system versions with Intune](../fundamentals/manage-os-versions.md).

### Plan for Change: Deploy macOS LOB apps by uploading PKG-type installer files<!-- 14190746 --> 
We recently announced the general availability to deploy macOS line-of-business (LOB) apps by uploading PKG-type installer files directly in the Microsoft Endpoint Manager admin center. This process no longer requires the use of the Intune App Wrapping Tool for macOS to convert *.pkg* files to *.intunemac* format. 
  
In August 2022, we removed the ability to upload wrapped *.intunemac* files in the Microsoft Endpoint Manager admin center. 

#### How does this affect you or your users?
There is no impact to apps previously uploaded with *.intunemac* files. You can upgrade previously uploaded apps by uploading the *.pkg* file type.

#### How can you prepare?
Moving forward, deploy macOS LOB apps by uploading and deploying PKG-type installer files in the Microsoft Endpoint Manager admin center. 

### Plan for change: Intune is moving to support Android 8.0 and later in January 2022<!-- 10946003 -->  

Microsoft Intune will be moving to support Android version 8.0 (Oreo) and later for mobile device management (MDM) enrolled devices on or shortly after January 7, 2022.  

#### How does this affect you or your users?

After January 7, 2022, MDM enrolled devices running Android version 7.x or earlier will no longer receive updates to the Android Company Portal or the Intune App. Enrolled devices will continue to have Intune policies applied but are no longer supported for any Intune scenarios. Company Portal and the Intune App will not be available for devices running Android 7.x and lower beginning mid-February; however, these devices will not be blocked from completing enrollment if the requisite app has been installed prior to this change. If you have MDM enrolled devices running Android 7.x or below, update them to Android version 8.0 (Oreo) or higher or replace them with a device on Android version 8.0 or higher.  

> [!NOTE]
> [Microsoft Teams devices](https://www.microsoft.com/en-us/microsoft-teams/across-devices/devices?rtc=2) are not impacted by this announcement and will continue to be supported regardless of their Android OS version.  

#### How can you prepare?  

Notify your helpdesk, if applicable, of this upcoming change in support. You can identify how many devices are currently running Android 7.x or below by navigating to **Devices** > **All devices** > **Filter**. Then filter by OS and sort by OS version. There are two admin options to help inform your users or block enrollment.

Here's how you can warn users:

- Create an app protection policy and configure [conditional launch](../apps/app-protection-policy-settings-android.md#conditional-launch) with a min OS version requirement that warns users.  
- Utilize a device compliance policy for [Android device administrator](../protect/compliance-policy-create-android.md) or [Android Enterprise](../protect/compliance-policy-create-android-for-work.md) and set the action for non-compliance to send an email or push notification to users before marking them noncompliant.  

Here's how you can block devices running on versions earlier than Android 8.0:  

- Create an app protection policy and configure conditional launch with a min OS version requirement that blocks users from app access.  
- Utilize a device compliance policy for Android device administrator or Android Enterprise to make devices running Android 7.x or earlier non-compliant. 
-  Set [enrollment restrictions](../fundamentals/manage-os-versions.md) that prevent devices running Android 7.x or earlier from enrolling.  

> [!NOTE]
> Intune app protection policies are supported on devices running Android 9.0 and later. See MC282986 for more details.  

### Plan for change: Intune APP/MAM is moving to support Android 9 and higher<!-- 10937255 -->

With the upcoming release of Android 12, Intune app protection policies (APP, also known as mobile application management) for Android will move to support Android 9 (Pie) and later on October 1, 2021. This change will align with Office mobile apps for Android support of the last four major versions of Android. 

Based on your feedback, we've updated our support statement. We're doing our best to keep your organization secure and protect your users and devices, while aligning with Microsoft app lifecycles.

> [!NOTE]
> This announcement doesn't affect [Microsoft Teams Android devices](https://www.microsoft.com/microsoft-teams/across-devices/devices?rtc=2). Those devices will continue to be supported regardless of their Android OS version.

#### How does this affect you or your users?

If you're using app protection policies (APP) on any device that's running Android version 8.x or earlier, or you decide to enroll any device that's running Android version 8.x or earlier, these devices will no longer be supported for APP. 

APP policies will continue to be applied to devices running Android 6.x to Android 8.x. But if you have problems with an Office app and APP, support will request that you update to a supported Office version for troubleshooting. To continue to receive support for APP, update your devices to Android version 9 (Pie) or later, or replace them with a device on Android version 9.0 or later before October 1, 2021.

#### How can you prepare?

Notify your helpdesk, if applicable, about this updated support statement. You also have two admin options to warn users:

- Configure a [conditional launch setting for APP](../apps/app-protection-policy-settings-android.md#conditional-launch) with a minimum OS version requirement to warn users.
- Use a device compliance policy for an [Android device administrator](../protect/compliance-policy-create-android.md) or [Android Enterprise](../protect/compliance-policy-create-android-for-work.md). Set the [action for noncompliance](../protect/actions-for-noncompliance.md) to send a message to users before marking them as noncompliant.

### Take action: Update to the latest version of the Android Company Portal app<!--10488117-->

Starting with the October (2110) service release, Intune will no longer support new Android device administrator enrollments that use Company Portal version 5.04993.0 or earlier. The reason is a change in the integration of Intune with Samsung devices.

#### How does this affect you or your users?

Users who need to enroll Samsung devices in an Android device administrator by using an older version of the Company Portal app (any version earlier than 5.04993.0) will no longer be successful. They'll need to update the Company Portal app to successfully enroll.

#### How can you prepare?

Update any older version of the Company Portal staged in your environment to support Android device administrator enrollments before the Intune October (2110) service release. Inform your users that they'll need to update to the latest version of the Android Company Portal to enroll their Samsung device. 

If applicable, inform your helpdesk in case users don't update the app before enrolling. We also recommend that you keep the Company Portal app updated to ensure that the latest fixes are available on your devices.

#### More information

- [How to update the Company Portal app](../user-help/install-a-new-version-of-the-company-portal-app.md)
- [Download the Microsoft Intune Company Portal for Android from the official Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=49140)

### Upgrade to the Microsoft Intune Management Extension<!-- 10102913 -->

We've released an upgrade to the Microsoft Intune Management Extension to improve handling of Transport Layer Security (TLS) errors on Windows 10 devices.

The new version for the Microsoft Intune Management Extension is 1.43.203.0. Intune automatically upgrades all versions of the extension that are earlier than 1.43.203.0 to this latest version. To check the version of the extension on a device, review the version for **Microsoft Intune Management Extension** in the program list under **Apps & features**.

For more information, see the information about security vulnerability CVE-2021-31980 in the [Microsoft Security Response Center](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-31980).

#### How does this affect you or your users?

No action is required. As soon as the client connects to the service, it automatically receives a message to upgrade.

### Update to Endpoint Security antivirus Windows 10 profiles<!-- 9741752   -->

We've made a minor change to improve the antivirus profile experience for Windows 10. There's no user effect, because this change affects only what you'll see in the UI.

#### How does this affect you or your users?

Previously, when you configured a [Windows security profile](../protect/antivirus-security-experience-windows-settings.md) for the Endpoint Security antivirus policy, you had two options for most settings: **Yes** and **Not configured**. Those settings now include **Yes**, **Not configured**, and a new option of **No**. 

Previously configured settings that were set to **Not configured** remain as **Not configured**. When you create new profiles or edit an existing profile, you can now explicitly specify **No**.

In addition, the setting **Hide the Virus and threat protection area in the Windows Security app** has a child setting, **Hide the Ransomware data recovery option in the Windows Security app**. If the parent setting is set to **Not configured** and the child setting is set to **Yes**, both the parent and child settings will be set to **Not configured**. That change will take effect when you edit the profile.

#### How can you prepare?

No action is needed. However, you might want to notify your helpdesk about this change.

### Plan for change: Intune is ending Company Portal support for unsupported versions of Windows

Intune follows the Windows 10 lifecycle for supported Windows 10 versions. We're now removing support for the associated Windows 10 Company Portals for Windows versions that are out of the Modern Support policy.

#### How does this affect you or your users?

Because Microsoft no longer supports these operating systems, this change might not affect you. You've likely already upgraded your OS or devices. This change will affect you only if you're still managing unsupported Windows 10 versions. 

Windows and Company Portal versions that this change affects include:

- Windows 10 version 1507, Company Portal version 10.1.721.0
- Windows 10 version 1511, Company Portal version 10.1.1731.0
- Windows 10 version 1607, Company Portal version 10.3.5601.0
- Windows 10 version 1703, Company Portal version 10.3.5601.0
- Windows 10 version 1709, any Company Portal version

We won't uninstall these Company Portal versions, but we will remove them from the Microsoft Store and stop testing our service releases with them.

If you continue to use an unsupported version of Windows 10, your users won't get the latest security updates, new features, bug fixes, latency improvements, accessibility improvements, and performance investments. You won't be able to co-manage users by using System Center Configuration Manager and Intune.

#### How can you prepare?

In the Microsoft Endpoint Manager admin center, use the [discovered apps](../apps/app-discovered-apps.md) feature to find apps with these versions. On a user's device, the Company Portal version is shown on the **Settings** page of the Company Portal. Update to a supported Windows and Company Portal version.  
