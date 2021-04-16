---
# required metadata
title: What's new in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Find out what's new in the Intune Azure portal
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/30/2021
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

!-- ########################## -->

## Week of April 12, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### Device configuration

### New modern authentication method with Apple Setup Assistant <!--4843770 -->

When creating an Automated Device Enrollment profile, can now choose a new authentication method: **Setup Assistant with modern authentication**. This method provides all the security from Setup Assistant but avoids the issue of leaving end users stuck on a device they can't use while the Company Portal installs on the device. The user has to authenticate using Azure AD multi-factor authentication (MFA) during the setup assistant screens. This will require an additional Azure AD login post-enrollment in the Company Portal app to gain access to corporate resources protected by Conditional Access. The correct Company Portal version will automatically be sent down as a required app to the device for iOS/iPadOS. For macOS, here are the options to get the Company Portal on the device - [Add the Company Portal for macOS app](../apps/apps-company-portal-macos.md).

Enrollment is completed once the user lands on the home screen, and users can freely use the device for resources not protected by Conditional Access. User affinity is established when users complete the additional Azure AD login into the Company Portal app on the device. If the tenant has multi-factor authentication turned on for these devices or users, the users will be asked to complete multi-factor authentication during enrollment during Setup Assistant. Multi-factor authentication is not required, but it is available for this authentication method within Conditional Access if needed.

This method has the following options for installing the Company Portal:

- For iOS/iPadOS: The **Install Company Portal** setting will not be there when choosing this flow for iOS/iPadOS. The CP will be a required app on the device with the correct app configuration policy on it once the end user lands on the home screen. ​User must sign in with Azure AD credentials into the CP after enrollment to gain access to resources protected by Conditional Access.
- For macOS: Users must sign into the Company Portal to complete Azure AD registration and gain access to resources protected by Conditional Access. The end user will not be locked to the CP after landing on the home page, but an additional login into the CP will be required to access corporate resources and be compliant.  For more information, see [Add the macOS Company Portal app](../apps/apps-company-portal-macos.md).

