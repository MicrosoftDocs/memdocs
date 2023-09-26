---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 09/27/2023
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

### Minimum SDK version warning for iOS devices<!-- 9410239  -->  
The **Min SDK version** for the iOS Conditional Launch setting on iOS devices will include a warn action. This action will warn end users if the min SDK version requirement is not met.

### Minimum OS for Apple line-of-business apps<!-- 24623225  -->  
You will soon be able to configure the minimum operating system for Apple line-of-business and iOS/iPadOS store apps to the latest Apple OS releases. You can set iOS/iPadOS 17.0 and macOS 14.0 as minimum OS for Apple line-of-business apps and iOS/iPadOS 17.0 as a minimum OS for iOS/iPadOS store apps.

Applies to:

- iOS/iPadOS
- macOS

### Android (AOSP) supports line-of-business (LOB) apps<!-- 24823138  -->  
You will soon be able to install and uninstall mandatory LOB apps on AOSP devices by using the **Required** and **Uninstall** group assignments. To learn more about managing LOB apps, see [Add an Android line-of-business app to Microsoft Intune](../apps/lob-apps-android.md).

Applies to:

- Android

### Update for users of Android Company Portal app<!-- 25109006  -->  
If users launch a version of the Android Company Portal app below 5.0.5333.0 (released November 2021), they will see a prompt encouraging them to update their Android Company Portal app. If a user with an older Android Company Portal version attempts a new device registration using a recent version of the Authenticator app, the process will likely fail. The way to resolve this is to update the Android Company Portal app.

