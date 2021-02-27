---
# required metadata
title: What's new in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Find out what's new in the Intune Azure portal
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
<<<<<<< HEAD
ms.date: 03/01/2021
=======
ms.date: 02/24/2021
>>>>>>> abda3d075d0c870198bb0a206ac99b1917c9bb8e
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# What's new in Microsoft Intune

Learn what's new each week in Microsoft Intune in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). You can also find [important notices](#notices), [past releases](whats-new-archive.md), and information about [how Intune service updates are released](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728). 

> [!Note]
> Each [monthly update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) may take up to three days to rollout and will be in the following order:
>
> - Day 1: Asia Pacific (APAC)
> - Day 2: Europe, Middle East, Africa (EMEA)
> - Day 3: North America
> - Day 4+: Intune for Government
>
> Some features may roll out over several weeks and might not be available to all customers in the first week. 
>
> Check the [In development page](in-development.md) for a list of upcoming features in a release.

**RSS feed**: Get notified when this page is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
### Scripts

<!-- ########################## -->
## Week of March 1, 2021 (Service release 2102)

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### App management

#### Support for Win32 app supersedence in Intune<!-- 8517457-->
We've enabled a public preview of app supersedence in Intune. You can now create supersedence relationships between apps, which allows you to update and replace existing Win32 apps with newer versions of the same app, or entirely different Win32 apps. For more information, see [Win32 app supersedence](../apps/apps-win32-supersedence.md).

#### Maximum OS version setting for app conditional launch on Android devices<!-- 7764870  -->
Using Intune app protection policies, you can add a new conditional launch setting to ensure end users are not using any pre-release or beta OS build to access work or school account data on Android devices. This setting ensures that you can vet all OS releases before end users are actively using new OS functionality on Android devices. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you will be able to find this setting by selecting **Apps** > **App protection policies**. For related information, see [How to create and assign app protection policies](../apps/app-protection-policies.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Device configuration

#### Use Cisco AnyConnect as a VPN connection type for Windows 10 and Windows Holographic for Business<!-- 2605377 -->
You can create VPN profiles using Cisco AnyConnect as a connection type (**Devices** > **Device configuration** > **Create profile** > **Windows 10 and later** for platform > **VPN** for profile > **Cisco AnyConnect** for connection type) without needing to use custom profiles.

This policy uses the Cisco AnyConnect app available in the Microsoft store. It doesn't use the Cisco AnyConnect desktop application.

For more information on VPN profiles in Intune, see [Create VPN profiles to connect to VPN servers](../configuration/vpn-settings-configure.md).

Applies to:

- Windows 10 and newer
- Windows Holographic for Business 

#### Run Microsoft Edge version 87 and newer in single app kiosk mode on Windows 10 devices<!-- 8271248   -->
On Windows 10 and newer devices, you configure a device to run as a kiosk that runs one app, or runs many apps (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Kiosk**). When you select single app mode, you can:
- Run Microsoft Edge version 87 and newer.
- Select **Add Microsoft Edge legacy browser** to run Microsoft Edge version 77 and older.

For more information on the settings you can configure in kiosk mode, see [Kiosk settings for Windows 10 and newer devices](../configuration/kiosk-settings-windows.md).

Applies to:
- Windows 10 and newer in single-app kiosk mode
- Microsoft Edge version 87 and newer
- Microsoft Edge version 77 and older

#### Administrative Templates is available in Settings Catalog, and has more settings<!-- 9262405 -->

In Intune, you can use Administrative Templates to create policies (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Administrative Templates** for profile).

In the Settings Catalog, Administrative Templates are also available, and has more settings (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Settings Catalog** for profile).

With this release, admins can configure additional settings that only existed in on-premises group policy, and weren't available in cloud-based MDM. These settings are available for **Windows Insider** client endpoint builds, and may be backported to in-market Windows versions, such as 1909, 2004, or 2010.

If you want to create Administrative Templates, and use all the available settings exposed by Windows, then use the Settings Catalog. 

For more information, see:
- [Use Windows 10 templates to configure group policy settings](../configuration/administrative-templates-windows.md)
- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)

Applies to:
- Windows 10 and newer

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Device enrollment

