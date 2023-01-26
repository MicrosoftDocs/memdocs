---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 01/26/2023
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

### Block pinning web pages to Managed Home Screen app<!-- 15593458 -->  
On Android Enterprise dedicated devices using Managed Home Screen, you can now use app configuration to configure the Managed Home Screen app to block pinning browser web pages to Managed Home Screen. The new `key` value is `block_pinning_browser_web_pages_to_MHS`. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

### Company Portal automatically installed on Android Enterprise dedicated devices<!-- 6423852  -->  
Intune Company Portal will now be automatically installed on all Android Enterprise dedicated devices to ensure the appropriate handling of app protection policies. Users will not be able to see or launch the Company Portal, and there are no requirements for users to interact with it. Admins will notice that the Company Portal is automatically installed on their Android Enterprise dedicated devices, without the ability to uninstall.

### Uninstall Win32 apps in the Company Portal<!-- 5145748 -->  
*The time frame for the release of this update is still being determined.*

Users will be able to uninstall Win32 apps in the Company Portal. If a Win32 app can be uninstalled by the user, the user will be able to select **Uninstall** for the Win32 app in the Company Portal. For more information about Win32 apps, go to [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

### Configure whether to show apps from Configuration Manager in Windows Company Portal<!-- 9135109 -->  
In the Microsoft Endpoint Manager admin center, you'll be able to choose whether to show or hide Configuration Manager apps from appearing in the Windows Company Portal. This option will be available in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Customization**. Next to **Settings**, select **Edit**. The option to **Show** or **Hide** the Configuration Manager applications will be located in the **App Sources** section of the pane. For related information about configuring the Company Portal app, see [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

### Global quiet time app policy settings<!-- 15424417 -->  
The global quiet time settings will allow you to create policies to schedule quiet time for your end users, which will automatically mute Microsoft Outlook email and Teams notifications on iOS/iPadOS and Android platforms. These policies can be used to limit end user notifications received after work hours. When this feature is available, you will be able to find it in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Quiet Time** > **Policies**.

<!-- *********************************************** -->

## Device configuration


### New settings available in the Apple Settings Catalog <!--16237513 -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. 

New settings are available in the Settings Catalog. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Accounts > Subscribed Calendars**:

- Account Description
- Account Host Name
- Account Password
- Account Use SSL
- Account Username

Applies to:
- iOS/iPadOS

**Networking > Domains**:

- Cross Site Tracking Prevention Relaxed Domains

Applies to:
- macOS

The following settings are also in Settings Catalog. Previously, they were only available in Templates:

**File Vault**:

- User Enters Missing Info 

Applies to:
- macOS

**Restrictions**:

- Rating Region

Applies to:
- iOS/iPadOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Updated descriptions for iOS/iPadOS and macOS settings in the settings catalog<!-- 16360170 -->
The settings catalog lists all the settings you can configure, and all in one place. For the iOS/iPadOS and macOS settings, the descriptions are updated to include more information.

For more information on the settings catalog, go to:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md)
- [Common tasks you can complete using the Settings Catalog in Intune](../configuration/settings-catalog-common-features.md)

Applies to:

- iOS/iPadOS
- macOS

### Support for multi-SIM iOS/iPadOS device inventory  <!--16360290 -->  
You'll soon be able to view the service subscription fields on devices that have multiple SIM cards installed under the per-device Hardware section. The inventory fields that are capable of reporting multiple values to Intune are:  

- ICCID
- IMEI
- MEID
- Phone number

These fields will default to using labels returned by the device, such as:  *Primary*, *Secondary*, *CTSubscriptionSlotOne*, and *CTSubscriptionSlotTwo*. These returned labels may be displayed in the language of the local device that is reporting its inventory to Intune.

Applies to:  
- iOS/iPadOS

### Support for Bulk Device Actions on devices running Android AOSP  <!--15397458 -->  
You will soon be able to complete "Bulk Device Actions" for devices running Android AOSP. The bulk device actions supported on devices running AOSP are Delete, Wipe and Restart.

Applies to:
- AOSP

### Grace period status visible in Intune Company Portal app for Android <!-- 13498225 -->  
The Intune Company Portal app for Android will show a grace period status to account for devices that don't meet compliance requirements but are still within their given grace period.  Users will see the date by which they need to become compliant and the instructions for how to become compliant. If they don't update their device by the given date, their status will change to noncompliant.

<!-- ***********************************************-->

## Device enrollment

### Skip or show Terms of Address pane in Setup Assistant  <!-- 14661838 -->  
Configure Intune to skip or show a new Setup Assistant pane called **Terms of Address** during Apple Automated Device Enrollment (ADE). The Terms of Address pane lets users on iOS/iPadOS and macOS devices personalize how apps address them.  The pane will be visible during ADE by default. You will be able to hide the pane on devices running iOS/iPadOS 16 and later, or macOS 13 and later. To access Setup Assistant pane settings, sign in to the Microsoft Endpoint Manager admin center. Then in your enrollment profile, expand the **Setup Assistant** category.

<!-- ***********************************************-->

## Device management

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

### Support for tamper protection in policies for Security settings management for Microsoft Defender for Endpoint <!-- 13204113 -->  
You’ll soon be able to manage Tamper protection for Microsoft Defender for Endpoint on unenrolled devices as part of the [MDE Security configuration](../protect/mde-security-integration.md#which-solution-should-i-use) scenario.

When this support is available, your tamper protection configurations from *Windows Security Experience* profiles for *Antivirus* policies can apply to all devices instead of only to those that are enrolled with Intune.

Applies to:  
- Windows 10
- Windows 11

### Attack surface reduction policy support for Security settings management for Microsoft Defender for Endpoint <!-- 13816760  -->  
Attack surface reduction policies will soon support devices managed through the [MDE Security configuration](../protect/mde-security-integration.md#which-solution-should-i-use) scenario. Today, only devices that are enrolled with Intune support this policy type.

Applies to:  
- Windows 10
- Windows 11

<!-- ***********************************************-->

## Monitor and troubleshoot

### Support to download mobile app diagnostics from the Microsoft Endpoint Manager admin center<!-- 9353471  -->  
Admins will soon be able to use the updated troubleshooting experience of the Microsoft Endpoint Manager admin center to access mobile app diagnostics. This includes the mobile app diagnostics and logs that users upload for Company Portal and App Protection.

Applies to:  
- Android
- iOS/iPadOS
- Windows

### Intune troubleshooting pane update<!-- 4442647  -->  
The Intune troubleshooting pane will provide a new experience.  It will provide details about user's devices, policies, applications, and status. The troubleshooting pane will include the following information:  

- A summary of policy, compliance, and application deployment status.
- Support for exporting, filtering, and sorting all reports.
- Support to filter by excluding policies and applications.
- Support to filter to a user’s single device.
- Details about available device diagnostics and disabled devices.
- Details about offline devices that haven't checked-in to the service for three or more days.

You can find the troubleshooting pane in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Troubleshoot**. To view the new experience during preview, select **Preview upcoming changes to Troubleshooting and provide feedback** to display the **Troubleshooting preview** pane, then select **Try it now**.

<!-- ***********************************************-->

## Tenant administration

### Improved UI experience for multiple certificate connectors<!-- 16263248 -->  
We’ll soon add pagination controls to the *Certificate connectors* view to help improve the experience when you have more than 25 certificate connectors configured. With the new controls, you’ll be able to see total number of connector records and easily navigate to a specific page when viewing your certificate connectors. 

To view certificate connectors, in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Tenant administration** > **Connectors and tokens** > **Certificate connectors**.

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
