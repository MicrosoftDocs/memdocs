---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 07/28/2022
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
  - M365-identity-device-management
  - highpri
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. In addition to the information in this article:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description will move from this article to [What's new](whats-new.md).  
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](whats-new.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control

-->

<!-- ***********************************************-->

## App management

### Noncompliance details available for Android (AOSP) in Microsoft Intune app<!-- 12645770 -->
Android (AOSP) users will be able to view the reasons why devices are marked as noncompliant in the Microsoft Intune app. This information will be available in the Intune app for devices enrolled as user-associated Android (AOSP) devices.

### Android strong biometric change detection<!-- 9740832 -->
The Android **Fingerprint instead of PIN for access** setting in Intune, which allows the end-user to use [fingerprint authentication](https://developer.android.com/about/versions/marshmallow/android-6.0.html#fingerprint-authentication) instead of a PIN, is being modified. This change will allow you to require end-users to set strong biometrics, as well as require end-users to confirm their app protection policy (APP) PIN if a change in strong biometrics is detected. You can find Android app protection polices in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **App protection policies** > **Create policy** > **Android**.

### New app types for Microsoft Endpoint Manager<!-- 7210233 -->
As an admin, you will be able to create and assign two new types of Intune apps:
- **iOS/iPadOS web clip** 
- **Windows web link**

These new app types work in a similar way to the existing **web link** application type, however they apply only for their specific platform, whereas web link applications apply across all platforms. With these new app types, you can assign to groups and also use assignment filters to limit the scope of assignment. You will find this functionality in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), by selecting **Apps** > **All Apps** > **Add**.

<!-- ***********************************************-->

## Device management

### View contents of macOS shell scripts and custom attributes<!-- 14757037 -->
You'll be able to view the contents of macOS shell scripts and custom attributes after you upload these to Intune. When this capability is available, you'll be able to view Shell scripts and custom attributes in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **macOS**. For related information, see [Use shell scripts on macOS devices in Intune](../apps/macos-shell-scripts.md).

### Intune moving to support iOS/iPadOS 16 and higher later this year<!-- 14778947 -->
Later this year, Apple is expected to release iOS/iPadOS 16. Due to this expected release, Microsoft Intune and the Intune Company Portal will require iOS/iPadOS 14 and higher shortly after the release of iOS/iPad 16. For related information, see [Supported operating systems and browsers in Intune](../fundamentals/supported-devices-browsers.md).

### Intune moving to support macOS 11.6 and higher later this year<!-- 14766663 -->
With Apple's expected release of macOS 13 Ventura later this year, Microsoft Intune, the Company Portal app, and the Intune MDM agent will be moving to support macOS 11.6 (Big Sur) and later. For related information, see [Supported operating systems and browsers in Intune](../fundamentals/supported-devices-browsers.md).

<!-- ***********************************************-->

## Device configuration

### iOS/iPadOS settings catalog will support declarative device management<!-- 15016105 -->
On iOS/iPadOS 15+ devices enrolled using [User Enrollment](../enrollment/ios-user-enrollment.md), the settings catalog will be able use Apple’s declarative device management (DDM) when configuring settings.

- No action is required to use DDM. The feature will be built into the settings catalog.
- There is no impact to existing policies in the settings catalog.
- iOS/iPadOS devices that aren't enabled for DDM will continue to use Apple’s standard MDM protocol.

For more information, go to:
- [Meet declarative device management](https://aka.ms/DDM2021) (opens Apple's web site)
- [Microsoft simplifies Endpoint Manager enrollment for Apple updates](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/microsoft-simplifies-endpoint-manager-enrollment-for-apple/ba-p/3570319)
- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md)

Applies to:
-  iOS/iPadOS 15 or later devices enrolled using Apple User Enrollment

### New macOS settings available in the Settings Catalog <!-- 15020250 -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. There are new settings are available in the Settings Catalog (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type).

New settings include:

**Microsoft Auto Update**:

- Current Channel
- Number of minutes for the final countdown timer

**Restrictions**:

- Allow Universal Control

The following settings are also in Settings Catalog. Previously, they were only available in Templates:

**Authentication > Extensible Single Sign On**:

- Extension Data
- Extension Identifier
- Hosts
- Realm
- Screen Locked Behavior
- Team Identifier
- Type
- URLs

**Authentication > Extensible Single Sign On > Extensible Single Sign On Kerberos**:

- Extension Data
- Allow Automatic Login
- Allow Password Change
- Credential Bundle ID ACL
- Credential Use Mode
- Custom Username Label
- Delay User Setup
- Domain Realm Mapping
- Help Text
- Include Kerberos Apps In Bundle ID ACL
- Include Managed Apps In Bundle ID ACL
- Is Default Realm
- Monitor Credentials Cache
- Perform Kerberos Only
- Preferred KDCs
- Principal Name
- Password Change URL
- Password Notification Days
- Password Req Complexity
- Password Req History
- Password Req Length
- Password Req Min Age
- Password Req Text
- Require TLS For LDAP
- Require User Presence
- Site Code
- Sync Local Password
- Use Site Auto Discovery
- Extension Identifier
- Hosts
- Realm
- Team Identifier
- Type

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:
- macOS

### New iOS/iPadOS settings in the Settings Catalog<!-- 15020319 -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. There are new iOS/iPadOS settings available in the Settings Catalog (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Settings catalog** for profile type). Previously, these settings were only available in Templates:

**Authentication > Extensible Single Sign On**:

- Extension Data
- Extension Identifier
- Hosts
- Realm
- Screen Locked Behavior
- Team Identifier
- Type
- URLs

**Authentication > Extensible Single Sign On > Extensible Single Sign On Kerberos**:

- Extension Data
- Allow Automatic Login
- Credential Bundle ID ACL
- Domain Realm Mapping
- Help Text
- Include Managed Apps In Bundle ID ACL
- Is Default Realm
- Preferred KDCs
- Principal Name
- Require User Presence
- Site Code
- Use Site Auto Discovery
- Extension Identifier
- Hosts
- Realm
- Team Identifier
- Type

**System Configuration > Lock Screen Message**:
- Asset Tag Information
- Lock Screen Footnote

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:
- iOS/iPadOS

### SCEP certificate profile support for Android (ASOP) devices<!-- 8506336 -->
To expand our support for the Android Open Source Project (AOSP) platform, you’ll soon be able to deploy Simple Certificate Enrollment Protocol (SCEP) certificate profiles to corporate-owned and userless devices. In Intune, you can find this functionality in **Devices** > **Configuration profiles** > **Create profile** > **Android (AOSP)**.

This expands on the [certificate profile support](../fundamentals/whats-new.md#certificate-profiles-support-for-android-asop-devices) that was added in June of 2022.

### Filter on the user scope or device scope in the Settings Catalog for Windows devices<!-- 13949975 -->
When you create a Settings Catalog policy, you can use **Add settings** > **Add filter** to filter settings based on the Windows OS edition (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Settings Catalog (preview)** for profile type).

When you **Add filter**, you'll be able to filter on the settings by user scope or device scope.

For more information, go to [Use the settings catalog to configure settings: Device scope vs. user scope settings](../configuration/settings-catalog.md#device-scope-vs-user-scope-settings)

Applies to:
- Windows 10
- Windows 11

### Import custom ADMX and ADML administrative templates to create a device configuration profile<!-- 4970862 -->
You can create a device configuration policy that uses built-in ADMX templates (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Administrative templates**).

You'll be able to import custom and 3rd party/partner ADMX and ADML templates into the Endpoint Manager admin center. Once imported, you can create a device configuration policy, assign the policy to your devices, and manage the settings in the policy.

For information on the built-in ADMX templates, see [Use Windows 10/11 templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md).

Applies to:
- Windows 11
- Windows 10

<!-- ***********************************************-->

## Device security

### Disable use of UDP connections on your Microsoft Tunnel Gateway servers<!-- 9295335 -->
You’ll soon be able to configure your Microsoft Tunnel Servers to disable use of UDP. When you disable use of UDP, the VPN server supports only TCP connections from tunnel clients. To support use of only TCP connections, your devices must use the generally available version of [Microsoft Defender for Endpoint as the Microsoft Tunnel client app](../protect/microsoft-tunnel-migrate-app.md) as the tunnel client app.

You’ll be able to disable UDP when creating or editing a *Server configuration* for Microsoft Tunnel Gateway. The Server configuration will support a new option named **Disable UDP Connections** that will be available for the *Server port* field.  [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant Administration** > **Microsoft Tunnel Gateway** > **Server configurations**.

### Reusable groups of settings for Microsoft Defender Firewall Rules<!-- 5653346, 6009514 -->
 
You’ll soon be able to add reusable groups of settings to your profiles for Microsoft Defender Firewall Rules. The reusable groups are collections of remote IP addresses and FQDNs that you define one time and can then use with one or more firewall rule profiles. You’ll no longer need to reconfigure the same group of IP addresses in each individual profile that might require them.  

Features of the reusable settings groups will include:  
- Add one or more remote IP addresses.  
- Add one or more FQDNs that can auto resolve to the remote IP address, or for one or more simple keywords when auto resolve for the group is off.  
- Use each settings group with one or more firewall rule profiles and the different  profiles can support different access configurations for the group.  

  For example, you can create two firewall rule profiles that reference the same reusable settings group and assign each profile to a different group of devices. The first profile can block access to all the remote IP addresses in the reusable settings group, while the second profile can be configured to allow access.  

- Edits to a settings group that's in use are automatically applied to the Firewall Rules profiles that use that group.  
  
Reusable groups will be configured on a new Tab for *Reusable settings* that will be available when you view endpoint security Firewall policy.  In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Endpoint security** > **Firewall**.

<!-- ***********************************************-->

## Device enrollment

### Configure zero-touch enrollment in the admin center<!-- 1872357 -->
Configure zero-touch enrollment seamlessly from the admin center. This feature will let you link your zero-touch account to Intune, add support information, configure zero-touch enabled devices with Android Device Policy, and customize provisioning extras.  

<!-- ***********************************************-->

## Monitor and troubleshoot

### Open Help and Support without losing your context in the Microsoft Endpoint Manager admin center<!-- 12469338 -->
You’ll soon be able to use the **?** icon in the Microsoft Endpoint Manager admin center to  open a help and support session without losing your current node of focus in the admin center. The **?** icon is always available in the upper right of the admin center title bar. This change will add an additional method for accessing *Help and support*.

When you select  **?**, the admin center will open a new and separate side-by-side pane you use to navigate the support experience. By opening this separate pane, you’ll be free to navigate the support experience without affecting your original location and focus on the admin center. You will however be free to navigate through the admin center in that original pane if you choose.

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
