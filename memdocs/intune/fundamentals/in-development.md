---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 08/12/2024
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

### Easy creation of Endpoint Privilege Management elevation rules based on support approval requests<!-- 28196775 -->

You’ll soon be able to create Endpoint Privilege Management (EPM) elevation rules directly from a support approval request or from details found in the Elevation report. This new process will replace the need to manually enter details about an elevation and how it should be managed, and supports creation of a new rules policy or adding the new rules to an existing policy.

Applies to:

- Windows 10
- Windows 11

For information about using EPM, see [Endpoint Privilege Management overview](../protect/epm-overview.md).

### Resource performance report for physical devices in Advanced Analytics<!-- 12659827 -->

We're introducing a Resource performance report for Windows physical devices in Intune Advanced Analytics. The report will be included as an Intune-add on under Microsoft Intune Suite.

The resource performance scores and insights for physical devices are aimed to help IT admins make CPU/RAM asset management and purchase decisions that improve the user experience while balancing hardware costs.

For more information, see [Microsoft Intune Suite](../fundamentals/intune-add-ons.md).

## App management

### Managed Home Screen for Android Enterprise Fully Managed devices<!-- 15603355 -->

Managed Home Screen (MHS) will be supported on Android Enterprise Fully Managed devices. This capability will offer organizations the ability to leverage MHS in scenarios where a device is associated with a single user.

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies now provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

## Device configuration

### Enhancements to multiple administrative approval <!-- 25174473 -->

Multi administrative approval (MAA) adds the ability to limit application access policies to Windows applications or all non-Windows applications or both. We're adding a new access policy to the multiple administrative approval feature.

For more information, see [multiple admin approval](../fundamentals/multi-admin-approval.md).

### New settings available in the Apple settings catalog <!-- 28308531 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Apple Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

#### iOS/iPadOS

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
- Allow Personalized Handwriting Results
- Allow Video Conferencing Remote Control
- Allow Genmoji
- Allow Image Playground
- Allow Image Wand
- Allow iPhone Mirroring
- Allow Writing Tools

#### macOS

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

<!-- *********************************************** -->

## Device enrollment  

### Use corporate Microsoft Entra account to enable Android Enterprise management options in Intune<!-- 25231452 -->  

Managing Intune-enrolled devices with Android Enterprise management options currently requires you to connect your Intune tenant to your managed Google Play account using a personal Gmail account. Soon you will be able to use a corporate Microsoft Entra account to establish the connection. This change is happening in new tenants, and doesn't affect tenants that have already established a connection. 

### Support ending for Apple User Enrollment with Company Portal<!-- 28361917 -->

After the release of iOS/iPadOS 18, Apple will no longer support profile-based Apple User Enrollment. As a result, Intune will end support for [user enrollment with Company Portal](../enrollment/apple-user-enrollment-with-company-portal.md) shortly after the release of iOS/iPadOS 18.

After Intune ends support for user enrollment with Company Portal:

- Existing enrolled devices won't be impacted.
- Users won't be able to enroll devices if they're targeted with this enrollment profile type.
- Microsoft Intune technical support will be available for existing enrolled devices with this enrollment profile type. Technical support won't be available for new enrollments.

To prepare, use a different management method to enroll devices. We recommend account-driven Apple User Enrollment for similar functionality and an improved user experience. For a simpler enrollment experience, try web- based device enrollment. For more information, see:

- [Set up account-driven Apple User Enrollment](../enrollment/apple-account-driven-user-enrollment.md)
- [Set up web-based device enrollment for iOS/iPadOS](../enrollment/web-based-device-enrollment-ios.md)  

### Account-driven Apple User Enrollment to be generally available for iOS/iPadOS 15+ devices<!-- 10277062 -->

Intune will support account-driven Apple User Enrollment, the new and improved version of Apple User Enrollment, for devices running iOS/iPadOS 15 and later. This new enrollment method utilizes just-in-time registration, removing the Company Portal app for iOS as an enrollment requirement. Device users will be able to initiate enrollment directly in the Settings app, resulting in a shorter and more efficient onboarding experience. For more information, see [Set up account driven Apple User Enrollment](../enrollment/apple-account-driven-user-enrollment.md) on Microsoft Learn.

If you prefer, you can continue to target iOS/iPadOS devices using the Apple User Enrollment method that requires Company Portal. Devices running iOS/iPadOS 14.8.1 and earlier will be unaffected by this update and can continue to use the method with Company Portal.

Applies to:

- iOS/iPadOS 15 and later

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
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, go to [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

Applies to:

- iOS/iPadOS

### 21 Vianet support for Mobile Threat Defense connector support on 21Vianet<!-- 10355489 -->

Intune operated by 21Vianet will soon support Mobile Threat Defense (MTD) connectors for Android and iOS/iPadOS devices for MTD vendors that also have support in that environment. When an MTD partner is supported and you sign in to a 21Vianet tenant, the supported connectors will be available.

Applies to:

- Android
- iOS/iPadOS

For more information, see:

- [Intune operated by 21Vianet in China](../fundamentals/china.md)
- [Mobile Threat Defense integration with Intune](../protect/mobile-threat-defense.md)

### New `cpuArchitecture` filter device property for app and policy assignments<!-- 7423106 -->

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

<!-- *********************************************** -->

## Device security

### Target Date Time setting for Apple software update enforcement will schedule updates using the local time on devices <!-- 28865232 -->

You will be able to specify the time that OS updates are enforced on devices in their local time zone. For example, configuring an OS update to be enforced at 5pm will schedule the update for 5pm in the device's local time zone. Currently, this setting uses the time zone that the policy is configured.

This change will only apply to new policies that are created in the August 2408 release and later. The **Target Date Time** setting is in the settings catalog at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type > **Declarative Device Management** > Software Update.

In a future release, the **UTC** text will be removed from the **Target Date Time** setting.

For more information on using the settings catalog to configure software updates, see [Managed software updates with the settings catalog](../protect/managed-software-updates-ios-macos.md).

Applies to:

- iOS/iPadOS
- macOS

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
