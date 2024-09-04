---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 08/23/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals

# optional metadata

#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
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

<!-- Common categories: use this order:
## Microsoft Intune Suite
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

## Microsoft Intune Suite

### Use Copilot with Endpoint Privilege Manager to help identify potential elevation risks<!-- 27265509 -->

We’re adding support for Copilot to help you investigate Endpoint Privilege Manager (EPM) elevation details. Copilot will help you evaluate information from you EPM elevation requests to identify potential indicators of compromise by using information from [Microsoft Defender](/defender-endpoint/microsoft-defender-endpoint).

EPM is available as an [Intune Suite add-on-capability](../fundamentals/intune-add-ons.md). To learn more about how you can use Copilot in Intune, see [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md).

### Endpoint Privilege Manager elevation rule support for file arguments and parameters<!--28077130 -->

Soon, the file elevation rules for Endpoint Privilege Manager (EPM) will support use of arguments or parameters that you want to allow. Arguments and parameters that aren't explicitly allowed will be blocked from use. This capability helps to improve control of the context for file elevations.

EPM is available as an [Intune Suite add-on-capability](../fundamentals/intune-add-ons.md).

<!-- ***********************************************-->

## App management

### New UI for Intune Company Portal app for Windows<!-- 27219294 -->

The UI for the Intune Company Portal app for Windows will be updated. Users will be able to use the same functionality they’re used to with an improved experience for their desktop app. With the updated design, users will see improvements in user experience for the **Home**, **Devices**, and **Downloads & updates** pages. The new design will be more intuitive and will highlights areas where users need to take action.

For more information, see [New look for Intune Company Portal app for Windows](https://techcommunity.microsoft.com/t5/intune-customer-success/new-look-for-intune-company-portal-app-for-windows/ba-p/4158755).

### Working Time settings for Microsoft Teams<!-- 14631539 -->

Working time settings will allow you to enforce policies that limit access and to mute notifications received during non-working time on Microsoft Teams app. You'll be able to limit access by using App Protection Policies (APP) to block end users from using the iOS/iPadOS or Android Teams app during non-working time. Also, you'll be able to create a non-working time policy to mute notifications from the Teams app to end users during non-working time.

Applies to:

- Android
- iOS/iPadOS

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies now provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

## Device configuration

### New settings available in the Apple settings catalog <!-- 28672633 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

#### iOS/iPadOS

**Declarative Device Management (DDM) > Math Settings**:

- Calculator
  - Basic Mode
  - Math Notes Mode
  - Scientific Mode

- System Behavior
  - Keyboard Suggestions
  - Math Notes

**Restrictions**:

- Allow Personalized Handwriting Results
- Allow Video Conferencing Remote Control
- Allow Genmoji
- Allow Image Playground
- Allow Image Wand
- Allow iPhone Mirroring
- Allow Writing Tools

**Web Content Filter**:

- Hide Deny List URLs

#### macOS

**Declarative Device Management (DDM) > Math Settings**:

- Calculator
  - Basic Mode
  - Math Notes Mode
  - Programmer Mode
  - Scientific Mode

- System Behavior
  - Keyboard Suggestions
  - Math Notes

**Restrictions**:

- Allow Genmoji
- Allow Image Playground
- Allow iPhone Mirroring
- Allow Writing Tools

**System Configuration > System Extensions**:

- Non Removable From UI System Extensions
- Non Removable System Extensions


### Device Firmware Configuration Interface (DFCI) supports VAIO devices <!-- 28186944 -->

For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type.

Some VAIO devices running Windows 10/11 are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

For more information about DFCI profiles, see:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](../../autopilot/dfci-management.md)

Applies to:

- Windows 10
- Windows 11

### Samsung ended support for multiple Android device administrator (DA) settings <!-- 24990472 -->