#### Sync status of enrollment program tokens<!-- 9235108  -->
The sync status for automated device enrollment tokens listed on the **Enrollment program tokens** pane has been removed to minimize confusion. The per-token information continues to be displayed. Enrollment program tokens are used to manage automated device enrollment with Apple Business Manager and Apple School Manager. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) you can find the token list for iOS/iPadOS devices by selecting **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment program tokens**. To find the token list for macOS devices, select **Devices** > **macOS** > **macOS enrollment** > **Enrollment program tokens**. For related information, see [Automatically enroll iOS/iPadOS devices](../enrollment/device-enrollment-program-enroll-ios.md) and [Automatically enroll macOS devices](../enrollment/device-enrollment-program-enroll-macos.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Device management

#### Collect diagnostics remote action<!--2167272   -->
A new remote action, **Collect diagnostics**, lets you collect the logs from corporate devices without interrupting or waiting for the end user. Collected logs include MDM, Autopilot, event viewers, key, Configuration Manager client, networking, and other critical troubleshooting logs. For more information see [Collect diagnostics from a Windows device](..\remote-actions\collect-diagnostics.md).

#### New options for export device data<!--6330532   -->
The following new options are available when exporting device data:
- Only include selected columns in the exported file.
- Include all inventory data in the exported file.
To see these options, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices** > **Export**.

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Device security

#### Use the variable CN={{UserPrincipalName}} in the subject and SAN of SCEP and PKCS certificate profiles for Android Enterprise devices<!-- 9290978   -->
You can now use the User attribute **CN={{UserPrincipalName}}** variable in the subject or SAN of a [PKCS certificate profile](/protect/certificates-pfx-configure#create-a-trusted-certificate-profile) or [SCEP certificate profile](/protect/certificates-profile-scep#create-a-scep-certificate-profile) for Android devices. This support requires the device have a user, such as devices enrolled as:
- Android Enterprise fully managed
- Android Enterprise personally-owned work profile

User attributes are not supported for devices that don’t have user associations, such as devices that are enrolled as Android Enterprise dedicated. For example, a profile that uses *CN={{UserPrincipalName}}* in the subject or SAN won’t be able to get the user principal name when there is no user on the device.

#### Use app protection policies for Defender for Endpoint on Android and iOS<!-- 6486982   7362746  -->
You can now use [Microsoft Defender for Endpoint in app protection policies for devices that run Android or iOS](../protect/advanced-threat-protection-cofigure.md#create-and-assign-app-protection-policy-to-set-device-risk-level).
- Configure your MAM conditional launch policy to include **Max allowed threat level** signals from Microsoft Defender for Endpoint on iOS devices and Android devices.
- Choose to **Block Access** or **Wipe Data** based on whether or not the device meets the expected threat level.

When configured, end users are prompted to install and set up the **Microsoft Defender for Endpoint** app from the applicable app store. As a prerequisite, you must set up your **Microsoft Defender for Endpoint** connector and switch on the toggle to send risk data to your app protection policies. For related information, see [App protection policies overview](../apps/app-protection-policy.md), and [Use Microsoft Defender for Endpoint in Microsoft Intune](..\protect\advanced-threat-protection.md).

#### Configure Attack surface reduction rules to block malware from gaining persistence through WMI<!-- 8902661   -->
You can now configure the rule named **Block persistence through WMI event subscription** as part of an [Attack surface reduction rules](../protect/endpoint-security-asr-policy.md#attack-surface-reduction-profiles) profile in Endpoint security.
 
This rule prevents malware from abusing WMI to attain persistence on a device. Fileless threats employ various tactics to stay hidden, to avoid being seen in the file system, and to gain periodic execution control. Some threats can abuse the WMI repository and event model to stay hidden.
 
When configured as [setting for *Attack surface reduction*](,,/protect/endpoint-security-asr-profile-settings.md#attack-surface-reduction-rules-profile) policy for Endpoint security, the following options are available:
- **Not configured** (default) – The setting returns to the Windows default, which is off and persistence is not blocked.
- **Block** – Persistence through WMI is blocked.
- **Audit** – Evaluate how this rule affects your organization if its enabled (set to Block).
- **Disable** - Turn this rule off. Persistence is not blocked.
 
This rule doesn’t support the *Warn* option, and is also available as a Device configuration setting from the [Settings catalog](../configuration/settings-catalog.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Intune apps

#### Company Portal website improved load performance<!-- 8765415  -->
To improve page load performance, app icons will now load in batches. End users may see a placeholder icon for some of their applications when visiting the Company Portal website. The related icons will load shortly after. For more information about the Company Portal, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md) and [Manage apps from the Company Portal website](../user-help/manage-apps-cpweb.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Monitor and troubleshoot

#### Restart frequency (preview) in Endpoint analytics <!--IN6225459 -->
Endpoint analytics [startup performance](../../analytics/startup-performance.md) currently provides IT with insights to measure and optimize PC boot times. However, restart frequency can be just as impactful to the user experience since a device that reboots daily because of blue screens will have a poor user experience even if the boot times are fast. We have now included a preview report on restart frequencies within your organization to help you identify problematic devices. For more information, see [Restart frequency (preview) in endpoint analytics](../../analytics/restart-frequency.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Role-based access control

#### Role-based access permissions update for Microsoft Tunnel Gateway<!-- 8554762   -->
To help control who has rights to manage the Microsoft Tunnel, we've added [**Microsoft Tunnel Gateway**](/intune/protect/microsoft-tunnel-prerequisites#permissions) as a new permissions group to Intune role-based access control. This new group includes the following permissions:

- **Create** - Configure Microsoft Tunnel Gateway servers, server configurations, and sites.
- **Update** (modify) - Update Microsoft Tunnel Gateway servers, server configurations, and sites.
- **Delete** - Delete Microsoft Tunnel Gateway servers, server configurations, and sites.
- **Read** - View Microsoft Tunnel Gateway servers, server configurations, and sites.

By default, Intune Administrators and Azure Active Directory administrators have these permissions. You can also add these permissions to [custom roles you create](/fundamentals/create-custom-role) for your Intune tenant.

#### Scope tag support for customization policies for Intune for Government and 21Vianet<!--9419267  -->
You can now assign scope tags to Customization policies for Intune for Government and Intune operated by 21Vianet. To do so, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration**> **Customization** where you will see **Scope tags** configuration options. 

<!-- ########################## -->
## Week of February 22, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### New version of the PFX Certificate Connector<!-- 9333009 -->

We’ve released a new version of the PFX Certificate Connector, version **6.2101.13.0**. This new connector version adds [improvements for logging](../protect/certificate-connectors.md#logging) to the PFX Connector:

- New location for Event Logs, with logs broken down into Admin, Operational & Debug
- Admin & Operational logs default to 50 MB - with auto archiving enabled.
- EventIDs for PKCS Import, PKCS Create and Revocation.

For more information about certificate connectors, including a list of connector releases for both certificate connectors, see [Certificate connectors](../protect/certificate-connectors.md).

<!-- ########################## -->
## Week of February 8, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### App management

#### End users can restart an app install from the Windows Company Portal<!-- 652935 -->
Using the Windows Company Portal, end users can restart an app installation if the progress seems to have stalled or is frozen. This functionality is allowed if the app installation progress has not changed in two hours. For related information, see [Add apps to Microsoft Intune](../apps/apps-add.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Device configuration

#### Google’s compliance screens are automatically shown on Android Enterprise 9.0+ dedicated devices running in kiosk mode<!-- 9323100  -->

In Intune, you can create a device configuration password policy and a device compliance password policy on Android Enterprise devices.

When you create the policies, Android Enterprise dedicated devices running in kiosk mode automatically use Google’s compliance screens. These screens guide and force users to set a password that meets your policy rules.

For more information on creating password and kiosk policies, see:

- [Android Enterprise settings to mark devices as compliant or not compliant](../protect/compliance-policy-create-android-for-work.md)
- [Android Enterprise device settings to allow or restrict features](../configuration/device-restrictions-android-for-work.md)

Applies to:

- Android Enterprise 9 and newer in kiosk mode

<!-- ########################## -->
## Week of February 1, 2021 (2101 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### App management

#### Configure whether a required iOS/iPadOS app is removable<!-- 8391462  -->
You can now configure whether a required iOS/iPadOS app is installed as a removable app by end users. This new setting applies to iOS store, LOB and built-in apps. You can find this setting in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** > **Add**. When setting the app assignments, you can select **Install as removable**. The default value is **Yes**, which means the app is removable. Existing required installs on iOS 14 have been updated to the default (removable) setting value. For more information about iOS/iPadOS apps, see [Microsoft Intune app management](..\apps\app-management.md).

#### Line-of-business apps supported on Shared iPad devices<!-- 8834566  -->
You can now deploy line-of-business (LOB) apps to Shared iPad devices. The line-of-business app must be assigned as **required** to a device group containing Shared iPad devices from the Microsoft Endpoint Manager admin center. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > **Add**. For related information, see [Add an iOS/iPadOS line-of-business app to Microsoft Intune](../apps/lob-apps-ios.md).

#### Microsoft Endpoint Configuration Manager connector <!-- 9229333, CM7138634 -->
The connector for Microsoft Endpoint Configuration Manager now displays in the admin center. To review the connector, go to **Tenant administration** > **Connectors and tokens** > **Microsoft Endpoint Configuration Manager**. Select a Configuration Manager hierarchy running version 2006, or later to display additional information about it.

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Device configuration

#### New version of the PFX Certificate Connector<!-- 9202990  -->

We’ve released a new version of the PFX Certificate Connector, version **6.2009.2.0**. This new connector version:

- Improves upgrade of the Connector to persist accounts that run Connector Services.

For more information about certificate connectors, including a list of connector releases for both certificate connectors, see [Certificate connectors](../protect/certificate-connectors.md).

#### Use device configuration to create folders and set the grid size on the Managed Home Screen<!-- 3041948 -->
On Android Enterprise dedicated devices, you can configure the Managed Home Screen settings (**Devices** > **Device configuration** > **Create profile** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile > Device restrictions** for profile > **Device experience**).

When using the Managed Home Screen in multi-app kiosk mode, there's a **Custom app layout** setting. With this setting, you can:
- Create folders, add apps to these folders, and put the folder on the Managed Home Screen. You don't have to order the folders.
- Choose whether or not to order apps and folders on the Managed Home Screen. If you order, you can also:

  - Set the grid size.
  - Add apps and folders to different places on the grid.

Previously, you had to use an [app configuration policy](../apps/app-configuration-managed-home-screen-app.md). 

For more information, see [Android Enterprise dedicate devices device experience settings](../configuration/device-restrictions-android-for-work.md#device-experience).

Applies to:
- Android Enterprise dedicated devices

#### Use the settings catalog to configure Microsoft Edge browser on macOS devices - public preview <!-- 4552197   -->
Currently on macOS devices, you configure the Microsoft Edge browser using a .plist preference file (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Preference file** for profile).

There's an updated UI to configure the Microsoft Edge browser: **Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog (preview)** for profile. Select the Microsoft Edge settings you want, and then configure them. In your profile, you can also add settings, or remove existing settings.

To see a list of the settings you can configure, go to [Microsoft Edge - Policies](/DeployEdge/microsoft-edge-policies). Be sure macOS is listed as a supported platform. If some settings aren't available in the settings catalog, then it's recommended to continue using the preference file only. 

For more information, see:
- [Settings catalog](../configuration/settings-catalog.md)
- [Add a property list file to macOS devices using Intune](../configuration/preference-file-settings-macos.md)

To see the policies you have configured, open Microsoft Edge, and go to [edge://policy](edge://policy).

Applies to:
- Microsoft Edge browser version 77 and newer on macOS 

#### Use NetMotion Mobility as a VPN connection type for Android Enterprise devices<!-- 7764263 7862120  -->
When you create a VPN profile, NetMotion Mobility is available as a VPN connection type for Android Enterprise:
- **Devices** > **Device configuration** > **Create profile** > **Android Enterprise** > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **VPN** for profile > **NetMotion Mobility**  for connection type
- **Devices** > **Device configuration** > **Create profile** > **Android Enterprise** > **Personally-Owned Work Profile** > **VPN** for profile > **NetMotion Mobility** for connection type

For more information on VPN profiles in Intune, see [Create VPN profiles to connect to VPN servers](../configuration/vpn-settings-configure.md).

Applies to:
- Android Enterprise Personally-Owned Work Profile
- Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile

#### Settings catalog and Templates when creating device configuration profiles for macOS and Windows 10 devices<!-- 8673623 8254609  -->
There are UI updates when creating device configuration profiles for macOS and Windows 10 devices (**Devices** > **Configuration profiles** > **Create profile** > **macOS** or **Windows 10 and later** for platform).

The profile shows **Settings catalog - preview** and **Templates**:
- **Settings catalog - preview**: Use this option to start from scratch and select settings you want from the library of available settings. For macOS, the settings catalog includes settings to configure the Microsoft Edge version 77 and newer. Settings catalog for Windows 10 includes many existing settings, and new settings, all in one place.
- **Templates**: Use this option to configure all the existing profiles, such as device restrictions, device features, VPN, Wi-Fi, and more.

This is only a UI change, and doesn't impact existing profiles.

For more information, see [Settings catalog](../configuration/settings-catalog.md).

Applies to:
- macOS device configuration
- Windows 10 device configuration

#### Home screen layout updates on supervised iOS/iPadOS devices<!-- 8710594 7978976    -->
On iOS/iPadOS devices, you can configure the Home Screen layout (**Devices** > **Device Configuration** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **Home screen layout**). In Intune, the Home Screen Layout feature is updated:

- <!-- 8710594 --> The home screen layout has a new design. This feature allows admins to see in real time how the apps and app icons look on pages, the dock, and within folders. When adding apps in this new designer, you can't add separate pages. But, when you add nine or more apps to a folder, then those apps automatically go on the next page.
    Existing policies are not impacted, and don't need to be changed. The setting values are transferred to the new UI without any negative effects. The setting behavior on devices is the same. 
- <!-- 7978976 --> Add a web link (web app) to a page, or to the dock. Be sure you add a specific URL of the web link only once. Existing policies are not impacted, and don't need to be changed.

For more information on the settings you can configure, including the home screen layout, see [iOS/iPadOS device settings to use common iOS/iPadOS features in Intune](../configuration/ios-device-features-settings.md).

Applies to:
- iOS/iPadOS supervised devices

#### Limit Apple's personalized advertising on iOS/iPadOS devices<!-- 8518601  -->
On iOS/iPadOS devices, you can configure Apple's personalized advertising. When enabled, personalized ads are limited in the App Store, Apple News, and Stocks apps (**Devices** > **Device Configuration** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile > **General** > **Limit Apple personalized advertising**).

This setting only impacts personalized ads. Configuring this setting sets **Settings** > **Privacy** > **Apple Advertising** to **off**. It doesn't impact non-personalized ads in the App Store, Apple News, and Stocks apps. For more information on Apple's advertising policy, see [Apple Advertising & Privacy](https://support.apple.com/HT205223) (opens Apple's web site).

To see the current settings you can configure in Intune, go to [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md).

Applies to:
- iOS/iPadOS 14.0 and newer, devices enrolled with device enrollment or automated device enrollment

#### Administrative templates includes new policies for Microsoft Edge version 88<!-- 9021341  -->
You can configure and deploy new ADMX settings that apply to Microsoft Edge version 88. To see the new policies, go to [Microsoft Edge release notes](https://docs.microsoft.com/deployedge/microsoft-edge-relnote-stable-channel#policy-updates).

For more information on this feature in Intune, see [Configure Microsoft Edge policy settings](../configuration/administrative-templates-configure-edge.md).

Applies to:
- Windows 10 and newer

#### Locale support in email notifications for non-compliance<!--7604191    -->
Compliance policies now support [Notification message templates](../protect/actions-for-noncompliance.md#create-a-notification-message-template) that include separate messages for different locales. Support for multiple languages no longer requires you to create separate templates and policies for each locale.

When you configure locale-specific messages in a template, non-compliant end-users receive the appropriate localized email notification message based on their O365 preferred language. You also designate one localized message in the template as the *default* message. The default message is sent to users that haven’t set a preferred language or when the template doesn’t include a specific message for their locale.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Hide more screens for the Apple Automated Device Enrollment Setup Assistant <!--7786092   -->
You can now set Automated Device Enrollment (ADE) profiles to hide these Setup Assistant Screens for iOS/iPadOS 14.0+ and macOS 11+ devices:
- Restore Completed, for iOS/iPadOS 14.0+.
- Software Update Completed, for iOS/iPadOS 14.0+.
- Accessibility, for macOS 11+ (the mac device must be connected to an Ethernet).

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Device management
 
#### Migrate device security polices from Basic Mobility and Security to Intune<!--6306140   -->
The policy migration tool lets you permanently move Mobile Device Management (MDM) device security policies deployed by Basic Mobility and Security (formerly MDM for Office 365 or Office MDM) to standard Intune MDM configuration profiles and compliance policies. Using this tool will disable all future policy creation and edits in Basic Mobility and Security device security policies.

To use the tool, you must:
- Already have purchased (but not yet assigned) Intune licenses for all the users of devices managed by Basic Mobility and Security.
- Contact support to check eligibility if you have purchased an Intune for Education subscription. 

For more information, see [Migrate your mobile device management from Basic Mobility and Security to Intune](migrate-to-intune.md).

#### Subnet ID and IP addresses on Properties page for corporate-owned Windows devices<!--5265589   -->
Subnet ID and IP addresses are now displayed on the **Properties** page for corporate-owned Windows devices. To see them, go to [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices** > choose a corporate-owned Windows device > **Properties**.

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Device security

#### Intune support for Microsoft Defender Application Guard now includes isolated Windows environments<!-- 8274282     -->
When you configure **Turn on Application Guard**  in an Intune [App and browser isolation profile](../protect/endpoint-security-asr-profile-settings.md#app-and-browser-isolation) in Endpoint security Attack surface reduction policy, you can choose from the following options when you enable Application Guard:

- **Microsoft Edge** - *Previously available*
- **Isolated Windows environments** - *New with this update*
- **Microsoft Edge** ***and*** **isolated Windows environments** - *New with this update*

Before this release, the setting was named *Turn on Application Guard for Edge (Options)*.

The new options for this setting expand Application Guard support beyond just URL’s for Edge. You can now enable Application Guard to help protect devices by opening potential threats in a hardware isolated Windows VM environment (container). For example, with support for isolated Windows environments, Application Guard can open untrusted Office documents in an isolated Windows VM.

With this change:
- Intune now supports the full range of values found in the Windows MDM CSP: [AllowWindowsDefenderApplicationGuard](/windows/client-management/mdm/windowsdefenderapplicationguard-csp).
- To help you understand the affect on device users when using isolated Windows environments, see [Application Guard testing scenarios](/windows/security/threat-protection/microsoft-defender-application-guard/test-scenarios-md-app-guard) in the Windows security documentation.
- Read more about Application Guard and support for Office apps in [Application Guard for Office](/microsoft-365/security/office-365-security/install-app-guard?view=o365-worldwide&preserve-view=true) in the Microsoft 365 documentation. 

#### New Application Guard settings in Attack surface reduction policy<!-- 8274336   -->
We’ve added two new settings to the App and browser isolation profile of Intune’s [Endpoint security Attack surface reduction policy](../protect/endpoint-security-asr-policy.md):
- **Application Guard allow camera and microphone access** – Manage access by Application Guard apps to a devices camera and microphone.
- **Application Guard allow use of Root Certificate Authorities from the user's device** – When you specify one or more root certificate thumbprints, the matching certificates are transferred to the Microsoft Defender Application Guard container.

For more information, see the settings for [App and browser isolation](../protect/endpoint-security-asr-profile-settings.md#app-and-browser-isolation).


#### Updates for Security Baselines<!-- 8391335, 8377369   -->
We have new versions available for the following [security baselines](../protect/security-baselines.md):  
- **[MDM Security baseline (Windows 10 Security)](../protect/security-baseline-settings-mdm-all.md?pivots=december-2020)**
- **[Microsoft Defender for Endpoint baseline](../protect/security-baseline-settings-defender-atp.md?pivots=december-2020)**
 
Updated baseline versions bring support for recent settings to help you maintain the best-practice configurations recommended by the respective product teams.

To understand what's changed between versions, see [Compare baseline versions](../protect/security-baselines.md#compare-baseline-versions) to learn how to export a .CSV file that shows the changes.  

#### Endpoint Security Firewall reports<!-- 5653366    -->
We’ve added two new reports that are dedicated to Firewall policies in Endpoint Security:
- [Windows 10 MDM devices with firewall off](../protect/endpoint-security-policy.md) is found in the Endpoint security node and displays the list of Windows 10 devices with the Firewall turned off. This report identifies each device by device name, device ID, user information, and the Firewall status.   
- [Windows 10 MDM Firewall status](../fundamentals/reports.md#windows-10-mdm-firewall-status-organizational) is an organizational report found in the *Reports* node, which lists the firewall status for your Windows 10 devices. This report displays status information that includes if the firewall is enabled, disabled, limited, or temporarily disabled.  

#### Summary view for Defender Antivirus reports<!-- 8846877   -->
We’ve updated the view for the Microsoft Defender Antivirus reports found in the **Reports** node of the Microsoft Endpoint Manager admin center. Now, when you select Microsoft Defender Antivirus in the **Reports** node, you’ll see the default view of the **Summary** tab, and a second tab for **Reports**. The **Reports** tab is where you’ll find the previously available [Antivirus agent status](../fundamentals/reports.md#antivirus-agent-status-report-organizational) and [Detected malware](../fundamentals/reports.md#detected-malware-report-organizational) organizational reports.
 
The new **Summary** tab displays the following information:
- Displays aggregate details for the Antivirus reports. 
- Includes a *Refresh* option that updates the counts of devices in each antivirus state. 
- Reflects the same data as found in the [Antivirus agent status organizational](../fundamentals/reports.md#antivirus-agent-status-report-organizational) report, which is now accessed from the **Reports** tab.

#### App protection policy support on Android and iOS/iPadOS for additional Mobile Threat Defense partners<!-- 8846351  -->
In October of 2019, Intune app protection policy added the capability to use data from our Microsoft Threat Defense partners.

With this update, we're expanding this support to the following partner for using an app protection policy to block or selectively wipe a user’s corporate data based on the health of the device:
- **McAfee MVision Mobile** on Android, iOS and iPadOS

For more information, see [Create Mobile Threat Defense app protection policy with Intune](../protect/mtd-app-protection-policy.md).

#### Increased certificate validity period for SCEP and PKCS profiles<!-- 8629805   -->
Intune now supports a **Certificate validity period** of up to **24** months in certificate profiles for [Simple Certificate Enrollment Protocol](../protect/certificates-profile-scep.md#create-a-scep-certificate-profile) (SCEP) and [Public Key Cryptography Standards](../protect/certificates-pfx-configure.md#create-a-pkcs-certificate-profile) (PKCS). This is an increase from the previous support period of up to 12 months.

This support applies to Windows and Android. Certificate validity periods are ignored by iOS/iPadOS and macOS.

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Monitor and troubleshoot

#### New co-management eligibility organizational report<!-- 7854306  -->
The **Co-management eligibility** report provides an eligibility evaluation for devices that can be co-managed. Co-management enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune. You will be able to view a summary for this report in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Reports** > **Cloud attached devices** > **Reports** tab > **Co-management eligibility**. For related report information, see [Intune reports](../fundamentals/reports.md).

#### New co-managed workloads organizational report<!-- 7854306  -->
The **Co-Managed Workloads** report provides a report of devices that are currently co-managed. Co-management enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune. You can view this report in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Reports** > **Cloud attached devices** > **Reports** tab >  **Co-Managed Workloads**. For more information, see [Intune reports](../fundamentals/reports.md).

#### Log Analytics include device details log<!--6014987  -->
Intune device detail logs are now available. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports** > **Log analytics**. You can correlate a set of device details to build custom queries and Azure workbooks. For more information, see [Azure Monitor integration reports (Specialist)](../fundamentals/reports.md#azure-monitor-integration-reports-specialist).


<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Role-based access control

#### Scope tag support for the Enrollment Status Page <!--4172335 -->
You can now assign scope tags to the Enrollment Status Page so only the roles you define will be able to see it. For more information, see [Create Enrollment Status Page profile and assign to a group](../enrollment/windows-enrollment-status.md#create-enrollment-status-page-profile-and-assign-to-a-group).

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Scripts

#### Additional Data Warehouse beta properties<!-- 8612282  -->
Additional properties are now available using the Intune Data Warehouse beta API. The following properties are exposed via the [devices](../developer/reports-ref-devices.md) entity in the beta API:
- `SubnetAddressV4Wifi` - The subnet address for IPV4 Wi-Fi connection.
- `IpAddressV4Wifi` - The IP address for IPV4 Wi-Fi connection.

For related information, see [Microsoft Intune Data Warehouse API](../developer/reports-nav-intune-data-warehouse.md).


<!-- ########################## -->
## Week of January 25, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### App management

#### Application icon update for iOS, macOS, and web Company Portal<!-- 7113985 -->
We've updated the app icon for the Company Portal for iOS, macOS, and web. This icon is also used by the Company Portal for Windows. End users will see the new icon in their device's application launcher and home screen, in Apple's App Store, and in experiences within the Company Portal apps.

#### Android Enterprise system app support in personally-owned work profiles<!-- 5291507 -->
You can now deploy Android Enterprise system apps to Android Enterprise personally-owned work profile devices. System apps are apps that do not appear in the Managed Google Play Store and often come pre-installed on the device. Once a system app is deployed, you will be unable to uninstall, hide, or otherwise remove the system app. For related information about system apps, see [Add Android Enterprise system apps to Microsoft Intune](../apps/apps-ae-system.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Monitor and troubleshoot

#### Update when exporting Intune reports using the Graph API<!-- 8764428 -->
When you use the `exportJobs` Graph API to export Intune reports without selecting any columns for the devices report, you will receive the default column set. To reduce confusion, we have removed columns from the default column set. The removed columns are `PhoneNumberE164Format`, `_ComputedComplianceState`, `_OS`, and `OSDescription`. These columns are still available for selection if you need them, but only explicitly, and not by default. If you have built automation around the default columns of the device export, and that automation uses any of these columns, you need to refactor your processes to explicitly select these and any other relevant columns. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

<!-- ########################## -->
## Week of January 18, 2021

### Device configuration

#### Microsoft Tunnel now supports Red Hat Enterprise Linux 8<!-- 8981769 -->

You can now use Red Hat Enterprise Linux (RHEL) 8 with the [Microsoft Tunnel](../protect/microsoft-tunnel-prerequisites.md#linux-server). To make use of for RHEL 8 you won't need to take any actions. Support has been added to the Docker containers which update automatically. In addition, this update also suppresses some extraneous logging.

<!-- ########################## -->
## Week of January 11, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### App management

#### Deleting Win32 apps in a dependency relationship<!-- 8997490 -->
Win32 apps added to Intune cannot be removed if they are in a dependency relationship. These apps can only be deleted after the dependency relationship is removed. This requirement is applied to both parent and child apps in a dependency relationship. Also, this requirement ensures that dependencies are enforced properly and that dependency behavior is more predictable. For more information, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

#### Scope tag support for customization policies<!--6182440  -->
You can now assign scope tags to Customization policies. To do so, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration**> **Customization** where you will see **Scope tags** configuration options. This feature is now available for Intune for Government or Intune operated by 21Vianet.

<!-- vvvvvvvvvvvvvvvvvvvvvv --> 
### Device configuration

#### New version of the PFX Certificate Connector<!-- 9139477 -->  

We’ve released a new version of the PFX Certificate Connector, version **6.2009.1.9**. This new connector version:

- Improvements to the renewal of the connector certificate.

For more information about certificate connectors, including a list of connector releases for both certificate connectors, see [Certificate connectors](../protect/certificate-connectors.md).

<!-- ########################## -->
## Week of January 4, 2021

### App management

#### Browser access enabled automatically during Android work profile enrollment<!-- 5411101  -->

During new Android Enterprise personally-owned work profile enrollments, browser access is now automatically enabled on the device. With this change, compliant devices can use the browser to access resources that are protected by conditional access without needing to take additional actions. Before this change, users had to launch the Company Portal and select **Settings** > **Enable Browser Access**, and then click **Enable**.

This change has no impact on devices that are already enrolled.


#### Win32 app download progress bar<!-- 5145837 -->
End users will now see a progress bar in the Windows Company Portal while a Win32 app is being downloaded. This feature will help customers better understand the app installation progress.  

#### Update to Company Portal for Android app icon<!-- 7114401 -->
We've updated the Company Portal for Android app icon to create a more modern look and feel for device users. To see what the new icon looks like, go to the [Intune Company Portal listing on Google Play](https://go.microsoft.com/fwlink/?linkid=2151341).  

<!-- ########################## -->
## Week of December 7, 2020

### Intune apps

#### Newly available protected apps for Intune<!-- 8766223 -->
The following protected apps are now available for Microsoft Intune:
- Dynamics 365 Remote Assist
- Box - Cloud Content Management
- STid Mobile ID
- FactSet 3.0
- Notate for Intune
- Field Service (Dynamics 365)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

<!-- ########################## -->
## Week of November 23, 2020

### App management

#### PowerShell scripts execute before apps, and time out reduced<!-- 8829670 -->

There are some updates to PowerShell scripts:

- Microsoft Intune management extension execution flow is reverted back to processing PowerShell scripts first, and then running Win32 apps.
- To resolve an Enrollment Status Page (ESP) time out issue, PowerShell scripts time out after 30 minutes. Previously, they timed out after 60 minutes.

For more information, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md).


<!-- ########################## -->
## Week of November 16, 2020  (2011 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->  
### Device configuration

#### Power menu, status bar notifications, and more restrictive settings available for Android Enterprise dedicated devices<!-- 6184533  -->
On Intune enrolled Android Enterprise dedicated devices running single or multi-app kiosk mode, you can:
- Restrict the power menu, system error warnings, and access to the Settings app.
- Choose if users can see the home and overview buttons, and notifications. 

To configure these settings, create a device restrictions configuration profile: **Devices** > **Configuration Profiles** > **Create profile** > **Android Enterprise** for platform > **Fully managed, dedicated, and Corporate-owned work profile > Device restrictions** > **General**.

For more information on these settings, and the other settings you can configure, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android Enterprise dedicated devices

#### New show previews setting for app notifications on iOS/iPadOS devices<!-- 8351845   -->
On iOS/iPadOS devices, there's a **Show Previews** setting (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **App Notifications**). Use this setting to choose when recent app notification previews are shown on devices.

For more information on app notification settings, and other settings you can configure, see [device settings to use common iOS/iPadOS features](../configuration/ios-device-features-settings.md).

#### On-demand rules with Microsoft Tunnel for iOS<!-- 8460915    -->
The Microsoft Tunnel now supports [on-demand rules for iOS/iPad devices](../protect/microsoft-tunnel-configure.md#ios). With on-demand rules you can specify the use of the VPN when conditions are met for specific FQDNs or IP addresses. 
 
To configure on-demand rules for iOS/iPadOS with Microsoft Tunnel, configure a VPN Profile for iOS/iPadOS as part of device configuration policy. On the profiles *Configuration settings* page, select *Microsoft Tunnel* as the *Connection type* and you’ll then have access to configure **On-Demand VPN Rules**.
 
For information about the on-demand VPN rules you can configure, see [Automatic VPN settings](../configuration/vpn-settings-ios.md#automatic-vpn).

Applies to:
- iOS/iPadOS

#### More authentication settings for Wi-Fi profiles on Windows 10 and newer devices<!-- 7980773 -->
New settings and features for Wi-Fi profiles on devices running Windows 10 and newer (**Devices** > **Device Configuration** > **Create profile** > **Windows 10 and later** for platform > **Wi-Fi** for profile > **Enterprise**):

- **Authentication mode**: Authenticate the user, device, either, or use guest authentication.
- **Remember credentials at each logon**: Force users to enter credentials whenever they connect to the VPN. Or, cache the credentials so users only enter their credentials once.
- More granular control over authentication behavior, including:
  - Authentication period
  - Authentication retry delay period
  - Start period
  - Maximum EAPOL-Start messages
  - Maximum authentication failures

- **Use separate VLANs for device and user authentication**: When using single sign-on, the Wi-Fi profile can use a different virtual LAN based on the user’s credentials. Your Wi-Fi server must support this feature.

To see these settings, and all the settings you can configure, go to [Add Wi-Fi settings for Windows 10 and later devices in Intune](../configuration/wi-fi-settings-windows.md).

Applies to:
- Windows 10 and newer

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Personally-owned work profile terminology<!--8361769   -->
To avoid confusion, the term for the *work profile* Android Enterprise management scenario will be changed to "personally-owned devices with a work profile" or *personally-owned work profile* throughout the Intune documentation and user interface. This is to differentiate it from the "corporate-owned work profile" (COPE) management scenario.

#### Windows Autopilot for HoloLens 2 (preview)<!--6305220   -->
Windows Autopilot for HoloLens 2 devices is now in public preview. Admins no longer have to register their tenants for flighting. For more information on using Autopilot for HoloLens, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot).

#### Ending support for iOS 11<!--7327321  -->
Intune enrollment and the Company Portal now support iOS versions 12 and later. Older versions aren't supported but will continue to receive policies.

#### Ending support for macOS 10.12<!--7327326  -->
Since macOS Big Sur has released, Intune enrollment and the Company Portal now support macOS versions 10.13 and later. Older versions aren't supported.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### New setting for Device Control profile for endpoint security<!-- 8456551     -->
We’ve added a new setting, **Block write access to removable storage** to the [Device control profile](../protect/endpoint-security-account-protection-profile-settings.md)  for Attack surface reduction policy in endpoint security.  When set to *Yes*, write access to removable storage is blocked.

#### Improvements to settings in Attack surface reduction rule profiles <!-- 7319334     -->
We’ve updated the options for applicable [settings in the Attack surface reduction rule profile](../protect/endpoint-security-asr-profile-settings.md#attack-surface-reduction-rules-profile) which is part of endpoint securities Attack surface reduction policy.  

We've brought consistency across settings to existing options, like *Disable* and *Enable*, and added a new option, *Warn*:  

- **Warn** - On devices that run Windows 10 version 1809 or later, the device user receives a message that they can bypass the setting. For example, on the setting *Block Adobe Reader from creating child processes*, the option of *Warn* presents users with the option to bypass that block and allow Adobe Reader to create a child process. On devices that run earlier versions of Windows 10, the rule enforces the behavior without the option to bypass it. 


#### Policy merge support for USB device ID’s in Device control profiles for endpoint security Attack surface reduction policy<!-- 7645254   -->
We’ve added support for *policy merge* of USB device ID’s to the [Device control](../protect/endpoint-security-asr-policy.md) profile for the endpoint security Attack surface reduction policy. The following settings from *device control* profiles are evaluated for policy merge:
- Allow hardware device installation by device identifiers
- Block hardware device installation by device identifiers
- Allow hardware device installation by setup classes
- Block hardware device installation by setup classes 
- Allow hardware device installation by device instance identifiers 
- Block hardware device installation by device instance identifiers 

Policy merge applies to the configuration of each setting across the different profiles that apply to a device. It doesn’t include evaluation between different settings, even when two settings are closely related.

For a more detailed example of what merges, and how to allow and block lists for each supported setting gets merged and applies on a device, see [Policy merge for settings](../protect/endpoint-security-asr-policy.md#policy-merge-for-settings) for device control profiles.

#### Improved Antivirus status operations report for endpoint security<!-- 7771023   -->
We’ve added new details to the [Antivirus status operations](reports.md#antivirus-agent-status-report-organizational) report for Windows Defender Antivirus, which is an endpoint security policy report.  
 
The following new columns of information will be available for each device:
 
- **Product status** – The status of Windows Defender on the device.
- **Tamper protection** – Is tamper protection enabled or disabled.
- **Virtual machine** – Is the device a virtual machine, or physical device.

#### Improved rule merge for Attack surface reduction rules<!--7798290      -->
Attack surface reduction rules now support new behavior for merger of settings from different policies, to create a superset of policy for each device. Only the settings that are not in conflict are merged, while those that are in conflict are not added to the superset of rules. Previously, if two policies included conflicts for a single setting, both policies were flagged as being in conflict, and no settings from either profile would be deployed.

Attack surface reduction rule merge behavior is as follows:

- Attack surface reduction rules from the following profiles are evaluated for each device the rules apply to:
  - Devices > Configuration policy > Endpoint protection profile > Microsoft Defender Exploit Guard > [Attack Surface Reduction](../protect/endpoint-protection-windows-10.md#attack-surface-reduction).
  - Endpoint security > Attack surface reduction policy > [Attack surface reduction rules](../protect/endpoint-security-asr-policy.md#attack-surface-reduction-profiles).
  - Endpoint security > Security baselines > Microsoft Defender for Endpoint Baseline > [Attack Surface Reduction Rules](../protect/security-baseline-settings-defender-atp.md#attack-surface-reduction-rules).
- Settings that do not have conflicts are added to a superset of policy for the device.
- When two or more policies have conflicting settings, the conflicting settings are not added to the combined policy, while settings that don’t conflict are added to the superset policy that applies to a device.
- Only the configurations for conflicting settings are held back.

#### MVISION Mobile – New Mobile Threat Defense partner <!-- 8112625  --> 
You can control mobile device access to corporate resources using Conditional Access based on risk assessment conducted by [MVISION Mobile](../protect/mcafee-mobile-threat-defense-connector.md), a Mobile Threat Defense solution from McAfee that integrates with Microsoft Intune.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### New Intune operational report to help troubleshoot configuration profile issues<!-- 6471222  -->
A new **Assignment failures** operational report is available in public preview to help troubleshoot errors and conflicts for configuration profiles that have been targeted to devices. This report will show a list of configuration profiles for the tenant and the number of devices in a state of error or conflict. Using this information, you can drill down to a profile to see a list of devices and users in a failure state related to the profile. Additionally, you can drill down even further to view a list of settings and setting details related to the cause of the failure. You have the ability to filter, sort, and search across all of the records throughout the report. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can find this report by selecting **Devices** > **Monitor** > **Assignment failures (preview)**. For more information about reports in Intune, see [Intune reports](../fundamentals/reports.md).

#### Reporting updates for Windows Virtual Desktop VMs<!--5736314   -->
The following settings are marked as **Not applicable** in the Policy reports:
- BitLocker settings
- Device encryption
- Defender Application Guard settings
- Defender Tamper Protection
- Wi-Fi profiles

#### Noncompliant policies report to troubleshoot devices in error or that are noncompliant<!-- 6471368    -->
In preview, the new **Noncompliant policies** report is an operational report you can use to help troubleshoot errors and conflicts for compliance policies targeting devices. The [Noncompliant policies report](reports.md#noncompliant-policies-operational) displays a list of compliance policies that have one or more devices with errors or that are in a state of noncompliance to the policy.

Use this report to:
 
- View the device compliance policies with devices in a noncompliant or error state, and then drill in to view of the list of devices and users in a failed state.
- Drill down further to see the list of settings and setting information causing a failure.
- Filter, sort, and search across all records in the report. We've added paging controls and improved export capability to a csv file.
- Identify when issues are occurring, and streamline troubleshooting.
 
For more information on monitoring device compliance, see [Monitor Intune Device compliance policies](../protect/compliance-policy-monitor.md).




<!-- ########################## -->
## Week of November 9, 2020  


<!-- vvvvvvvvvvvvvvvvvvvvvv -->  
### App management  

#### Improvements to work profile messaging in Company Portal for Android<!--8378333  -->
We've updated messaging in Company Portal for Android to better introduce and explain how work profile works. The new messaging appears:  
* After the work profile setup flow. Users see a new informational screen explaining where to find work apps, with links to help documentation.  
* When a user accidentally re-enables the Company Portal app in the personal profile. We redesigned a screen (**Your device now has a profile just for work**) with clearer explanations and new illustrations to guide users to their work apps, with links to help documentation.  
* On the **Help** page. In the **Frequently Asked Questions** section, there's a new link to help documentation about how to set up work profile and find apps.  

<!-- ########################## -->
## Week of October 26, 2020 (2010 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### New and updated planning, setup, and enrollment deployment guides

The existing planning and migration guides are rewritten, and updated with new guidance. There's also some new deployment guides that focus on Intune setup, and enrollment for Android, iOS/iPadOS, macOS, and Windows devices.

For more information, go to [Overview](migration-guide.md).

### App management

#### Apps that require enrollment are hidden when enrollment is set to unavailable<!-- 6305901  -->
Apps assigned with the **Available for enrolled devices** and **Required** intents won't be displayed in the Company Portal for users where the device enrollment setting is set to **Unavailable**. This change is only applicable when viewing the Company Portal app or website from an unenrolled device, including unenrolled devices that use app protection policies (MAM-WE). The apps will still be visible for users viewing the Company Portal from an enrolled device, regardless of the value of the **Device enrollment** setting. For more information, see [Device enrollment setting options](../apps/company-portal-app.md#device-enrollment-setting-options).

#### Improvements to iOS Company Portal privacy message customization<!-- 7006929  -->
You now have greater ability to customize the privacy messaging in the iOS Company Portal. In addition to the previous support for being able to customize what your organization *can't see*, you will now also be able to customize what your organization's *can see* in the privacy message displayed to end users in the iOS Company Portal. To support this feature, devices will need to be running at least Company Portal version 4.11 to see the customized messaging about what can be seen. This feature will be available in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Customization**. For related information, see the Company Portal [Privacy](../apps/company-portal-app.md#privacy) message. 

#### Android app protection policies (MAM) on COPE devices<!-- 7088497  -->
Newly added Mobile Application Management (MAM) support enables Android app protection policies on Android Enterprise corporate-owned​ devices with a work profile (COPE). For more information about app protection policies, see [App protection policies overview](../apps/app-protection-policy.md#app-protection-experience-for-android-devices).

#### Max Company Portal version age for Android devices<!-- 5151625  -->
You can set an age limit as the maximum number of days for the Company Portal (CP) version for Android devices. This setting ensures that end users are within a certain range of CP releases (in days). When the setting for the devices is not met, the selected action for this setting is triggered. Actions include **Block access**, **Wipe data**, or **Warn**. You can find this setting in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **App protection policies** > **Create policy**. The **Max Company Portal version age (days)** setting will be available in the **Device conditions** section of the **Conditional launch** step. For more information, see [Android app protection policy settings - Conditional launch](../apps/app-protection-policy-settings-android.md#conditional-launch).

#### Mac LOB apps will be supported as managed apps on macOS 11 and higher<!-- 7750527  -->
Intune supports the **Install as managed** app property that can be configured for Mac line-of-business (LOB) apps deployed to macOS 11 and higher. When this setting is on, the Mac LOB app will be installed as a managed app on supported devices (macOS 11 and higher). Managed line-of-business apps can be removed using the **uninstall** assignment type on supported devices (macOS 11 and higher). In addition, removing the MDM profile removes all managed apps from the device. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **macOS** > **Add**. For more information about adding apps, see [Add apps to Microsoft Intune](../apps/apps-add.md).

#### Enable Outlook S/MIME emails to be always signed or encrypted<!-- 8375748  -->
You can enable Outlook S/MIME emails to be always signed or encrypted when you create an Outlook email profile under app configuration for iOS/iPadOS and Android Enterprise devices.  The setting is available when you choose **Managed devices** when creating an Outlook app configuration policy. You can find this setting in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **App configuration policies** > **Add** > **Managed devices**. For related information, see [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md). 

#### Win32 app support for Workplace join (WPJ) devices <!-- 1862833  -->
Existing Win32 apps are supported for Workplace join (WPJ) devices. PowerShell scripts, which were not previously supported on WPJ devices, can now be deployed to WPJ devices. Specifically, device context PowerShell scripts work on WPJ devices, but user context PowerShell scripts are ignored by design. User context scripts will be ignored on WPJ devices and will not be reported to the Microsoft Endpoint Manager console. For more information about PowerShell, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Device Firmware Configuration Interface (DFCI) is generally available<!-- 5858274 -->

DFCI is an open-source Unified Extensible Firmware Interface (UEFI) framework. It allows you to securely manage the UEFI (BIOS) settings of your Windows Autopilot devices using Microsoft Endpoint Manager. It also limits end-user control over firmware configurations.
 
Unlike traditional UEFI management, DFCI removes the need for managing third-party solutions. It also provides zero-touch firmware management by using Microsoft Endpoint Manager for cloud management. DFCI also accesses the existing Windows Autopilot device information for authorization. 

For more information on this feature, see [Use DFCI profiles on Windows devices in Intune](../configuration/device-firmware-configuration-interface-windows.md). 

> [!IMPORTANT]
> DFCI policy reporting in the Endpoint Manager admin center wasn't working as expected. All policies reported a "Pending" status. This behavior is fixed.

#### Use the Connect Automatically setting on Android Enterprise basic Wi-Fi profiles<!-- 6329130   -->
On Android Enterprise devices, you can create basic Wi-Fi profiles that include common Wi-Fi settings, such as the connection name. You can configure the **Connect automatically** setting that automatically connects to your Wi-Fi network when devices are in range.

To see these settings, go to [Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices](../configuration/wi-fi-settings-android-enterprise.md).

Applies to:
- Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile

#### New user experience and new Enable direct download setting on macOS devices using associated domains<!-- 7739958   -->
When you create an Associated Domain configuration profile on macOS devices, the user experience is updated (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device features** for profile > **Associated domains**). You still enter your App ID and Domains. 

On macOS 11+ supervised devices enrolled with user approved device enrollment or automated device enrollment, you can use the **Enable direct download** setting. Enabling direct downloads allows domain data to downloaded directly from the devices, instead of downloading through a content delivery network (CDN).

For more information, see [Associated domains on macOS devices](../configuration/macos-device-features-settings.md#associated-domains).

Applies to:
- macOS 11+ (supervised)


#### New lockout password settings on macOS devices<!-- 7780272   -->
New settings are available when you create a macOS password profile (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device restrictions** for profile > **Password**):

- **Maximum allowed sign-in attempts**: The maximum number of times users can try to consecutively sign in before the device locks them out, is from 2-11. Set this value to a higher number. Setting this value to 2 or 3 isn't recommended, as mistakes are common.

  Applies to all enrollment types.

- **Lockout duration**: Choose how long the lockout lasts, in minutes. During a device lockout, the sign-in screen is inactive, and users can't sign in. When the lockout duration ends, user can sign in again. To use this setting, configure the **Maximum allowed sign-in attempts** setting.

  Applies to macOS 10.10 and newer, and all enrollment types.

To see these settings, go to [macOS password device restrictions](../configuration/device-restrictions-macos.md#password).

Applies to:
- macOS

#### Required password type default setting is changing on Android Enterprise devices<!-- 8092655   -->
On Android Enterprise devices, you can create a device password profile that sets the **Required password type** (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Device restrictions** > **Device password**).

The **Required password type** setting default is changing from **Numeric** to **Device default**.

Existing profiles aren't impacted. New profiles will automatically use **Device default**. 

Most devices don't require a password when **Device default** is selected. If you want to require your users to set up a passcode on their devices, configure the **Required password type** setting to something more secure than **Device default**.

To see the settings you can restrict, go to [Android Enterprise device settings to allow or restrict features](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android Enterprise


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Intune support for provisioning Azure Active Directory shared devices<!--6327412 -->
With Intune, you can now provision Android Enterprise dedicated devices with Microsoft Authenticator automatically configured into Azure AD shared device mode. For more information on how to use this enrollment type, see [Set up Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Update for Microsoft Tunnel<!-- 8629678  -->

We’ve released a [new version](../protect/microsoft-tunnel-configure.md#microsoft-tunnel-updates) of the Microsoft Tunnel Gateway, which includes the following changes:

- Fixes for logging. [View the Microsoft Tunnel system logs](../protect/microsoft-tunnel-monitor.md#view-microsoft-tunnel-logs) when you run the *journalctl -t mstunnel_monitor* command line on the tunnel server.
- Additional bug fixes.

The Tunnel Gateway server will automatically update to the new release.

#### App protection policy support on Android and iOS/iPadOS for additional partners<!-- 4452423, 4731168   -->
In October of 2019, Intune app protection policy added the capability to use data from our Microsoft Threat Defense partners.

With this update, we're expanding this support to the following two partners for using an app protection policy to block or selectively wipe a user’s corporate data based on the health of the device:

- **Check Point Sandblast** on Android, iOS and iPadOS
- **Symantec Endpoint Security** on Android, iOS and iPadOS

For more information, see [Create Mobile Threat Defense app protection policy with Intune](../protect/mtd-app-protection-policy.md).

#### Endpoint Manager Security tasks include details about misconfigured settings from Microsoft Defender for Endpoint TVM <!-- 5568193   -->
Microsoft Endpoint Manager Security tasks now report on and provide remediation details for misconfigurations discovered by Threat Vulnerability Management (TVM). The misconfigurations that are reported to Intune are limited to issues for which remediation guidance can be provided.
 
TVM is part of Microsoft Defender for Endpoint. Prior to this update, details from TVM only included details and remediation steps for Applications.
 
When you view Security tasks, you’ll find a new column named *Remediation Type* that identifies the type of issue:
- Application – Vulnerable applications and remediation steps. This has been available in Security tasks prior to this update.
- Configuration – A new category of details from TVM that identify misconfiguration and provides steps to help you remediate them.  
 
For more information on security tasks, see [Use Intune to remediate vulnerabilities identified by Microsoft Defender for Endpoint](../protect/atp-manage-vulnerabilities.md).

#### Endpoint security Firewall policies for tenant attached devices <!--  7323417   -->
As a public preview, you can deploy endpoint security [policy for Firewalls](../protect/endpoint-security-firewall-policy.md) to devices you manage with Configuration Manager. This scenario requires you to configure a tenant attach between a supported version of Configuration Manager and your Intune subscription. 

Firewall policy for tenant attached devices is supported for devices that run *Windows 10 and later*, and requires your environment to run *Configuration Manager current branch 2006* with the in-console hotfix *KB4578605*.

For more information, see the [requirements for Intune endpoint security policies](../protect/tenant-attach-intune.md#configuration-manager-version-requirements-for-intune-endpoint-security-policies) to support Tenant Attach.

#### Expanded settings to manage hardware device installation through block and allow lists<!-- 7339038      -->
In **Device control** profiles, which are part of endpoint security [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md), we’ve revised and [expanded our settings for managing hardware device installation](../protect/endpoint-security-asr-profile-settings.md#device-control). You’ll now find settings to define *block* lists and separate *allow* lists using *device IDs*, *setup classes*, and *instance identifiers*.  The following six settings are now available:

- Allow hardware device installation by device identifiers 
- Block hardware device installation by device identifiers 
- Allow hardware device installation by setup class 
- Block hardware device installation by setup class 
- Allow hardware device installation by device instance identifiers 
- Block hardware device installation by device instance identifiers 
 
Each of these settings supports the options of *Yes*, *No*, and *Not configured*.
When you configure *Yes* you can then define the block or allow list for that setting.
On a device, hardware that is specified in an allow list can install or update. However, if that same hardware is specified on a block list, the block overrides the allow list and installation or update of the hardware is prevented.

#### Improvements to endpoint security Firewall rules<!-- 7732448    -->
We've made several changes to improve the experience of configuring firewall rules in the [Microsoft Defender Firewall rules profile](../protect/endpoint-security-firewall-profile-settings.md#microsoft-defender-firewall-rules) for endpoint security Firewall policy.  
 
Improvements include:
- Improved layout in the UI, including section headers to organize the view.
- Increasing the character limit for the description field. 
- Validation of IP address entries.
- Sorting of IP address lists.
- Option to *select all* addresses when you clear entries from an IP address list.

#### Use Microsoft Defender for Endpoint in compliance policies for iOS<!-- 7895451  -->
As a public preview, you can now use Intune device compliance policy to [onboard iOS devices to Microsoft Defender for Endpoint](../protect/advanced-threat-protection-configure.md#onboard-devices).
 
After you onboard your enrolled iOS/iPadOS devices, your compliance policies for iOS can use the *threat level* signals from Microsoft Defender. These are the same signals that you can use for Android and Windows 10 devices.
             
The Defender for iOS app should move from public preview to generally availability by the end of the year.

####  Security Experience profiles for Endpoint Security Antivirus policy now have tri-state options<!-- 8082161   -->
We’ve added a third state of configuration for settings in the *Windows Security experience* profile for Endpoint security Antivirus policies.  This update applies to the [Windows Security experience](../protect/antivirus-security-experience-windows-settings.md) for Windows 10 and later).  
 
For example, where a setting previously offered **Not configured** and **Yes**, if supported by the platform, you now have the additional option of **No**.

#### Updated version of the Edge security baseline<!-- 8230830     -->
We’ve added a new [security baseline for Edge](../protect/security-baseline-settings-edge.md) to Intune: September 2020 (Edge version 85 and later).  
 
Updated baseline versions bring support for recent settings to help you maintain the best-practice configurations recommended by the respective product teams.
 
To understand what's changed between versions, see [Compare baseline versions](../protect/security-baselines.md#compare-baseline-versions) to learn how to export a .CSV file that shows the changes.  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### New Windows 10 feature update failures report<!-- 6473121  -->
The **Feature update failures** operational report provides failure details for devices that are targeted with a **Windows 10 feature updates** policy and have attempted an update. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Monitor** > **Feature update failures** to view this report. For more information, see [Feature update failures report](../protect/windows-update-compliance-reports.md#use-the-feature-update-failures-operational-report).

#### Updates to Antivirus reports<!-- 8456632  -->
Both the **Antivirus agent status report** and the **Detected malware report** have been updated. These reports now show data visualizations and provide additional columns of information (**SignatureUpdateOverdue**, **MalwareID**, **displayName**, and **InitialDetectionDateTime**). In addition, remote actions are included in the Antivirus agent status report. For more information, see the [Antivirus agent status report](../fundamentals/reports.md#antivirus-agent-status-report-organizational) and the [Detected malware report](../fundamentals/reports.md#detected-malware-report-organizational).

#### Updated Help and Support for Microsoft Endpoint Manager  <!-- 7328994  -->
The Help and Support experience uses machine learning to display solutions, diagnostics, and insights that will help you resolve your issues. We've updated the help and support page in Microsoft Endpoint Manager admin center with a new, easier to navigate, consistent UX experience. The new UX has now been rolled out in all blades in the console and will help us get you more relevant help. 

You'll now find an [updated and consolidated support experience](../../get-support.md) for the following cloud-based offerings from within the admin center:

- **Intune**
- **Configuration Manager**
- **Co-management**
- **Microsoft Managed Desktop**


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Scripts

#### View PowerShell scripts in the Intune Troubleshooting pane<!-- 7100075  -->
You can now view your assigned PowerShell scripts in the Troubleshooting pane. PowerShell scripts provide Windows 10 client communication with Intune to run enterprise management tasks, such as advanced device configuration and troubleshooting. For more information, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md).

#### Collect custom device or user properties using shell scripts on managed Macs<!-- 8099433  -->
You can create a custom attribute profile which enables you to collect custom properties from a managed macOS device using shell scripts. You can find this feature in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **macOS** > **Custom attributes**.  For related information, see [Use shell scripts on macOS devices in Intune](../apps/macos-shell-scripts.md).


<!-- ########################## -->
## Week of October 19, 2020

### Device configuration

#### Changes for Password settings in Device restriction profiles for Android device administrator<!-- 7662279  -->

Recently we added *Password complexity* as a new setting for [Device compliance](../protect/compliance-policy-create-android.md#password) policy and [Device restriction](../configuration/device-restrictions-android.md#password)
for *Android device administrator*. We've now added additional changes to the UI for settings in both policy types to help Intune accommodate the password changes in Android version 10 and later. These changes help ensure settings for passwords continue to apply to devices as expected.
  
You'll find the following changes to the Intune UI for passwords settings for the two policy types, which won't affect existing profiles:

- Settings are reorganized into sections that are based on which device versions the setting applies to, like Android 9 and earlier, or Android 10 and later. 
- Updates to labels and example text in the UI.
- Clarifications for references to PINs as *numerical* or *alphabetical*, or *alphanumeric*.

Applies to:  
- Android device administrator

<!-- ########################## -->
## Week of October 12, 2020

### Device configuration

#### Configure the macOS Microsoft Enterprise SSO plug-in<!-- 5627576 8278906-->

> [!IMPORTANT]
> On macOS, the Microsoft Azure AD SSO extension is listed in the Intune user interface, but wasn't working as expected. This feature is now working, and is available to use in public preview.

The Microsoft Azure AD team created a redirect single sign-on (SSO) app extension. This app extension allows macOS 10.15+ users to access Microsoft apps, organization apps, and websites that support Apple's SSO feature. It authenticates using Azure AD, with one sign-on.

With the Microsoft Enterprise SSO plug-in release, you can configure the SSO extension with the new Microsoft Azure AD app extension type in Intune (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device features** for profile >  **Single sign-on app extension** > SSO app extension type > **Microsoft Azure AD**).

To get SSO with the Microsoft Azure AD SSO app extension type, users need to install and sign in to the Company Portal app on their macOS devices.

For more information about macOS SSO app extensions, see [Single sign-on app extension](../configuration/device-features-configure.md#single-sign-on-app-extension).

Applies to:
- macOS 10.15 and newer

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### New Microsoft Tunnel version<!-- 8504252 -->

We’ve released a [new version](../protect/microsoft-tunnel-configure.md#microsoft-tunnel-updates) of the Microsoft Tunnel Gateway. The following changes are included in the new version:

- Microsoft Tunnel now logs operational and monitoring details to Linux server logs in the *syslog* format. You can [View the Microsoft Tunnel system logs](../protect/microsoft-tunnel-monitor.md#view-microsoft-tunnel-logs) when you run the `journalctl -t` command line on the tunnel server.
- Various bug fixes.

<!-- ########################## -->
## Week of October 5, 2020
 
<!-- vvvvvvvvvvvvvvvvvvvvvv -->  
### Device configuration

#### New version of the PFX Certificate Connector<!-- 8476079 -->

We’ve released a new version of the PFX Certificate Connector, version **6.2008.60.612**. This new connector version:

- Fixes an issue with PKCS certificate delivery to Android Enterprise Fully Managed devices. The issue required the cryptography Key Storage Provider (KSP) be a legacy provider. You can now use a Cryptographic Next Generation (CNG) Key Storage Provider as well.
- Changes to *CA Account* tab of the PFX Certificate Connector: The Username and password (credentials) that you specify are now used to issue certificates and to revoke certificates. Previously these credentials were used only for certificate revocation.

For more information about certificate connectors, including a list of connector releases for both certificate connectors, see [Certificate connectors](../protect/certificate-connectors.md).

<!-- ########################## -->
## Week of September 28, 2020  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->  

### App management  
#### Improved work profile messaging in Company Portal for Android  
The Company Portal screen previously titled "You're Halfway There!" has been updated to better explain how work profile management works. Users will see this screen if they re-enable Company Portal in the personal profile after they've already gone through work profile enrollment. They may also see this screen during work profile enrollment on some Android OS versions, as shown in the help doc, [Enroll with Android work profile](../user-help/enroll-device-android-work-profile.md).  

### Device management
<!-- ########################## -->

#### Tamper Protection policy for Tenant Attached devices in preview<!-- 7303958  -->

In preview, we’ve added a new profile to Intune endpoint security Antivirus policy that you can use to [manage Tamper Protection on tenant attached devices](../protect/endpoint-security-antivirus-policy.md#devices-managed-by-configuration-manager): **Windows Security experience (preview)**.

The new profile is found under the *Windows 10 and Windows Server (ConfigMgr)* platform when you create a new Antivirus policy.

Before you can use Intune endpoint security policies with tenant attached devices, you need to configure Configuration Manager [tenant attach](../protect/tenant-attach-intune.md), and synchronize devices with Intune.

Also be aware of the specific [prerequisites](../protect/endpoint-security-antivirus-policy.md#prerequisites-for-tamper-protection) that are required to use and support tamper protection with Intune policy.


## Week of September 21, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Tenant attach: Run scripts from the admin center
<!--7220536, CM6234688-->
Bring the power of the Configuration Manager on-premises [Run scripts](../../configmgr/apps/deploy-use/create-deploy-scripts.md) feature to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to run PowerShell scripts from the cloud against an individual Configuration Manager managed device in real time. This feature gives all the traditional benefits of PowerShell scripts that have already been defined and approved by the Configuration Manager admin to this new environment. For more information, see [Tenant attach: Run Scripts from the admin center](../../configmgr/tenant-attach/scripts.md).

### App management

#### Unified delivery of Azure AD Enterprise and Office Online applications in the Windows Company Portal<!-- 1817861 -->
In the 2006 release, we announced [Unified delivery of Azure AD Enterprise and Office Online applications in the Company Portal website](../fundamentals/whats-new.md#unified-delivery-of-azure-active-directory-enterprise-and-office-online-applications-in-the-windows-company-portal). This feature is supported in the Windows Company Portal. On the **Customization** pane of Intune, select to **Hide** or **Show** both **Azure AD Enterprise applications** and **Office Online applications** in the Windows Company Portal. Each end user will see their entire application catalog from the chosen Microsoft service. By default, each additional app source will be set to **Hide**. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Customization** to find this configuration setting. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

#### Windows Company Portal app descriptions with rich text<!-- 5146060 -->
Using markdown, you can now display app descriptions using rich text in the Windows Company Portal. For more information about the Company Portal, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

#### App protection policies allow administrators to configure incoming Org data locations<!-- 4176693 -->
You can now control which trusted data sources are allowed to open into organization documents. Similar to the existing **Save copies of org data** app protection policy option, you can define which incoming data locations are trusted. This functionality relates to the following app protection policy settings:
- **Save copies of org data**
- **Open data into org documents**
- **Allow users to open data from selected services**

In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App protection policies** > **Create policy**. To use this functionality, Intune policy-managed applications must implement support for this control. For more information, see [iOS app protection policy settings](../apps/app-protection-policy-settings-ios.md) and [Android app protection policy settings](../apps/app-protection-policy-settings-android.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### COPE preview update: New settings to create requirements for the work profile password for Android Enterprise corporate-owned devices with a work profile<!--7088355  -->
New settings now give admins the ability to set requirements for the work profile password for Android Enterprise corporate-owned devices with a work profile:

- Required password type
- Minimum password length
- Number of days until password expires
- Number of passwords required before user can reuse a password
- Number of sign-in failures before wiping device

For more information, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

#### COPE preview update: New settings to configure the personal profile for Android Enterprise corporate-owned devices with a work profile<!-- 7086356   -->
For Android Enterprise corporate-owned devices with a work profile, there are new settings you can configure that only apply to the personal profile (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work profile** > **Device restrictions** for profile > **Personal profile**):

- **Camera**: Use this setting to block access to the camera during personal usage.
- **Screen capture**: Use this setting to block screen captures during personal usage.
- **Allow users to enable app installation from unknown sources in the personal profile**: Use this setting to allow users to install apps from unknown sources in the personal profile. 

Applies to:
- Android Enterprise corporate-owned devices with a work profile, personally enabled devices.

To see all the settings you can configure, go to [Android Enterprise device settings to allow or restrict features](../configuration/device-restrictions-android-for-work.md).

#### Analyze your on-premises GPOs using Group Policy analytics<!--7200950   -->
In **Devices** > **Group Policy analytics (preview)**, you can import your group policy objects (GPOs) in the Endpoint Manager admin center. When you import, Intune automatically analyzes the GPO, and shows the policies that have equivalent settings in Intune. It also shows GPOs that are deprecated, or aren't supported anymore. For deeper information, go to **Reports** >  **Group policy analytics (preview)** > Migration readiness report.

For more information on this feature, see [Group Policy analytics](../configuration/group-policy-analytics.md).

Applies to:
- Windows 10 and newer

#### Block App Clips on iOS/iPadOS, and Defer non-OS software updates on macOS devices<!-- 7518422   -->
When you create a Device Restrictions profile on iOS/iPadOS and macOS devices, there are some new settings:

**iOS/iPadOS 14.0+ Block App Clips**

- Applies to iOS/iPadOS 14.0 and newer.
- Devices must be enrolled with device enrollment or automated device enrollment (supervised devices).
- The **Block App Clips** setting blocks App Clips on managed devices (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile > **General**). When blocked, users can't add any App Clips, and existing App Clips are removed.

**macOS 11+ Defer software updates**

- Applies to macOS 11 and newer. On supervised macOS devices, the device must have user approved device enrollment, or enrolled through automated device enrollment.
- The existing **Defer software updates** setting can now delay OS and non-OS updates (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device restrictions** for profile > **General**). The existing **Delay visibility of software updates** setting applies to OS and non-OS updates. Deferring non-OS software updates doesn't impact scheduled updates.
- The behavior of existing policies isn't changed, affected, or deleted. Existing policies will automatically migrate to the new setting with your same configuration.

To see the device restrictions settings you can configure, see [iOS/iPadOS](../configuration/device-restrictions-ios.md) and [macOS](../configuration/device-restrictions-macos.md).

#### New settings using per-app VPN or on-demand VPN on iOS/iPadOS and macOS devices<!-- 7758772 7758837 7758886   -->
You can configure automatic VPN profiles in **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **VPN** for profile > **Automatic VPN**. There are new per-app VPN settings you can configure:

- **Prevent users from disabling automatic VPN**: When creating an automatic **Per-app VPN** or **On-demand VPN** connection, you can force users to keep the automatic VPN enabled and running.
- **Associated domains**: When creating an automatic **Per-app VPN** connection, you can add associated domains in the VPN profile that automatically start the VPN connection. For more information on associated domains, see [Associated domains](../configuration/device-features-configure.md#associated-domains).
- **Excluded domains**: When creating an automatic **Per-app VPN** connection, you can add domains that can bypass the VPN connection when per-app VPN is connected.

To see these settings, and other settings you can configure, go to [iOS/iPadOS VPN settings](../configuration/vpn-settings-ios.md) and [macOS VPN settings](../configuration/vpn-settings-macos.md).

Set up [per-app Virtual Private Network (VPN) for iOS/iPadOS devices](../configuration/vpn-setting-configure-per-app.md#create-a-per-app-vpn-profile).

Applies to:
- iOS/iPadOS 14 and newer
- macOS Big Sur (macOS 11)

#### Set maximum transmission unit for IKEv2 VPN connections on iOS/iPadOS devices<!-- 7758937  -->
Starting with iOS/iPadOS 14 and newer devices, you can configure a custom maximum transmission unit (MTU) when using IKEv2 VPN connections (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **VPN** for profile > **IKEv2** for connection type).

For more information on this setting, and the others you can configure, see [IKEv2 settings](../configuration/vpn-settings-ios.md#ikev2-settings).

Applies to:
- iOS/iPadOS 14 and newer

#### Per-account VPN connection for email profiles on iOS/iPadOS devices<!-- 7759116   -->
Starting with iOS/iPadOS 14, email traffic for the native Mail app can be routed through a VPN based on the account the user is using. In Intune, you can configure the **VPN profile for per account VPN** setting (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Email** for profile > **Exchange ActiveSync email settings**). 

This feature lets you select a per-app VPN profile to use for an account-based VPN connection. The per-app VPN connection automatically turns on when users use their organization account in the Mail app.

To see this setting and the others you can configure, go to [Add e-mail settings for iOS and iPadOS devices](../configuration/email-settings-ios.md).

Applies to:
- iOS/iPadOS 14 and newer

#### Disable MAC address randomization on Wi-Fi networks on iOS/iPadOS devices<!-- 7758689   -->
Starting with iOS/iPadOS 14, by default, devices present a randomized MAC address instead of the physical MAC address when connecting to a network. This behavior is recommended for privacy, as it's harder to track a device by its MAC address. This feature also breaks functionality that relies on a static MAC address, including network access control (NAC).

You can disable MAC address randomization on a per-network basis in Wi-Fi profiles (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Wi-Fi** for profile > **Basic** or **Enterprise** for Wi-Fi type).

To see this setting, and the others you can configure, go to [Add Wi-Fi settings for iOS and iPadOS devices](../configuration/wi-fi-settings-ios.md).

Applies to:
- iOS/iPadOS 14 and newer

#### New settings for Device control profiles <!-- 8368028 -->
We’ve added a pair of settings to the [*Device control* profile](../protect/endpoint-security-asr-profile-settings.md#device-control-profile) for the *Attack surface reduction* policy for devices that run Windows 10 or later:

- **Removable storage**
- **USB connections (HoloLens only)**
 
*Attack surface reduction* policy is part of [Endpoint security](../protect/endpoint-security-policy.md) in Intune.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Enrollment Status Page shows critical kiosk policies<!--7021540 -->
You'll now be able to see the following policies tracked on the Enrollment Status Page
- Assigned access
- Kiosk browser settings
- Edge browser settings

All other kiosk policies aren't currently tracked.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Support for PowerPrecision and PowerPrecision+ Batteries for Zebra devices<!--3724987  -->
On a device's hardware details page, you can now see the following information about Zebra devices using PowerPrecision and PowerPrecision+ batteries:
- State-of-Health rating as determined by Zebra (PowerPrecision+ batteries only)
- Number of full charge cycles consumed
- Date of last check-in for battery last found in the device
- Serial number of the battery pack last found in the device

#### COPE preview update: Reset work profile password for Android Enterprise corporate-owned devices with a work profile <!--7217228  -->
You can now reset the work profile password on Android Enterprise corporate-owned devices with a work profile. For more information, see [Reset a passcode](../remote-actions/device-passcode-reset.md#reset-a-passcode).

#### Rename a co-managed device that is Azure Active Directory joined<!--7728043  -->
You can now rename a co-managed device that is Azure AD joined. For more information, see [Rename a device in Intune](../remote-actions/device-rename.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Microsoft Tunnel Gateway VPN solution in preview<!-- 7843124  -->
You can now deploy [Microsoft Tunnel Gateway](../protect/microsoft-tunnel-overview.md) to provide remote access to on-premises resources on iOS and Android Enterprise (Fully managed, Corporate-Owned Work Profile, Work profile) devices.

Microsoft Tunnel supports per-app and full device VPN, split tunneling, and conditional access capabilities using modern authentication.  Tunnel can support multiple gateway servers for high availability for production readiness.

#### Additional biometric authentication support for Android devices<!-- 5706213  -->
New Android devices are making use of a more diverse set of biometrics beyond fingerprints. When OEMs implement support for non-fingerprint biometrics, end users have the potential to use this capability for secure access and a better experience. With the 2009 release of Intune, you can allow your end users to use fingerprint or Face Unlock, depending on what the Android device supports. You can configure whether all biometric types beyond fingerprint can be used to authenticate. For more information, see [App protection experience for Android devices](../apps/app-protection-policy.md#app-protection-experience-for-android-devices).

#### New details in the Endpoint security configuration for a device<!-- 7745029     -->
You can now view additional details for devices as part of a devices *Endpoint security configuration*. When you drill-in to view status details about policies you've deployed to devices, you’ll now find the following setting:
 
- **UPN** (User Principle Name): The UPN identifies which endpoint security profile is assigned to a given user on the device. This information is useful to help differentiate between multiple users on a device and multiple entries of a profile or baseline that’s assigned to the device. 

For more information, see [Resolve conflicts for security baselines](../protect/security-baselines-monitor.md#resolve-conflicts-for-security-baselines).

#### Expanded RBAC permissions for the Endpoint Security role<!--7312374    -->
The **Endpoint Security Manager** role for Intune has additional [role-based access control (RBAC) permissions for **remote tasks**](../protect/endpoint-security.md#permissions-granted-by-the-endpoint-security-manager-role).
 
This role grants access to the Microsoft Endpoint Manager admin center and can be used by individuals who manage security and compliance features, including security baselines, device compliance, conditional access, and Microsoft Defender for Endpoint.
 
New permissions for *remote tasks* include:
 
- Reboot now
- Remote lock
- Rotate BitLockerKeys (Preview)
- Rotate FileVault key
- Sync devices
- Microsoft Defender
- Initiate Configuration Manger action
 
To view the full set of permission for any Intune RBAC role, go to (**Tenant admin** > **Intune roles** > *select a role* > **Permissions**).

#### Updates for Security Baselines<!-- 7102146, 7103916     -->
We have new versions available for the following [security baselines](../protect/security-baselines.md):  
 
- **[MDM Security baseline (Windows 10 Security)](../protect/security-baseline-settings-mdm-all.md?pivots-mdm-sept-2020)**
- **[Microsoft Defender for Endpoint baseline](../protect/security-baseline-settings-defender-atp.md?pivots=atp-sept-2020)**
 
Updated baseline versions bring support for recent settings to help you maintain the best-practice configurations recommended by the respective product teams.

To understand what's changed between versions, see [Compare baseline versions](../protect/security-baselines.md#compare-baseline-versions) to learn how to export a .CSV file that shows the changes.  

#### Use Endpoint security configuration details to identify the source of policy conflicts for devices<!-- 7567503    -->
To aid in conflict resolution, you can now drill-in through a security baseline profile to view the *Endpoint security configuration* for a selected device. From there, you can select settings that show a *Conflict* or *Error* and continue to drill-in further to view a list of details that includes the profiles and policies that are part of the conflict.
 
If you then select a policy that is a source of a conflict, Intune opens that policies Overview pane where you can review or modify the policies configuration.
 
The following policy types can be identified as a source of conflict when you drill in through a security baseline:

- Device configuration policy
- Endpoint security policies
 
For more information, see [Resolve conflicts for security baselines](../protect/security-baselines-monitor.md#resolve-conflicts-for-security-baselines).

#### Support for certificates with a key size of 4096 on iOS and macOS devices<!-- 7659175   -->
When you configure a *SCEP certificate* profile for iOS/iPadOS or macOS devices, you can now specify a **Key size (bits)** of **4096** bits. 
 
Intune supports 4096-bit keys for the following platforms: 
- iOS 14 and later
- macOS 11 and later  
 
To configure SCEP certificate profiles, see [Create a SCEP certificate profile](../protect/certificates-profile-scep.md#create-a-scep-certificate-profile).

#### Android 11 deprecates deployment of trusted root certificates to device administrator enrolled devices<!--7662775  -->
Beginning with Android 11, trusted root certificates can no longer install the trusted root certificate on devices that enroll as *Android device administrator*. This limitation doesn’t affect Samsung Knox devices. For non-Samsung devices, users must manually install the trusted root certificate on the device. 
 
After the trusted root certificate is manually installed on a device, you can use SCEP to provision certificates to the device. You must still create and deploy a *trusted certificate* policy to the device, and link that policy to the *SCEP certificate* profile.

- If the trusted root certificate is on the device, the SCEP certificate profile can install successfully. 
- If the trusted certificate can't be found on the device, the SCEP certificate profile will fail.

For more information, see [Trusted certificate profiles for Android device administrator](../protect/certificates-trusted-root.md#trusted-certificate-profiles-for-android-device-administrator).


#### Tri-state options for more settings in Endpoint Security Firewall policy<!-- 6586159  -->
We've added a third state of configuration to a few more settings in [Endpoint security Firewall policies for Windows 10](../protect/endpoint-security-firewall-profile-settings.md).

The following settings are updated:
- **Stateful File Transfer Protocol (FTP)** now supports *Not configured*, *Allow*, and *Disabled*.
- **Require keying modules to only ignore the authentication suites they don’t support** now supports *Not configured*, *Enabled*, and *Disabled*.

#### Improved certificate deployment for Android Enterprise <!-- 6296499     -->
We’ve improved our support for using [S/MIME certificates for Outlook](../protect/certificates-s-mime-encryption-sign.md) for encryption and signing on Android Enterprise devices that enroll as Fully Managed, Dedicated, and Corporate-Owned Work Profiles. Previously, use of S/MIME required the device user to allow access. Now, the S/MIME certificates can be used without user interaction.   

To deploy S/MIME certificates to supported Android devices, use a [PKCS imported certificate profile](../protect/certificates-imported-pfx-configure.md) or [SCEP certificate profile](../protect/certificates-profile-scep.md) for Device configuration. Create a profile for **Android Enterprise** and then select **PKCS imported certificate** from the category for *Fully Managed, Dedicated, and Corporate-Owned Work Profile*.

#### Improved status details in security baseline reports<!-- 7221051 -->
We’ve begun improving many of the [status details for Security baseline](../protect/security-baselines-monitor.md). You’ll now see more meaningful and detailed status when viewing information about the baseline Versions you’ve deployed.

Specifically, when you select a baseline, select *Version*, and the select an instance of that baseline, the initial Overview displays the following information:
 
- **Security baseline posture** chart - This chart now displays the following status details:
  - **Matches default baseline** – This status replaces *Matches baseline* and identifies when a devices configuration matches the default (unmodified) baseline configuration.
  - **Matches custom settings** – This status identifies when a devices configuration matches the baseline that you’ve configured (customized) and deployed.
  - **Misconfigured** – This status is a rollup that represents three status conditions from a device: *Error*, *Pending*, or *Conflict*. These separate states are available from other views, as detailed below.
  - **Not applicable** - This status represents a device that can’t receive the policy. For example, the policy updates a setting specific to the latest version of Windows, but the device runs an older (earlier) version that doesn’t support that setting. 
- **Security baseline posture by category** - This is a list view that displays device status by category. The available columns mirror much of the *Security baseline posture* chart, but in place of *Misconfigured* you’ll see three columns for the status that make up Misconfigured:
  - **Error**: The policy failed to apply. The message typically displays with an error code that links to an explanation.
  - **Conflict**: Two settings are applied to the same device, and Intune can't sort out the conflict. An administrator should review.
  - **Pending**: The device hasn't checked in with Intune to receive the policy yet.

#### New setting for Password complexity for Android 10 and later for device administrator enrolled devices<!-- 7992114 -->

To support new options for Android 10 and later on devices enrolled as Android device administrator, we’ve added a new setting called **Password complexity** to both [*Device compliance*](../protect/compliance-policy-create-android.md#password) policy and [*Device restriction*](../configuration/device-restrictions-android.md#password) policy.  You use this new setting to manage a *measure* of the password strength that factors in the password type, length, and quality. 
 
Password Complexity doesn’t apply to Samsung Knox devices. On these devices, password length and type settings override Password complexity.

Password complexity supports the following options:

- **None** - No password
- **Low** - The password satisfies one of the following:
  - Pattern
  - PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences
- **Medium** - The password satisfies one of the following:
  - PIN with no repeating (4444) or ordered (1234, 4321, 2468) sequences, length at least 4
  - Alphabetic, length at least 4
  - Alphanumeric, length at least 4
- **High** - The Password satisfies one of the following:
  - PIN with no repeating (4444) or ordered (1234, 4321, 2468) sequences, length at least 8
  - Alphabetic, length at least 6
  - Alphanumeric, length at least 6

This new setting remains a work in progress. In late October 2020, Password complexity will take effect on devices.

If you set *Password complexity* to something other than *None*, you must also configure an additional setting to ensure that end users who use a password that doesn’t meet your complexity requirements will receive a warning to update their password.

- Device compliance: Set **Require a password to unlock mobile devices** to **Require**.
- Device restriction: Set **Password** to **Require**

If you don’t set the additional setting to Require, users with weak passwords won’t receive the warning.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Endpoint analytics is generally available
<!--8048029-->
Endpoint analytics aims to improve user productivity and reduce IT support costs by providing insights into the user experience. These insights enable IT to optimize the end-user experience with proactive support and to detect regressions to the user experience by assessing user impact of configuration changes. For more information, see [Endpoint analytics](../../analytics/overview.md).

#### Bulk actions for devices listed in operational report<!-- 8218481  -->
As part of the new antivirus reports coming out under Microsoft Endpoint Manager security, the **Windows 10 detected malware** operational report provides bulk actions that are applicable to the devices selected within the report. Actions include **Restart**, **Quick scan**, and **Full scan**. For more information, see [Windows 10 detected malware report](../fundamentals/reports.md#detected-malware-report-organizational).

#### Export Intune reports using Graph APIs<!-- 8270831  -->
All reports that have been migrated to the Intune reporting infrastructure will be available for export from a single top-level export API. For more information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

#### New and improved Microsoft Defender Antivirus reporting for Windows 10 and newer<!-- 6018169  -->
We're adding four new reports for Microsoft Defender Antivirus on Windows 10 in Microsoft Endpoint Manager. These reports include:
- Two operational reports, *Windows 10 unhealthy endpoints* and *Windows 10 detected malware*. In Microsoft Endpoint Manager, select **Endpoint security** > **Antivirus**.
- Two organizational reports, *Antivirus agent status* and *Detected malware*. In Microsoft Endpoint Manager, select **Reports** > **Microsoft Defender Antivirus**.

For more information, see [Intune reports](../fundamentals/reports.md) and [Manage endpoint security in Microsoft Intune](../protect/endpoint-security.md).

#### New Windows 10 feature update report<!-- 6473128  -->
The **Windows 10 feature update** report provides an overall view of compliance for devices that are targeted with a **Windows 10 feature updates** policy. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports** > **Windows updates** to view the summary for this report. To see reports for specific policies, from the **Windows updates** workload, select the **Reports** tab and open the **Windows Feature Update Report**. For more information, see [Windows 10 feature updates](../fundamentals/reports.md#windows-10-feature-updates-organizational).


<!-- ########################## -->
## Week of September 7, 2020
<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Tenant attach: Device timeline in the admin center<!--7220536, CM7141381-->
When Configuration Manager synchronizes a device to Microsoft Endpoint Manager through tenant attach, you'll be able to see a timeline of events. This timeline shows past activity on the device that can help you troubleshoot problems. For more information, see [Tenant attach: Device timeline in the admin center](../../configmgr/tenant-attach/timeline.md).

#### <a name="bkmk_hinv"></a> Tenant attach: Resource explorer in the admin center<!--IN7220536, CM6479284 -->
From the Microsoft Endpoint Management admin center, you can view hardware inventory for uploaded Configuration Manager devices by using resource explorer. For more information, see [Tenant attach: Resource explorer in the admin center](../../configmgr/tenant-attach/resource-explorer.md).

#### Tenant attach: CMPivot from the admin center<!--IN7220536, CM6024392-->
Bring the power of CMPivot to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to be able to initiate real-time queries from the cloud against an individual ConfigMgr managed device and return the results back to the admin center. This gives all the traditional benefits of CMPivot, which allows IT Admins and other designated personas the ability to quickly assess the state of devices in their environment and take action.

For more information about CMPivot from the admin center, see [CMPivot prerequisites](../../configmgr/tenant-attach/cmpivot-start.md), [CMPivot overview](../../configmgr/tenant-attach/cmpivot-overview-attached.md), and [CMPivot sample scripts](../../configmgr/tenant-attach/cmpivot-samples-attached.md).

## Week of August 31, 2020

### Device configuration

#### New version of the PFX Certificate Connector and changes for PKCS certificate profile support<!--  4839686  -->

We’ve released a new version of the PFX Certificate Connector, version **6.2008.60.607**. This new connector version:

- Supports PKCS certificate profiles on all supported platforms except Windows 8.1
 
  We’ve consolidated all of the PCKS support in the PFX Certificate Connector.  This means if you don’t use SCEP in your environment, and don’t use NDES for other intents, you can remove the Microsoft Certificate Connector and uninstall NDES from your environment. 
 
- Because the Microsoft Certificate Connector hasn’t had functionality removed, you can continue to use them to support PKCS certificate profiles.
- Supports certificate revocation for Outlook S/MIME
- Requires .NET Framework 4.7.2

For more information about certificate connectors, including a list of connector release for both certificate connectors, see [Certificate connectors](../protect/certificate-connectors.md)


<!-- ########################## -->
## Week of August 24, 2020 (2008 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Associated licenses revoked before deletion of Apple VPP token<!--6195322  -->
When you delete an Apple VPP token in Microsoft Endpoint Manager, all Intune-assigned licenses associated with that token are automatically revoked before the deletion.

#### Improvement to Update device settings page in Company Portal app for Android to shows descriptions <!-- 7414768  -->
In the Company Portal app on Android devices, the **Update device settings** page lists the settings that need updated to be compliant. Users expand the issue to see more information, and see the **Resolve** button.

This user experience is improved. The listed settings are expanded by default to show the description, and show the **Resolve** button, when applicable. Previously, the issues were collapsed by default. This new default behavior reduces the number of clicks, so users can resolve issues more quickly.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Use NetMotion as a VPN connection type for iOS/iPadOS and macOS devices<!-- 1333631   -->
When you create a VPN profile, NetMotion is available as a VPN connection type (**Devices** > **Device configuration** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **VPN** for profile > **NetMotion** for connection type).

For more information on VPN profiles in Intune, see [Create VPN profiles to connect to VPN servers](../configuration/vpn-settings-configure.md).

Applies to:
- iOS/iPadOS
- macOS

#### More Protected Extensible Authentication Protocol (PEAP) options for Windows 10 Wi-Fi profiles<!-- 3805024  -->
On Windows 10 devices, you can create Wi-Fi profiles using the Extensible Authentication Protocol (EAP) to authenticate Wi-Fi connections (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Wi-Fi** for profile > **Enterprise**).

When you select Protected EAP (PEAP), there are new settings available:
- **Perform server validation in PEAP phase 1**: In PEAP negotiation phase 1, the server is verified by the certificate validation.
  - **Disable user prompts for server validation in PEAP phase 1**: In PEAP negotiation phase 1, user prompts asking to authorize new PEAP servers for trusted certification authorities aren't shown.
- **Require cryptographic binding**: Prevents connections to PEAP servers that don't use cryptobinding during the PEAP negotiation.

To see the settings you can configure, go to [Add Wi-Fi settings for Windows 10 and later devices](../configuration/wi-fi-settings-windows.md).

Applies to: 
- Windows 10 and newer

#### Prevent users from unlocking Android Enterprise work profile devices using face and iris scanning<!--6069759 idmiss -->
You can now prevent users from using face or iris scanning to unlock their work profile-managed devices, either at the device level or the work profile level. This can be set in **Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Work profile > Device restrictions** for profile > **Work profile settings** and **Password** sections.

For more information, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md#personally-owned-devices-with-a-work-profile).

Applies to: 
- Android Enterprise work profile

#### Use SSO app extensions on more iOS/iPadOS apps with the Microsoft Enterprise SSO plug-in<!-- 7369991  -->
The [Microsoft Enterprise SSO plug-in for Apple devices](/azure/active-directory/develop/apple-sso-plugin) can be used with all apps that support SSO app extensions. In Intune, this feature means the plug-in works with mobile iOS/iPadOS apps that don't use the Microsoft Authentication Library (MSAL) for Apple devices. The apps don't need to use MSAL, but they do need to authenticate with Azure AD endpoints.

To configure your iOS/iPadOS apps to use SSO with the plug-in, add the app bundle identifiers in an iOS/iPadOS configuration profile (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **Single sign-on app extension** > **Microsoft Azure AD** for SSO app extension type > **App bundle IDs**).

To see the current SSO app extension settings you can configure, go to [Single sign-on app extension](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

Applies to:
- iOS/iPadOS

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Deploy endpoint security Antivirus policy to tenant attached devices (preview)<!-- 5475441  -->
As a preview, you can deploy endpoint security [policy for Antivirus](../protect/endpoint-security-antivirus-policy.md) to devices you manage with Configuration Manager. This scenario requires you to configure a tenant attach between a supported version of Configuration Manager and your Intune subscription. The following versions of Configuration Manager are supported:

- Configuration Manager current branch 2006

For more information, see the [requirements for Intune endpoint security policies](../protect/tenant-attach-intune.md#
requirements-for-intune-endpoint-security-policies) to support Tenant Attach.

#### Changes for Endpoint security Antivirus policy exclusions<!--5583940, 6018119    -->
We’ve introduced two changes for managing the Microsoft Defender Antivirus exclusion lists you configure as part of an [Endpoint Security Antivirus policy](../protect/endpoint-security-antivirus-policy.md). The changes help you to prevent conflicts between different policies and resolve exclusion list conflicts that might exist in your previously deployed policies.

Both of the changes apply to policy settings for the following [Microsoft Defender Antivirus Configuration Service Providers](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions) (CSPs):

- Defender/ExcludedPaths
- Defender/ExcludedExtensions
- Defender/ExcludedProcesses

The changes are:

- New profile type: **Microsoft Defender Antivirus exclusions** - Use this new profile type for Windows 10 and later to define a policy that is focused only on Antivirus exclusions. This profile helps simplify management of your exclusion lists by separating them from other policy configurations.

  The exclusions you can configure include Defender *processes*, *file extensions*, and *files* and *folders* that you don’t want Microsoft Defender to scan.

- **Policy merge** – Intune now merges the list of exclusions you’ve defined in separate profiles into a single list of exclusions to apply to each device or user. For example, if you target a user with three separate policies, the exclusion lists from those three policies merge into a single superset of *Microsoft Defender Antivirus exclusions*, that then apply to that user.

#### Import and export lists of address ranges for Windows firewall rules<!-- 8125400  -->

We've added support to **Import** or **Export** a list of address ranges using .csv files to the Microsoft Defender Firewall rules profile in the Firewall policy for Endpoint security. The following Windows firewall rule settings now support import and export:

- **Local address ranges**
- **Remote address ranges**

We've also improved validation of both local and remote address range entry to help prevent duplicate or invalid entries.

For more information about these settings, see the settings for [Microsoft Defender Firewall rules](../protect/endpoint-security-firewall-profile-settings.md#microsoft-defender-firewall-rules).





<!-- ########################## -->
## Week of August 17, 2020

### Intune apps

#### Custom brand image now displayed in the Windows Company Portal profile page<!-- 4280187 -->
As a Microsoft Intune administrator, you can upload a custom brand image to Intune which will be displayed as a background image on the user's profile page in the Windows Company Portal app. For more information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md#branding).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### The Company Portal adds Configuration Manager application support<!-- 4297660 -->
The Company Portal now supports Configuration Manager applications. This feature allows end users to see both Configuration Manager and Intune deployed applications in the Company Portal for co-managed customers. This new version of the Company Portal will display Configuration Manager deployed apps for all co-managed customers. This support will help administrators consolidate their different end-user portal experiences. For more information, see [Use the Company Portal app on co-managed devices](../../configmgr/comanage/company-portal.md). 

### Device security

#### Set device compliance state from third-party MDM providers<!-- 6361689 -->

Intune now supports [third-party MDM solutions as a source of device compliance details](../protect/device-compliance-partners.md). This third-party compliance data can be used to enforce Conditional Access policies for Microsoft 365 apps on iOS and Android through integration with Microsoft Intune.  Intune evaluates the compliance details from the third-party provider to determine if a device is trusted, and then sets the conditional access attributes in Azure AD.  You'll continue to create your Azure AD Conditional Access policies from within the Microsoft Endpoint Manager admin center or the Azure AD portal.

The following third-party MDM providers are supported with this release, as a public preview:

- VMware Workspace ONE UEM (previously known as AirWatch)

*This update is rolling out to customers globally. You should see this capability within the next week.*

<!-- ########################## -->
## Week of August 10, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Tenant attach: Install an application from the admin center <!-- IN7220536 CM6024389-->
You can now initiate an application install in real time for a tenant attached device from the Microsoft Endpoint Manager admin center. For more information, see [Tenant attach: Install an application from the admin center](../../configmgr/tenant-attach/applications.md).

<!-- ########################## -->
## Week of July 27, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Power BI compliance report template V2.0<!-- 636958 -->
Power BI template apps enable Power BI partners to build Power BI apps with little or no coding, and deploy them to any Power BI customer. Admins can update the version of the Power BI compliance report template from V1.0 to V2.0. V2.0 includes an improved design, as well as changes to the calculations and data that are surfaced as part of the template. For more information, see [Connect to the Data Warehouse with Power BI](../developer/reports-proc-get-a-link-powerbi.md) and [Update a template app](/power-bi/service-template-apps-install-distribute#update-a-template-app). Additionally, see the blog post [Announcing a New Version of the Power BI Compliance Report with Intune Data Warehouse](https://aka.ms/new_compliance_report).

<!-- ########################## -->
## Week of July 13, 2020  (2007 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Exchange On-Premises Connector support<!-- 7138486  -->
Intune is removing support for the Exchange On-Premises Connector feature from the Intune service beginning in the 2007 (July) release. Existing customers with an active connector will be able to continue with the current functionality at this time. New customers and existing customers that do not have an active connector will no longer be able to create new connectors or manage Exchange ActiveSync (EAS) devices from Intune. For those customers, Microsoft recommends the use of Exchange [hybrid modern authentication (HMA)](/office365/enterprise/hybrid-modern-auth-overview) to protect access to Exchange on-premises. HMA enables both Intune App Protection Policies (also known as MAM) and Conditional Access through Outlook Mobile for Exchange on-premises.

#### S/MIME for Outlook on iOS and Android devices without enrollment<!-- 6517155 -->
You can now enable S/MIME for Outlook on iOS and Android devices using an app configuration policy for managed apps. This allows for policy delivery regardless of device enrollment state. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App configuration policies** > **Add** > **Managed apps**. Additionally, you can choose whether or not to allow users to change this setting in Outlook. However, to automatically deploy S/MIME certificates to Outlook for iOS and Android, the device must be enrolled. For general information about S/MIME, see [S/MIME overview to sign and encrypt email in Intune](../protect/certificates-s-mime-encryption-sign.md). For more information about Outlook configuration settings, see [Microsoft Outlook configuration settings](../apps/app-configuration-policies-outlook.md) and [Add app configuration policies for managed apps without device enrollment](../apps/app-configuration-policies-managed-app.md). For Outlook for iOS and Android S/MIME information, see [S/MIME scenarios](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-scenarios) and [Configuration keys - S/MIME settings](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-settings). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### New VPN settings for Windows 10 and newer devices<!-- 6602122   -->

When you create a VPN profile using the IKEv2 connection type, there are new settings you can configure (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **VPN** for profile > **Base VPN**):

- **Device Tunnel**: Allows devices to automatically connect to VPN without requiring any user interaction, including user log-on. This feature requires you to enable **Always On**, and use **Machine certificates** as the authentication method.
- Cryptography suite settings: Configure the algorithms used to secure IKE and child security associations, which allow you to match client and server settings.

To see the settings you can configure, go to [Windows device settings to add VPN connections using Intune](../configuration/vpn-settings-windows-10.md).

Applies to:

- Windows 10 and newer

#### Configure more Microsoft Launcher settings in a device restrictions profile on Android Enterprise devices (COBO)<!-- 6285001  -->

On Android Enterprise Fully Managed devices, you can configure more Microsoft Launcher settings using a device restrictions profile (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Device Owner only** > **Device restrictions** > **Device experience** > **Fully managed**). 

To see these settings, go to [Android Enterprise device settings to allow or restrict features](../configuration/device-restrictions-android-for-work.md#device-experience).

You can also configure the Microsoft Launcher settings using an [app configuration profile](../apps/configure-microsoft-launcher.md).

Applies to:

- Android Enterprise device owner fully managed devices (COBO)

#### New features for Managed Home Screen on Android Enterprise device owner dedicated devices (COSU)<!-- 7414175 7133328 7133720 7134873 7135184    -->

On Android Enterprise devices, administrators can use device configuration profiles to customize the Managed Home Screen on dedicated devices using multi-app kiosk mode (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Device Owner Only** > **Device Restrictions** for profile > **Device experience** > **Dedicated device** > **Multi-app**).

Specifically, you can:

- Customize icons, change the screen orientation, and show app notifications on badge icons <!--7414175-->
- Hide the Managed Settings shortcut <!--7133328-->
- Easier access to the debug menu <!--7133720-->
- Create an allowed list of Wi-Fi networks <!-- 7134873-->
- Easier access to the device information <!-- 7135184-->

For more information, see [Android Enterprise device settings to allow or restrict features](../configuration/device-restrictions-android-for-work.md) and [this blog](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060).

Applies to:

- Android Enterprise device owner, dedicated devices (COSU)

#### Administrative templates updated for Microsoft Edge 84<!--7722068-->
The ADMX settings available for Microsoft Edge have been updated. End users can now configure and deploy new ADMX settings added in Edge 84. For more information, see the [Edge 84 release notes](/deployedge/microsoft-edge-relnote-stable-channel#policy-updates).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Corporate-owned, personally enabled devices (preview)<!--4442275  -->
Intune now supports Android Enterprise corporate-owned devices with a work profile for OS versions Android 8 and above. Corporate-owned devices with a work profile is one of the corporate management scenarios in the Android Enterprise solution set. This scenario is for single user devices intended for corporate and personal use. This corporate-owned, personally enabled (COPE) scenario offers:

- work and personal profile containerization
- device-level control for admins
- a guarantee for end users that their personal data and applications will remain private

The first public preview release will include a subset of the features that will be included in the generally available release. Additional features will be added on a rolling basis. The features that will be available in the first preview include:

- Enrollment: Admins can create multiple enrollment profiles with unique tokens that do not expire. Device enrollment can be done through NFC, token entry, QR code, Zero Touch, or Knox Mobile Enrollment.
- Device configuration: A subset of the existing fully managed and dedicated device settings.
- Device compliance: The compliance policies that are currently available for fully managed devices.
- Device Actions: Delete device (factory reset), reboot device, and lock device.  
- App management: App assignments, app configuration, and the associated reporting capabilities 
- Conditional Access

For more information about corporate-owned with work profile preview, see the [support blog](https://techcommunity.microsoft.com/t5/intune-customer-success/microsoft-announces-public-preview-for-android-enterprise/ba-p/1524325).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Updates to the remote lock action for macOS devices<!--7032805   -->
Changes to the remote lock action for macOS devices include:
- The recovery pin is displayed for 30 days before deletion (instead of 7 days).
- If an admin has a second browser open and tries to trigger the command again from a different tab or browser, Intune lets the command to go through. But the reporting status is set to failed rather than generating a new pin.
- The admin isn't allowed to issue another remote lock command if the previous command is still pending or if the device hasn’t checked back in.
These changes are designed to prevent the correct pin from being overwritten after multiple remote lock commands.

#### Device actions report differentiates between wipe and protected wipe<!--7118901 -->
The **Device actions** report now differentiates between the wipe and protected wipe actions. To see the report, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Monitor** > **Device Actions** (under **Other**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Microsoft Defender Firewall rule migration tool preview<!-- 6423187   -->
As a public preview, we're working on a PowerShell based tool that will migrate Microsoft Defender Firewall rules. When you install and run the tool, it automatically creates endpoint security firewall rule policies for Intune that are based on the current configuration of a Windows 10 client. For more information, see [Endpoint security firewall rule migration tool overview](../protect/endpoint-security-firewall-rule-tool.md).

#### Endpoint detection and response policy for onboarding Tenant Attached devices to Microsoft Defender for Endpoint is Generally Available<!-- 7303816   -->
As part of endpoint security in Intune, the [Endpoint detection and response (EDR) policies for use with devices managed by Configuration Manager](../protect/endpoint-security-edr-policy.md) are no longer in *preview* and are  now *Generally Available*.

To use EDR policy with devices from a supported version of Configuration Manager, configure [Tenant attach for Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md). After you complete the tenant attach configuration, you can deploy EDR policies to onboard devices managed by Configuration Manager to Microsoft Defender for Endpoint.

#### Bluetooth settings are available in Device Control profiles for Endpoint security Attack surface reduction policy <!--7032084   -->
We've added settings to manage Bluetooth on Windows 10 devices to the [Device control profile](../protect/endpoint-security-asr-profile-settings.md#device-control-profile) for *Endpoint security Attack surface Reduction policy*.  These are the same settings as those that have been available in Device restriction profiles for *Device configuration*.

#### Manage source locations for definition updates with endpoint security antivirus policy for Windows 10 devices<!-- 6347801   -->  
We've added two new settings to the *Updates* category of [endpoint security antivirus policy for Windows 10 devices](../protect/antivirus-microsoft-defender-settings-windows.md#updates)  that can help you manage how devices get update definitions:

- *Define file shares for downloading definition updates*
- *Define the order of sources for downloading definition updates*

With the new settings, you can add UNC file shares as download source locations for definition updates, and define the order in which different source locations are contacted.

#### Improved security baselines node<!-- 7433136    -->
We've made some changes to improve the usability of the [security baseline node](../protect/security-baselines.md) in the Microsoft Endpoint Manager admin center. Now when you drill in to **Endpoint security** > **Security baselines** and then select a security baseline type like the MDM Security Baseline, you're presented with the **Profiles** pane. On the Profiles pane, you view the profiles you've created for that Baseline type.  Previously the console presented an Overview pane which included an aggregate data roll up that didn't always match the details found in the reports for individual profiles.

Unchanged, from the Profiles pane you can select a profile to drill-in to view that profiles properties as well as various reports that are available under *Monitor*.  Similarly, at the same level as Profiles you can still select **Versions** to view the various versions of that profile type that you've deployed. When you drill-in to a version, you also gain access to reports, similar to the profile reports. 

#### Derived credentials support for Windows<!-- 4886090   -->
You can now use derived credentials with your Windows devices. This will  expand on the existing support for iOS/iPadOS and Android, and will be available for the same derived credential providers:
- Entrust
- Intercede
- DISA Purebred

Support for Widows includes use of a derived credential to authenticate to Wi-Fi or VPN profiles. For Windows devices, the derived credential is issued from the client app that's provided by the derived credential provider that you use.

#### Manage FileVault encryption for devices that were encrypted by the device user and not by Intune<!--5239424  -->
Intune can now [assume management of FileVault disk encryption on a macOS device that was encrypted by the device user](../protect/encrypt-devices-filevault.md#assume-management-of-filevault-on-previously-encrypted-devices), and not by Intune policy.  This scenario requires:
- The device to receive disk encryption policy from Intune that enables FileVault.
- The device user to use the Company Portal website to upload their personal recovery key for the encrypted device to Intune. To upload the key, they select the *Store recovery key* option for their encrypted macOS device.

After the user uploads their recovery key, Intune rotates the key to confirm it is valid. Intune can now manage the key and encryption as if it used policy to encrypt the device directly. Should a user need to recover their device, they can access the recovery key using any device from the following locations:   
- Company Portal website
- Company Portal app for iOS/iPadOS 
- Company Portal app for Android
- Intune app

#### Hide the personal recovery key from a device user during macOS FileVault disk encryption<!--  5475632-->
When you use endpoint security policy to configure macOS FileVault disk encryption, use the [**Hide recovery key**](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) setting to prevent display of the *personal recovery key* to the device user, while the device is being encrypted. By hiding the key during encryption, you can help keep it secure as users won’t be able to write it down while waiting for the device to encrypt. 

Later, if recovery is needed, a user can always use any device to view their personal recovery key through the Intune Company Portal website, the iOS/iPadOS Company Portal, the Android Company Portal, or the Intune app.

#### Improved view of security baseline details for devices<!-- 5536846  -->
You can now drill-in to the details for a device to view the settings details for security baselines that apply to the device. The settings appear in a simple, flat list, which includes the setting category, setting name, and status. For more information, see [View Endpoint security configurations per device](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Device compliance logs now in English<!--6014904  -->
The Intune DeviceComplianceOrg logs previously only had enumerations for ComplianceState, OwnerType, and DeviceHealthThreatLevel. Now, these logs have English information in the columns.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Assign profile and Update profile permission changes<!--7177586   -->
Role-based access control permissions have changed for Assign profile and Update profile for the Automated Device Enrollment flow:

Assign profile: Admins with this permission can also assign the profiles to tokens and assign a default profile to a token for Automated Device Enrollment.

Update profile: Admins with this permission can update existing profiles only for Automated Device Enrollment.

To see these roles, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Roles** > **All roles** > **Create** > **Permissions** > **Roles**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Scripting

#### Additional Data Warehouse v1.0 properties<!-- 6125732  -->
Additional properties are available using the Intune Data Warehouse v1.0. The following properties are now exposed via the [devices](../developer/reports-ref-devices.md#devices) entity:
- `ethernetMacAddress` -  The unique network identifier of this device.
- `office365Version` - The version of Microsoft 365 that is installed on the device.

The following properties are now exposed via the [devicePropertyHistories](../developer/reports-ref-devices.md#devicepropertyhistories) entity:
- `physicalMemoryInBytes` - The physical memory in bytes.
- `totalStorageSpaceInBytes` - Total storage capacity in bytes.

For more information, see [Microsoft Intune Data Warehouse API](../developer/reports-nav-intune-data-warehouse.md).

<!-- ########################## -->
## Week of July 06, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Update to device icons in Company Portal and Intune apps on Android<!-- 6057023 -->
We have updated the device icons in the Company Portal and Intune apps on Android devices to create a more modern look and feel and to align with the Microsoft Fluent Design System. For related information, see [Update to icons in Company Portal app for iOS/iPadOS and macOS](whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### iOS Company Portal will support Apple's Automated Device Enrollment without user affinity<!-- 7282707 --> 
The iOS Company Portal is now supported on devices enrolled using Apple's Automated Device Enrollment without requiring an assigned user. An end user can sign in to the iOS Company Portal to establish themselves as the primary user on an iOS/iPadOS device enrolled without device affinity. For more information about Automated Device Enrollment, see [Automatically enroll iOS/iPadOS devices with Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Tenant attach: ConfigMgr client details in the admin center (preview)<!-- 7552762 -->

You can now see ConfigMgr client details including collections, boundary group membership, and real-time client information for a specific device in the Microsoft Endpoint Manager admin center. For more information, see [Tenant attach: ConfigMgr client details in the admin center (preview)](../../configmgr/tenant-attach/client-details.md).

## Week of June 22, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Newly available protected apps for Intune<!-- 7248952 -->
The following protected apps are now available:
- BlueJeans Video Conferencing
- Cisco Jabber for Intune
- Tableau Mobile for Intune
- ZERO for Intune

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Use Endpoint analytics to improve user productivity and reduce IT support costs<!-- 5653063 --> 
During the next week, this feature will be rolled out. Endpoint analytics aims to improve user productivity and reduce IT support costs by providing insights into the user experience. The insights enable IT to optimize the end-user experience with proactive support and to detect regressions to the user experience by assessing user impact of configuration changes. For more information, see [Endpoint analytics preview](../../analytics/overview.md).

#### Proactively remediate end user device issues using script packages<!-- 5933328 -->
You can create and run script packages on end user devices to proactively find and fix the top support issues in your organization. Deploying script packages will help you reduce support calls. Choose to create your own script packages or deploy one of the script packages we've written and used in our environment to reduce support tickets. Intune allows you to see the status of your deployed script packages and to monitor the detection and remediation results. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports** > **Endpoint analytics** > **Proactive remediations**. For more information, see [Proactive remediations](../../analytics/proactive-remediations.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Use Microsoft Defender for Endpoint in compliance policies for Android<!-- 4425686  -->

You can now use Intune to [onboard Android devices to Microsoft for Endpoint](../protect/advanced-threat-protection-configure.md#onboard-devices). After your enrolled devices are onboarded, your compliance policies for Android can use the *threat level* signals from Microsoft Defender for Endpoint. These are the same signals that you could previously use for Windows 10 devices.

#### Configure Defender for Endpoint web protection for Android devices<!-- 6185563  -->

When you use Microsoft Defender for Endpoint for Android devices, you can [configure Microsoft Defender for Endpoint web protection](../protect/advanced-threat-protection-manage-android.md) to disable the phishing scan feature, or prevent the scan from using VPN.

Depending on how your Android device enrolls with Intune, the following options are available:

- Android device administrator - Use custom OMA-URI settings to disable the web protection feature, or disable only the use of VPNs during scans.
- Android Enterprise work profile - Use an app configuration profile and the configuration designer to disable all web protection capabilities.

<!-- ########################## -->
## Week of June 15, 2020  (2006 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management  

#### Telecommunications data transfer protection for managed apps<!-- 6884491  -->
When a hyperlinked phone number is detected in a protected app, Intune will check whether a protection policy has been applied that allows the number to be transferred to a dialer app. You can choose how to handle this type of content transfer when it is initiated from a policy managed app. When creating an app protection policy in Microsoft Endpoint Manager, select a managed app option from the **Send org data to other apps**, then select an option from **Transfer telecommunications data to**. For more information about this data protection setting, see [Android app protection policy settings in Microsoft Intune](../apps/app-protection-policy-settings-android.md) and [iOS app protection policy settings](../apps/app-protection-policy-settings-ios.md). 

#### Unified delivery of Azure Active Directory Enterprise and Office Online applications in the Windows Company Portal<!-- 7414033  -->
On the **Customization** pane of Intune, you can select to **Hide** or **Show** both **Azure AD Enterprise applications** and **Office Online applications** in the Company Portal. Each end-user will see their entire application catalog from the chosen Microsoft service. By default, each additional app source will be set to **Hide**. This feature will first take effect in the Company Portal website, with support in the Windows Company Portal expected to follow. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Customization** to find this configuration setting. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

#### Improvements to the Company Portal for macOS enrollment experience<!-- 6444452  -->
The Company Portal for macOS enrollment experience has a simpler enrollment process that aligns more closely with the Company Portal for iOS enrollment experience. Device users will  see:  
- A sleeker user interface.  
- An improved enrollment checklist.  
- Clearer instructions about how to enroll their devices.  
- Improved troubleshooting options.  

For more information about the Company Portal, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

#### Improvements to Devices page of iOS/iPadOS and macOS Company Portals<!-- 6055001 -->
We've made changes to the Company Portal **Devices** page to improve the app experience for iOS/iPadOS and Mac users. In addition to creating a more modern look and feel, we reorganized the device details under a single column with defined section headers so that it's easier for users to see their device status. We also added clearer messaging and  troubleshooting steps for users whose devices fall out of compliance. For more information about Company Portal, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md). To manually sync a device, see [Sync your iOS device manually](../user-help/sync-your-device-manually-ios.md).  

#### Cloud setting for iOS/iPadOS Company Portal app<!-- 7071303  -->
A new **Cloud** setting for the iOS/iPadOS Company Portal allows users to redirect their authentication towards the appropriate cloud for your organization. By default, the setting is configured to **Automatic**, which directs authentication towards the cloud automatically detected by the user's device. If authentication for your organization must be redirected towards a cloud other than the cloud that is automatically detected (such as Public or Government), your users can manually select the appropriate cloud by selecting the **Settings** app > **Company Portal** > **Cloud**. Your users should only change the **Cloud** setting from **Automatic** if they are signing in from another device and the appropriate cloud is not automatically detected by their device. 

#### Duplicate Apple VPP tokens<!-- 7101606  -->
Apple VPP tokens with the same **Token Location** are now marked as **Duplicate** and can be synced again when the duplicate token has been removed. You can still assign and revoke licenses for tokens that are marked as duplicate. However, licenses for new apps and books purchased may not be reflected once a token is marked as duplicate. To find Apple VPP tokens for your tenant, from [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Connectors and tokens** > **Apple VPP Tokens**. For more information about VPP tokens, see [How to manage iOS and macOS apps purchased through Apple Volume Purchase Program with Microsoft Intune](../apps/vpp-apps-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Add multiple root certificates for EAP-TLS authentication in Wi-Fi profiles on macOS devices<!-- 2077871  -->

On macOS devices, you can create a Wi-Fi profile, and select the Extensible Authentication Protocol (EAP) authentication type  (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Wi-Fi** for profile > **Wi-Fi type** set to Enterprise).

When you set the **EAP Type** to **EAP-TLS**, **EAP-TTLS**, or **PEAP** authentication,  you can add multiple root certificates. Previously, you could only add one root certificate.

For more information on the settings you can configure, see [Add Wi-Fi settings for macOS devices in Microsoft Intune](../configuration/wi-fi-settings-macos.md).

Applies to:
- macOS

#### Use PKCS certificates with Wi-Fi profiles on Windows 10 and newer devices<!-- 3246388   -->
You can authenticate Windows Wi-Fi profiles with SCEP certificates (**Device configuration** > **Profiles** > **Create profile** > **Windows 10 and later** for platform > **Wi-Fi** for profile type > **Enterprise** > **EAP type**). Now, you can use PKCS certificates with your Windows Wi-Fi profiles. This feature allows users to authenticate Wi-Fi profiles using new or existing PKCS certificate profiles in your tenant. 

For more information on the Wi-Fi settings you can configure, see [Add Wi-Fi settings for Windows 10 and later devices in Intune](../configuration/wi-fi-settings-windows.md).

Applies to:
- Windows 10 and newer

#### Wired network device configuration profiles for macOS devices<!-- 3508686  -->
A new macOS device configuration profile is available that configures wired networks (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Wired Network** for profile). Use this feature to create 802.1x profiles to manage wired networks, and deploy these wired networks to your macOS devices.

For more information in this feature, see [Wired networks on macOS devices](../configuration/wired-networks-configure.md).

Applies to:
- macOS

#### Use Microsoft Launcher as the default launcher for fully managed Android Enterprise devices<!-- 4927976   -->
On Android Enterprise device owner devices, you can set Microsoft Launcher as the default launcher for fully managed devices (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Device owner** > **Device restrictions** for profile > **Device experience**). To configure all other Microsoft Launcher settings, use [app configuration policies](../apps/configure-microsoft-launcher.md). 

Also, there are some other UI updates, including **Dedicated devices** being renamed to **Device experience**.

To see all the settings you can restrict, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md). 

Applies to:
- Android Enterprise device owner fully managed devices (COBO)

#### Use Autonomous Single App Mode settings to configure the iOS Company Portal app to be a sign in/sign out app<!-- 7055619   -->
On iOS/iPadOS devices, you can configure apps to run in autonomous single app mode (ASAM). Now, the Company Portal app supports ASAM, and can be configured to be a "sign in/sign out" app. In this mode, users must sign in to the Company Portal app to use other apps and the Home screen button on the device. When they sign out of the Company Portal app, the device returns to single app mode, and locks on the Company Portal app.

To configure the Company Portal to be in ASAM, go to **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile > **Autonomous Single App Mode**.

For more information, see [Autonomous single app mode (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) and [single app mode](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1) (opens Apple's web site).

Applies to:
- iOS/iPadOS

#### Configure content caching on macOS devices<!-- 7106872   -->
On macOS devices, you can create a configuration profile that configures content caching (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device features** for profile). Use these settings to delete cache, allow shared cache, set a cache limit on the disk, and more.

For more information on content caching, see [ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (opens Apple's web site).

To see the settings you can configure, go to [macOS device feature settings in Intune](../configuration/macos-device-features-settings.md).

Applies to:
- macOS

#### Add new schema settings, and search for existing schema settings using OEMConfig on Android Enterprise<!-- 6394386   -->
In Intune, you can use OEMConfig to manage settings on Android Enterprise devices (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **OEMConfig** for profile). When you use the **Configuration designer**, the properties in the app schema are shown. Now, in the **Configuration designer**, you can:

- Add new settings to the app schema.
- Search for new and existing settings in the app schema.

For more information on OEMConfig profiles in Intune, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Applies to:
- Android Enterprise

#### Block Shared iPad temporary sessions on Shared iPad devices<!-- 6613794  -->
In Intune, there's a new **Block Shared iPad temporary sessions** setting that blocks temporary sessions on Shared iPad devices (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile type > **Shared iPad**). When enabled, end users can't use the Guest account. They must sign in to the device with their Managed Apple ID and password. 

For more information, see [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md).

Applies to:
- Shared iPad devices running iOS/iPadOS 13.4 and newer

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Bring-your-own-devices can use VPN to deploy<!--5015344  -->
The new  Autopilot profile **Skip Domain Connectivity Check** toggle lets you deploy Hybrid Azure AD Join devices without access to your corporate network using your own 3rd party Win32 VPN client. To see the new toggle, go to [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices**  > **Windows** > **Windows enrollment** > **Deployment profiles** > **Create profile** > **Out-of-box experience (OOBE)**.

#### Enrollment Status Page profiles can be set to device groups<!--3952138 -->
Previously, Enrollment Status Page (ESP) profiles could only be targeted to user groups. Now you can also set them to target device groups. For more information, see [Set up an Enrollment Status Page](../enrollment/windows-enrollment-status.md).

#### Automated Device Enrollment sync errors<!-- 6988214 -->
New errors will be reported for iOS/iPadOS and macOS devices, including
- Invalid characters in the phone number or if that field is empty. 
- Invalid or empty configuration name for the profile. 
- Invalid/expired cursor value or if no cursor is found.
- Rejected or expired token. 
- The department field is empty or the length is too long. 
- Profile is not found by Apple and a new one needs to be created. 
- A count of removed Apple Business Manager devices will be added to the overview page where you see the status of your devices.

#### Shared iPads for Business<!--6367326   -->
You can use Intune and Apple Business Manager to easily and securely set up Shared iPad so that multiple employees can share devices. Apple's [Shared iPad](https://developer.apple.com/education/shared-ipad/) provides a personalized experience for multiple users while preserving user data. Using a Managed Apple ID, users can access their apps, data, and settings after signing into any Shared iPad in their organization. Shared iPad works with federated identities.

To see this feature, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **iOS** > **iOS enrollment** > **Enrollment program tokens** > **choose a token** > **Profiles** > **Create profile** > **iOS**. On the **Management Settings** page, select **Enroll without User Affinity** and you'll see the **Shared iPad** option.

Requires: iPadOS 13.4 and later. This release added support for temporary sessions with Shared iPad so that users can access a device without a Managed Apple ID. Upon logout, the device erases all user data so that the device is immediately ready for use, eliminating the need for a device wipe. 

#### Updated user interface for Apple's Automated Device Enrollment<!--7430322 -->
The user interface has been updated to replace Apple's Device Enrollment Program to Automated Device Enrollment to reflect Apple terminology.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Device remote lock pin available for macOS<!--7281557   -->
The availability for macOS device remote lock pins has been increased from 7 days to 30 days.

#### Change primary user on co-managed devices<!--7319183  -->
You can change a device's primary user for co-managed Windows devices. For more information on how to find and change it, see [Find the primary user of an Intune device](../remote-actions/find-primary-user.md). This feature will be rolling out gradually over the next few weeks.

#### Setting the Intune primary user also sets the Azure AD owner property<!--7319227 -->
This new feature automatically sets the owner property on newly-enrolled Hybrid Azure AD joined devices at the same time that the Intune primary user is set. For more information on the primary user, see [Find the primary user of an Intune device](../remote-actions/find-primary-user.md).

This is a change to the enrollment process and only applies to newly enrolled devices. For existing Hybrid Azure AD Joined devices, you must manually update the Azure AD Owner property. To do this, you can use the [Change primary user feature](../remote-actions/find-primary-user.md#change-a-devices-primary-user) or [a script](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices).

When Windows 10 devices become Hybrid Azure Active Directory Joined, the first user of the device becomes the primary user in Endpoint Manager.  Currently, the user isn't set on the corresponding Azure AD device object. This causes an inconsistency when comparing the *owner* property from an Azure AD portal with the *primary user* property in Microsoft Endpoint Manager admin center. The Azure AD owner property is used for securing access to BitLocker recovery keys. The property isn't populated on Hybrid Azure AD Joined devices. This limitation prevents set up of self-service of BitLocker recovery from Azure AD. This upcoming feature solves this limitation.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Hide the recovery key from users during FileVault 2 encryption for macOS devices<!-- 5459801  -->
We've added a new setting to the *FileVault* category within the [macOS Endpoint Protection](../protect/endpoint-protection-macos.md#filevault) template: **Hide recovery key**. This setting hides the personal key from the end user during FileVault 2 encryption. 

To view the personal recovery key of an encrypted macOS device, the device user can go to any of the following locations and click on *get recovery key* for the macOS device: 

- The iOS/iPadOS company portal app
- The Intune app
- The company portal website
- The Android company portal app

#### Support for S/MIME signing and encryption certificates with Outlook on Android Fully Managed<!--5896415   -->
You can now use certificates for S/MIME signing and encryption with Outlook on devices that run Android Enterprise Fully Managed.

This expands on the support added last month for other Android versions (Support for S/MIME signing and encryption certificates with Outlook on Android). You can provision these certificates by using SCEP and PKCS imported certificate profiles.

For more information about this support, see [Sensitivity labeling and protection in Outlook for iOS and Android](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) in the Exchange documentation.

#### Add a link to your company portal support website to emails for noncompliance<!-- 7225498    -->
When you [configure a notification message template](../protect/actions-for-noncompliance.md#create-a-notification-message-template) for sending email notifications for noncompliance, use the new setting **Company Portal Website Link** to automatically include a link to your Company Portal website. With this option set to *Enable*, users with noncompliant devices who receive email based on this template can use the link to open a website to learn more about why their device isn’t compliant. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Licensing

#### Admins no longer require an Intune license to access Microsoft Endpoint Manager admin console<!--1335430 -->
You can now set a tenant-wide toggle that removes the Intune license requirement for admins to access the MEM admin console and query graph APIs. Once you remove the license requirement, you can never reinstate it. 


> [!Note]
> Some actions, including the Teamviewer Connector flow, still require an Intune license to complete.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Scripts 

#### Availability of Shell scripts on macOS devices<!-- 7134839  -->
Shell scripts for macOS devices are now available for Government Cloud and China customers. For more information about shell scripts, see [Use shell scripts on macOS devices in Intune](../apps/macos-shell-scripts.md).



<!-- ########################## -->
## Week of June 8, 2020   

### App management  

#### Updates to informational screen in Company Portal for iOS/iPadOS <!--7032452 -->
An informational screen in Company Portal for iOS/iPadOS has been updated to better explain what an admin can see and do on devices. These clarifications are only about corporate-owned devices. Only the text has been updated, no actual modifications have been made to what the admin can see or do on user devices. To see the updated screens, go to [UI updates for Intune end-user apps](./whats-new-app-ui.md).

#### Updated Android APP Conditional Launch end-user experience<!-- 5736084 -->
The 2006 release of the Android Company Portal has changes that build on the updates from the 2005 release. In 2005, we rolled out an update where end users of Android devices that are issued a warn, block, or wipe by an app protection policy see a full page message describing the reason for the warn, block, or wipe and the steps to remediate the issues. In 2006, first-time users of Android apps assigned an app protection policy will be taken through a guided flow to remediate issues that cause their app access to be blocked. 



## What's New archive
For previous months, see the [What's New archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
