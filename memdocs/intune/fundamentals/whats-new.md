---
# required metadata
title: What's new in Microsoft Intune
titleSuffix:
description: Find out what's new in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/06/2024
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
> Each [monthly update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) can take up to three days to rollout and will be in the following order:
>
> - Day 1: Asia Pacific (APAC)
> - Day 2: Europe, Middle East, Africa (EMEA)
> - Day 3: North America
> - Day 4+: Intune for Government
>
> Some features roll out over several weeks and might not be available to all customers in the first week.
>
> For a list of upcoming Intune feature releases, see [In development for Microsoft Intune](../fundamentals/in-development.md). For new information about Autopilot, see [Windows Autopilot What's new](/autopilot/windows-autopilot-whats-new).

You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).

## Week of May 6, 2024

### Device management

#### Intune and the macOS Company Portal app support Platform SSO (public preview)<!-- 24325427 -->

On Apple devices, you can use Microsoft Intune and the Microsoft Enterprise SSO plug-in to configure single sign-on (SSO) on for apps and websites that support Microsoft Entra authentication, including Microsoft 365.

On macOS devices, Platform SSO is available in public preview. Platform SSO expands the SSO app extension by allowing you to configure different authentication methods, simplify the sign-in process for users, and reduce the number of passwords they need to remember.

Platform SSO is included in the Company Portal app version 5.2404.0 and newer.

For more information on Platform SSO and to get started, go to:

- [Configure Platform SSO for macOS devices in Microsoft Intune](../configuration/platform-sso-macos.md)
- [Single sign-on (SSO) overview and options for Apple devices in Microsoft Intune](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)

Applies to:

- macOS 13 and later

## Week of April 29, 2024

### App management

<<<<<<< Updated upstream
#### Updates to the Managed Home Screen experience 
We recently released and improved the Managed Home Screen experience, which is now Generally Available. The app has been redesigned to improve the core workflows throughout the application. The updated design offers a more usable and supportable experience. 
=======
#### Updates to the Managed Home Screen experience<!-- 24990268 --> 
We recently released and improved the Managed Home Screen experience, which is now Generally Available. The app has been redesigned to improve the core workflows throughout the application. The updated design offers a more usable and supportable experience.
>>>>>>> Stashed changes

With the release, we stop investing in previous Managed Home Screen workflows. New features and fixes for Managed Home Screen are only added to the new experience. During August 2024, the new experience will automatically be enabled for all devices.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md) and [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

<<<<<<< Updated upstream
#### Require end users to enter PIN to resume activity on Managed Home Screen
=======
#### Require end users to enter PIN to resume activity on Managed Home Screen<!-- 9322838 -->
>>>>>>> Stashed changes
In Intune, you can require end users to enter their session PIN to resume activity on Managed Home Screen after the device has been inactive for a specified period of time. Set the **Minimum inactive time before session PIN is required** setting to the number of seconds the device is inactive before the end user must input their session PIN. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Device IPv4 and IPv6 details available from Managed Home Screen
IPv4 and IPv6 connectivity details are now both available from the **Device Information** page of the Managed Home Screen app. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](..\remote-actions\collect-diagnostics.md).

