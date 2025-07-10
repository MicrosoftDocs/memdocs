---
# required metadata
title: What's new in Microsoft Intune
titleSuffix:
description: Find out what's new in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: laurawi
ms.date: 07/10/2025
ms.topic: whats-new
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
- Information about [how Intune service updates are released](intune-service-servicing-information.md)

> [!NOTE]
> Each [monthly update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) can take up to three days to roll out and will be in the following order:
>
> - Day 1: Asia Pacific (APAC)
> - Day 2: Europe, Middle East, Africa (EMEA)
> - Day 3: North America
> - Day 4+: Intune for Government
>
> Some features roll out over several weeks and might not be available to all customers in the first week.
>
> For a list of upcoming Intune feature releases, see [In development for Microsoft Intune](../fundamentals/in-development.md).
>
> For new information about Windows Autopilot solutions, see:
>
> - [Windows Autopilot device preparation: What's new](/autopilot/device-preparation/whats-new)
> - [Windows Autopilot: What's new](/autopilot/whats-new)

You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
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
## Week of July 14, 2025

### Device management

#### Experience Microsoft Copilot in Intune<!-- 29339619, 31192897 -->

You can now use Microsoft Copilot in Intune to explore your Intune data using natural language, take action on the results, manage policies and settings, understand your security posture, troubleshoot device issues, and view insights about enrolled Surface devices.

##### Explorer

Use natural language to explore your Intune data and take action based on the results. Admins can run queries against Intune resource data, including questions about devices, apps, policies, updates, and compliance. When a query runs, a Copilot summary helps you understand the results and offers suggestions. You can add devices or users from the query results to a group to target apps and policies. There are also example queries that you can filter to find an example that best matches your request or use to help you create your own request.

Data coverage, querying capabilities, and actionability will evolve over time as we make improvements to how you explore your data.

To learn more about this feature, see [Explore Intune data and get Microsoft Copilot recommendations](../copilot/copilot-intune-explorer.md)

##### Conversational chat experience

Use Copilot in Intune chat experience to interact with your data through natural language. This feature helps you perform key administrative tasks, get insights, and troubleshoot issues. You can use the chat experience for:

- Policy and setting management: Use Copilot in Intune to summarize an existing policy or learn more about individual policy settings and recommended values.
- Device details and troubleshooting: Use Copilot in Intune to get device details and troubleshoot a device to get device-specific information like the installed apps, group memberships and more.
- Device Query: Use Copilot in Intune to help you create Kusto Query Language (KQL) queries to run when using device query in Intune.
- Endpoint Privilege Management (EPM): Use Copilot in Intune to help identify potential elevation risks from within the EPM support approved workflow.

##### Microsoft Copilot in Surface Management Portal

Microsoft Copilot in Intune includes the Surface Management Portal, a workspace in the Intune admin center that brings together vital data and insights about enrolled Surface devices, all in one place.

 - Gain insights into device compliance, support activity, applicable warranty or protection plan coverage, and carbon emission estimates.
 - Monitor the status of each device, including applicable warranty or protection plan expirations and active support requests.
 - Centralize Surface-specific device administration in a single environment.
 - Automatically access comprehensive information from your Intune-enrolled Surface devices, which flows into the Surface Management Portal when users sign in for the first time.

To learn more about this feature, see [Security Copilot in Microsoft Surface Management Portal](../copilot/security-copilot-surface-portal.md)

## Week of June 23, 2025 (Service release 2506)

### App management

#### Microsoft Intune support for Apple AI features<!-- 12792722, 30550110, 30220799 -->

Intune app protection policies have new standalone settings for Apple AI features (Genmojis, Writing tools, and screen capture). Note that these standalone settings are supported by apps that have updated to version 19.7.12 or later for Xcode 15, and 20.4.0 or later for Xcode 16 of the Intune App SDK and App Wrapping Tool. Previously, these Apple AI features were blocked when the app protection policy **Send Org data to other apps** setting is configured to a value other than **All apps**.

For more information about Intune's related app protection policies, see [iOS app protection policy settings](../apps/app-protection-policy-settings-ios.md).

#### Add Enterprise App Catalog apps to ESP blocking apps list<!-- 29846319 -->

Windows Autopilot now supports Enterprise App Catalog apps. Microsoft Intune Enterprise App Management enables IT admins to easily manage applications from the Enterprise App Catalog. Using Windows Autopilot, you can select apps from the Enterprise App Catalog as blocking apps in the Enrollment Status Page (ESP) and the Device Preparation Page (DPP) profiles. This allows you to ensure those apps are delivered before the user can access the desktop.

For related information, see [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md), [Overview of Windows Autopilot device preparation](/autopilot/device-preparation/overview), and [Add an Enterprise App Catalog app to Microsoft Intune](../apps/apps-add-enterprise-app.md).

Applies to:

- Windows

#### Managed Home Screen orientation changes with Android 16<!-- 30316862 -->

Starting with Android 16, Android stops enforcing screen orientation on devices with 600dp and larger display settings. This change impacts the Managed Home Screen (MHS) on devices with larger form factors, like tablets.

On these Android 16 devices, orientation is determined by the device's orientation setting, not the MHS settings you configure.

To learn more about Android 16 changes, go to [Behavior changes: Apps targeting Android 16 or higher](https://developer.android.com/about/versions/16/behavior-changes-16) (opens Android website).

Applies to:

- Android Enterprise


### Device configuration

#### New settings available in the Apple settings catalog<!-- 32498293 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring settings catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the settings catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Managed Settings**:

- Idle Reboot Allowed

##### macOS

**Authentication > Extensible Single Sign On (SSO)**:

- Allow Device Identifiers In Attestation

**Microsoft Edge**:

- The Microsoft Edge category has been updated with hundreds of new settings. Learn more about available macOS Edge settings at [Microsoft Edge - Policies](/deployedge/microsoft-edge-policies).

Apple deprecated the Identification payload in macOS 15.4.

#### New Block Bluetooth setting in the Android Enterprise settings catalog<!-- 15583647 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There's a new **Block Bluetooth** setting (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type). When set to **True**, Bluetooth is disabled on the device.

There's also a **Block Bluetooth Configuration** setting that prevents end users from changing the Bluetooth setting on the device.

These settings are different and have different results. Some examples include:

- **Scenario**: An end user turned on the Bluetooth setting on their device. The admin creates an Intune policy that sets the **Block Bluetooth** setting to **True**.

  In this situation, Bluetooth is blocked on the device, even though the end user turned it on.

- **Scenario**: An end user turned on the Bluetooth setting on their device. The admin creates an Intune policy that sets the **Block Bluetooth Configuration** setting to **True**.

  In this situation, Bluetooth is turned on since the end user previously turned it on. The end user can't turn off Bluetooth. If the end user previously turned Bluetooth off, and then the **Block Bluetooth Configuration** policy applies, then Bluetooth is turned off and the end user can't turn it back on.

For a list of existing settings you can configure in the settings catalog, see [Android Enterprise device settings list in the Intune settings catalog](../configuration/settings-catalog-android.md).

Applies to:

- Android Enterprise corporate-owned devices with a work profile (COPE)
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)

### Device management

#### New reporting system for improved performance and data consistency<!-- 31823383 -->

Microsoft Intune is rolling out the new Policy Reporting Service (PRS) V3. The new system brings faster report generation, improved reliability, and better data consistency.
 
In the first phase, some high-traffic compliance and device configuration reports are transitioning to the new system.
 
Users will notice quicker updates in the Intune admin center and fewer issues with stale data. No action is required from users, as your reports transition automatically.

To learn more about the Intune reports you can use, see [Intune reports](reports.md).

### Device security

#### New attributes and S/MIME baseline requirements for SCEP certificate profiles <!-- 33116047 -->

Intune supports two new attributes for subject name settings in SCEP and PKCS device configuration profiles. They include:

- G={{GivenName}}
- SN={{SurName}}

Beginning July 16th, you are required to use these attributes in the subject name format if you're using a third party public certificate authority (CA) integrated with the Intune SCEP API for issuing S\MIME (encryption or signing) certificates anchored up to a public root CA. After that date, a public CA will not issue or sign S\MIME certificates that omit these attributes. 

For more information, see [S/MIME certificate requirements for third party public CA](../protect/certificates-profile-scep.md#smime-certificate-requirements-for-third-party-public-ca).

### Intune apps

#### Newly available protected apps for Intune<!-- 32647747, 32692741, 32775449, 32920017 -->

The following protected apps are now available for Microsoft Intune:

- Datasite for Intune by Datasite (iOS)
- Mijn InPlanning by Intus Workforce Solutions (iOS)
- Nitro PDF Pro by Nitro Software, Inc. (iOS)
- SMART TeamWorks by SMART Technologies ULC (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

####  New status column in Windows hardware attestation report<!-- 26527908 -->

We added a new column, **Attest Status**, to the Windows hardware attestation report to improve visibility into attestation errors. This column shows error messages received during the attestation process, helping you identify issues from both the service and client sides.  Error types shown in this column include:

- WinINet errors
- HTTP bad request errors
- Other attestation-related failures

For more information about the report, see [Windows hardware attestation report](../fundamentals/reports.md#windows-hardware-attestation-report-organizational).

## Week of June 9, 2025

### App management

#### ARM64 support for Win32 apps<!-- 28475401 -->

When adding a Win32 app to Intune, you can select an option to check and install the app on Windows devices running ARM64 operating systems. This capability is available from the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **All apps** > **Create**. The ARM64 option is available by selecting the **Operating system architecture** option under the **Requirements** step. To ensure that you don't have any impact to any Win32 applications that you previously targeted to 64-bit devices, your existing 64-bit Win32 applications will also have ARM64 selected. After the availability of being able to specifically target ARM64 operating system architectures, selecting x64 won't target ARM64 devices.

For related information, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

Applies to:

- Windows devices

## Week of June 2, 2025

## Device security

#### Vulnerability Remediation Agent for Intune (public preview)<!-- 33475311 -->
 
The Vulnerability Remediation Agent is currently in a limited public preview and available to only a select group of customers. If you're interested in gaining access or would like to learn more, please reach out to your sales team for further details and next steps.

When run, this agent uses data from Microsoft Defender Vulnerability Management to identify and then provide remediation guidance for vulnerabilities on your managed devices. You run and access the agent and view its results from within the Intune admin center where you'll see suggestions prioritized by the agent for remediation. Each suggestion includes key information like associated CVEs, severity, exploitability, affected systems, organizational exposure, business impact, and remediation guidance.
 
This information empowers you with a current assessment of potential risk to your environment and guidance to help you decide which risk to address first.

For more information about this agent including prerequisites, see [Vulnerability Remediation Agent for Security Copilot in Microsoft Intune](../protect/vulnerability-remediation-agent.md).

## Week of May 26, 2025 (Service release 2505)

### Microsoft Intune Suite

#### Endpoint Privilege Management rules explicitly deny elevation<!-- 30225542 -->
 
Endpoint Privilege Management (EPM) elevation rules now include a new file elevation type of **Deny**. An EPM elevation rule set to *Deny* blocks the specified file from running in an elevated context. While we recommend using file elevation rules to allow users to elevate specific files, a deny rule can help you ensure that certain files like known and potentially malicious software can't be run in an elevated context.

*Deny* rules support the same configuration options as other [elevation types](../protect/epm-policies.md#manually-configure-elevation-rules-for-windows-elevation-rules-policy) except for child processes, which aren't used.

For more information about EPM, which is available as an [Intune Suite add-on-capability](../fundamentals/intune-add-ons.md), see [Endpoint Privilege Management overview](../protect/epm-overview.md).

### App management

#### Newly available protected apps for Intune<!-- 31844143, 31974161, 32037902, 32038043 -->

The following protected apps are now available for Microsoft Intune:

- Windows App by Microsoft Corporation (Android)
- Microsoft Clipchamp by Microsoft Corporation (iOS)
- 4CEE Connect by 4CEE Development
- Mobile Helix Link for Intune by Mobile Helix

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Device configuration

### Manage DFCI profiles for Windows devices<!-- 30305262 -->

We've added support to use DFCI profiles to manage UEFI (BIOS) settings for NEC devices that run Windows 10 or Windows 11. Not all NEC devices running Windows are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

You can manage DFCI profiles from within the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by going to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type. For more information about DFCI profiles, see:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](../../autopilot/dfci-management.md)

Applies to:

- Windows

### Device enrollment

#### Custom naming template for AOSP devices <!-- 31707864 -->

Use a custom template for naming AOSP user-affiliated and userless devices when they enroll with Intune. The template is available to configure in the enrollment profile. It can contain a combination of free text and predefined variables, such as device serial number, device type, and for user-affiliated devices, the owner's username. For more information about how to configure the template, see: 

- [Set up Intune enrollment for Android (AOSP) corporate-owned userless devices](../enrollment/android-aosp-corporate-owned-userless-enroll.md)
- [Set up Intune enrollment for Android (AOSP) corporate-owned user-associated devices](../enrollment/android-aosp-corporate-owned-user-associated-enroll.md)


#### Change to role-based access control for device enrollment limits<!-- 27115176 -->

We updated role-based access control (RBAC) for device limits. If you're currently assigned the [policy and profile manager](../fundamentals/role-based-access-control-reference.md#policy-and-profile-manager) role, or the *device configurations* permissions that are built-in to the role, you now have read-only access to device enrollment limit policies. To create and edit these policies, you must be an Intune Administrator.

### Device management

#### Cross Platform Device Inventory<!-- 25964936 -->

Android, iOS, and Mac devices are added to device inventory. Intune now collects a default set of inventory data including 74 Apple properties and 32 Android properties.

For more information, see [View device details with Microsoft Intune](../remote-actions/device-inventory.md).

#### Enhanced security during unattended Remote Help sessions on Android devices<!--25977108 -->

During an unattended Remote Help sessions on Android devices, we've enhanced the security and user awareness during remote assistance by blocking the screen of the device, and notifying users if they interact with it. 

This feature is for Zebra and Samsung devices that enrolled as Android Enterprise corporate owned dedicated devices. 

For more information on Remote Help, see [Remote Help](../fundamentals/remote-help-android.md).

### Device security

#### Detect rooted corporate-owned Android Enterprise devices<!--31672848 -->

Configure compliance policies to detect if a corporate-owned Android Enterprise device is rooted. If Microsoft Intune detects that a device is rooted, you can have it marked as noncompliant. This feature is now available for devices enrolled as fully managed, dedicated, or corporate-owned with a work profile. For more information, see [Device compliance settings for Android Enterprise in Intune](../protect/compliance-policy-create-android-for-work.md).

Applies to:

- Android

#### New endpoint security profile for configuring Endpoint detection and response and Antivirus exclusion settings on Linux devices <!-- 26549863 -->

As part of the Intune scenario for [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md), you can use a new *Endpoint detection and response* profile for Linux named [**Microsoft Defender Global Exclusions (AV+EDR)**](../protect/endpoint-security-edr-policy.md#linux) that you can now use to manage Linux device exclusions for both Microsoft Defender *Endpoint detection and response* (EDR) and *Antivirus* (AV).

This profile supports settings related to global exclusion settings as detailed in [Configure and validate exclusions on Linux](/defender-endpoint/linux-exclusions) in the Microsoft Defender documentation. These exclusion configurations can apply to both the antivirus and EDR engines on the Linux client to stop associated real time protection EDR alerts for excluded items. Exclusions can be defined by the file path, folder, or process explicitly defined by the admin in the policy.

The new Intune profile:

- Is available in addition to the existing endpoint security Antivirus policy for Microsoft Defender Antivirus.
- Is supported for devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario.
- Isn't supported for Linux devices managed directly by Intune.

For details about the available Defender settings, see [Configure security settings in Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint](/defender-endpoint/linux-preferences) in the Defender for Endpoint documentation.

Applies to:
- Linux

### Tenant administration

#### Data collection from SimInfo entity on Windows devices<!--30120558 -->

You can now collect data from the SimInfo entity on Windows devices with enhanced device inventory. 
For more information, see [Intune Data Platform](../../analytics/data-platform-schema.md).
Applies to:

- Windows

## Week of April 28, 2025

### App management

#### Intune support for Apple specialty devices<!-- 32486291 -->
We've extended app protection policies (APP) to support Microsoft Edge (v136 or later), OneDrive (v16.8.4 or later), and Outlook (v4.2513.0 or later). To enable this setting for these specific apps on visionOS devices, you must set `com.microsoft.intune.mam.visionOSAllowiPadCompatApps` to `Enabled` in your app configuration policy. Once you have assigned your app configuration policy, you can create and assign your app protection policy for your VisionOS devices. For more information, see [Protect data on VisionOS devices](../apps/app-configuration-policies-managed-app.md#protect-data-on-visionos-devices).

### Tenant administration

#### New icon for Microsoft Intune<!-- 29148691 -->
Microsoft Intune has a new icon. The Intune icon is being updated across platforms and apps associated with Intune, such as the Intune admin center and Intune Company Portal app. The new icon will gradually be implemented over the next few months.

## Week of April 21, 2025 (Service release 2504)

### Microsoft Intune Suite

#### Endpoint Privilege Management elevation rule support for file arguments and parameters<!-- 28077130 -->

File elevation rules for Endpoint Privilege Management (EPM) now support [command line file arguments](../protect/epm-policies.md#use-file-arguments-for-elevation-rules). When an elevation rule is configured to define one or more file arguments, EPM allows that file to run in an elevated request only when one of the defined arguments is used. EPM blocks elevation of the file should a command line argument be used that isn't defined by the elevation rule. Use of file arguments in your file elevation rules can help you refine how and for what intent different files are successfully run in an elevated context by Endpoint Privilege Management.

EPM is available as an [Intune Suite add-on-capability](../fundamentals/intune-add-ons.md).

### App management

#### Relationship viewer available for Intune apps<!-- 17644546 -->

The relationship viewer provides a graphical depiction of the relationships between different applications in the system, including superseding and dependent applications. Admins can find relationship viewer in Intune by selecting **Apps** > **All apps** > *a Win32 app* > **Relationship viewer**. The relationship viewer supports both Win32 apps and Enterprise App Catalog apps. For more information, see [App relationship viewer](../apps/apps-win32-app-management.md#app-relationship-viewer).

#### Apple VPP using new API v2.0<!-- 29567109 -->

Apple recently updated the API for their volume purchase program (VPP), which is used to manage apps and books. Apple's related API is now version 2.0. Version 1.0 is deprecated. To support the Apple updates, Microsoft Intune has updated to use the new API, which is faster and more scalable than the previous version.

Applies to:

- iOS/iPadOS
- macOS

#### Additional org data storage service options for Android and iOS apps<!-- 29606862 -->

Intune now provides additional storage services options when saving copies of org data using an app protection policy for Android or iOS. In addition to the existing org data storage options, you can also select **iManage** and **Egnyte** as storage options. You must select these services as exemptions from your block list by setting **Save copies of org data** to **Block**, then selecting the allowed storage services next to the **Allow user to save copies to selected services** setting. Note that this setting doesn't apply to all applications.

For more information about data protection using app protection policies, see [iOS app protection policy settings - Data protection](../apps/app-protection-policy-settings-ios.md#data-protection) and [Android app protection policy settings - Data protection](../apps/app-protection-policy-settings-android.md#data-protection).

Applies to:

- Android
- iOS

### Device configuration

#### Updated device configuration template for Windows Delivery Optimization<!-- 32411831 -->

We've updated the device configuration template for Windows [Delivery Optimization](../configuration/delivery-optimization-windows.md). The new template uses the settings format as found in the Settings Catalog, with settings that are taken directly from the Windows Configuration Service Providers (CSPs) for Windows Delivery Optimization, as documented by Windows at [Policy CSP – DeliveryOptimization](/windows/client-management/mdm/policy-csp-DeliveryOptimization).

With this change you can no longer create new versions of the old profile. However, your preexisting instances of the old profile remain available to use.

For more information about this change, see the Intune Customer Success blog at [Support tip: Windows device configuration policies migrating to unified settings platform in Intune](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-windows-device-configuration-policies-migrating-to-unified-settings-/4189665).

Applies to:

- Windows 10
- Windows 11

#### New settings available in the Apple settings catalog<!-- 31523569 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

We've added a new setting in the Settings Catalog. To see this setting, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), see **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

##### macOS

**Login > Login Window**:
- Show Input Menu

### Android settings in the Settings Catalog <!-- 31524383 -->

The settings catalog supports Android Enterprise and Android Open Source Project (AOSP).

Currently, to configure Android settings, you use the built-in templates. The settings from these templates are also available in the settings catalog. More settings will continue to be added.

In the Intune admin center, when you create a device configuration profile, you select the **Profile Type** (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > select your **Platform** > **Profile Type**). All the profile types are moved to **Profile Type** > **Templates**.

This change:

- Is a UI change with no impact on your existing policies. Your existing policies won't change. You can continue to create, edit, and assign these policies the same way.
- provides the same UI experience as iOS/iPadOS, macOS, and Windows templates.

In the new settings catalog experience, the management mode associated with the setting is available in the tooltip.
To get started with settings catalog, see [Use the settings catalog to configure settings on your devices](../configuration/settings-catalog.md).

Applies to:

- Android Enterprise
- AOSP

### Device enrollment

#### Custom device naming template for Android Enterprise corporate-owned devices<!-- 3465701 -->

You can use a custom template for naming Android Enterprise corporate-owned devices when they enroll with Intune. The template is available to configure in the enrollment profile. It can contain a combination of custom text and predefined variables, such as device serial number, device type, and for user-affiliated devices, the owner's username. For more information, see:

 - [Android Enterprise corporate-owned devices with work profile](../enrollment/android-corporate-owned-work-profile-enroll.md#create-an-enrollment-profile)
 - [Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md#create-an-enrollment-profile)
 - [Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md#step-2-create-new-enrollment-profile)

Applies to:

- Android

#### Enrollment-time grouping for Android Enterprise corporate devices <!-- 17530981 -->

Now available for Android Enterprise corporate-owned devices, *enrollment time grouping* enables you to assign a static Microsoft Entra group to devices at enrollment time. When a targeted Android device enrolls, it receives all assigned policies, apps, and settings, typically by the time the user lands on the home screen. You can configure one static Microsoft Entra group per enrollment profile under the **Device group** tab in the Microsoft Intune admin center. For more information, see [Enrollment time grouping](../enrollment/enrollment-time-grouping.md).

### Device management

#### Intune ending support for custom profiles for personally owned work profile devices<!-- 27424084 -->

Starting in April 2025, Intune no longer supports custom profiles for Android Enterprise personally owned work profile devices. With this end of support:

- Admins won't be able to create new custom profiles for personally owned work profile devices. However, admins can still view and edit previously created custom profiles.

- Personally-owned work profile devices that currently have a custom profile assigned won't experience any immediate change of functionality. Because these profiles are no longer supported, the functionality set by these profiles might change in the future.

- Intune technical support no longer supports custom profiles for personally owned work profile devices.

All custom policies should be replaced with other policy types. Learn more about [Intune ending support for personally owned work profile custom profiles](https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-ending-support-for-custom-profiles-for-personally-owned-work-profile-devi/4287414)

### Device security

#### New settings added to the Windows security baseline version 24H2<!-- 32413310 -->

> [!NOTE]
> Rollout of the new settings for the security baseline is underway, but taking longer than usual. Due to this delay, the new settings might not be available until the week of May 5, 2025.

The most recent Intune security baseline for Windows, version 24H2, is updated to include 15 new settings for managing the Windows Configuration Service Provider (CSP) for [*Lanman Server*](/windows/client-management/mdm/policy-csp-lanmanserver) and [*Lanman Workstation*](/windows/client-management/mdm/policy-csp-lanmanworkstation). These settings were previously unavailable in the baseline due to missing CSP support. The addition of these settings provides better control and configuration options.
 
Because this is an update to an existing baseline version and not a new baseline version, the new settings aren't visible in the baselines properties until you edit and save the baseline:
 
- **Pre-existing baseline instances**:  
Before the new settings are available in a preexisting baseline instance, you must select and then *Edit* that baseline instance. To have the baseline deploy the new settings, you must then *Save* that baseline instance. When the baseline is opened for editing, each of the new settings becomes visible with its default security baseline configuration. Before saving, you can reconfigure one or more of the new settings or make no changes other than to save the current configuration that then uses the baseline defaults for each of the new settings.

- **New baseline instances**:  
When you create a new instance of a Windows security baseline version 24H2, that instance includes the new settings along with all the previously available settings.
 
Following are the new settings that are added to the version 24H2 baseline, and the baseline default for each:
[**Lanman Server**](../protect/security-baseline-settings-mdm-all.md?pivots=mdm-24h2#lanman-server)  
- [Audit Client Does Not Support Encryption](/windows/client-management/mdm/policy-csp-lanmanserver#auditclientdoesnotsupportencryption) – Baseline default: *Enabled*
- [Audit Client Does Not Support Signing](/windows/client-management/mdm/policy-csp-lanmanserver#auditclientdoesnotsupportsigning) – Baseline default: *Enabled*
- [Audit Insecure Guest Logon](/windows/client-management/mdm/policy-csp-lanmanserver#auditinsecureguestlogon) – Baseline default: *Enabled*
- [Auth Rate Limiter Delay In Ms](/windows/client-management/mdm/policy-csp-lanmanserver#authratelimiterdelayinms) – Baseline default: *2000*
- [Enable Auth Rate Limiter](/windows/client-management/mdm/policy-csp-lanmanserver#enableauthratelimiter) – Baseline default: *Enabled*
- [Max SMB 2 Dialect](/windows/client-management/mdm/policy-csp-lanmanserver#maxsmb2dialect) – Baseline default: *SMB 3.1.1*
- [Min SMB 2 Dialect](/windows/client-management/mdm/policy-csp-lanmanserver#minsmb2dialect) – Baseline default: *SMB 3.0.0*
- [Enable Mailslots](/windows/client-management/mdm/policy-csp-lanmanserver#enablemailslots) - Baseline default: *Disabled*

[**Lanman Workstation**](../protect/security-baseline-settings-mdm-all.md?pivots=mdm-24h2#lanman-workstation)  
- [Audit Insecure Guest Logon](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#auditinsecureguestlogon) – Baseline default: *Enabled*
- [Audit Server Does Not Support Encryption](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#auditserverdoesnotsupportencryption) – Baseline default: *Enabled*
- [Audit Server Does Not Support Signing](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#auditserverdoesnotsupportsigning) – Baseline default: *Enabled*
- [Max SMB 2 Dialect](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#maxsmb2dialect) – Baseline default: *SMB 3.1.1*
- [Min SMB 2 Dialect](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#minsmb2dialect) – Baseline default: *SMB 3.0.0*
- [Require Encryption](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#requireencryption) – Baseline default: *Disabled*
- [Enable Mailslots](/windows/client-management/mdm/policy-csp-LanmanWorkstation#enablemailslots) - Baseline default: *Disabled*

For more information, see [Intune security baselines](../protect/security-baselines.md).

### Intune apps

#### Newly available protected apps for Intune<!-- 31436626, 31437166, 31494251 -->

The following protected apps are now available for Microsoft Intune:

- FileOrbis for Intune by FileOrbis FZ LLC
- PagerDuty for Intune by PagerDuty, Inc.
- Outreach.io by Outreach Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Tenant administration

#### Updates to Intune admin center home page<!-- 25914324 -->

Microsoft Intune admin center's home page has been updated to include additional links to interactive demos, documentation, and training. To see these updates, navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

## Week of April 14, 2025

### Device configuration

#### Hotpatch updates for Windows 11 Enterprise are now available<!--27009405 -->

Hotpatch updates for Windows 11 Enterprise, version 24H2 for x64 (AMD/Intel) CPU devices are now available. With hotpatch updates, you can deploy and apply security updates faster to help protect your organization from cyberattacks, while minimizing user disruptions.
From the Microsoft Intune admin center, navigate to **Devices > Windows updates > Create Windows quality update policy** and toggle it to **Allow**.

**Enroll and prepare**
The Windows quality update policy can auto-detect if your targeted devices are eligible for hotpatch updates. Devices running Windows 10 and Windows 11, version 23H2 and lower will continue to receive the standard monthly security updates, helping ensure that your ecosystem stays protected and productive.

**Maintain robust security with hotpatch updates**
The general availability of hotpatch technology for Windows clients marks a significant step forward in enhancing security and productivity for Windows 11 Enterprise users.
Hotpatch updates help ensure that devices are secured more quickly and that users stay productive with minimal disruptions. We encourage organizations to take advantage of this new feature to maintain a robust security posture while minimizing the impact on the user experience. Hotpatch updates are generally available on Intel and AMD-powered devices as of April 2, 2025, with the feature becoming available on Arm64 devices at a later date.

For more information, see:

- [Hotpatch for Windows client now available - Windows IT Pro Blog](https://techcommunity.microsoft.com/blog/windows-itpro-blog/hotpatch-for-windows-client-now-available/4399808)

- [Hotpatch updates](/windows/deployment/windows-autopatch/manage/windows-autopatch-hotpatch-updates)
- [Hotpatch for client comes to Windows 11 Enterprise](https://techcommunity.microsoft.com/blog/windows-itpro-blog/hotpatch-for-client-comes-to-windows-11-enterprise/4302717)

- [Skilling: Hotpatch on Windows client and server](https://techcommunity.microsoft.com/blog/windows-itpro-blog/skilling-snack-hotpatch-on-windows-client-and-server/4358086)

- [The hottest way to update Windows 11 and Windows Server 2025](https://techcommunity.microsoft.com/event/windowsevents/the-hottest-way-to-update-windows-11-and-windows-server-2025/4376174)

- [Hotpatch release notes](https://support.microsoft.com/help/5048812)

## Week of March 24, 2025

### Device security

### New Microsoft Tunnel readiness check for auditd package<!-- 28148207 -->

The [Microsoft Tunnel readiness tool](../protect/microsoft-tunnel-prerequisites.md#run-the-readiness-tool) now includes a check for the **auditd** package for Linux System Auditing (LSA). The presence of *auditd* is optional and not a required prerequisite by Microsoft Tunnel for the Linux server.

When the mst-readiness tool runs, it now raises a non-blocking warning if the audit package isn't installed. By default, Red Hat Enterprise Linux versions 7 and later install this package by default. Ubuntu versions of Linux currently require this optional package to be installed.

For more information on *auditd* and how to install it on your Microsoft Tunnel server, see [Linux system auditing](../protect/microsoft-tunnel-prerequisites.md#linux-system-auditing).

## Week of March 17, 2025 (Service release 2503)

### Microsoft Intune Suite

#### Endpoint Privilege Management support for ARM 64-bit devices<!-- 28313554 -->

[Endpoint Protection Manager](/mem/intune/protect/epm-overview) (EPM) now supports managing file elevations on devices that run on ARM 64-bit architecture.

Applies to:

- Windows

### Device configuration

#### New settings available in the Apple settings catalog <!-- 31056047 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Restrictions**:
- Allow Apple Intelligence Report
- Allow Default Calling App Modification
- Allow Default Messaging App Modification
- Allow Mail Smart Replies
- Allow Notes Transcription
- Allow Safari Summary

##### macOS

**Remote Desktop**:
- Remote Desktop

**Restrictions**:
- Allow Apple Intelligence Report
- Allow Mail Smart Replies
- Allow Notes Transcription
- Allow Safari Summary

### Device management

#### New settings for Windows LAPS policy<!-- 30287386 -->

Intune policies for [Windows Local Administrator Password Solution (LAPS)](../protect/windows-laps-overview.md) now include several new settings and updates to two previously available settings. Use of [LAPS](/windows-server/identity/laps/laps-overview) which is a Windows built-in solution can help you secure the built-in local administrator account that is present on each Windows device. All the settings that you can manage through Intune LAPS policy are described in the Windows [LAPS CSP](/windows/client-management/mdm/LAPS-csp).

The following new settings are available: *(Each setting name is a link that opens the CSP documentation for that setting.)*

- [Automatic Account Management Enable Account](/windows/client-management/mdm/laps-csp#policiesautomaticaccountmanagementenableaccount)
- [Automatic Account Management Enabled](/windows/client-management/mdm/laps-csp#policiesautomaticaccountmanagementenabled)
- [Automatic Account Management Name Or Prefix](/windows/client-management/mdm/laps-csp#policiesautomaticaccountmanagementnameorprefix)
- [Automatic Account Management Randomize Name](/windows/client-management/mdm/laps-csp#policiesautomaticaccountmanagementrandomizename)
- [Automatic Account Management Target](/windows/client-management/mdm/laps-csp#policiesautomaticaccountmanagementtarget)
- [Passphrase Length](/windows/client-management/mdm/laps-csp#policiespassphraselength)

The following settings have new options available:

- [Password Complexity](/windows/client-management/mdm/laps-csp#policiespasswordcomplexity) – The following are new options available for this setting:
  - Passphrase (long words)
  - Passphrase (short words)
  - Passphrase (short words with unique prefixes)
- [Post Authentication Actions](/windows/client-management/mdm/laps-csp#policiespostauthenticationactions) - The following option is now available for this setting:
  - Reset the password, logoff the managed account, and terminate any remaining processes: upon expiration of the grace period, the managed account password is reset, any interactive logon sessions using the managed account are logged off, and any remaining processes are terminated.

By default, each setting in LAPS policies is set to *Not configured*, which means the addition of these new settings won't change the behavior of your existing policies. To make use of the new settings and options, you can create new profiles or edit your existing profiles.

Applies to:

- Windows

#### Configure devices to stay on the latest OS version using declarative device management (DDM)<!-- 28323647 -->

As part of the [Settings Catalog](../configuration/settings-catalog.md), you can now configure devices to automatically update to the latest OS version using DDM. To use these new settings in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS**for platform > **Settings catalog** for profile type.

**Declarative device management > Software Update Enforce Latest**.

- **Enforce Latest Software Update Version**: If true, devices will upgrade to the latest OS version that is available for that device model. This uses the Software Update Enforcement configuration and will force devices to restart and install the update after the deadline passes.
- **Delay In Days**: Specify the number of days that should pass before a deadline is enforced. This delay is based on either the posting date of the new update when released by Apple, or when the policy is configured.
- **Install Time**: Specify the local device time for when updates are enforced. This setting uses the 24-hour clock format where midnight is 00:00 and 11:59pm is 23:59. Ensure that you include the leading 0 on single digit hours. For example, 01:00, 02:00, 03:00.

Learn more about configuring managed updates through DDM at [Managed software updates](../protect/managed-software-updates-ios-macos.md).

Applies To:

- iOS/iPadOS
- macOS

#### Remote Help supports Azure Virtual Desktop muti-session<!-- 24590822 -->

Remote Help now provides support for multi-session AVD with several users on a single virtual machine. Earlier, Remote Help was supporting Azure Virtual Desktop (AVD) sessions with one user on one virtual machine (VM).

For more information, see:

- [Remote Help](../fundamentals/remote-help.md)
- [Remote Help on windows](../fundamentals/remote-help-windows.md)
- [Using Azure Virtual Desktop multi-session with Microsoft Intune](../fundamentals/azure-virtual-desktop-multi-session.md)

#### Copilot assistant for device query<!-- 26933762 -->

You can now use Copilot to generate a KQL query to help you get data from across multiple devices in Intune. This capability is available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Device query** > **Query with Copilot**. For more information, see [Query with Copilot in device query](../copilot/copilot-intune-overview.md#-use-copilot-to-create-kql-queries-to-get-device-details).

### Intune apps

#### Newly available protected apps for Intune<!-- 31070614, 31093579, 31093668, 31187306 -->

The following protected apps are now available for Microsoft Intune:

- FacilyLife by Apleona GmbH (iOS)
- Intapp 2.0 by Intapp, Inc. (Android)
- DealCloud by Intapp, Inc. (Android)
- Lemur Pro for Intune by Critigen LLC (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of March 03, 2025

### Monitor and troubleshoot

#### Updates to the Feature updates report<!--31305861 -->

We are introducing a new **Update Substate** in Service-side data. This substate is displayed in the reports for devices that are invalid in Microsoft Entra and is known as **Not supported**.

For more information, see [Use Windows Update for Business reports for Windows Updates](../protect/windows-update-reports.md#use-the-windows-10-feature-updates-organizational-report)

## Week of February 24, 2025 (Service release 2502)

### App management

#### VPP token name more easily available in Apps workload<!-- 5479088 -->

The **VPP token name** column, available in the Apps workload, allows you to quickly determine the token and app association. This column is now available in the **All apps** list (**Apps** > **All apps**) and the app selection pane for **App configuration policies** (**Apps** > **App configuration policies**). For more information about VPP apps, see [Manage volume-purchased apps and books with Microsoft Intune](../apps/vpp-apps.md).

Applies to:

- iOS/iPadOS
- macOS

### Device configuration

#### New Windows AI settings available in the Windows settings catalog<!-- 30339749 -->

The Settings Catalog lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog for Windows. To see these settings, in the Microsoft Intune admin center, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** > **Settings catalog** for profile type.

The new settings are:

- Disable AI Data Analysis
- Set Deny Uri List For Recall
- Set Deny App List For Recall
- Set Maximum Storage Space For Recall Snapshots
- Set Maximum Storage Duration For Recall Snapshots

Applies to:

- Windows

#### Low privileged account for Intune Connector for Active Directory for Hybrid join Windows Autopilot flows<!-- 28662823 -->

We've updated the Intune Connector for Active Directory to use a low privileged account to increase the security of your environment. The old connector will continue to work until deprecation in late May 2025.

For more information, see [Deploy Microsoft Entra hybrid joined devices by using Intune and Windows Autopilot](../../autopilot/windows-autopilot-hybrid.md).

#### Managed Home Screen QR Code Authentication in public preview<!-- 25348926 -->

Managed Home Screen for Android devices natively supports QR Code Authentication in Microsoft Entra ID. Authentication involves both a QR code and PIN. This capability eliminates the need for users to enter and re-enter long UPNs and alphanumeric passwords. For more information, see [Sign in to Microsoft Teams or Managed Home Screen (MHS) with QR code](/entra/identity/authentication/how-to-authentication-qr-code#sign-in-to-microsoft-teams-or-managed-home-screen-mhs-with-qr-code).

Applies to:

- Android devices

#### Additional device details for Managed Home Screen<!-- 27006536 -->

Android **OS version**, **Security patch**, and **Last device reboot time** details are now available from the **Device Information** page of the Managed Home Screen app. For related information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

Applies to:

- Android Enterprise devices

#### Display ringtone selector for Managed Home Screen<!-- 26826233 -->

In Intune, you can choose to expose a setting in the Managed Home Screen app to allow users to select a ringtone. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

Applies to:

- Android devices

### Device security

#### Manage the DeviceControlEnabled configuration for Microsoft Defender Device Control on Windows devices<!-- 31171641 -->

You can now use Intune to manage the configuration of the Microsoft Defender CSP for [DeviceControlEnabled](/windows/client-management/mdm/defender-csp#configurationdevicecontrolenabled) for Device Control. DeviceControlEnabled is used to enable or disable support for the Microsoft Defender Device Control feature on Windows devices.

You can use the following two Microsoft Intune options to configure DeviceControlEnabled. With both options, the setting appears as **Device Control Enabled**, and is found in the *Defender* category:

- Configure a [**Device Control** template](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy), which is a profile for [Attack Surface Reduction](../protect/endpoint-security-asr-policy.md) policy.
- Configure a [**Settings Catalog** profile](../configuration/settings-catalog.md#create-the-policy) for Windows.

Both the Device Control template and Settings Catalog support the following options for *Device Control Enabled*:

- Device Control is enabled
- Device Control is disabled (Default)

Applies to:

- Windows

#### Manage the DefaultEnforcement configuration for Microsoft Defender Device Control on Windows devices<!-- 30253799 -->

You can now use Intune to manage the configuration of the Microsoft Defender CSP for [DefaultEnforcement](/windows/client-management/mdm/defender-csp#configurationdefaultenforcement) for Device Control. DefaultEnforcement manages the configuration of Device Control on devices that don't receive Device Control policies or for devices that receive and evaluate a policy for Device Control when no rules in the policy are matched.

You can use the following two Microsoft Intune options to configure DefaultEnforcement. With both options, the setting appears as **Default Enforcement**, and is found in the *Defender* category:

- Configure a [**Device Control** template](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy), which is a profile for [Attack Surface Reduction](../protect/endpoint-security-asr-policy.md) policy.
- Configure a [**Settings Catalog** profile](../configuration/settings-catalog.md#create-the-policy) for Windows.

Both the Device Control template and Settings Catalog support the following options for *Default Enforcement*:

- Default Allow Enforcement (Default)
- Default Deny Enforcement

Applies to:

- Windows

### Intune apps

#### Newly available protected app for Intune<!-- 30508606 -->

The following protected app is now available for Microsoft Intune:

- Applications Manager - Intune by ManageEngine

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Device configuration

#### New settings available in the Apple settings catalog<!-- 30457000 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings For Apple devices in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

#### iOS/iPadOS

**Managed Settings**:
- Default Applications
- Wallpaper

**Networking > Domains**:
- Cross Site Tracking Prevention Relaxed Apps

**Restrictions**:
- Allowed External Intelligence Workspace IDs
- Allow Notes Transcription Summary
- Allow Satellite Connection
- Allow Visual Intelligence Summary

#### macOS

**Networking > Domains**:

- Cross Site Tracking Prevention Relaxed Apps

**Restrictions**:

- Allow Bookstore
- Allow Bookstore Erotica
- Allow Explicit Content
- Rating Apps
- Rating Movies
- Rating Region
- Rating TV Shows

**System Configuration > File Provider**:

- Management Allows Known Folder Syncing
- Management Known Folder Syncing Allow List


## Week of February 17, 2025

### Monitor and troubleshoot

#### Limited live chat support in Intune<!-- 30477421 -->

Intune is introducing limited live chat support within the Intune admin console. Live chat isn't available for all tenants or inquiries at this time.

## Week of February 10, 2025

### Device security

#### Updated security baseline for Windows version 24H2<!-- 29819143 -->

You can now deploy the Intune security baseline for **Windows version 24H2** to your Windows 10 and Windows 11 devices. The new baseline version uses the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline represents the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows

### Monitor and troubleshoot

#### Device Query for Multiple Devices<!--25234456 -->

We've added Device query for multiple devices. This feature allows you to gain comprehensive insights about your entire fleet of devices using Kusto Query Language (KQL) to query across collected inventory data for your devices.

Device query for multiple devices is now supported for devices running Windows 10 or later. This feature is now included as part of Advanced Analytics.

Applies to:

- Windows

## Week of February 5, 2025 (Service release 2501)

### Microsoft Intune Suite

#### Use Microsoft Security Copilot with Endpoint Privilege Management to help identify potential elevation risks<!-- 27265509 -->

When your Azure Tenant is licensed for Microsoft Security Copilot, you can now use Security Copilot to help you investigate Endpoint Privilege Management (EPM) file elevation requests from within the EPM [support approved](../protect/epm-support-approved.md#use-microsoft-security-copilot-to-analyze-file-elevation-requests) work flow.

With this capability, while reviewing the properties of a file elevation request, you'll now find option to **Analyze with Copilot**. Use of this option directs Security Copilot to use the files hash in a prompt Microsoft Defender Threat Intelligence to evaluate the file potential indicators of compromise so you can then make a more informed decision to either approve or deny that file elevation request. Some of the results that are returned to your current view in the admin center include:

- The files' reputation
- Information about the trust of the publisher
- The risk score for the user requesting the file elevation
- The risk score of the device from which the elevation was submitted

EPM is available as an [Intune Suite add-on-capability](../fundamentals/intune-add-ons.md). To learn more about how you can currently use Copilot in Intune, see [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md).

To learn more about Microsoft Security Copilot, see, [Microsoft Security Copilot](/copilot/security/microsoft-security-copilot).

### App management

#### Update to Apps workload experience in Intune<!-- 15507048 -->

The Apps area in Intune, commonly known as the Apps workload, is updated to provide a more consistent UI and improved navigation structure so you can find the information you need faster. To find the **App** workload in Intune, navigate to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Apps**.

### Device configuration

#### New settings available in the Windows settings catalog to Configure multiple display mode<!-- 30305854 -->

The Settings Catalog lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog to *Configure Multiple Display Mode* for
Windows 24H2. To see available settings, in the Microsoft Intune admin center, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later for platform** > **Settings catalog** for profile type.

The **Configure Multiple Display Mode** setting allows monitors to extend or clone the display by default, facilitating the need for manual setup. It streamlines the multi-monitor configuration process, ensuring a consistent and user-friendly experience.

Applies to:

- Windows

### Device security

#### Updated security baseline for Microsoft Edge v128<!-- 29463902 -->

You can now deploy the Intune security baseline for **Microsoft Edge version 128**. This update brings support for recent settings so you can continue to maintain best-practice configurations for Microsoft Edge.

[View the default configuration of settings in the updated baseline](../protect/security-baseline-v2-edge-settings.md?pivots=edge-v128).

For information about security baselines with Intune, see [Use security baselines to configure Windows devices in Intune](../protect/security-baselines.md).

Applies to:

- Windows

### Intune apps

#### Newly available protected app for Intune<!-- 30061339 -->

The following protected app is now available for Microsoft Intune:

- MoveInSync by MoveInSync Technologies

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of January 27, 2025

### Device security

#### Security baselines for HoloLens 2<!-- 24914095 -->

You can now deploy two distinct instances of the security baseline for HoloLens 2. These baselines represent Microsoft's best practice guidelines and experience from deploying and supporting HoloLens 2 devices to customers across various industries. The two baselines instances:

- **Standard Security Baseline for HoloLens 2**:
  The standard security baseline for HoloLens 2 represents the recommendations for configuring security settings that are applicable to all types of customers irrespective of HoloLens 2 use case scenarios. [View the default configuration of settings in the standard security baseline](../protect/security-baseline-hololens2-standard.md).

- **Advanced Security Baseline for HoloLens 2**:
  The advanced security baseline for HoloLens 2 represents the recommendations for configuring security settings for the customers who have strict security controls of their environment and require stringent security policies to be applied to any device used in their environment. [View the default configuration of settings in the advanced security baseline](../protect/security-baseline-hololens2-advanced.md).

To learn more about security baselines with Intune, see [Use security baselines to configure Windows devices in Intune](../protect/security-baselines.md).

Applies to:

- Windows

## Week of January 20, 2025

### Monitor and troubleshoot

#### Use Support Assistant to resolve issues<!-- 29084113 -->

Support Assistant is now available in Intune. It leverages AI to enhance your help and support experience, ensuring more efficient issue resolution. Support Assistant is available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshoot + support** > **Help and Support**, or by selecting the question mark near your profile pic. Currently, the Support Assistant is in preview. You can enable and disable Support Assistant by choosing to opt in and opt out at any time. For related information, see [How to get support in the Microsoft Intune admin center](/mem/get-support).

## Week of December 30, 2024

### Device enrollment

#### Intune ends support for Android device administrator on devices with access to Google Mobile Services<!-- 24563742 -->
As of December 31, 2024, Microsoft Intune no longer supports Android device administrator management on devices with access to Google Mobile Services (GMS). This change comes after Google deprecated Android device administrator management and ceased support. Intune support and help documentation remains for devices without access to GMS running Android 15 or earlier, and Microsoft Teams devices migrating to Android Open Source Project (AOSP) management. For more information about how this change impacts your tenant, see [Intune ending support for Android device administrator on devices with GMS access in December 2024](https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-ending-support-for-android-device-administrator-on-devices-with-gms-in-de/3915443).


## Week of December 16, 2024 (Service release 2412)

### App management

#### Increased scale for Customization policies<!-- 25308499 -->

You can now create up to 25 policies that customize the Company Portal and Intune app experience. The previous maximum number of Customization policies was 10. Navigate to the Intune admin center, and select **Tenant administration** > **Customization**.

For more information about customizing the Company Portal and Intune apps, see [Customizing the user experience](../apps/company-portal-app.md#customizing-the-user-experience).

### Device security

#### Support for tamper protection in policies for Security settings management for Microsoft Defender for Endpoint<!-- 13204113 -->

You can now manage the Microsoft Defender for Endpoint CSP setting for [tamper protection](/windows/client-management/mdm/defender-csp) on unenrolled devices you manage as part of the [Defender for Endpoint security settings management](../protect/mde-security-integration.md#which-solution-should-i-use) scenario.

With this support, tamper protection configurations from *Windows Security Experience* profiles for *Antivirus* policies now apply to all devices instead of only to those that are enrolled with Intune.

### Device configuration

#### Ending support for administrative templates when creating a new configuration profile<!-- 29989512 -->

Customers cannot create new Administrative Templates configuration profile through **Devices > Configuration > Create > New policy > Windows 10 and later > Administrative Templates**. A (retired) tag is seen next to **Administrative Templates** and the **Create** button is now greyed out. Other templates continue to be supported.

However, customers can now use the Settings Catalog for creating new **Administrative Templates** configuration profile by navigating to **Devices > Configuration > Create > New policy > Windows 10 and later > Settings Catalog**.

There are no changes in the following UI experiences:

- Editing an existing Administrative template.
- Deleting an existing Administrative template.
- Adding, modifying, or deleting settings in an existing Administrative template.
- **Imported Administrative templates (Preview)** template, which is used for Custom ADMX.

For more information, see [Use ADMX templates on Windows 10/11 devices in Microsoft Intune](..\configuration\administrative-templates-windows.md).

Applies to:

- Windows

### Device management

#### More Wi-Fi configurations are now available for personally-owned work profile devices<!-- 28331156 -->

Intune Wi-Fi configuration profiles for Android Enterprise personally-owned work profile devices now support configuration of pre-shared keys and proxy settings.

You can find these settings in the admin console in **Devices** > **Manage devices** > **Configuration** > **Create** > **New Policy**. Set **Platform** to Android Enterprise and then in the **Personally-Owned Work Profile** section, select Wi-Fi and then select the **Create** button.

In the **Configuration settings** tab, when you select Basic Wi-Fi type, several new options are available:

1. Security type, with options for Open (no authentication), WEP-Pre-shared key, and WPA-Pre-shared key.

2. Proxy settings, with the option to select Automatic and then specify the proxy server URL.

It was possible to configure these in the past with Custom Configuration policies, but going forward, we recommend setting these in the Wi-Fi Configuration profile, because [Intune is ending support for Custom policies in April 2024.](https://aka.ms/Intune/Android-customprofiles).

For more information, see [Wi-Fi settings for personally-owned work profile devices.](../configuration/wi-fi-settings-android-enterprise.md).

Applies to:

- Android Enterprise

## Week of December 9, 2024

### Tenant administration

#### Intune now supports Ubuntu 24.04 LTS for Linux management.<!--28363586 -->

We're now supporting device management for Ubuntu 24.04 LTS. You can enroll and manage Linux devices running Ubuntu 24.04, and assign standard compliance policies, custom configuration scripts, and compliance scripts.

For more information, see the following in Intune documentation:

- [Deployment guide: Manage Linux devices in Microsoft Intune](../fundamentals/deployment-guide-platform-linux.md)
- [Enrollment guide: Enroll Linux desktop devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-linux.md). To enroll Linux devices, ensure that they're running Ubuntu 20.04 LTS or higher.

Applies to:

- Linux Ubuntu Desktops

## Week of December 2, 2024

### Device enrollment

#### Change to enrollment behavior for iOS enrollment profile type<!-- 29068674 -->

At Apple WWDC 2024, Apple ended support for profile-based Apple user enrollment. For more information, see [Support has ended for profile-based user enrollment with Company Portal](../fundamentals/whats-new-archive.md#support-has-ended-for-apple-profile-based-user-enrollment-with-company-portal). As a result of this change, we updated the behavior that occurs when you select **Determine based on user choice** as the enrollment profile type for bring-your-own-device (BYOD) enrollments.

Now when users select **I own this device** during a BYOD enrollment, Microsoft Intune enrolls them via account-driven user enrollment, rather than profile-based user enrollment, and then secures only work-related apps. Less than one percent of Apple devices across all Intune tenants are currently enrolled this way, so this change doesn't affect most enrolled devices. There is no change for iOS users who select **My company owns this device** during a BYOD enrollment. Intune enrolls them via device enrollment with Intune Company Portal, and then secures their entire device.

If you currently allow users in BYOD scenarios to determine their enrollment profile type, you must take action to ensure account-driven user enrollment works by completing all prerequisites. For more information, see [Set up account driven Apple user enrollment](../enrollment/apple-account-driven-user-enrollment.md). If you don't give users the option to choose their enrollment profile type, there are no action items.

### Device management

#### Device Inventory for Windows<!-- 24853010 -->

Device inventory lets you collect and view additional hardware properties from your managed devices to help you better understand the state of your devices and make business decisions.

You can now choose what you want to collect from your devices, using the catalog of properties and then view the collected properties in the Resource Explorer view.

For more information, see:

- [Properties catalog](../configuration/properties-catalog.md)
- [Data collection platform](../../analytics/data-platform-schema.md)

Applies to:

- Windows 10 and later (Corporate owned devices managed by Intune)

## What's new archive
<!-- Past announcements that are older than six months will be moved to the archive -->

For previous months, see the [What's new archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
