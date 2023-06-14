---
# required metadata
title: What's new in Microsoft Intune
titleSuffix:
description: Find out what's new in Microsoft Intune
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- tier2
- M365-identity-device-management
- highseo
---

# What's new in Microsoft Intune

Learn what's new each week in Microsoft Intune.

You can also read:  
- [**Important notices**](#notices)
- [Past releases](whats-new-archive.md) in the What's new archive
- Information about [how Intune service updates are released](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728)

> [!NOTE]
> Each [monthly update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) may take up to three days to rollout and will be in the following order:
>
> - Day 1: Asia Pacific (APAC)
> - Day 2: Europe, Middle East, Africa (EMEA)
> - Day 3: North America
> - Day 4+: Intune for Government
>
> Some features may roll out over several weeks and might not be available to all customers in the first week.
>
> For a list of upcoming Intune feature releases, see [In development for Microsoft Intune](../fundamentals/in-development.md). For new information about Autopilot, see [Windows Autopilot What's new](../../autopilot/windows-autopilot-whats-new.md).

You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Get notified when this page is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us` -->

<!-- Common categories: -->

<!-- ### App management -->
<!-- ### Device configuration -->
<!-- ### Device enrollment -->
<!-- ### Device management -->
<!-- ### Device security -->
<!-- ### Intune apps -->
<!-- ### Monitor and troubleshoot -->
<!-- ### Role-based access control -->
<!-- ### Scripts -->
<!-- ### Tenant administration -->

## Week of June 12, 2023

### App management

#### Microsoft Store for Business or Microsoft Store for Education<!-- 24250535 wndraft wnready -->
Apps added from the Microsoft Store for Business or Microsoft Store for Education will no longer deploy to devices and users. Apps will show as "not applicable" in reporting. Apps already deployed are unaffected. Use the [new Microsoft Store app](../apps/store-apps-microsoft.md) to deploy Microsoft Store apps to devices or users. For related information, see [Plan for Change: Ending support for Microsoft Store for Business and Education apps](../fundamentals/whats-new.md#plan-for-change-ending-support-for-microsoft-store-for-business-and-education-apps) for upcoming dates when Microsoft Store for Business apps will no longer deploy and Microsoft Store for Business apps will be removed.

For more information, see the following resources:
- [Update to Intune integration with the Microsoft Store on Windows](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/update-to-intune-integration-with-the-microsoft-store-on-windows/ba-p/3585077)
- [Embracing the Future of Microsoft Store with Intune: A Step-by-Step Guide](https://www.youtube.com/watch?v=c534X9yMvDo)
- [Embracing the Future of Microsoft Store with Intune for Education: A Step-by-Step Guide](https://www.youtube.com/watch?v=Heoi0RuClQM)

## Week of June 5, 2023

### Device configuration

### Android Enterprise 11+ devices can use Zebra's latest OEMConfig app version<!-- 8675347 -->  

On Android Enterprise devices, you can use OEMConfig to add, create, and customize OEM-specific settings in Microsoft Intune (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **OEMConfig**).

There's a new **Zebra OEMConfig Powered by MX** OEMConfig app that aligns more closely to Google's standards. This app supports Android Enterprise 11.0 and newer devices.

The older **Legacy Zebra OEMConfig** app continues to support devices with Android 11 and earlier.

In your Managed Google Play, there are two versions of Zebra OEMConfig app. Be sure to select the correct app that applies to your Android device versions.

For more information on OEMConfig and Intune, go to [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Applies to:

- Android Enterprise 11.0 and newer

## Week of May 29, 2023  


### Device management

### Intune UI displays Windows Server devices as distinct from Windows clients for the Security Management for Microsoft Defender for Endpoint scenario<!-- 16882836 -->  
To support the [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md) (MDE security configuration) scenario, Intune now differentiates Windows devices in Azure Active Directory as either *Windows Server* for devices that run Windows Server, or as *Windows* for devices that run Windows 10 or Windows 11.

With this change, you'll be able to improve policy targeting for MDE security configuration. For example, you can use dynamic groups that consist of only Windows Server devices, or only Windows client devices (Windows 10/11).

For more information about this change, see the Intune customer success blog [Support tip: Windows Server devices will now be identified as a new OS platform in Microsoft Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-windows-server-devices-will-now-be-identified-as-a/ba-p/3767773).

### Tenant administration  

#### Organizational messages for Windows 11 now generally available<!-- 15272978 -->  
Use organizational messages to deliver branded, personalized call-to-actions to employees. Select from more than 25 messages that support employees through device onboarding and lifecycle management, in 15 different languages. Messages can be assigned to Azure AD user groups. They're shown just above the taskbar, in the notifications area, or in the Get started app on devices running Windows 11. Messages continue to appear or reappear based on the frequency you configure in Intune, and until the user has visited the customized URL.

Other features and functionality added in this release include:

- Confirm licensing requirements prior to first message.
- Choose from eight new themes for taskbar messages.  
- Give messages a custom name.
- Add scope groups and scope tags.
- Edit the details of a scheduled message.

Scope tags were previously unavailable for organizational messages. With the addition of scope tag support, Intune adds the default scope tag to every message created before June 2023. Admins that want access to those messages must be associated with a role that has the same tag. For more information about available features and how to set up organizational messages, see
[Overview of organizational messages](../remote-actions/organizational-messages-overview.md).   

## Week of May 22, 2023 (Service release 2305)

### App management

#### Update to macOS shell scripts maximum running time limit<!-- 23187517 -->
Based on customer feedback, we're updating the Intune agent for macOS (version 2305.019) to extend the maximum script run time to 60 minutes. Previously, the Intune agent for macOS only allowed shell scripts to run for up to 15 minutes before reporting the script as a failure. The Intune agent for macOS 2206.014 and higher supports the 60-minute timeout.

#### Assignment filters support app protection policies and app configuration policies<!-- 7476247 -->  
Assignment filters support MAM app protection policies and app configuration policies. When you create a new filter, you can fine tune MAM policy targeting using the following properties:

- Device Management Type
- Device Manufacturer
- Device Model
- OS Version
- Application Version
- MAM Client Version

> [!IMPORTANT]
> All new and edited app protection policies that use **Device Type** targeting are replaced with assignment filters.

For more information on filters, go to [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md).

#### Update to MAM reporting in Intune<!-- 10100428  -->  
MAM reporting has been simplified and overhauled, and now uses Intune's newest reporting infrastructure. Benefits of this include improved data accuracy and instantaneous updating. You can find these streamlined MAM reports in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Monitor**. All MAM data available to you is contained within the new **App protection status** report and **App configuration status** report.

#### Global quiet time app policy settings<!-- 15424417   -->  
The global quiet time settings allow you to create policies to schedule quiet time for your end users. These settings automatically mute Microsoft Outlook email and Teams notifications on iOS/iPadOS and Android platforms. These policies can be used to limit end user notifications received after work hours. For more information, see [Quiet time notification policies](../apps/app-office-policies.md#quiet-time-notification-policies).

### Device configuration

#### Introducing enhanced chat in Remote Help<!-- 10602997 -->

Introducing enhanced chat with Remote Help. With the new and enhanced chat you can maintain a continuous thread of all messages. This chat provides support for special characters and additional languages including Chinese and Arabic.

For more information on Remote Help, go to [Remote Help](../fundamentals/remote-help.md).

Applies to:
Windows 10/11 

#### Remote Help administrators can reference audit log sessions<!-- 9052185  -->  
For Remote Help, in addition to existing session reports, administrators can now reference audit logs sessions created in Intune. This feature enables administrators to reference past events for troubleshooting and analyzing log activities.

For more information on Remote Help, go to [Remote Help](../fundamentals/remote-help.md).

Applies to:

- Windows 10
- Windows 11

#### Turn on/off Personal data encryption on Windows 11 devices using the settings catalog<!-- 10346018  -->  
The settings catalog includes hundreds of settings that you can configure and deploy to your devices.

In the settings catalog, you can turn on/off **Personal data encryption** (PDE). PDE is a security feature introduced in Windows 11 version 22H2 that provides more encryption features for Windows.

PDE is different than BitLocker. PDE encrypts individual files and content, instead of whole volumes and disks. You can use PDE with other encryption methods, such as BitLocker.

For more information on the settings catalog, go to:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md)
- [Common Tasks you can complete using the Settings Catalog in Intune](../configuration/settings-catalog-common-features.md)

This feature applies to:

- Windows 11

#### Visual Studio ADMX settings are in the Settings Catalog and Administrative Templates <!-- 10875730 -->  
Visual Studio settings are included in the Settings Catalog and Administrative Templates (ADMX). Previously, to configure Visual Studio settings on Windows devices, you imported them with ADMX import.

For more information on these policy types, go to:

- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)
- [Use Windows 10/11 templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md)
- [Visual Studio Administrative Templates (ADMX)](/visualstudio/install/administrative-templates)

Applies to:

- Windows 10
- Windows 11

#### Group policy analytics supports scope tags<!-- 12714882  -->  
In Group Policy analytics, you import your on-premises GPO. The tool analyzes your GPOs and shows the settings that can (and can't) be used in Intune.

When you import your GPO XML file in Intune, you can select an existing scope tag. If you don't select a scope tag, then the **Default** scope tag is automatically selected. Previously, when you imported a GPO, the scope tags assigned to you were automatically applied to the GPO.

Only admins within that scope tag can see the imported policies. Admins not in that scope tag can't see the imported policies.

Also, admins within their scope tag can migrate the imported policies that they have permissions to see. To migrate an imported GPO into a Settings Catalog policy, a scope tag must be associated with the imported GPO. If a scope tag isn't associated, then it can't migrate to a Settings Catalog policy. If no scope tag is selected, then a default scope tag is automatically applied.

For more information on scope tags and Group Policy analytics, go to:

- [Analyze your on-premises GPOs using Group Policy analytics in Microsoft Intune](../configuration/group-policy-analytics.md)
- [Create a Settings Catalog policy using your imported GPOs](../configuration/group-policy-analytics-migrate.md)
- [Use role-based access control (RBAC) and scope tags for distributed IT](scope-tags.md)

#### Introducing Intune integration with the Zebra Lifeguard Over-the-Air service (public preview)<!-- 14340034  -->  
Now available in public preview, Microsoft Intune supports integration with Zebra Lifeguard Over-the-Air service, which allows you to deliver OS updates and security patches over-the-air to eligible Zebra devices that are enrolled with Intune. You can select the firmware version you want to deploy, set a schedule, and stagger update downloads and installs. You can also set minimum battery, charging status, and network conditions requirements for when the update can happen.

Available for Android Enterprise Dedicated and Fully Managed Zebra devices that are running Android 8 or later, and requires an account with Zebra.

#### New Google domain allowlist settings for Android Enterprise personally owned devices with a work profile<!-- 14711684 -->  
On Android Enterprise personally owned devices with a work profile, you can configure settings that restrict device features and settings.

Currently, there's an **Add and remove accounts** setting that can allow Google accounts be added to the work profile. For this setting, when you select **Allow all accounts types**, you can also configure:

- **Google domain allow-list**:  Restricts users to add only certain Google account domains in the work profile. You can import a list of allowed domains or add them in the admin center using the `contoso.com` format. When left blank, by default, the OS might allow adding all Google domains in the work profile.

For more information on the settings you can configure, go to [Android Enterprise device settings list to allow or restrict features on personally owned devices using Intune](../configuration/device-restrictions-android-enterprise-personal.md).

Applies to:

- Android Enterprise personally owned devices with a work profile

#### Renaming Proactive remediation to Remediations and moving to a new location<!-- 16526263  -->  
Proactive remediations are now Remediations and are available from **Devices** > **Remediations**. You can still find Remediations in both the new location and the existing **Reports** > **Endpoint Analytics** location until the next Intune service update.

Remediations are currently not available in the new [Devices experience preview](../fundamentals/microsoft-intune-admin-center-devices.md).

Applies to:

- Windows 10
- Windows 11

#### Remediations are now available in Intune for US Government GCC High and DoD<!-- 16526300 -->  
Remediations (previously known as proactive remediations) are now available in [Microsoft Intune for US Government GCC High and DoD](../fundamentals/intune-govt-service-description.md)

Applies to:

- Windows 10
- Windows 11

#### Create inbound and outbound network traffic rules for VPN profiles on Windows devices<!-- 17943658 -->  

> [!NOTE]
> This setting is coming in a future release, possibly the 2307 Intune release.

You can create a device configuration profile that deploys a VPN connection to devices (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **VPN** for profile type).

In this VPN connection, you can use the **Apps and Traffic rules** settings to create network traffic rules.

There's a new **Direction** setting you can configure. Use this setting to allow Inbound and Outbound traffic from the VPN connection:

- **Outbound** (default): Allows only traffic to external networks/destinations to flow using the VPN. Inbound traffic is blocked from entering the VPN.
- **Inbound**: Allows only traffic coming from external networks/ sources to flow using the VPN. Outbound traffic is blocked from entering the VPN.

For more information on the VPN settings you can configure, including the network traffic rule settings, go to [Windows device settings to add VPN connections using Intune](../configuration/vpn-settings-windows-10.md).

Applies to:

- Windows 10 and later

#### New settings available in the macOS settings catalog <!-- 18430228  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type.

**Microsoft Defender > Antivirus engine**:

- Scanning inside archive files
- Enable file hash computation

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### Wipe device action and new obliteration behavior setting available for macOS<!-- 16647226 -->  
You can now use the **Wipe** device action instead of Erase for macOS devices. Additionally, you can configure the **Obliteration Behavior** setting as part of the **Wipe** action.

This new key allows you to control the wipe fallback behavior on Macs that have Apple Silicon or the T2 Security Chip. To find this setting, navigate to **Devices** > **macOS** > [Select a device] > **Overview** > **Wipe** in the **Device action** area.

For more information on the Obliteration Behavior setting, go to Apple's Platform Deployment site [Erase Apple devices - Apple Support](https://support.apple.com/guide/deployment/erase-devices-dep0a819891e/web).

Applies to:

- macOS  

### Device enrollment  

#### Account driven Apple User Enrollment available for iOS/iPadOS 15+ devices (public preview)<!-- 14161683  -->  
Intune supports account driven user enrollment, a new and improved variation of Apple User Enrollment for iOS/iPadOS 15+ devices. Now available for public preview, the new option utilizes just-in-time registration, which eliminates the need for the Company Portal app during enrollment. Device users can initiate enrollment directly in the Settings app, resulting in a shorter and more efficient onboarding experience. You can continue to target iOS/iPadOS devices using the existing profile-based user enrollment method that uses Company Portal. Devices running iOS/iPadOS, version 14.8.1 and earlier remain unaffected by this update and can continue to use the existing method. For more information, see [Set up account driven Apple User Enrollment](../enrollment/apple-account-driven-user-enrollment.md).  

### Device security

#### New security baseline for Microsoft 365 Office Apps<!-- 9587103  -->  
We've released a new security baseline to help you manage security configurations for **M365 Office Apps**. This new baseline uses an updated template and experience that uses the unified settings platform seen in the Intune settings catalog. You can view the list of settings in the new baseline at [Microsoft 365 Apps for Enterprise baseline settings (Office)](../protect/security-baseline-v2-office-settings.md).

The new Intune security baseline format aligns the presentation of settings that are available to the settings found in the Intune settings catalog. This alignment helps resolve past issues for setting names and implementations for settings that could create conflicts. The new format also improves the reporting experience for baselines in the Intune admin center.

The Microsoft 365 Office Apps baseline can help you rapidly deploy configurations to your Office Apps that meet the security recommendations of the Office and security teams at Microsoft. As with all baselines, the default baseline represents the recommended configurations. You can modify the default baseline to meet the requirements of your organization.

To learn more, see [Security baselines overview](../protect/security-baselines.md).

Applies to:

- Windows 10
- Windows 11

#### Security baseline update for Microsoft Edge version 112<!-- 3408610  -->  
We've released a new version of the Intune security baseline for Microsoft Edge, version 112. In addition to releasing this new version for Microsoft Edge, the new baseline uses an updated template experience that uses the unified settings platform seen in the Intune settings catalog. You can view the list of settings in the new baseline at [Microsoft Edge baseline settings (version 112 and higher)](../protect/security-baseline-v2-edge-settings.md).

The new Intune security baseline format aligns the presentation of settings that are available to the settings found in the Intune settings catalog. This alignment helps resolve past issues for setting names and implementations for settings that could create conflicts. The new format also improves the reporting experience for baselines in the Intune admin center.

Now that the new baseline version is available, all new profiles you create for Microsoft Edge use the new baseline format and version. While the new version becomes the default baseline version, you can continue to use the profiles you've previously created for older versions of Microsoft Edge. But, you can't create new profiles for those older versions of Microsoft Edge.

To learn more, see [Security baselines overview](../protect/security-baselines.md).

Applies to:

- Windows 10
- Windows 11

### Intune apps

#### Newly available protected apps for Intune<!-- 17782795, 17782816, 17851777, 17644967, 17948005, 17971727 -->  
The following protected apps are now available for Microsoft Intune:

- Achievers by Achievers Inc.
- Board.Vision for iPad by Trusted Services PTE. LTD.
- Global Relay by Global Relay Communications Inc.
- Incorta (BestBuy) by Incorta, Inc. (iOS)
- Island Enterprise Browser by Island (iOS)
- Klaxoon for Intune by Klaxoon (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of May 8, 2023

### Device configuration

#### Device Firmware Configuration Interface (DFCI) supports Dynabook devices<!-- 10249859 -->
For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type.

Some Dynabook devices running Windows 10/11 are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

For more information about DFCI profiles, go to:
- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](../../autopilot/dfci-management.md)

Applies to:
- Windows 10
- Windows 11

#### eSIM bulk activation for Windows PCs via download server is now available on the Settings Catalog<!-- 19809114 -->
You can now perform at-scale configuration of Windows eSIM PCs using the Settings Catalog. A download server (SM-DP+) is configured using a configuration profile. 

Once the devices receive the configuration, they automatically download the eSIM profile. For more information, go to [eSIM configuration of a download server](../configuration/esim-device-configuration-download-server.md)

Applies to:

- Windows 11
- eSIM capable devices

## Week of May 1, 2023

### App management

#### macOS shell scripts maximum running time limit<!-- 19396575 -->
We have fixed an issue that caused Intune tenants with long-running shell scripts to not report back on the script run status. The macOS Intune agent stops any macOS shell scripts that run longer than 15 minutes. These scripts report as failed. The new behavior is enforced from macOS Intune agent version 2305.019.

#### DMG app installation for macOS<!-- 13911806 -->  
The DMG app installation feature for macOS is now generally available. Intune supports **required** and **uninstall** assignment types for DMG apps. The Intune agent for macOS is used to deploy DMG apps. For related information, see [Deploy DMG-type applications to managed macOS devices](../fundamentals/whats-new-archive.md#deploy-dmg-type-applications-to-managed-macos-devices).

#### Deprecation of Microsoft Store for Business and Education<!-- 19677954 -->
The Microsoft Store for Business connector is no longer accessible in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Apps added from the Microsoft Store for Business or Microsoft Store for Education won't sync with Intune. Apps that have previously synced continue to be available and deploy to devices and users.

It's now also possible to delete Microsoft Store for Business apps from the **Apps** pane in the Microsoft Intune admin center so that you can clean up your environment as you move to the new Microsoft Store app type.

For related information, see [Plan for Change: Ending support for Microsoft Store for Business and Education apps](../fundamentals/whats-new.md#plan-for-change-ending-support-for-microsoft-store-for-business-and-education-apps) for upcoming dates when Microsoft Store for Business apps won't deploy and Microsoft Store for Business apps are removed.

### Device configuration

#### Remote Help now supports conditional access capability<!--16108299 -->  
Administrators can now utilize conditional access capability when setting up policies and conditions for Remote Help. For example, multi-factor authentication, installing security updates, and locking access to Remote Help for a specific region or IP addresses.

For more information, go to:

- [Conditional access](../protect/conditional-access.md)
- [Remote Help](../fundamentals/remote-help.md#setup-conditional-access-for-remote-help)

### Device security

#### Updated settings for Microsoft Defender in endpoint security Antivirus policy<!-- 19991301  -->  
We've updated the available settings in the *Microsoft Defender Antivirus* profile for endpoint security Antivirus policy.  You can find this profile in the Intune admin center at **Endpoint security** > **Antivirus** > *Platform:* **Windows 10, Windows 11, and Windows Server**  > *Profile:* **Microsoft Defender Antivirus**.  
- **The following settings have been added**:

  - Metered Connection Updates
  - Disable Tls Parsing
  - Disable Http Parsing
  - Disable Dns Parsing
  - Disable Dns Over Tcp Parsing
  - Disable Ssh Parsing
  - Platform Updates Channel
  - Engine Updates Channel
  - Security Intelligence Updates Channel
  - Allow Network Protection Down Level
  - Allow Datagram Processing On Win Server
  - Enable Dns Sinkhole

  For more information about these settings, see the [Defender CSP]( /windows/client-management/mdm/Defender-csp?WT.mc_id=Portal-fx).
The new settings are also available through the Intune [Settings Catalog](../configuration/settings-catalog.md).

- **The following setting has been deprecated**:

  - Allow Intrusion Prevention System

  This setting now appears with the *Deprecated* tag. If this deprecated setting was previously applied on a device, the setting value is updated to *NotApplicable* and has no effect on the device. If this setting is configured on a device, there's no effect on the device.

Applies to:

- Windows 10
- Windows 11

## Week of April 17, 2023 (Service release 2304)

### App management

#### Changes to iCloud app backup and restore behavior on iOS/iPadOS and macOS devices<!-- 16261392  -->  
As an app setting, you can select to **Prevent iCloud app backup** for iOS/iPadOS and macOS devices. You have the option to *not* backup managed App Store apps and line-of-business (LOB) apps on iOS/iPadOS, as well as managed App Store apps on macOS devices (macOS LOB apps don't support this feature), for both user and device licensed VPP/non-VPP apps. This update includes both new and existing App Store/LOB apps sent with and without VPP that are being added to Intune and targeted to users and devices.

Preventing the backup of the specified managed apps ensures that these apps can be properly deployed via Intune when the device is enrolled and restored from backup. If the admin configures this new setting for new or existing apps in their tenant, then managed apps can and will be reinstalled for devices. But, Intune doesn't allow them to be backed up.

This new setting appears in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by modifying the properties of an app. For an existing app, you can select **Apps** > **iOS/iPadOS** or **macOS** > *select the app* > **Properties** > Assignment **Edit**. If no group assignment has been set, select **Add group** to add a group. Modify either the setting under **VPN**, **Uninstall on device removal**, or **Install as removable**. Then, select **Prevent iCloud app backup**. The **Prevent iCloud app backup** setting is used to prevent backup of app data for the application. Set to **No** to allow the app to be backed up by iCloud.

For more information, see [Changes to applications' backup and restore behavior on iOS/iPadOS and macOS devices](https://techcommunity.microsoft.com/t5/intune-customer-success/changes-to-applications-backup-and-restore-behavior-on-ios/ba-p/3692064) and [Assign apps to groups with Microsoft Intune](../apps/apps-deploy.md).

#### Prevent automatic updates for Apple VPP apps<!-- 16876430   -->  
You can control the automatic update behavior for Apple VPP at the per-app assignment level using the **Prevent automatic updates** setting. This setting is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** or **macOS** > *Select a volume purchase program app* > **Properties** > **Assignments** > *Select an Azure AD group* > **App settings**.

Applies to:

- iOS/iPadOS
- macOS

### Device configuration

#### Updates to the macOS Settings Catalog <!-- 17673709  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type.

The new setting is located under:

**Microsoft AutoUpdate (MAU) > [targeted app]**:

- Update channel override

The following settings have been deprecated:

**Microsoft AutoUpdate (MAU) > [targeted app]**:

- Channel Name (Deprecated)

**Privacy > Privacy Preferences Policy Control > Services > Listen Event or Screen Capture**:

- Allowed

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### The Microsoft Enterprise SSO plug-in for Apple devices is now generally available<!-- 17826329  -->  
In Microsoft Intune, there's a Microsoft Enterprise SSO plug-in. This plug-in provides single sign-on (SSO) to iOS/iPadOS and macOS apps and websites that use Microsoft Azure AD for authentication.

This plug-in is now generally available (GA).

For more information about configuring the Microsoft Enterprise SSO plug-in for Apple devices in Intune, go to [Microsoft Enterprise SSO plug-in in Microsoft Intune](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md).

Applies to:

- iOS/iPadOS
- macOS

#### Disable Activation Lock device action for supervised macOS devices<!-- 16813146  -->  

You can now use the **Disable Activation Lock** device action in Intune to bypass Activation Lock on Mac devices without requiring the current username or password. This new action is available in **Devices** > **macOS** > select one of your listed devices > **Disable Activation Lock**.

More information on managing Activation Lock is available at [Bypass iOS/iPadOS Activation Lock with Intune](../remote-actions/device-activation-lock-disable.md) or on Apple's website at [Activation Lock for iPhone, iPad, and iPod touch - Apple Support](https://support.apple.com/en-us/HT201365).

Applies to:

- macOS 10.15 or later

#### ServiceNow Integration is now Generally Available (GA)<!-- 18163832  -->  
Now generally available, you can view a list of ServiceNow incidents associated with the user you've selected in the Intune Troubleshooting workspace.  This new feature is available under **Troubleshooting + Support** > select a user > **ServiceNow Incidents**.  The list of incidents shown have a direct link back to the source incident and show key information from the incident.  All incidents listed link the "Caller" identified in the incident with the user selected for Troubleshooting.

For more information, go to [Use the troubleshooting portal to help users at your company](service-now-integration.md).

#### More permissions to support administrators in controlling delivery of organization messages<!-- 16982298  -->  

With more permissions administrators can control delivery of content created and deployed from Organizational messages and the delivery of content from Microsoft to users.

The **Update organizational message control** RBAC permission for organizational messages, determines who can change the Organizational Messages toggle to allow or block Microsoft direct messages. This permission is also added to the **Organizational Messages Manager** built-in role.

Existing custom roles for managing Organizational Messages must be modified to add this permission for users to modify this setting.

- For more information, about role-based access control (RBAC), see [RBAC with Microsoft Intune](../fundamentals/role-based-access-control.md).
- For more information, about prerequisites for organization messages, see [Organizational messages prerequisites](../remote-actions/organizational-messages-prerequisites.md#role-based-access-control-requirements).

### Device management

#### Endpoint security firewall rules support for ICMP type<!-- 5653356  -->  
You can now use the **IcmpTypesAndCodes** setting to configure inbound and outbound rules for [Internet Control Message Protocol](/windows/security/threat-protection/windows-firewall/create-an-inbound-icmp-rule) (ICMP) as part of a firewall rule. This setting is available in the [*Microsoft Defender Firewall rules*](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune) profile for the *Windows 10, Windows 11, and Windows Server* platform.

Applies to:

- Windows 11 and later

#### Manage Windows LAPS with Intune policies (public preview)<!-- 11890571  -->  
Now available in a public preview, manage Windows Local Administrator Password Solution (Windows LAPS) with Microsoft Intune [Account protection policies](../protect/endpoint-security-account-protection-policy.md). To get started, see [Intune support for Windows LAPS](../protect/windows-laps-overview.md).

[Windows LAPS](/windows-server/identity/laps/laps-overview) is a Windows feature that allows you to manage and backs up the password of a local administrator account on your Azure Active Directory-joined or Windows Server Active Directory-joined devices.

To manage LAPS, Intune configures the Windows [LAPS configuration service provider](/windows/client-management/mdm/LAPS-csp) (CSP) that is built in to Windows devices. It takes precedence over other sources of Windows LAPS configurations, like GPOs or the Microsoft Legacy LAPS tool. Some of the capabilities you can use when Intune manages Windows LAPS include:

- Define password requirements like complexity and length that apply to the local administrator accounts on a device.
- Configure devices to rotate their local admin account passwords on a schedule. And, back up the account and password in your Azure Active Directory or on-premises Active Directory.
- Use an Intune device action from the admin center to manually rotate the password for an account on your own schedule.
- View account details from within the Intune admin center, like the account name and password. This information can help you recover devices that are otherwise inaccessible.
- Use Intune reports to monitor your LAPS policies, and when devices last rotated passwords manually or by schedule.  

Applies to:

- Windows 10
- Windows 11

#### New settings available for macOS software update policies<!-- 16646756  -->  
macOS software update policies now include the following settings to help manage when updates install on a device. These settings are available when the *All other updates* update type is configured to *Install later*:

- **Max User Deferrals**:  When the *All other updates* update type is configured to *Install later*, this setting allows you to specify the maximum number of times a user can postpone a minor OS update before it's installed. The system prompts the user once a day. Available for devices running macOS 12 and later.

- **Priority**: When the *All other updates* update type is configured to *Install later*, this setting allows you to specify values of *Low* or *High* for the scheduling priority for downloading and preparing minor OS updates. Available for devices running macOS 12.3 and later.

For more information, see [Use Microsoft Intune policies to manage macOS software updates](../protect/software-updates-macos.md).

Applies to:

- macOS

#### Introducing the new partner portals page<!-- 17829024  -->  
You can now manage hardware specific information on your HP or Surface devices from our partner portals page.

The HP link takes you to HP Connect where you can update, configure, and secure the BIOS on your HP devices.
The Microsoft Surface link takes you to the Surface Management Portal where you can get insights into device compliance, support activity, and warranty coverage.

To access the Partner portals page, you must enable the Devices pane preview and then navigate to **Devices** > **Partner Portals**.

#### Windows Update compatibility reports for Apps and Drivers are now generally available<!-- 17917026  -->  
The following Microsoft Intune reports for [Windows Update compatibility](../protect/windows-update-compatibility-reports.md) are out of preview and now generally available:

- **Windows feature update device readiness report** - This report provides per-device information about compatibility risks that are associated with an upgrade or update to a chosen version of Windows.

- **Windows feature update compatibility risks report** - This report provides a summary view of the top compatibility risks across your organization for a chosen version of Windows. You can use this report to understand which compatibility risks impact the greatest number of devices in your organization.

These reports can help you plan an upgrade from Windows 10 to 11, or for installing the latest Windows feature update.

### Device security

#### Microsoft Intune Endpoint Privilege Management is generally available<!--1564177  -->  
Microsoft Endpoint Privilege Management (EPM) is now generally available and no longer in preview.

With [Endpoint Privilege Management](../protect/epm-overview.md), admins can set policies that allow standard users to perform tasks normally reserved for an administrator. To do so, you configure policies for *automatic* and *user-confirmed* workflows that elevate the run-time permissions for apps or processes you select. You then assign these policies to users or devices that have end users running without Administrator privileges. After policy is received by a device, EPM brokers the elevation on behalf of the user, allowing them to elevate approved applications without needing full administrator privileges. EPM also includes built-in insights and reporting.

Now that EPM is out of preview, it requires another license to use. You can choose between a stand-alone license that adds only EPM, or license EPM as part of the Microsoft Intune Suite. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

While Endpoint Privilege Management is now generally available, the [reports for EPM](../protect/epm-reports.md) will transition to a feature in *preview*, and will receive some more enhancements before being removed from preview.

#### Support for WDAC Application ID tagging with Intune Firewall Rules policy<!-- 17224780  -->  
Intune's *Microsoft Defender Firewall Rules* profiles, which are available as part of [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md), now include the Policy App ID setting. This setting is described in the [*MdmStore/FirewallRules/{FirewallRuleName}/PolicyAppId*](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx#mdmstorefirewallrulesfirewallrulenamepolicyappid) CSP and supports specifying a Windows Defender Application Control (WDAC) Application ID tag.

With this capability, you can scope your firewall rules to an application or a group of applications and rely on your WDAC policies to define those applications. By using tags to link to and rely on WDAC policies, your Firewall Rules policy won't need to rely on the firewall rules option of an absolute file path, or use of a variable file path that can reduce security of the rule.

Use of this capability requires you to have WDAC policies in place that include *AppId* tags that you can then specify in your Intune Microsoft Defender Firewall Rules.

For more information, see the following articles in the Windows Defender Application Control documentation:

- [About application control for Windows](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)
- [WDAC Application ID (AppId) Tagging guide](/windows/security/threat-protection/windows-defender-application-control/appidtagging/windows-defender-application-control-appid-tagging-guide)

Applies to:

- Windows 10/11

#### New App and browser isolation profile for Intune's endpoint security Attack Surface Reduction policy<!-- 17392386  -->  
We have released a new experience creating new *App and Browser Isolation* profiles for endpoint security Attack Surface Reduction policy. The experience for editing your previously created App and Browser isolation policies remains the same, and you can continue to use them. This update applies only for the new [App and Browser Isolation](../protect/endpoint-security-asr-policy.md#attack-surface-reduction-profiles) policies you create for the *Windows 10 and later* platform.

This update is part of the continuing [rollout of new profiles for endpoint security policies](../fundamentals/whats-new-archive.md#new-profile-templates-and-settings-structure-for-endpoint-security-policies), which began in April 2022.

Additionally, the new profile includes the following changes for the settings it includes:

- **Block external content from non-enterprise approved sites** - This setting is removed from the updated profile as it was supported only by Microsoft Edge Legacy. Microsoft Edge Legacy support ended in March 2021. [Microsoft 365 apps say farewell to Internet Explorer 11 and Windows 10 sunsets Microsoft Edge Legacy - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/microsoft-365-blog/microsoft-365-apps-say-farewell-to-internet-explorer-11-and/ba-p/1591666).

- **Clipboard file type** – This setting is added to the updated profile and determines the type of content that can be copied from the host to Application Guard environment and vice versa. You can view the CSP for this new setting at [Settings/ClipboardFileType](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#settingsclipboardfiletype) in the WindowsDefenderApplicationGuard CSP documentation.

### Intune apps

#### Newly available protected apps for Intune<!-- 17318943, 17319737, 17457189, 17624650  -->
The following protected apps are now available for Microsoft Intune:
- ixArma by INAX-APPS (iOS)
- myBLDNG by Bldng.ai (iOS)
- RICOH Spaces V2 by Ricoh Digital Services
- Firstup - Intune by Firstup, Inc. (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Role-based access control

#### New Assign (RBAC) permissions for organizational messages<!-- 16872833  -->  
The **Assign** RBAC permissions for organizational messages determines who can assign target Azure AD groups to an organizational message. To access RBAC permissions, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Roles**.

This permission is also added to the **Organizational Messages Manager** built-in role.  Existing custom roles for managing Organizational Messages must be modified to add this permission for users to modify this setting.

- For more information, about role-based access control (RBAC), see [RBAC with Microsoft Intune](../fundamentals/role-based-access-control.md).
- For more information, about prerequisites for organization messages, see [Organizational messages prerequisites](../remote-actions/organizational-messages-prerequisites.md#role-based-access-control-requirements).

### Tenant administration

#### Delete organizational messages<!-- 15273028  -->  
You can now delete organizational messages from Microsoft Intune.  After you delete a message, it's removed from Intune, and no longer appears in the admin center. You can delete a message anytime, regardless of its status. Intune automatically cancels active messages after you delete them. For more information, see [Delete organizational messages](../remote-actions/organizational-messages-cancel.md#delete-message).  

#### Review audit logs for organizational messages<!-- 16576073 -->  
Use audit logs to track and monitor organizational message events in Microsoft Intune. To access the logs, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Audit logs**. For more information, see [Audit logs for Intune activities](../fundamentals/monitor-audit-logs.md#audit-logs-for-intune-workloads).  

## Week of April 10, 2023

### Device configuration

#### User configuration support for Windows 10 multi-session VMs is now GA<!-- 17060455 -->

You can now:

- Configure user scope policies using **Settings catalog** and assign to groups of users.
- Configure user certificates and assign to users.
- Configure PowerShell scripts to install in the user context and assign to users.

Applies to:

- **Windows 10**
- Virtual machines created in [Azure Public and Azure Government clouds](../fundamentals/intune-govt-service-description.md)

## Week of April 3, 2023

### Device configuration

#### Add Google accounts to Android Enterprise personally owned devices with a work profile<!-- 9113561 -->

On Android Enterprise personally owned devices with a work profile, you can configure settings that restrict device features and settings. Currently, there's an **Add and remove accounts** setting. This setting prevents accounts from being added in the work profile, including preventing Google accounts.

This setting changed. You can now add Google accounts. The **Add and remove accounts** setting options are:

- **Block all accounts types**: Prevents users from manually adding or removing accounts in the work profile. For example, when you deploy the Gmail app into the work profile, you can prevent users from adding or removing accounts in this work profile.
- **Allow all accounts types**: Allows all accounts, including Google accounts. These Google accounts are blocked from installing apps from the **Managed Google Play Store**.

  This setting requires:

  - Google Play app version 80970100 or higher

- **Allow all accounts types, except Google accounts** (default): Intune doesn't change or update this setting. By default, the OS might allow adding accounts in the work profile.

For more information on the settings you can configure, go to [Android Enterprise device settings list to allow or restrict features on personally owned devices using Intune](../configuration/device-restrictions-android-enterprise-personal.md).

Applies to:

- Android Enterprise personally owned devices with a work profile

## Week of March 27, 2023

### App management

#### Update macOS DMG apps<!-- 13155074 -->
You can now update apps of type **macOS apps (DMG)** deployed using Intune. To edit a DMG app that's already created in Intune, upload the app update with the same bundle identifier as the original DMG app. For related information, see [Add a macOS DMG app to Microsoft Intune](../apps/lob-apps-macos-dmg.md).

#### Install required apps during pre-provisioning<!-- 12716381 -->
A new toggle is available in the Enrollment Status Page (ESP) profile that allows you to select whether you want to attempt to install required applications during the pre-provisioning (white glove) technician phase. We understand that installing as many applications as possible during pre-provisioning is desired to reduce the end user setup time. If there's an app install failure, ESP continues except for the apps specified in the ESP profile. To enable this function, you need to edit your Enrollment Status Page profile by selecting **Yes** on the new setting entitled **Only fail selected apps in technician phase**. This setting only appears if you have blocking apps selected. For information about ESP, go to [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).

## Week of March 20, 2023 (Service release 2303) 

### App management

### More minimum OS versions for Win32 apps<!-- 16842404  -->  
Intune supports more minimum operating system versions for Windows 10 and 11 when installing Win32 apps. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **Windows** > **Add** > **Windows app (Win32)**. In the **Requirements** tab next to **Minimum operating system**, select one of the available operating systems. Other OS options include:

- Windows 10 21H2
- Windows 10 22H2
- Windows 11 21H2
- Windows 11 22H2

#### Managed apps permission is no longer required to manage VPP apps<!-- 17205644  -->  
You can view and manage VPP apps with only the **Mobile apps** permission assigned. Previously, the **Managed apps** permission was required to view and manage VPP apps. This change doesn't apply to Intune for Education tenants who still need to assign the **Managed apps** permission. More information about permissions in Intune is available at [Custom role permissions](../fundamentals/create-custom-role.md#custom-role-permissions).

### Device configuration

#### New settings and setting options available in the macOS Settings Catalog <!-- 16813395  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Microsoft Defender > Tamper protection**:

- Enforcement level

**Microsoft Office > Microsoft OneDrive**:

- Automatic upload bandwidth percentage
- Automatically and silently enable the Folder Backup feature (aka Known Folder Move)
- Block apps from downloading online-only files
- Block external sync
- Disable automatic sign in
- Disable download toasts
- Disable personal accounts
- Disable tutorial
- Display a notification to users once their folders have been redirected
- Enable Files On-Demand
- Enable simultaneous edits for Office apps
- Force users to use the Folder Backup feature (aka Known Folder Move)
- Hide dock icon
- Ignore named files
- Include ~/Desktop in Folder Backup (aka Known Folder Move)
- Include ~/Documents in Folder Backup (aka Known Folder Move)
- Open at login
- Prevent users from using the Folder Backup feature (aka Known Folder Move)
- Prompt users to enable the Folder Backup feature (aka Known Folder Move)
- Set maximum download throughput
- Set maximum upload throughput
- SharePoint Prioritization
- SharePoint Server Front Door URL
- SharePoint Server Tenant Name

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### Add custom Bash scripts to configure Linux devices<!-- 12508999  -->  
In Intune, you can add existing Bash scripts to configure Linux devices (**Devices** > **Linux** > **Configuration Scripts**).

When you create this script policy, you can set the context that the script runs in (user or root), how frequently the script runs, and how many times execution should retry.

For more information on this feature, go to [Use custom Bash scripts to configure Linux devices in Microsoft Intune](../configuration/custom-settings-linux.md).

Applies to:

- Linux Ubuntu Desktops

### Device enrollment

#### Support for the await final configuration setting for iOS/iPadOS Automated device enrollment (public preview)<!-- 13156553  -->  
Now in public preview, Intune supports a new setting called **Await final configuration** in eligible new and existing iOS/iPadOS automated device enrollment profiles. This setting enables an out-of-the-box locked experience in Setup Assistant. It prevents device users from accessing restricted content or changing settings on the device until most Intune device configuration policies are installed. You can configure the setting in an existing automated device enrollment profile, or in a new profile (**Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment program tokens** > **Create profile**). For more information, see [Create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).  

#### New setting gives Intune admins control over device-to-category mapping<!-- 15029839 -->  
Control visibility of the device category prompt in Intune Company Portal. You can now hide the prompt from end users and leave the device-to-category mapping up to Intune admins. The new setting is available in the admin center under **Tenant Administration** > **Customization** > **Device Categories**. For more information, see [Device categories](../apps/company-portal-app.md#device-categories).

#### Support for multiple enrollment profiles and tokens for fully managed devices <!-- 14205233  -->  
Create and manage multiple enrollment profiles and tokens for Android Enterprise fully managed devices. With this new functionality, you can now use the *EnrollmentProfileName* dynamic device property to automatically assign enrollment profiles to fully managed devices. The enrollment token that came with your tenant remains in a default profile. For more information, see [Set up Intune enrollment of Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md).

#### New Azure AD frontline worker experience for iPad (public preview)<!-- 6367427  -->  
*This capability begins to roll out to tenants in mid-April.*

Intune now supports a frontline worker experience for iPhones and iPads using Apple automated device enrollment. You can now enroll devices that are enabled in Azure AD shared mode via zero-touch. For more information about how to configure automated device enrollment for shared device mode, see [Set up enrollment for devices in Azure AD shared device mode](../enrollment/automated-device-enrollment-shared-device-mode.md).  

Applies to:

- iOS/iPadOS

### Device management

#### Endpoint security firewall policy support for log configurations<!-- 16730565   -->  
You can now configure settings in [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune) that configure firewall logging options. These settings can be found in the *Microsoft Defender Firewall* profile template for the *Windows 10 and later* platform, and are available for the *Domain*, *Private*, and *Public* profiles in that template.

Following are the new settings, all found in the [Firewall configuration service provider (CSP)](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx):

- Enable Log Success Connections
- Log File Path
- Enable Log Dropped Packets
- Enable Log Ignored Rules

Applies to:

- Windows 10
- Windows 11

#### Endpoint security firewall rules support for Mobile Broadband (MBB)<!-- 16730577  -->  
The **Interface Types** setting in [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune) now include the option for **Mobile Broadband**. Interface Types is available in the **Microsoft Defender Firewall Rules** profile for all platforms that support Windows. For information about the use of this setting and option, see [Firewall configuration service provider (CSP)](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx).

Applies to:  

- Windows 10
- Windows 11

#### Endpoint security firewall policy support for network list manager settings<!-- 9803477  -->  
We've added a pair of network list manager settings to [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune). To help determine when an Azure AD device is or isn't on your on-premises domain subnets, you can use the network list manager settings. This information can help firewall rules apply correctly.

The following settings are found in a new category named *Network List Manager*, that's available in the *Microsoft Defender Firewall* profile template for the *Windows 10, Windows 11, and Windows Server* platform:

- Allowed Tls Authentication Endpoints
- Configured Tls Authentication Network Name

For information about Network Categorization settings, see [NetworkListManager CSP](/windows/client-management/mdm/policy-csp-networklistmanager).

Applies to:  

- Windows 10
- Windows 11

#### Improvements to Devices area in admin center (public preview) <!-- 12775837 -->  
The Devices area in the admin center now has a more consistent UI, with more capable controls and an improved navigation structure so you can find the information you need faster. To opt in to the public preview and try out the new experience, go to **Devices** and flip the toggle at the top of the page. Improvements include:

* A new scenario-focused navigation structure.
* New location for platform pivots to create a more consistent navigation model.
* A reduction in journey, helping you get to your destination faster.
* Monitoring and reports are within the management workflows, giving you easy access to key metrics and reports without having to leave the workflow.
* A consistent way across list views to search, sort, and filter data.

For more information about the updated UI, see [Try new Devices experience in Microsoft Intune](microsoft-intune-admin-center-devices.md).

### Device security

#### Microsoft Intune Endpoint Privilege Management (public preview)<!-- 15654169   -->  
As a public preview, you can now use Microsoft Intune Endpoint Privilege Management. With Endpoint Privilege Management, admins can set policies that allow standard users to perform tasks normally reserved for an administrator. Endpoint Privilege Management can be configured in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) at **Endpoint security** > **Endpoint Privilege Management**.

With the public preview, you can configure policies for *automatic* and *user-confirmed* workflows that elevate the run-time permissions for apps or processes you select. You then assign these policies to users or devices that have end users running without Administrator privileges. Once policy is received, Endpoint Privilege Management will broker the elevation on behalf of the user, allowing them to elevate approved applications without needing full administrator privileges. The preview also includes built-in insights and reporting for Endpoint Privilege Management.

To learn how to activate the public preview and use Endpoint Privilege Management policies, start with [Use Endpoint Privilege Management with Microsoft Intune](../protect/epm-overview.md). Endpoint Privilege Management is part of the [Intune Suite](../fundamentals/intune-add-ons.md) offering, and free to try while it remains in public preview.

### Intune apps

#### Newly available protected apps for Intune<!-- 16927438, 17030201, 17074872 17103353 -->  
The following protected apps are now available for Microsoft Intune:

- EVALARM by GroupKom GmbH (iOS)
- ixArma by INAX-APPS (Android)
- Seismic | Intune by Seismic Software, Inc.
- Microsoft Viva Engage by Microsoft (formally Microsoft Yammer)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Diagnostic data collection for Endpoint Privilege Management<!-- 17392824   -->  
To support the release of Endpoint Privilege Management, we've updated [Collect diagnostics from a Windows device](../remote-actions/collect-diagnostics.md) to include the following data, which is collected from devices enabled for Endpoint Privilege Management:

- Registry keys:  
  - HKLM\SOFTWARE\Microsoft\EPMAgent

- Commands:  
  - %windir%\system32\pnputil.exe /enum-drivers
 
- Log files:  
  - %ProgramFiles%\Microsoft EPM Agent\Logs\\\*.*
  - %windir%\system32\config\systemprofile\AppData\Local\mdm\\\*.log

#### View status for pending and failed organizational messages<!-- 17017707  -->  
We've added two more states to organizational message reporting details to make it easier to track pending and failed messages in the admin center.

- **Pending**: The message hasn't been scheduled yet and is currently in progress.
- **Failed**: The message failed to schedule due to a service error.

For information about reporting details, see [View reporting details for organizational messages](../remote-actions/organizational-messages-reporting.md).  


#### More reporting information related to tenant attach devices<!-- 9220597  -->  
You can now view information for tenant attach devices in the existing antivirus reports under the Endpoint Security workload. A new column differentiates between devices managed by Intune and devices managed by Configuration Manager. This reporting information is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Endpoint security** > **Antivirus**.

## Week of March 13, 2023

### Device management

#### Meta Quest 2 and Quest Pro are now in Open Beta (US only) on Microsoft Intune for Android Open Source Devices

Microsoft Intune for Android open source project devices (AOSP) has welcomed Meta Quest 2 and Quest Pro into Open Beta for the US market.

For more information, go to [Operating systems and browsers supported by Microsoft Intune](../fundamentals/supported-devices-browsers.md)

Applies to:

- Microsoft Intune (AOSP)  

### App management

#### Trusted Root Certificates Management for Intune App SDK for Android<!-- 15135752 -->
If your Android application requires SSL/TLS certificates issued by an on-premises or private certificate authority to provide secure access to internal websites and applications, the Intune App SDK for Android now has support for certificate trust management. For more information and examples, see [Trusted Root Certificates Management](../developer/app-sdk-android-phase7.md#trusted-root-certificates-management).

#### System context support for UWP apps<!-- 16544103 -->
In addition to user context, you can deploy Universal Windows Platform (UWP) apps from the **Microsoft Store app (new)** in system context. If a provisioned *.appx* app is deployed in system context, the app auto-installs for each user that logs in. If an individual end user uninstalls the user context app, the app still shows as installed because it's still provisioned. In addition, the app must not already be installed for any users on the device. Our general recommendation is to not mix install contexts when deploying apps. Win32 apps from the **Microsoft Store app (new)** already support system context.

## Week of March 6, 2023  

### App management

#### Deploy Win32 apps to device groups<!-- 7359954 -->
You can now deploy Win32 apps with **Available** intent to device groups. For more information, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md). 

### Device management  

#### New URL for Microsoft Intune admin center<!-- 17441426 -->  
The Microsoft Intune admin center has a new URL: [https://intune.microsoft.com](https://intune.microsoft.com). The previously used URL, [https://endpoint.microsoft.com](https://endpoint.microsoft.com), continues to work but will redirect to the new URL in late 2023. We recommend taking the following actions to avoid issues with Intune access and automated scripts: 

* Update login or automation to point to `https://intune.microsoft.com`. 
* Update your firewalls, as needed, to allow access to the new URL. 
* Add the new URL to your favorites and bookmarks. 
* Notify your helpdesk and update IT administrator documentation.  

### Tenant administration

#### Add CMPivot queries to Favorites folder<!-- 16702226 -->
You can add your frequently used queries to a **Favorites** folder in CMPivot. CMPivot allows you to quickly assess the state of a device managed by Configuration Manager via Tenant Attach and take action. The functionality is similar to one already present in the Configuration Manager console. This addition helps you keep all your most used queries in one place. You can also add tags to your queries to help search and find queries. The queries saved in the Configuration Manager console aren't automatically added to your **Favorites** folder. You need to create new queries and add them to this folder. For more information about CMPivot, see [Tenant attach: CMPivot usage overview](../../configmgr/tenant-attach/cmpivot-start.md).

### Device enrollment

#### New Microsoft Store apps now supported with the Enrollment Status Page<!-- 16280325 -->
The Enrollment Status Page (ESP) now supports the new Microsoft store applications during Windows Autopilot. This update enables better support for the new Microsoft Store experience and should be rolling out to all tenants starting with Intune 2303. For related information, see [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).

## Week of February 27, 2023

### Device configuration

#### Support for Locate device on Android Enterprise corporate owned fully managed and Android Enterprise corporate owned work profile devices<!--12391424 -->

You can now use "Locate device" on Android Enterprise corporate owned fully managed and Android Enterprise corporate owned work profile devices. With this feature, admins are able to locate lost or stolen corporate devices on-demand.

In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you need to turn the feature on using **Device Restrictions** in **Device Configuration** for Android Enterprise.

Select **Allow** on the **Locate device** toggle for fully managed and corporate owned work profile devices and select applicable groups. **Locate device** is available when you select **Devices**, and then select **All devices**. From the list of devices you manage, select a supported device, and choose the **Locate device** remote action.

For information on locating lost or stolen devices with Intune, go to:

- [Locate lost or stolen devices with Intune](../remote-actions/device-locate.md)

Applies to:

- Android Enterprise corporate owned fully managed
- Android Enterprise corporate owned dedicated devices
- Android Enterprise corporate owned work profile

#### Intune add-ons <!-- 13817801 -->

Microsoft Intune Suite provides mission-critical advanced endpoint management and security capabilities into Microsoft Intune. 

You can find add-ons to Intune in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) under **Tenant administration** > **Intune add-ons**.

For detailed information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

#### View ServiceNow Incidents in the Intune Troubleshooting workspace (Preview)<!-- 12508062 -->

In public preview, you can view a list of ServiceNow incidents associated with the user you've selected in the Intune Troubleshooting workspace. This new feature is available under **Troubleshooting + Support** > select a user > **ServiceNow Incidents**. The list of incidents shown have a direct link back to the source incident and show key information from the incident. All incidents listed link the "Caller" identified in the incident with the user selected for Troubleshooting.

For more information, go to [Use the troubleshooting portal to help users at your company](service-now-integration.md).

### Device security

#### Microsoft Tunnel for MAM is now generally available<!-- 16883728  -->

Now out of preview and generally available, you can add [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-overview.md) to your tenant. Tunnel for MAM supports connections from unenrolled [Android](../protect/microsoft-tunnel-mam-android.md) and [iOS](../protect/microsoft-tunnel-mam-ios.md) devices. This solution provides your tenant with a lightweight VPN solution that allows mobile devices access to corporate resources while adhering to your security policies.

In addition, MAM Tunnel for iOS now supports Microsoft Edge.

Previously, Tunnel for MAM for Android and iOS was in public preview and free for use. With this release as generally available, this solution now requires an add-on license for its use.

For licensing details, see [Intune add-ons](../fundamentals/intune-add-ons.md).

Applies to:  
- Android
- iOS  

### Tenant administration  

#### Organizational messages now support custom destination URLs <!-- 16576068  -->

You can now add any custom destination URL to organizational messages in the taskbar, notifications area, and Get Started app. This feature applies to Windows 11. Messages created with Azure AD-registered domains that are in a scheduled or active state are still supported. For more information, see [Create organizational messages](../remote-actions/organizational-messages-create.md?tabs=taskbar#step-1-create-a-message). 

## Week of February 20, 2023 (Service release 2302)

### App management

#### Latest iOS/iPadOS version available as minimum OS requirement for LOB and store apps<!-- 16433620  -->  
You can specify iOS/iPadOS 16.0 as the minimum operating system for line-of-business and store app deployments. This setting option is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** > *iOS store app or Line-of-business app*. For more information about managing apps, see [Add apps to Microsoft Intune](../apps/apps-add.md).

#### Newly available protected app for Intune<!-- 16655639  -->  
The following protected app is now available for Microsoft Intune:

- Egnyte for Intune by Egnyte

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Device configuration

#### Endpoint Manager admin center is renamed to Intune admin center<!-- 15560662   -->  
The Microsoft Endpoint Manager admin center is now called the **Microsoft Intune admin center**.

#### A new Associated Assignments tab for your filters<!-- 7538503  -->  
When you assign an app or policy, you can filter the assignment using different device properties, such as device manufacturer, model, and ownership. You can create and associate a filter with the assignment.

After you create a filter, there's a new **Associated Assignments tab**. This tab shows all the policy assignments, the groups that receive the filter assignments, and if the filter is using **Exclude** or **Include**:

1. Sign in to the Microsoft Intune admin center.
2. Go to **Devices** > **Filters** > Select an existing filter > **Associated Assignments tab**.
 
For more information on filters, go to:

- [Use filters when assigning your apps, policies, and profiles in Intune](filters.md)
- [Device properties, operators, and rule editing when creating filters in Intune](filters-device-properties.md)

#### Size and generation included in iOS/iPadOS model information<!-- 16406692  -->  
You can view the size and generation for enrolled iOS/iPadOS devices as part of the **Model** attribute in **Hardware device details**.

Go to **Devices > All devices** > select one of your listed devices and select **Hardware** to open its details. For example, iPad Pro 11 inch (3rd generation) displays for the device model instead of iPad Pro 3. For more information, go to: [See device details in Intune](../remote-actions/device-inventory.md#hardware-device-details)

Applies to:  
- **iOS/iPadOS**

#### Disable Activation Lock device action for supervised iOS/iPadOS devices<!-- 15571509 -->  
You can use the **Disable Activation Lock** device action in Intune to bypass Activation Lock on iOS/iPadOS devices without requiring the current username or password.

This new action is available under  **Devices > iOS/iPadOS >** *select one of your listed devices* **> Disable Activation Lock**.

More information on managing Activation Lock is available at [Bypass iOS/iPadOS Activation Lock with Intune](../remote-actions/device-activation-lock-disable.md) or on Apple's website at [Activation Lock for iPhone, iPad, and iPod touch - Apple Support.](https://support.apple.com/en-us/HT201365)

Applies to:  
- **iOS/iPadOS**

#### Allow Temporary Enterprise Feature Control is available in the Settings Catalog<!-- 15752120  -->  
In on-premises group policy, there's an **Enable features introduced via servicing that are off by default** setting.

In Intune, this setting is known as **Allow Temporary Enterprise Feature Control** and is available in the Settings Catalog. This servicing adds features that off by default. When set to **Allowed**, these features are enabled and turned on.

For more information on this feature, go to:

- [AllowTemporaryEnterpriseFeatureControl](/windows/client-management/mdm/policy-csp-Update#allowtemporaryenterprisefeaturecontrol) policy CSP
- [Blog: Commercial control for continuous innovation](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/commercial-control-for-continuous-innovation/ba-p/3737575)

The Windows features that enabled by this policy setting will be released later in 2023. Intune is releasing this policy setting now for your awareness and preparation, which is before any need to use the setting with future Windows 11 releases.

For more information on the settings catalog, go to [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md).

Applies to:

- Windows 11

### Device management

#### Device Control support for Printer Protection (Preview)<!-- 12355154  -->  
In public preview, Device Control profiles for Attack Surface Reduction policy now support [reusable settings groups for Printer Protection](../protect/reusable-settings-groups.md#add-reusable-groups-to-a-device-control-profile).

Microsoft Defender for Endpoint Device Control [Printer Protection](/microsoft-365/security/defender-endpoint/printer-protection-overview) enables you to audit, allow, or prevent printer with or without exclusions within Intune. It allows you to block users from printing via a non-corporate network printer or non-approved USB printer. This feature adds another layer of security and data protection for work from home and remote work scenarios.

Applies to:  
- Windows 10
- Windows 11

#### Support to delete stale devices that are managed through Security Management for Microsoft Defender for Endpoint<!--14729617  -->   
You can now **Delete** a device that's managed through the [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md) solution from within the Microsoft Intune admin center. The delete option appears along with other device management options when you view the device's Overview details. To locate a device managed by this solution, in the admin center go to **Devices** > **All devices**, and then select a device that displays either *MDEJoined* or *MDEManaged* in the *Managed by* column.

#### New settings and setting options available in the Apple Settings Catalog<!-- 16813380  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

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

### Device security
 
#### Use Endpoint security Antivirus policy to manage Microsoft Defender update behavior (Preview)<!-- 11890335 -->  
As part of a public preview for Endpoint security [Antivirus policy](../protect/endpoint-security-antivirus-policy.md), you can use the new profile **Defender Update controls** for the *Windows 10 and later* platform to manage update settings for Microsoft Defender. The new profile includes settings for the rollout release channel by which devices and users receive Defender Updates that are related to daily security intelligence updates, monthly platform updates, and monthly engine updates.

This profile includes the following settings, which are all directly taken from [Defender CSP - Windows Client Management](/windows/client-management/mdm/policy-csp-Defender).

- Engine Updates Channel
- Platform Updates Channel
- Security Intelligence Updates Channel

These settings are also available from the [settings catalog](../configuration/settings-catalog.md) for the *Windows 10 and later* profile.

Applies to:  
- Windows 10
- Windows 11

## Week of February 6, 2023

### Tenant administration

#### Apply recommendations and insights to enrich the Configuration Manager site health and device management experience<!--16957774 -->

You can now use the Microsoft Intune admin center to view recommendations and insights for your Configuration Manager sites. These recommendations can help you improve the site health and infrastructure and enrich the device management experience.

Recommendations include:  

- How to simplify your infrastructure
- Enhance device management
- Provide device insights
- Improve the health of the site

To view recommendations, open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Connectors and tokens** > **Microsoft Endpoint Configuration Manager**,  and select a *site* to view recommendations for that site.  Once selected, the *Recommendations* tab displays each insight along with a *Learn more* link. This link opens details on how to apply that recommendation.

For more information, see [Enable Microsoft Intune tenant attach - Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md).

## Week of January 30, 2023

### Device management

#### HTC Vive Focus 3 supported on Microsoft Intune for Android Open Source Devices<!--15670082--> 

Microsoft Intune for Android open source project devices (AOSP) now supports HTC Vive Focus 3. 

For more information, go to [Operating systems and browsers supported by Microsoft Intune](../fundamentals/supported-devices-browsers.md)

Applies to:

- Microsoft Intune (AOSP)
#### Introducing support for laser pointers in Remote Help<!-- 16108312 -->

In Remote Help, you can now use a laser pointer when you're providing assistance on Windows.

For more information on Remote Help, go to [Remote Help](/mem/intune/fundamentals/remote-help).

Applies to:

 - Windows 10/11
## Week of January 23, 2023 (Service release 2301)

### App management

#### Configure whether to show Configuration Manager apps in Windows Company Portal<!-- 9135109 -->
In Intune, you can choose whether to show or hide Configuration Manager apps from appearing in the Windows Company Portal. This option is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Customization**. Next to **Settings**, select **Edit**. The option to **Show** or **Hide** the Configuration Manager applications are located in the **App Sources** section of the pane. For related information about configuring the Company Portal app, see [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

#### Block pinning web pages to Managed Home Screen app<!-- 15593458 -->
On Android Enterprise dedicated devices using Managed Home Screen, you can now use app configuration to configure the Managed Home Screen app to block pinning browser web pages to Managed Home Screen. The new `key` value is `block_pinning_browser_web_pages_to_MHS`. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

### Device management

#### Grace period status visible in Microsoft Intune app for Android<!-- 13498225 -->  
The Microsoft Intune app for Android now shows a grace period status to account for devices that don't meet compliance requirements but are still within their given grace period. Users can see the date by which devices must be compliant, and the instructions for how to become compliant. If they don't update their device by the given date, the device is marked as noncompliant. For more information, see the following docs:  
- [Configure compliance policies with actions for noncompliance](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance)    
- [Check compliance status](../user-help/check-compliance-microsoft-intune-app-android.md)  


#### Software update policies for macOS are now generally available<!-- 12393100 -->   
Software update policies for macOS devices are now generally available. This general availability applies to supervised devices running macOS 12 (Monterey) and later. We will continue to add improvements to this feature going forward.  

For more information, see [Use Microsoft Intune policies to manage macOS software updates](../protect/software-updates-macos.md).

#### Windows Autopilot device diagnostics<!-- 16697347 -->
Windows Autopilot diagnostics is available to download in Microsoft Intune admin center from either in the Autopilot deployments monitor or Device Diagnostics monitor for an individual device.

### Device enrollment

#### Enrollment notifications now generally available<!-- 16545401 -->
Enrollment notifications are now generally available, and are supported on Windows, Apple, and Android devices. This feature is only supported with user-driven enrollment methods. For more information, see [Set up enrollment notifications](../enrollment/enrollment-notifications.md).  

#### Skip or show Terms of Address pane in Setup Assistant<!-- 14661838 -->  
Configure Microsoft Intune to skip or show a new Setup Assistant pane called **Terms of Address** during Apple Automated Device Enrollment. The Terms of Address pane lets users on iOS/iPadOS and macOS devices personalize their device by selecting how the system addresses them: feminine, neutral, or masculine.  The pane is visible during enrollment by default, and is available for select languages.  You can hide it on devices running iOS/iPadOS 16 and later, and macOS 13 and later. For more information about the Setup Assistant screens supported in Intune, see:  

- [Setup Assistant screens for Macs](../enrollment/device-enrollment-program-enroll-macos.md#setup-assistant-screen-reference)
- [Setup Assistant screens for iOS/iPadOS](../enrollment/device-enrollment-program-enroll-ios.md#setup-assistant-screen-reference)

### Device security

#### Microsoft Tunnel for Mobile Application Management for iOS/iPadOS (Preview)<!-- 15769204, 9851288 -->  

As a public preview, you can use the Mobile Application Management (MAM) to the Microsoft Tunnel VPN gateway for iOS/iPadOS. With this preview for iOS devices that haven't enrolled with Intune, supported apps on those unenrolled devices can use Microsoft Tunnel to connect to your organization when working with corporate data and resources. This feature includes VPN gateway support for:

- Secure access to on-premises apps and resources using modern authentication
- Single Sign On and conditional access

For more information, go to:

- [Microsoft Tunnel for Mobile Application Management for iOS/iPadOS admin guide (public preview)](../protect/microsoft-tunnel-mam-ios.md)
- [Microsoft Tunnel for MAM iOS SDK developer guide](../developer/tunnel-mam-ios-sdk.md)

Applies to:

- iOS/iPadOS

####  Attack surface reduction policy support for Security settings management for Microsoft Defender for Endpoint <!-- 13816760 -->  
Attack surface reduction policy is supported by devices managed through the [MDE Security configuration](../protect/mde-security-integration.md#which-solution-should-i-use) scenario. To use this policy with devices that use Microsoft Defender for Endpoint but aren't enrolled with Intune:

1. In the Endpoint Security node, create a new *Attack surface reduction* policy.
2. Select **Windows 10, Windows 11, and Windows Server** as the *Platform*.
3. Select **Attack Surface Reduction Rules** for the *Profile*.  

Applies to:  
- Windows 10
- Windows 11

#### SentinelOne – New mobile threat defense partner<!-- 13911932 -->
You can now use [SentinelOne](../protect/sentinelone-mobile-threat-defense-connector.md) as an integrated Mobile Threat Defense (MTD) partner with Intune. By configuring the SentinelOne connector in Intune, you can control mobile device access to corporate resources using conditional access that's based on risk assessment in your compliance policy. The SentinelOne connector can also send risk levels to app protection policies.

### Device configuration

#### Device Firmware Configuration Interface (DFCI) supports Fujitsu devices<!--10249866 -->

For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type).

Some Fujitsu devices running Windows 10/11 are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

For more information about DFCI profiles, go to:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](../../autopilot/dfci-management.md)

Applies to:

- Windows 10
- Windows 11

#### Support for Bulk Device Actions on devices running Android AOSP<!--15397458 -->
You can now complete "Bulk Device Actions" for devices running Android AOSP. The bulk device actions supported on devices running AOSP are Delete, Wipe and Restart.

Applies to:  
- AOSP

#### Updated descriptions for iOS/iPadOS and macOS settings in the settings catalog<!-- 16360170 -->
The settings catalog lists all the settings you can configure, and all in one place. For the iOS/iPadOS and macOS settings, for each setting category, the descriptions are updated to include more detailed information.

For more information on the settings catalog, go to:
- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md)
- [Common tasks you can complete using the Settings Catalog in Intune](../configuration/settings-catalog-common-features.md)

Applies to:
- iOS/iPadOS
- macOS

#### New settings available in the Apple Settings Catalog<!--16237513  -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

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


#### Filter app and policy assignments by the device's Azure AD Join type (`deviceTrustType`)<!-- 8110331 -->
When you assign an app or policy, you can filter the assignment using different device properties, such as device manufacturer, operating system SKU, and more.

A new device filter property `deviceTrustType` is available for Windows 10 and later devices. With this property, you can filter app and policy assignments depending on the Azure AD Join type, with values of "Azure AD Joined", "Hybrid Azure AD Joined", and "Azure AD registered".

For more information on filters and the device properties you can use, go to:
- [Use filters when assigning your apps, policies, and profiles in Intune](filters.md)
- [Device properties, operators, and rule editing when creating filters in Intune](filters-device-properties.md)

Applies to:

- Windows 10 and later

### Monitor and troubleshoot

#### Download mobile app diagnostics in the Microsoft Intune admin center (public preview)<!-- 9353471 -->  
Now in public preview, access user-submitted mobile app diagnostics in the admin center, including app logs sent through Company Portal app for Android, AOSP, or Windows, with support for iOS, macOS, and Microsoft Edge for iOS coming at a later date. For more information about accessing mobile app diagnostics for Company Portal, see [Configure Company Portal](../apps/company-portal-app.md#app-logs).

#### WinGet troubleshooting using diagnostic files<!-- 16724699 -->
[WinGet](/windows/package-manager/winget/) is a command line tool that enables you to discover, install, upgrade, remove, and configure applications on Windows 10 and Windows 11 devices. When working with [Win32 app management in Intune](../apps/apps-win32-app-management.md), you can now use the following file locations to help troubleshoot WinGet:
- *%TEMP%\winget\defaultstate\*.log*
- *Microsoft-Windows-AppXDeployment/Operational*
- *Microsoft-Windows-AppXDeploymentServer/Operational*

#### Intune troubleshooting pane update<!-- 4442647 -->  
A new experience for the Intune Troubleshooting pane provides details about user's devices, policies, applications, and status. The troubleshooting pane includes the following information:

- A summary of policy, compliance, and application deployment status.
- Support for exporting, filtering, and sorting all reports.
- Support to filter by excluding policies and applications.
- Support to filter to a user's single device.
- Details about available device diagnostics and disabled devices.
- Details about offline devices that haven't checked-in to the service for three or more days.

You can find the troubleshooting pane in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Troubleshoot**. To view the new experience during preview, select **Preview upcoming changes to Troubleshooting and provide feedback** to display the **Troubleshooting preview** pane, then select **Try it now**.

#### New report for devices without compliance policy (preview)<!--14911124 --> 
We've added a new report named **Devices without compliance policy** to the Device compliance reports you can access through the *Reports* node of the Microsoft Intune admin center.  This report, which is in preview, uses a  newer reporting format that provides for more capabilities.

To learn about this new organizational report, see [Devices without compliance policy (Organizational)](../fundamentals/reports.md#devices-without-compliance-policy-organizational).

An older version of this report remains available through the *Devices > Monitor* page of the admin center. Eventually, that older report version will be retired, though it remains available for now.  

#### Service health messages for tenant issues that require administrative attention<!-- 14791676 -->  
The *Service health and message center page* in the Microsoft Intune admin center can now display messages for **Issues in your environment that require action**. These messages are important communications that are sent to a tenant to alert administrators about issues in their environment that might require action to resolve. 

You can view messages for *Issues in your environment that require action* in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by going to **Tenant administration** > **Tenant status** and then selecting the **Service health and message center** tab.

For more information about this page of the admin center, see [View details about your Tenant on the Intune tenant status page](../fundamentals/tenant-status.md).

### Tenant administration

#### Improved UI experience for multiple certificate connectors<!-- 16263248 -->
We've added pagination controls to the *Certificate connectors* view to help improve the experience when you have more than 25 certificate connectors configured. With the new controls, you can see the total number of connector records and easily navigate to a specific page when viewing your certificate connectors.

To view certificate connectors, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Tenant administration** > **Connectors and tokens** > **Certificate connectors**.

### Intune apps

#### Newly available protected app for Intune<!-- 16620158 -->
The following protected app is now available for Microsoft Intune:
- Voltage SecureMail by Voltage Security

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Scripts

#### Preview PowerShell script package content in Endpoint Analytics<!-- 12930245 -->
Admins can now see a preview of a PowerShell script's content for proactive remediations. The content is displayed in a grayed-out box with scrolling capability. Admins can't edit the content of the script in the preview. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports** > **Endpoint analytics** > **Proactive remediations**. For related information, see [PowerShell scripts for Proactive remediations](../../analytics/powershell-scripts.md).

## Week of January 16, 2023

### App management

#### Win32 app supersedence GA<!-- 9318154 -->
We have rolled out the feature set for Win32 app supersedence GA, which adds support for apps with supersedence during ESP and also allows supersedence and dependency relationships to be added in the same app subgraph. For more information, see [Win32 app supersedence improvements](https://aka.ms/Intune/Win32-Supersedence). For information about Win32 app supersedence, see [Add Win32 app supersedence](../apps/apps-win32-supersedence.md).

## Week of January 9, 2023

### Device configuration

#### The Company Portal app enforces Password Complexity setting on Android Enterprise 12+ personally owned devices with a work profile<!-- 16211313  -->  

On Android Enterprise 12+ personally owned devices with a work profile, you can create a compliance policy and/or device configuration profile that sets the password complexity. Starting with the 2211 release, this setting is available in the Intune admin center:

- **Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > Personally owned with a work profile
- **Devices** > **Compliance policies** > **Create policy** > **Android Enterprise** for platform > Personally owned with a work profile

The Company Portal app enforces the **Password complexity** setting.

For more information on this setting and the other settings you can configure on personally owned devices with a work profile, go to:

- [Device compliance settings for Android Enterprise in Intune](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile)
- [Device restriction settings list for Android Enterprise in Intune](../configuration/device-restrictions-android-enterprise-personal.md)

Applies to:

- Android Enterprise 12+ personally owned devices with a work profile

## Week of December 19, 2022

### Intune apps

#### Newly available protected app for Intune<!-- 15448654 -->
The following protected app is now available for Microsoft Intune:
- Appian for Intune by Appian Corporation (Android)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of December 12, 2022 (Service release 2212)

### Device configuration

#### Remote Help client app includes a new option to disable chat functionality in the Tenant level setting<!-- 14685052 -->  
In the Remote Help app, admins can disable chat functionality from the new tenant level setting. Turning on the disable chat feature removes the chat button in the Remote Help app. This setting can be found in the Remote Help **Settings** tab under **Tenant Administration** in Microsoft Intune.

For more information, see [Configure Remote Help for your tenant](/mem/intune/fundamentals/remote-help#configure-remote-help-for-your-tenant).

**Applies to**: Windows 10/11

#### New settings available in the macOS Settings Catalog<!-- 16069006 -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**File Vault > File Vault Options**:

- Block FV From Being Disabled
- Block FV From Being Enabled

**Restrictions**:

- Allow Bluetooth Modification

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### There are default settings for SSO extension requests on iOS, iPadOS, and macOS devices<!-- 15082414-15084030 -->  

When you create a single sign-on app extension configuration profile, there are some settings you configure. The following settings use the following default values for all SSO extension requests:

- **AppPrefixAllowList** key
  - macOS default value: `com.microsoft.,com.apple.`
  - iOS/iPadOS default value: `com.apple.`

- **browser_sso_interaction_enabled** key
  - macOS default value: `1`
  - iOS/iPadOS default value: `1`

- **disable_explicit_app_prompt** key
  - macOS default value: `1`
  - iOS/iPadOS default value: `1`

If you configure a value other than the default value, then the configured value overwrites the default value. 

For example, you don't configure the `AppPrefixAllowList` key. By default, all Microsoft apps (`com.microsoft.`) and all Apple apps (`com.apple.`) are enabled for SSO on macOS devices. You can overwrite this behavior by adding a different prefix to the list, such as `com.contoso.`.

For more information on the Enterprise SSO plug-in, go to [Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS and macOS devices in Microsoft Intune](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)

Applies to:

- iOS/iPadOS
- macOS

### Device enrollment

#### Enrollment token lifetime increases to 65 years for Android Enterprise dedicated devices<!-- 15094454  -->  
Now you can create an enrollment profile for Android Enterprise dedicated devices that's valid for up to 65 years.  If you have an existing profile, the enrollment token still expires at whatever date you chose when you created the profile, but during renewal you can extend the lifetime. For more information about creating an enrollment profile, see [Set up Intune enrollment for Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md#create-an-enrollment-profile).

### Device management

#### Update policies for macOS now available for all supervised devices<!-- 16141990  -->  
Software update policies for macOS devices now apply to all macOS supervised devices. Previously, only those devices that enrolled through Automated Device Enrollment (ADE) would qualify to receive updates. For more information on configuring update policies for macOS, see [Use Microsoft Intune policies to manage macOS software updates](../protect/software-updates-macos.md).

Applies to:  
- macOS

#### Policy and reports for Windows feature updates and expedited quality updates are now Generally Available<!-- 15738456 -->  
Both the policies and reports for managing feature updates and quality updates (expedited updates) for Windows 10 and later, are out of preview and now generally available.

For more information about these policies and reports, see:

- [Feature updates policy](../protect/windows-10-feature-updates.md)
- [Expedite quality updates policy](../protect/windows-10-expedite-updates.md)
- [Windows Update compliance reports](../protect/windows-update-reports.md)

Applies to:  
-  Windows 10/11

## Week of November 28, 2022

### App management

#### Microsoft Store apps in Intune<!-- 12708346 -->  
You can now search, browse, configure, and deploy Microsoft Store apps within Intune. The new Microsoft Store app type is implemented using the Windows Package Manager. This app type features an expanded catalog of apps, which includes both UWP apps and Win32 apps. Roll out of this feature is expected to complete by December 2, 2022.  For more information, see [Add Microsoft Store apps to Microsoft Intune](../apps/store-apps-microsoft.md).

### Tenant administration

#### Access policies for multiple Administrator Approval (public preview)<!-- 9348867  -->
In public preview, you can use Intune *access policies* to require that a second Administrator Approval account be used to approve a change before the change is applied. This capability is known as multiple Administrator Approval (MAA).

You create an access policy to protect a type of resource, like App deployments. Each access policy also includes a group of users who are *approvers* for the changes protected by the policy. When a resource like an app deployment configuration is protected by an access policy, any changes that are made to the deployment, including creating, deleting, or modifying an existing deployment won't apply until a member of the approvers group for that access policy reviews and approves that change.

Approvers can also reject requests. The individual requesting a change and the approver can provide notes about the change, or why it was approved or rejected.

Access policies are supported for the following resources:

- **Apps** – Applies to [app deployments](../apps/apps-add.md), but doesn't apply to app protection policies.
- **Scripts** – Applies to deploying scripts to devices that run [macOS](../apps/macos-shell-scripts.md) or [Windows](../apps/intune-management-extension.md).

For more information, see [Use Access policies to require multiple administrative approval](../fundamentals/multi-admin-approval.md).  

### Device security

#### Microsoft Tunnel for Mobile Application Management for Android (Preview)<!-- 15769204 -->  
As a public preview, you can now use Microsoft Tunnel with unenrolled devices. This capability is called [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-mam.md) (MAM). This preview supports Android, and without any changes to your existing Tunnel infrastructure, supports the Tunnel VPN gateway for:

- Secure access to on-premises apps and resources using modern authentication
- Single Sign On and conditional access

To use Tunnel MAM, unenrolled devices must install Microsoft Edge, Microsoft Defender for Endpoint, and the Company Portal. You can then use the Microsoft Intune admin center to configure the following profiles for the unenrolled devices:

- An App configuration profile for managed apps, to configure Microsoft Defender on devices for use as the Tunnel client app.
- A second App configuration profile for managed apps, to configure Microsoft Edge to connect to Tunnel.
- An App protection profile to enable automatic start of the Microsoft Tunnel connection.

Applies to:  
- Android Enterprise

## What's new archive
<!-- Past announcements that are older than six months will be moved to the archive -->

For previous months, see the [What's new archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
