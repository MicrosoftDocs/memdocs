---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 07/31/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals

# optional metadata

#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. Also:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description will move from this article to [What's new](whats-new.md).  
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](whats-new.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Tenant administration
## Notices
-->

<!-- ***********************************************-->

## App management  

### New macOS web clip app type<!-- 24128407 -->
In Intune, you will be able to pin web apps to the dock on your macOS devices (**Apps** > **macOS** > **Add** > **macOS web clip**). For related information about the settings you can currently configure, go to [Add web apps to Microsoft Intune](../apps/web-app.md).  

Applies to:
- macOS

### Samsung Knox conditional launch check<!-- 8610063  -->  
Administrators will be able to add additional detection of device health compromise on Samsung Knox devices. Using a new Intune App Protection Policy conditional launch check, you will be able to require that hardware-level device tamper detection and device attestation be performed for compatible Samsung devices.

### Intune migrating from SafetyNet Attestation API to Google Play Integrity API<!-- 15571389   -->  
Google has deprecated the [SafetyNet Attestation API](https://developer.android.com/training/safetynet/attestation) and replaced it with the [Play Integrity API](https://developer.android.com/google/play/integrity). Intune will be migrating to the new API for app protection policies. The "SafetyNet device attestation" setting name will be updated to align with the new Google Play Integrity API for all policies in the Intune user interface (UI). For related information, see [Discontinuing the SafetyNet Attestation API](https://developer.android.com/training/safetynet/deprecation-timeline) and [Migrating from the SafetyNet Attestation API](https://developer.android.com/google/play/integrity/migrate).

### Advanced application management<!-- 10986080  -->  
Advanced application management provides you with an enterprise catalog of applications that are easily accessible. It also provides application update capabilities. The enterprise catalog is planned to be available in public preview in late Q2 2023. The application update capabilities are planned to be available in early Q3 2023.

### Company Portal automatically installed on Android Enterprise dedicated devices<!-- 6423852  -->  
Intune Company Portal will now be automatically installed on all Android Enterprise dedicated devices to ensure the appropriate handling of app protection policies. Users won't be able to see or launch the Company Portal, and there are no requirements for users to interact with it. Admins will notice that the Company Portal is automatically installed on their Android Enterprise dedicated devices, without the ability to uninstall.

### Support for multi-SIM iOS/iPadOS device inventory<!--17016690 (replaced 16360290 for tracking -->

You'll be able to view the service subscription fields on devices that have multiple SIM cards installed under the per-device Hardware section. The inventory fields that are capable of reporting multiple values to Intune are:

- **ICCID**
- **IMEI**
- **MEID**
- **Phone number**

These fields will default to using labels returned by the device, such as:  *Primary*, *Secondary*, *CTSubscriptionSlotOne*, and *CTSubscriptionSlotTwo*. These returned labels may be displayed in the language of the local device that is reporting its inventory to Intune.

Applies to:

- **iOS/iPadOS**

### Uninstall Win32 and Microsoft store apps using the Windows Company Portal<!-- 4664389  -->  
End-users will soon be able to  uninstall Win32 apps and Microsoft store apps using the Windows Company Portal if the apps were assigned as available and were installed on-demand by the end-users. For Win32 apps, you have the option to enable or disable this feature (off by default). For Microsoft store apps, it is always on and available for your end-users. If an app can be uninstalled by the end-user, the end-user will be able to select **Uninstall** for the app in the Windows Company Portal. For related information, see [Add apps to Microsoft Intune](../apps/apps-add.md).

<!-- *********************************************** -->

## Device configuration  

### New SSO, login, restrictions, passcode, and tamper protection settings available in the Apple settings catalog<!-- 24335541 -->

A range of new settings will be available in the Settings Catalog for iOS/iPadOS and macOS. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you'll be able to see these settings at **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** > **Settings catalog** for profile type.  

**Authentication > Extensible Single Sign On (SSO)**:

- Account Display Name
- Additional Groups
- Administrator Groups
- Authentication Method
- Authorization Right
- Group
- Authorization Group
- Enable Authorization
- Enable Create User At Login
- Login Frequency
- New User Authorization Mode
- Account Name
- Full Name
- Token To User Mapping
- User Authorization Mode
- Use Shared Device Keys

Applies to:
- macOS 13.0 and later

**Login > Login Window**:

- Autologin Password
- Autologin Username

**Restrictions**:

- Allow ARD Remote Management Modification
- Allow Bluetooth Sharing Modification
- Allow Cloud Freeform
- Allow File Sharing Modification
- Allow Internet Sharing Modification
- Allow Local User Creation
- Allow Printer Sharing Modification
- Allow Remote Apple Events Modification
- Allow Startup Disk Modification
- Allow Time Machine Backup

**Security > Passcode**:

- Password Content Description
- Password Content Regex

Applies to:
- macOS 14.0 and later

**Restrictions**:

- Allow iPhone Widgets On Mac

Applies to:
- iOS/iPadOS 17.0 and later

**Microsoft Defender > Tamper protection**:

- Process's arguments
- Process path
- Process's Signing Identifier
- Process's Team Identifier
- Process exclusions

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Remote Help for Android in public preview <!-- 16238217 -->
Remote Help will be available in public preview for Android Enterprise Dedicated devices from Zebra and Samsung. With Remote Help, IT Pros can remotely view the device screen and take full control in both attended and unattended scenarios, to diagnose and resolve issues quickly and efficiently.

Applies to:

* Android Enterprise Dedicated devices, manufactured by Zebra or Samsung

<!-- *********************************************** -->

## Device enrollment

### Just-in-time registration and compliance remediation for iOS/iPadOS Setup Assistant with modern authentication becoming generally available<!-- 16276610  -->  
Just-in-time registration and compliance remediation for Setup Assistant with modern authentication will become generally available. With just-in-time (JIT) registration, the device user doesn't need to use the Company Portal app for Azure Active Directory registration and compliance checking. JIT registration and compliance remediation is embedded into the user's provisioning experience, so they can view their compliance status and take action within the work app they're trying to access. Additionally, this establishes single-sign on across the device. For more information about how to set up JIT registration, see [Set up Just in Time Registration](../enrollment/automated-device-enrollment-authentication.md#set-up-just-in-time-registration).

### Awaiting final configuration for iOS/iPadOS automated device enrollment becoming generally available<!-- 17473384  -->  
Soon to be generally available, awaiting final configuration enables a locked experience at the end of Setup Assistant to ensure that critical device configuration policies install on devices. The locked experience works on devices targeted with new and existing enrollment profiles. Supported devices include:

- iOS/iPadOS 13+ devices enrolling with Setup Assistant with modern authentication  

- iOS/iPadOS 13+ devices enrolling without user affinity
- iOS/iPadOS 13+ devices enrolling with Azure AD shared mode

This setting is applied once during the out-of-box automated device enrollment experience in Setup Assistant. The device user doesn't experience it again unless they re-enroll their device. Awaiting final configuration is enabled by default for new enrollment profiles. For more information about how to enable awaiting final configuration, see [Create an Apple enrollment profile](..//enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

<!-- *********************************************** -->

## Device management

### Intune will support iOS/iPadOS 15.x as the minimum version<!-- 24161619  -->  
Later this year, Apple is expected to release iOS/iPadOS version 17. After the release of iOS/iPadOS 17, the minimum version supported by Intune will be iOS/iPadOS 15.x.

For more information on this change, go to [Plan for change: Intune is moving to support iOS/iPadOS 15 and later](whats-new.md#plan-for-change-intune-is-moving-to-support-iosipados-15-and-later).

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, go to [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

Applies to:

- iOS/iPadOS

### Changes to Android notification permission prompt behavior<--! 19783177  -->  
We're updating how our Android apps handle notification permissions to align with recent changes made by Google to the Android platform.  After their changes, notification permissions are granted to apps as follows:

- On devices running Android 12 and earlier: Apps are permitted to send notifications to users by default.
- On devices running Android 13 and later: Notification permissions vary depending on the API the app targets.
  - Apps targeting API 32 and lower: Google has added a notification permission prompt that appears when the user opens the app. Management apps will still be able to configure apps so that they're automatically granted notification permissions.
  - Apps targeting API 33 and higher: App developers define when the notification permission prompts appear. Management apps will still be able to configure apps so that they're automatically granted notification permissions.

You and your device users can expect to see the following changes now that our apps target API 33:

- Company Portal used for work profile management: Users will see a notification permission prompt in the personal instance of the Company Portal when they first open it. Users will not see a notification permission prompt in the work profile instance of Company Portal because notification permissions will be automatically permitted. Users will be able to turn off Company Portal notifications in the Settings app.
- Company Portal used for device administrator management: Users will see a notification permission prompt when they first open the Company Portal app.
- Microsoft Intune app: No changes to existing behavior. Users will not see a prompt because notifications are automatically permitted.
- Microsoft Intune app for AOSP: No changes to existing behavior. Users will not see a prompt because notifications are automatically permitted.

<!-- *********************************************** -->

## Device security  
### New settings available for macOS Antivirus policy<!-- 24191427 -->  

The [Microsoft Defender Antivirus](../protect/endpoint-security-antivirus-policy.md) profile for macOS devices will be getting several new settings. The new settings will add capabilities to manage:

- Running scans after definitions are updated
- Turning on-demand scans of archives on or off
- Turning the file hash computation on or off
- Tamper protection for macOS
- device Visibility of the status menu icon
- Visibility of the feedback option
- Network protection
- Controlling sign-in to the consumer version of Microsoft Defender

For more information about how to set preferences for Microsoft Defender for Endpoint on macOS in enterprise organizations, see [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences?view=o365-worldwide).  
## Monitor and troubleshoot  
### Anomaly correlation in Intune Endpoint analytics will be generally available <!-- 24577118 -->

Anomaly correlation, a part of our Anomaly detection feature in Intune Endpoint analytics will be generally available.  

Devices associated with a high or medium severity anomaly are correlated into groups based on one or more factors they have in common.  A correlation group will contain a detailed view with key information about the common factors between all affected devices in that group. You will also be able to view a breakdown of devices currently affected by the anomaly and 'at risk' devices, those that haven't yet shown symptoms of the anomaly.

### Updates for compliance policies and reports<!-- 15425771  -->  
We’re working on the improvements for Intune compliance policies and reports which include the following:

- Adding support for Linux
- Providing more up-to-date and simplified reporting experience for the policy Overview.
- Aligning the policy report experience with the experience for device configuration profiles.

For more information about these changes, see the Intune Support Team blog at [https://aka.ms/Intune/device_compl_report](https://aka.ms/Intune/device_compl_report).  

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->
<!-- *********************************************** --> 

<!-- ## Tenant administration -->
<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
