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
- tier1
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

## Device configuration

### Disable Activation Lock device action for supervised iOS/iPadOS devices<!-- 15571509 -->  
You'll soon be able to use the **Disable Activation Lock** device action in Intune to bypass Activation Lock on iOS/iPadOS devices without requiring the current username or password.

This new action will be available under **Devices > iOS/iPadOS > select one of your listed devices > Disable Activation Lock**.

More information on managing Activation Lock is available at [Bypass iOS/iPadOS Activation Lock with Intune - Microsoft Intune | Microsoft Learn](../remote-actions/device-activation-lock-disable.md) or on Apple's website at [Activation Lock for iPhone, iPad, and iPod touch - Apple Support.](https://support.apple.com/en-us/HT201365).

Applies to:  
- **iOS/iPadOS**

### Size and generation included in iOS/iPadOS model information<!-- 16406692 -->  
You'll soon be able to view the size and generation for enrolled iOS/iPadOS devices as part of the **Model** attribute in **Hardware device details**. Go to **Devices > All devices** > select one of your listed devices and select **Hardware** to open its details.

For example, iPad Pro 11-inch (3rd generation) will display for the device model instead of iPad Pro 3.

For more information, go to: [See device details in Intune](../remote-actions/device-inventory.md#hardware-device-details)

Applies to:
- **iOS/iPadOS**

### Support for multi-SIM iOS/iPadOS device inventory<!--16360290-->

You'll soon be able to view the service subscription fields on devices that have multiple SIM cards installed under the per-device Hardware section. The inventory fields that are capable of reporting multiple values to Intune are:

- **ICCID**
- **IMEI**
- **MEID**
- **Phone number**

These fields will default to using labels returned by the device, such as:  *Primary*, *Secondary*, *CTSubscriptionSlotOne*, and *CTSubscriptionSlotTwo*. These returned labels may be displayed in the language of the local device that is reporting its inventory to Intune.

Applies to:
- **iOS/iPadOS**

<!-- *********************************************** -->

## Device management

### View ServiceNow Incidents in the Intune Troubleshooting workspace<!-- 12508062  -->  
You'll soon be able to view a list of ServiceNow incidents associated with the user you've selected in the Intune Troubleshooting workspace. This new feature will be available under **Troubleshooting + Support** > select a user > **ServiceNow Incidents**. The list of incidents shown have a direct link back to the source incident and show key information from the incident. All incidents listed will link the "Caller" identified in the incident with the user selected for Troubleshooting.

For more information go to [Use the troubleshooting portal to help users at your company](help-desk-operators.md).

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

### On-demand proactive remediation for a Windows device<!-- 14783338  -->  
A new device action that is in public preview allows you to run a proactive remediation on-demand to a single Windows device. The **Run** remediation device action will allow you to resolve issues without having to wait for a proactive remediation to run on its assigned schedule. You will also be able to view the status of proactive remediations under **Remediations** in the **Monitor** section of a device.

### Support to delete stale devices that are managed through Security Management for Microsoft Defender for Endpoint<!-- 14729617   -->  
You’ll soon be able to select the action to **Delete** a device that’s managed through the [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md) solution from within the Microsoft Endpoint Manager admin center. The delete option will appear along with other device management options when you view the device’s Overview details. To locate a device managed by this solution, in the admin center go to **Devices** > **All devices**, and then select a device that displays either *MDEJoined* or *MDEManaged* in the *Managed by* column.

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
