---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 07/08/2024
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

### New actions for Microsoft Cloud PKI<!-- 24231040 -->

The following actions will be added to Microsoft Cloud PKI:

- Delete: Delete a certification authority (CA).
- Pause: Temporarily suspend use of a CA.
- Revoke a CA certificate: Revoke a CA certificate.

You’ll be able to access all new actions in the Microsoft Intune admin center and Graph API.

## App management

### Intune will support additional macOS app types from the Company Portal<!-- 26133163 -->

Intune will support the ability to deploy DMG and PKG apps as **Available** in the Intune macOS Company Portal. This capability enables end users to browse and install agent-deployed applications using Company Portal for macOS.

Applies to:

- macOS

### The Intune App SDK and Intune App Wrapping Tool are moving to a different GitHub repo<!-- 27264674, 27264632 -->

The Intune App SDK and Intune App Wrapping Tool are moving to a different GitHub repository and a new account. There will be redirects in place for all existing repositories. In addition, the Intune sample applications are also included in this move. This change relates to both Android and iOS platforms.

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies now provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

## Device configuration

### New settings available in the Apple settings catalog<!-- 28052449 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

#### iOS/iPadOS

**Restrictions**:

- Allow Auto Dim

#### macOS

**Privacy > Privacy Preferences Policy Control**:

- Bluetooth Always

### Allow access to all apps in Google Play store setting values are changing for Android Enterprise<!-- 28367525 -->

In an Intune device restrictions configuration policy, you can configure the **Allow access to all apps in Google Play store** setting using the **Allow** and **Not configured** options (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully managed, dedicated and corporate-owned work profile > Device restrictions** for profile type > **Applications).

The available options are being updated to **Allow**, **Block**, and **Not configured**.

There's no impact to existing profiles using this setting.

For more information on this setting and the values you can currently configure, see [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:

- Android Enterprise Fully managed, dedicated and corporate-owned work profile


<!-- *********************************************** -->

## Device enrollment

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

## Device management

### Copilot in Intune will have device query feature using Kusto Query Language (KQL) (public preview)<!-- 24874816 -->

When you use Copilot in Intune, there's a new device query feature that uses KQL.

Use this feature to ask questions about your devices using a natural language. If device query can answer your question, Copilot generates the KQL query you can run to get the data you want.

To learn more about how you can currently use Copilot in Intune, see [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md).

### Changes for Account Protection policies<!-- 24810271 -->

Account Protection policies can help you protect the credentials of your users, and focus on settings for Windows Hello and Credential Guard, which are part of Windows identity and access management.

To help improve Intune Account Protection policies, we will be removing older templates that use an outdated settings format, and consolidating Account Protection management through use of a single new profile. The settings in the new profile will use the newer unified settings format for device management, be available through the settings catalog, and help to improve the reporting experience in the Intune admin center.

The new profile will be found in the account protection policy node of endpoint security, and will be named *Account Protection*. With this profile you’ll be able to manage the same settings as before, though the new profile will present updated names and options for those settings.

The old profile we're removing is the *Account Protection (Preview)* template that's available through endpoint security Account Protection policy.

For more information about this type of policy, see [Manage device security with endpoint security policies](../protect/ endpoint-security-account-protection-policy.md).

Applies to:

- Windows 10
- Windows 11

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

### New `operatingSystemVersion` filter property with new comparison operators (preview)<!-- 10033345 -->

There's a new `operatingSystemVersion` filter property. This property:

- Is in [public preview](public-preview.md) and still being developed. So, some features, like **Preview devices**, don't work yet.

- Should be used instead of the existing `OSVersion` property. The `OSVersion` property is being deprecated. When `operatingSystemVersion` is generally available (GA), the `OSVersion` property will retire, and you won't be able to create new filters using this property. Existing filters that use `OSVersion` continue to work.

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

For more information on filters and the device properties you can currently use, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [Filter properties](filters-device-properties.md)

### Government community cloud (GCC) support for Remote Help for macOS devices<!-- 25568551 -->

GCC customers will soon be able to use Remote Help for macOS devices on both web app and native application.

Applies to:

- macOS 12, 13 and 14

For more information, see:

[Remote Help on macOS](../fundamentals/remote-help-macos.md)
[Microsoft Intune for US Government GCC service description](../fundamentals/intune-govt-service-description.md)

<!-- *********************************************** -->

## Device security

### Defender for Endpoint security settings support in government cloud environments<!-- 24191406 -->

Customer tenants in US Government Community (GCC) High, and Department of Defense (DoD) environments will soon be able to use Intune to manage the Defender security settings on the devices you’ve onboarded to Defender without enrolling those devices with Intune. This capability is known as [Defender for Endpoint security settings management](../protect/mde-security-integration.md).

For more information about the Intune features supported in GCC High and DoD environments, see [Intune US Government service description](../fundamentals/intune-govt-service-description.md).

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

<!-- ## Monitor and troubleshoot -->
 
<!-- *********************************************** -->

<!-- ## Tenant administration -->

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