For information on how to use this authentication method on iOS/iPadOS devices, see [Automatically enroll iOS/iPadOS devices by using Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

For information on how to use this authentication method on macOS devices, see [Automatically enroll macOS devices with the Apple Business Manager or Apple School Manager](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile).

<!-- ########################## -->
## Week of March 29, 2021 (Service release 2103)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Intune management agent for macOS devices is now a universal app<!-- 9294405 -->
When you deploy shell scripts or custom attributes for macOS devices from Microsoft Endpoint Manager, it deploys the new universal version of the Intune management agent app that runs natively on Apple Silicon Mac machines. The same deployment will install the x64 version of the app on Intel Mac machines. Rosetta 2 is required to run x64 (Intel) version of apps on Apple Silicon Macs. To install Rosetta 2 on Apple Silicon Macs automatically, you can deploy a shell script in Endpoint Manager. For more information, see [Microsoft Intune management agent for macOS](../apps/macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).

### Device security

#### Update for Microsoft Tunnel<!-- 9574820 -->

We’ve released a [new version](../protect/microsoft-tunnel-configure.md#microsoft-tunnel-updates) of the Microsoft Tunnel Gateway, which includes the following changes:

- Various bug fixes and enhancements.

The Tunnel Gateway server will automatically update to the new release.


<!-- ########################## -->
## Week of March 22, 2021 (Service release 2103)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management
#### Microsoft 365 Apps for macOS devices are now universal apps<!-- 9076318  -->
When you deploy Microsoft 365 Apps for macOS devices from Microsoft Endpoint Manager, it now deploys the new universal versions of the app that runs natively on Apple Silicon Macs. The same deployment will install the x64 versions of the app on Intel Macs running macOS 10.14 and higher. To add Microsoft 365 Apps for macOS, in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apps** > **All apps** > **Add**. Select **macOS** in the **App type** list under **Microsoft 365 Apps**. For related information, see [Assign Microsoft 365 to macOS devices with Microsoft Intune](../apps/apps-add-office365-macos.md).

#### Additional configuration keys for the Microsoft Launcher app<!-- 9364310  -->
You can now set folder configuration settings for Microsoft Launcher on Android Enterprise corporate owned fully managed devices. By using an app configuration policy and configuration key values, you can set values for folder shape, folder opened to full screen, and folder scroll direction. Also, you can position the folder on the home screen in addition to positioning apps and weblinks. Additionally, you can choose to allow end users to modify the folder style values within the app. For more information about Microsoft Launcher, see [Configure Microsoft Launcher for Android Enterprise with Intune](..\apps\configure-microsoft-launcher.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### More Microsoft Edge settings, and setting categories are removed in Settings Catalog for macOS<!-- 9220407   -->
On macOS devices, you can use the Settings Catalog to configure Microsoft Edge version 77 and newer (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings Catalog**).

In this release:

- More Microsoft Edge settings are added.
- Temporarily, the setting categories are removed. To find a specific setting, use the **Microsoft Edge - All** category, or search for the setting name. For a list of settings, see  [Microsoft Edge - Policies](/DeployEdge/microsoft-edge-policies).

For more information on the Settings Catalog, see [Use the settings catalog to configure settings](../configuration/settings-catalog.md).

Applies to:
- macOS
- Microsoft Edge

#### Windows 10 in cloud configuration is available as a Guided Scenario<!-- 9272086  -->
Windows 10 in cloud configuration is a Microsoft-recommended device configuration for Windows 10. Windows 10 in cloud configuration is optimized for the cloud and designed for users with focused workflow needs.

There's a guided scenario that automatically adds the apps, and creates the policies that configures your Windows 10 devices in a cloud configuration.

For more information, see [Guided scenario for Windows 10 in cloud configuration](../fundamentals/cloud-configuration.md).

Applies to:
- Windows 10 and newer

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Increasing recommended maximum number of iOS/iPadOS and macOS devices per enrollment token<!--8568668  -->
Previously, we recommended that you don't exceed 60,000 iOS/iPadOS or macOS devices per Automated Device Enrollment (ADE) token. This recommended limit is now increased to 200,000 devices per token. For more information about ADE tokens, see [Automatically enroll iOS/iPadOS devices by using Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume).

#### Update of column names in All devices view and Export report<!-- 8854380  -->
To accurately reflect the data in the columns, we've updated the column names in the All devices view and the Export report to be "Primary User UPN", "Primary User email address", and "Primary User display name".

### End of support for Internet Explorer 11<!--9218996 -->
Intune will end support for Internet Explorer 11 admin access to the Admin Portal web app UI on March 31, 2021. Move to Edge or another [supported browser](supported-devices-browsers.md) before that time to administer any of your Microsoft services built on Azure.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Health status details for Microsoft Tunnel Gateway servers<!-- 8460911    -->
We've added the ability to see detailed heath status information for Tunnel Gateway servers within the Microsoft Endpoint Manager admin center.

On the new [*Health check* tab](../protect/microsoft-tunnel-monitor.md#use-the-admin-center-ui), you'll see the following information:

- Last check-in - When the server last checked-in with Intune.
- Number of current connections - The number of active connections at last check-in
- Throughput- The megabits per second that traverse the serves NIC at last check-in.
- CPU usage - The average CPU use.
- Memory usage - The average memory use.
- Latency - The average time for IP packets to traverse the NIC.
- TLS certificate expiration status and days before expiration - How long the TLS certificate that secures client to server communication for the tunnel remains valid.

#### Public preview of Tunnel client functionality in Microsoft Defender for Endpoint app for Android<!-- 9248143 -->

As announced at Ignite, Microsoft Tunnel client functionality is migrating into the Microsoft Defender for Endpoint app. With this preview, you can start to use a preview version of Microsoft Defender for Endpoint as the Tunnel app for supported devices. The existing Tunnel client remains available, but will eventually be phased out in favor of the Defender for Endpoint app.

This public preview applies to:  
- Android Enterprise
  - Fully managed
  - Corporate-owned work profile
  - Personally-owned work profile

For this preview, you must opt in to gain access to the preview version of Microsoft Defender for Endpoint, and then migrate supported devices from the standalone Tunnel client app to the preview app. For details, see [Migrate to the Microsoft Defender for Endpoint app](../protect/microsoft-tunnel-migrate-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Intune apps

#### Microsoft Launcher configuration keys<!-- 8980621  -->
For Android Enterprise fully managed devices, the Microsoft Launcher for Intune app now provides additional customization. In Launcher, you can configure the set of displayed apps and weblinks, as well as the order of these apps and weblinks. The displayed app list and position (order) of app configurations have been merged together to simplify home screen customization. For more information, see [Configure Microsoft Launcher](../apps/configure-microsoft-launcher.md).

#### Microsoft Edge for macOS devices will be a universal app<!-- 9175989 9176098 9176466 9275782  -->
When you deploy the Microsoft Edge app for macOS devices from Microsoft Endpoint Manager, it now deploys the new universal version of the app that runs natively on Apple Silicon Macs. The same deployment will install the x64 version of the app on Intel Macs. To add Microsoft Edge for macOS, in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apps** > **All apps** > **Add**. Select **macOS** in the **App type** list under **Microsoft Edge, version 77 and later**. For related information, see [Add Microsoft Edge to macOS devices using Microsoft Intune](../apps/apps-edge-macos.md).

#### Newly available protected apps for Intune<!-- 9099719  -->
The following protected apps are now available for Microsoft Intune:
- FleetSafer by Cogosense Technology Inc.
- Senses by Mazrica Inc.
- Fuze Mobile for Intune by Fuze, Inc.
- MultiLine for Intune by Movius Interactive Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

#### Improved notification experience in the iOS/iPadOS Company Portal app<!-- 7219429  -->
The Company Portal app can now store, as well as display, push notifications sent to your users' iOS/iPadOS devices from the Microsoft Endpoint Manager admin center. Users who have opted in to receive Company Portal push notifications can view and manage the customized stored messages that you send to their devices in the **Notifications** tab of the Company Portal. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Scripting


#### Export localized Intune report data using Graph APIs<!-- 8612346  -->
You can now specify that the report data that you export using the Microsoft Endpoint Manager reporting export [API](../fundamentals/reports-export-graph-apis.md) can contain localized columns only, or localized and non-localized columns. The localized and non-localized columns option will be selected by default for most reports, which will prevent breaking changes. For related information about reports, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md) and [Intune reports and properties available using Graph API](../fundamentals/reports-export-graph-apis.md).

<!-- ########################## -->
## Week of March 8, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### New version of the PFX Certificate Connector<!-- 9494956-->

We’ve released a new version of the PFX Certificate Connector, version **6.2101.16.0**. This update adds improvements to to the PFX Create flow to prevent duplication of Certificate Request files on on-premises servers that host the connector.

For more information about certificate connectors, including a list of connector releases for both certificate connectors, see [Certificate connectors](../protect/certificate-connectors.md).

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
You can now use the User attribute **CN={{UserPrincipalName}}** variable in the subject or SAN of a [PKCS certificate profile](../protect/certificates-pfx-configure.md#create-a-trusted-certificate-profile) or [SCEP certificate profile](../protect/certificates-profile-scep.md#create-a-scep-certificate-profile) for Android devices. This support requires the device have a user, such as devices enrolled as:
- Android Enterprise fully managed
- Android Enterprise personally-owned work profile

User attributes are not supported for devices that don’t have user associations, such as devices that are enrolled as Android Enterprise dedicated. For example, a profile that uses *CN={{UserPrincipalName}}* in the subject or SAN won’t be able to get the user principal name when there is no user on the device.

#### Use app protection policies for Defender for Endpoint on Android and iOS<!-- 6486982   7362746  -->
You can now use [Microsoft Defender for Endpoint in app protection policies for devices that run Android or iOS](../protect/advanced-threat-protection-configure.md#create-and-assign-app-protection-policy-to-set-device-risk-level).
- Configure your MAM conditional launch policy to include **Max allowed threat level** signals from Microsoft Defender for Endpoint on iOS devices and Android devices.
- Choose to **Block Access** or **Wipe Data** based on whether or not the device meets the expected threat level.

When configured, end users are prompted to install and set up the **Microsoft Defender for Endpoint** app from the applicable app store. As a prerequisite, you must set up your **Microsoft Defender for Endpoint** connector and switch on the toggle to send risk data to your app protection policies. For related information, see [App protection policies overview](../apps/app-protection-policy.md), and [Use Microsoft Defender for Endpoint in Microsoft Intune](..\protect\advanced-threat-protection.md).

#### Configure Attack surface reduction rules to block malware from gaining persistence through WMI<!-- 8902661   -->
You can now configure the rule named **Block persistence through WMI event subscription** as part of an [Attack surface reduction rules](../protect/endpoint-security-asr-policy.md#attack-surface-reduction-profiles) profile in Endpoint security.

This rule prevents malware from abusing WMI to attain persistence on a device. Fileless threats employ various tactics to stay hidden, to avoid being seen in the file system, and to gain periodic execution control. Some threats can abuse the WMI repository and event model to stay hidden.

When configured as [setting for *Attack surface reduction*](../protect/endpoint-security-asr-profile-settings.md#attack-surface-reduction-rules-profile) policy for Endpoint security, the following options are available:
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

#### Endpoint analytics in Microsoft Productivity Score  <!-- IN8529842 -->

There's a new Endpoint Analytics page in [Microsoft Productivity Score](/microsoft-365/admin/productivity/productivity-score) that shares organizational level insights with the other roles outside of Microsoft Endpoint Manager. Understanding how your devices contribute to your end-users' experience is critical to enabling users to reach their goals. For more information, see [Endpoint analytics in Microsoft Productivity Score](../../analytics/productivity-score.md).
#### Endpoint analytics Application Reliability report<!-- IN5653073 -->
A new **Application Reliability** report will be available in Endpoint analytics. This report provides insight into potential issues for desktop applications on managed PCs. You can quickly identify the top applications that are impacting end user productivity, as well as see aggregate app usage and app failure metrics for these applications. You'll be able to troubleshoot by drilling into a specific device and viewing a timeline of app reliability events. This report is expected to be available in public preview during March 2021. For more information, see [Endpoint analytics application reliability](../../analytics/app-reliability.md).

#### Restart frequency (preview) in Endpoint analytics <!--6225459 -->
Endpoint analytics [startup performance](../../analytics/startup-performance.md) currently provides IT with insights to measure and optimize PC boot times. However, restart frequency can be just as impactful to the user experience since a device that reboots daily because of blue screens will have a poor user experience even if the boot times are fast. We have now included a preview report on restart frequencies within your organization to help you identify problematic devices. For more information, see [Restart frequency (preview) in endpoint analytics](../../analytics/restart-frequency.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Role-based access permissions update for Microsoft Tunnel Gateway<!-- 8554762   -->
To help control who has rights to manage the Microsoft Tunnel, we've added [**Microsoft Tunnel Gateway**](../protect/microsoft-tunnel-prerequisites.md#permissions) as a new permissions group to Intune role-based access control. This new group includes the following permissions:

- **Create** - Configure Microsoft Tunnel Gateway servers, server configurations, and sites.
- **Update** (modify) - Update Microsoft Tunnel Gateway servers, server configurations, and sites.
- **Delete** - Delete Microsoft Tunnel Gateway servers, server configurations, and sites.
- **Read** - View Microsoft Tunnel Gateway servers, server configurations, and sites.

By default, Intune Administrators and Azure Active Directory administrators have these permissions. You can also add these permissions to [custom roles you create](create-custom-role.md) for your Intune tenant.

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

To see the policies you have configured, open Microsoft Edge, and go to `edge://policy`.

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
You can configure and deploy new ADMX settings that apply to Microsoft Edge version 88. To see the new policies, go to [Microsoft Edge release notes](/deployedge/microsoft-edge-relnote-stable-channel#policy-updates).

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

## What's New archive

For previous months, see the [What's New archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
