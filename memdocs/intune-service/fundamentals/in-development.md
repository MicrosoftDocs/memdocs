---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 04/01/2025
ms.topic: article
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
- When a feature enters production, whether it's in preview or generally available, the feature description moves from this article to [What's new](whats-new.md).
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

### Endpoint Privilege Management elevation rule support for file arguments and parameters<!--28077130 -->

Soon, the file elevation rules for Endpoint Privilege Management (EPM) will support use of arguments or parameters that you want to allow. Arguments and parameters that aren't explicitly allowed will be blocked from use. This capability helps to improve control of the context for file elevations.

EPM is available as an [Intune Suite add-on-capability](../fundamentals/intune-add-ons.md).

<!-- ***********************************************-->

## App management

### Add Enterprise App Catalog apps to ESP blocking apps list<!-- 29846319 -->

Enterprise App Catalog apps will be supported with Windows Autopilot. Microsoft Intune Enterprise App Management enables IT admins to easily manage applications from the Enterprise App Catalog. Using Windows Autopilot, you'll be able to select blocking apps from the Enterprise App Catalog in the Enrollment Status Page (ESP) and the Device Preparation Page (DPP) profiles. This change allows you to update apps more easily without needing to update those profiles with the latest versions. 

For related information, see [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md), [Overview of Windows Autopilot device preparation](/autopilot/device-preparation/overview), and [Add an Enterprise App Catalog app to Microsoft Intune](../apps/apps-add-enterprise-app.md).

Applies to:

- Windows

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies will soon provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

### Android settings in the Settings Catalog <!-- 31524383 (was 26981326) -->

The settings catalog will soon support Android Enterprise and AOSP.

Currently, to configure Android settings, you use the built-in templates. The settings from these templates are also available in the settings catalog. More settings will continue to be added.

In the Intune admin center, when you create a device configuration profile, you select the **Profile Type** (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > select your **Platform** > **Profile Type**). All the profile types are moved to **Profile Type** > **Templates**.

This change:

- Will be a UI change with no impact on your existing policies. Your existing policies don't change. You'll still be able to create, edit, and assign these policies the same way.
- Will be the same UI experience as iOS/iPadOS, macOS, and Windows templates.

To get started with settings catalog, go to [Use the settings catalog to configure settings on your devices](../configuration/settings-catalog.md).

Applies to:

- Android Enterprise
- AOSP

<!-- *********************************************** -->

## Device enrollment

### Enrollment-time grouping for Android Enterprise corporate devices <!-- 17530981 -->

Soon to be available for Android Enterprise corporate-owned devices, *enrollment time grouping* enables you to assign a static Microsoft Entra group to devices at enrollment time. When a targeted Android device enrolls, it will receive all assigned policies, apps, and settings, typically by the time the user lands on the home screen. Intune admins will be able to configure one static Microsoft Entra group per enrollment profile under the **Device group** tab.


### Custom device naming template for Android Enterprise corporate-owned devices<!-- 3465701 -->

You'll soon be able to use a custom template for naming Android Enterprise corporate-owned devices when they enroll with Intune. The template will be available to configure in the enrollment profile. It can contain a combination of free text and predefined variables, such as device serial number, device type, and for user-affiliated devices, the owner's username.

Applies to:

- Android

<!-- *********************************************** -->

## Device management

### Intune ending support for custom profiles for personally owned work profile devices<!-- 27424084 -->

Starting in April 2025, Intune will no longer support custom profiles for Android Enterprise personally owned work profile devices. After this time:

- Admins won’t be able to create new custom profiles for personally owned work profile devices. However, admins can still view and edit previously created custom profiles.

- Personally-owned work profile devices that currently have a custom profile assigned won't experience any immediate change of functionality. Because these profiles are no longer supported, the functionality set by these profiles might change in the future.

- Intune technical support will no longer support custom profiles for personally owned work profile devices.

All custom policies should be replaced with other policy types. Learn more about [Intune ending support for personally owned work profile custom profiles](https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-ending-support-for-custom-profiles-for-personally-owned-work-profile-devi/4287414).

### Remote actions with multiple administrative approval (MAA)<!-- 27043113 -->

Intune *access policies* help protect against a compromised administrative account by requiring that a second administrative account is used to approve a change before the change is applied. This capability is known as multiple administrative approvals (MAA). The remote actions **Retire**, **Wipe**, and **Delete** will support MAA. Onboarding Remote device actions to MAA helps to mitigate the risk of unauthorized or compromised remote actions being taken on devices by a single administrative account, thereby enhancing the overall security posture of the environment.

For more information on multiple administrative approvals, see [Use multiple administrative approvals in Intune](../fundamentals/multi-admin-approval.md).

### Introducing platform level targeting of Device Cleanup rule<!-- 13835920 -->

We're adding a feature that will allow a customer to:

- Configure one device cleanup rule per platform (Windows, iOS/macOS, iPadOS, Android, Linux)
- Configure a different RBAC permission and assign the permission to different RBAC roles

Platform level targeting of the Device Cleanup rule helps administrators to remove stale and inactive devices from their tenant based on the active days rule specified by the admin. Scoped and targeted Device cleanup rules add an intermediate stage where an admin will be able to target removing stale devices by having a rule configured at the platform or OS level.

For more information, see [device cleanup rules](../remote-actions/devices-wipe.md#automatically-remove-devices-with-cleanup-rules).

<!-- *********************************************** -->

## Device security

### Linux support for Endpoint detection and response exclusion settings<!-- 26549863 -->

We're adding a new Endpoint Security template under Endpoint detection and response (EDR) for the Linux platform that will be supported through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario.

The template will support settings related to global exclusion settings. Applicable to antivirus and EDR engines on the client, the settings can configure exclusions to stop associated real time protection EDR alerts for the excluded items. Exclusions can be defined by the file path, folder, or process explicitly defined by the admin in the policy.

Applies to:

- Linux

### Support for Intune Device control policy for devices managed by Microsoft Defender for Endpoint<!--   -->

You'll be able to use the endpoint security policy for *Device control* (Attack surface reduction policy) from the Microsoft Intune with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.

- **Device control** policies are part of endpoint security [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

Applies to the following when you use the *Windows* platform:

- Windows 10
- Windows 11

When this change takes effect, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive this policy will get it.

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

## Tenant administration

### Updates to Intune admin center home page<!-- 25914324 -->

Microsoft Intune admin center's home page will be updated to include additional links to interactive demos, documentation, and training.

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
