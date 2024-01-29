---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 01/29/2024
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

### Update to Intune Management Extension on Windows<!-- 26472055  -->  
Intune Management Extension on Windows will be updated. To support this update, Windows clients must have a minimum of **.NET Framework 4.7.2** (available from Windows Update as of July 10, 2018).
 
### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->
To protect organizational data for MAM managed accounts and apps, Intune app protection policies now provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

### Intune migrating from SafetyNet Attestation API to Google Play Integrity API<!-- 15571389   -->  
Google has deprecated the [SafetyNet Attestation API](https://developer.android.com/training/safetynet/attestation) and replaced it with the [Play Integrity API](https://developer.android.com/google/play/integrity). Intune will be migrating to the new API for app protection policies. The "SafetyNet device attestation" setting name will be updated to align with the new Google Play Integrity API for all policies in the Intune user interface (UI). For related information, see [Discontinuing the SafetyNet Attestation API](https://developer.android.com/training/safetynet/deprecation-timeline) and [Migrating from the SafetyNet Attestation API](https://developer.android.com/google/play/integrity/migrate).

### Enterprise application management<!-- 10986080  -->  
Enterprise Application Management provides a catalog of prepackaged applications designed to simplify discovery, delivery, and updates for third and first party apps. Enterprise Application Management will be generally available in early Q1 2024.

### Company Portal automatically installed on Android Enterprise dedicated devices<!-- 6423852  -->  
Intune Company Portal will now be automatically installed on all Android Enterprise dedicated devices to ensure the appropriate handling of app protection policies. Users won't be able to see or launch the Company Portal, and there are no requirements for users to interact with it. Admins will notice that the Company Portal is automatically installed on their Android Enterprise dedicated devices, without the ability to uninstall.

### Support for multi-SIM iOS/iPadOS device inventory<!-- 17016690  -->  
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

### New settings available in the Apple settings catalog <!-- 25280353 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** > **Settings catalog** for profile type.  

**Full Disk Encryption > FileVault**:

- Force Enable In Setup Assistant

Applies to:

- macOS

**Restrictions**:

- Allow Live Voicemail
- Force Preserve ESIM On Erase

Applies to:

- iOS/iPadOS

**Restrictions**:

- Force Classroom Unprompted Screen Observation

Applies to:

- iOS/iPadOS
- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

### New setting for updating MAC address randomization on Android Enterprise devices <!-- 24259789 -->

Admins will have a set of new settings to update MAC address randomization on Android Enterprise devices (**Devices** > **Configuration** > **Create** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Wi-Fi** for profile type).

Starting with Android 10, when connecting to a network, devices present a randomized MAC address instead of the physical MAC address. Using randomized MAC addresses is recommended for privacy, as it's harder to track a device by its MAC address. However, randomized MAC addresses break functionality that relies on a static MAC address, including network access control (NAC).

Your options:

- **Use device default**: Intune doesn't change or update this setting. By default, when connecting to a network, devices will present a randomized MAC address instead of the physical MAC address when connecting to a new network. Any updates made by the user to the setting will persist.

- **Use randomized MAC**: Enables MAC address randomization on devices. When connecting to a new network, devices present a randomized MAC address, instead of the physical MAC address. If the user changes this value on their device, it will reset to **Use randomized MAC** on the next Intune sync.

- **Use device MAC**: Forces devices to present their actual Wi-Fi MAC address instead of a random MAC address. This setting allows devices to be tracked by their MAC address. Only use this value when necessary, such as for network access control (NAC) support. If the user changes this value on their device, it will reset to **Use device MAC** on next sync.

Applies to:

- Android 13 and newer

For more information on the current Wi-Fi settings you can configure, go to [Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices in Microsoft Intune](../configuration/wi-fi-settings-android-enterprise.md).

### Import up to 20 custom ADMX and ADML administrative templates<!-- 25780608  -->  
You can import custom ADMX and ADML administrative templates in Microsoft Intune. Currently, you can import up to 10 files.

You'll be able to upload 20 files.

For more information on this feature, go to [Import custom ADMX and ADML administrative templates into Microsoft Intune (public preview)](../configuration/administrative-templates-import-custom.md).

Applies to:

- Windows 10/11

### The macOS Company Portal app will support platform SSO (public preview)<!-- 24325427  -->  
In Intune, you can configure the Enterprise SSO plug-in on Apple devices using a device configuration profile (**Devices** > **Configuration** > **Create** > **macOS** for platform > **Settings Catalog** for profile > **Authentication** > **Extensible Single sign-on (SSO)**).

The Company Portal app version will support the platform SSO settings for macOS 13 and later. Platform SSO allows you to sync your Microsoft Entra ID password to local accounts on Macs using the Enterprise Single Sign-On extension.

For more information on the Enterprise SSO plug-in, go to:

- [Use Intune to deploy the Microsoft Enterprise SSO plug-in for Apple devices](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)
- [Entra ID and the Microsoft Enterprise SSO plug-in overview for Apple devices](/azure/active-directory/develop/apple-sso-plugin)

Applies to:

- macOS 13 and later

### Use assignment filters on Endpoint Privilege Management (EPM) policies<!-- 25230705   -->  
You can use assignment filters to assign a policy based on rules you create. A filter allows you to narrow the assignment scope of a policy, like targeting devices with a specific OS version or a specific manufacturer.

You can use filters on Endpoint Privilege Management (EPM) policies.

For more information about assignment filters, go to [Use filters when assigning your apps, policies, and profiles in Intune](filters.md).

Applies to:

- Windows 10/11

<!-- *********************************************** -->

## Device enrollment

### New local primary account configuration for macOS automated device enrollment (ADE) <!-- 5877061 -->

Configure local primary account settings for Macs enrolling in Intune via Apple automated device enrollment (ADE). These settings, supported on devices running macOS 10.11 and later, will be available in new and existing enrollment profiles under the new **Account Settings** tab. For this feature to work, the enrollment profile must be configured with user-device affinity and one of the following authentication methods:   

- Setup Assistant with modern authentication  
- Setup Assistant (legacy)  

### RBAC changes coming to enrollment settings for Windows Hello for Business<!-- 25661866   -->  
We're updating RBAC in the enrollment area for Windows Hello for Business. Enrollment settings related to Windows Hello for Business will be read-only for all roles except the Intune Service Administrator. The Intune Service Administrator will be able to edit enrollment settings.

<!-- *********************************************** -->

## Device management

### End-user access to BitLocker Recovery Keys for enrolled Windows devices<!-- 8077173 -->
End-users will be able to view the BitLocker Recovery Key for enrolled Windows devices in the Web Company Portal. This capability will reduce helpdesk calls in the event they get locked out of their corporate machines. End users can access their enrolled Windows device's Recovery Key by clicking on **View Recovery Key** under their device after logging into the Web Company Portal. This is a similar experience to the MyAccount website which allows end users see their recovery keys as well.

Access to BitLocker recovery keys by end-users can be prevented when not allowed within your organization by using the Entra ID toggle **Restrict non-admin users from recovering the BitLocker key(s) for their owned device**. For more information about how to prevent access to BitLocker recovery keys, see [Manage device identities using the Microsoft Entra admin center](/entra/identity/devices/manage-device-identities).

### Introducing a remote action to pause the config refresh enforcement interval<!--24249019  -->  
In the Windows Settings Catalog, you can configure **Config Refresh**. This feature lets you set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check in to Intune. The device will replay and re-enforce settings based on previously received policy to minimize the chance for configuration drift.

To support this feature, a remote action will be added to allow a pause in action. If an admin needs to make changes or run remediation on a device for troubleshooting or maintenance, they can issue a pause from Intune for a specified period. When the period expires, settings will be enforced again.

The remote action **Pause config refresh** can be accessed from the device summary page.

For information on currently available Remote actions, see [Remote actions](../remote-actions/device-management.md).

<!-- *********************************************** -->

## Device security

### HTML formatting supported in noncompliance email notifications <!-- 24197255   -->  
HTML formatting will be supported in noncompliance email notifications for all platforms. You'll be able to use supported HTML tags to add formatting such as italics, URL links, and bulleted lists to your organization's messages.

### Support for Intune Device control policy for devices managed by Microsoft Defender for Endpoint<!-- 15466620, 25470154  -->  

You will be able to use the endpoint security policy for *Device control* (Attack surface reduction policy) from the Microsoft Intune with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.
 
- **Device control** policies are part of endpoint security [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

  Applies to:
  - Windows 10/11- - Available for the *Windows 10, Windows 11, and Windows Server* platform.
 
Prepare for February 2024. This policy change is expected to be released with the February 2024 service update for Intune. When this change takes effect, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive this policy will get it.

<!-- *********************************************** -->

## Monitor and troubleshoot

### Battery report<!-- 9747162 -->  
We're working on a battery health report to provide visibility into the health of batteries in your organization’s devices and its influence on user experience. The scores and insights in this report are aimed to help IT admins with asset management and purchase decisions that improve user experience while balancing hardware costs.

The battery health report is a part of Microsoft Intune Advanced Analytics. It will be included as an Intune-add on under [Microsoft Intune Suite](../fundamentals/intune-add-ons.md) and requires an extra cost to the licensing options that include Microsoft Intune.

### Run on-demand pivot queries on single devices<!--16719466  -->  
Intune allows you to quickly gain on-demand information about the state of your device. When you enter a query on a selected device, Intune will run a query in real time. The data returned can then be used to respond to security threats, troubleshoot the device, or make business decisions.

This feature will be available as part of Microsoft Intune Advanced Analytics, which is available as part of Microsoft Intune Suite, or as an individual add-on. For more information, see [Microsoft Intune add-ons](../fundamentals/intune-add-ons.md).

Applies to:

- Windows devices

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

## Tenant administration

### Customization pane support for excluding groups<!-- 17654599 -->
The Customization pane will support setting groups to exclude when assigning policies. You will find this setting in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Customization**.

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
