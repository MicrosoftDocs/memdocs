---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 11/21/2022
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

### Company Portal automatically installed on Android Enterprise dedicated devices<!-- 6423852  -->
Microsoft's Company Portal will now be automatically installed on all Android Enterprise (AE) dedicated devices to ensure the appropriate handling of app protection policies. Users will not be able to see or launch the Company Portal, and there are no requirements for users to interact with it. Admins will notice that the Company Portal is automatically installed on their AE dedicated devices, without the ability to uninstall.

### Uninstall Win32 apps in the Company Portal<!-- 5145748 -->  
Users will be able to uninstall Win32 apps in the Company Portal. If a Win32 app can be uninstalled by the user, the user will be able to select **Uninstall** for the Win32 app in the Company Portal. For more information about Win32 apps, go to [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

### Configure whether to show apps from Configuration Manager in Windows Company Portal<!-- 9135109 -->  
In the Intune console, you'll be able to choose whether to show or hide Configuration Manager apps from appearing in the Windows Company Portal. This option will be available in [Intune](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Customization**. Next to **Settings**, select **Edit**. The option to **Show** or **Hide** the Configuration Manager applications will be located in the **App Sources** section of the pane. For related information about configuring the Company Portal app, see [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

### Global quiet time app policy settings<!-- 15424417 -->  
The global quiet time settings will allow you to create policies to schedule quiet time for your end users, which will automatically mute Microsoft Outlook email and Teams notifications on iOS/iPadOS and Android platforms. These policies can be used to limit end user notifications received after work hours. When this feature is available, you will be able to find it in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Quiet Time** > **Policies**.

<!-- ***********************************************-->

## Device configuration

### New settings available in the macOS Settings Catalog <!-- 16069006   -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**File Vault > File Vault Options**:  
- Destroy FV Key On Standby
- Block FV From Being Disabled
- Block FV From Being Enabled

**Restrictions**:  
- Allow Bluetooth Modification

Applies to:  
- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

### The Company Portal app will enforce Password Complexity setting on Android Enterprise 12+ personally owned devices with a work profile<!-- 16211313 -->  
On Android Enterprise 12+ personally owned devices with a work profile, you can create a compliance policy and/or device configuration profile that sets the password complexity. Starting with the 2211 release, this setting is available in the Endpoint Manager admin center:

- **Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > Personally owned with a work profile
- **Devices** > **Compliance policies** > **Create policy** > **Android Enterprise** for platform > Personally owned with a work profile

In the 2212 release, the Company Portal app will enforce the **Password complexity** setting.

For more information on this setting and the other settings you can configure on personally owned devices with a work profile, go to:

- [Device compliance settings for Android Enterprise in Intune](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile
- [Android Enterprise device settings list to allow or restrict features on personally owned devices using Intune](../configuration/device-restrictions-android-enterprise-personal.md)

Applies to:

- Android Enterprise 12+ personally owned devices with a work profile

### There are default settings for SSO extension requests on macOS devices<!-- 15082414  -->  
When you create a single sign-on app extension configuration profile, there are some settings you configure. The following settings will use the following default values for all SSO extension requests:

- **AppPrefixAllowList** key
  Default value: `com.microsoft.,com.apple.`

- **browser_sso_interaction_enabled** key
  Default value: `1`

- **disable_explicit_app_prompt** key
  Default value: `1`

If you configure a value other than the default value, then the configured value will overwrite the default value. 

For example, you don't configure the `AppPrefixAllowList` key. By default, all Microsoft apps (`com.microsoft.`) and all Apple apps (`com.apple.`) will be enabled for SSO. You can overwrite this behavior by adding a different prefix to the list, such as `com.contoso.`.

For more information on the Enterprise SSO plug-in, go to [Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS and macOS devices in Microsoft Intune](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)

Applies to:

- macOS

### There are default settings for SSO extension requests on iOS/iPadOS devices<!-- 15084030 -->  
When you create a single sign-on app extension configuration profile, there are some settings you configure. The following settings will use the following default values for all SSO extension requests:

- **AppPrefixAllowList** key
  Default value: `com.apple.`

- **browser_sso_interaction_enabled** key
  Default value: `1`

- **disable_explicit_app_prompt** key
  Default value: `1`

If you configure a value other than the default value, then the configured value will overwrite the default value. 

For example, you don't configure the `AppPrefixAllowList` key. By default, all Apple apps (`com.apple.`) will be enabled for SSO. You can overwrite this behavior by adding a different prefix to the list, such as `com.contoso.`.

For more information on the Enterprise SSO plug-in, go to [Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS and macOS devices in Microsoft Intune](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)

Applies to:

- iOS/iPadOS

<!-- ***********************************************-->

## Device enrollment

### Enrollment token lifetime will increase to 65 years for Android Enterprise dedicated devices  <!-- 12775837 -->  
You'll be able to create an enrollment profile for Android Enterprise dedicated devices that's valid for up to 65 years. If you have an existing profile, the enrollment token will still expire at whatever date you chose when you created the profile, but when you renew it you'll be able to extend the lifetime to 65 years.

<!-- ***********************************************-->

## Device management

### Update policies for macOS now available for all supervised devices<!-- 16141990   -->  
You'll soon be able to manage software update policies for macOS devices that weren't supervised through Automated Device Enrollment (ADE). Update policies for macOS are available under **Devices** > **Update policies for macOS (preview)**. For more information on configuring update policies for macOS, see [Use Microsoft Intune policies to manage macOS software updates | Microsoft Learn](../protect/software-updates-macos.md).

Applies to:
- macOS

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

### Microsoft Tunnel for Mobile Application Management for Android (public preview)<!-- 15769204  -->  
In a public preview, we’re adding support for Mobile Application Management (MAM) to the Microsoft Tunnel VPN gateway. With this preview for Android devices that have not enrolled with Intune, supported apps will be able to use Microsoft Tunnel to connect to your organization when working with corporate data and resources. This includes VPN gateway support for:  

- Secure access to on-premises apps and resources using modern authentication
- Single Sign On and conditional access.

To use Tunnel for MAM on an unenrolled device will require the following three profiles:  

- An App configuration profile for managed apps, to configure Microsoft Defender on devices for use as the Tunnel client app 
- A second App configuration profile for managed apps, to configure Microsoft Edge to connect to Tunnel.
- An App protection profile to enable automatic start of the Microsoft Tunnel connection

For information about using Tunnel on enrolled devices, see [Microsoft Tunnel overview](../protect/microsoft-tunnel-overview.md)

Applies to:

- Android Enterprise

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
