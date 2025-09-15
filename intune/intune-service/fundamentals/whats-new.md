---
# required metadata
title: What's new in Microsoft Intune
titleSuffix:
description: Find out what's new in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: laurawi
ms.date: 09/10/2025
ms.topic: whats-new
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: intuner
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
> Each [monthly update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) can take up to three days to roll out and is in the following order:
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

## Week of September 15, 2025

### Device management

#### Intune supports iOS/iPadOS 17.x as the minimum version<!--33405397-->

Apple released iOS 26 and iPadOS 26. With this release, Microsoft Intune—including the Intune Company Portal and app protection policies (APP, also known as MAM)—now requires iOS/iPadOS 17 or later.

For more information on this change, go to [Plan for change: Intune is moving to support iOS/iPadOS 17 and later](#plan-for-change-intune-is-moving-to-support-iosipados-17-and-later).

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, go to [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

> [!div class="checklist"]
> Applies to:
> - iOS/iPadOS

#### Intune supports macOS 14.x as the minimum version<!--33412147 -->

Apple released macOS 26 (Tahoe). With this release, Microsoft Intune, the Company Portal app, and the Intune MDM agent now require macOS 14 (Sonoma) or later.

For more information on this change, go to [Plan for change:  Intune is moving to support macOS 14 and later](#plan-for-change-intune-is-moving-to-support-macos-14-and-higher-later-this-year).

> [!NOTE]
> macOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, go to [Support statement](https://aka.ms/Intune/macOS/ADE-DE-support).

For a list of supported OS version, see [Supported operating systems and browsers in Intune](supported-devices-browsers.md).

> [!div class="checklist"]
> Applies to:
>
> - macOS

### Device security

#### Company Portal supports Purebred's new derived credentials experience<!--31973776-->

Apple has released iOS 26 and iPadOS 26. With this update, Purebred (version 3) introduces a new and improved derived credentials experience. As part of day zero support, Company Portal will support Purebred's updated workflow.

- If your organization plans to continue using the older version of Purebred, there will be no changes to your derived credentials experience in Purebred or Company Portal—even if you upgrade to the latest version of Company Portal.
- If your organization plans to upgrade to the new version of Purebred, make sure to update to Company Portal version 5.2509.0 to ensure compatibility.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

## Week of September 8, 2025

### Device security

#### JavaScript WebSockets support with Microsoft Tunnel for Mobile Application Management for iOS <!-- 28660712 wndraft    -->

Microsoft Tunnel for Mobile Application Management (MAM) for iOS now supports JavaScript WebSockets from web views. This support helps improve communications for apps that require real-time communications that rely on WebSockets.

While JavaScript WebSockets are now supported, Tunnel for MAM iOS does not support native WebSocket APIs or apps that rely on them.

For more information, see [Microsoft Tunnel for Mobile Application Management for iOS/iPadOS admin guide](../protect/microsoft-tunnel-mam-ios.md).

## Week of September 1, 2025

### Device management

#### Enrollment Status Page support for installing Windows security updates during Windows OOBE <!-- 7183120 -->

> [!IMPORTANT]
>
> As of September 9, 2025, this capability is delayed to help ensure delivery of the best possible experience. The new setting on the Enrollment Status Page (ESP) can be configured on both new and existing ESP profiles, but the automatic installation of monthly security update releases and the new user interface isn't available yet. This post will be updated with a revised timeline as soon as it's available.

The Windows out-of-box experience (OOBE) by default installs the latest available security updates to help ensure devices are secure and up to date from day one. Windows OOBE is used by Intune and by Windows Autopilot scenarios through the Intune enrollment status page (ESP) configurations. Intune refers to these security updates Windows quality updates.

To help you manage this behavior, we've updated the Intune enrollment status page with a new setting you can use to allow or block the automatic installation of these updates.

The new setting is **Install Windows quality updates**. These security updates, also known as Windows quality updates in Intune, are installed by default during the Windows out-of-box experience OOBE that's used by Intune and by Windows Autopilot.

By default, this setting is set to *Yes* in all new ESP profiles you create, which results in the most recent security updates being installed. In all your previously created ESP profiles this setting is set to *No* until you choose to edit those profiles to change it. When set to *No*, OOBE doesn't install the updates which can give your internal teams time to test the updates before allowing them to install on new devices you provision.

For more information about the Intune enrollment status page, see [Set up Enrollment Status Page](/intune/intune-service/enrollment/windows-enrollment-status). For information about Windows quality updates, see [Windows quality update policy](/intune/intune-service/protect/windows-quality-update-policy).

Applies to:
- Windows

### Device security

### Device configuration recommendations from the Security Copilot Vulnerability Remediation Intune agent<!-- 34346149 -->

To help reduce your organization's attack surface against vulnerabilities, the Security Copilot Vulnerability Remediation Intune agent now provides recommended configurations for settings related to a reported vulnerability.

You can find the recommended configurations after selecting *Agent suggestions* for a reported vulnerability, which opens the *Suggested action* pane.  On the suggested action pane there is a new section of information titled **Configurations**.

If the Intune settings catalog contains relevant settings for the reported vulnerability, the Configurations section provides information to help you configure device policies. These policies can help minimize future risk from that vulnerability. This includes:

- A list of the settings that are relevant to the current vulnerability, which can be deployed through an Intune settings catalog policy. Only the specific settings that are relevant to the vulnerability are listed.
- Each setting is presented with a recommended configuration.
- Selecting the citation icon next to a setting displays that settings description. The description can also include a link to content for the Configuration Service Provider (CSP) that the setting represents.

If there are no recommended device configuration settings to deploy, the Configurations section will indicate that no recommended settings catalog policy configurations are available.

To learn more about Agent suggestions, remediation guidance, and the new recommended configurations, see [Agent suggestions](../protect/vulnerability-remediation-agent.md#agent-suggestions) in Vulnerability Remediation Agent for Security Copilot in Microsoft Intune.

## Week of August 25, 2025

### App management

#### Offline Mode and App access without sign in for Android Enterprise Dedicated Devices on Managed Home Screen<!-- 30303710, 25476290  -->

Managed Home Screen (MHS) for Android Enterprise dedicated devices now supports two new features: **Offline mode** and **App access without sign in**.

- **Offline mode** – Lets users access designated apps when the device is offline or unable to connect to the network. You can configure a grace period before requiring users to sign in once connectivity is restored.
- **App access without sign in** – Lets users launch specific apps from the MHS sign-in screen via the MHS top bar, regardless of network status. This is useful for apps that need to be available immediately, such as help desk or emergency tools.

These features are designed for dedicated devices enrolled in Microsoft Entra shared device mode and can be configured via device configuration policy.

**Applies to**:
- Android Enterprise dedicated devices

## Week of August 18, 2025 (Service release 2508)

### App management

#### Android app configuration policies support new variable values<!-- 32843208 -->

Android Enterprise app configuration policies in Intune now support more variable values. The new values include account name, device name, employee ID, MEID, serial number, and the last four digits of the serial number.

For more information, see [Supported variables for configuration values](../apps/app-configuration-policies-use-android.md#supported-variables-for-configuration-values).

**Applies to**:
- Android Enterprise

### Device configuration

#### Managed Installer support for user and device groups <!-- 30293237 -->

We've updated our Managed Installer policy to add the capability to target individual groups of users and devices, using one or more individual policies. Until now, a Managed Installer policy was a tenant-wide configuration that applied to all Windows devices. With this update, separate policies can now be assigned to different device groups providing you with more flexibility.

If you previously had a tenant-wide managed installer policy in effect, that policy remains available with a group assignment to all your devices. This reconfiguration is equivalent to the previous tenant-wide configuration it had before. You can choose to use that converted policy or implement new policies with more granular control.

For more information about configuring and using managed installers, see [Get started with managed installers](../protect/endpoint-security-app-control-policy.md#get-started-with-managed-installers).

Applies to:
- Windows

#### New Windows settings in the settings catalog <!-- 34345586 34545262-->

The Intune [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure, and all in one place. There are new settings in the Windows settings catalog (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type).

**Microsoft Edge Administrative Templates policy updates**:

- **v138** - Intune supports the following new ADMX-backed policies:

  | Setting | CSP |
  | --- | --- |
  | **Microsoft Edge** > **Allow pages to use the built-in AI APIs** | BuiltInAIAPIsEnabled |
  | **Microsoft Edge** > **Control access to AI-enhanced search in History** | EdgeHistoryAISearchEnabled |
  | **Microsoft Edge - Default Settings (users can override)\ Identity and sign-in** > **Use Primary Work Profile as default to open external links** | EdgeOpenExternalLinksWithPrimaryWorkProfileEnabled |
  | **Microsoft Edge** > **Allow SpeculationRules prefetch for ServiceWorker-controlled URLs** | PrefetchWithServiceWorkerEnabled |
  | **Microsoft Edge** > **Control whether TLS 1.3 Early Data is enabled in Microsoft Edge** | TLS13EarlyDataEnabled |
  | **Microsoft Edge** > **Allow pages to use the built-in AI APIs** | BuiltInAIAPIsEnabled |
  | **Microsoft Edge** > **Allow SpeculationRules prefetch for ServiceWorker-controlled URLs** | PrefetchWithServiceWorkerEnabled |

  The following legacy settings are deprecated, and should not be used:

  | Setting | CSP |
  | --- | --- |
  | **Microsoft Edge\ Private Network Request Settings** | InsecurePrivateNetworkRequestsAllowed |
  | **Microsoft Edge Network Settings** > **Enable zstd content encoding support** | ZstdContentEncodingEnabled |
  | **Microsoft Edge Network Settings** > **Specifies whether to block requests from public websites to devices on a user's local network** (deprecated) | LocalNetworkAccessRestrictionsEnabled |

- **v139** - Intune supports the following new ADMX-backed policies for Microsoft Edge:

  | Setting | CSP |
  | --- | --- |
  | **Microsoft Edge** > **Identity and sign-in** > **Prioritize app-specified profile to open external links** | EdgeOpenExternalLinksWithAppSpecifiedProfile |
  | **Microsoft Edge** > **Extensions** > **Specify extensions users must allow in order to navigate using InPrivate mode** | MandatoryExtensionsForIncognitoNavigation |
  | **Microsoft Edge** > **Control whether Microsoft 365 Copilot Chat shows in the Microsoft Edge for Business toolbar** | Microsoft365CopilotChatIconEnabled |
  | **Microsoft Edge** > **Configuration policy for Microsoft Edge for Business Reporting Connectors** | OnSecurityEventEnterpriseConnector |
  | **Microsoft Edge** > **Allow software WebGL fallback using SwiftShader** | EnableUnsafeSwiftShader |

  The following legacy settings are deprecated, and should not be used:

  | Setting | CSP |
  | --- | --- |
  | **Microsoft Edge** > **Controls whether the new HTML parser behavior for the `<select>` element is enabled** | SelectParserRelaxationEnabled |
  | **Microsoft Edge** > **Enable keyboard focusable scrollers** | KeyboardFocusableScrollersEnabled |

- Some existing policies have string updates that reflect the latest browser behavior and terminology.

**OneDrive**:

-  **Disable a toast and activity center message to encourage a user to sign in OneDrive using an existing credential that is made available to Microsoft applications** - This setting allows IT admins to prevent detection of new accounts in OneDrive, helping enforce organizational sync and access controls.

**Administrative Templates\Windows Components\Sync your settings**:

- **Enable Windows Backup** - This setting allows IT admins to manage syncing behavior for Windows Backup features. Specifically, this policy controls whether language preferences are included in backup sync, which helps organizations tailor backup configurations to their needs.

Applies to:

- Windows

#### New day zero settings available in the Apple settings catalog<!-- 33437616 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Declarative Device Management (DDM) > Audio Accessory Settings**:

- Temporary Pairing Disabled
- Temporary Pairing Unpairing Time
- Unpairing Policy
- Unpairing Hour

**Declarative Device Management (DDM) > Safari Settings**:

- Accept Cookies
- Allow Disabling Fraud Warning
- Allow History Clearing
- Allow JavaScript
- Allow Private Browsing
- Allow Popups
- Allow Summary
- Page Type
- Homepage URL
- Extension Identifier

**Restrictions**:

- Allow Safari History Clearing
- Allow Safari Private Browsing
- Denied ICCIDs For iMessage And FaceTime
- Denied ICCIDs For RCS

##### macOS

**Authentication > Extensible Single Sign On Kerberos**:

- Allow Platform SSO Auth Fallback

**Declarative Device Management (DDM) > Safari Settings**:

- Allow History Clearing
- Allow Private Browsing
- Allow Summary
- Page Type
- Homepage URL
- Extension Identifier

**Restrictions**:

- Allow Safari History Clearing
- Allow Safari Private Browsing

#### New setting in the Android settings catalog<!-- 32864836 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There's a new **Hide organization name** setting (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type). When set to **True**, the enterprise name isn't shown on the device, such as lock screen.

For a list of existing settings you can configure in the settings catalog, see [Android Enterprise device settings list in the Intune settings catalog](../configuration/settings-catalog-android.md).

Applies to:

- Android Enterprise corporate-owned devices with a work profile (COPE)
- Android Enterprise corporate owned fully managed (COBO)

### Device enrollment

#### Intune supports Ubuntu 22.04 and later<!-- 32756619 -->

Microsoft Intune and the Microsoft Intune app for Linux now support Ubuntu 22.04 LTS and Ubuntu 24.04 LTS, and has ended support for Ubuntu 20.04 LTS. Devices that are currently enrolled on Ubuntu 20.04 LTS remain enrolled even though the version is no longer supported. New devices are unable to enroll if they're running Ubuntu 20.04 LTS. To see what devices or users might be affected, check your Intune reporting. In the admin center, go to **Devices **> **All devices** and filter OS by Linux. You can add more columns to help identify who in your organization has devices running Ubuntu 20.04 LTS. Notify your users to upgrade their devices to a supported Ubuntu version.

For more information about Linux enrollment, see [Linux device enrollment guide for Microsoft Intune](deployment-guide-enrollment-linux.md).


### Device management

#### Wipe remote action supports multiple administrative approval (MAA)<!-- 27043113 -->

When you use the multiple administrative approval (MAA) feature, you require a second admin account to approve a change before the change is applied.

The **[Wipe](../remote-actions/devices-wipe.md)** remote action supports MAA. Use MAA with the **Wipe** action to help mitigate the risk of unauthorized or compromised remote actions by a single admin account.

For more information on multiple administrative approval, see [Use multiple administrative approvals in Intune](../fundamentals/multi-admin-approval.md).

#### Configure Windows Backup for Organizations (public preview)<!-- 33829628 -->

Intune administrators can configure a new feature in public preview called Windows Backup for Organizations. With this feature, you can back up your organization's Windows 10 or Windows 11 settings and restore them on a Microsoft Entra joined device. Backup settings are configurable in the Microsoft Intune admin center settings catalog, while a tenant-wide setting that lets you restore a device is available in the admin center under **Enrollment**. The backup setting is available now in public preview, while the restore setting will be available for public preview beginning August 26th.

For more information about this feature, see [Windows Backup for Organizations in Microsoft Intune](../enrollment/windows-backup-restore.md).

#### New resolution button improves compliance remediation experience<!-- 31370959 -->

We improved the Just in Time (JIT) compliance remediation experience for device users in Microsoft Intune. Intune has collaborated with Microsoft Defender to:

- Remove user clicks required to view and learn remediation steps.
- Add a **Resolve** button to reduce time-to-remediation.

When a user opens a productivity app and sees they are marked noncompliant due to Microsoft Defender, the user can now select **Resolve.** This action redirects them to Microsoft Defender, where Microsoft Defender takes steps to remediate the user and then redirect the user back to their productivity app.

Even if you aren't using Microsoft Defender, if you have Conditional Access turned on your users can have an improved experience.  With JIT compliance remediation, users go through an embedded flow that shows them their compliance status, noncompliance reasoning, and a list of actions right within a productivity app. This flow eliminates extra steps, the need to switch between apps, and reduces the number of authentications.

As an admin, if you have JIT registration and compliance remediation set up already, you have no action items. If you don't, set it up today to support this new functionality. For more information, see:

- [Set up just-in-time registration](../enrollment/set-up-just-in-time-registration.md).
- [Update iOS device settings](../user-help/how-do-i-find-the-serial-number-on-my-device-ios.md).

### Intune apps

#### Newly available protected apps for Intune<!-- 33434077, 33434100, 33434308, 33434387, 33434700, 33573103, 33573273-->

The following protected apps are now available for Microsoft Intune:

- Avenza Maps for Intune by Avenza Systems Inc.
- Datasite for Intune by Datasite (Android)
- Dialpad by Dialpad, Inc.
- Dialpad Meetings by Dialpad, Inc.
- Omega 365 by Omega 365 Core AS
- Symphony Messaging Intune by Symphony Communication Services, LLC
- Zoho Projects - Intune by Zoho Corporation (Android)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Declarative software update reports for Apple devices<!-- 25207078, 31557946 -->

You can now use several new [software update reports for Apple devices](../protect/software-updates-ios.md) that are powered by Apples built-in declarative reporting infrastructure. The declarative reporting infrastructure provides Intune with a near real-time view of the software update status of managed devices. The following Apple software update reports are now available:

- A *per-device software update report* - Per-device software update reports are available in the Intune Admin center by going to *Devices* and then selecting an applicable device. In the Devices Overview pane for that device, below Monitor, you'll find the report listed as **iOS software updates** for iOS or iPadOS devices, and as **macOS software updates** for macOS devices.

  With these per-device reports available, the previously available macOS per-device **Software updates** report is now deprecated. While the deprecated report remains available in the admin center and can still be used while viewing a device, the report will be removed from Intune with a future update.

- **Apple software update failures** - With this operational report, you can view details across your entire managed Apple device fleet. Details include why the update failed to install and the timestamp of the last failure. To find this report, in the admin center go to *Devices* > *Monitor*, and then select the report's name to view the report details.

- **Apple software update report** - This is an organizational report that displays details about pending and current software update information across your entire managed Apple device fleet. To find this report, in the admin center go to *Reports* > *Device management* > *Apple updates*, select the *Reports* tab, and then select the report tile.

- **Apple software update summary report** - View the Apple software update summary report, in the admin center go to *Reports* > *Device management* > *Apple updates*, and then select the *Summary* tab. Here you'll see a roll-up of update status from macOS, iOS, and iPadOS devices. This includes the version of the latest update that is available for each platform, and the date that update became available.

The following Apple devices support these new reports:
- iOS 17 and later
- iPadOS 17 and later
- macOS 14 and later

For more information about the changes behind these reports, see [Support tip: Move to declarative device management for Apple software updates](https://techcommunity.microsoft.com/blog/IntuneCustomerSuccess/support-tip-move-to-declarative-device-management-for-apple-software-updates/4432177).

### Role-based access control

#### Multi-administrator approval support for role-based access control<!-- 26838684 -->

Multi-administrator approval (MAA) now supports role-based access control. When enabled, any changes to roles, including modifications to role permissions, admin groups, or member group assignments, require a second administrator to approve the change before it's applied. This dual authorization process helps protect your organization from unauthorized or accidental role-based access control changes.

For more information, see [Role-based access control in Microsoft Intune](../fundamentals/role-based-access-control.md).

## Week of August 11, 2025

### Device management

#### Platform SSO is generally available (GA) and also supports custom TGT<!-- 33990050 -->

Platform SSO is a feature in Microsoft Entra that enables single sign-on (SSO) using a Microsoft Entra ID on macOS devices. Using the Intune settings catalog, you can configure Platform SSO and use Intune to deploy the Platform SSO configuration to your macOS devices.

- Microsoft Entra announced that Platform SSO for macOS devices is generally available (GA). For more information on this Microsoft Entra feature, see [Microsoft Enterprise SSO plug-in for Apple devices](/entra/identity-platform/apple-sso-plugin).
- Microsoft Entra supports Kerberos Ticket Granting Tickets (TGTs) to access on-premises Active Directory and Microsoft Entra ID using [Apple's Kerberos SSO extension](https://support.apple.com/guide/deployment/depe6a1cda64/web).

  On the Company Portal version 5.2508.0 and newer, you can use the Intune settings catalog Platform SSO policy to enable Kerberos SSO to on-premises and cloud resources using the TGTs.

To configure Platform SSO in Intune, see:

- [Configure Platform SSO for macOS devices in Intune](../configuration/platform-sso-macos.md)
- [Common Platform SSO scenarios for macOS devices in Intune](../configuration/platform-sso-scenarios.md)

Applies to:

- macOS

### Device security

#### Update required for Microsoft Tunnel endpoints<!-- 32817331 -->

As part of our ongoing improvements to the Microsoft Tunnel infrastructure, we introduced new endpoints with the [March 19, 2025 release](../protect/microsoft-tunnel-upgrade.md#march-19-2025). You must upgrade your Microsoft Tunnel to the March 19, 2025 release version or later to ensure you're using the new endpoints. Once you upgrade to this version or later, you can't downgrade to an earlier version. Earlier releases that rely on legacy endpoints aren't supported and might cause service disruptions. To continue with uninterrupted service, we recommend upgrading to the latest supported build and avoiding rollback to unsupported versions.

## Week of July 28, 2025

### Device management

#### New Microsoft Graph permissions for API calls to device management endpoints<!-- 20952394 -->

Calls to several Microsoft Graph APIs now require one of two newer *DeviceManagement* permissions that replace the use of previously supported permissions. The following are the two new permissions and the original permissions that the new permissions replace:
- **DeviceManagementScripts.Read.All** - This new permission replaces use of *DeviceManagementConfiguration.Read.All*
- **DeviceManagementScripts.ReadWrite.All** - This new permission replaces use of the *DeviceManagementConfiguration.ReadWrite.All*

Access to the following Microsoft Graph API calls now require using the new permissions:

- ~/deviceManagement/deviceShellScripts
- ~/deviceManagement/deviceHealthScripts
- ~/deviceManagement/deviceComplianceScripts
- ~/deviceManagement/deviceCustomAttributeShellScripts
- ~/deviceManagement/deviceManagementScripts 

Currently both the *DeviceManagementScripts* and the older *DeviceManagementConfiguration* permissions remain functional. However, in early September 2025, tools and scripts that rely on the older permissions to access the listed APIs fail to function.

For more information, see [How to use Microsoft Entra ID to access the Intune APIs in Microsoft Graph](../developer/Intune-graph-apis.md).

## Week of July 21, 2025 (Service release 2507)

### Microsoft Intune Suite

#### Endpoint Privilege Management support for wildcards in elevation rules<!-- 30290730 -->

You can now use wildcards in the file name and file path of elevation rules you define for Endpoint Privilege Management (EPM). Wildcards allow for more flexible rule creation with broader matching capabilities, enabling file elevations for trusted files that have names that might change with subsequent revisions.

For file names, use of wildcards is supported only in the file name and not for the file extension. You can use a question mark `?` to replace a single character at any point in the file name and an asterisk `*` to replace a string of characters at the end of the file name.

The following are a few examples of wildcard use for a Visual Studio setup file called `VSCodeUserSetup-arm64-1.99.2.exe` found in `C:\Users\<username>\Downloads\`:

- File name:
  - `VSCodeUserSetup*.exe`
  - `VSCodeUserSetup-arm64-*.exe`
  - `VSCodeUserSetup-?????-1.??.?.exe`

- File path:
  - `C:\Users\*\Downloads\`

For more information, see [Use variables in elevation rules](../protect/epm-elevation-rules.md#use-variables-in-elevation-rules) in Configure policies for Endpoint Privilege Management.

### App management

#### Newly available OEMConfig apps in Intune <!-- 5306739 -->

The following OEMConfig app is now available in Intune for Android Enterprise:

- RugGear

For more information about OEMConfig, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

### Device configuration

#### New settings available in the Apple settings catalog <!-- 33064192 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Cellular Private Network**:

- Cellular Data Preferred
- CSG Network Identifier
- Data Set Name
- Enable NR Standalone
- Geofences
- Network Identifier
- Version Number

##### macOS

**Microsoft Edge**:

- The Microsoft Edge category is updated with new settings. Learn more about available macOS settings for Microsoft Edge at [Microsoft Edge - Policies](/deployedge/microsoft-edge-policies).

### Device management

#### Platform support for Device Cleanup rules<!-- 13835920 -->

Using [cleanup rules](../remote-actions/devices-wipe.md#automatically-hide-devices-with-cleanup-rules), you can configure Intune to automatically clean up devices that appear to be inactive, stale, or unresponsive.

With this feature, you can:

- Configure individual device cleanup rules per platform, like Windows, iOS/iPadOS, macOS, and Android.
- Use the [Audit logs](monitor-audit-logs.md) to see the devices that the device cleanup rules conceal from the Intune reports.
- Use [role-based access control (RBAC)](role-based-access-control.md) to customize the user roles that can create device cleanup rules.

For more information, see [device cleanup rules](../remote-actions/devices-wipe.md#automatically-hide-devices-with-cleanup-rules).

### Device security

#### macOS support for local administrator account configuration with  (password solution) - GA <!-- 25385731 -->

macOS automated device enrollment (ADE) profiles can configure newly enrolled macOS devices that run macOS 12 or later with both a local administrator and local user account, along with support for the Microsoft Local Admin Password Solution (LAPS).

With this support:
- You can use macOS automated device enrollment (ADE) profiles to configure the local administrator and user accounts for a device. When configured, this capability applies to all new macOS device enrollments and device re-enrollments assigned to that enrollment profile.
- Intune creates a randomized, unique, and secure password for the device's admin account. It's 15 alphanumeric characters.
- Intune automatically rotates the password every six months by default.
- Previously enrolled devices aren't affected unless they re-enroll with Intune through an applicable ADE profile.

For account creation, the profile supports the following variables:

- **Admin account username**:
  - {{serialNumber}} - for example, F4KN99ZUG5V2
  - {{partialupn}} - for example, John.Dupont
  - {{managedDeviceName}} - for example, F2AL10ZUG4W2_14_4/15/2025_12:45PM
  - {{onPremisesSamAccountName}} - for example, JDoe

- **Admin account full name**:
  - {{username}} - for example, John@contoso.com
  - {{serialNumber}} - for example, F4KN99ZUG5V2
  - {{onPremisesSamAccountName}} - for example, JDoe

To support LAPS:
- There are two new role-based access control permissions for *Enrollment program* that can grant an administrative account permission to view a managed devices password, and to rotate that password.
- By default, these permissions aren't part of any built-in Intune RBAC role, and must be explicitly assigned to admins through custom roles.

To learn about all the details for this new capability, see [Configure support for macOS ADE local account configuration with LAPS in Microsoft Intune](../enrollment/macos-laps.md).

### Intune apps

#### Newly available protected apps for Intune<!-- 33015811, 33016789 -->

The following protected apps are now available for Microsoft Intune:

- Vault CRM by Veeva Systems Inc. (iOS)
- Workvivo by Workvivo

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of July 14, 2025

### Device management

#### Experience Microsoft Copilot in Intune<!-- 29339619, 31192897 -->

You can now use Microsoft Copilot in Intune to explore your Intune data using natural language, take action on the results, manage policies and settings, understand your security posture, troubleshoot device issues, and view insights about enrolled Surface devices.

- **Explore your Intune data** - Use natural language to explore your Intune data and take action based on the results. Admins can run queries against Intune resource data, including questions about devices, apps, policies, updates, and compliance. When a query runs, a Copilot summary helps you understand the results and offers suggestions. You can add devices or users from the query results to a group to target apps and policies. There are also example queries that you can filter to find an example that best matches your request or use to help you create your own request.

  Data coverage, querying capabilities, and actionability will evolve over time as we make improvements to how you explore your data.

  To learn more about this feature, see [Explore Intune data with natural language and take action](../copilot/copilot-intune-explorer.md).

- **Conversational chat experience** - Use the Copilot in Intune chat experience to interact with your data using natural language to manage tasks, get insights, and troubleshoot issues. Here's what you can do with the chat experience:

  - Policy and setting management: Use Copilot in Intune to summarize an existing policy or learn more about individual policy settings and recommended values.
  - Device details and troubleshooting: Use Copilot in Intune to get device details and troubleshoot a device to get device-specific information like the installed apps, group memberships and more.
  - Device Query: Use Copilot in Intune to help you create Kusto Query Language (KQL) queries to run when using device query in Intune.
  - Endpoint Privilege Management (EPM): Use Copilot in Intune to help identify potential elevation risks from within the EPM support approved workflow.

- **Microsoft Copilot in Surface Management Portal** - Microsoft Copilot in Intune includes the Surface Management Portal, a workspace in the Intune admin center that brings together vital data and insights about enrolled Surface devices, all in one place.

  - Gain insights into device compliance, support activity, applicable warranty or protection plan coverage, and carbon emission estimates.
  - Monitor the status of each device, including applicable warranty or protection plan expirations and active support requests.
  - Centralize Surface-specific device administration in a single environment.
  - Automatically access comprehensive information from your Intune-enrolled Surface devices, which flows into the Surface Management Portal when users sign in for the first time.

  To learn more about this feature, see [Security Copilot in Microsoft Surface Management Portal](../copilot/security-copilot-surface-portal.md).

### Monitor and troubleshoot

#### Export device query results to CSV file <!-- 27967896 -->

Now after running a multiple-device query, you can export up to 50,000 query results to a CSV file. For more information, see [How to use device query for multiple devices](../../analytics/device-query-multiple-devices.md#how-to-use-device-query-for-multiple-devices).

## Week of June 23, 2025 (Service release 2506)

### App management

#### Microsoft Intune support for Apple AI features<!-- 12792722, 30550110, 30220799 -->

Intune app protection policies have new standalone settings for Apple AI features (Genmojis, Writing tools, and screen capture). Apps running the following Intune App SDK and App Wrapping Tool versions support the standalone settings:

- Xcode 15 version 19.7.12 or later
- Xcode 16 version 20.4.0 or later

Previously, these Apple AI features were blocked when the app protection policy **Send Org data to other apps** setting is configured to a value other than **All apps**.

For more information about Intune's related app protection policies, see [iOS app protection policy settings](../apps/app-protection-policy-settings-ios.md).

#### Add Enterprise App Catalog apps to ESP blocking apps list<!-- 29846319 -->

Windows Autopilot now supports Enterprise App Catalog apps. Microsoft Intune Enterprise App Management enables IT admins to easily manage applications from the Enterprise App Catalog. Using Windows Autopilot, you can select apps from the Enterprise App Catalog as blocking apps in the Enrollment Status Page (ESP) and the Device Preparation Page (DPP) profiles. This feature allows you to ensure those apps are delivered before the user can access the desktop.

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

- The Microsoft Edge category has hundreds of new settings. Learn more about available macOS Edge settings at [Microsoft Edge - Policies](/deployedge/microsoft-edge-policies).

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

#### New reporting system for improved performance and data consistency <!-- 31823383, 33812267 -->

Microsoft Intune is rolling out the new Policy Reporting Service (PRS) V3. The new system brings faster report generation, improved reliability, and better data consistency.

In the first phase, some high-traffic compliance and device configuration reports are transitioning to the new system.

Users notice quicker updates in the Intune admin center and fewer issues with stale data. No action is required from users, as your reports transition automatically.

With (PRS) V3, device reports only update when a device checks in. This behavior is an intentional change from previous versions.

If a policy is removed but the device hasn't checked in, the report continues to show the last known status. The policy is removed during the next check-in, at which point the report is updated. This behavior improves accuracy but can differ from what customers experienced with (PRS) V1.

To learn more about the Intune reports you can use, see [Intune reports](reports.md).

### Device security

#### New attributes and S/MIME baseline requirements for SCEP certificate profiles <!-- 33116047 -->

Intune supports two new attributes for subject name settings in SCEP and PKCS device configuration profiles. They include:

- G={{GivenName}}
- SN={{SurName}}

Beginning July 16, if you're using a third party public certificate authority (CA) integrated with the Intune SCEP API for issuing S\MIME (encryption or signing) certificates anchored up to a public root CA, then you  must use these attributes in the subject name format. After that date, a public CA will not issue or sign S\MIME certificates that omit these attributes.

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

When adding a Win32 app to Intune, you can select an option to check and install the app on Windows devices running ARM64 operating systems. This capability is available from the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **All apps** > **Create**. The ARM64 option is available by selecting the **Operating system architecture** option under the **Requirements** step. To ensure that you don't have any impact to any Win32 applications that you previously targeted to 64-bit devices, your existing 64-bit Win32 applications also have ARM64 selected. After the availability of being able to specifically target ARM64 operating system architectures, selecting x64 won't target ARM64 devices.

For related information, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

Applies to:

- Windows devices

## Week of June 2, 2025

### Device security

#### Vulnerability Remediation Agent for Intune (public preview)<!-- 33475311 -->

The Vulnerability Remediation Agent is currently in a limited public preview and available to only a select group of customers. If you're interested in gaining access or would like to learn more, please reach out to your sales team for further details and next steps.

When run, this agent uses data from Microsoft Defender Vulnerability Management to identify and then provide remediation guidance for vulnerabilities on your managed devices. You run and access the agent and view its results from within the Intune admin center where you see suggestions prioritized by the agent for remediation. Each suggestion includes key information like associated CVEs, severity, exploitability, affected systems, organizational exposure, business impact, and remediation guidance.

This information empowers you with a current assessment of potential risk to your environment and guidance to help you decide which risk to address first.

For more information about this agent including prerequisites, see [Vulnerability Remediation Agent for Security Copilot in Microsoft Intune](../protect/vulnerability-remediation-agent.md).

## Week of May 26, 2025 (Service release 2505)

### Microsoft Intune Suite

#### Endpoint Privilege Management rules explicitly deny elevation<!-- 30225542 -->

Endpoint Privilege Management (EPM) elevation rules now include a new file elevation type of **Deny**. An EPM elevation rule set to *Deny* blocks the specified file from running in an elevated context. We recommend using file elevation rules to allow users to elevate specific files. But, a deny rule can help you ensure that certain files like known and potentially malicious software can't be run in an elevated context.

*Deny* rules support the same configuration options as other [elevation types](../protect/epm-elevation-rules.md#creating-elevation-rules-with-endpoint-privilege-management) except for child processes, which aren't used.

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

You can use DFCI profiles to manage UEFI (BIOS) settings for NEC devices that run Windows 10 or Windows 11. Not all NEC devices running Windows are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

You can manage DFCI profiles from within the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by going to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type. For more information about DFCI profiles, see:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](../../autopilot/dfci-management.md)

Applies to:

- Windows

### Device enrollment

#### Custom naming template for AOSP devices <!-- 31707864 -->

Use a custom template for naming AOSP user-affiliated and userless devices when they enroll with Intune. The template is available to configure in the enrollment profile. It can contain a combination of free text and predefined variables (like device serial number, device type), and for user-affiliated devices, the owner's username. For more information about how to configure the template, see:

- [Set up Intune enrollment for Android (AOSP) corporate-owned userless devices](../enrollment/android-aosp-corporate-owned-userless-enroll.md)
- [Set up Intune enrollment for Android (AOSP) corporate-owned user-associated devices](../enrollment/android-aosp-corporate-owned-user-associated-enroll.md)


#### Change to role-based access control for device enrollment limits<!-- 27115176 -->

We updated role-based access control (RBAC) for device limits. If you're currently assigned the [policy and profile manager](../fundamentals/role-based-access-control-reference.md#policy-and-profile-manager) role, or the *device configurations* permissions that are built-in to the role, you now have read-only access to device enrollment limit policies. To create and edit these policies, you must be an Intune Administrator.

### Device management

#### Cross Platform Device Inventory<!-- 25964936 -->

Android, iOS, and Mac devices are added to device inventory. Intune now collects a default set of inventory data including 74 Apple properties and 32 Android properties.

For more information, see [View device details with Microsoft Intune](../fundamentals/device-inventory.md).

#### Enhanced security during unattended Remote Help sessions on Android devices<!--25977108 -->

During an unattended Remote Help sessions on Android devices, the screen of the device is blocked and users are notified if they interact with it. This feature enhances the security and user awareness during remote assistance.

This feature is for Zebra and Samsung devices that enrolled as Android Enterprise corporate owned dedicated devices.

For more information on Remote Help, see [Remote Help](../fundamentals/remote-help-android.md).

### Device security

#### Detect rooted corporate-owned Android Enterprise devices<!--31672848 -->

Configure compliance policies to detect if a corporate-owned Android Enterprise device is rooted. If Microsoft Intune detects that a device is rooted, you can mark it as noncompliant. This feature is now available for devices enrolled as fully managed, dedicated, or corporate-owned with a work profile. For more information, see [Device compliance settings for Android Enterprise in Intune](../protect/compliance-policy-create-android-for-work.md).

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
App protection policies (APP) support Microsoft Edge (v136 or later), OneDrive (v16.8.4 or later), and Outlook (v4.2513.0 or later). To enable this setting for these specific apps on visionOS devices, you must set `com.microsoft.intune.mam.visionOSAllowiPadCompatApps` to `Enabled` in your app configuration policy. Once you assign your app configuration policy, you can create and assign your app protection policy for your VisionOS devices. For more information, see [Protect data on VisionOS devices](../apps/app-configuration-policies-managed-app.md#protect-data-on-visionos-devices).

### Tenant administration

#### New icon for Microsoft Intune<!-- 29148691 -->
Microsoft Intune has a new icon. The Intune icon is being updated across platforms and apps associated with Intune, such as the Intune admin center and Intune Company Portal app. The new icon will gradually be implemented over the next few months.

## Week of April 21, 2025 (Service release 2504)

### Microsoft Intune Suite

#### Endpoint Privilege Management elevation rule support for file arguments and parameters<!-- 28077130 -->

File elevation rules for Endpoint Privilege Management (EPM) now support [command line file arguments](../protect/epm-elevation-rules.md#use-file-arguments-for-elevation-rules). When an elevation rule is configured to define one or more file arguments, EPM allows that file to run in an elevated request only when one of the defined arguments is used. EPM blocks elevation of the file should a command line argument be used that isn't defined by the elevation rule. Use of file arguments in your file elevation rules can help you refine how and for what intent different files are successfully run in an elevated context by Endpoint Privilege Management.

EPM is available as an [Intune Suite add-on-capability](../fundamentals/intune-add-ons.md).

### App management

#### Relationship viewer available for Intune apps<!-- 17644546 -->

The relationship viewer provides a graphical depiction of the relationships between different applications in the system, including superseding and dependent applications. Admins can find relationship viewer in Intune by selecting **Apps** > **All apps** > *a Win32 app* > **Relationship viewer**. The relationship viewer supports both Win32 apps and Enterprise App Catalog apps. For more information, see [App relationship viewer](../apps/apps-win32-app-management.md#app-relationship-viewer).

#### Apple VPP using new API v2.0<!-- 29567109 -->

Apple recently updated the API for their volume purchase program (VPP), which is used to manage apps and books. Apple's related API is now version 2.0. Version 1.0 is deprecated. To support the Apple updates, Microsoft Intune uses the new API, which is faster and more scalable than the previous version.

Applies to:

- iOS/iPadOS
- macOS

#### More org data storage service options for Android and iOS apps<!-- 29606862 -->

Intune now provides more storage services options when saving copies of org data using an app protection policy for Android or iOS. In addition to the existing org data storage options, you can also select **iManage** and **Egnyte** as storage options. You must select these services as exemptions from your block list by setting **Save copies of org data** to **Block**, then selecting the allowed storage services next to the **Allow user to save copies to selected services** setting. This setting doesn't apply to all applications.

For more information about data protection using app protection policies, see [iOS app protection policy settings - Data protection](../apps/app-protection-policy-settings-ios.md#data-protection) and [Android app protection policy settings - Data protection](../apps/app-protection-policy-settings-android.md#data-protection).

Applies to:

- Android
- iOS

### Device configuration

#### Updated device configuration template for Windows Delivery Optimization<!-- 32411831 -->

The device configuration template for Windows [Delivery Optimization](../configuration/delivery-optimization-windows.md) is updated. The new template uses the settings format in the Settings Catalog. Settings are taken directly from the Windows Configuration Service Providers (CSPs) for Windows Delivery Optimization, as documented by Windows at [Policy CSP – DeliveryOptimization](/windows/client-management/mdm/policy-csp-DeliveryOptimization).

With this change, you can no longer create new versions of the old profile. However, your preexisting instances of the old profile remain available to use.

For more information about this change, see the Intune Customer Success blog at [Support tip: Windows device configuration policies migrating to unified settings platform in Intune](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-windows-device-configuration-policies-migrating-to-unified-settings-/4189665).

Applies to:

- Windows 10
- Windows 11

#### New settings available in the Apple settings catalog<!-- 31523569 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There's a new setting in the Settings Catalog. To see this setting, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), see **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

##### macOS

**Login > Login Window**:
- Show Input Menu

### Android settings in the Settings Catalog <!-- 31524383 -->

The settings catalog supports Android Enterprise and Android Open Source Project (AOSP).

Currently, to configure Android settings, you use the built-in templates. The settings from these templates are also available in the settings catalog. More settings are continually being added.

In the Intune admin center, when you create a device configuration profile, you select the **Profile Type** (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > select your **Platform** > **Profile Type**). All the profile types are moved to **Profile Type** > **Templates**.

This change:

- Is a UI change with no impact on your existing policies - Your existing policies won't change. You can continue to create, edit, and assign these policies the same way.
- Provides the same UI experience as iOS/iPadOS, macOS, and Windows templates.

In the new settings catalog experience, the management mode associated with the setting is available in the tooltip.
To get started with settings catalog, see [Use the settings catalog to configure settings on your devices](../configuration/settings-catalog.md).

Applies to:

- Android Enterprise
- AOSP

### Device enrollment

#### Custom device naming template for Android Enterprise corporate-owned devices<!-- 3465701 -->

You can use a custom template for naming Android Enterprise corporate-owned devices when they enroll with Intune. The template is available to configure in the enrollment profile. It can contain a combination of custom text and predefined variables (like device serial number, device type), and for user-affiliated devices, the owner's username. For more information, see:

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

- Admins can't create new custom profiles for personally owned work profile devices. However, admins can still view and edit previously created custom profiles.

- Personally owned work profile devices that currently have a custom profile assigned won't experience any immediate change of functionality. Because these profiles are no longer supported, the functionality set by these profiles might change in the future.

- Intune technical support no longer supports custom profiles for personally owned work profile devices.

All custom policies should be replaced with other policy types. Learn more about [Intune ending support for personally owned work profile custom profiles](https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-ending-support-for-custom-profiles-for-personally-owned-work-profile-devi/4287414)

### Device security

#### New settings added to the Windows security baseline version 24H2<!-- 32413310 -->

> [!NOTE]
> Rollout of the new settings for the security baseline is underway, but taking longer than usual. Due to this delay, the new settings might not be available until the week of May 5, 2025.

The most recent Intune security baseline for Windows, version 24H2, is updated to include 15 new settings for managing the Windows Configuration Service Provider (CSP) for [*Lanman Server*](/windows/client-management/mdm/policy-csp-lanmanserver) and [*Lanman Workstation*](/windows/client-management/mdm/policy-csp-lanmanworkstation). These settings were previously unavailable in the baseline due to missing CSP support. The addition of these settings provides better control and configuration options.

This update is an update to an existing baseline version and not a new baseline version. So, the new settings aren't visible in the baselines properties until you edit and save the baseline:

- **Pre-existing baseline instances**:
Before the new settings are available in a preexisting baseline instance, you must select and then *Edit* that baseline instance. To have the baseline deploy the new settings, you must then *Save* that baseline instance. When the baseline is opened for editing, each of the new settings becomes visible with its default security baseline configuration. Before saving, you can reconfigure one or more of the new settings. Or, make no changes other than to save the current configuration that then uses the baseline defaults for each of the new settings.

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

Microsoft Intune admin center's home page includes more links to interactive demos, documentation, and training. To see these updates, navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

## Week of April 14, 2025

### Device configuration

#### Hotpatch updates for Windows 11 Enterprise are now available<!--27009405 -->

Hotpatch updates for Windows 11 Enterprise, version 24H2 for x64 (AMD/Intel) CPU devices are now available. With hotpatch updates, you can deploy and apply security updates faster to help protect your organization from cyberattacks, while minimizing user disruptions.
From the Microsoft Intune admin center, navigate to **Devices > Windows updates > Create Windows quality update policy** and toggle it to **Allow**.

**Enroll and prepare**
The Windows quality update policy can auto-detect if your targeted devices are eligible for hotpatch updates. Devices running Windows 10 and Windows 11, version 23H2 and lower continue to receive the standard monthly security updates, helping ensure that your ecosystem stays protected and productive.

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

Intune policies for [Windows Local Administrator Password Solution (LAPS)](../protect/windows-laps-overview.md) now include several new settings and updates to two previously available settings. [LAPS](/windows-server/identity/laps/laps-overview) is a built-in Windows solution and can help you secure the built-in local administrator account that's present on each Windows device. All the settings that you can manage through Intune LAPS policy are described in the Windows [LAPS CSP](/windows/client-management/mdm/LAPS-csp).

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
  - Reset the password, log off the managed account, and terminate any remaining processes: upon expiration of the grace period, the managed account password is reset, any interactive logon sessions using the managed account are logged off, and any remaining processes are terminated.

By default, each setting in LAPS policies is set to *Not configured*, which means the addition of these new settings won't change the behavior of your existing policies. To make use of the new settings and options, you can create new profiles or edit your existing profiles.

Applies to:

- Windows

#### Configure devices to stay on the latest OS version using declarative device management (DDM)<!-- 28323647 -->

As part of the [Settings Catalog](../configuration/settings-catalog.md), you can now configure devices to automatically update to the latest OS version using DDM. To use these new settings in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS**for platform > **Settings catalog** for profile type.

**Declarative device management > Software Update Enforce Latest**.

- **Enforce Latest Software Update Version**: If true, devices upgrade to the latest OS version that is available for that device model. This feature uses the Software Update Enforcement configuration and forces devices to restart and install the update after the deadline passes.
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

## What's new archive
<!-- Past announcements that are older than six months will be moved to the archive -->

For previous months, see the [What's new archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