On Android device administrator managed (DA) devices, Samsung has deprecated many [Samsung Knox APIs](https://docs.samsungknox.com/dev/knox-sdk/api-reference/deprecated-api-methods/) (opens Samsung's web site) configuration settings.

In Intune, this deprecation impacts the following device restrictions settings, compliance settings and trusted certificate profiles:

- [Device restriction settings for Android in Microsoft Intune](../configuration/device-restrictions-android.md)
- [View the Android device administrator compliance settings for Microsoft Intune compliance policies](../protect/compliance-policy-create-android.md)
- [Create trusted certificate profiles in Microsoft Intune](../protect/certificates-trusted-root.md#trusted-certificate-profiles-for-android-device-administrator)

In the Intune admin center, when you create or update a profile with these settings, the impacted settings are noted.

Though the functionality might continue to work, there's no guarantee that it will continue working for any or all Android DA versions supported by Intune. For more information on Samsung support for deprecated APIs, see [What kind of support is offered after an API is deprecated?](https://docs.samsungknox.com/dev/knox-sdk/faqs/general/deprecated-api-support-change.htm) (opens Samsung's web site).

Instead, you can manage Android devices with Intune using one of the following Android Enterprise options:

- [Set up enrollment of Android Enterprise personally owned work profile devices](../enrollment/android-work-profile-enroll.md)
- [Set up Intune enrollment of Android Enterprise corporate-owned devices with work profile](../enrollment/android-corporate-owned-work-profile-enroll.md)
- [Set up enrollment for Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md)
- [Set up Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md)
- [App protection policies overview](../apps/app-protection-policy.md)

Applies to:

- Android device administrator (DA)

### Consent prompt update for remote log collection<!-- 28072852 -->

End users might see a different consent experience for remote log collection after the Android APP SDK 10.4.0 and iOS APP SDK 19.6.0 updates. End users will no longer see a common prompt from Intune and will only see a prompt from the application if it has one.

Applies to:

- Android
- iOS/iPadOS

<!-- *********************************************** -->

## Device enrollment

### New Setup Assistant screens available for configuration <!-- 26607203, 2532989 -->

New Setup Assistant screens will be available to configure in the Microsoft Intune admin center. You can hide or show these screens during automated device enrollment.

For macOS:

- **Wallpaper**: Show or hide the macOS Sonoma wallpaper setup pane that appears after an upgrade on devices running macOS 14 and later.
- **Lockdown mode**: Show or hide the macOS lockdown mode setup pane on devices running macOS 14 and later.
- **Intelligence**: Show or hide the intelligence setup pane on devices running macOS 15 and later.

For iOS/iPadOS:

- **Emergency SOS**: Show or hide the safety (emergency SOS) setup pane on devices running iOS/iPadOS 16 and later.
- **Action button**: Show or hide the action button setup pane on devices running iOS/iPadOS 17 and later.
- **Intelligence**: Show or hide the intelligence setup pane on devices running iOS/iPadOS 18 and later.

You can configure these screens in new and existing enrollment policies.

Applies to:

- iOS/iPadOS
- macOS

### Support ending for Apple User Enrollment with Company Portal<!-- 28361917 -->

After the release of iOS/iPadOS 18, Apple will no longer support profile-based Apple User Enrollment. As a result, Intune will end support for [user enrollment with Company Portal](../enrollment/apple-user-enrollment-with-company-portal.md) shortly after the release of iOS/iPadOS 18.

After Intune ends support for user enrollment with Company Portal:

- Existing enrolled devices won't be impacted.
- Users won't be able to enroll devices if they're targeted with this enrollment profile type.
- Microsoft Intune technical support will be available for existing enrolled devices with this enrollment profile type. Technical support won't be available for new enrollments.

To prepare, use a different management method to enroll devices. We recommend account-driven Apple User Enrollment for similar functionality and an improved user experience. For a simpler enrollment experience, try web- based device enrollment. For more information, see:

- [Set up account-driven Apple User Enrollment](../enrollment/apple-account-driven-user-enrollment.md)
- [Set up web-based device enrollment for iOS/iPadOS](../enrollment/web-based-device-enrollment-ios.md)

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

## Device management

### Intune will support macOS 13.x as the minimum version<!-- 28391869 -->

With Apple's release of macOS 15 Sequoia, Microsoft Intune, the Company Portal app, and the Intune MDM agent will now require macOS 13 (Big Sur) and later.

For more information on this change, see [Plan for change: Intune is moving to support macOS 13 and later](../fundamentals/whats-new.md#plan-for-change-intune-is-moving-to-support-macos-13-and-higher-later-this-year).

> [!NOTE]
> macOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement](https://aka.ms/Intune/macOS/ADE-DE-support).

Applies to:

- macOS

### Intune supports iOS/iPadOS 16.x as the minimum version<!-- 28391935 -->

Later this year, we expect iOS18 and iPadOS 18 to be released by Apple. Microsoft Intune, including the Intune Company Portal and Intune app protection policies (APP, also known as MAM), will require iOS/iPadOS 16 and higher shortly after the iOS/iPadOS 18 release.

For more information on this change, see [Plan for change: Intune is moving to support iOS/iPadOS 16 and later](../fundamentals/whats-new.md#plan-for-change-intune-is-moving-to-support-iosipados-16-and-later).

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

## Device security

### New disk encryption template for Personal Data Encryption<!-- 28677934 -->

We’re adding a new template named *Personal Data Encryption* (PDE) to endpoint security BitLocker policy. The new template configures the Windows PDE configuration service provider (CSP) that was introduced in Windows 11 22H2.

PDE is different than BitLocker. PDE encrypts individual files and content, instead of whole volumes and disks. You can use PDE with other encryption methods, such as BitLocker.

Previously, the [PDE CSP](/windows/client-management/mdm/personaldataencryption-csp) was made available through the [Intune settings catalog](../fundamentals/whats-new-archive.md#turn-onoff-personal-data-encryption-on-windows-11-devices-using-the-settings-catalog).

Applies to:

- Windows 11

### Defender for Endpoint security settings support in government cloud environments<!-- 24191406 -->

Customer tenants in US Government Community Cloud (GCC) High, and Department of Defense (DoD) environments will soon be able to use Intune to manage the Defender security settings on the devices you’ve onboarded to Defender without enrolling those devices with Intune. This capability is known as [Defender for Endpoint security settings management](../protect/mde-security-integration.md).

For more information about the Intune features supported in GCC High and DoD environments, see [Intune US Government service description](../fundamentals/intune-govt-service-description.md).

### Support for Intune Device control policy for devices managed by Microsoft Defender for Endpoint<!-- 15466620 -->

You'll be able to use the endpoint security policy for *Device control* (Attack surface reduction policy) from the Microsoft Intune with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.

- **Device control** policies are part of endpoint security [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

Applies to the following when you use the *Windows 10, Windows 11, and Windows Server* platform:

- Windows 10
- Windows 11

When this change takes effect, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive this policy will get it.

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

<!-- ## Monitor and troubleshoot -->
 
<!-- *********************************************** -->

<!-- ## Tenant administration -->

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
