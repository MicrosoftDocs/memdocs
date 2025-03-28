---
# required metadata
title: What's new in Microsoft Intune
titleSuffix:
description: Find out what's new in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/27/2025
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
- Information about [how Intune service updates are released](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728)

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

## Week of March 24, 2025

### Device security

### New Microsoft Tunnel readiness check for auditd package<!-- 28148207 -->

The [Microsoft Tunnel readiness tool](../protect/microsoft-tunnel-prerequisites.md#run-the-readiness-tool) now includes a check for the **auditd** package for Linux System Auditing (LSA). The presence of *auditd* is optional and not a required prerequisite by Microsoft Tunnel for the Linux server.

When the mst-readiness tool runs, it now raises a non-blocking  warning if the audit package isn't installed. By default, Red Hat Enterprise Linux versions 7 and later install this package by default. Ubuntu versions of Linux currently require this optional package to be installed.

For more information on *auditd* and how to install it on your Microsoft Tunnel server, see [Linux system auditing](../protect/microsoft-tunnel-prerequisites.md#linux-system-auditing).

## Week of March 17, 2025 (Service release 2503)

### Microsoft Intune Suite

#### Endpoint Privilege Manager support for ARM 64-bit devices<!-- 28313554 -->

[Endpoint Protection Manager](/mem/intune/protect/epm-overview) (EPM) now supports managing file elevations on devices that run on ARM 64-bit architecture.
 
Applies to:
 
- Windows

### Device configuration

#### New settings available in the Apple settings catalog <!-- 31056047 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

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

You can now use Copilot to generate a KQL query to help you get data from across multiple devices in Intune. This capability is available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Device query** > **Query with Copilot**. For more information, see [Query with Copilot in device query](../copilot/copilot-intune-overview.md#query-with-copilot-in-device-query).

### Intune apps

#### Newly available protected apps for Intune<!-- 31070614, 31093579, 31093668, 31187306 -->

The following protected apps are now available for Microsoft Intune:

- FacilyLife by Apleona GmbH (iOS)
- Intapp 2.0 by Intapp, Inc. (Andriod)
- DealCloud by Intapp, Inc. (Andriod)
- Lemur Pro for Intune by Critigen LLC (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).


## Week of March 03, 2025

### Monitor and troubleshoot

#### Updates to the Feature updates report<!--31305861 -->

We are introducing a new **Update Substate** in Service-side data. This substate is displayed in the reports for devices that are invalid in Microsoft Entra and is known as **Not supported**.

For more information, see [Use Windows Update for Business reports for Windows Updates](../protect/windows-update-reports.md#use-the-windows-10-feature-updates-organizational-report)

## Week of February 24, 2025  (Service release 2502)

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

#### Low privileged account for Intune Connector for Active Directory for Hybrid join Autopilot flows<!-- 28662823 -->

We've updated the Intune Connector for Active Directory to use a low privileged account to increase the security of your environment. The old connector will no longer be available for download but will continue to work until deprecation in late May 2025.

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

You can now use Intune to manage the configuration of the Microsoft Defender CSP for  [DefaultEnforcement](/windows/client-management/mdm/defender-csp#configurationdefaultenforcement) for Device Control. DefaultEnforcement manages the configuration of Device Control on devices that don’t receive Device Control policies or for devices that receive and evaluate a policy for Device Control when no rules in the policy are matched.

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

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

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

## Week of February 5, 2025  (Service release 2501)

### Microsoft Intune Suite
 
#### Use Microsoft Security Copilot with Endpoint Privilege Manager to help identify potential elevation risks<!-- 27265509 -->

When your Azure Tenant is licensed for Microsoft Security Copilot, you can now use Security Copilot to help you investigate Endpoint Privilege Manager (EPM) file elevation requests from within the EPM [support approved](../protect/epm-support-approved.md#use-microsoft-security-copilot-to-analyze-file-elevation-requests) work flow.

With this capability, while reviewing the properties of a file elevation request, you'll now find option to **Analyze with Copilot**. Use of this option directs Security Copilot to use the files hash in a prompt Microsoft Defender Threat Intelligence to evaluate the file potential indicators of compromise so you can then make a more informed decision to either approve or deny that file elevation request. Some of the results that are returned to your current view in the admin center include:

- The files’ reputation
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

You can now deploy two distinct instances of the security baseline for HoloLens 2. These baselines represent Microsoft’s best practice guidelines and experience from deploying and supporting HoloLens 2 devices to customers across various industries. The two baselines instances:

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

For more information, see [Wi-Fi settings for personally-owned work profile devices.](../configuration/wi-fi-settings-android-enterprise.md#personally-owned-work-profile).

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

## Week of November 18, 2024 (Service release 2411)

### App management

#### Configuration values for specific managed applications on Intune enrolled iOS devices<!-- 30293382 -->

Starting with Intune's September (2409) service release, the **IntuneMAMUPN**, **IntuneMAMOID**, and **IntuneMAMDeviceID** app configuration values are automatically sent to managed applications on Intune enrolled iOS devices for the following apps:

- Microsoft Excel
- Microsoft Outlook
- Microsoft PowerPoint
- Microsoft Teams
- Microsoft Word

For more information, see [Plan for Change: Specific app configuration values will be automatically sent to specific apps](../fundamentals/whats-new.md#plan-for-change-specific-app-configuration-values-will-be-automatically-sent-to-specific-apps) and Intune [Support tip: Intune MAM users on iOS/iPadOS userless devices may be blocked in rare cases](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-intune-mam-users-on-iosipados-userless-devices-may-be-blocked-in-rar/4254335).

#### Additional installation error reporting for LOB apps on AOSP devices<!-- 27157460 -->

Additional details are now provided for app installation reporting of Line of Business (LOB) apps on Android Open Source Project (AOSP) devices. You can view installation error codes and detailed error messages for LOB apps in Intune.

For information about app installation error details, see [Monitor app information and assignments with Microsoft Intune](../apps/apps-monitor.md#app-installation-error-reporting).

Applies to:

- Android Open Source Project (AOSP) devices

#### Microsoft Teams app protection on VisionOS devices (preview)<!-- 29913431 -->

Microsoft Intune app protection policies (APP) are now supported on the Microsoft Teams app on VisionOS devices. 

To learn more about how to target policies to VisionOS devices, see [Managed app properties](../fundamentals/filters-device-properties.md#managed-app-properties) for more information about filters for managed app properties.

Applies to:

- Microsoft Teams for iOS on VisionOS devices

## Week of October 28, 2024

### Device security

#### Defender for Endpoint security settings support in government cloud environments (generally available)<!-- 30064299 -->

Now generally available, customer tenants in the Government Community Cloud (GCC), US Government Community High (GCC High), and Department of Defense (DoD) environments can use Intune to manage the Defender security settings on the devices you’ve onboarded to Defender without enrolling those devices with Intune. Previously, support for Defender security settings was in public preview.

This capability is known as [Defender for Endpoint security settings management](../protect/mde-security-integration.md).

## Week of October 14, 2024 (Service release 2410)

### App management

#### Updates to app configuration policies for Android Enterprise devices<!-- 26711672 -->

App configuration policies for Android Enterprise devices now support overriding the following permissions:

- Access background location
- Bluetooth (connect)

For more information about app configuration policies for Android Enterprise devices, see [Add app configuration policies for managed Android Enterprise devices](../apps/app-configuration-policies-use-android.md).

Applies to:

- Android Enterprise devices

### Device configuration

#### Windows Autopilot device preparation support in Intune operated by 21Vianet in China<!-- MAXADO-9313795 / INADO-28687730 -->

Intune now supports *Windows Autopilot device preparation* policy for [Intune operated by 21Vianet in China](../fundamentals/china.md) cloud. Customers with tenants located in China can now use *Windows Autopilot device preparation* with Intune to provision devices.

For information about this Autopilot support, see the following in the Autopilot documentation:

- Overview: [Overview of Windows Autopilot device preparation](/autopilot/device-preparation/overview)
- Tutorial: [Windows Autopilot device preparation scenarios](/autopilot/device-preparation/tutorial/scenarios)

### Device management

#### Minimum OS version for Android devices is Android 10 and later for user-based management methods<!-- 14755802 -->

Beginning in October 2024, Android 10 and later is the [minimum Android OS version that is supported for user-based management methods](../fundamentals/supported-devices-browsers.md#android), which includes:

- Android Enterprise personally-owned work profile
- Android Enterprise corporate owned work profile
- Android Enterprise fully managed
- Android Open Source Project (AOSP) user-based
- Android device administrator
- App protection policies (APP)
- App configuration policies (ACP) for managed apps

For enrolled devices on unsupported OS versions (Android 9 and lower)

- Intune technical support isn't provided.
- Intune won't make changes to address bugs or issues.
- New and existing features aren't guaranteed to work.

While Intune doesn't prevent enrollment or management of devices on unsupported Android OS versions, functionality isn't guaranteed, and use isn't recommended.

Userless methods of Android device management (Dedicated and AOSP userless) and Microsoft Teams certified Android devices aren't affected by this change.

#### Collection of additional device inventory details<!-- 29460196 -->

Intune now collects additional files and registry keys to assist in troubleshooting the [Device Hardware Inventory](../remote-actions/collect-diagnostics.md) feature.

Applies to:

- Windows

## Week of October 7, 2024

### App management

#### New UI for Intune Company Portal app for Windows<!-- 27219294 -->

The UI for the Intune Company Portal app for Windows is updated. Users now see an improved experience for their desktop app without changing the functionality they've used in the past. Specific UI improvements are focused on the **Home**, **Devices**, and **Downloads & updates** pages. The new design is more intuitive and highlights areas where users need to take action.

For more information, see [New look for Intune Company Portal app for Windows](https://techcommunity.microsoft.com/t5/intune-customer-success/new-look-for-intune-company-portal-app-for-windows/ba-p/4158755). For end user details, see [Install and share apps on your device](../user-help/install-apps-cpapp-windows.md).

### Device security

#### New strong mapping requirements for SCEP certificates authenticating with KDC<!-- 29005591 -->

The Key Distribution Center (KDC) requires user or device objects to be strongly mapped to Active Directory for certificate-based authentication. This means that a Simple Certificate Enrollment Protocol (SCEP) certificate's subject alternative name (SAN) must have a security identifier (SID) extension that maps to the user or device SID in Active Directory. The mapping requirement protects against certificate spoofing and ensures that certificate-based authentication against the KDC continues working.

To meet requirements, modify or create a SCEP certificate profile in Microsoft Intune. Then add a `URI` attribute and the `OnPremisesSecurityIdentifier` variable to the SAN. After you do that, Microsoft Intune appends a tag with the SID extension to the SAN and issues new certificates to targeted users and devices. If the user or device has a SID on premises that's synced to Microsoft Entra ID, the certificate shows the SID. If they don't have a SID, a new certificate is issued without the SID.

For more information and steps, see [Update certificate connector: Strong mapping requirements for KB5014754](../protect/certificates-profile-scep.md).

Applies to:

- Windows 10/11, iOS/iPadOS, and macOS user certificates
- Windows 10/11 device certificates

This requirement isn't applicable to device certificates used with Microsoft Entra joined users or devices, because the SID attribute is an on-premises identifier.

#### Defender for Endpoint security settings support in government cloud environments (public preview)<!-- 24191406 -->

In public preview, customer tenants in US Government Community (GCC) High, and Department of Defense (DoD) environments can now use Intune to manage the Defender security settings on the devices that onboarded to Defender without enrolling those devices with Intune. This capability is known as [Defender for Endpoint security settings management](../protect/mde-security-integration.md).

For more information about the Intune features supported in GCC High and DoD environments, see [Intune US Government service description](../fundamentals/intune-govt-service-description.md).

## Week of September 30, 2024

### Device security

#### Updates to PKCS certificate issuance process in Microsoft Intune Certificate Connector, version 6.2406.0.1001 <!-- 24186560 -->

We updated the process for Public Key Cryptography Standards (PKCS) certificate issuance in Microsoft Intune to support the security identifiers (SID) information requirements described in [KB5014754](https://support.microsoft.com/topic/kb5014754-certificate-based-authentication-changes-on-windows-domain-controllers-ad2c23b0-15d8-4340-a468-4d4f3b188f16). As part of this update, an OID attribute containing the user or device SID is added to the certificate. This change is available with the Certificate Connector for Microsoft Intune, version 6.2406.0.1001, and applies to users and devices synced from Active Directory on-premises to Microsoft Entra ID.

The SID update is available for user certificates across all platforms, and for device certificates specifically on Microsoft Entra hybrid joined Windows devices.

For more information, see:

- [What's new for the certificate connector](../protect/certificate-connector-overview.md#september-19-2024)

- [Apply PFX changes to certificate](../protect/certificates-pfx-configure.md)

## What's new archive
<!-- Past announcements that are older than six months will be moved to the archive -->

For previous months, see the [What's new archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
