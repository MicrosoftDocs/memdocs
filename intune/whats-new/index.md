---
title: What's new in Microsoft Intune
description: Find out what's new in Microsoft Intune.
ms.date: 05/01/2026
ms.topic: whats-new
ms.reviewer: intuner
ms.collection:
- M365-identity-device-management
---

# What's new in Microsoft Intune

Learn what's new each week in Microsoft Intune.

You can also read:

- [**Important notices**](#notices)
- [Past releases](archive/index.md) in the What's new archive
- Information about [how Intune service updates are released](../fundamentals/servicing-information.md)

> [!NOTE]
> Each [monthly update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) can take up to three days to roll out and is in the following order:
>
> - Day 1: Asia Pacific (APAC)
> - Day 2: Europe, Middle East, Africa (EMEA)
> - Day 3: North America
> - Day 4+: Intune for Government
>
> Some features roll out over several weeks and might not be available to all customers in the first week.
>
> For a list of upcoming Intune feature releases, see [In development for Microsoft Intune](./in-development.md).
>
> For new information about Windows Autopilot solutions, see:
>
> - [Windows Autopilot device preparation: What's new](/autopilot/device-preparation/whats-new)
> - [Windows Autopilot: What's new](/autopilot/whats-new)

You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../fundamentals/use-docs.md#notifications).
<!-- **RSS feed**: Get notified when this page is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us` -->

<!-- Common categories - in this order:

### Microsoft Intune Suite
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
### Scripts
### Tenant administration

-->
## Week of April 27, 2026 (Service release 2604)

### Microsoft Intune Suite

#### Expanded support for Endpoint Privilege Management support approved elevation requests<!-- 33479618 -->

Intune's Endpoint Privilege Management (EPM) now supports [support approved elevation requests](../epm/manage-support-approvals.md) from all users of a device. This update expands the utility of support approved file elevations and helps to improve scenarios that involve shared devices.

Previously, file elevation requests that require support approval were supported from only a device's primary user or the user who enrolled the device.

For more information about this type of elevation request, see [Support approved file elevations for Endpoint Privilege Management](../epm/manage-support-approvals.md).

### Device configuration

#### Configure credential manager permissions for Android Enterprise devices<!-- 31358911 -->

You can now control which applications act as system-level credential providers on managed Android Enterprise devices running Android 14 and higher. Credential providers are responsible for password autofill and passkey storage.

To configure credential manager permissions, go to **Apps** > **Android** > **Configuration** > **Managed Devices** and choose **Android Enterprise** as the platform type.

By default, Android blocks third-party credential providers on managed devices. This configuration setting lets you:

- Allow specific apps (such as Microsoft Authenticator or a third-party password manager) to act as credential providers
- Enable passkey-based sign-in across managed Android Enterprise devices
- Maintain control over which credential sources are trusted on corporate devices

A known limitation is that Google Password Manager can't act as a credential provider on corporate-owned work profile or personally owned work profile devices. It is blocked on the end user's device. Use a different credential app as a workaround.

For more information, see [Add app configuration policies for managed Android Enterprise devices](../app-management/configuration/configure-managed-android.md).

> [!div class="checklist"]
> Applies to:
>
> - Android fully managed devices (COBO)
> - Android dedicated devices (COSU)
> - Android corporate-owned devices with a work profile (COPE)
> - Android personally owned devices with a work profile (BYOD) using Android Management API (AM API)

#### Block location setting for Android Enterprise can keep Location services enabled<!-- 36703827 -->

On Android Enterprise devices, you can use the **General > Block location** in the [settings catalog](../device-configuration/settings-catalog/ref-android-settings.md) to disable the location services on the device and prevent users from turning it on.

This setting is now called **Location** and has three options you can configure:

- Device default - Intune doesn't change or update this setting. By default, the OS allows end users to turn location services on or off.
- Location enabled - Requires location services to be on and prevents end users from turning them off.
- Location disabled - Requires location services to be off and prevents end users from turning them on.

For a list of all the settings you can configure, see [Android Intune settings catalog settings list](../device-configuration/settings-catalog/ref-android-settings.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned devices with a work profile (COPE) running Android 10 and earlier
> - Android Enterprise corporate owned fully managed (COBO)
> - Android Enterprise corporate owned dedicated devices (COSU)

### Device enrollment

#### Access management for Apple services<!-- 31209876 -->

You can now use Apple access management settings in Apple Business Manager and Apple School Manager to configure service access for Apple accounts on organization-owned devices. These controls let you choose what devices users can sign in to and which apps and services are available to them. For more information, see [Configure service access for Apple accounts](../device-enrollment/apple/setup-account-service-access.md).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

#### Microsoft Intune supports userless ADE for visionOS and tvOS devices<!-- 29219451 -->

Microsoft Intune has added support for userless Apple automated device enrollment (ADE) for visionOS and tvOS devices, enabling you to enroll and manage Apple Vision Pro and Apple TV through Apple Business Manager or Apple School Manager. This capability supports ADE without user affinity and includes custom configuration uploads for settings, default enrollment restrictions, and device actions. The feature is available with Microsoft Intune Plan 2 as part of the Microsoft 365 Suite.

Enrolled visionOS and tvOS devices appear alongside iOS and iPadOS devices in the Intune admin center within **Apple mobile** and can be filtered. Support requires tvOS 26 and later or visionOS 26 and later. We recommend that you keep these devices up to date to receive the latest security fixes.

For more information, see:

- [Overview of Apple ADE for Apple mobile](../device-enrollment/apple/overview-automated-enrollment-apple.md)
- [Use the Intune settings catalog to configure settings](../device-configuration/settings-catalog/index.md)
- [Device actions](../device-management/actions/index.md)

> [!div class="checklist"]
> Applies to:
>
> - tvOS 26 and later
> - visionOS 26 and later

### Device management

#### Support for Ubuntu 26.04 LTS<!-- 36899679 -->

Microsoft Intune now supports Ubuntu 26.04 LTS. Support for Ubuntu 22.04 LTS ends in August 2026. Devices already enrolled on Ubuntu 22.04 remain enrolled, but you should notify users to upgrade to a supported Ubuntu version. You can identify devices running Ubuntu 22.04 in the Intune admin center by going to **Devices** > **All devices**, filtering by **Linux**, and adding the **OS version** column. For more information, see [Enroll Linux desktop devices in Microsoft Intune](../device-enrollment/guide-linux.md).

#### Preview the new device page in the Intune admin center (public preview)<!-- 16532161, 36646300 -->

In the Intune admin center, when you go to **Devices** > **All Devices** and select a device, you can see device-specific info, like device properties.

This page is redesigned and is available for you to preview. To enable the new experience:

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **All Devices**.
2. Move the **Preview new device view** toggle to **On**.

The new experience is only available when you go to **Devices** > **All Devices** and select a device. If you open a device page from a different part of the Intune admin center, like from a report, the original page view is shown, even with the toggle enabled.

When turned on, you see the new full page layout that gives you a single view of the device. Use this view to:

- Track device activity
- Access tools and reports
- Manage device information

The single device page has the following tabs:

- **Device action status**: Shows requested, in‑progress, and recently completed device actions. You can search, sort, and filter this list. You can quickly see what actions are running or have completed without leaving the device view.
- **Tools and reports**: This tab was previously called **Overview**. It shows monitoring reports, like compliance and device configuration status, tools, like remediations. These features were previously accessed in other parts of the Intune admin center.
- **Properties**: Contains admin‑modifiable device properties with visible scope tags and a dedicated editing view.
- **Device details**: This tab was previously called **Hardware**. It provides physical device information and key Intune and Microsoft Entra management details.

Other features:

- Device actions are grouped, ordered, and labeled consistently across platforms and device types, and only shows relevant and permitted actions. Destructive actions are separated and require confirmation, reducing unintentional actions.

- The updated layout uses a standard structure across device types and platforms, while adapting to platform‑specific capabilities.

- Improved labeling, hierarchy, and formatting make device information easier to scan and understand. The **Essentials** section elevates important device information and is accessible from any tab.

All existing device management capabilities remain available. This update focuses on making them easier to find and use.

#### New remote actions to suspend and restore Managed Home Screen on Android devices<!-- 10741483 -->

Intune has two new remote actions that allow admins to temporarily suspend and restore Managed Home Screen (MHS) on Android devices. These actions let users exit MHS and access the device's default launcher for a defined period, without removing policies or requiring a PIN.

When the specified duration expires, or when the *restore managed home screen action* is triggered, MHS automatically re-locks the device into the kiosk experience. This helps maintain security while reducing disruption during troubleshooting or short-term use outside of MHS.

To learn more, see:

- [Suspend Managed Home Screen](../device-management/actions/suspend-managed-home-screen.md)
- [Restore Managed Home Screen](../device-management/actions/restore-managed-home-screen.md)

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned Fully Managed (COBO)
> - Android Enterprise corporate-owned Dedicated (COSU)

#### Updated minimum version for Intune Management Extension on Windows<!-- 35502983 -->

Windows devices managed by Intune need to run Intune Management Extension version 1.58.103.0 or later. Devices on earlier versions no longer receive configurations or updates that depend on the Intune Management Extension, including Win32 app deployments, PowerShell scripts, remediations, and platform scripts.

The Intune Management Extension updates automatically, so most managed devices should already have a compatible version. Verify that your devices can sync with Intune to receive updates.

> [!div class="checklist"]
> Applies to:
>
> - Windows 10/11

### Device security

#### Autopatch update risk visibility report<!-- 37672980 -->

The *Autopatch update risk visibility* report extends the *security update status* dashboard with granular insight into patch compliance and risk across your managed devices. It classifies devices as *Current*, *Exposed*, or *Critical* and highlights policies contributing to risk, so you can identify and remediate issues faster.

For more information, see [Protect your estate: Reassess your Windows update policies](https://aka.ms/ReassessProtect).

> [!div class="checklist"]
> Applies to:
>
> - Windows

#### Updated security baseline for Microsoft Edge v139<!-- 35894707 -->

Microsoft Edge version 139 security baseline is now available in Microsoft Intune. This baseline reflects current Microsoft security recommendations for the Microsoft Edge browser and is the latest available Edge security baseline in Intune.

The Edge v139 security baseline includes new settings, updated default values, and retired settings.

Existing security baseline profiles don't automatically update to the new version. To use this baseline, Intune admins can [create a new baseline profile](../device-security/security-baselines/configure-baselines.md#create-a-profile-for-a-security-baseline) or [update an existing profile to the latest version](../device-security/security-baselines/configure-baselines.md#update-a-baseline-profile-to-the-latest-version).

We recommend carefully reviewing the settings in the new baseline before moving from a previous baseline version, especially if existing profiles include customizations.

For a detailed breakdown of setting changes, see the blog post [Security baseline for Microsoft Edge version 139](https://techcommunity.microsoft.com/blog/microsoft-security-baselines/security-baseline-for-microsoft-edge-version-139/4441251).

To view the default configuration of settings in the updated baseline, see [Microsoft Edge security baseline settings reference](../device-security/security-baselines/ref-edge-settings.md?pivots=edge-v139).

### Intune apps

#### Direct Android line-of-business app management<!-- 25065436, 29267431 -->

You can now manage Android line-of-business (LOB) apps directly in Microsoft Intune without publishing them to Managed Google Play on Android Enterprise corporate-owned fully managed (COBO) and dedicated (COSU) devices.

With direct LOB app management, admins can upload APK files directly to Intune and deploy required apps to supported Android Enterprise enrollment types using a native Intune workflow.

Direct LOB app management enables you to:

- Deploy in-house LOB APKs to fully managed and dedicated devices without publishing them to Managed Google Play
- Manage the app lifecycle directly from Intune
- Create app configuration policies for directly deployed LOB apps, giving you the same configuration flexibility you have for Managed Google Play apps

For more information, see [Add an Android line-of-business app to Microsoft Intune](../app-management/deployment/add-lob-android.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

#### Newly available protected apps for Intune<!-- 36921208, 36933292 -->

The following protected apps are now available for Microsoft Intune:

- Harvey AI by Harvey AI Corporation (iOS)
- Continia Expense App by Continia Software A/S

For more information about protected apps, see [Microsoft Intune protected apps](../app-management/ref-protected-apps.md).

### Tenant administration

#### Change Review Agent suggestions available inline in Multi Admin Approval (public preview)<!-- 36876605 -->

The [Change Review Agent](../copilot/agents/change-review-agent.md) now provides risk-based recommendations directly in the Multi Admin Approval experience for Windows PowerShell scripts. On the *My requests* and *All requests* tabs, a new **Agent Response** column displays when a suggestion is available. You can then select the suggestion to open and complete the Change Review Agent's approval workflow for that request without leaving the Multi Admin Approval node.

Change Review Agent suggestions continue to be available in the agent's primary experience as well.

For more information, see [Change Review Agent suggestions in Multi Admin Approval](../fundamentals/role-based-access-control/multi-admin-approval.md#change-review-agent-suggestions-in-multi-admin-approval).

## Week of April 20, 2026  

### Device security  

#### New reporting considerations for compliance policies<!-- 37266708 -->

New guidance has been added to the Microsoft Intune compliance policy reporting documentation to help explain how device compliance results appear in Intune reports. This update clarifies expected reporting behavior related to device check-in timing and user association, helping you better interpret compliance policy reports. For more information, see [Known reporting behaviors](../device-security/compliance/monitor-policy.md#known-reporting-behaviors).  

### Monitor and troubleshoot

#### Intune Data Warehouse (beta) connector retirement in Power BI<!-- 37106409 -->

The Intune Data Warehouse (beta) connector v1 in Power BI is retired. If you use Power BI reports that rely on this connector, you need to transition to Intune connector v2 or the OData Feed connector before the transition completes. Power BI reports created after November 2025 already use connector v2, while reports created before that date may still use the beta connector and need updating. This change improves the long-term reliability and supportability of Intune data access.

**Customer impact**: This change does not introduce new user interface experiences. Customers who still rely on the Intune Data Warehouse (beta) connector in Power BI may be affected if they have not transitioned to supported alternatives. Customers already using supported and documented data access options do not experience disruption.

**Required customer action**: Review the published guidance and transition away from the Intune Data Warehouse (beta) connector in Power BI before the transition completes. Customers who do not take action lose access to data through the beta connector after it is retired.

**Timing and rollout**: Customer communications begin in late April 2026. The transition occurs gradually over two weeks starting April 20, 2026.

For more information, see [Use the Microsoft Intune Data Warehouse](../developer/data-warehouse/create-reports.md).

> [!div class="checklist"]
> Applies to:
>
> - Windows
> - iOS/iPadOS
> - macOS
> - Android

## Week of April 6, 2026 

### Device enrollment  

#### Support for Android XR devices<!-- 36123576 -->  

Microsoft Intune now supports management of Android XR devices using Android Enterprise dedicated and fully managed enrollment modes. You can enroll Android XR devices, deploy apps through managed Google Play, and apply core security and compliance policies. Android XR devices appear and are managed alongside other Android devices in the Intune admin center. For more information about supported scenarios and current limitations, see [Microsoft Intune announces Android Enterprise management support for Android XR](https://techcommunity.microsoft.com/blog/microsoftintuneblog/microsoft-intune-announces-android-enterprise-management-support-for-android-xr/4508499).  

### Tenant administration    

#### New TeamViewer connector experience in Microsoft Intune<!-- 35094013 -->

There is a new TeamViewer integration in Microsoft Intune that simplifies onboarding and improves reliability for remote assistance workflows. The new connector replaces the existing TeamViewer connector experience and provides a more streamlined experience in the Intune admin center. If you're using the previous TeamViewer connector, you must migrate to the new connector within 12 months to maintain functionality. For more information about the new connector, see [Use the TeamViewer integration in Microsoft Intune](../device-management/tools/setup-teamviewer.md).  

## Week of March 30, 2026 (Service release 2603)

### App management

#### Declarative Device Management for Apple line-of-business apps on iOS/iPadOS<!-- 30457044 -->

Microsoft Intune now supports Apple Declarative Device Management (DDM) for required line-of-business apps on devices running iOS/iPadOS 18 and later. By changing the management type to DDM in App information, you can deploy and configure apps using Apple's policy-based model, which improves delivery efficiency, provides real-time app status, and expands per-app options such as associated domains.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

### Device configuration

#### Recovery lock features available for macOS devices <!-- 28675745 32541429 -->

On macOS devices, you can configure a recovery OS password that prevents users from booting company-owned devices into recovery mode, reinstalling macOS, and bypassing remote management. Admins can also rotate this password.

There are two ways to use this feature:

- **Settings catalog policy** - In a [settings catalog](/intune/device-configuration/settings-catalog) policy, you can use the Recovery Lock settings to:

  - Turn on the recovery lock feature
  - Configure a password rotation schedule

- **Remote device action** - Use the [Recovery Lock device action](../device-management/actions/rotate-recovery-lock-passcode.md) to manually rotate the recovery lock password for a specific device.

The Recovery Lock password can be viewed in the per-setting status report > **Passwords and keys**. To view the Recovery Lock password, the signed-in administrator needs the **Remote tasks/View macOS recovery lock password** permission.

> [!div class="checklist"]
> Applies to:
>
> - macOS

> [!NOTE]
> This feature is gradually rolling out and may not yet be available in your tenant. Full availability is expected by late April 2026.

#### New supported OEMConfig app for Android Enterprise <!-- 36423115 -->

The following OEMConfig app is available in Intune for Android Enterprise:

- Inventus | `com.inventus.oemconfig.gen`

For more information about OEMConfig, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../device-configuration/templates/configure-oemconfig-android.md).

#### New settings in the Windows settings catalog <!-- 36922863 -->

There are new settings in the Windows settings catalog. To see and configure these settings in Intune, create a Windows settings catalog profile (**Devices > Configuration profiles > Create profile > Windows 10 and later > Settings catalog**).

The new policies include:

- **Connectivity > Disable Cross Device Resume**: This feature lets Windows suggest continuing an activity users start on a device, like a phone, to a PC. IT admins can use this policy to turn off this feature and prevent users from continuing tasks, like browsing files or continuing to use supported apps that require linking between a phone and PC. 

  When set to **CrossDeviceResume is Disabled**, the Windows device doesn't receive any CrossDeviceResume notification. Users won't see any "resume from your phone" prompts. When you select **CrossDeviceResume is Enabled**, the Windows device does receive notification to resume activity from linked devices. If you don't configure this policy setting, the default behavior is that the CrossDeviceResume feature is turned on, which means users see the notification. Changes to this policy take effect on reboot.

  This policy:

  - Is available to Windows Insiders.
  - Uses the [DisableCrossDeviceResume](/windows/client-management/mdm/policy-csp-Connectivity#disablecrossdeviceresume) CSP.

- **Windows AI > Remove Microsoft Copilot App**: This policy setting allows you to uninstall the Microsoft Copilot app from devices. It applies to devices and users that meet the following conditions:

  - The Microsoft 365 Copilot and Microsoft Copilot apps are both installed.
  - The Microsoft Copilot app was not installed by the user.
  - The Microsoft Copilot app was not opened in the last 14 days.

  If this policy is enabled, the Microsoft Copilot app is uninstalled. Users can still re-install if they choose to.

  [RemoveMicrosoftCopilotApp](/windows/client-management/mdm/policy-csp-WindowsAI#removemicrosoftcopilotapp) CSP

> [!div class="checklist"]
> Applies to:
>
> - Windows

To learn more about the settings catalog, see [Use the Intune settings catalog to configure settings](/intune/device-configuration/settings-catalog).

#### New updates to the Apple settings catalog <!-- 36630003 -->

The [Settings Catalog](/intune/device-configuration/settings-catalog) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](/intune/device-configuration/settings-catalog).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type. 

##### iOS/iPadOS

**Declarative Device Management (DDM) > External Intelligence Settings**:

- Allow Sign In
- Allowed Workspace IDs

**Declarative Device Management (DDM) > Intelligence Settings**:

- Allow Apple Intelligence Report
- Allow Genmoji
- Allow Image Playground
- Allow Image Wand
- Allow Personalized Handwriting Results
- Allow Visual Intelligence Summary
- Allow Writing Tools
- Mail > Allow Smart Replies
- Mail > Allow Summary
- Notes > Allow Transcription
- Notes > Allow Transcription Summary
- Safari > Allow Summary
- Force On Device Only Dictation
- Force On Device Only Translation

**Declarative Device Management (DDM) > Keyboard Settings**:

- Allow Definition Lookup
- Allow Auto Correction
- Allow Dictation
- Allow Predictive Text
- Allow Slide To Type
- Allow Spell Check
- Allow Text Replacement
- Allow Math Keyboard Suggestions

**Declarative Device Management (DDM) > Siri Settings**:

- Allow User Generated Content
- Allow While Locked
- Force Profanity Filter

##### macOS

**Declarative Device Management (DDM) > External Intelligence Settings**:

- Allow Sign In
- Allowed Workspace IDs

**Declarative Device Management (DDM) > Intelligence Settings**:

- Allow Apple Intelligence Report
- Allow Genmoji
- Allow Image Playground
- Allow Writing Tools
- Mail > Allow Smart Replies
- Mail > Allow Summary
- Notes > Allow Transcription
- Notes > Allow Transcription Summary
- Safari > Allow Summary
- Force On Device Only Dictation

**Declarative Device Management (DDM) > Keyboard Settings**:

- Allow Definition Lookup
- Allow Dictation
- Allow Math Keyboard Suggestions

**Declarative Device Management (DDM) > Siri Settings**:

- Force Profanity Filter

**System Configuration > File Provider**:

- Management Allows Remote Syncing
- Management Remote Syncing Allow List
- Management Allows External Volume Syncing
- Management External Volume Syncing Allow List
- Management Domain Auto Enablement List

**Restrictions**:

- Allow Rosetta Usage Awareness

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

### Device management  

#### Remote Help connectivity update for Windows devices<!-- 29252975 -->

We've improved connectivity when using the [Launch Remote Help](../remote-help/start-session.md#provide-help) capability in the Intune admin center for Windows devices. For the best experience, we recommend updating firewall rules to include this new endpoint:

- `*.trouter.communications.svc.cloud.microsoft`

For the current list of required network endpoints, see [Network requirements for PowerShell scripts and Win32 apps](../fundamentals/endpoints.md?tabs=north-america#network-requirements-for-powershell-scripts-and-win32-apps) and [Remote Help](../fundamentals/endpoints.md#remote-help) in the Intune endpoints documentation.

With this endpoint addition, we've also added a new [Intune Management Extension log](../device-management/tools/management-extension-windows.md#ime-log-files), NotificationInfra.log, which tracks notifications sent through the Microsoft real-time communication channel.

> [!div class="checklist"]
> Applies to:
>
> - Windows  

#### Support for Red Hat Enterprise Linux 9 and later<!-- 33087035 --> 
Microsoft Intune supports Red Hat Enterprise Linux (RHEL) 9 LTS and RHEL 10 LTS. Support for RHEL 8 LTS will end in July 2026. Devices already enrolled on RHEL 8 will remain enrolled. You can identify devices running RHEL 8 in the Intune admin center by going to **Devices** > **All devices**, filtering OS by Linux, and adding OS version columns. Notify users to upgrade their devices to a supported RHEL version.  For more information about enrolling Linux devices, see [Enrollment guide: Enroll Linux desktop devices in Microsoft Intune](../device-enrollment/guide-linux.md).  

#### Microsoft Intune app for Linux now supports the Microsoft Identity Broker<!-- 36124475 -->

The Microsoft Intune app for Linux now uses the Microsoft Identity Broker on supported Ubuntu and Red Hat Enterprise Linux (RHEL) distributions. Broker version 2.0.2 and later introduces a major architectural change from the previous Java-based broker. This update enables new single sign-on (SSO) experiences using phish-resistant MFA, smart card authentication, and certificate-based authentication with Microsoft Entra ID. For more information, see [Enabling Phish-Resistant MFA (PRMFA) on Linux devices](/entra/identity/devices/sso-linux?tabs=debian-install%2Cdebian-update%2Cdebian-uninstall#enabling-phish-resistant-mfa-prmfa-on-linux-devices-preview).  

### Device security

#### Intune security baseline for Windows 11, version 25H2<!-- 34955665  -->

The Windows security baseline for *Windows 11, version 25H2* is now available in Microsoft Intune. This baseline reflects current Microsoft security recommendations for supported Windows devices and is the latest available Windows security baseline in Intune.

The Windows 11, version 25H2 security baseline includes new settings, updated default values, retired settings, and revised security guidance. Existing security baseline profiles don't automatically update to the new version.

To use the Windows 11, version 25H2 security baseline, Intune admins can [create a new baseline profile](../device-security/security-baselines/configure-baselines.md#create-a-profile-for-a-security-baseline) or [update an existing profile to the latest version](../device-security/security-baselines/configure-baselines.md#update-a-baseline-profile-to-the-latest-version).

The following two settings aren't included in this baseline release and will be added in a future baseline update. Each change will be communicated to customers when available:

- **Disable Internet Explorer 11 launch via COM automation** – This setting isn't included at release due to a known issue. The Windows client team is addressing the issue, and the setting will be added in a future baseline update.
- **Configure NetBIOS settings** – This setting is pending availability in the Settings Catalog and will be added to the baseline in a future update.

We recommend carefully reviewing the settings in the new baseline before moving from a previous baseline version, especially if existing profiles include customizations.

For a detailed breakdown of setting changes, see the Windows blog post [Windows 11, version 25H2 security baseline](https://techcommunity.microsoft.com/blog/microsoft-security-baselines/windows-11-version-25h2-security-baseline/4456231).

To view the default configuration of the Intune baseline for Windows 11, version 25H2, see [Windows MDM baseline settings](../device-security/security-baselines/ref-windows-mdm-settings.md?pivots=mdm-25h2#security-baseline-for-windows-version-25h2).

> [!div class="checklist"]
> Applies to:
>
> - Windows 11

#### Hotpatching default enablement in Windows Autopatch<!--36869440-->

Starting with the May 2026 Windows security update, hotpatch updates are enabled by default for all eligible devices managed through Windows Autopatch. Hotpatch updates install faster and require fewer restarts, helping devices get
secure sooner.

If your organization isn't ready for this change, you can opt out using either of the following options:

- **Tenant-level setting**: Opt out of hotpatch updates across all eligible devices in your tenant. This option becomes available April 1, 2026 in the Intune admin center.
- **Quality update policy**: Control hotpatch behavior for a specific group of devices. Hotpatch settings configured in a quality update policy override the tenant-level setting for devices assigned to that policy.

Key dates:

- **April 1, 2026**: Tenant-level opt-out setting available in the Intune admin center.
- **May 2026 security update**: Hotpatch updates enabled by default.

For more information, see the Windows IT Pro Blog (https://aka.ms/HotpatchByDefault).

### Intune apps

#### Newly available protected apps for Intune <!-- 36620792, 36620880, 36621194, 36621352, 36627824 -->

The following protected apps are now available for Microsoft Intune:

- PerfectServe Clinical Collab by PerfectServe
- Synigo Pulse by Synigo B.V.
- DeepL for Intune by DeepL SE
- Foxit PDF Editor by Foxit Software Inc.
- EasyPlant QC Inspections by Technip Energies (Android)

For more information about protected apps, see [Microsoft Intune protected apps](../app-management/ref-protected-apps.md).

### Monitor and troubleshooting  

#### Support Assistant access expanded to all authenticated users<!-- 35992187 -->  

All authenticated users can now access Support Assistant in the Intune admin center to find solutions and troubleshooting guidance. Creating and managing support tickets still requires a Microsoft Entra role that includes the *microsoft.office365.supportTickets* permission. For more information, see [How to get support in the Microsoft Intune admin center](../fundamentals/it-pro-support/get-support-admin-center.md).  

#### Support for system proxy settings in endpoint analytics and Advanced Analytics<!--30148318 -->

Devices configured with system-level (WinHTTP) proxy settings can now send telemetry to endpoint analytics and Advanced Analytics, enabling more comprehensive reporting. Endpoint Privilege Management (EPM) will also include elevation usage data from these devices.

No admin action is required. If endpoint analytics or EPM is enabled for a device, telemetry and events will automatically appear in the User Experience (Device blade), endpoint Analytics reports, and EPM.

For more details about displaying advanced proxy settings, see [Netsh.exe commands](/windows/win32/winhttp/netsh-exe-commands#show-advproxy).

> [!div class="checklist"]
> Applies to:
>
> - Windows

#### Improvements to device query for multiple devices<!-- 32041372, 29800657, 33412956 -->

Device query for multiple devices now includes new capabilities to help you work with query results more efficiently.

You can use a search text box to search across all resulting rows of a query, use column headers to add filters for specific values, and create Microsoft Entra security groups directly from a query's device results.

For more information, see [Device query for multiple devices](../advanced-analytics/device-query-multiple-devices.md).

### Role-based access control

#### Scoped permissions for Role-based access control (public preview)<!-- 37134761 -->

Intune now includes an opt-in public preview to enable **Scoped permissions**, making your role-based access control (RBAC) configuration more precise. Enabling Scoped permissions is a one-time choice that can't be undone. In the future, this will become the default behavior for all tenants.

Previously, when an admin had multiple role assignments using different scope tags for the same permission category, Intune merged permissions across those assignments, which could unintentionally grant broader access than intended. With Scoped permissions enabled, each role assignment's permissions apply only within its own scope tag context, so admins receive exactly the access you intended.

To help you prepare before enabling this change, Intune includes a new **Permissions Assessment Report**. The report details your tenant's current permissions and shows how they will change after enabling Scoped permissions. You can rerun the report as often as needed, adjust role assignments, and communicate any changes to affected admins before opting in.

For more information about the current default behavior, the Scoped permissions opt-in public preview, and the new report, see [Permission behavior across role assignments](../fundamentals/role-based-access-control/scope-tags.md#permission-behavior-across-role-assignments).

## Week of March 24, 2026

### Tenant administration

#### Guided scenarios being removed from the Intune admin center<!-- 29654118 -->

All guided scenarios except Windows 365 Boot are removed from the Microsoft Intune admin center. You can no longer access the guided scenario wizards, but any Intune objects previously created by these wizards remain available and manageable. The Windows 365 Boot guided scenario remains available from the Windows 365 overview page in the Intune admin center. No action is required.

For alternative step-by-step guidance, see the following resources:

- [Microsoft Intune documentation](https://go.microsoft.com/fwlink/?linkid=2310495)
- [Intune prescriptive guides](https://go.microsoft.com/fwlink/?linkid=2300666)
- Intune administration guides: [https://m365accelerator.microsoft.com/intune](https://m365accelerator.microsoft.com/intune)
  - [Securing apps for mobile | Android](https://m365accelerator.microsoft.com/intune/manage-and-secure-apps-for-android)
  - [Securing apps for mobile | iOS](https://m365accelerator.microsoft.com/intune/manage-and-secure-apps-for-ios)
  - [Configuring Intune and Configuration Manager to co-manage devices](https://m365accelerator.microsoft.com/intune/microsoft-intune-and-configuration-manager-co-management-setup-guide)
  - [Manage and secure devices for Windows](https://m365accelerator.microsoft.com/intune/windows-device-management)
- [Microsoft Copilot in Intune](../copilot/index.md)

> [!div class="checklist"]
> Applies to:
>
> - Windows 10/11
> - iOS/iPadOS
> - Android

## Week of March 16, 2026  

### Device management

#### Improved Remote Help update reporting on macOS<!-- 35705883 -->  

We've improved the update and reporting experience for Remote Help on macOS to make version management more reliable and transparent for IT admins.  
 
After you deploy the latest Remote Help client (version 1.0.26012221) through Microsoft Intune, you can now view the full client version in your device inventory and during app upgrades. This improvement makes it easier to verify deployments. Remote Help installations deployed through Intune are also registered with Microsoft AutoUpdate (MAU), allowing Intune-managed macOS devices to automatically receive future Remote Help updates. For more information, see [Deploy Remote Help with Microsoft Intune](../remote-help/deploy.md).

## Week of March 2, 2026 (Service release 2602)

### App management

#### Newly available protected apps for Intune <!-- 36072390, 36072616 -->

The following protected apps are now available for Microsoft Intune:

- Jump by Accio Inc.
- Mijn InPlanning by Intus Workforce Solutions (Android)

For more information about protected apps, see [Microsoft Intune protected apps](../app-management/ref-protected-apps.md).

### Device configuration

#### Apple declarative device management (DDM) supports assignment filters<!-- 24298491 -->

You can use assignment filters in policy assignments for DDM-based configurations, like software updates.

> [!NOTE]
> This feature is rolling out slowly and should be available for all customers by late March 2026.

To learn more about filters, see [Use assignment filters to assign your apps, policies, and profiles in Microsoft Intune](../fundamentals/filters/overview.md).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

#### New settings in the Windows settings catalog <!-- 36822089 -->

There are new settings in the Windows settings catalog. To see and configure these settings in Intune, create a Windows settings catalog profile (**Devices > Configuration profiles > Create profile > Windows 10 and later > Settings catalog**).

The new policies include:

**Microsoft Edge**:

- **Control whether an informational webpage for Edge for Business is shown in the new tab after major browser updates**: When **Enabled** or not configured, users with Microsoft Entra ID profiles see an informational page about new Edge for Business features after major browser updates. When **Disabled**, the informational page isn't shown to users.

  This policy:

  - Applies only to Microsoft Entra ID profiles. It doesn't apply to Microsoft account (MSA) profiles.
  - Is available starting in Microsoft Edge version 144, which allows you to configure the setting before any version 145 changes.

- **Enable Silent Printing**: When **Enabled**, Microsoft Edge automatically closes the print preview window and prints to the default printer using its default settings. If the default printer is **Save as PDF**, the file is saved to the user's Downloads folder. When **Disabled** or not configured, silent printing is disabled. The print preview window stays open, and the user must choose the print settings as usual.

**Microsoft Edge > Content settings**:

- **Allow precise geolocation on these sites**: When **Enabled**, enter a list of URL patterns for sites that are allowed to access the user's high-accuracy geolocation without prompting for permission. When **Disabled** or not configured, the default geolocation setting applies to all sites (if configured) or the user's personal setting is used.

  For information about valid URL patterns and examples, see [Filter formats for URL list-based policies](/deployedge/edge-learnmmore-url-list-filter%20format). Wildcards (*) are supported.

- **Block geolocation on these sites**: When **Enabled**, enter a list of URL patterns for sites that are blocked from requesting or accessing the user's geolocation. These sites can't prompt the user for location permissions. When **Disabled** or not configured, the default geolocation setting applies to all sites (if configured) or the user's personal browser setting is used.

  For information about valid URL patterns and examples, see [Filter formats for URL list-based policies](/deployedge/edge-learnmmore-url-list-filter%20format). Wildcards (*) are supported.

**Windows Backup and Restore**:

- **Enable Windows Restore**: Choose to enable Windows Restore. When enabled, the restore process for a device can be initiated:

  - At the time of device enrollment during the out-of-box experience (OOBE), or
  - The first time a user signs in with their Microsoft Entra ID account after the device finishes enrolling.

  It allows a user to restore their backed‑up Windows settings and Microsoft Store apps from the cloud to a new or reset device. It restores the user experience settings and configuration preferences. It's not a full system image. To learn more, see [Windows Backup for Organizations overview](/windows/configuration/windows-backup).

  Your options:

  - Windows Restore Not Configured
  - Windows Restore Enabled

  This policy:

  - Was previously for Windows Insiders and is now generally available (GA).
  - Uses the [WindowsBackupAndRestore CSP](/windows/client-management/mdm/windowsbackupandrestore-csp).

> [!div class="checklist"]
> Applies to:
>
> - Windows

To learn more about the settings catalog, see [Use the Intune settings catalog to configure settings](../device-configuration/settings-catalog/index.md).

#### New updates to the Apple settings catalog <!-- 36180374 -->

The [Settings Catalog](../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../device-configuration/settings-catalog/index.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**AirPlay**:

- Device Name

##### macOS

**AirPlay**:

- Device Name

**Microsoft Defender**:

- The Microsoft Defender category is updated with new settings. Learn more about available macOS Defender settings at [Microsoft Defender - Policies](/defender-endpoint/mac-preferences).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

### Device enrollment  

#### New setting controls MDM enrollment during account registration on Windows (public preview)<!-- 14724061 --> 

A new setting that affects the Microsoft Entra account registration experience on Windows is available in the Microsoft Intune admin center. The setting, **Disable MDM enrollment when adding work or school account on Windows**, controls whether devices enroll in MDM during the account registration flow. The default setting is set to **No**, which allows MDM enrollment. No action is required unless you want to change the default enrollment behavior. This Microsoft Entra setting is in public preview. For more information, see [Enable MDM automatic enrollment for Windows](../device-enrollment/windows/enable-automatic-mdm.md).  

### Device management

#### Multi-administrator approval support for device compliance and device configuration policies<!-- 26838614 -->

Multi-administrator approval now supports device configuration policies created through the settings catalog and device compliance policies. When you turn on this feature, any changes you make, including creating, editing, or deleting a policy, must be approved by a second administrator before they take effect. This dual-authorization process helps protect your organization from unauthorized or accidental changes to role-based access control.

For more information, see [Use Access policies to require Multi Admin Approval](../fundamentals/role-based-access-control/multi-admin-approval.md).

### Device security

#### Intune ending support for legacy Apple MDM software update policies<!--36742761 -->

With the release of iOS 26, iPadOS 26, and macOS 26, Apple has deprecated legacy mobile device management (MDM) software update commands and payloads. As a result, Microsoft Intune will soon end support for creating legacy iOS/iPadOS and macOS software update policies.
To continue managing Apple software updates in Intune, configure update policies using Apple's declarative device management (DDM) model. DDM provides a more modern and reliable approach to managing software updates, with improved device autonomy and reporting.

For guidance on moving to DDM‑based software updates, see the Intune Customer Success blog: [Move to declarative device management for Apple software updates](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-move-to-declarative-device-management-for-apple-software-updates/4432177).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

#### Autopatch update readiness<!--34573480 -->

Autopatch update readiness provides a unified experience for tracking and remediating Windows update issues across Intune-enrolled devices and Windows Autopatch group-enrolled devices.
With a single dashboard, admins can view all managed devices, including enrollment status and policy assignments, to better understand update readiness across their environment.

Key capabilities include:

- **Device update journey**: View granular update states for each device to quickly identify where updates are blocked and why.
- **Centralized alerting**: See actionable alerts for update failures, policy conflicts, and readiness gaps in one place, with integrated remediation guidance.
- **Update readiness checker**: Proactively evaluate devices for deployment risks and flag devices as At Risk based on signals such as disk space, appraiser data, and setup conditions.
- **Repair devices with OS reinstall**: Remediate upgrade‑blocked devices by triggering an OS reinstall for common issues like insufficient disk space or app compatibility problems, with supporting alerts and reporting.

For more information, see [Autopatch update readiness](/windows/deployment/windows-autopatch/monitor/windows-autopatch-update-readiness-overview).

> [!div class="checklist"]
> Applies to:
>
> - Windows

### Monitor and troubleshoot

#### Updates to operators in device query for multiple devices<!--36180651 -->

Device query for multiple devices now includes expanded operator support, clearer query validation, and improved results to make building and interpreting queries easier.

- **New join types supported**\
  You can now use the following join types when querying across entities:
  - `leftsemi`
  - `rightsemi`
  - `leftanti`
  - `rightanti`
- **Updated join behavior**\
  Joins that use `on Device.DeviceId` are no longer supported. Queries should instead:
  - Use `on Device`, or
  - Omit the on clause entirely when joining on the device entity.
- **Updated device references in operators**\
  Using Device by itself is no longer supported in operators such as `distinct`, `summarize`, or `order by`. Queries must reference a specific device property.
- **Improved query results**\
  Queries that involve a device—either by querying a device directly or by joining a device with another entity—now return the device as a clickable link in the results, allowing you to quickly navigate to device details.
- **Clearer error messages**\
  Some query error messages have been updated to provide clearer, more descriptive guidance when queries are invalid.

## Week of February 9, 2026 (Service release 2601)

### Microsoft Intune Suite

#### Endpoint Privilege Management support on Azure Virtual Desktop<!-- 26079227 -->

Endpoint Privilege Management (EPM) elevation policies now support deployment to users on Azure Virtual Desktop (AVD) single-session virtual machines.

For information about using EPM, which is available as an [Intune Suite add-on-capability](../fundamentals/add-ons.md), see [Plan and Prepare for Endpoint Privilege Management Deployment](../epm/deployment-planning.md).

### App management

#### Lenovo Device Orchestration (LDO) link in the Intune admin center<!-- 32634377 -->

Microsoft Intune now includes a direct link to **Lenovo Device Orchestration (LDO)** in the Intune admin center. This integration expands the **Partner portals** experience by giving IT admins a single, secure entry point to manage supported Lenovo devices.

From the Intune admin center, IT admins can open the Lenovo Device Orchestration portal directly to access Lenovo-specific device management capabilities.

> [!div class="checklist"]
> Applies to:
>
> - Windows 11

#### Newly available protected apps for Intune<!-- 35601128, 36072132, 36072263, 36078662 -->

The following protected apps are now available for Microsoft Intune:

- Clarity Express for Intune by Rego Consulting Corporation
- Datadog by Datadog Inc.
- Qlik Analytics by Qlik
- Tier1 for Intune by SS&C Technologies, Inc. (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../app-management/ref-protected-apps.md).

### Device configuration

#### New settings in the Windows settings catalog<!-- 34625889 -->

There are new settings in the Windows settings catalog. To see and configure these settings in Intune, create a Windows settings catalog profile (**Devices > Configuration profiles > Create profile > Windows 10 and later > Settings catalog**).

The new policies include:

- Microsoft Edge - Includes the latest Microsoft Edge browser policies, up to version 143.0.3650.23, including:

  - **Allow sharing tenant-approved browsing history with Microsoft 365 Copilot Search**
  - **Enable RAM (memory) resource controls**
  - **Specifies whether to opt out of Local Network access restrictions**

  Due to differences in release cadences between Microsoft Edge and Intune, there can be a one-to-two-week delay in the settings catalog.

- Experience > **Disable Share App Promotions** - This policy setting allows IT admins to control if promotional apps are shown in the [Windows Share Sheet](/windows/apps/develop/windows-integration/integrate-sharesheet-overview). If you enable this policy, Windows doesn't show promotional apps in the Share Sheet.

- Licensing > **Enable ESU Subscription Check**: This policy is deprecated and only works on Windows 10. Setting this policy has no effect on other supported Windows versions. This policy enables or disables subscription check for Windows 10 Extended Security Updates. If enabled, the device check for the ESU subscription status of the signed-in Microsoft Entra ID user account.

- Windows AI - Includes the following new settings that are available to Windows Insiders:

  - **Disable Agent Workspaces** - Enables or disables Agent Workspaces.
  - **Disable Agent Connectors** - Enables or disables Agent Connectors.
  - **Disable Remote Agent Connectors** - Enables or disables remote Agent Connectors.
  - **Agent Connector Minimum Policy** - Configures the minimum policy value that controls how agent connectors run on the machine.

- Google Chrome - Includes the Google Chrome ADMX browser policies, up to version 141.0.7390.108.

  Due to differences in release cadences between Chrome and Intune, Intune can be one to two versions behind the latest released Chrome version.

- Firewall > **Enable Audit Mode** - If enabled, the target machine goes into Firewall audit mode.

- Microsoft Visual Studio > Copilot settings > **Disable agent mode** - This existing Copilot setting is updated to include localization. This setting prevents users from using GitHub Copilot agent mode.

- Windows Components > Internet Explorer > Internet Control Panel > Security Page:

  - **Turn on automatic detection of intranet** - This policy setting enables intranet mapping rules to be applied automatically if the computer belongs to a domain. If you enable this policy setting, automatic detection of the intranet is turned on, and intranet mapping rules are applied automatically if the computer belongs to a domain.

  - **Intranet Sites: Include all sites that bypass the proxy server** - This policy setting controls whether sites which bypass the proxy server are mapped into the local Intranet security zone. If you enable this policy setting, sites which bypass the proxy server are mapped into the Intranet Zone.

> [!div class="checklist"]
> Applies to:
>
> - Windows

To learn more about the settings catalog, see [Use the Intune settings catalog to configure settings](../device-configuration/settings-catalog/index.md).

#### New supported OEMConfig apps for Android Enterprise<!-- 35178386 -->

The following OEMConfig apps are available in Intune for Android Enterprise:

- FCNT - Senior Care | `com.fcnt.mobile_phone.seniorcareconfig`
- FCNT - Schema | `com.fcnt.mobile_phone.schematest`
- Sonim | `com.sonim.oemappconfig`

For more information about OEMConfig, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../device-configuration/templates/configure-oemconfig-android.md).

#### Filter by Android management mode in the settings catalog<!-- 31844205 -->

The [settings catalog](../device-configuration/settings-catalog/index.md) includes hundreds of settings that you can configure. There are built-in features that help filter the available settings.

When you create an Android settings catalog policy, there's a management mode filter option that filters the available settings by their enrollment type, including:

- Fully managed
- Corporate-owned work profile
- Dedicated

To learn more about the settings catalog, see:

- [Use the Intune settings catalog to configure settings](../device-configuration/settings-catalog/index.md)
- [Android Intune settings catalog settings list](../device-configuration/settings-catalog/ref-android-settings.md)

#### New updates to the Apple settings catalog<!-- 35787099 -->

The [Settings Catalog](../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../device-configuration/settings-catalog/index.md).

There is a new setting in the Settings Catalog. To see this setting, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Restrictions**:

- Rating Apps Exempted Bundle IDs: This setting lets admins specify apps that can bypass the 17 and older restriction.

  For example, a device can have its content restricted to ages 9 and below. With this restriction, apps with an age-based rating of 17 and older are automatically blocked. Admins can use this setting to allow specific apps to bypass this restriction.

Apple rebranded **Rapid Security Responses** to **Background Security Improvements**. This change is updated in the settings catalog. For more information on Background Security Improvements, see [Background Security Improvements on Apple devices](https://support.apple.com/guide/deployment/background-security-improvements-dep93ff7ea78/web) (opens Apple's web site).

### Device management

#### More options for assignment filters > Device Management Type property for managed apps on Android and iOS/iPadOS<!-- 25040926 -->

When you create policies for your managed apps, you can use [assignment filters](../fundamentals/filters/overview.md) to assign policies based on rules you create. In these rules, you can use different device and app properties, including the **Device Management Type** property on Android and iOS/iPadOS.

> [!NOTE]
> This feature is rolling out slowly and should be available for all customers by late March 2026.

For Android, the **Device Management Type** property for managed apps is:

- Adding the following options:

  - Corporate-owned with work profile
  - Corporate-owned fully managed
  - Corporate-owned dedicated devices with Entra ID Shared mode
  - Corporate-owned dedicated devices without Entra ID Shared mode
  - Personally owned work profile

- To replace the following option:

  - Android Enterprise

For iOS/iPadOS, the **Device Management Type** property for managed apps is:

- Adding the following options:

  - Automated Device Enrollment user-associated devices
  - Automated Device Enrollment userless devices
  - Account Driven User Enrollment
  - Device Enrollment with Company Portal and Web Enrollment

- To replace the following option:

  - Managed

##### What you need to know

- If you're using the legacy values in your filters, the values are automatically mapped to the new available values for that platform.
- For the automatic mapping to work correctly, devices must be registered with Microsoft Entra and have a Microsoft Entra Device ID. If the devices don't meet these requirements, the app assignment filters won't match to the more granular management types. You can use an Intune [app configuration policy](../app-management/configuration/configure-managed-apps.md#add-an-app-configuration-policy-for-managed-apps-on-iosipados-and-android-devices) to force Microsoft Entra device registration with the `com.microsoft.intune.mam.IntuneMAMOnly.RequireAADRegistration=Enabled` key.
- If the device is MDM-managed by a third-party or partner service, the managed app assignment filters won't match to the more granular management types.

To learn more about filters, see:

- [Use assignment filters to assign your apps, policies, and profiles in Microsoft Intune](../fundamentals/filters/overview.md)
- [App and device properties, operators, and rule editing when creating assignment filters in Microsoft Intune](../fundamentals/filters/ref-device-properties.md)

> [!div class="checklist"]
> Applies to:
>
> - Android
> - iOS/iPadOS

#### Intune certificate inventory integration with Zimperium mobile threat defense<!-- 35519603 -->

You can now configure the Zimperium Mobile Threat Defense (MTD) connector to synchronize certificate inventory from your managed iOS devices. This enhancement helps you identify when a device threat level is elevated due to approved but potentially malicious certificates on the device. The following settings are now available when configuring the connector:

- **Enable Certificate Sync for iOS/iPadOS devices** - Allows this Mobile Threat Defense partner to request a list of installed certificates on iOS/iPadOS devices from Intune to use for threat analysis purposes.
- **Send full certificate inventory data on personally owned iOS/iPadOS devices** - This setting controls the certificate inventory data that Intune shares with this Mobile Threat Defense partner for personally owned devices. Data is shared when the partner syncs certificate data and requests the certificate inventory list.

When certificate sync is enabled, the following data is shared:

- Account ID
- Entra ID Device ID
- Device Owner
- Certificate List
  - Common Name
  - Data
  - Is Identity

For more information, see [Mobile Threat Defense toggle options](../device-security/mobile-threat-defense/enable-connector.md#mobile-threat-defense-toggle-options).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

### Device security

#### Update firewall configurations for new Intune network endpoints<!-- 34445623 -->

As part of Microsoft's ongoing [Secure Future Initiative (SFI)](https://www.microsoft.com/trust-center/security/secure-future-initiative), Microsoft Intune began using Azure Front Door (AFD) IP addresses in addition to the existing Intune service IPs in December 2025.

Customers that use IP-based allowlist, Azure service tags, or have strict outbound filtering in their firewall, VPN, proxy, or other network infrastructure may block this new traffic, causing degraded or failed device connectivity. This can affect core Intune functions including device and app management.

- **If your organization uses Fully Qualified Domain Name (FQDN)-based rules or does not restrict outbound traffic**, no changes are typically required. However, you should verify that the appropriate wildcard rules are configured, specifically `*.manage.microsoft.com`, to ensure all Intune services remain reachable. Microsoft continues to recommend using FQDN-based wildcard rules whenever possible to reduce administrative overhead for organizations that require outbound filtering.
- **If your organization uses IP-based allowlists** in your firewall, proxy, or VPN rules, you must add the Azure Front Door IP ranges below or use Azure service tag `AzureFrontDoor.MicrosoftSecurity` to avoid potential connectivity issues for managed devices.

Required IP addresses for commercial endpoints:

- 13.107.219.0/24
- 13.107.227.0/24
- 13.107.228.0/23
- 150.171.97.0/24
- 2620:1ec:40::/48
- 2620:1ec:49::/48
- 2620:1ec:4a::/47

Required IP addresses for US government endpoints:

- 51.54.53.136/29
- 51.54.114.160/29
- 62.11.173.176/29

For the authoritative and up-to-date list of network endpoints required by Intune client and host services, see [Intune core service](../fundamentals/endpoints.md#intune-core-service) in *Network endpoints for Microsoft Intune*, and [Ports and IP addresses list](../fundamentals/endpoints-us-government.md#ports-and-ip-addresses-list) in *US government endpoints for Microsoft Intune*.

For additional context on this change, see [Support Tip: Upcoming Microsoft Intune Network Changes](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-upcoming-microsoft-intune-network-changes/4452738).

### Monitor and troubleshoot

#### Windows feature update reports support Windows 11, version 25H2<!-- 36157178 -->
 
The *Windows feature update compatibility risks report* and *Windows feature update device readiness report* support Windows 11, version 25H2 as a selectable target OS. When you choose this version under **Select target OS**, the reports provide updated insights to help you assess device readiness and identify potential compatibility risks before deploying the feature update.

> [!div class="checklist"]
> Applies to:
>
> - Windows

### Tenant administration

#### Admin tasks in Microsoft Intune are now generally available<!-- 32978931 -->

**Admin tasks** in the Intune admin center are out of preview and now generally available. Admin tasks provide a centralized view where admins can discover, organize, and act on common tasks that are otherwise spread throughout the Intune admin center. Located under **Tenant Administration**, this unified experience supports search, filtering, and sorting to help you focus on what needs attention, without navigating across multiple nodes.

The following task types are supported:

- Endpoint Privilege Management file elevation requests
- Microsoft Defender security tasks
- Multi Admin Approval requests

Intune only shows tasks you have permission to manage. When you select a task, Intune opens the same interface and workflow you'd use if managing the task from its original location. This ensures a consistent experience whether you're working from the admin tasks node or directly within the source capability.

To learn more, see:

- [Admin tasks](../device-management/admin-tasks.md)

## Week of January 12, 2026

### App management

#### PowerShell script installer for Win32 apps <!-- 34496511 -->

When adding a Win32 app, you can upload a PowerShell script to serve as the installer instead of specifying a command line. Intune packages the script with the app content and runs it in the same context as the app installer, enabling richer setup workflows like prerequisite checks, configuration changes, and post-install actions. Installation results appear in the Intune admin center based on the script's return code.

For more information, see [Win32 app management in Microsoft Intune](../app-management/deployment/win32.md).

> [!div class="checklist"]
> Applies to:
>
> - Windows

## Week of December 8, 2025  

### Device enrollment  

#### ACME protocol support for iOS/iPadOS and macOS enrollment <!-- 25140355 -->

As we prepare to support managed device attestation in Intune, we are starting a phased rollout of an infrastructure change for new enrollments that includes support for the *Automated Certificate Management Environment (ACME) protocol*. Now when new Apple devices enroll, the management profile from Intune receives an ACME certificate instead of a SCEP certificate. ACME provides better protection than SCEP against unauthorized certificate issuance through robust validation mechanisms and automated processes, which helps reduce errors in certificate management. 

Existing OS and hardware eligible devices do not get the ACME certificate unless they re-enroll. There is no change to the end user's enrollment experience, and no changes to the Microsoft Intune admin center. This change only impacts enrollment certificates and has no impact on any device configuration policies. 

ACME is supported for Apple Device Enrollment (BYOD), Apple Configurator enrollment, and automated device enrollment (ADE) methods. Eligible OS versions include:  

* iOS 16.0 or later  

* iPadOS 16.1 or later  

* macOS 13.1 or later    

#### New Setup Assistant screens now generally available for iOS/iPadOS and macOS automated device enrollment profiles <!-- 29832295, 29832295 -->

You can hide or show 12 new Setup Assistant screens during automated device enrollment (ADE). The default is to show these screens in Setup Assistant. 

The screens you can skip during iOS/iPadOS enrollment, and the applicable versions, include:

- **App Store** (iOS/iPadOS 14.3+)
 - **Camera button** (iOS/iPadOS 18+)
 - **Web content filtering** (iOS/iPadOS 18.2+)
 - **Safety and handling** (iOS/iPadOS 18.4+)
 - **Multitasking** (iOS/iPadOS 26+)
 - **OS Showcase** (iOS/iPadOS 26+)

The screens you can skip during macOS enrollment include:

- **App Store** (macOS 11.1+)
   - **Get Started** (macOS 15+)
   - **Software update** (macOS 15.4+)
   - **Additional privacy settings** (macOS 26+)
   - **OS Showcase** (macOS 26.1+)
   - **Update completed** (macOS 26.1+)

For more information about available Setup Assistant skipkeys, see:

- [Set up automated device enrollment for iOS/iPadOS](../device-enrollment/apple/setup-automated-ios.md#setup-assistant-screen-reference)  
- [Set up automated device enrollment for macOS](../device-enrollment/apple/setup-automated-macos.md#setup-assistant-screen-reference)

## Week of December 1, 2025

### App management

#### Secure enterprise browser managed by Intune (public preview) <!-- 31609121 -->

Microsoft Intune now supports policy management for Microsoft Edge for Business as a secure enterprise browser. By implementing policies through Intune, admins can confidently transition from Windows-based desktop environments to secure, browser-based workflows for accessing corporate resources without requiring device enrollment.

For more information, see [Secure Your Corporate Data in Intune with Microsoft Edge for Business](../solutions/edge-data-security/overview.md).

## Week of November 17, 2025  

### Device enrollment  

#### Configure Windows Backup for Organizations <!--29202026 -->  

*Windows Backup for Organizations* is generally available in Microsoft Intune. With this feature, you can back up your organization's Windows settings and restore them on a Microsoft Entra joined device. Backup settings are configurable in the Microsoft Intune admin center settings catalog, while a tenant-wide setting that lets you restore a device is available in the admin center under **Enrollment**. For more information about this feature, see [Windows Backup for Organizations in Microsoft Intune](../device-enrollment/windows/enable-backup-restore.md). 

### Device management

#### Security Copilot in Intune agents are available for public preview <!-- 32766422 35360466 35100315 35320958 -->

Security Copilot agents in Intune are AI-powered assistants that specialize in specific scenarios. The Intune agents are available in the Intune admin center > **Agents**, and are available for Security Copilot users.

The following Intune agents are available:

- The **[Change Review Agent](../copilot/agents/change-review-agent.md)** evaluates Multi Admin Approval requests for Windows PowerShell scripts on Windows devices. It provides risk-based recommendations and contextual insights to help admins understand script behavior and associated risks.

  These insights can help Intune admins make informed decisions more quickly about whether to approve or deny requests. This agent supports Intune-managed devices running Windows.

- The **[Device Offboarding Agent](../copilot/agents/device-offboarding-agent.md)** identifies stale or misaligned devices across Intune and Microsoft Entra ID. It provides actionable insights and requires admin approval before offboarding any devices. This agent complements existing Intune automation by showing insights and handling ambiguous cases where automated cleanup isn't enough.

  The agent supports Intune-managed devices running Windows, iOS/iPadOS, macOS, Android, and Linux. During public preview, admins can directly disable Microsoft Entra ID objects, with additional remediation steps provided as guidance.

- The **[Policy Configuration Agent](../copilot/agents/policy-configuration-agent.md)** analyzes uploaded documents or industry benchmarks and automatically identifies matching Intune settings. Admins can upload their requirements, like compliance standards or internal policy documents, and the agent intelligently shows relevant settings from the Intune settings catalog.

  The agent also guides you through policy creation and helps you configure each setting that best suits your organization's needs. This agent supports devices running Windows.

To learn more, see:

- [Security Copilot agents in Intune](../copilot/agents/index.md)

#### Intune support for iVerify as a mobile threat defense partner<!-- 35838315 -->

You can now use iVerify Enterprise as a mobile threat defense partner (MTD) for enrolled devices that run the following platforms:  

- Android 9.0 and later
- iOS/iPadOS 15.0 and later

To learn more about this support, see [Set up iVerify Mobile Threat Defense Connector](../device-security/mobile-threat-defense/iverify.md).

### Tenant administration

#### Manage tasks and requests from the centralized Admin tasks node in Microsoft Intune (public preview)<!-- 3542038 -->

The new **Admin tasks** node in the Intune admin center provides a centralized view to discover, organize, and act on security tasks and user elevation requests. Located under **Tenant Administration**, this unified experience supports search, filtering, and sorting to help you focus on what needs attention—without navigating across multiple nodes.

The following task types are supported:

- Endpoint Privilege Management file elevation requests
- Microsoft Defender security tasks
- Multi Admin Approval requests

Intune only shows tasks you have permission to manage. When you select a task, Intune opens the same interface and workflow you'd use if managing the task from its original location. This ensures a consistent experience whether you're working from the admin tasks node or directly within the source capability.

For more information, see [Admin tasks](../device-management/admin-tasks.md).

## Week of November 10, 2025 (Service release 2511)

### Microsoft Intune Suite

#### Scope tag enforcement for Endpoint Privilege Management elevation requests<!-- 33479826  -->

When viewing Endpoint Privilege Management [elevation requests](../epm/manage-support-approvals.md#about-support-approved-elevations), applicable scope tags are now enforced. This means administrators can view and manage only the requests for devices and users that fall within their assigned scope. This change helps maintain administrative boundaries and strengthen security. Previously, admins with permissions to manage elevation requests could view all elevation requests, regardless of scope.

### App management

#### More volume options available in Managed Home Screen <!-- 16462284 -->

Admins can now enable more volume controls in the Managed Home Screen (MHS) app for Android Enterprise dedicated and fully managed devices. In addition to the existing media volume control, this update introduces configuration settings to show or hide sliders for **call**, **ring and notification**, and **alarm** volumes.

Each new option can be independently enabled through app configuration policies. When turned on, users can adjust these specific volume levels directly from the Managed Settings page within MHS, without leaving kiosk mode. This enhancement provides task workers greater flexibility to manage sound levels for different environments while keeping the device securely locked down.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../app-management/configuration/configure-managed-home-screen.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise (dedicated and fully managed devices)

#### Reset Managed Google Play store mode to Basic <!-- 33632857 -->

You can now reset the Managed Google Play store layout from **Custom** back to **Basic** in the Intune admin center (**Apps** > **All apps** > **Create Managed Google Play app**).

In **Basic** mode, all approved apps are automatically visible to users. In **Custom** mode, newly approved apps must be manually added to collections before they appear in the store. The new **Reset to Basic** button lets admins quickly revert to Basic mode without needing to contact support. When selected, Intune deletes all existing collections and immediately displays a success or failure message.

For more information about Managed Google Play store layout options, see [Approve and deploy Android Enterprise apps in Intune](../app-management/deployment/add-managed-google-play.md).

> [!div class="checklist"]
> Applies to:
>
> - Android

#### Updated Service Level Objectives for Enterprise App Management <!-- 30049867 -->

**Service Level Objectives (SLOs)** are now available in Enterprise App Management (EAM) to provide clearer expectations for when app updates become available in the Enterprise App Catalog. SLO processing timelines begin when Intune first receives the updated app package.

Most app updates complete automated validation within 24 hours. Updates that require manual vendor testing or approval typically complete within seven days.

For more information, see [Enterprise App Management overview](../app-management/deployment/enterprise-app-management.md).

#### New cut, copy, and paste options for Windows app protection <!-- 25427327 -->

Intune adds two new values to the **Allow cut, copy and paste for** setting in Windows app protection policies (starting with Microsoft Edge) to give admins more control over data movement:

- Org data destinations and any source: Users can paste from any source into the org context, and can cut/copy only to org destinations.  
- Org data destinations and org data sources: Users can cut/copy/paste only within the org context.

These options extend familiar mobile APP data-transfer controls to Windows, helping prevent data leaks on unmanaged devices while preserving productivity. For more information, see [App protection policies overview](../app-management/protection/overview.md).

> [!div class="checklist"]
> Applies to:
>
>- Windows

### Device configuration

#### Settings available in both Templates and Settings Catalog for Android Enterprise <!-- 34876806 -->

Some settings that were only available in Templates are now also supported in the settings catalog.

The [settings catalog](../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../device-configuration/settings-catalog/index.md).

To create a new settings catalog policy, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type.

The following settings are available in the settings catalog:

**General**:

- Block Contact sharing via Bluetooth (work profile level)
- Block searching of work contacts and displaying work contact caller-id in personal profile
- Data sharing between work and personal profiles
- Skip first use hints

**Work profile password**:

- Number of days until password expires
- Number of passwords required before user can reuse a password
- Number of sign-in failures before wiping device
- Required password type
  - Minimum password length
  - Number of characters required
  - Number of lowercase characters required
  - Number of non-letter characters required
  - Number of numeric characters required
  - Number of symbol characters required
  - Number of uppercase characters required
- Required unlock frequency

To learn more about these settings, see [Android Intune settings catalog settings list](../device-configuration/settings-catalog/ref-android-settings.md).

Applies to:

- Android Enterprise

#### New Assist Content Sharing setting in the Android Enterprise settings catalog<!-- 31479342 -->

The [Settings Catalog](../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../device-configuration/settings-catalog/index.md).

There are new settings (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type):

- **Block assist content sharing with privileged apps**: If **True**, this setting blocks assist content, like screenshots and app details, from being sent to a privileged app, like an assistant app. The setting can be used to block the **Circle to Search** AI feature.

For some guidance on managing AI features on Android devices, see [Manage AI on Android with Intune - A Guide for IT Admins](../solutions/ai/manage-ai-android.md).

Applies to:

- Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)

### Device enrollment  

#### New opt-in upgrade allows existing customers to move from managed Google Play accounts to Microsoft Entra ID accounts<!-- 30675087 --> 

Microsoft Intune offers a new opt-in upgrade that allows existing Android Enterprise customers to move from using managed Google Play accounts to using Microsoft Entra ID accounts for Android device management. You are eligible for upgrade if you previously used a consumer Gmail account. This change streamlines the onboarding process by eliminating the need for a separate Gmail account and by leveraging your work account. This change is not required. To learn more about this change, see:

- [New onboarding flow to managing Android Enterprise devices with Microsoft Intune](https://techcommunity.microsoft.com/blog/intunecustomersuccess/new-onboarding-flow-to-managing-android-enterprise-devices-with-microsoft-intune/4206602)
- [Connect your Intune account to your managed Google Play account](../device-enrollment/android/connect-managed-google-play.md#upgrade-to-a-managed-google-domain)

#### Incomplete user enrollment report removed <!-- 26395805 -->

The incomplete user enrollments report has been removed and is no longer functional in the Microsoft Intune admin center. The following corresponding APIs have also been removed from Microsoft Intune:  

- getEnrollmentAbandonmentDetailsReport
- getEnrollmentAbandonmentSummaryReport
- getEnrollmentFailureDetailsReport

Scripts or automation using these Graph APIs will stop working now that the report has been removed. In place of this report, we recommend using the enrollment failures report. For more information, see [View enrollment reports](../device-enrollment/monitor-reports.md#enrollment-failures-report).  

### Device management 

#### Query and results improvements to Explorer feature with Security Copilot in Intune <!--33987602-->

With your Security Copilot license, you can query your Intune data using the **[Explorer in Intune](../copilot/explorer.md)** feature. 

When you create your queries, you have more filter options. For example:

- Queries with a number operator let you choose equal, greater than, and less than values.
- Queries that forced you to choose one option, like platform, allow you to select multiple options.

In the query results, there are also more columns available to view your data.

To learn more about this feature, see [Explore Intune data with natural language and take action](../copilot/explorer.md).

#### Device Management Type assignment filter property supports Android enrollment options for Managed Devices<!-- 33016364 -->

When you create a policy in Intune, you can use [assignment filters](../fundamentals/filters/overview.md) to assign a policy based on rules you create. You can create a rule using different [properties](../fundamentals/filters/ref-device-properties.md), like `deviceManagementType`.

For managed devices, the Device Management Type property supports the following Android enrollment options:

- Corporate-owned dedicated devices with Entra ID Shared mode
- Corporate-owned dedicated devices without Entra ID Shared mode
- Corporate-owned with work profile
- Corporate-owned fully managed
- Personally owned device with a work profile
- AOSP user-associated devices
- AOSP userless devices

To learn more about assignment filters and the properties you can currently use, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](../fundamentals/filters/overview.md)
- [App and device properties, operators, and rule editing when creating filters in Microsoft Intune](../fundamentals/filters/ref-device-properties.md)

Applies to:

- Android

#### New prompts available to explore your Intune data <!-- 33787582 -->

You can use Security Copilot in Intune to explore new prompts related to your data using natural language. Use these new prompts to view data on:

- Users and groups
- Role based access control (RBAC)
- Audit logs

When you start typing your request, a list of prompts that best match your request are shown. You can also continue typing for more suggestions.

Each query returns a Copilot summary to help you understand the results and offers suggestions. With this information, you can also:

- Add devices or users from the results to a group so you can target apps and policies to this group.
- Filter example queries to find or build requests that match your needs.

To learn more, see [Explore Intune data with natural language and take action](../copilot/explorer.md).

### Device security

#### Microsoft Tunnel access by rooted Android devices is blocked by the Microsoft Defender client<!-- 30336962 -->

Microsoft Tunnel uses the Microsoft Defender client app to provide Android devices access to tunnel. The latest version of the Defender for Endpoint client can now detect when a device is rooted. If a device is determined to be rooted, Defender:

- Marks the device's risk category as *High*
- Immediately drops active Tunnel connections
- Prevents further use of Tunnel until the device is determined to no longer be rooted
- Sends a notification to the device user about the device status

This capability is a feature of the Defender client on Android and doesn't replace the use of Intune compliance policies for Android to manage the settings like *Rooted devices*, *Play Integrity Verdict*, and *Require the device to be at or under the Device Threat Level*.

For more information about features of Microsoft Tunnel, see [Overview of Microsoft Tunnel](../device-security/microsoft-tunnel/overview.md#capabilities).

### Tenant administration

#### Soft-deleted Microsoft Entra groups now visible in Intune <!-- 30035949 -->

This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).

Microsoft Intune now displays soft-deleted Microsoft Entra groups in the Intune admin center. When a group is soft-deleted, its assignments no longer apply. However, if the group is restored, its previous assignments are automatically reinstated.

For more information, see [Include and exclude app assignments in Microsoft Intune](../app-management/deployment/configure-assignment-scope.md).

## Week of October 20, 2025 (Service release 2510)

### Microsoft Intune Suite

#### Support for user account context in Endpoint Privilege Management Elevation Rules<!-- 25617968 -->

Endpoint Privilege Management (EPM) has a new option for elevation rules that runs the elevated file using the user's context instead of a virtual account. The option is **Elevate as current user**.

With the *Elevate as current user* elevation type, files or processes that are elevated run under the signed-in user's own account, rather than a virtual account. This preserves the user's profile paths, environment variables, and personalized settings, helping to ensure that installers and tools that rely on the active user profile function correctly. Because the elevated process maintains the same user identity before and after elevation, audit trails remain consistent and accurate. Prior to elevation, the user is required to enter their credentials for Windows Authentication. This process supports multifactor authentication (MFA) for enhanced security.

For more information, see [Use Endpoint Privilege Management with Microsoft Intune](../epm/deployment-planning.md#important-concepts-for-endpoint-privilege-management).

####  Endpoint Privilege Management Dashboard for user readiness and elevation trends<!-- 26123334 -->

You can now use an Endpoint Privilege Management (EPM) dashboard that presents insights about file elevations and trends in your organization and help identify users that might be ready to be moved to run as standard users in place of running with local admin permissions.

Insights provided by the dashboard include:

- Users who have only unmanaged file elevations
- Users who have both managed and unmanaged file elevations
- User with only managed elevations
- Frequently unmanaged elevations
- Frequently approved by support
- Frequently denied elevations

For more information about the dashboard and these new insights, see [Overview dashboard](../epm/monitor-reports.md#elevation-report-by-user) in Reports for Endpoint Privilege Management.

### Device configuration

#### System Info property available in properties catalog for device inventory<!-- 30326613 -->

You can create a [properties catalog](../device-configuration/collect-device-properties.md) policy that lets you collect and view hardware properties from your managed Windows devices. There's a **System Info** category that shows system-level device insights, like OS version, hardware details, and configuration state.

To learn more and get started, see [properties catalog](../device-configuration/collect-device-properties.md).

> [!div class="checklist"]
> Applies to:
>
>-  Windows

#### New settings available in the Android Enterprise settings catalog<!-- 31495587 34438509 34458121 -->

There are new settings in the Android settings catalog. To create a new settings catalog policy and see these settings in the Intune admin center, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type.

- **Wi-Fi Direct**

  - **General** > **Block Wi-Fi Direct**: If **True**, this setting blocks Wi-Fi Direct. Wi-Fi Direct is a direct, peer-to-peer connection between devices using Wi-Fi frequencies.  If **False**, Intune doesn't change or update this setting. By default, the OS might allow Wi-Fi Direct.

   > [!div class="checklist"]
   > Applies to:
   >
   > - Android Enterprise corporate-owned devices with a work profile (COPE)
   > - Android Enterprise corporate owned fully managed (COBO)
   > - Android Enterprise corporate owned dedicated devices (COSU)

- **Hide organization name**

  The **General** > **Hide organization name** setting supports corporate owned single use dedicated devices. Previously, this setting was only supported on corporate-owned devices with a work profile and corporate owned fully managed devices.

- Some settings that were only available in Templates are available in the settings catalog.

  **General**: 

  - Allow copy and paste between work and personal profiles
  - Allow network escape hatch
  - Allow USB storage
  - Block access to status bar
  - Block date and time changes
  - Block location
  - Block microphone adjustment
  - Block mounting of external media
  - Block notification windows
  - Block screen capture (work profile-level)
  - Block Wi-Fi setting changes

To learn more about these settings, see [Android Intune settings catalog settings list](../device-configuration/settings-catalog/ref-android-settings.md).

The [settings catalog](../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../device-configuration/settings-catalog/index.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

### Device enrollment

#### Edit managed Google Play organization name<!--32268351 -->

Now you can edit the managed Google Play organization name directly in the Microsoft Intune admin center under **Devices** > **Android** > **Enrollment** > **Managed Google Play**. The updated name, which is validated on input, appears in the admin center. It might also appear on Android device lock screens within a message like, *This device is managed by [organization name]*. For more information, see [Connect Intune account to managed Google Play account](../device-enrollment/android/connect-managed-google-play.md).

### Device management

#### Settings catalog supports Windows 11 25H2 settings <!--35412243-->

The release of Windows 11 25H2 includes new policy configuration service providers (CSPs). These settings are available in the [settings catalog](../device-configuration/settings-catalog/common-tasks.md) for you to configure.

To learn more, see the [Microsoft Intune Settings Catalog Updated to Support New Windows 11, version 25H2 Settings](https://aka.ms/Intune/Windows25H2-settings) blog post.

To get started with the settings catalog, see:

- [Use the Intune settings catalog to configure settings](../device-configuration/settings-catalog/index.md)
- [Common tasks you can complete using the settings catalog](../device-configuration/settings-catalog/common-tasks.md)

> [!div class="checklist"]
> Applies to:
>
> - Windows

#### New client version for Remote Help for macOS <!-- 35620986 -->

With the new Remote Help client, version 1.0.2510071, Microsoft Intune now supports macOS 26. Earlier versions of the Remote Help client aren't compatible with macOS 26. The app is automatically updated through Microsoft AutoUpdate (MAU) if opted-in, so no action is required from you or your users. The latest client version resolves an issue that previously caused the screen to appear blank on first launch and fail to connect. For more information, see [Use Remote Help with Microsoft Intune](../remote-help/index.md?tabs=macos).

### Device security

#### Intune to end support for legacy Apple MDM software updates<!-- 33004946 -->

With the release of iOS 26, iPadOS 26, and macOS 26, Apple has deprecated legacy mobile device management (MDM) software update commands and payloads. To align with this change, Intune will soon end support for the following MDM-based workloads:

- iOS/iPadOS update policies
- macOS update policies
- Software update settings in:
  - iOS/iPadOS **templates** > **Device restrictions**
  - iOS/iPadOS **settings catalog** > **Restrictions**
  - macOS **templates** > **Device restrictions**
  - macOS **settings catalog** > **Restrictions**
  - macOS **settings catalog** > **Software update**
- Reports:
  - iOS/iPadOS update installation failures
  - macOS update installation failures
  - macOS per-device software updates

These functionalities [are now available through declarative device management (DDM)](../device-updates/apple/index.md), which provides a more modern and reliable approach to managing Apple software updates. For more information about this transition, see the Intune Customer Success blog [Move to declarative device management for Apple software updates](https://aka.ms/Intune/Apple-DDM-software-updates).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

### Intune apps

#### Newly available protected apps for Intune<!-- 33926210, 33926415, 34631356, 34631695, 34631844, 34632442  -->

The following protected apps are now available for Microsoft Intune:

- Total Triage by CareXM
- Intapp by Intapp Inc.
- ANDPAD by ANDPAD Inc.
- ANDPAD CHAT by ANDPAD Inc.
- ANDPAD Inspection by ANDPAD Inc.
- ANDPAD Blueprint by ANDPAD Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../app-management/ref-protected-apps.md).

### Monitor and troubleshoot

#### Enrollment time grouping failure report generally available for Android and Windows <!-- 33290045 -->

Now generally available in the Microsoft Intune admin center, the enrollment time grouping failures report shows failures, which include devices that failed to become a member of the specified static device group during one of the following processes:

- Windows Autopilot device preparation provisioning
- Enrollment of Android Enterprise fully managed devices
- Enrollment of Android corporate-owned work profile devices 
- Enrollment of Android Enterprise dedicated devices 

The enrollment time grouping failures report is available in the admin center under **Devices** > **Monitor** > **Enrollment time grouping failures**. Recently updated information could take up to 20 minutes to appear in the report. For more information, see [Enrollment time grouping in Microsoft Intune](../device-enrollment/setup-time-grouping.md#reporting).

## What's new archive
<!-- Past announcements that are older than six months will be moved to the archive -->

For previous months, see the [What's new archive](archive/index.md).

## Notices

[!INCLUDE [Intune notices](./includes/intune-notices.md)]
