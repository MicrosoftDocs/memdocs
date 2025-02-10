---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 02/06/2025
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
 
# optional metadata

#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. Also:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description will move from this article to [What's new](whats-new.md).
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](whats-new.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

<!-- Common categories: use this order:
## Microsoft Intune Suite
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

## Microsoft Intune Suite

### Endpoint Privilege Management support for Arm64<!-- 28313554 -->

You'll soon be able to use [Endpoint Protection Management](/mem/intune/protect/epm-overview) (EPM) file elevations on devices that run on Arm64 architecture.

Applies to:

- Windows

### Endpoint Privilege Management elevation rule support for file arguments and parameters<!--28077130 -->

Soon, the file elevation rules for Endpoint Privilege Management (EPM) will support use of arguments or parameters that you want to allow. Arguments and parameters that aren't explicitly allowed will be blocked from use. This capability helps to improve control of the context for file elevations.

EPM is available as an [Intune Suite add-on-capability](../fundamentals/intune-add-ons.md).

<!-- ***********************************************-->

## App management

### Additional device details for Managed Home Screen<!-- 27006536 -->

Android **OS version**, **Security patch** and **Last device reboot time** details will be available from the **Device Information** page of the Managed Home Screen app. For related information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

Applies to:
- Android Enterprise devices

### Managed Home Screen authentication support in public preview<!-- 25348926 -->
Managed Home Screen for Android devices will natively support authentication in Microsoft Entra ID with a QR code and PIN. This capability will eliminate the need for users to enter and re-enter long UPNs and alphanumeric passwords.

Applies to:

- Android devices


### Display ringtone selector for Managed Home Screen<!-- 26826233 -->

In Intune, you can choose to expose a setting in the Managed Home Screen app to allow users to select a ringtone. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

Applies to:

- Android devices

### Add Enterprise App Catalog apps to ESP blocking apps list<!-- 29846319 -->

Enterprise App Catalog apps will be supported with Windows Autopilot. Microsoft Intune Enterprise App Management enables IT admins to easily manage applications from the Enterprise App Catalog. Using Windows Autopilot, you'll be able to select blocking apps from the Enterprise App Catalog in the Enrollment Status Page (ESP) and the Device Preparation Page (DPP) profiles. This allows you to update apps more easily without needing to update those profiles with the latest versions. 

For related information, see [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md), [Overview of Windows Autopilot device preparation](/autopilot/device-preparation/overview), and [Add an Enterprise App Catalog app to Microsoft Intune](../apps/apps-add-enterprise-app.md).

Applies to:

- Windows

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies now provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

## Device configuration

### New Default Enforcement device control setting available in the Windows settings catalog<!-- 30253799 -->

The Settings Catalog lists all the settings you can configure in a device policy, and all in one place.

There will soon be new settings in the Settings Catalog for Windows 24H2. To see these settings, in the Microsoft Intune admin center, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later ** > **Settings catalog** for profile type.

This setting is available in both the settings catalog and the ASR device control template. The Default Enforcement device control setting enables a default enforcement to be applied if:

- There are no policy rules present, or
- At the end of the policy rules evaluation none were matched.

Applies to:

- Windows

### New settings available in the Apple settings catalog<!-- 30457000 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

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

### Android settings in the Settings Catalog <!-- 26981326 -->

The settings catalog will soon support Android Enterprise and AOSP.

Currently, to configure Android settings, you use the built-in templates. The settings from these templates are also available in the settings catalog. More settings will continue to be added.

In the Intune admin center, when you create a device configuration profile, you select the **Profile Type** (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > select your **Platform** > **Profile Type**). All the profile types are moved to **Profile Type** > **Templates**.

This change:

- Will be a UI change with no impact on your existing policies. Your existing policies won't change. You'll still be able to create, edit, and assign these policies the same way.
- Will be the same UI experience as iOS/iPadOS, macOS, and Windows templates.

To get started with settings catalog, go to [Use the settings catalog to configure settings on your devices](../configuration/settings-catalog.md).

Applies to:

- Android Enterprise
- AOSP

### Low privileged account for Intune Connector for Active Directory for Hybrid join Autopilot flows<!-- 28662823 -->

We're updating the Intune Connector for Active Directory to use a low privileged account to increase the security of your environment. The old connector will no longer be available for download but will continue to work until deprecation.

For more information, see [Deploy Microsoft Entra hybrid joined devices by using Intune and Windows Autopilot](../../autopilot/windows-autopilot-hybrid.md).

<!-- *********************************************** -->

<!--  ## Device enrollment  -->

<!-- *********************************************** -->

## Device management

### New settings for Windows LAPS policy<!-- 30287386 -->

We are updating Intunes policies for [Windows Local Administrator Password Solution (LAPS)](../protect/windows-laps-overview.md) by adding new settings and updating some existing settings. Use of [LAPS](/windows-server/identity/laps/laps-overview) which is a Windows built-in solution can help you secure the built-in local administrator account that is present on each Windows device.  

The new settings will include the following:

- AutomaticAccountManagementEnabled
- AutomaticAccountManagementTarget
- AutomaticAccountManagementNameOrPrefix
- AutomaticAccountManagementEnableAccount
- AutomaticAccountManagementRandomizeName
- PassphraseLength

The following settings will update to support new options:

- PasswordComplexity
- PostAuthenticationActions

The settings found in Intune LAPS policy are available from the Windows [LAPS CSP](/windows/client-management/mdm/LAPS-csp).

Applies to:

- Windows

### Configure devices to stay on the latest OS version using declarative device management (DDM)<!-- 28323647 -->

As part of the [Settings Catalog](../configuration/settings-catalog.md), you'll be able to configure devices to automatically update to the latest OS version using DDM. To use these new settings in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** for platform > **Settings catalog** for profile type.

**Declarative device management > Software Update Enforce Latest**.

- **Enforce Latest Software Update Version**: If true, devices will upgrade to the latest OS version that is available for that device model. This uses the Software Update Enforcement configuration and will force devices to restart and install the update after the deadline passes.
- **Delay In Days**: Specify the number of days that should pass before a deadline is enforced after a new update is released by Apple.
- **Install Time**: Specify the local device time for when updates are enforced. This setting uses the 24-hour clock format where midnight is 00:00 and 11:59pm is 23:59. Ensure that you include the leading 0 on single digit hours. For example, 01:00, 02:00, 03:00.

Learn more about configuring managed updates through DDM at [Managed software updates] (../protect/managed-software-updates-ios-macos.md).

Applies To:

- iOS/iPadOS


### Remote actions with multiple administrative approval (MAA)<!-- 27043113 -->

Intune *access policies* help protect against a compromised administrative account by requiring that a second administrative account is used to approve a change before the change is applied. This capability is known as multiple administrative approvals (MAA). The remote actions **Retire**, **Wipe** and **Delete** will support MAA. Onboarding Remote device actions to MAA will help mitigate the risk of unauthorized or compromised remote actions being taken on device(s) by a single administrative account thereby enhancing the overall security posture of the environment.

For more information on multiple administrative approvals, see [Use multiple administrative approvals in Intune](../fundamentals/multi-admin-approval.md).

### Remote Help supports Azure Virtual Desktop multi-session <!-- 24590822 -->

Currently, Remote Help supports Azure Virtual Desktop (AVD) sessions with one user on one virtual machine (VM). Going forward, Remote Help will enable support for multi-session AVD with several users on a single virtual machine.

For more information, see:

- [Remote Help](../fundamentals/remote-help.md)
- [Using Azure Virtual Desktop multi-session with Microsoft Intune](../fundamentals/azure-virtual-desktop-multi-session.md)

###  Introducing platform level targeting of Device Cleanup rule<!-- 13835920 -->

We're adding a feature that will allow a customer to:

- Configure one device cleanup rule per platform (Windows, iOS/macOS, iPadOS, Android, Linux)
- Configure a different RBAC permission and assign the permission to different RBAC roles

Platform level targeting of the Device Cleanup rule will help administrators to remove stale and inactive devices from their tenant based on the active days rule specified by the admin. Scoped and targeted Device cleanup rules add an intermediate stage where an admin will be able to target removing stale devices by having a rule configured at the platform or OS level. 

For more information, see [device cleanup rules](../remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules).

### Copilot assistant for device query<!-- 26933762 -->

You'll soon be able to use Copilot to generate a KQL query to help you get data from across multiple devices in Intune. This capability will be available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Device query** > **Query with Copilot**.

<!-- *********************************************** -->

## Device security

### Updated security baseline for Windows version 24H2<!-- 29819143 -->

We're working on an update to add an Intune security baseline for **Windows version 24H2**. The new baseline version will use the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline will represent the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows

### Linux support for Endpoint detection and response exclusion settings<!-- 26549863 -->

We're adding a new Endpoint Security template under Endpoint detection and response (EDR) for the Linux platform that will be supported through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario.

The template will support settings related to global exclusion settings. Applicable to antivirus and EDR engines on the client, the settings can configure exclusions to stop associated real time protection EDR alerts for the excluded items. Exclusions can be defined by the file path, folder, or process explicitly defined by the admin in the policy.

Applies to:

- Linux

### New Microsoft Tunnel readiness check for auditd package<!-- 28148207 -->

We're updating the [Microsoft Tunnel readiness tool](../protect/microsoft-tunnel-prerequisites.md#run-the-readiness-tool) to detect if the **auditd** package for Linux System Auditing (LSA) is installed on your Linux Server. When this check is in place, the mst-readiness tool will raise a warning if the audit package isn't installed. Auditing isn't a required prerequisite for the Linux Server, but recommended.

For more information on *auditd* and how to install it on your Microsoft Tunnel server, see [Linux system auditing](../protect/microsoft-tunnel-prerequisites.md#linux-system-auditing).

### Support for Intune Device control policy for devices managed by Microsoft Defender for Endpoint<!-- 15466620 -->

You'll be able to use the endpoint security policy for *Device control* (Attack surface reduction policy) from the Microsoft Intune with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.

- **Device control** policies are part of endpoint security [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

Applies to the following when you use the *Windows 10, Windows 11, and Windows Server* platform:

- Windows 10
- Windows 11

When this change takes effect, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive this policy will get it.

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

## Monitor and troubleshoot

### Device Query for Multiple Devices<!--25234456 -->

We're adding Device query for multiple devices. This feature allows you to gain comprehensive insights about your entire fleet of devices using Kusto Query Language (KQL) to query across collected inventory data for your devices.

Device query for multiple devices will be supported for devices running Windows 10 or later. This feature will be included as part of Advanced Analytics.

Applies to:

- Windows

<!-- *********************************************** -->

<!-- ## Tenant administration -->

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
