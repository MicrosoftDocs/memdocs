---
# required metadata
title: What's new in Microsoft Intune
titleSuffix:
description: Find out what's new in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- tier2
- M365-identity-device-management
- highseo
---

# What's new in Microsoft Intune

Learn what's new each week in Microsoft Intune.

You can also read:

- [**Important notices**](#notices)
- [Past releases](whats-new-archive.md) in the What's new archive
- Information about [how Intune service updates are released](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728)

> [!NOTE]
> Each [monthly update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) can take up to three days to rollout and will be in the following order:
>
> - Day 1: Asia Pacific (APAC)
> - Day 2: Europe, Middle East, Africa (EMEA)
> - Day 3: North America
> - Day 4+: Intune for Government
>
> Some features roll out over several weeks and might not be available to all customers in the first week.
>
> For a list of upcoming Intune feature releases, see [In development for Microsoft Intune](../fundamentals/in-development.md).
>
> For new information about Windows Autopilot solutions, see:
>
> - [Windows Autopilot device preparation: What's new](/autopilot/device-preparation/whats-new)
> - [Windows Autopilot: What's new](/autopilot/whats-new)

You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Get notified when this page is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us` -->

<!-- Common categories - in this order:

### Microsoft Intune Suite
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
### Scripts
### Tenant administration

-->
## Week of November 18, 2024

### App management

#### Microsoft Teams app protection on VisionOS devices (preview)<!-- 29913431 -->
Microsoft Intune app protection policies (APP) are now supported on the Microsoft Teams app on VisionOS devices. To learn more about how to target policies to VisionOS devices, see [Managed app properties](../fundamentals/filters-device-properties.md#managed-app-properties) for more information about filters for managed app properties.

Applies to:
- Microsoft Teams for iOS on VisionOS devices

## Week of October 28, 2024

### Device security

#### Defender for Endpoint security settings support in government cloud environments (generally available)<!-- 30064299 -->

Now generally available, customer tenants in the Government Community Cloud (GCC), US Government Community High (GCC High), and Department of Defense (DoD) environments can use Intune to manage the Defender security settings on the devices you’ve onboarded to Defender without enrolling those devices with Intune. Previously, support for Defender security settings was in public preview.

This capability is known as [Defender for Endpoint security settings management](../protect/mde-security-integration.md).

## Week of October 14, 2024 (Service release 2410)

### App management

#### Updates to app configuration policies for Android Enterprise devices<!-- 26711672 -->

App configuration policies for Android Enterprise devices now support overriding the following permissions:

- Access background location
- Bluetooth (connect)

For more information about app configuration policies for Android Enterprise devices, see [Add app configuration policies for managed Android Enterprise devices](../apps/app-configuration-policies-use-android.md).

Applies to:

- Android Enterprise devices

### Device configuration

#### Windows Autopilot device preparation support in Intune operated by 21Vianet in China<!-- MAXADO-9313795 / INADO-28687730 -->

Intune now supports *Windows Autopilot device preparation* policy for [Intune operated by 21Vianet in China](../fundamentals/china.md) cloud. Customers with tenants located in China can now use *Windows Autopilot device preparation* with Intune to provision devices.

For information about this Autopilot support, see the following in the Autopilot documentation:

- Overview: [Overview of Windows Autopilot device preparation](/autopilot/device-preparation/overview)
- Tutorial: [Windows Autopilot device preparation scenarios](/autopilot/device-preparation/tutorial/scenarios)

### Device management

#### Minimum OS version for Android devices is Android 10 and later for user-based management methods<!-- 14755802 -->

Beginning in October 2024, Android 10 and later is the minimum Android OS version that is supported for user-based management methods, which includes:

- Android Enterprise personally-owned work profile
- Android Enterprise corporate owned work profile
- Android Enterprise fully managed
- Android Open Source Project (AOSP) user-based
- Android device administrator
- App protection policies (APP)
- App configuration policies (ACP) for managed apps

For enrolled devices on unsupported OS versions (Android 9 and lower)

- Intune technical support is not provided.
- Intune won't make changes to address bugs or issues.
- New and existing features aren't guaranteed to work.

While Intune doesn't prevent enrollment or management of devices on unsupported Android OS versions, functionality isn't guaranteed, and use isn't recommended.

Userless methods of Android device management (Dedicated and AOSP userless) and Microsoft Teams certified Android devices are not affected by this change.

#### Collection of additional device inventory details<!-- 29460196 -->

Intune now collects additional files and registry keys to assist in troubleshooting the Device Hardware Inventory feature.

Applies to:

- Windows

## Week of October 7, 2024

### App management

#### New UI for Intune Company Portal app for Windows<!-- 27219294 -->

The UI for the Intune Company Portal app for Windows is updated. Users now see an improved experience for their desktop app without changing the functionality they've used in the past. Specific UI improvements are focused on the **Home**, **Devices**, and **Downloads & updates** pages. The new design is more intuitive and highlights areas where users need to take action.

For more information, see [New look for Intune Company Portal app for Windows](https://techcommunity.microsoft.com/t5/intune-customer-success/new-look-for-intune-company-portal-app-for-windows/ba-p/4158755). For end user details, see [Install and share apps on your device](../user-help/install-apps-cpapp-windows.md).

### Device security

#### New strong mapping requirements for SCEP certificates authenticating with KDC<!-- 29005591 -->

The Key Distribution Center (KDC) requires user or device objects to be strongly mapped to Active Directory for certificate-based authentication. This means that a Simple Certificate Enrollment Protocol (SCEP) certificate's subject alternative name (SAN) must have a security identifier (SID) extension that maps to the user or device SID in Active Directory. The mapping requirement protects against certificate spoofing and ensures that certificate-based authentication against the KDC continues working.

To meet requirements, modify or create a SCEP certificate profile in Microsoft Intune. Then add a `URI` attribute and the `OnPremisesSecurityIdentifier` variable to the SAN. After you do that, Microsoft Intune appends a tag with the SID extension to the SAN and issues new certificates to targeted users and devices. If the user or device has a SID on premises that's been synced to Microsoft Entra ID, the certificate shows the SID. If they don't have a SID, a new certificate is issued without the SID.

For more information and steps, see [Update certificate connector: Strong mapping requirements for KB5014754](../protect/certificates-profile-scep.md).

Applies to:

- Windows 10/11, iOS/iPadOS, and macOS user certificates
- Windows 10/11 device certificates

This requirement isn't applicable to device certificates used with Microsoft Entra joined users or devices, because the SID attribute is an on-premises identifier.

#### Defender for Endpoint security settings support in government cloud environments (public preview)<!-- 24191406 -->

In public preview, customer tenants in US Government Community (GCC) High, and Department of Defense (DoD) environments can now use Intune to manage the Defender security settings on the devices that onboarded to Defender without enrolling those devices with Intune. This capability is known as [Defender for Endpoint security settings management](../protect/mde-security-integration.md).

For more information about the Intune features supported in GCC High and DoD environments, see [Intune US Government service description](../fundamentals/intune-govt-service-description.md).

## Week of September 30, 2024

### Device security

#### Updates to PKCS certificate issuance process in Microsoft Intune Certificate Connector, version 6.2406.0.1001 <!-- 24186560 -->

We've updated the process for Public Key Cryptography Standards (PKCS) certificate issuance in Microsoft Intune to support the security identifiers (SID) information requirements described in [KB5014754](https://support.microsoft.com/topic/kb5014754-certificate-based-authentication-changes-on-windows-domain-controllers-ad2c23b0-15d8-4340-a468-4d4f3b188f16). As part of this update, an OID attribute containing the user or device SID is added to the certificate. This change is available with the Certificate Connector for Microsoft Intune, version 6.2406.0.1001, and applies to users and devices synced from Active Directory on-premises to Microsoft Entra ID.

The SID update is available for user certificates across all platforms, and for device certificates specifically on Microsoft Entra hybrid joined Windows devices.

For more information, see:

- [What's new for the certificate connector](../protect/certificate-connector-overview.md#september-19-2024)

- [Apply PFX changes to certificate](../protect/certificates-pfx-configure.md)  

## Week of September 23, 2024 (Service release 2409)

### App management

#### Working Time settings for app protection policies<!-- 14631539 -->

Working time settings allow you to enforce policies that limit access to apps and mute message notifications received from apps during non-working time. The limit access setting is now available for the Microsoft Teams and Microsoft Edge apps. You can limit access by using App Protection Policies (APP) to block or warn end users from using the iOS/iPadOS or Android Teams and Microsoft Edge apps during non-working time by setting the **Non-working time** conditional launch setting. Also, you can create a non-working time policy to mute notifications from the Teams app to end users during non-working time.

Applies to:

- Android
- iOS/iPadOS

#### Streamlined app creation experience for apps from Enterprise App Catalog<!-- 29411991 -->

We've streamlined the way apps from Enterprise App Catalog are added to Intune. We now provide a direct app link rather than duplicating the app binaries and metadata. App contents now download from a `*.manage.microsoft.com` subdomain. This update helps to improve the latency when adding an app to Intune. When you add an app from Enterprise App Catalog, it syncs immediately and is ready for additional action from within Intune.

#### Update Enterprise App Catalog apps<!-- 24875279 -->

Enterprise App Management is enhanced to allow you to update an **Enterprise App Catalog** app. This capability guides you through a wizard that allows you to add a new application and use supersedence to update the previous application.

For more information, see [Guided update supersedence for Enterprise App Management](../apps/apps-eam-supersedence.md).

### Device configuration

#### Samsung ended support for multiple Android device administrator (DA) settings <!-- 24990472 -->

On Android device administrator managed (DA) devices, Samsung has deprecated many [Samsung Knox APIs](https://docs.samsungknox.com/dev/knox-sdk/api-reference/deprecated-api-methods/) (opens Samsung's web site) configuration settings.

In Intune, this deprecation impacts the following device restrictions settings, compliance settings, and trusted certificate profiles:

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

#### Device Firmware Configuration Interface (DFCI) supports VAIO devices <!-- 28186944 -->

For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type.

Some VAIO devices running Windows 10/11 are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

For more information about DFCI profiles, see:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](../../autopilot/dfci-management.md)

Applies to:

- Windows 10
- Windows 11

#### New settings available in the Apple settings catalog <!-- 28672633 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Declarative Device Management (DDM) > Math Settings**:

- Calculator
  - Basic Mode
  - Math Notes Mode
  - Scientific Mode

- System Behavior
  - Keyboard Suggestions
  - Math Notes

**Web Content Filter**:

- Hide Deny List URLs

##### macOS

**Declarative Device Management (DDM) > Math Settings**:

- Calculator
  - Basic Mode
  - Math Notes Mode
  - Programmer Mode
  - Scientific Mode

- System Behavior
  - Keyboard Suggestions
  - Math Notes

**System Configuration > System Extensions**:

- Non Removable From UI System Extensions
- Non Removable System Extensions

#### Consent prompt update for remote log collection<!-- 28072852 -->

End users might see a different consent experience for remote log collection after the Android APP SDK 10.4.0 and iOS APP SDK 19.6.0 updates. End users no longer see a common prompt from Intune and only see a prompt from the application, if it has one.

Adoption of this change is per-application and is subject to each applications release schedule.

Applies to:

- Android
- iOS/iPadOS

### Device enrollment

#### New Setup Assistant screens available for configuration for ADE <!-- 26607203, 2532989 -->

New Setup Assistant screens are available to configure in the Microsoft Intune admin center. You can hide or show these screens during automated device enrollment (ADE).

For macOS:

- **Wallpaper**: Show or hide the macOS Sonoma wallpaper setup pane that appears after an upgrade on devices running macOS 14.1 and later.
- **Lockdown mode**: Show or hide the lockdown mode setup pane on devices running macOS 14.1 and later.
- **Intelligence**: Show or hide the Apple Intelligence setup pane on devices running macOS 15 and later.

For iOS/iPadOS:

- **Emergency SOS**: Show or hide the safety setup pane on devices running iOS/iPadOS 16 and later.
- **Action button**: Show or hide the setup pane for the action button on devices running iOS/iPadOS 17 and later.
- **Intelligence**: Show or hide the Apple Intelligence setup pane on devices running iOS/iPadOS 18 and later.

You can configure these screens in new and existing enrollment policies. For more information and additional resources, see:

- [Set up Apple automated device enrollment for iOS/iPadOS](../enrollment/device-enrollment-program-enroll-ios.md)
- [Set up Apple automated device enrollment for Macs](../enrollment/device-enrollment-program-enroll-macos.md)

#### Extended expiration date for corporate-owned, user-associated AOSP enrollment tokens<!-- 25782149 -->

Now when you create an enrollment token for Android Open Source Project (AOSP) corporate-owned, user-associated devices, you can select an expiration date that's up to 65 years into the future, an improvement over the previous 90 day expiration date. You can also modify the expiration date of existing enrollment tokens for Android Open Source Project (AOSP) corporate-owned, user-associated devices.

### Device security

#### New disk encryption template for Personal Data Encryption<!-- 28677934 -->

You can now use the new *Personal Data Encryption* (PDE) template that is available through endpoint security [*disk encryption* policy](../protect/encrypt-devices.md). This new template configures the Windows [PDE configuration service provider](/windows/client-management/mdm/personaldataencryption-csp) (CSP), which was introduced in Windows 11 22H2. The PDE CSP is also available through the settings catalog.

PDE differs from BitLocker in that it encrypts files instead of whole volumes and disks. PDE occurs in addition to other encryption methods such as BitLocker. Unlike BitLocker that releases data encryption keys at boot, PDE doesn't release data encryption keys until a user signs in using Windows Hello for Business.

Applies to:

- Windows 11 version 22h2 or later

For more information about PDE, including prerequisites, related requirements, and recommendations, see the following articles in the Windows security documentation:

- [PDE overview](/windows/security/operating-system-security/data-protection/personal-data-encryption/)
- [Configure PDE](/windows/security/operating-system-security/data-protection/personal-data-encryption/configure)
- [PDE frequently asked questions (FAQ)](/windows/security/operating-system-security/data-protection/personal-data-encryption/faq)

### Intune Apps

#### Newly available protected app for Intune<!-- 28730764 -->

The following protected app is now available for Microsoft Intune:

- Notate for Intune by Shafer Systems, LLC

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of September 9, 2024

### App management

#### Managed Home Screen user experience update<!-- 28232751 -->

All Android devices automatically migrate to the updated Managed Home Screen (MHS) user experience. For more information, see [Updates to the Managed Home Screen experience](https://techcommunity.microsoft.com/t5/intune-customer-success/updates-to-the-managed-home-screen-experience/bc-p/3997842).

### Device enrollment

#### Support has ended for Apple profile-based user enrollment with Company Portal<!-- 28361917 -->

Apple supports two types of manual enrollment methods for users and devices in bring-your-own-device (BYOD) scenarios: *profile-based enrollment* and *account-driven enrollment*. Apple has ended support for profile-based user enrollment, known in Intune as *user enrollment with Company Portal*. This method was their privacy-focused BYOD enrollment flow that used managed Apple IDs. As a result of this change, Intune has ended support for [profile-based user enrollment with Company Portal](../enrollment/apple-user-enrollment-with-company-portal.md). Users can no longer enroll devices targeted with this enrollment profile type. This change doesn't affect devices that are already enrolled with this profile type, so you can continue to manage them in the admin center and receive Microsoft Intune technical support. Less than 1% of Apple devices across all Intune tenants are currently enrolled this way, so this change doesn't affect most enrolled devices.

There's no change to profile-based device enrollment with Company Portal, the default enrollment method for BYOD scenarios. Devices enrolled via Apple automated device enrollment also remain unaffected.

We recommend account-driven user enrollment as a replacement method for devices. For more information about your BYOD enrollment options in Intune, see:

- [Account-driven user enrollment](../enrollment/apple-account-driven-user-enrollment.md)
- [Web-based device enrollment](../enrollment/web-based-device-enrollment-ios.md)
- [Device enrollment with Company Portal](../enrollment/ios-device-enrollment.md#app-or-web-based-enrollment) (default enrollment method for BYOD scenarios)

For more information about the device enrollment types supported by Apple, see [Intro to Apple device enrollment types](https://support.apple.com/en-mide/guide/deployment/dep08f54fcf6/web) in the Apple Platform Deployment guide.

### Device management

#### Intune now supports iOS/iPadOS 16.x as the minimum version<!-- 28391935 -->

Later this year, we expect iOS 18 and iPadOS 18 to be released by Apple. Microsoft Intune, including the Intune Company Portal and Intune app protection policies (APP, also known as MAM), will require iOS/iPadOS 16 and higher shortly after the iOS/iPadOS 18 release.

For more information on this change, see [Plan for change: Intune is moving to support iOS/iPadOS 16 and later](whats-new.md#plan-for-change-intune-is-moving-to-support-iosipados-16-and-later).

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

Applies to:

- iOS/iPadOS

#### Intune now supports macOS 13.x as the minimum version<!-- 28391869 -->

With Apple's release of macOS 15 Sequoia, Microsoft Intune, the Company Portal app, and the Intune MDM agent will now require macOS 13 (Ventura) and later.

For more information on this change, see [Plan for change: Intune is moving to support macOS 13 and later](whats-new.md#plan-for-change-intune-is-moving-to-support-macos-13-and-higher-later-this-year)

> [!NOTE]
> macOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement](https://aka.ms/Intune/macOS/ADE-DE-support).

Applies to:

- macOS

## Week of August 19, 2024 (Service release 2408)

### Microsoft Intune Suite

#### Easy creation of Endpoint Privilege Management elevation rules from support approval requests and reports<!-- 28196775 -->

You can now create Endpoint Privilege Management (EPM) elevation rules directly from a support approved elevation request or from details found in the EPM Elevation report. With this new capability, you won’t need to manually identify specific file detection details for elevation rules. Instead, for files that appear in the Elevation report or a support approved elevation request, you can select that file to open its elevation detail pane, and then select the option to **Create a rule with these file details**.

When you use this option, you can then choose to add the new rule to one of your existing elevation policies, or create a new policy with only the new rule.

Applies to:

- Windows 10
- Windows 11

For information about this new capability, see [Windows elevation rules policy](../protect/epm-policies.md) in the *Configure policies for Endpoint Privilege management* article.

#### Introducing the Resource performance report for physical devices in Advanced Analytics<!-- 12659827 -->

We're introducing the Resource performance report for Windows physical devices in Intune Advanced Analytics. The report is included as an Intune-add on under Microsoft Intune Suite.

The resource performance scores and insights for physical devices are aimed to help IT admins make CPU/RAM asset management and purchase decisions that improve the user experience while balancing hardware costs.

For more information, see:

- [Resource Performance Report](../../analytics/resource-performance-report.md)
- [Microsoft Intune Suite](../fundamentals/intune-add-ons.md)

### App management

#### Managed Home Screen for Android Enterprise Fully Managed devices<!-- 15603355 -->

Managed Home Screen (MHS) is now supported on Android Enterprise Fully Managed devices. This capability offers organizations the ability to leverage MHS in scenarios where a device is associated with a single user.

For related information, see:

- [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md)
- [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md)
- [Configure permissions for the Managed Home Screen (MHS) on Android Enterprise devices using Microsoft Intune](../configuration/oemconfig-managed-home-screen-permissions-android.md)

#### Updates to the Discovered Apps report<!-- 28898418 -->

The **Discovered Apps** report, which provides a list of detected apps that are on Intune enrolled devices for your tenant, now provides publisher data for Win32 apps, in addition to Store apps. Rather than providing publisher information only in the exported report data, we're including it as a column in the **Discovered Apps** report.

For more information, see [Intune Discovered apps](../apps/app-discovered-apps.md#monitor-discovered-apps-with-intune).

#### Improvements to Intune Management Extension logs<!-- 26113668 -->

We have updated how log activities and events are made for Win32 apps and the Intune Management Extension (IME) logs. A new log file (*AppWorkload.log*) contains all logging information related to app deployment activities conducted by the IME. These improvements provide better troubleshooting and analysis of app management events on the client.

For more information, see [Intune management extension logs](../apps/intune-management-extension.md#intune-management-extension-logs).

### Device configuration

#### New settings available in the Apple settings catalog <!-- 28308531 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Apple Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Declarative Device Management (DDM) > Safari Extension Settings**:

- Managed Extensions
  - Allowed Domains
  - Denied Domains
  - Private Browsing
  - State

**Declarative Device Management (DDM) > Software Update Settings**:

- Automatic Actions
  - Download
  - Install OS Updates

- Deferrals
  - Combined Period In Days

- Notifications

- Rapid Security Response
  - Enable
  - Enable Rollback

- Recommended Cadence

**Restrictions**:

- Allow ESIM Outgoing Transfers
- Allow Genmoji
- Allow Image Playground
- Allow Image Wand
- Allow iPhone Mirroring
- Allow Personalized Handwriting Results
- Allow Video Conferencing Remote Control
- Allow Writing Tools

##### macOS

**Authentication > Extensible Single Sign On (SSO)**:

- Platform SSO
  - Authentication Grace Period
  - FileVault Policy
  - Non Platform SSO Accounts
  - Offline Grace Period
  - Unlock Policy

**Authentication > Extensible Single Sign On Kerberos**:

- Allow Password
- Allow SmartCard
- Identity Issuer Auto Select Filter
- Start In Smart Card Mode

**Declarative Device Management (DDM) > Disk Management**:

- External Storage
- Network Storage

**Declarative Device Management (DDM) > Safari Extension Settings**:

- Managed Extensions
  - Allowed Domains
  - Denied Domains
  - Private Browsing
  - State

**Declarative Device Management (DDM) > Software Update Settings**:

- Allow Standard User OS Updates

- Automatic Actions
  - Download
  - Install OS Updates
  - Install Security Update

- Deferrals
  - Major Period In Days
  - Minor Period In Days
  - System Period In Days

- Notifications

- Rapid Security Response
  - Enable
  - Enable Rollback

**Restrictions**:

- Allow Genmoji
- Allow Image Playground
- Allow iPhone Mirroring
- Allow Writing Tools

**System Policy > System Policy Control**:

- Enable XProtect Malware Upload

#### Enhancements to multi administrative approval<!-- 25174473 -->

Multi administrative approval adds the ability to limit application access policies to Windows applications or all non-Windows applications or both. We're adding a new access policy to the multiple administrative approval feature to allow approvals for changes to multiple administrative approval.

For more information, see [Multi admin approval](../fundamentals/multi-admin-approval.md).

### Device enrollment

#### Account-driven Apple User Enrollment now generally available for iOS/iPadOS 15+<!-- 10277062 -->

Intune now supports account-driven Apple User Enrollment, the new, and improved version of Apple User Enrollment, for devices running iOS/iPadOS 15 and later. This new enrollment method utilizes just-in-time registration, removing the Company Portal app for iOS as an enrollment requirement. Device users can initiate enrollment directly in the Settings app, resulting in a shorter and more efficient onboarding experience.

For more information, see [Set up account driven Apple User Enrollment](../enrollment/apple-account-driven-user-enrollment.md) on Microsoft Learn.

Apple has announced they are ending support for profile-based Apple User Enrollment. As a result, Microsoft Intune will end support for Apple User Enrollment with Company Portal shortly after the release of iOS/iPadOS 18. We recommend enrolling devices with account-driven Apple User Enrollment for similar functionality and an improved user experience.

#### Use corporate Microsoft Entra account to enable Android Enterprise management options in Intune<!-- 25231452 -->

Managing Intune-enrolled devices with Android Enterprise management options previously required you to connect your Intune tenant to your managed Google Play account using an enterprise Gmail account. Now you can use a corporate Microsoft Entra account to establish the connection. This change is happening in new tenants, and doesn't affect tenants that have already established a connection.

For more information, see [Connect Intune account to Managed Google Play account - Microsoft Intune | Microsoft Learn](../enrollment/connect-intune-android-enterprise.md).

### Device management

#### 21Vianet support for Mobile Threat Defense connectors<!-- 10355489 -->

Intune operated by 21Vianet now supports Mobile Threat Defense (MTD) connectors for Android and iOS/iPadOS devices for MTD vendors that also have support in that environment. When an MTD partner is supported and you sign in to a 21Vianet tenant, the supported connectors are available.

Applies to:

- Android
- iOS/iPadOS

For more information, see:

- [Intune operated by 21Vianet in China](../fundamentals/china.md)
- [Mobile Threat Defense integration with Intune](../protect/mobile-threat-defense.md)

#### New `cpuArchitecture` filter device property for app and policy assignments<!-- 7423106 -->

When you assign an app, compliance policy, or configuration profile, you can filter the assignment using different device properties, such as device manufacturer, operating system SKU, and more.

A new `cpuArchitecture` device filter property is available for Windows and macOS devices. With this property, you can filter app and policy assignments depending on the processor architecture.

For more information on filters and the device properties you can use, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [Filter properties](filters-device-properties.md)
- [Supported workloads](filters-supported-workloads.md)

Applies to:

- Windows 10
- Windows 11
- macOS

### Device security

#### Windows platform name change for endpoint security policies<!-- 16104088 -->

When you create an endpoint security policy in Intune, you can select the Windows platform. For multiple templates in endpoint security, there are now only two options to choose for the Windows platform: **Windows** and **Windows (ConfigMgr)**.

Specifically, the platform name changes are:

| Original | New |
| --- | --- |
| Windows 10 and later​ | Windows |
| Windows 10 and later (ConfigMgr)​ | Windows (ConfigMgr)​ |
| Windows 10, Windows 11, and Windows Server | Windows |
| Windows 10, Windows 11, and Windows Server​ (ConfigMgr) | Windows (ConfigMgr)​ |

These changes apply to the following policies:

- Antivirus
- Disk encryption
- Firewall
- Endpoint Privilege Management
- Endpoint detection and response
- Attack surface reduction
- Account protection

##### What you need to know

- This change is only in the user experience (UX) that admins see when they create a new policy. There is no effect on devices.
- The functionally is the same as the previous platform names.
- There are no additional tasks or actions for existing policies.

For more information on endpoint security features in Intune, see [Manage endpoint security in Microsoft Intune](../protect/endpoint-security.md).

Applies to:

- Windows

#### Target Date Time setting for Apple software update enforcement schedules updates using the local time on devices <!-- 28865232 -->

You can specify the time that OS updates are enforced on devices in their local time zone. For example, configuring an OS update to be enforced at 5pm schedules the update for 5pm in the device's local time zone. Previously, this setting used the time zone of the browser where the policy was configured.

This change only applies to new policies that are created in the August 2408 release and later. The **Target Date Time** setting is in the settings catalog at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type > **Declarative Device Management** > Software Update.

In a future release, the **UTC** text will be removed from the **Target Date Time** setting.

For more information on using the settings catalog to configure software updates, see [Managed software updates with the settings catalog](../protect/managed-software-updates-ios-macos.md).

Applies to:

- iOS/iPadOS
- macOS

### Intune Apps

#### Newly available protected apps for Intune<!-- 28676100, 28442762, 28421791, 28441819, 28618264 -->

The following protected apps are now available for Microsoft Intune:

- Singletrack for Intune (iOS) by Singletrack
- 365Pay by 365 Retail Markets
- Island Browser for Intune (Android) by Island Technology, Inc.
- Recruitment.Exchange by Spire Innovations, Inc.
- Talent.Exchange by Spire Innovations, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Tenant administration

#### Organizational messages now in Microsoft 365 admin center<!-- 27711197 -->

The organizational message feature has moved out of the Microsoft Intune admin center and into its new home in the Microsoft 365 admin center. All organizational messages you created in Microsoft Intune are now in the Microsoft 365 admin center, where you can continue to view and manage them. The new experience includes highly requested features such as the ability to author custom messages, and deliver messages on Microsoft 365 apps.

For more information, see:

- [Introducing organizational messages (preview) in the Microsoft 365 admin center](https://techcommunity.microsoft.com/t5/microsoft-365-blog/introducing-organizational-messages-preview-in-the-microsoft-365/ba-p/4123890)
- [Organizational messages in the Microsoft 365 admin center](/microsoft-365/admin/misc/organizational-messages-microsoft-365)
- [Support tip: Organizational messages is moving to Microsoft 365 admin center - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-organizational-messages-is-moving-to-microsoft-365/ba-p/4148332)

## Week of July 29, 2024

### Microsoft Intune Suite

#### Endpoint Privilege Management, Advanced Analytics, and Intune Plan 2 are available for GCC High and DoD<!-- 25230811, 25300700, 27030977, 27234960 -->

We are excited to announce that the following capabilities from the Microsoft Intune Suite are now supported in U.S. Government Community Cloud (GCC) High and U.S. Department of Defense (DoD) environments.

Add-on capabilities:

- [Endpoint Privilege Management](../protect/epm-overview.md)
- [Advanced Analytics](../../analytics/advanced-endpoint-analytics.md) - With this release, GCC High and DoD support for Advanced Endpoint Analytics doesn't include the [*Device query*](../../analytics/device-query.md) functionality.

Plan 2 capabilities:

- [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-mam.md)
- [Firmware-over-the-air update](../protect/zebra-lifeguard-ota-integration.md)
- [Specialty devices management](../fundamentals/specialty-devices-with-intune.md)

For more information, see:

- [Use Microsoft Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md)
- [Microsoft Intune for US Government GCC service description](../fundamentals/intune-govt-service-description.md)

### Device enrollment

#### ACME protocol support for iOS/iPadOS and macOS enrollment<!-- 25140355 -->

As we prepare to support managed device attestation in Intune, we are starting a phased rollout of an infrastructure change for new enrollments that includes support for the *Automated Certificate Management Environment (ACME) protocol*. Now when new Apple devices enroll, the management profile from Intune receives an ACME certificate instead of a SCEP certificate. ACME provides better protection than SCEP against unauthorized certificate issuance through robust validation mechanisms and automated processes, which helps reduce errors in certificate management.

Existing OS and hardware eligible devices do not get the ACME certificate unless they re-enroll. There is no change to the end user's enrollment experience, and no changes to the Microsoft Intune admin center. This change only impacts enrollment certificates and has no impact on any device configuration policies.

ACME is supported for Apple Device Enrollment, Apple Configurator enrollment, and Automated device enrollment (ADE) methods. Eligible OS versions include:

- iOS 16.0 or later
- iPadOS 16.1 or later
- macOS 13.1 or later

## Week of July 22, 2024 (Service release 2407)

### Microsoft Intune Suite

#### New actions for Microsoft Cloud PKI<!-- 24231040 -->

The following actions have been added for Microsoft Cloud PKI issuing and root certification authorities (CA):

- Delete: Delete a CA.
- Pause: Temporarily suspend use of a CA.
- Revoke: Revoke a CA certificate.

You can access all new actions in the Microsoft Intune admin center and Graph API. For more information, see [Delete Microsoft Cloud PKI certification authority](../protect/microsoft-cloud-pki-delete.md).

### App management

#### Intune support for additional macOS app types from the Company Portal<!-- 26133163 -->

Intune supports the capability to deploy DMG and PKG apps as **Available** in the Intune macOS Company Portal. This capability enables end users to browse and install agent-deployed applications using Company Portal for macOS. This capability requires a minimum version of the Intune agent for macOS v2407.005 and Intune Company Portal for macOS v5.2406.2.

#### Newly available Enterprise App Catalog apps for Intune<!-- 28691663 -->

The Enterprise App Catalog has updated to include additional apps. For a complete list of supported apps, see [Apps available in the Enterprise App Catalog](../apps/apps-enterprise-app-management.md#apps-available-in-the-enterprise-app-catalog).

#### The Intune App SDK and Intune App Wrapping Tool are now in a different GitHub repo<!-- 27264674, 27264632 -->

The Intune App SDK and Intune App Wrapping Tool have moved to a different GitHub repository and a new account. There are redirects in place for all existing repositories. In addition, the Intune sample applications are also included in this move. This change relates to both Android and iOS platforms.

### Device configuration

#### New clipboard transfer direction settings available in the Windows settings catalog <!-- 28748086 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type.

**Administrative Templates > Windows Components > Remote Desktop Services > Remote Desktop Session Host > Device and Resource Redirection**:

- Restrict clipboard transfer from server to client
- Restrict clipboard transfer from server to client (User)
- Restrict clipboard transfer from client to server
- Restrict clipboard transfer from client to server (User)

For more information on configuring the clipboard transfer direction in Azure Virtual Desktop, see [Configure the clipboard transfer direction and types of data that can be copied in Azure Virtual Desktop](/azure/virtual-desktop/clipboard-transfer-direction-data-types).

Applies to:

- Windows 11
- Windows 10

#### New settings available in the Apple settings catalog <!-- 28052449 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Restrictions**:

- Allow Auto Dim

##### macOS

**Privacy > Privacy Preferences Policy Control**:

- Bluetooth Always

#### Android Enterprise has new values for the Allow access to all apps in Google Play store setting<!-- 28367525 -->

In an Intune device restrictions configuration policy, you can configure the **Allow access to all apps in Google Play store** setting using the **Allow** and **Not configured** options (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully managed, dedicated and corporate-owned work profile > Device restrictions** for profile type > **Applications**).

The available options are updated to **Allow**, **Block**, and **Not configured**.

There's no impact to existing profiles using this setting.

For more information on this setting and the values you can currently configure, see [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:

- Android Enterprise Fully managed, dedicated and corporate-owned work profile

### Device enrollment

#### New support for Red Hat Enterprise Linux<!-- 25160548 -->

Microsoft Intune now supports device management for Red Hat Enterprise Linux. You can enroll and manage Red Hat Enterprise Linux devices, and assign standard compliance policies, custom configuration scripts, and compliance scripts. For more information, see [Deployment guide: Manage Linux devices in Microsoft Intune](deployment-guide-platform-linux.md) and [Enrollment guide: Enroll Linux desktop devices in Microsoft Intune](deployment-guide-enrollment-linux.md).

Applies to:

- Red Hat Enterprise Linux 9
- Red Hat Enterprise Linux 8

#### New Intune report and device action for Windows enrollment attestation (public preview)<!-- 12581956 -->

Use the new device attestation status report in Microsoft Intune to find out if a device has attested and enrolled securely while being hardware-backed. From the report, you can attempt remote attestation via a new device action.

For more information, see:

- [Windows enrollment attestation](../enrollment/windows-enrollment-attestation.md)
- [Intune Reports](../fundamentals/reports.md#device-attestation-status-report)

#### Just-in-time registration and compliance remediation available for all iOS/iPadOS enrollments<!-- 27759589 -->

You can now configure just-in-time (JIT) registration and JIT compliance remediation for all Apple iOS and iPadOS enrollments. These Intune-supported features improve the enrollment experience because they can take the place of the Intune Company Portal app for device registration and compliance checks. We recommend setting up JIT registration and compliance remediation for new enrollments, and to improve the experience for existing enrolled devices. For more information, see [Set up just in time registration in Microsoft Intune](../enrollment/set-up-just-in-time-registration.md).

### Device management

#### Consolidation of Intune profiles for identity protection and account protection <!-- 24810271 -->

We have consolidated the Intune profiles that were related to identity and account protection, into a single new profile named *Account protection*. This new profile is found in the [account protection policy node of endpoint security](../protect/endpoint-security-account-protection-policy.md), and is now the only profile template that remains available when creating new policy instances for identity and account protection. The new profile includes Windows Hello for Business settings for both users and devices, and settings for Windows Credential Guard.

Because this new profile uses Intune’s unified settings format for device management, the profiles settings are also available through the settings catalog, and help to improve the reporting experience in the Intune admin center.

You can continue to use any instances of the following profile templates that you already have in place, but Intune no longer supports creating new instances of these profiles:

- **Identity protection** – previously available from *Devices* > *Configuration* > *Create* > *New Policy* > *Windows 10 and later* > *Templates* > *Identity Protection*
- **Account protection (Preview)** – previously available from *Endpoint Security* > *Account protection* > *Windows 10 and later* > *Account protection (Preview)*

Applies to:

- Windows 10
- Windows 11

#### New `operatingSystemVersion` filter property with new comparison operators (preview) <!-- 10033345 -->

There's a new `operatingSystemVersion` filter property. This property:

- Is in [public preview](public-preview.md) and still being developed. So, some features, like **Preview devices**, don't work yet.

- Should be used instead of the existing `OSVersion` property. The `OSVersion` property is being deprecated.

  When `operatingSystemVersion` is generally available (GA), the `OSVersion` property will retire, and you won't be able to create new filters using this property. Existing filters that use `OSVersion` continue to work.

- Has new comparison operators:

  - `GreaterThan`: Use for version value types.

    - Allowed values: `-gt` | `gt`
    - Example: `(device.operatingSystemVersion -gt 10.0.22000.1000)`

  - `GreaterThanOrEquals`: Use for version value types.

    - Allowed values: `-ge` | `ge`
    - Example: `(device.operatingSystemVersion -ge 10.0.22000.1000)`

  - `LessThan`: Use for version value types.

    - Allowed values: `-lt | lt`
    - Example: `(device.operatingSystemVersion -lt 10.0.22000.1000)`

  - `LessThanOrEquals`: Use for version value types.

    - Allowed values: `-le` | `le`
    - Example: `(device.operatingSystemVersion -le 10.0.22000.1000)`

For managed devices, `operatingSystemVersion` applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

For managed apps, `operatingSystemVersion` applies to:

- Android
- iOS/iPadOS
- Windows

For more information on filters and the device properties you can use, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [Filter properties](filters-device-properties.md)

#### Government community cloud (GCC) support for Remote Help for macOS devices<!-- 25568551 -->

GCC customers can now use Remote Help for macOS devices on both web app and native application.

Applies to:

- macOS 12, 13 and 14

For more information, see:

- [Remote Help on macOS](../fundamentals/remote-help-macos.md)
- [Microsoft Intune for US Government GCC service description](../fundamentals/intune-govt-service-description.md)

### Device security

#### Updated security baseline for Windows 365 Cloud PC<!-- 26504698 -->

You can now deploy the Intune security baseline for **Windows 365 Cloud PC**. This new baseline is based on Windows **version 24H1**. This new baseline version uses the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline represents the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

To view the new baselines included settings with their default configurations, see, [Windows 365 baseline settings version 24H1](../protect/security-baseline-settings-windows-365.md?pivots=win365-24h1).

### Intune apps

#### Newly available protected apps for Intune<!-- 28334000, 28157519, 28311088, 28156655, 28246919, 28246936, 28100886 -->

The following protected apps are now available for Microsoft Intune:

- Asana: Work in one place (Android) by Asana, Inc.
- Goodnotes 6 (iOS) by Time Base Technology Limited
- Riskonnect Resilience by Riskonnect, Inc.
- Beakon Mobile App by Beakon Mobile Team
- HCSS Plans: Revision control (iOS) by Heavy Construction Systems Specialists, Inc.
- HCSS Field: Time, cost, safety (iOS) by Heavy Construction Systems Specialists, Inc.
- Synchrotab for Intune (iOS) by Synchrotab, LLC

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of July 15, 2024

### Device management

#### New setting in the Device Control profile for Attack surface reduction policy<!-- 28761508 -->

We've added a new category and setting to the Device Control profile for the *Windows 10, Windows 11, and Windows Server* platform of Intune [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

The new setting is **Allow Storage Card**, and found in the new **System** category of the profile. This setting is also available from the Intune [settings catalog](../configuration/settings-catalog.md) for the Windows devices.

This setting controls whether the user is allowed to use the storage card for device storage, and can prevent programmatic access to the storage card. For more information on this new setting, see [AllowStorageCard](/windows/client-management/mdm/policy-csp-system?branch=main&branchFallbackFrom=pr-en-us-15655&WT.mc_id=Portal-fx#allowstoragecard) in the Windows documentation.

## Week of July 8, 2024

### Device management

#### Copilot in Intune now has the device query feature using Kusto Query Language (KQL) (public preview)<!-- 24874816 -->

When you use Copilot in Intune, there's a new device query feature that uses KQL.
Use this feature to ask questions about your devices using a natural language. If device query can answer your question, Copilot generates the KQL query you can run to get the data you want.

To learn more about how you can currently use Copilot in Intune, see [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md).

### Monitor and Troubleshoot

#### New actions for policies, profiles, and apps<!-- 15283153 -->

You can now remove, reinstall, and reapply individual policies, profiles, and apps for iOS/iPadOS devices and Android corporate owned devices. You can apply these actions without changing assignments or group membership. These actions are intended to help resolve customer challenges that are external to Intune. Also, these actions can help to quickly restore end user productivity.

For more information, see [Remove apps and configuration](../remote-actions/remove-apps-config.md)

### App management

#### MAC address available from the Managed Home Screen app<!-- 25994454 -->

MAC address details are now available from the **Device Information** page of the Managed Home Screen (MHS) app. For information about MHS, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### New configuration capabilities for Managed Home Screen<!-- 25013268 -->

You can now configure Managed Home Screen (MHS) to enable a virtual app-switcher button that allows end users to easily navigate between apps on their kiosk devices from MHS. You can select between a floating or swipe-up app-switcher button. The configuration key is `virtual_app_switcher_type` and the possible values are `none`, `float`, and `swipe_up`. For information related to configuring the Managed Home Screen app, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

### Device enrollment

#### Update for Apple user and device enrollments with Company Portal <!-- 27557088 -->

We've made changes to the device registration process for Apple devices enrolling with Intune Company Portal. Previously, Microsoft Entra device registration occurred during enrollment. With this change, registration occurs after enrollment.

Existing enrolled devices aren't affected by this change. For new user or device enrollments that utilize Company Portal, users must return to Company Portal to complete registration:

- For iOS users: Users with notifications enabled are prompted to return to the Company Portal app for iOS. If they disable notifications, they aren't alerted, but still need to return to Company Portal to complete registration.

- For macOS devices: The Company Portal app for macOS detects the installation of the management profile and automatically register the device, unless the user closes the app. If they close the app, they must reopen it to complete registration.

If you're using dynamic groups, which rely on device registration to work, it's important for users to complete device registration. Update your user guidance and admin documentation as needed. If you're using Conditional Access (CA) policies, no action is required. When users attempt to sign in to a CA-protected app, they are prompted to return to Company Portal to complete registration.

These changes are currently rolling out and will be made available to all Microsoft Intune tenants by the end of July. There's no change to the Company Portal user interface. For more information about device enrollment for Apple devices, see:

- [Enrollment guide: Enroll macOS devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-macos.md#device-enrollment-end-user-tasks)
- [Enrollment guide: Enroll iOS and iPadOS devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-ios-ipados.md)

## Week of June 24, 2024

### Device enrollment

#### Add corporate device identifiers for Windows<!-- 25873757 -->

Microsoft Intune now supports corporate device identifiers for devices running Windows 11, version 22H2 and later so that you can identify corporate machines ahead of enrollment. When a device that matches the model, manufacturer, and serial number criteria enrolls, Microsoft Intune marks it as a corporate device and enable the appropriate management capabilities. For more information, see [Add corporate identifiers](../enrollment/corporate-identifiers-add.md).

## Week of June 17, 2024 (Service release 2406)

### Microsoft Intune Suite

#### Endpoint Privilege Management support for MSI and PowerShell file types<!-- 25230336 -->

Endpoint Privilege Management (EPM) *elevation rules* now support the elevation of Windows Installer and PowerShell files in addition to executable files that were previously supported. The new file extensions that EPM supports include:

- .msi
- .ps1

For information about using EPM, see [Endpoint Privilege Management](../protect/epm-overview.md).

#### View the certification authority key type in Microsoft Cloud PKI properties<!-- 27032276 -->

A new Microsoft Cloud PKI property called *CA keys* is available in the admin center and shows the type of certification authority keys used for signing and encryption. The property displays one of the following values:

- HSM: Indicates the use of a hardware security module-backed key.
- SW: Indicates the use of a software-backed key.

Certification authorities created with a licensed Intune Suite or Cloud PKI standalone add-on use HSM signing and encryption keys. Certification authorities created during a trial period use software-backed signing and encryption keys. For more information about Microsoft Cloud PKI, see [Overview of Microsoft Cloud PKI for Microsoft Intune](../protect/microsoft-cloud-pki-overview.md).

### App management

#### US GCC and GCC High support for Managed Home Screen<!-- 25827679 -->

Managed Home Screen (MHS) now supports sign-in for the US Government Community (GCC), US Government Community (GCC) High, and U.S. Department of Defense (DoD) environments. For more information, see [Configure the Managed Home Screen](../apps/app-configuration-managed-home-screen-app.md) and [Microsoft Intune for US Government GCC service description](../fundamentals/intune-govt-service-description.md).

Applies to:

- Android Enterprise

#### Updates to the Managed Apps report<!-- 26711898 -->

The Managed Apps report now provides details about Enterprise App Catalog apps for a specific device. For more information about this report, see [Managed Apps report](../fundamentals/reports.md#managed-apps-report-operational).

### Device configuration

#### New settings available in the Apple settings catalog <!--27175914 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Restrictions**:

- Allow Web Distribution App Installation

**System Configuration > Font**:

- Font
- Name

##### macOS

**Privacy > Privacy Preferences Policy Control**:

- Bluetooth Always

Applies to:

- iOS/iPadOS
- macOS

#### OS Version picker available for configuring managed iOS/iPadOS DDM software updates using the settings catalog<!-- 27565292 -->

Using the [Intune settings catalog](../configuration/settings-catalog.md), you can configure Apple's declarative device management (DDM) feature to manage software updates on iOS/iPadOS devices.

When you configure a managed software update policy using the settings catalog, you can:

- Select a target OS version from a list of updates made available by Apple.
- Manually enter the target OS version, if needed.

For more information about configuring managed software update profiles in Intune, see [Use the settings catalog to configure managed software updates](../protect/managed-software-updates-ios-macos.md).

Applies to:

- iOS/iPadOS

#### Intune admin center UI updates at Devices > By platform<!-- 25104008 -->

In the Intune admin center, you can select **Devices** > **By platform**, and view the policy options for the platform you select. These platform-specific pages are updated and include tabs for navigation.

For a walkthrough of the Intune admin center, see [Tutorial: Walkthrough Microsoft Intune admin center](tutorial-walkthrough-endpoint-manager.md).

### Device enrollment

### RBAC changes to enrollment platform restrictions for Windows<!-- 25036419 -->

We've updated role-based access controls (RBAC) for all enrollment platform restrictions in the Microsoft Intune admin center. The Global Administrator and Intune Service Administrator roles can create, edit, delete, and reprioritize enrollment platform restrictions. For all other built-in Intune roles, restrictions are read-only.

**Applies to:**

- Android
- Apple
- Windows 10/11

It's important to know that with these changes:

- Scope tag behavior doesn't change. You can apply and use scope tags as usual.
- If an assigned role or permission is currently preventing a user from viewing enrollment platform restrictions, nothing changes. The user will still be unable to view enrollment platform restrictions in the admin center.

For more information, see [Create device platform restrictions](../enrollment/create-device-platform-restrictions.md).

### Device management

### Updates to replace Wandera with Jamf is complete in the Intune admin center<!-- 26525211 -->

We've completed a rebrand in the Microsoft Intune admin center to support replacing Wandera with Jamf. This includes updates to the name of the Mobile Threat Defense connector, which is now *Jamf*, and changes to the minimum required platforms to use the Jamf connector:

- Android 11 and later
- iOS / iPadOS 15.6 and later

For information about Jamf and other Mobile Threat Defense (MTD) vendors that Intune supports, see [Mobile Threat Defense partners](../protect/mobile-threat-defense.md).

### Intune apps

#### Newly available protected apps for Intune<!-- 28033401, 28035558, 27795962, 27795905, 27831146, 27795905 -->

The following protected apps are now available for Microsoft Intune:

- Atom Edge (iOS) by Arlanto GmbH
- HP Advance for Intune by HP Inc.
- IntraActive by Fellowmind
- Microsoft Azure (Android) by Microsoft Corporation
- Mobile Helix Link for Intune by Mobile Helix
- VPSX Print for Intune by Levi, Ray & Shoup, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md)

### Monitor and troubleshoot

#### View BitLocker recovery key in Company Portal apps for iOS and macOS<!-- 26615990 -->

End users can view the BitLocker recovery key for an enrolled Windows device and the FileVault recovery key for an enrolled Mac in the Company Portal app for iOS and Company Portal app for macOS. This capability will reduce helpdesk calls in the event the end user gets locked out of their corporate machines. End users can access the recovery key for an enrolled device by signing into the Company Portal app and selecting **Get recovery key**. This experience is similar to the recovery process on the Company Portal website, which also allows end users to see recovery keys.

You can prevent end users within your organization from accessing BitLocker recovery keys by configuring the **Restrict non-admin users from recovering the BitLocker keys for their owned device** setting in Microsoft Entra ID.

Applies to:

- macOS
- Windows 10/11

For more information, see:

- [Manage BitLocker policy for Windows devices with Intune](../protect/encrypt-devices.md)
- [Get recovery key for Windows](../user-help/get-recovery-key-windows.md)
- [Use FileVault disk encryption for macOS with Intune](../protect/encrypt-devices-filevault.md)
- [Get recovery key for Mac](../user-help/get-recovery-key-cpweb.md)
- [Manage device identities using the Microsoft Entra admin center](/entra/identity/devices/manage-device-identities#configure-device-settings)

### Role-based access control

#### New granular RBAC controls for Intune endpoint security<!-- 5475572 -->

We’ve begun to replace the role-based access control (RBAC) rights to endpoint security policies that are granted by the *Security baselines* permission with a series of more granular permissions for specific endpoint security tasks. This change can help you assign the specific rights your Intune admins require to do specific jobs instead of relying on either the [built-in](../fundamentals/role-based-access-control.md#built-in-roles) *Endpoint Security Manager* role or a [custom role](../fundamentals/create-custom-role.md) that includes the *Security baseline* permission. Prior to this change, the *Security baseline* permission grants rights across all endpoint security policies.

The following new RBAC permissions are available for endpoint security workloads:

- App Control for Business
- Attack surface reduction
- Endpoint detection and response

Each new permission supports the following rights for the related policy:

- Assign
- Create
- Delete
- Read
- Update
- View Reports

Each time we add a new granular permission for an endpoint security policy to Intune, those same rights are removed from the *Security baselines* permission. If you use custom roles with the *Security baselines* permission, the new RBAC permission is assigned automatically to your custom roles with the same rights that were granted through the *Security baseline* permission. This autoassignment ensures your admins continue to have the same permissions they have today.

For more information about current RBAC permissions and built-in roles, see:

- [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md)
- [Built-in role permissions for Microsoft Intune](../fundamentals/role-based-access-control-reference.md)
- [Assign role-based access controls for endpoint security policy](../protect/endpoint-security-policy.md#assign-role-based-access-controls-for-endpoint-security-policy) in *Manage device security with endpoint security policies in Microsoft Intune*.

> [!IMPORTANT]
>
> With this release, the granular permission of **Antivirus** for endpoint security policies might be temporarily visible in some Tenants. This permission is not released and isn't supported for use. Configurations of the *Antivirus* permission are ignored by Intune. When *Antivirus* becomes available to use as a granular permission, it's availability will be announced in this [What's new in Microsoft Intune](../fundamentals/whats-new.md) article.

## Week of June 3, 2024

### Device enrollment

#### New enrollment time grouping feature for devices <!-- 16902437 -->

Enrollment time grouping is a new, faster way to group devices during enrollment. When configured, Intune adds devices to the appropriate group without requiring inventory discovery and dynamic membership evaluations. To set up enrollment time grouping, you must configure a static Microsoft Entra security group in each enrollment profile. After a device enrolls, Intune adds it to the static security group and delivers assigned apps and policies.

This feature is available for Windows 11 devices enrolling via Windows Autopilot device preparation. For more information, see [Enrollment time grouping in Microsoft Intune](../enrollment/enrollment-time-grouping.md).

## Week of May 27, 2024

### Microsoft Intune Suite

#### New primary endpoint for Remote Help

To improve the experience for [Remote Help](../fundamentals/remote-help.md) on Windows, Web, and macOS devices, we have updated the primary endpoint for Remote Help:

- Old primary endpoint: `https://remoteassistance.support.services.microsoft.com`
- New primary endpoint: `https://remotehelp.microsoft.com`

If you use Remote Help and have firewall rules that block the new primary endpoint, admins and users might experience connectivity issues or disruptions when using Remove Help.

To support the new primary endpoint on Windows devices, upgrade Remote Help to version 5.1.124.0. Web and macOS devices don't require an updated version of Remote Help to make use of the new primary endpoint.

Applies to:

- macOS 11, 12, 13 and 14
- Windows 10/11
- Windows 11 on ARM64 devices
- Windows 10 on ARM64 devices
- Windows 365

For information on the newest version of Remote Help, see the *March 13, 2024* entry for [What's New for Remote Help](../fundamentals/remote-help-windows.md#march-13-2024). For information about Intune endpoints for Remote Help, see [Remote Help](../fundamentals/intune-endpoints.md#remote-help) in *Network endpoints for Microsoft Intune*.

### Device management

### Evaluate compliance of Windows Subsystem for Linux (public preview)<!-- 24557103 -->

Now in a public preview, Microsoft Intune supports compliance checks for instances of Windows Subsystem for Linux (WSL) running on a Windows host device.

With this preview you can create a custom compliance script that evaluates the required distribution and version of WSL. WSL compliance results are included in the overall compliance state of the host device.

Applies to:

- Windows 10
- Windows 11

For information about this capability, see [Evaluate compliance of Windows Subsystem for Linux (public preview)](../protect/compliance-wsl.md).

## Week of May 20, 2024 (Service release 2405)

### Device configuration

#### New settings available in the macOS settings catalog<!-- 26970197 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the macOS Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

**Microsoft AutoUpdate (MAU)**:

- Microsoft Teams (work or school)
- Microsoft Teams classic

**Microsoft Defender > Features**:

- Use Data Loss Prevention
- Use System Extensions

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:

- macOS

### Device enrollment

#### Stage Android device enrollment to reduce end-user steps<!-- 15503468 -->

To reduce the enrollment time for end users, Microsoft Intune supports device staging for Android Enterprise devices. With *device staging*, you can stage an enrollment profile and complete all related enrollment steps for workers receiving these devices:

- Corporate-owned fully managed devices
- Corporate-owned devices with a work profile

When frontline workers receive the devices, all they have to do is connect to Wi-Fi and sign in to their work account. A new *device staging token* is required to enable this feature. For more information, see [Device staging overview](../enrollment/device-staging-overview.md).

### Device management

#### End user access to BitLocker Recovery Keys for enrolled Windows devices<!-- 8077173 -->

End users can now view the BitLocker Recovery Key for enrolled Windows devices from the Company Portal website. This capability can reduce helpdesk calls in the event the end user gets locked out of their corporate machines. End users can access the recovery key for an enrolled device by signing into the Company Portal website and selecting **Show recovery key**. This experience is similar to the MyAccount website, which also allows end users to see recovery keys.

You can prevent end users within your organization from accessing BitLocker recovery keys by configuring the Microsoft Entra toggle **Restrict non-admin users from recovering the BitLocker key(s) for their owned device**.

For more information, see:

- [Manage device identities using the Microsoft Entra admin center](/entra/identity/devices/manage-device-identities#configure-device-settings)
- [Get recovery key for Windows](../user-help/get-recovery-key-windows.md)
- [Manage BitLocker policy for Windows devices with Intune](../protect/encrypt-devices.md)

#### New version of Windows hardware attestation report<!-- 15425680 -->

We've released a new version of the Windows hardware attestation report that shows the value of settings attested by Device Health Attestation and Microsoft Azure Attestation for Windows 10/11. The Windows hardware attestation report is built on a new reporting infrastructure, and reports on new settings added to Microsoft Azure Attestation. The report is available in the admin center under **Reports** > **Device Compliance** > **Reports**.

For more information, see [Intune reports](reports.md#windows-hardware-attestation-report-organizational).

The Windows health attestation report previously available under **Devices** > **Monitor** has been retired.

Applies to:

- Windows 10
- Windows 11

#### Optional Feature updates<!--12769586 -->

Feature updates can now be made available to end users as **Optional** updates, with the introduction of **Optional** Feature updates. End users see the update in the **Windows Update** settings page in the same way that it's shown for consumer devices.

End users can easily opt in to try out the next Feature update and provide feedback. When it's time to roll out the feature as a **Required** update, then admins can change the setting on the policy, and update the rollout settings so that the update is deployed as a **Required** update to devices that don't yet have it installed.

For more information on Optional Feature updates, see [Feature updates for Windows 10 and later policy in Intune](..//protect/windows-10-feature-updates.md#create-and-assign-feature-updates-for-windows-10-and-later-policy).

Applies to:

- Windows 10
- Windows 11

### Device security

#### Updated security baseline for Microsoft Defender for Endpoint<!-- 26504935 -->

You can now deploy the Intune security baseline for **Microsoft Defender for Endpoint**. The new baseline, **version 24H1**, uses the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline represents the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

### Intune apps

#### Newly available protected apps for Intune<!-- 27575008, 27575336 -->

The following protected apps are now available for Microsoft Intune:

- Fellow.app by Fellow Insights Inc
- Unique Moments by Unique AG

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of May 6, 2024

### Device management

#### Intune and the macOS Company Portal app support Platform SSO (public preview)<!-- 24325427 -->

On Apple devices, you can use Microsoft Intune and the Microsoft Enterprise SSO plug-in to configure single sign-on (SSO) for apps and websites that support Microsoft Entra authentication, including Microsoft 365.

On macOS devices, Platform SSO is available in public preview. Platform SSO expands the SSO app extension by allowing you to configure different authentication methods, simplify the sign-in process for users, and reduce the number of passwords they need to remember.

Platform SSO is included in the Company Portal app version 5.2404.0 and newer.

For more information on Platform SSO and to get started, see:

- [Configure Platform SSO for macOS devices in Microsoft Intune](../configuration/platform-sso-macos.md)
- [Single sign-on (SSO) overview and options for Apple devices in Microsoft Intune](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)

Applies to:

- macOS 13 and later

### Tenant administration

#### Customize your Intune admin center experience<!-- 24155584 -->

You can now customize your Intune admin center experience by using collapsible navigation and favorites. The left navigation menus in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) are updated to support expanding and collapsing each subsection of the menu. In addition, you can set admin center pages as favorites. This portal capability will gradually roll out over the next week.

By default, menu sections are expanded. You can choose your portal menu behavior by selecting the **Settings** gear icon at the top right to display the **Portal settings**. Then, select **Appearance + startup views** and set the **Service menu behavior** to **Collapsed** or **Expanded** as the default portal option. Each menu section retains the expanded or collapsed state that you choose. Additionally, selecting the star icon next to a page on the left navigation adds the page to a **Favorites** section near the top of the menu.

For related information, see [Change the Portal settings](../fundamentals/tutorial-walkthrough-endpoint-manager.md#change-the-portal-settings).

## Week of April 29, 2024

### App management

#### Updates to the Managed Home Screen experience<!-- 24990268 -->

We recently released and improved the Managed Home Screen experience, which is now Generally Available. The app is redesigned to improve the core workflows throughout the application. The updated design offers a more usable and supportable experience.

With the release, we stop investing in previous Managed Home Screen workflows. New features and fixes for Managed Home Screen are only added to the new experience. During August 2024, the new experience is automatically enabled for all devices.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md) and [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

#### Require end users to enter PIN to resume activity on Managed Home Screen<!-- 9322838 -->

In Intune, you can require end users to enter their session PIN to resume activity on Managed Home Screen after the device is inactive for a specified period of time. Set the **Minimum inactive time before session PIN is required** setting to the number of seconds the device is inactive before the end user must input their session PIN.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Device IPv4 and IPv6 details available from Managed Home Screen<!-- 25994445 -->

IPv4 and IPv6 connectivity details are now both available from the **Device Information** page of the Managed Home Screen app. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](..\remote-actions\collect-diagnostics.md).

#### Updates to Managed Home Screen sign-in support<!-- 25597636 -->

Managed Home Screen now supports domainless sign-in. Admins can configure a domain name, which will be automatically appended to usernames upon sign-in. Also, Managed Home Screen supports a custom login hint text to be displayed to users during the sign-in process.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md) and [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

#### Allow end users to control Android Enterprise device auto-rotation<!-- 9322838 -->

In Intune, you can now expose a setting in the Managed Home Screen app that allows the end user to turn on and off the device's auto-rotation. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Allow end users to adjust Android Enterprise device screen brightness<!-- 9322834 -->

In Intune, you can expose settings in the Managed Home Screen app to adjust screen brightness for Android Enterprise devices. You can choose to expose a setting in the app to allow end users to access a brightness slider to adjust the device screen brightness. Also, you can expose a setting to allow end users to toggle adaptive brightness.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Migrated to .NET MAUI from Xamarin<!-- 27143739 -->

Xamarin.Forms has evolved into .NET Multi-platform App UI (MAUI). Existing Xamarin projects should be migrated to .NET MAUI. For more information about upgrading Xamarin projects to .NET, see the [Upgrade from Xamarin to .NET & .NET MAUI](/dotnet/maui/migration/?WT.mc_id=dotnet-35129-website) documentation.

Xamarin support ended as of May 1, 2024 for all Xamarin SDKs including Xamarin.Forms and Intune App SDK Xamarin Bindings. For Intune support on Android and iOS platforms, see [Intune App SDK for .NET MAUI - Android](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android)and [Microsoft Intune App SDK for MAUI.iOS](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS).

## Week of April 22, 2024 (Service release 2404)

### App management

#### Auto update available with Win32 app supersedence<!-- 17644510 -->

Win32 app supersedence provides the capability to supersede apps deployed as available with **auto-update** intent. For example, if you deploy a Win32 app (app A) as available and installed by users on their device, you can create a new Win32 app (app B) to supersede app A using **auto-update**. All targeted devices and users with app A installed as available from the Company Portal are superseded with app B. Also, only app B shows in the Company Portal. You can find the **auto-update** feature for available app supersedence as a toggle under the **Available assignment** in the **Assignments** tab.

For more information about app supersedence, see [Add Win32 app supersedence](../apps/apps-win32-supersedence.md).

### Device configuration

#### Error message is shown when OEMConfig policy exceeds 500 KB on Android Enterprise devices<!-- 15326924 -->

On Android Enterprise devices, you can use an OEMConfig device configuration profile to add, create and/or customize OEM specific settings.

When you create an OEMConfig policy that exceeds 500 KB, then the following error is shown in the Intune admin center:

`Profile is larger than 500KB. Adjust profile settings to decrease the size.`

Previously, OEMConfig policies that exceeded 500 KB were shown as pending.

For more information on OEMConfig profiles, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Applies to:

- Android Enterprise

### Device security

#### Windows Firewall CSP changes for processing Firewall Rules<!-- 10734904 -->

Windows changed how the Firewall configuration service provider (CSP) enforces rules from Atomic blocks of firewall rules. The Windows Firewall CSP on a device implements the firewall rule settings from your [Intune endpoint security Firewall policies](../protect/endpoint-security-firewall-policy.md). The change of CSP behavior now enforces an all-or-nothing application of firewall rules from each Atomic block of rules.

- Previously, the CSP on a device would go through the firewall rules in an Atomic block of rules - one rule (or setting) at a time with the goal of applying all the rules in that Atomic block, or none of them. If the CSP encountered any issue with applying any rule from the block to the device, the CSP wouldn't only stop that rule, but also cease to process subsequent rules without trying to apply them. However, rules that applied successfully before a rule failed, would remain applied to the device. This behavior can lead to a partial deployment of firewall rules on a device, since the rules that were applied before a rule failed to apply aren't reversed.

- With the change to the Firewall CSP, when any rule in the block is unsuccessful in applying to the device, all the rules from that same Atomic block that were applied successfully are rolled back. This behavior ensures the desired all-or-nothing behavior is implemented and prevents a partial deployment of firewall rules from that block. For example, if a device receives an Atomic block of firewall rules that has a misconfigured rule that can't apply, or has a rule that isn't compatible with the devices operating system, then the CSP fails all the rules from that block, And, it rolls back any rules that applied to that device.

This change of Firewall CSP behavior is available on devices that run the following Windows versions or later:

- Windows 11 21H2
- Windows 11 22H2
- Windows 10 21H2

For more information on the subject of how the Windows Firewall CSP uses Atomic blocks to contain firewall rules, see the note near the top of [Firewall CSP](/windows/client-management/mdm/firewall-csp) in the Windows documentation.

For troubleshooting guidance, see the Intune support blog [How to trace and troubleshoot the Intune Endpoint Security Firewall rule creation process](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-trace-and-troubleshoot-the-intune-endpoint-security/ba-p/3261452).

#### CrowdStrike – New mobile threat defense partner<!-- 16882021 -->

We added [CrowdStrike Falcon](../protect/crowdstrike-falcon-defense-connector.md) as an integrated Mobile Threat Defense (MTD) partner with Intune. By configuring the CrowdStrike connector in Intune, you can control mobile device access to corporate resources using Conditional Access that's based on risk assessment in your compliance policies.

With the Intune 2404 service release, the CrowdStrike connector is now available in the admin center. However, it isn't useable until CrowdStrike publishes the required App Configuration profile details necessary to support iOS and Android devices. The profile details are expected sometime after second week of May.

### Intune apps

#### Newly available protected apps for Intune<!-- 26825160, 26954999, 26891466, 27184602 -->

The following protected apps are now available for Microsoft Intune:

- Asana: Work in one place by Asana, Inc.
- Freshservice for Intune by Freshworks, Inc.
- Kofax Power PDF Mobile by Tungsten Automation Corporation
- Remote Desktop by Microsoft Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Windows update distribution report<!--16579592 -->

The Windows update distribution report in Intune provides a summarized report. This report shows:

- The number of devices that are on each quality update level.
- The percentage of coverage for each update across Intune managed devices, including co-managed devices.

You can drill down further in the report for each quality update that aggregates devices based on the Windows 10/11 feature version and the update statuses.

Finally, the admins can get the list of devices that aggregate to the numbers shown in the previous two reports, which can also be exported and used for troubleshooting and analysis along with the Windows Update for business reports.

For more information on Windows update distribution reports, see [Windows Update reports on Intune](../protect/windows-update-reports.md#windows-update-distribution-report).

Applies to:

- Windows 10
- Windows 11

#### Intune support of Microsoft 365 remote application diagnostics<!-- 17409991 -->

The Microsoft 365 remote application diagnostics allows Intune admins to request Intune app protection logs and Microsoft 365 application logs (where applicable) directly from the Intune console. You can find this report in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Troubleshoot** > *select a user* > **Summary** > *App protection**. This feature is exclusive to applications that are under Intune app protection management. If supported, the application specific logs are gathered and stored within dedicated storage solutions for each application.

For more information, see [Collect diagnostics from an Intune managed device](../remote-actions/collect-diagnostics.md).

#### Remote Help supports full control of a macOS device<!--22985205 -->

Remote Help now supports helpdesk connecting to a user's device and requesting full control of the macOS device.

For more information, see:

- [Remote Help on macOS](../fundamentals/remote-help-macos.md)
- [Remote Help Web App](../fundamentals/remote-help-webapp.md)

Applies to:

- macOS 12, 13 and 14

## What's new archive
<!-- Past announcements that are older than six months will be moved to the archive -->

For previous months, see the [What's new archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
