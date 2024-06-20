---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 06/14/2024
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

<!-- ## Microsoft Intune Suite -->

## App management

### New actions for policies, profiles, and apps<!-- 15283153 -->

You'll be able to remove, reinstall, and reapply individual policies, profiles, and apps for iOS/iPadOS devices and Android corporate owned devices. You'll be able to apply these actions without changing assignments or group membership. These actions are intended to help resolve customer challenges that are external to Intune. Also, these actions can help to quickly restore end user productivity.

Applies to:

- iOS/iPadOS
- Android Enterprise corporate owned devices

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies now provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

<<<<<<< HEAD
<!-- ## Device configuration -->
=======
## Device configuration

### Version picker available for configuring managed Apple DDM software updates using the settings catalog<!-- 27565292 -->

Using the [Intune settings catalog](../configuration/settings-catalog.md), you can configure Apple's declarative device management (DDM) feature to manage software updates on iOS/iPadOS and macOS devices.

When you configure a managed software update policy using the settings catalog, you'll be able to:

- Select a target OS version from a list of updates made available by Apple.
- Manually enter the target OS version, if needed.

For more information about configuring managed software update profiles in Intune, see [Use the settings catalog to configure managed software updates](../protect/managed-software-updates-ios-macos.md).

Applies to:

- iOS/iPadOS
- macOS

### Intune admin center UI updates at Devices > By platform<!-- 25104008 -->

In the Intune admin center, you can select **Devices** > **By platform**, and view the policy options for the platform you select. These platform-specific pages are being updated and will include tabs for navigation.

### New settings available in the Apple settings catalog <!--27175914 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There will be new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

#### iOS/iPadOS

**Restrictions**:

- Allow Web Distribution App Installation

**System Configuration > Font**:

- Font
- Name

#### macOS

**Privacy > Privacy Preferences Policy Control**:

- Bluetooth Always

Applies to:

- iOS/iPadOS
- macOS
>>>>>>> 65b3a6828c8042b75f1782932bfa6a8b6f1e2519

<!-- *********************************************** -->

## Device enrollment

### Define corporate device identifiers for Windows<!-- 25873757 -->

Microsoft Intune will support corporate device identifiers for Windows devices. You'll be able to upload a CSV file with model, manufacturer, and serial number to identify corporate machines ahead of enrolling. When a device that matches the model, manufacturer, and serial number criteria enrolls, it will be marked as corporate and managed appropriately.

### Intune adding support for Red Hat Enterprise Linux<!-- 25160548 -->

Microsoft Intune will support device management for Red Hat Enterprise Linux. You'll be able to enroll and manage Red Hat Enterprise Linux devices, and assign standard compliance policies, custom configuration scripts, and compliance scripts.

Applies to:

- Red Hat Enterprise Linux 9
- Red Hat Enterprise Linux 8

### Account-driven Apple User Enrollment to be generally available for iOS/iPadOS 15+ devices<!-- 10277062 -->

Intune will support account-driven Apple User Enrollment, the new and improved version of Apple User Enrollment, for devices running iOS/iPadOS 15 and later. This new enrollment method utilizes just-in-time registration, removing the Company Portal app for iOS as an enrollment requirement. Device users will be able to initiate enrollment directly in the Settings app, resulting in a shorter and more efficient onboarding experience. For more information, see [Set up account driven Apple User Enrollment](../enrollment/apple-account-driven-user-enrollment.md) on Microsoft Learn.

If you prefer, you can continue to target iOS/iPadOS devices using the Apple User Enrollment method that requires Company Portal. Devices running iOS/iPadOS 14.8.1 and earlier will be unaffected by this update and can continue to use the method with Company Portal.

Applies to:

- iOS/iPadOS 15 and later

<!-- *********************************************** -->

<!-- ## Device management  -->

<!-- *********************************************** -->

## Device security

### Defender for Endpoint security settings support in government cloud environments<!-- 24191406 -->

Customer tenants in US Government Community (GCC) High, and Department of Defense (DoD) environments will soon be able to use Intune to manage the Defender security settings on the devices you’ve onboarded to Defender without enrolling those devices with Intune. This capability is known as [Defender for Endpoint security settings management](/intune/protect/mde-security-integration).

For more information about the Intune features supported in GCC High and DoD environments, see [Intune US Government service description](/intune/fundamentals/intune-govt-service-description).

### Updated security baseline for Windows 365 Cloud PC<!-- 26504698 -->

We're working on an update to the Intune security baseline for **Windows 365 Cloud PC**. The new baseline version uses the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline represents the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

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

<!-- ## Monitor and troubleshoot  -->
 
<!-- *********************************************** -->

<!-- ## Tenant administration -->

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
