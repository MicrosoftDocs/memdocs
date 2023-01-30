---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 02/01/2023
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
  - highseo
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

### Latest iOS/iPadOS version available as minimum OS requirement for LOB and store apps<!-- 16433620  -->  
You'll soon be able to specify iOS/iPadOS 16.0 as the minimum operating system for line-of-business and store app deployments. This new setting option will be available in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** > *iOS store app or Line-of-business app*. For more information about managing apps, see [Add apps to Microsoft Intune](../apps/apps-add.md).

### Company Portal automatically installed on Android Enterprise dedicated devices<!-- 6423852  -->  
Intune Company Portal will now be automatically installed on all Android Enterprise dedicated devices to ensure the appropriate handling of app protection policies. Users will not be able to see or launch the Company Portal, and there are no requirements for users to interact with it. Admins will notice that the Company Portal is automatically installed on their Android Enterprise dedicated devices, without the ability to uninstall.

### Uninstall Win32 apps in the Company Portal<!-- 5145748 -->  
*The time frame for the release of this update is still being determined.*

Users will be able to uninstall Win32 apps in the Company Portal. If a Win32 app can be uninstalled by the user, the user will be able to select **Uninstall** for the Win32 app in the Company Portal. For more information about Win32 apps, go to [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

### Global quiet time app policy settings<!-- 15424417 -->  
The global quiet time settings will allow you to create policies to schedule quiet time for your end users, which will automatically mute Microsoft Outlook email and Teams notifications on iOS/iPadOS and Android platforms. These policies can be used to limit end user notifications received after work hours. When this feature is available, you will be able to find it in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Quiet Time** > **Policies**.

<!-- *********************************************** -->

## Device management

### Add Google accounts to Android Enterprise personally owned devices with a work profile<!-- 9113561 -->  
On Android Enterprise personally owned devices with a work profile, you can configure settings that restrict device features and settings. Currently, there is an **Add and remove accounts** setting. This setting prevents accounts from being added in the work profile, including preventing Google accounts.

This setting is changing, and you will be able to add Google accounts. The **Add and remove accounts** setting options will be:  
- **Block all accounts types**: Prevents users from manually adding or removing accounts in the work profile. For example, when you deploy the Gmail app into the work profile, you can prevent users from adding or removing accounts in this work profile.

- **Allow all accounts types**: Allows all accounts, including Google accounts. These Google accounts are blocked from installing apps from the **Managed Google Play Store**. This option requires Google Play app version 80970100 or higher.
- **Allow all accounts types, except Google accounts** (default): Intune doesn't change or update this setting. By default, the OS might allow adding accounts in the work profile.

For more information on the settings you can configure, go to [Android Enterprise device settings list to allow or restrict features on personally owned devices using Intune](../configuration/device-restrictions-android-enterprise-personal.md).

Applies to:  
- Android Enterprise personally owned devices with a work profile

### New settings and setting options available in the Apple Settings Catalog<!-- 16813380 -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Login > Service Management - Managed Login Items**:  
- Team Identifier

**Microsoft Office > Microsoft Office**:  
- Office Activation Email Address

Applies to:  
- macOS

**Networking > Domains**:  
- Cross Site Tracking Prevention Relaxed Domains

Applies to:  
- iOS/iPadOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Support to delete stale devices that are managed through Security Management for Microsoft Defender for Endpoint<!-- 14729617   -->  
You’ll soon be able to select the action to **Delete** a device that’s managed through the [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md) solution from within the Microsoft Endpoint Manager admin center. The delete option will appear along with other device management options when you view the device’s Overview details. To locate a device managed by this solution, in the admin center go to **Devices** > **All devices**, and then select a device that displays either *MDEJoined* or *MDEManaged* in the *Managed by* column.

### Improvements to Devices area in admin center (public preview) <!-- 12775837  -->  
The **Devices** area in the admin center will be updated to provide a more consistent UI, with more capable controls and an improved navigation structure so you can find the information you need faster. You will be able to opt in to the public preview to try out the new experience. Changes will include:  
* A new scenario-focused navigation structure that brings monitoring in line with management workflows.
* New in-line monitoring pages with easy access to key metrics and reports.
* Reduction in journey, helping you get to your destination faster.
* New location for platform pivots that help to create a more consistent navigation model.
* A consistent way across list views to search, sort, and filter data.

The following device pages will be updated:  
* Overview
* All devices
* Compliance
* Configuration
* Windows 10 updates
* Apple updates
* Enrollment

### Software update policies for macOS will soon be generally available<!-- 12393100 -->  
Software update policies for macOS devices will soon be out of preview and generally available. This general availability will apply to supervised devices running macOS 12 (Monterey) and later. We will continue to add improvements to this feature going forward.

For more information, see [Use Microsoft Intune policies to manage macOS software updates](../protect/software-updates-macos.md).


### Endpoint security firewall rules support for ICMP type<!-- 5653356 -->  
We’re adding a new setting named **IcmpTypesAndCodes** to the endpoint security firewall rules template for Windows 10. To configure this in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Endpoint security** > **Firewall** > **Create Policy** > Platform: *Windows 10, Windows 11, and Windows Server*  > Profile: *Microsoft Defender Firewall Rules*).

With this new setting, you’ll be able to configure inbound and outbound rules for [Internet Control Message Protocol](/windows/security/threat-protection/windows-firewall/create-an-inbound-icmp-rule) (ICMP) as part of a firewall rule.

Applies to:  
- Windows 10, Windows 11, and Windows Server

<!-- ***********************************************-->

## Device security

### New endpoint security Antivirus template to manage Microsoft Defender update behavior<!-- 11890335  -->  
You’ll soon be able to use a new endpoint security policy template for Antivirus to manage updates for Microsoft Defender. With this new template you’ll be able to manage settings for the rollout release channel by which devices and users receive Defender Updates that are related to daily security intelligence updates, monthly platform updates, and monthly engine updates.

When available, you’ll find the new template in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Endpoint security** > **Antivirus**.  The settings in the profile will be from the Defender CSP. See [Defender CSP - Windows Client Management](/windows/client-management/mdm/defender-csp).

Applies to:  
- Windows 10
- Windows 11

### Support for tamper protection in policies for Security settings management for Microsoft Defender for Endpoint <!-- 13204113 -->  
You’ll soon be able to manage Tamper protection for Microsoft Defender for Endpoint on unenrolled devices as part of the [MDE Security configuration](../protect/mde-security-integration.md#which-solution-should-i-use) scenario.

When this support is available, your tamper protection configurations from *Windows Security Experience* profiles for *Antivirus* policies can apply to all devices instead of only to those that are enrolled with Intune.

Applies to:  
- Windows 10
- Windows 11

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
