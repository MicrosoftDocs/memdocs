---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 10/17/2024
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

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies now provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

<!-- ## Device configuration -->

<!-- *********************************************** -->

<!-- ## Device enrollment -->

<!-- *********************************************** -->

## Device management

### Device Inventory for Windows<!-- 24853010 -->

Device inventory lets you collect and view additional hardware properties from your managed devices to help you better understand the state of your devices and make business decisions.

You'll soon be able to choose what you want to collect from your devices, using the catalog of properties and then view the collected properties in the Resource Explorer view.

Applies to:

- Windows (Corporate owned devices managed by Intune)

<!-- *********************************************** -->

## Device security

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