### Intune migrating from SafetyNet Attestation API to Google Play Integrity API<!-- 15571389   -->  
Google has deprecated the [SafetyNet Attestation API](https://developer.android.com/training/safetynet/attestation) and replaced it with the [Play Integrity API](https://developer.android.com/google/play/integrity). Intune will be migrating to the new API for app protection policies. The "SafetyNet device attestation" setting name will be updated to align with the new Google Play Integrity API for all policies in the Intune user interface (UI). For related information, see [Discontinuing the SafetyNet Attestation API](https://developer.android.com/training/safetynet/deprecation-timeline) and [Migrating from the SafetyNet Attestation API](https://developer.android.com/google/play/integrity/migrate).

### Enterprise application management<!-- 10986080  -->  
Enterprise Application Management provides a catalog of prepackaged applications designed to simplify discovery, delivery, and updates for third and first party apps. Enterprise Application Management will be generally available in early Q1 2024.

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

<!-- *********************************************** -->

## Device configuration

### New device configuration settings that configure enhanced permissions to apps on Android Enterprise devices<!-- 14029609  -->  
In Intune, you can create a device restrictions profile that manages app installation from unknown sources, app auto updates, and more (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Device Restrictions** for profile type > **Applications**).

There are new settings that give enhanced permissions to some selected apps:

- **Allow other apps to install and manage certificates**: Admins can select multiple apps for this permission. The selected apps are granted access to certificate installation and management.
- **Allow this app to access Android security logs**: Admins can select one app for this permission. The selected app is granted access to security logs.
- **Allow this app to access Android network activity logs**: Admins can select one app for this permission The selected app is granted access to network activity logs.

For more information on the settings you can configure, go to [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune > Applications](../configuration/device-restrictions-android-for-work.md#applications).

Applies to:

- Android Enterprise fully managed devices
- Android Enterprise dedicated devices
- Android Enterprise corporate-owned devices with a work profile

### New settings available in the macOS settings catalog <!-- 24950434  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration profiles** > **Create profile** > **macOS** > **Settings catalog** for profile type.  

**Microsoft Defender > Antivirus engine**:

- Enforcement Level

**Privacy > Privacy Preferences Policy Control**:

- System Policy App Data

**Restrictions**:

- Force On Device Only Dictation

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Import and export settings catalog policies<!-- 3470151  -->  
The Intune [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure, and all in one place (**Devices** > **Configuration profiles** > **Create profile** > Select your **platform** > For **Profile**, select **Settings catalog**).

The settings catalog policies can be imported and exported:

- To export an existing policy, select the profile > select the ellipsis > **Export**.
- To import a previously exported settings catalog policy, select **Create profile** > **Import policy** > select the previously exported file.

For more information about the settings catalog, go to [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md).

### New setting to block users from using the same password to unlock the device and access the work profile on Android Enterprise personally owned devices with a work profile<!-- 6167371  -->  
On Android Enterprise personally owned devices with a work profile, users can use the same password to unlock the device and access the work profile.

There's a new setting that can enforce different passwords to unlock the device and access the work profile (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** > **Personally Owned Work Profile** for platform > **Device Restrictions** for profile type):

- **One lock for work profile and device**: **Block** prevents users from using the same password for the lock screen on the device and work profile. End users are required to enter the device password to unlock the device and enter their work profile password to access their work profile. When set to **Not Configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to access their work profile using a single password.

This setting is optional and doesn't impact existing configuration profiles.

Currently, if the work profile password doesn't meet the policy requirements, then device users see a notification. The device isn't marked as non-compliant. A separate compliance policy for the work profile is being created and will be available in a future release.

For a list of settings you can currently configure on personally owned devices with a work profile, go to [Android Enterprise device settings list to allow or restrict features on personally owned devices using Intune](../configuration/device-restrictions-android-enterprise-personal.md).

Applies to:

- Android Enterprise personally owned devices with a work profile (BYOD)

<!-- *********************************************** -->

## Device enrollment

### Web-based enrollment with JIT registration for personal iOS/iPadOS devices <!-- 15412485  -->  
Intune will support web-based enrollment with just in time (JIT) registration for personal devices set up via Apple device enrollment. JIT registration reduces the number of authentication prompts shown to users throughout the enrollment experience and establishes SSO across the device. Enrollment takes place on the web version of Intune Company Portal, eliminating need for the app. Additionally, this enrollment method enables employees and students without managed Apple IDs to enroll devices and access volume-purchased apps.

<!-- *********************************************** -->

## Device management

### Introducing a remote action to pause the config refresh enforcement interval<!-- 24249019  -->  
In the Windows Settings Catalog you can configure **Config Refresh**. This feature lets you set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check-in to Intune. The device will replay and re-enforce settings based on previously received policy to minimize the chance for configuration drift.

To support this feature, a remote action will be added to allow a pause in action. If an admin needs to make changes or run remediation on a device for troubleshooting or maintenance, they can issue a pause from Intune for a specified period. When the period expires, settings will be enforced again.

The remote action **Pause config refresh** can be accessed from the device summary page.

For information on currently available Remote actions, see [Remote actions](../remote-actions/device-management.md).

### Remote Help for Android is now generally available<!--17675897  -->  
Remote Help will be generally available for Android Enterprise Dedicated devices from Zebra and Samsung.

With Remote Help, IT Pros can remotely view the device screen and take full control in both attended and unattended scenarios, to diagnose and resolve issues quickly and efficiently.

Applies to:

- Android Enterprise Dedicated devices, manufactured by Zebra or Samsung

For more information, go to [Remote Help on Android](../fundamentals/remote-help-android.md).

<!-- *********************************************** -->

## Device security

### Defender for Endpoint security settings management enhancements and support for Linux and macOS will soon be generally available<!-- 24190967  -->  
The improvements introduced in the Defender for Endpoint security settings management [opt-in public preview](../fundamentals/whats-new.md#defender-for-endpoint-security-settings-management-enhancements-and-support-for-linux-and-macos-in-public-preview) will soon be generally available. This change will include support all of the opt-in preview behavior – without having to enable support for preview features in Microsoft Defender for Endpoint.

When the opt-in public preview behavior becomes generally available, the following endpoint security profiles for Linux and macOS that were added as part of the opt-in preview will also generally available:

**Linux**:

- Microsoft Defender Antivirus
- Microsoft Defender Antivirus exclusions
- Endpoint detection and response

**MacOS**:

- Microsoft Defender Antivirus
- Microsoft Defender Antivirus exclusions
- Endpoint detection and response

For more information, see [Microsoft Defender for Endpoint Security settings management](../protect/mde-security-integration.md?pivots=mdssc-preview) in the Intune documentation.

###  Mvision Mobile is changing to Trellix Mobile Security<!-- 16208061 -->  
The Intune [Mobile Threat Defense partner](../protect/mobile-threat-defense.md) **Mvision Mobile**  is transitioning to **Trellix Mobile Security**. With this change we’ll be updating Intune UI and our documentation to match. For example, the *Mvision Mobile connector* will soon be *Trellix Mobile Security*.

If you have questions about this change, reach out to your Trellix Mobile Security representative.

### Configure declarative software updates for Apple devices in the Settings Catalog<!-- 24989083  -->  
You'll be able to manage software updates using Apple's declarative device management (DDM) configuration using the Settings Catalog (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type:).

For more information about DDM, go to [Apple's declarative device management (DDM)](https://developer.apple.com/documentation/devicemanagement/leveraging_the_declarative_management_data_model_to_scale_devices) (opens Apple's website).

DDM allows you to install a specific update by an enforced deadline. The autonomous nature of DDM provides an improved user experience as the device handles the entire software update lifecycle. It prompts users that an update is available and also downloads, prepares the device for the installation, & installs the update.

In the settings catalog, the following declarative software update settings will be available at **Declarative device management > Software Update**:

- **Details URL**: The web page URL that shows the update details. Typically, this is a web page hosted by your organization that users can select if they need organization-specific help with the update.
- **Target Build Version**: The target build version to update the device to, like `20A242`. The build version can include a supplemental version identifier, like `20A242a`. If the build version you enter isn’t consistent with the **Target OS Version** value you enter, then the **Target OS Version** value takes precedence.
- **Target Local Date Time**: The local date time value that specifies when to force install the software update. If the user doesn’t trigger the software update before this time, then the device force installs it.
- **Target OS Version**: The target OS version to update the device to. This value is the OS version number, like `16.1`. You can also include a supplemental version identifier, like `16.1.1`.

For information on the settings you can currently configure, go to:

- [Manage iOS/iPadOS software update policies in Intune](../protect/software-updates-ios.md)
- [Manage macOS software update policies in Intune](../protect/software-updates-macos.md)
- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md)

Applies to:

- iOS/iPadOS 17.0 and later
- macOS 14.0 and later

<!-- *********************************************** -->

<!-- ## Monitor and troubleshoot -->

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

## Tenant administration

### Intune admin center home page update<!-- 16950040 -->  
The Intune admin center home page has been redesigned with a fresh new look and more dynamic content. The **Status** section has been simplified. You can explore Intune related capabilities in the **Spotlight** section. The **Get more out of Intune** section provides links to the Intune community and blog, as well as Intune customer success. Also, the **Documentation and training** section provides links to **What's New in Intune**, **Feature in development**, and additional training. This update will be available when you access [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Home**.

### `endpoint.microsoft.com` URL will redirect to `intune.microsoft.com` <!-- 25169925  -->  
Previously, it was announced that the Microsoft Intune admin center has a new URL (`https://intune.microsoft.com`). The `https://endpoint.microsoft.com` URL will redirect to `https://intune.microsoft.com`.


<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