<<<<<<< Updated upstream
#### Updates to Managed Home Screen sign-in support
Managed Home Screen now supports domainless sign-in. Admins can configure a domain name, which will be automatically appended to usernames upon sign-in. Also, Managed Home Screen supports a custom login hint text to be displayed to users during the sign-in process.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md) and [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

#### Allow end users to control Android Enterprise device auto-rotation
=======
#### Updates to Managed Home Screen sign-in support<!-- 24990268 -->
Managed Home Screen now supports domainless sign-in. Admins can configure a domain name, which will be automatically appended to usernames upon sign-in. Also, Managed Home Screen supports a custom sign-in hint text to be displayed to users during the sign-in process.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md) and [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

#### Allow end users to control Android Enterprise device auto-rotation<!-- 9322838 -->
>>>>>>> Stashed changes
In Intune, you can now expose a setting in the Managed Home Screen app, which will allow the end user to turn on and off the device's auto-rotation. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Allow end users to adjust Android Enterprise device screen brightness
In Intune, you can expose settings in the Managed Home Screen app to adjust screen brightness for Android Enterprise devices. You can choose to expose a setting in the app to allow end users to access a brightness slider to adjust the device screen brightness. Also, you can expose a setting to allow end users to toggle adaptive brightness. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

<<<<<<< Updated upstream
#### Migrated to .NET MAUI from Xamarin
=======
#### Migrated to .NET MAUI from Xamarin<!-- 27143739 -->
>>>>>>> Stashed changes
Xamarin.Forms has evolved into .NET Multi-platform App UI (MAUI). Existing Xamarin projects should be migrated to .NET MAUI. For more information about upgrading Xamarin projects to .NET, see the [Upgrade from Xamarin to .NET & .NET MAUI](/dotnet/maui/migration/?WT.mc_id=dotnet-35129-website) documentation.

Xamarin support ended as of May 1, 2024 for all Xamarin SDKs including Xamarin.Forms and Intune App SDK Xamarin Bindings. For Intune support on Android and iOS platforms, see [Intune App SDK for .NET MAUI - Android](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android)and [Microsoft Intune App SDK for MAUI.iOS](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS).

## Week of April 22, 2024 (Service release 2404)

### App management

#### Auto update available with Win32 app supersedence

Win32 app supersedence provides the capability to supersede apps deployed as available with **auto-update** intent. For example, if you deploy a Win32 app (app A) as available and installed by users on their device, you can create a new Win32 app (app B) to supersede app A using **auto-update**. All targeted devices and users with app A installed as available from the Company Portal are superseded with app B. Also, only app B shows in the Company Portal. You can find the **auto-update** feature for available app supersedence as a toggle under the **Available assignment** in the **Assignments** tab.

For more information about app supersedence, see [Add Win32 app supersedence](../apps/apps-win32-supersedence.md).

### Device configuration

#### Error message is shown when OEMConfig policy exceeds 500 KB on Android Enterprise devices

On Android Enterprise devices, you can use an OEMConfig device configuration profile to add, create and/or customize OEM specific settings.

When you create an OEMConfig policy that exceeds 500 KB, then the following error is shown in the Intune admin center:

`Profile is larger than 500KB. Adjust profile settings to decrease the size.`

Previously, OEMConfig policies that exceeded 500 KB were shown as pending.

For more information on OEMConfig profiles, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Applies to:

- Android Enterprise

### Device security

#### Windows Firewall CSP changes for processing Firewall Rules

Windows changed how the Firewall configuration service provider (CSP) enforces rules from Atomic blocks of firewall rules. The Windows Firewall CSP on a device implements the firewall rule settings from your [Intune endpoint security Firewall policies](../protect/endpoint-security-firewall-policy.md). The change of CSP behavior now enforces an all-or-nothing application of firewall rules from each Atomic block of rules.

- Previously, the CSP on a device would go through the firewall rules in an Atomic block of rules - one rule (or setting) at a time with the goal of applying all the rules in that Atomic block, or none of them. If the CSP encountered any issue with applying any rule from the block to the device, the CSP wouldn't only stop that rule, but also cease to process subsequent rules without trying to apply them. However, rules that applied successfully before a rule failed, would remain applied to the device. This behavior can lead to a partial deployment of firewall rules on a device, since the rules that were applied before a rule failed to apply aren't reversed.

- With the change to the Firewall CSP, when any rule in the block is unsuccessful in applying to the device, all the rules from that same Atomic block that were applied successfully are rolled back. This behavior ensures the desired all-or-nothing behavior is implemented and prevents a partial deployment of firewall rules from that block. For example, if a device receives an Atomic block of firewall rules that has a misconfigured rule that can't apply, or has a rule that isn't compatible with the devices operating system, then the CSP fails all the rules from that block, And, it rolls back any rules that applied to that device.

This change of Firewall CSP behavior is available on devices that run the following Windows versions or later:

- Windows 11 21H2
- Windows 11 22H2
- Windows 10 21H2

For more information on the subject of how the Windows Firewall CSP uses Atomic blocks to contain firewall rules, see the note near the top of [Firewall CSP](/windows/client-management/mdm/firewall-csp) in the Windows documentation.

For troubleshooting guidance, see the Intune support blog [How to trace and troubleshoot the Intune Endpoint Security Firewall rule creation process](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-trace-and-troubleshoot-the-intune-endpoint-security/ba-p/3261452).

#### CrowdStrike – New mobile threat defense partner

We added [CrowdStrike Falcon](../protect/crowdstrike-falcon-defense-connector.md) as an integrated Mobile Threat Defense (MTD) partner with Intune. By configuring the CrowdStrike connector in Intune, you can control mobile device access to corporate resources using Conditional Access that's based on risk assessment in your compliance policies.

<<<<<<< Updated upstream
With the Intune 2404 service release, the CrowdStrike connector is now available in the admin center. However, it isn't useable until CrowdStrike publishes the required App Configuration profile details necessary to support iOS and Android devices. The profile details are expected sometime after second week of May.
=======
With the Intune 2404 service release, the CrowdStrike connector is now available in the admin center. However, it isn't useable until CrowdStrike publishes the required App Configuration profile details necessary to support iOS and Android devices. The profile details is expected sometime after second week of May.
>>>>>>> Stashed changes

### Intune apps

#### Newly available protected apps for Intune

The following protected apps are now available for Microsoft Intune:

- Asana: Work in one place by Asana, Inc.
- Freshservice for Intune by Freshworks, Inc.
- Kofax Power PDF Mobile by Tungsten Automation Corporation
- Remote Desktop by Microsoft Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Windows update distribution report

The Windows update distribution report in Intune provides a summarized report. This report shows:

- The number of devices that are on each quality update level.
- The percentage of coverage for each update across Intune managed devices, including co-managed devices.

You can drill down further in the report for each quality update that aggregates devices based on the Windows 10/11 feature version and the update statuses.

Finally, the admins can get the list of devices that aggregate to the numbers shown in the previous two reports, which can also be exported and used for troubleshooting and analysis along with the Windows Update for business reports.

For more information on Windows update distribution reports, see [Windows Update reports on Intune](../protect/windows-update-reports.md#windows-update-distribution-report).

#### Intune support of Microsoft 365 remote application diagnostics

The Microsoft 365 remote application diagnostics allows Intune admins to request Intune app protection logs and Microsoft 365 application logs (where applicable) directly from the Intune console. You can find this report in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Troubleshoot** > *select a user* > **Summary** > *App protection**. This feature is exclusive to applications that are under Intune app protection management. If supported, the application specific logs are gathered and stored within dedicated storage solutions for each application.

For more information, see [Collect diagnostics from an Intune managed device](../remote-actions/collect-diagnostics.md).

#### Remote Help supports full control of a macOS device

Remote Help now supports helpdesk connecting to a user's device and requesting full control of the macOS device.

For more information, see:

- [Remote Help on macOS](../fundamentals/remote-help-macos.md)
- [Remote Help Web App](../fundamentals/remote-help-webapp.md)

Applies to:

- macOS 12, 13 and 14

## Week of April 15, 2024

### Intune apps

#### Newly available protected app for Intune

The following protected app is now available for Microsoft Intune:

- Atom Edge by Arlanto Apps

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of April 1, 2024

### Device management

#### Copilot in Intune is available in the Intune admin center (public preview)

Copilot in Intune is integrated in the Intune admin center, and can help you get information quickly. You can use Copilot in Intune for the following tasks:

✅ **Copilot can help you manage your settings and policies**

- **Copilot tooltip on settings**: When you add settings to a policy or review settings in an existing policy, there's a new Copilot tooltip. When you select the tooltip, you get AI generated guidance based on Microsoft content and recommendations. You can see what each setting does, how the setting works, any recommended values, if the setting is configured in another policy, and more.

- **Policy summarizer**: On existing policies, you get a Copilot summary of the policy. The summary describes what the policy does, the users and groups assigned to the policy, and the settings in the policy. This feature can help you understand the impact of a policy and its settings on your users and devices.

✅ **Copilot shows device details and can help troubleshoot**

- **All about a device**: On a device, you can use Copilot to get key information about the device, including its properties, configuration, and status information.

- **Device compare**: Use Copilot to compare the hardware properties and device configurations of two devices. This feature helps you determine what's different between two devices with similar configurations, especially when troubleshooting.

- **Error code analyzer**: Use Copilot in the device view to analyze an error code. This feature helps you understand what the error means and provides a potential resolution.

✅ **Intune capabilities in Copilot for Security**

Intune has capabilities available in the Copilot for Security portal. SOC Analysts and IT admins can use these capabilities to get more information on policies, devices, group membership, and more. On a single device, you can get more specific information that's unique to Intune, like compliance status, device type, and more.

You can also ask Copilot to tell you about a user's devices and get a quick summary of critical information. For example, the output shows links to the user's devices in Intune, device ID, enrollment date, last check-in date, and compliance status. If you're an IT admin and reviewing a user, then this data provides a quick summary.

As a SOC analyst that's investigating a suspicious or potentially compromised user or device, information like enrollment date and last check-in can help you make informed decisions.

For more information on these features, see:

- [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md)
- [Access your Microsoft Intune data in Copilot for Security](../copilot/security-copilot.md)

Applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

#### GCC customers can use Remote Help for Windows and Android devices

The [Microsoft Intune Suite](intune-add-ons.md) includes advanced endpoint management and security features, including Remote Help.

On Windows and enrolled Android Enterprise dedicated devices, you can use remote help on US Government GCC environments.

For more information on these features, see:

- [Microsoft Intune for US Government GCC service description](intune-govt-service-description.md)
- [Use Remote Help with Microsoft Intune](remote-help.md)

Applies to:

- Windows 10/11
- Windows 10/11 on ARM64 devices
- Windows 365
- Samsung and Zebra devices enrolled as Android Enterprise dedicated devices

### Device configuration

#### New BIOS device configuration profile for OEMs

There's a new **BIOS configuration and other settings** device configuration policy for OEMs. Admins can use this new policy to enable or disable different BIOS features that secure device. In the Intune device configuration policy, you add the BIOS configuration file, deploy a Win32 app, and then assign the policy to your devices.

For example, admins can use the [Dell Command tool](https://www.dell.com/support/kbdoc/000108963/how-to-use-and-troubleshoot-dell-command-update-to-update-all-drivers-bios-and-firmware-for-your-system) (opens Dell's website) to create the BIOS configuration file. Then, they add this file to the new Intune policy.

For more information on this feature, see [Use BIOS configuration profiles on Windows devices in Microsoft Intune](../configuration/bios-configuration.md).

Applies to

- Windows 10 and later

## Week of March 25, 2024 (Service release 2403)

### Microsoft Intune Suite

#### New elevation type for Endpoint Privilege Management

Endpoint Privilege Management has a new file elevation type, **support approved**. Endpoint Privilege Management is a feature component of the Microsoft Intune Suite and is also available as a standalone [Intune add-on](../fundamentals/intune-add-ons.md).

A support-approved elevation gives you a third option for both the default elevation response and the elevation type for each rule. Unlike automatic or user confirmed, a support-approved elevation request requires Intune administrators to manage which files can run as elevated on a case-by-case basis.

With support approved elevations, users can request approval to elevate an application that isn't explicitly allowed for elevation by automatic or user approved rules. This takes the form of an elevation request that must be reviewed by an Intune administrator who can approve or deny the elevation request.

When the request is approved, users are notified that the application can now be run as elevated, and they have 24 hours from the time of approval to do so before the elevation approval expires.

Applies to:

- Windows 10
- Windows 11

For more information on this new capability, see [Support approved elevation requests](../protect/epm-support-approved.md).

### App management

#### Extended capabilities for Managed Google Play apps on personally owned Android devices with a work profile

There are new capabilities extended to work profile devices. The following capabilities were previously available only on corporate-owned devices:

- **Available apps for device groups**: You can use Intune to make apps available for device groups through the Managed Google Play store. Previously, apps could only be made available to user groups.

- **Update priority setting**: You can use Intune to configure the app update priority on devices with a work profile. To learn more about this setting, see [Update a Managed Google Play app](../apps/apps-add-android-for-work.md#update-a-managed-google-play-app).

- **Required apps display as available in Managed Google Play**: You can use Intune to make required apps available for users through the Managed Google Play store. Apps that are part of existing policies now display as available.

These new capabilities will follow a phased rollout over multiple months.

Applies to:

- Android Enterprise personally owned devices with a work profile

### Device configuration

#### New settings available in the Apple settings catalog

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Declarative Device Management (DDM) > Passcode**:

- Maximum Passcode Age In Days
- Minimum Complex Characters
- Require Alphanumeric Passcode

**Restrictions**:

- Allow Marketplace App Installation

##### macOS

**Declarative Device Management (DDM) > Passcode**:

- Change At Next Auth
- Custom Regex
- Failed Attempts Reset In Minutes
- Maximum Passcode Age In Days
- Minimum Complex Characters
- Require Alphanumeric Passcode

**Full Disk Encryption > FileVault**:

- Recovery Key Rotation In Months

#### New settings available in the Windows settings catalog

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **Windows 10 and later** for platform > **Settings catalog** for profile type.

- **Delivery optimization**:

  - **DO Disallow Cache Server Downloads On VPN** - This setting blocks downloads from Microsoft Connected Cache servers when the device connects using VPN. By default, the device is allowed to download from Microsoft Connected Cache when connected using VPN.

  - **DO Set Hours To Limit Background Download Bandwidth** - This setting specifies the maximum background download bandwidth. Delivery Optimization uses this bandwidth during and outside business hours across all concurrent download activities as a percentage of available download bandwidth.

  - **DO Set Hours To Limit Foreground Download Bandwidth** - This setting specifies the maximum foreground download bandwidth. Delivery Optimization uses this bandwidth during and outside business hours across all concurrent download activities as a percentage of available download bandwidth.

  - **DO Vpn Keywords** - This policy allows you to set one or more keywords used to recognize VPN connections.

- **Messaging**:

  - **Allow Message Sync** - This policy setting allows the backup and restore of cellular text messages to Microsoft's cloud services.

- **Microsoft Defender Antivirus**:

  - **Specify the maximum depth to scan archive files**
  - **Specify the maximum size of archive files to be scanned**

For more information on these settings, see:

- [Policy CSP - DeliveryOptimization](/windows/client-management/mdm/policy-csp-deliveryoptimization)
- [Policy CSP - Messaging](/windows/client-management/mdm/policy-csp-messaging#allowmessagesync)
- [Policy CSP - ADMX_MicrosoftDefenderAntivirus](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus)

Applies to:

- Windows 10 and later

#### New archive file scan settings added to Antivirus policy for Windows devices

We added the following two settings to the *Microsoft Defender Antivirus* profile for [endpoint security Antivirus policy](../protect/endpoint-security-antivirus-policy.md#antivirus-profiles) that apply to Windows 10 and Windows 11 devices:

- [Specify the maximum depth to scan archive files](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#scan_archivemaxdepth) - This setting allows you to configure the maximum directory depth level into which archive files such as .ZIP or .CAB are unpacked during scanning.
- [Specify the maximum size of archive files to be scanned](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#scan_archivemaxsize) - This setting allows you to configure the maximum size of archive files such as .ZIP or .CAB that are scanned. The value represents file size in kilobytes (KB).

With Antivirus policy, you can manage these settings on devices enrolled by Intune and on devices managed through the [Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario.

Both settings are also available in the [settings catalog](../configuration/settings-catalog.md) at **Devices** > **Configuration** > **Create** > **Windows 10 and later** for platform > **Settings catalog** for profile type > **Defender**.

Applies to:

- Windows 10
- Windows 11

#### Updates to assignment filters

You can use [Intune assignment filters](filters.md) to assign a policy based on rules you create.

Now, you can:

- Use managed app assignment filters for Window MAM app protection policies and app configuration policies.
- Filter your existing assignment filters by **Platform**, and by the **Managed apps** or **Managed devices** filter type. When you have many filters, this feature makes it easier to find specific filters you created.

For more information on these features, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [Data protection for Windows MAM](../apps/protect-mam-windows.md)

This feature applies to:

- **Managed devices** on the following platforms:

  - Android device administrator
  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - macOS
  - Windows 10/11

- **Managed apps** on the following platforms:

  - Android
  - iOS/iPadOS
  - Windows

### Device management

#### New compliance setting lets you verify device integrity using hardware-backed security features

A new compliance setting called **Check strong integrity using hardware-backed security features** lets you verify device integrity using hardware-backed key attestation. If you configure this setting, strong integrity attestation is added to Google Play's integrity verdict evaluation. Devices must meet device integrity to remain compliant. Microsoft Intune marks devices that don't support this type of integrity check as noncompliant.

This setting is available in profiles for Android Enterprise fully managed, dedicated, and corporate-owned work profile, under **Device Health** > **Google Play Protect**. It only becomes available when the Play integrity verdict policy in your profile is set to **Check basic integrity** or **Check basic integrity & device integrity**.

Applies to:

- Android Enterprise

For more information, see [Device compliance - Google Play Protect](../protect/compliance-policy-create-android-for-work.md#google-play-protect).

#### New compliance settings for Android work profile, personal devices

Now you can add compliance requirements for work profile passwords without impacting device passwords. All new Microsoft Intune settings are available in compliance profiles for Android Enterprise personally owned work profiles under **System Security** > **Work Profile Security**, and include:

- Require a password to unlock work profile
- Number of days until password expires
- Number of previous passwords to prevent reuse
- Maximum minutes of inactivity before password is required
- Password complexity
- Required password type
- Minimum password length

If a work profile password fails to meet requirements, Company Portal marks the device as noncompliant. Intune compliance settings take precedence over the respective settings in an Intune device configuration profile. For example, the password complexity in your compliance profile is set to *medium*. The password complexity in a device configuration profile is set to *high*. Intune prioritizes and enforces the compliance policy.

Applies to:

- Android Enterprise personally owned devices with a work profile

For more information, see [Compliance settings - Android Enterprise](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile).

#### Windows quality updates support for expediting non-security updates

Windows quality updates now support expediting non-security updates for those times when a quality fix needs to be deployed faster than the normal quality update settings.

Applies to:

- Windows 11 devices

For more information about installing an expedited update, see [Expedite Windows quality updates in Microsoft Intune](../protect/windows-10-expedite-updates.md#create-and-assign-an-expedited-quality-update).

#### Introducing a remote action to pause the config refresh enforcement interval

In the Windows Settings Catalog, you can configure **Configuration Refresh**. This feature lets you set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check in to Intune. The device will replay and re-enforce settings based on previously received policy to minimize the chance for configuration drift.

To support this feature, a remote action is added to allow a pause in action. If an admin needs to make changes or run remediation on a device for troubleshooting or maintenance, they can issue a pause from Intune for a specified period. When the period expires, settings are enforced again.

The remote action **Pause configuration refresh** can be accessed from the device summary page.

For more information, see:

- [Remote actions](../remote-actions/device-management.md)
- [Pause Config Refresh Remote action](../remote-actions/pause-config-refresh.md)

### Device security

#### Updated security baseline for Windows version 23H2

You can now deploy the Intune security baseline for Windows version 23H2. This new baseline is based on the **version 23H2** of the Group Policy security baseline found in the [Security Compliance Toolkit and Baselines](https://www.microsoft.com/en-us/download/details.aspx?id=55319) from the Microsoft Download Center, and includes only the settings that are applicable to devices managed through Intune. Use of this updated baseline can help you maintain best-practice configurations for your Windows devices.

This baseline uses the unified settings platform seen in the Settings Catalog. It features an improved user interface and reporting experience, consistency and accuracy improvements related to setting tattooing, and can support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft. As with all baselines, the default baseline represents the recommended configurations, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

To view the new baselines included settings with their default configurations, see, [Windows MDM security baseline version 23H2](../protect/security-baseline-settings-mdm-all.md?pivots=mdm-23h2).

#### Use a rootless implementation of Podman to host Microsoft Tunnel

When prerequisites are met, you can use a rootless Podman container to host a Microsoft Tunnel server. This capability is available when you use [Podman for Red Hat Enterprise Linux (RHEL)](../protect/microsoft-tunnel-prerequisites.md#linux-server) version 8.8 or later, to host Microsoft Tunnel.

When using a rootless Podman container, the mstunnel services run under a non-privileged service user. This implementation can help limit impact from a container escape. To use a rootless Podman container, you must start the tunnel installation script using a modified command line.

For more information about this Microsoft Tunnel install option, see [Use a rootless Podman container](../protect/microsoft-tunnel-configure.md#use-a-rootless-podman-container).

#### Improvements for Intune deployments of Microsoft Defender for Endpoint

We improved and simplified the experience, workflow, and report details for onboarding devices to Microsoft Defender when using Intune's endpoint detection and response (EDR) policy. These changes apply for Windows devices managed by Intune and by the tenant-attach scenario. These improvements include:

- Changes to the EDR node, dashboards, and reports to improve the visibility of your Defender EDR deployment numbers. See [About the endpoint detection and response node](../protect/endpoint-security-edr-policy.md#about-the-endpoint-detection-and-response-node).

- A new tenant-wide option to deploy a preconfigured EDR policy that streamlines the deployment of Defender for Endpoint to applicable Windows devices. See [Use a preconfigured EDR policy](../protect/endpoint-security-edr-policy.md#use-a-preconfigured-edr-policy).

- Changes to Intune's the Overview page of the endpoint security node. These changes provide a consolidated view of reports for the device signals from Defender for Endpoint on your managed devices. See [Use a preconfigured EDR policy](../protect/endpoint-security-edr-policy.md#use-a-preconfigured-edr-policy).

These changes apply to the Endpoint security and endpoint detection and response nodes of the admin center, and the following device platforms:

- Windows 10
- Windows 11

#### Windows quality updates will support expediting non-security updates

Windows quality updates now support expediting non-security updates for those times when a quality fix needs to be deployed faster than the normal quality update settings.

Applies to:

- Windows 11 devices

For more information about installing an expedited update, see [Expedite Windows quality updates in Microsoft Intune](../protect/windows-10-expedite-updates.md#create-and-assign-an-expedited-quality-update).

### Intune apps

#### Newly available protected apps for Intune

The following protected apps are now available for Microsoft Intune:

- Cerby by Cerby, Inc.
- OfficeMail Go by 9Folders, Inc.
- DealCloud by Intapp, Inc.
- Intapp 2.0 by Intapp, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of March 3, 2024

### Device enrollment

#### Role-based access control changes to enrollment settings for Windows Hello for Business

We updated Role-based access control (RBAC) in the enrollment area for Windows Hello for Business. Enrollment settings related to Windows Hello for Business are read-only for all roles except the Intune Service Administrator. The Intune Service Administrator can create and edit Windows Hello for Business enrollment settings.

For more information, see [Role-based access control](../protect/windows-hello.md#role-based-access-control) in the *Windows Hello at device enrollment* article.

### Device security

#### New enrollment configuration for Windows Hello for Business

A new Windows Hello for Business enrollment setting, **Enable enhanced sign in security** is available in the Intune admin center. Enhanced sign-in security is a Windows Hello feature that prevents malicious users from gaining access to a user's biometrics through external peripherals.

For more information about this setting, see [Create a Windows Hello for Business policy](../protect/windows-hello.md#create-a-windows-hello-for-business-policy).

#### HTML formatting supported in noncompliance email notifications

Intune now supports HTML formatting in noncompliance email notifications for all platforms. You can use supported HTML tags to add formatting such as italics, URL links, and bulleted lists to your organization's messages.

For more information, see [Create a notification message template](../protect/actions-for-noncompliance.md#create-a-notification-message-template).

## Week of February 26, 2024

### Microsoft Intune Suite

#### New Microsoft Cloud PKI service

Use the Microsoft Cloud PKI service to simplify and automate certificate lifecycle management for Intune-managed devices. ​Microsoft Cloud PKI is a feature component of the Microsoft Intune Suite and is also available as a standalone [Intune add-on](../fundamentals/intune-add-ons.md). The cloud-based service provides a dedicated PKI infrastructure for your organization, and doesn't require on-premises servers, connectors, or hardware. Microsoft Cloud PKI automatically issues, renews, and revokes certificates for all OS platforms supporting the SCEP certificate device configuration profile. Issued certificates can be used for certificate-based authentication for Wi-Fi, VPN, and other services supporting certificate-based authentication. For more information, see [Overview of Microsoft Cloud PKI](../protect/microsoft-cloud-pki-overview.md).

Applies to:

- Windows
- Android
- iOS/iPadOS
- macOS

### Intune apps

#### Newly available protected app for Intune

The following protected app is now available for Microsoft Intune:

- Cinebody by Super 6 LLC

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of February 19, 2024 (Service release 2402)

### App management

#### Additional app configuration permissions for Android apps

There are six new permissions that can be configured for an Android app using an app configuration policy. They are:

- Allow background body sensor data
- Media Video (read)
- Media Images (read)
- Media Audio (read)
- Nearby Wifi Devices
- Nearby Devices

For more information about how to use app config policies for Android apps, see [Add app configuration policies for managed Android Enterprise devices](../apps/app-configuration-policies-use-android.md).

#### Newly available protected apps for Intune

The following protected apps are now available for Microsoft Intune:

- Bob HR by Hi Bob Ltd
- ePRINTit SaaS by ePRINTit USA LLC
- Microsoft Copilot by Microsoft Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

#### Update to Intune Management Extension on Windows

To support expanded functionality and bug fixes, use .NET Framework 4.7.2 or higher with the Intune Management Extension on Windows clients. If a Windows client continues to use an earlier version of the .NET Framework, the Intune Management Extension continues to function. The .NET Framework 4.7.2 is available from Windows Update as of July 10, 2018, which is included in Win10 1809 (RS5) and newer. Multiple versions of the .NET Framework can coexist on a device.

### Device configuration

#### Use assignment filters on Endpoint Privilege Management (EPM) policies

You can use assignment filters to assign a policy based on rules you create. A filter allows you to narrow the assignment scope of a policy, like targeting devices with a specific OS version or a specific manufacturer.

You can use filters on Endpoint Privilege Management (EPM) policies.

For more information, see:

- [Use filters when assigning your apps, policies, and profiles in Intune](filters.md)
- [List of platforms, policies, and app types supported by filters in Intune](filters-supported-workloads.md)

Applies to:

- Windows 10
- Windows 11

#### New settings available in the Apple settings catalog

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

- **Restrictions**

  - Allow Live Voicemail
  - Force Classroom Unprompted Screen Observation
  - Force Preserve ESIM On Erase

##### macOS

- **Full Disk Encryption > FileVault** > Force Enable In Setup Assistant
- **Restrictions** > Force Classroom Unprompted Screen Observation

For more information, see:

- [Use FileVault disk encryption for macOS with Intune](../protect/encrypt-devices-filevault.md)
- [Create a policy using settings catalog](../configuration/settings-catalog.md)

#### Import up to 20 custom ADMX and ADML administrative templates

You can import custom ADMX and ADML administrative templates in Microsoft Intune. Previously, you could import up to 10 files. Now, you can upload up to 20 files.

Applies to:

- Windows 10
- Windows 11

For more information on this feature, see [Import custom ADMX and ADML administrative templates into Microsoft Intune (public preview)](../configuration/administrative-templates-import-custom.md).

#### New setting for updating MAC address randomization on Android Enterprise devices

There's a new **MAC address randomization** setting on Android Enterprise devices (**Devices** > **Configuration** > **Create** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Wi-Fi** for profile type).

Starting with Android 10, when connecting to a network, devices present a randomized MAC address instead of the physical MAC address. Using randomized MAC addresses is recommended for privacy, as it's harder to track a device by its MAC address. However, randomized MAC addresses break functionality that relies on a static MAC address, including network access control (NAC).

Your options:

- **Use device default**: Intune doesn't change or update this setting. By default, when connecting to a network, devices present a randomized MAC address instead of the physical MAC address. Any updates made by the user to the setting persist.

- **Use randomized MAC**: Enables MAC address randomization on devices. When devices connect to a new network, devices present a randomized MAC address, instead of the physical MAC address. If the user changes this value on their device, it resets to **Use randomized MAC** on the next Intune sync.

- **Use device MAC**: Forces devices to present their actual Wi-Fi MAC address instead of a random MAC address. This setting allows devices to be tracked by their MAC address. Only use this value when necessary, such as for network access control (NAC) support. If the user changes this value on their device, it resets to **Use device MAC** on the next Intune sync.

Applies to:

- Android 13 and newer

For more information on the Wi-Fi settings you can configure, see [Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices in Microsoft Intune](../configuration/wi-fi-settings-android-enterprise.md).

#### Turn Off Copilot in Windows setting in the Windows settings catalog

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There's a new setting in the Settings Catalog. To see this setting, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **Windows** for platform > **Settings catalog** for profile type.

- **Windows AI > Turn Off Copilot in Windows (User)**

  - If you enable this policy setting, users can't use Copilot. The Copilot icon won't appear on the taskbar.
  - If you disable or don't configure this policy setting, users can use Copilot when it's available to them.

This setting uses the [Policy CSP - WindowsAI](/windows/client-management/mdm/policy-csp-windowsai).

For more information about configuring Settings Catalog policies in Intune, including user scope vs. device scope, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:

- Windows 10 and later

#### Windows Autopilot self-deploying mode is now generally available

Windows Autopilot self-deploying mode is now generally available and out of preview. Windows Autopilot self-deploying mode enables you to deploy Windows devices with little to no user interaction. Once the device connects to network, the device provisioning process starts automatically: the device joins Microsoft Entra ID, enrolls in Intune, and syncs all device-based configurations targeted to the device. Self-deploying mode ensures that the user can't access desktop until all device-based configuration is applied. The Enrollment Status Page (ESP) is displayed during OOBE so users can track the status of the deployment. For more information, see:

- [Windows Autopilot self-deploying mode](/autopilot/self-deploying)
- [Step by step tutorial for Windows Autopilot self-deploying mode in Intune](/autopilot/tutorial/self-deploying/self-deploying-workflow)

This information is also published in [Windows Autopilot: What's new](/autopilot/windows-autopilot-whats-new).

#### Windows Autopilot for pre-provisioned deployment is now generally available

Windows Autopilot for pre-provisioned deployment is now generally available and out of preview. Windows Autopilot for pre-provisioned deployment is used by organizations that want to ensure devices are business-ready before the user accesses them. With pre-provisioning, admins, partners, or OEMs can access a technician flow from the Out-of-box experience (OOBE) and kick off device setup. Next, the device is sent to the user who completes provisioning in the user phase. Pre-provisioning delivers most the configuration in advance so the end user can get to the desktop faster. For more information, see:

- [Windows Autopilot for pre-provisioned deployment](/autopilot/pre-provision).
- [Step by step tutorial for Windows Autopilot for pre-provisioned deployment Microsoft Entra join in Intune](/autopilot/tutorial/pre-provisioning/azure-ad-join-workflow)
- [Step by step tutorial for Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join in Intune](/autopilot/tutorial/pre-provisioning/hybrid-azure-ad-join-workflow).

This information is also published in [Windows Autopilot: What's new](/autopilot/windows-autopilot-whats-new).

### Device enrollment

#### ESP setting to install required apps during Windows Autopilot pre-provisioning

The setting **Only fail selected blocking apps in technician phase** is now generally available to configure in Enrollment Status Page (ESP) profiles. This setting only appears in ESP profiles that have *blocking apps* selected.

For more information, see  [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md#create-new-profile).

#### New local primary account configuration for macOS automated device enrollment

Configure local primary account settings for Macs enrolling in Intune via Apple automated device enrollment. These settings, supported on devices running macOS 10.11 and later, are available in new and existing enrollment profiles under the new **Account Settings** tab. For this feature to work, the enrollment profile must be configured with user-device affinity and one of the following authentication methods:

- Setup Assistant with modern authentication
- Setup Assistant (legacy)

Applies to:

- macOS 10.11 and later

For more information about macOS account settings, see [Create an Apple enrollment profile in Intune](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile).

#### Await final configuration for macOS automated device enrollment now generally available

Now generally available, *await final configuration* enables a locked experience at the end of Setup Assistant to ensure that critical device configuration policies are installed on devices. The locked experience works on devices targeted with new and existing enrollment profiles, enrolling via one of these authentication methods:

- Setup Assistant with modern authentication
- Setup Assistant (legacy)
- Without user device affinity

Applies to:

- macOS 10.11 and later

For information about how to enable await final configuration, see [Create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile).

### Device management

#### AOSP devices check for new tasks and notifications approximately every 15 minutes

On devices enrolled with Android (AOSP) management, Intune attempts to check for new tasks and notifications approximately every 15 minutes. To use this feature, devices must be using the Intune app version 24.02.4 or newer.

Applies to:

- Android (AOSP)

For more information, see:

- [How to use Intune in environments without Google Mobile Services](../apps/manage-without-gms.md#some-tasks-can-be-delayed)
- [Policy refresh intervals in Intune](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals)

#### New device management experience for Government clouds in Microsoft Intune

In government clouds, there's a new device management experience in the Intune admin center. The **Devices** area now has a more consistent UI, with more capable controls and an improved navigation structure so you can find what you need faster.

If you want to try the new experience before your tenant is updated, go to **Devices** > **Overview**, select the **Preview upcoming changes to Devices and provide feedback** notification banner, and select **Try it now**.

#### Bulk approval of drivers

Bulk actions are now available for Windows Driver update policies.  With bulk actions, multiple driver updates can be approved, paused, or declined at the same time, saving time and effort.  

When you bulk approve drivers, the date for when the drivers become available to applicable devices can also be set, enabling drivers to be installed together.

Applies to:

- Windows 10
- Windows 11

For more information, see [Bulk driver updates](../protect/windows-driver-updates-policy.md#bulk-driver-updates).

#### App Control for Business policy limitation is resolved

A previously documented limitation for App Control for Business policy (WDAC), that limited the number of active policies per device to 32, is resolved by Windows. The issue involves a potential [Boot stop failure when more than 32 policies are active](/windows/security/application-security/application-control/windows-defender-application-control/operations/known-issues#boot-stop-failure-blue-screen-occurs-if-more-than-32-policies-are-active) on a device.

This issue is resolved for devices that run Windows 10 1903 or later with a Windows security update released on or after March 12, 2024. Older versions of Windows can expect to receive this fix in future Windows security updates.

Applies to:

- Windows 10 version 1903 and later

To learn more about App Control for Business policy for Intune, see [Manage approved apps for Windows devices with App Control for Business policy and Managed Installers for Microsoft Intune](../protect/endpoint-security-app-control-policy.md).

### Tenant administration

#### Customization pane support for excluding groups

The Customization pane now supports selecting groups to exclude when assigning policies. You can find this setting in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Customization**.

For more information, see [Assign policies in Microsoft Intune](../configuration/device-profile-assign.md).

## Week of January 29, 2024

### Microsoft Intune Suite

#### Microsoft Intune Enterprise Application Management

Enterprise Application Management provides an Enterprise App Catalog of Win32 applications that are easily accessible in Intune. You can add these applications to your tenant by selecting them from the Enterprise App Catalog. When you add an Enterprise App Catalog app to your Intune tenant, default installation, requirements, and detection settings are automatically provided. You can modify these settings as well. Intune hosts Enterprise App Catalog apps in Microsoft storage.

For more information, see:

- [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md)
- [Microsoft Intune Enterprise Application Management](../apps/apps-enterprise-app-management.md)
- [Add an Enterprise App Catalog app to Microsoft Intune](../apps/apps-add-enterprise-app.md)

#### Microsoft Intune Advanced Analytics

Intune Advanced Analytics provides comprehensive visibility of the end-user experience in your organization and optimizes it with data driven insights. It includes near real-time data about your devices with Device query, increased visibility with custom device scopes, a battery health report and a detailed device timeline for troubleshooting device issues, and anomaly detection to help identify potential vulnerabilities or risks across your device estate.

- **Battery health report**

  The battery health report provides visibility into the health of batteries in your organization's devices and its influence on user experience. The scores and insights in this report are aimed to help IT admins with asset management and purchase decisions that improve user experience while balancing hardware costs.

- **Run on-demand device queries on single devices**

  Intune allows you to quickly gain on-demand information about the state of your device. When you enter a query on a selected device, Intune runs a query in real time.

  The data returned can then be used to respond to security threats, troubleshoot the device, or make business decisions.

  Applies to:

  - Windows devices

Intune Advanced Analytics is part of the Microsoft Intune Suite. For added flexibility, this new set of capabilities, together with the existing Advanced Analytics features, is also now available as an individual add-on to Microsoft subscriptions that include Intune.

To use Device query and battery health report in your tenant, or any of the existing Advanced Analytics capabilities, you must have a license for either:

- The Intune Advanced Analytics add-on
- The Microsoft Intune Suite add-on

For more information, see:

- [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md)
- [Microsoft Intune Advanced Analytics](../../analytics/advanced-endpoint-analytics.md)
- [Battery health](../../analytics/battery-health.md)
- [Device query](../../analytics/device-query.md)

## Week of January 22, 2024 (Service release 2401)

### App management

#### Install DMG and PKG apps up to 8 GB in size on managed Macs

The size-limit of DMG and PKG apps that can be installed using Intune on managed Macs has been increased. The new limit is 8 GB and is applicable to apps (DMG and unmanaged PKG) that are installed using the Microsoft Intune management agent for macOS.

For more information about DMG and PKG apps, see [Add a macOS DMG app to Microsoft Intune](../apps/lob-apps-macos-dmg.md) and [Add an unmanaged macOS PKG app to Microsoft Intune](../apps/macos-unmanaged-pkg.md).

#### Intune support of store-signed LOB apps for Surface Hub devices

Intune now supports the deployment of store-signed LOB apps (single file `.appx`, `.msix`, `.appxbundle`, and `.msixbundle`) to Surface Hub devices. The support for store-signed LOB apps enables offline store apps to be deployed to Surface Hub devices following the retirement of the Microsoft Store for Business.

#### Route SMS/MMS messages to specific app

You can configure an app protection policy to determine which SMS/MMS app must be used when the end user intends to send a SMS/MMS message after getting redirected from a policy managed app. When the end user selects on a number with the intent of sending an SMS/MMS message, the app protection settings are used to redirect to the configured SMS/MMS app. This capability relates to the **Transfer messaging data to** setting and applies to both iOS/iPadOS and Android platforms.

For more information, see [iOS app protection policy settings](../apps/app-protection-policy-settings-ios.md) and [Android app protection policy settings](../apps/app-protection-policy-settings-android.md).

#### End user app PIN reset

For managed apps that require a PIN to access, allowed end users can now reset the app PIN at any time. You can require an app PIN in Intune by selecting the **PIN for access** setting in iOS/iPadOS and Android app protection policies.

For more information about app protection policies, see [App protection policies overview](../apps/app-protection-policy.md).

#### Maximum app package size

The maximum package size for uploading apps to Intune is changed from 8 GB to 30 GB for paid customers. Trial tenants are still restricted to 8 GB.

For more information, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md#prerequisites).

### Device configuration

#### New setting that disables location on Android Enterprise devices

On Android Enterprise devices, there's a new setting that allows admins to control the location (**Devices** > **Configuration** > **Create** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile > Device Restrictions** for profile type > **General**):

- **Location**: **Block** disables the **Location** setting on the device and prevents users from turning it on. When this setting is disabled, then any other setting that depends on the device location is affected, including the **Locate device** remote action. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using location on the device.

Applies to:

- Android Enterprise

For more information on the settings you can configure, see [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

#### Date and time picker for managed software updates in the settings catalog on iOS/iPadOS and macOS devices

Using the settings catalog, you can enforce managed updates on iOS/iPadOS and macOS devices by entering a date and time (**Devices** > **Configuration** > **Create** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type > **Declarative Device Management > Software Update**).

Previously, you had to manually type the date and time. Now, there's a date and time picker for the **Target Local Date Time** setting:

**Declarative Device Management (DDM) > Software Update**:

- Target Local Date Time

> [!IMPORTANT]
> If you create a policy using this setting before the January 2024 release, then this setting shows `Invalid Date` for the value. The updates are still scheduled correctly and use the values you originally configured, even though it shows `Invalid Date`.
>
> To configure a new date and time, you can delete the `Invalid Date` values, and select a new date and time using the date time picker. Or, you can create a new policy.

Applies to:

- iOS/iPadOS
- macOS

For more information about configuring Managed software updates in Intune, see [Use the settings catalog to configure managed software updates](../protect/managed-software-updates-ios-macos.md).

### Device management

#### New device management experience in Microsoft Intune

We're rolling out an update to the device management experience in the Intune admin center. The **Devices** area now has a more consistent UI, with more capable controls and an improved navigation structure so you can find what you need faster. The new experience, previously in public preview, will gradually roll out for general availability over the coming weeks. The public preview experience continues to be available until your tenant receives the update.

The availability of this new admin center experience varies tenant by tenant. While a few will see this update immediately, many might not see the new experience for several weeks. For Government clouds, the availability of this experience is estimated around late February 2024.

Due to the rollout timelines, we're updating our documentation to the new experience as soon as possible to help ease the transition to the new admin center layout. We're unable to provide a side-by-side content experience during this transition and believe providing documentation that aligns to the newer experience brings more value to more customers. If you want to try the new experience and align with doc procedures before your tenant is updated, go to **Devices** > **Overview**, select the notification banner that reads **Preview upcoming changes to Devices and provide feedback**, and select **Try it now**.

#### BlackBerry Protect Mobile now supports app protection policies

You can now use Intune app protection policies with *BlackBerry Protect Mobile* (powered by Cylance AI). With this change, Intune supports BlackBerry Protect Mobile for mobile application management (MAM) scenarios for [unenrolled devices](../protect/mtd-add-apps-unenrolled-devices.md). This support includes the use of risk assessment with Conditional access and configuration of Conditional Launch settings for unenrolled devices.

While configuring the CylancePROTECT Mobile connector (formerly BlackBerry Mobile), you now can select options to turn on *App protection policy evaluation* for both Android and iOS/iPadOS devices.

For more information, see [Set up BlackBerry Protect Mobile](../protect/blackberry-mobile-threat-defense-connector.md), and [Create Mobile Threat Defense app protection policy with Intune](../protect/mtd-app-protection-policy.md).

### Device security

#### Support for Intune Defender Update control policies for devices managed by Microsoft Defender for Endpoint

You can now use the endpoint security policy for *Defender Update control* (Antivirus policy) from the Microsoft Intune admin center with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.

- **Defender Update control** policies are part of endpoint security [Antivirus policy](../protect/endpoint-security-antivirus-policy.md).

Applies to the following when you use the *Windows 10, Windows 11, and Windows Server* platform:

- Windows 10
- Windows 11

With this support available, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive the policy will get it.

### Intune apps

#### Newly available protected apps for Intune

The following protected apps are now available for Microsoft Intune:

- PrinterOn Print by PrinterOn, Inc. (iOS/iPadOS)
- Align for Intune by MFB Technologies, Inc. (iOS/iPadOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Monitoring reports for devices

In Intune, you can view a new list of all device monitoring reports. You can find these reports in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Monitor**. The **Monitor** pane provides reports related to configuration, compliance, enrollment, and software updates. Additionally, there are other reports that you can view, such as **Device actions**.

For more information, see [Intune reports](../fundamentals/reports.md).

#### Exported report data maintains search results

Intune can now maintain your report search and filter results when exporting report data. For example, when you use the [Noncompliant devices and settings](../fundamentals/reports.md#noncompliant-devices-report-organizational) report, set the OS filter to "Windows", and search for "PC", the exported data will only contain Windows devices with "PC" in their name. This capability is also available when calling the `ExportJobs` API directly.

#### Easy upload of diagnostic logs for Microsoft Tunnel servers

You can now use a single click within the Intune admin center to have Intune enable, collect, and submit eight hours of verbose logs for a Tunnel Gateway Server to Microsoft. The verbose logs can then be referenced while working with Microsoft to identify or resolve issues with a Tunnel server.

In contrast, the collection of verbose logs previously required you to sign on to the server, run manual tasks and scripts to enable and collect verbose logs, and then copy them to a location from which you can transfer them to Microsoft.

To find this new capability, in the admin center go to **Tenant administration** > **Microsoft Tunnel Gateway** > select a server > select the **Logs** tab. On this tab, is a new section named **Send verbose server logs** with button labeled **Send logs**, and a list view that displays the various log sets that have been collected and submitted to Microsoft.

When you select the **Send logs** button:

- Intune captures and submits the current server logs as a baseline, prior to collecting verbose logs.
- Verbose logging is automatically enabled at level 4, and runs for eight hours to provide time to reproduce an issue for capture in those logs.
- After eight hours, Intune submits the verbose logs and then restores the server to its default verbosity level of zero (0), for normal operations. If you previously set logs to run at a higher verbosity level, you can restore your custom verbosity level after log collection and upload is complete.
- Each time Intune collects and submits logs, it updates the list view below the button. 
- Below the button is a list of past log submissions, displaying their verbosity level and an Incident ID that you can use when working with Microsoft to reference a specific set of logs.

For more information about this capability, see [Easy upload of diagnostic logs for Tunnel servers](../protect/microsoft-tunnel-monitor.md#easy-upload-of-diagnostic-logs-for-tunnel-servers).

## Week of December 11, 2023 (Service release 2312)

### App management

#### Support to add unmanaged PKG-type applications to managed macOS devices is now generally available

You can now upload and deploy unmanaged PKG-type applications to managed macOS devices using the Intune MDM agent for macOS devices. This feature enables you to deploy custom PKG installers, such as unsigned apps and component packages. You can add a PKG app in the Intune admin center by selecting **Apps** > **macOS** > **Add** > **macOS app (PKG)** for app type.

Applies to:

- macOS

For more information, see [Add an unmanaged macOS PKG app to Microsoft Intune](../apps/macos-unmanaged-pkg.md). To deploy managed PKG-type app, you can continue to [add macOS line-of-business (LOB) apps to Microsoft Intune](../apps/lob-apps-macos.md). For more information about the Intune MDM agent for macOS devices, see [Microsoft Intune management agent for macOS](../apps/lob-apps-macos-agent.md).

#### Windows MAM supported in government cloud environments and in 21 Vianet in China

Customer tenants in US Government Community (GCC), US Government Community (GCC) High, and Department of Defense (DoD) environments are now able to use Windows MAM. For related information, see [Deploying apps using Intune on the GCC High and DoD Environments](../apps/apps-deploy-gcc-dod.md) and [Data protection for Windows MAM](../apps/protect-mam-windows.md).

In addition, Windows MAM is available for Intune operated by 21Vianet in China. For more information, see [Intune operated by 21Vianet in China](../fundamentals/china.md).

### Device configuration

#### Updated security baseline for Microsoft Edge v117

We released a new version of the Intune security baseline for **Microsoft Edge**, version [**v117**](../protect/security-baselines.md#available-security-baselines). This update brings support for recent settings so you can continue to maintain best-practice configurations for Microsoft Edge.

We also updated our [reference article](../protect/security-baseline-v2-edge-settings.md?pivots=edge-v117) for this baseline where you can view the default configuration of the settings this baseline version includes.

### Device management

#### Support for variables in noncompliant email notifications

Use variables to personalize email notifications that are sent when a user's device becomes noncompliant. The variables included in the template, such as `{{username}}` and `{{devicename}}`, are replaced by the actual username or device name in the email that users receive. Variables are supported with all platforms.

For more information and a list of supported variables, see [Create a notification message template](../protect/actions-for-noncompliance.md#create-a-notification-message-template).

#### Updated report visualization for Microsoft Defender for Endpoint connector

We updated the reporting visualization for the Microsoft Defender for Endpoint connector. This [report visualization](../protect/advanced-threat-protection-configure.md#view-the-count-of-devices-that-are-onboarded-to-microsoft-defender-for-endpoint) displays the count of devices that are onboarded to Defender for Endpoint based on status from the Defender CSP, and visually aligns to other recent report views that use a bar to represent the percentage of devices with different status values.

### Device security

#### New settings for scheduling Antivirus scans added to Antivirus policy for Windows devices

We added two settings to the *Microsoft Defender Antivirus* profile for [endpoint security Antivirus policy](../protect/endpoint-security-antivirus-policy.md#antivirus-profiles) that applies to Windows 10 and Windows 11 devices. These two settings work together to first enable support for a random start time of a device's antivirus scan, and to then define a range of time during which the randomized scan start can begin. These settings are supported with devices managed by Intune and devices managed through the [Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario.

- [**RandomizeScheduleTaskTimes**](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#admx-microsoftdefenderantivirus-randomizescheduletasktimes) – This setting enables randomization of the scan start time on devices.
- [**SchedulerRandomizationTime**](/windows/client-management/mdm/defender-csp?WT.mc_id=Portal-fx#configurationschedulerrandomizationtime) – With this setting, you can set boundaries for the random start time.

In addition to being added to the Microsoft Defender Antivirus profile, both settings are now available from the [settings catalog](../configuration/settings-catalog.md).

Applies to:

- Windows 10
- Windows 11

#### Microsoft Tunnel support for direct proxy exclusion list in VPN profiles for Android Enterprise

Intune now supports configuration of a *Proxy exclusion list* when you [configure a VPN profile for Microsoft Tunnel](../protect/microsoft-tunnel-configure.md#create-a-vpn-profile) for Android devices. With an exclusion list, you can exclude specific domains from your proxy setup without requiring the use of a Proxy Auto-Configuration (PAC) file. The proxy exclusion list is available with both Microsoft Tunnel and Microsoft Tunnel for MAM.

The proxy exclusion list is supported in environments that use a single proxy. The exclusion list isn't suitable or supported when you use multiple proxy servers, for which you should continue to use a `.PAC` file.

Applies to:

- Android Enterprise

#### Microsoft Tunnel server health metric to report on TLS certificate revocation

We added a new health metric for Microsoft Tunnel named **TLS certificate revocation**. This new health metric report on the status of the Tunnel Servers TLS certificate by accessing the Online Certificate Status Protocol (OCSP) or CRL address as defined in the TLS certificate. You can view the status of this new check with all the health checks in the Microsoft Intune admin center by navigating to **Tenant administration** > **Microsoft Tunnel Gateway** > **Health status**, selecting a server, and then selecting that servers **Health check** tab.

This metric runs as part of the existing Tunnel Health checks, and supports the following status:

- *Healthy*: The TLs certificate isn't revoked
- *Warning*: Unable to check if the TLS certificate is revoked
- *Unhealthy*: The TLS certificate is revoked, and should be updated

For more information about the TLS certificate revocation check, see [Monitor Microsoft Tunnel](../protect/microsoft-tunnel-monitor.md).

### Intune apps

#### Newly available protected app for Intune

The following protected app is now available for Microsoft Intune:

- Akumina EXP by Akumina Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of November 27, 2023

### App management

#### Configure offline caching in Microsoft 365 (Office) for Android devices

When the **Save As to Local Storage** setting is set to **blocked** in an [app protection policy](../apps/app-protection-policies.md), you can use a configuration key in an app configuration policy to enable or disable offline caching. This setting is only applicable to the Microsoft 365 (Office) app on Android.

For more information, see [Data protection settings in Microsoft 365 (Office)](../apps/manage-microsoft-office.md#data-protection-settings-in-microsoft-365-office).

#### Win32 app grace period settings on a device

On a device where a Win32 app with grace period settings is deployed, low-rights users without administrative privileges can now interact with the grace period UX. Admins on the device continue to be able to interact with the grace period UX on the device.

For more information about grace period behavior, see [Set Win32 app availability and notifications](../apps/apps-win32-app-management.md#set-win32-app-availability-and-notifications).

#### Managed Home Screen app configuration additions

Now in public preview, Microsoft Managed Home Screen (MHS) is updated to improve the core workflows and user experience. In addition to some user interface changes, there's a new top bar navigation where admins can configure device identifying attributes to be displayed. Additionally, users can access settings, sign in/out, and view notifications when permissions are requested on the top bar.

You can add more settings to configure the Managed Home Screen app for Android Enterprise. Intune now supports the following settings in your Android Enterprise app configuration policy:

- Enable updated user experience
- Top Bar Primary Element
- Top Bar Secondary Element
- Top Bar User Name Style

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Intune APP SDK for .NET MAUI

Using the Intune APP SDK for .NET MAUI, you can develop Android or iOS apps for Intune that incorporate the [.NET Multi-platform App UI](https://dotnet.microsoft.com/apps/maui). Apps developed using this framework allow you to enforce [Intune mobile application management](../apps/app-management.md). For .NET MAUI support on Android, see [Intune App SDK for .NET MAUI - Android](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android). For .NET MAUI support on iOS, see [Intune App SDK for .NET MAUI - iOS](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS).

## Week of November 13, 2023 (Service release 2311)

### App management

#### New grace period status added in apps for Android, Android AOSP

The Intune Company Portal app for Android and Microsoft Intune app for Android AOSP now show a grace period status for devices that don't meet compliance requirements but are still within their given grace period. Users can see the date by which devices must be compliant, and the instructions for how to become compliant. If users don't update their device by the given date, the device is marked as noncompliant.

For more information, see the following articles:

- [Configure compliance policies with actions for noncompliance](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance)
- [Check compliance in Intune app for AOSP](../user-help/check-compliance-aosp.md)
- [Check compliance in Company Portal for Android](../user-help/check-compliance-on-your-device-android.md)

### Device configuration

#### New settings available in the Apple settings catalog

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Managed Settings**:

- Data roaming
- Personal hotspot
- Voice roaming (deprecated): This setting is deprecated in iOS 16.0. Data roaming is the replacement setting.

##### Shared iPad

**Managed Settings**:

- Diagnostic submission

##### macOS

**Microsoft Defender > Antivirus engine**:

- Enable passive mode (deprecated): This setting is deprecated. Enforcement level is the replacement setting.
- Enable real-time protection (deprecated): This setting is deprecated. Enforcement level is the replacement setting.
- Enforcement level

#### Settings to manage Windows Subsystem for Linux are now available in the Windows settings catalog

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings to the Windows settings catalog for *Windows Subsystem for Linux* (WSL). These settings enable Intune integration with WSL so admins can manage deployments of WSL and controls into Linux instances themselves.

To find these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Devices** > **Configuration** > **Create** > **New Policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type.

**Windows Subsystem for Linux**:

- Allow kernel debugging
- Allow custom networking configuration
- Allow custom system distribution configuration
- Allow kernel command line configuration
- Allow custom kernel configuration
- Allow WSL1
- Allow the Windows Subsystem for Linux
- Allow the Inbox version of the Windows Subsystem For Linux
- Allow user setting firewall configuration
- Allow nested virtualization
- Allow passthrough disk mount
- Allow the debug shell

Applies to:

- Windows 10
- Windows 11

### Device enrollment

#### Enrollment for iOS/iPadOS devices in shared device mode now generally available

Now generally available to configure in the Microsoft Intune admin center, set up automated device enrollment for iOS/iPadOS devices that are in shared device mode. Shared device mode is a feature of Microsoft Entra that enables your frontline workers to share a single device throughout the day, signing in and out as needed.

For more information, see [Set up enrollment for devices in shared device mode](../enrollment/automated-device-enrollment-shared-device-mode.md).

### Device management

#### Improvements to new device experience in admin center (public preview)

We made the following changes to the new Devices experience in the Microsoft Intune admin center:

- More entry points to platform-specific options: Access the platform pages from the **Devices** navigation menu.
- Quick entry to monitoring reports: Select the titles of the metrics cards to go to the corresponding monitoring report.
- Improved navigation menu: We added icons back in to provide more color and context as you navigate.

Flip the toggle in the Microsoft Intune admin center to try out the new experience while it's in public preview and share your feedback. 

For more information, see:

- [New Microsoft Intune Devices experience - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/intune-customer-success/new-microsoft-intune-devices-experience/ba-p/3777342)
- [Try new Devices experience - Microsoft Learn](microsoft-intune-admin-center-devices.md)

### Device security

#### Additional settings for the Linux Antivirus policy template

We expanded support for Linux by adding the following settings to the *Microsoft Defender Antivirus* template for Linux devices:

- cloudblocklevel
- scanarhives
- scanafterdefinitionupdate
- maximumondemandscanthreads
- behaviormonitoring
- enablefilehashcomputation
- networkprotection
- enforcementlevel
- nonexecmountpolicy
- unmonitoredfilesystems

The Microsoft Defender Antivirus template for Linux is supported for devices [managed by Intune](../protect/endpoint-security-antivirus-policy.md), and devices managed only by Defender through the [Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario.

#### Updated security baseline for Microsoft 365 Apps for Enterprise

We released a new version of the Intune security baseline for **Microsoft 365 Apps for Enterprise**, version [**2306**](../protect/security-baselines.md#available-security-baselines).

The Microsoft 365 Office Apps baseline can help you rapidly deploy configurations to your Office Apps that meet the security recommendations of the Office and security teams at Microsoft. As with all baselines, the default baseline represents the recommended configurations. You can modify the default baseline to meet the requirements of your organization.

We also updated our [reference article](../protect/security-baseline-v2-office-settings.md?pivots=v2306) for this baseline where you can view the default configuration of the settings this baseline version includes.

#### Deprecation and replacement of two settings found in the Linux and macOS endpoint security Antivirus policies

There are two deprecated settings that in the *Antivirus engine* category of [Microsoft Defender Antivirus](../protect/endpoint-security-antivirus-policy.md) profiles of both macOS and Linux. These profiles are available as part of Intune's endpoint security Antivirus policies.

For each platform, a single setting replaces the two deprecated settings. This new setting aligns with how Microsoft Defender for Endpoint manages the device configurations.

The following are the two deprecated settings:

- *Enable real-time protection* now appears as *Enable real-time protection (deprecated)*
- *Enable passive mode* now appears as *Enable passive mode (deprecated)*

The new setting that replaces the two deprecated settings:

- *Enforcement level* - By default, Enforcement level is set to *Passive* and supports options of *Real time* and *On demand*.

These settings are also available from the Intune [settings catalog](../configuration/settings-catalog.md) for each platform, where the old settings are also marked as deprecated and replaced by the new setting.

With this change, a device that has either of the *deprecated* settings configured will continue to apply that configuration until the device is targeted by the new setting *Enforcement level*. Once targeted by Enforcement Level, the deprecated settings no longer are applied to the device.

The *deprecated* settings will be removed from the Antivirus profiles and the settings catalog in a future update to Intune.

> [!NOTE]
> The changes for Linux are now available. The macOS settings are marked as deprecated, but the *Enforcement level* setting will not be available until December.

Applies to:

- Linux
- macOS

#### Microsoft Defender Firewall profiles are renamed to Windows Firewall

<<<<<<< Updated upstream
To align to Firewall branding changes in Windows, we're updating the names of Intune profiles for endpoint security Firewall policies. In profiles that have *Microsoft Defender Firewall* in the name we're replacing that with *Windows Firewall*.
=======
To align to Firewall branding changes in Windows, we are updating the names of Intune profiles for endpoint security Firewall policies. In profiles that have *Microsoft Defender Firewall* in the name we're replacing that with *Windows Firewall*.
>>>>>>> Stashed changes

The following platforms have profiles that are affected, with only the profile names being affected by this change:

- Windows 10 and later (ConfigMgr)
- Windows 10, Windows 11, and Windows Server

#### Endpoint security Firewall policy for Windows Firewall to manage firewall settings for Windows Hyper-V

We added new settings to the *Windows Firewall* profile (formerly *Microsoft Defender Firewall*) for endpoint security [Firewall policy](../protect/endpoint-security-firewall-policy.md). The new settings can be used to manage Windows Hyper-V settings. To configure the new settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Endpoint security** > **Firewall** > Platform: **Windows 10, Windows 11, and Windows Server** > Profile: **Windows Firewall**.

The following settings are added to the *Firewall* category:

- **Target** - When *Target* is set to **Windows Subsystem for Linux**, the following child settings are applicable:
  - Enable Public Network Firewall
  - Enable Private Network Firewall
  - Allow Host Policy Merge
  - Enable Domain Network Firewall
  - Enable Loopback

Applies to:

- Windows 10
- Windows 11

For more information about these settings, see [Windows Firewall with Advanced Security](/windows/security/operating-system-security/network-security/windows-firewall/windows-firewall-with-advanced-security).

#### New Endpoint Security Firewall policy profile for Windows Hyper-V Firewall Rules

We released a new profile named *Windows Hyper-V Firewall Rules* that you can find through the *Windows 10, Windows 11, and Windows Server* platform path for endpoint security [Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune). Use this profile to manage the firewall settings and rules that apply to specific Hyper-V containers on Windows, including applications like the Windows Subsystem for Linux (WSL) and the Windows Subsystem for Android (WSA).

Applies to:

- Windows 10
- Windows 11

### Intune apps

#### Newly available protected apps for Intune

The following protected apps are now available for Microsoft Intune:

- Hey DAN for Intune by Civicom, Inc.
- Microsoft Azure by Microsoft Corporation (iOS)
- KeePassium for Intune by KeePassium Labs (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of November 6, 2023

### App management

#### Minimum version update for iOS Company Portal

Users are required to update to v5.2311.1 of the iOS Company Portal. If you enabled the **[Block installing apps using App Store](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised)** device restriction setting, you'll likely need to push an update to the related devices that use this setting. Otherwise, no action is needed.

If you have a helpdesk, you might want to make them aware of the prompt to update the Company Portal app. In most cases, users have app updates set to automatic, so they receive the updated Company Portal app without taking any action. Users that have an earlier app version are prompted to update to the latest Company Portal app.

### Device security

#### Defender for Endpoint security settings management enhancements and support for Linux and macOS are generally available<!-- 24190967 -->

The improvements that were introduced in the Defender for Endpoint security settings management [opt-in public preview](../fundamentals/whats-new-archive.md#defender-for-endpoint-security-settings-management-enhancements-and-support-for-linux-and-macos-in-public-preview) are now generally available.

With this change, the default behavior for security settings management includes all the behavior added for the opt-in preview – without having to enable support for preview features in Microsoft Defender for Endpoint. This includes the general availability and support for the following endpoint security profiles for Linux and macOS:

**Linux**:

- Microsoft Defender Antivirus
- Microsoft Defender Antivirus exclusions
- Endpoint detection and response

**MacOS**:

- Microsoft Defender Antivirus
- Microsoft Defender Antivirus exclusions
- Endpoint detection and response

For more information, see [Microsoft Defender for Endpoint Security settings management](../protect/mde-security-integration.md) in the Intune documentation.

### Device management

### Feature updates and reports support Windows 11 policies

The new setting on Feature update policies enables an organization to deploy Windows 11 to those devices that are eligible for the upgrade, while ensuring devices not eligible for the upgrade are on the latest Windows 10 feature update with a single policy. As a result, admins don't need to create or manage groups of eligible and non-eligible devices.

For more information on feature updates, see [Feature updates for Windows 10 and later](../protect/windows-10-feature-updates.md).

## Week of October 30, 2023

### Device security

#### Strict Tunnel Mode in Microsoft Edge available for Microsoft Tunnel for MAM on Android and iOS/iPadOS devices

In Intune, you can use the Microsoft Tunnel for mobile application management (MAM) on Android and iOS/iPadOS devices. With the MAM tunnel, unmanaged devices (devices not enrolled in Intune) can access on-premises apps and resources.

There's a new **Strict Tunnel Mode** feature you can configure for Microsoft Edge. When users sign into Microsoft Edge with an organization account, if the VPN isn't connected, then **Strict Tunnel Mode** blocks internet traffic. When the VPN reconnects, internet browsing is available again.

To configure this feature, create a Microsoft Edge app configuration policy, and add the following setting:

- **Key**: `com.microsoft.intune.mam.managedbrowser.StrictTunnelMode`
- **Value**: `True`

Applies to:

- Android Enterprise version 10 and later
- iOS/iPadOS version 14 and later

For more information, see:

- [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-mam.md)
- [Microsoft Tunnel for MAM - Android](../protect/microsoft-tunnel-mam-android.md)
- [Microsoft Tunnel for MAM - iOS/iPadOS](../protect/microsoft-tunnel-mam-ios.md)

## What's new archive

For previous months, see the [What's new archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
