---
title: What's new in previous months in the Microsoft Intune
description: Review older announcements from the Intune what's new page
ms.date: 04/20/2026
ms.topic: whats-new

ROBOTS: NOINDEX,NOFOLLOW
ms.reviewer: lebacon
ms.collection:
- M365-identity-device-management
---

# What's new in the Microsoft Intune - previous months

<!-- Maintenance plan:

     Maintain ~2 years of archived content -->

## Week of October 13, 2025

### Device management

#### Windows 10 support in Intune <!-- 34754868 -->

[!INCLUDE [Windows 10 support](../../includes/windows-10-support.md)]

For more information, see [Support statement for Windows 10 in Intune](../index.md#update-to-support-statement-for-windows-10-in-intune).

> [!div class="checklist"]
> Applies to:
>
> - Windows 10

<!-- *********************************************** -->

## Week of September 29, 2025

### App management

#### PowerShell script installer support for Enterprise App Catalog apps<!--29857395-->

You can now upload a PowerShell script to install Enterprise App Catalog apps as an alternative to using a command line. This option gives you more flexibility when deploying apps.

For more information, see [Add an Enterprise App Catalog app to Microsoft Intune](../../app-management/deployment/add-enterprise-catalog-app.md).

> [!div class="checklist"]
> Applies to:
>
> - Windows

#### End of support for older versions of the Android Intune Company Portal app <!--33827426-->

Support for Android Intune Company Portal versions earlier than **5.0.5421.0** ended on October 1, 2025. Devices running an older version of the app might no longer maintain their registration status and can be marked noncompliant.

To keep devices registered and compliant, users must download the latest version of the Company Portal from the [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

## Week of September 22, 2025

### Device security

#### Update for the Vulnerability Remediation Agent for Security Copilot in Intune (public preview)<!-- 35028555 -->

We've updated the Vulnerability Remediation Agent for Security Copilot, adding the following changes to the ongoing limited public preview:

- **Role-based access control (RBAC) for Microsoft Defender** - We've updated the [RBAC guidance](../../copilot/agents/vulnerability-remediation-agent.md#prerequisites) to reflect how RBAC is implemented in Microsoft Defender XDR. Guidance is now provided for configurations that use [**Unified RBAC**](/defender-xdr/manage-rbac) (a single set of permissions across services) and for [**granular RBAC**](/defender-endpoint/rbac) (customized permissions per service).

  When using granular RBAC configurations, ensure the agent's identity is scoped in Microsoft Defender to include all relevant device groups. The agent can't access or report on devices outside its assigned scope.

- **Agent Identity** – You can now [manually change the account that the agent uses as its identity](../../copilot/agents/vulnerability-remediation-agent.md). From the agents *Settings* tab, select **Choose another identity** to open a sign-in prompt. Enter and authenticate the new account. Ensure the new account has sufficient permission to access the Microsoft Defender Vulnerability Remediation data.

  Changes to the agent's identity won't affect the agent's run history, which remains available.

These updates provide greater flexibility and control for organizations using the Vulnerability Remediation Agent in preview. To learn more about this Agent, see [Vulnerability Remediation Agent for Security Copilot in Microsoft Intune](../../copilot/agents/vulnerability-remediation-agent.md).

## Week of September 15, 2025 (Service release 2509)

### Device configuration

#### Filter device configuration profiles by the policy type<!-- 33223685 -->

In the Intune admin center > **Devices** > **Configuration** > **Policies** tab, you can use the **Add filters** feature to filter your list of policies by platform, scope tags, and the last modified date.

**Policy type** is available in the **Add filters** feature. So, you can filter your list of policies by their type, like the settings catalog, custom, device restrictions, and the other policy types.

To learn more about viewing and monitoring existing profiles, see [View and monitor device configuration policies in Microsoft Intune](../../device-configuration/monitor-device-profile.md).

#### New day zero settings available in the Apple settings catalog <!-- 33806647 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Managed Settings > Default Applications**:

- Calling
- Messaging

**Restrictions**:

- Allowed Camera Restriction Bundle IDs

**Web > Web Content Filter**:

- Safari History Retention Enabled

##### macOS

**Authentication > Extensible Single Sign On Kerberos**:

- Use Platform SSO TGT

**Microsoft Defender**:

- The Microsoft Defender category is updated with new settings. Learn more about available macOS Defender settings at [Microsoft Defender - Policies](/defender-endpoint/mac-preferences).

**Restrictions**:

- Allow Call Recording
- Allow Live Voicemail

**Web > Web Content Filter**:

- Safari History Retention Enabled

#### Settings available in both Templates and Settings Catalog for Android Enterprise <!-- 34226745 -->

Some settings that were only available in Templates are now also supported in the settings catalog.

The [settings catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

To create a new settings catalog policy, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type.

The following settings are in the settings catalog:

**Applications**:

- Allow installation from unknown sources
- App auto-updates (work profile-level)

**General**:

- Block roaming data services
- Block Bluetooth configuration
- Block Wi-Fi access point configuration
- Default permission policy
- Block access to camera
- Allow access to developer settings
- Block beaming data from apps using NFC (work-profile level)

  This setting is deprecated in A10. While it still configures correctly on newer devices, it has no effect because the feature isn't available.

- Block factory reset
- Block tethering and access to hotspots
- Block volume changes

  This setting appears as successfully applied to corporate-owned devices with a work profile, but it has no effect.

**System Security**:

- Require threat scan on apps
- Require Common Criteria mode

**Users and accounts**:

- User can configure credentials (work profile-level)
- Block account changes

To learn more about these settings, see [Android Intune settings catalog settings list](../../device-configuration/settings-catalog/ref-android-settings.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

### Device management

#### Device category management supports Multi Admin Approval<!-- 26838632 -->

Intune [device categories](../../device-management/create-device-categories.md) support Multi Admin Approval. When Multi Admin Approval is enabled, changes to device categories, including creating a new one, editing or deleting one, require a second administrator to approve the change before it's applied. This dual authorization process helps protect your organization from unauthorized or accidental role-based access control changes.

For more information on multiple administrative approvals, see [Use multiple administrative approvals in Intune](../../fundamentals/role-based-access-control/multi-admin-approval.md).

#### New Private Space and USB access settings in the Android Enterprise settings catalog <!-- 30802944 24213820 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

There are new settings (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type):

- **Block private space**: When set to **True**, users are prevented from creating or using private spaces on the device. All existing private spaces are deleted.

  > [!div class="checklist"]
  > Applies to:
  >
  > - Android Enterprise corporate-owned devices with a work profile (COPE)

- **USB access**: Allows admins to select what files and/or data can be transferred via USB. If admins block file transfer, only files are blocked from being transferred. Other connections are allowed, like a mouse. If admins block USB data transfer, all data is blocked.

  > [!div class="checklist"]
  > Applies to:
  >
  > - Android Enterprise corporate-owned devices with a work profile (COPE) (At work profile level)
  > - Android Enterprise corporate owned fully managed (COBO)
  > - Android Enterprise corporate owned dedicated devices (COSU)

For a list of existing settings you can configure in the settings catalog, see [Android Enterprise device settings list in the Intune settings catalog](../../device-configuration/settings-catalog/ref-android-settings.md).

#### New prompts available to explore your Intune data<!-- 34601881 -->

You can use Microsoft Copilot in Intune to explore new prompts related to your Intune data using natural language. Use these new prompts to view data on:

- Android and Apple device updates
- Windows Autopilot
- [Endpoint Privilege Management](../../epm/overview.md)
- [Advanced Analytics](../../advanced-analytics/index.md)

When you start typing your request, a list of prompts that best match your request are shown. You can also continue typing for more suggestions.

Each query returns a Copilot summary to help you understand the results and offers suggestions. With this information, you can also:

- Add devices or users from the results to a group so you can target apps and policies to this group.
- Filter example queries to find or build requests that match your needs.

To learn more, see [Explore Intune data with natural language and take action](../../copilot/explorer.md).

#### Intel vPro Fleet Services integration in Intune partner portal <!-- 33964910 -->

Microsoft Intune now integrates with Intel vPro Fleet Services, bringing hardware-level remote management directly into the Intune experience. This solution enables IT admins to securely manage, recover, and troubleshoot Intel vPro devices even when the operating system is unresponsive, or the device is powered off. With Microsoft Entra ID single sign-on, teams gain authenticated access without requiring more infrastructure or licensing.

Key capabilities include:

- Hardware-level BIOS and OS recovery through Intel Active Management Technology (AMT)
- Centralized workflows within Intune
- Enhanced security and access control
- Broad compatibility with Intel vPro devices (2018 or later)

This integration simplifies endpoint management and improves operational efficiency, and scales to support diverse device fleets.

#### Device Inventory (formerly Resource explorer) <!-- 33630406 -->

The **Resource explorer** pane under **Monitor** for Windows devices is now called **Device Inventory**. Only the name changed—the experience and data remain the same.

References in Intune documentation and the Intune admin center are updated to reflect the new name.

> [!div class="checklist"]
> Applies to:
>
> - Windows

> [!NOTE]
> The **Resource explorer** pane that displays Configuration Manager data via [tenant attach](../../configmgr/tenant-attach/resource-explorer.md) still retains its original name.

#### New features in Copilot for Microsoft Intune <!-- 32549162 -->

- **Easier access to Copilot Chat** - Copilot Chat is embedded directly into the Intune admin center header. So, IT admins can access Copilot Chat from any screen in the admin center. This feature helps admins get faster insights and support.

- **Context-aware conversations with Copilot Chat** - As you type, a dynamic prompt box provides real-time suggestions and recommends prompts relevant to what you're trying to ask. You can troubleshoot devices, manage policies, explore Windows 365 features, and more. You can also directly access the Microsoft docs to learn more.

  Copilot Chat retains your conversation history and remains context aware as you move through the admin center. This continuity helps minimize repetitive prompts.

- **Expanded support for Windows 365 Cloud PC** - With this general availability update, Copilot now supports Windows 365 Cloud PC management. IT admins can access important info, like licensing status, connection quality, configuration details, and performance metrics. This feature makes it easier for admins to monitor and manage Cloud PCs directly from the Intune admin center.

To learn more about Copilot in Intune and to get started, see [Microsoft Copilot in Intune](../../copilot/index.md).

#### Intune supports iOS/iPadOS 17.x as the minimum version<!--33405397-->

Apple released iOS 26 and iPadOS 26. With this release, Microsoft Intune—including the Intune Company Portal and app protection policies (APP, also known as MAM)—now requires iOS/iPadOS 17 or later.

For more information on this change, see [Plan for change: Intune is moving to support iOS/iPadOS 17 and later](../index.md#plan-for-change-intune-is-moving-to-support-iosipados-17-and-later).

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

> [!div class="checklist"]
> Applies to:
> - iOS/iPadOS

#### Intune supports macOS 14.x as the minimum version<!--33412147 -->

Apple released macOS 26 (Tahoe). With this release, Microsoft Intune, the Company Portal app, and the Intune MDM agent now require macOS 14 (Sonoma) or later.

For more information on this change, see [Plan for change: Intune is moving to support macOS 14 and later](../index.md#plan-for-change-intune-is-moving-to-support-macos-14-and-higher-later-this-year).

> [!NOTE]
> macOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement](https://aka.ms/Intune/macOS/ADE-DE-support).

For a list of supported OS version, see [Supported operating systems and browsers in Intune](../../fundamentals/ref-supported-platforms.md).

> [!div class="checklist"]
> Applies to:
>
> - macOS

### Device security

#### New security baseline update experience<!-- 31607281  -->

The Intune security baseline update experience is updated for the more recent versions of security baselines. With this change, when you update a security baseline that was created after May 2023 to a more recent version of that same baseline, you now have two options to help automatically configure the updated baseline:

- Keep customizations – With this option, Intune applies all the settings customizations from the original baseline that you're upgrading to the new baselines template. The result is that the new baseline instance retains (includes) all your organization's specific modifications.
- Discard customizations – With this option, Intune creates a new 'default' baseline instance that uses the new baseline version. Each setting in that baseline uses the baseline default and none of your settings customizations are automatically applied.

With both options, your decision is applied to a new profile instance of that baseline, which uses the latest baseline version. This new profile won't have the scope tags or assignments from the original, which you can add later after the new profile has been created. This change gives you time to configure other settings if desired before the updated profile is assigned and begins to deploy the latest baseline version to devices. Meanwhile, your original baseline is left unchanged and remains active. But, its setting configurations become read-only.

For more information, see [Update a baseline profile to the latest version](../../device-security/security-baselines/configure-baselines.md#update-a-baseline-profile-to-the-latest-version)  in Manage security baseline profiles in Microsoft Intune.

#### Company Portal supports Purebred's new derived credentials experience<!--31973776-->

Apple released iOS 26 and iPadOS 26. With this update, Purebred (version 3) introduces a new and improved derived credentials experience. As part of day zero support, Company Portal supports Purebred's updated workflow.

- If your organization plans to continue using the older version of Purebred, there are no changes to your derived credentials experience in Purebred or Company Portal—even if you upgrade to the latest version of Company Portal.
- If your organization plans to upgrade to the new version of Purebred, make sure to update to Company Portal version 5.2509.0 to ensure compatibility.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

### Monitor and troubleshoot

#### Give feedback about multiple device query<!--  -->

Use the new feedback feature on the multiple device query page to submit feedback about multiple device query.

## Week of September 8, 2025

### Device security

#### JavaScript WebSockets support with Microsoft Tunnel for Mobile Application Management for iOS <!-- 28660712 -->

Microsoft Tunnel for Mobile Application Management (MAM) for iOS now supports JavaScript WebSockets from web views. This support helps improve communications for apps that require real-time communications that rely on WebSockets.

While JavaScript WebSockets are now supported, Tunnel for MAM iOS doesn't support native WebSocket APIs or apps that rely on them.

For more information, see [Microsoft Tunnel for Mobile Application Management for iOS/iPadOS admin guide](../../device-security/microsoft-tunnel/mam-ios.md).

## Week of September 1, 2025

### Device management

#### Enrollment Status Page support for installing Windows security updates during Windows OOBE <!-- 7183120 -->

> [!IMPORTANT]
>
> Beginning on January 13, 2026, this capability is available. The first Windows Update that is offered as available is the `2026-01 B` quality update.

The Windows out-of-box experience (OOBE) by default installs the latest available security updates to help ensure devices are secure and up to date from day one. Windows OOBE is used by Intune and by Windows Autopilot scenarios through the Intune enrollment status page (ESP) configurations. Intune refers to these security updates Windows quality updates.

To help you manage this behavior, we've updated the Intune enrollment status page with a new setting you can use to allow or block the automatic installation of these updates.

The new setting is **Install Windows quality updates**. These security updates, also known as Windows quality updates in Intune, are installed by default during the Windows out-of-box experience OOBE that's used by Intune and by Windows Autopilot.

By default, this setting is set to *Yes* in all new ESP profiles you create, which results in the most recent security updates being installed. In all your previously created ESP profiles, this setting is set to *No* until you choose to edit those profiles to change it. When set to *No*, OOBE doesn't install the updates, which can give your internal teams time to test the updates before allowing them to install on new devices you provision.

For more information about the Intune enrollment status page, see [Set up Enrollment Status Page](../../device-enrollment/windows/setup-status-page.md). For information about Windows quality updates, see [Windows quality update policy](../../device-updates/windows/manage-quality-updates.md).

> [!div class="checklist"]
> Applies to:
>
> - Windows

### Device security

### Device configuration recommendations from the Security Copilot Vulnerability Remediation Intune agent<!-- 34346149 -->

To help reduce your organization's attack surface against vulnerabilities, the Security Copilot Vulnerability Remediation Intune agent now provides recommended configurations for settings related to a reported vulnerability.

You can find the recommended configurations after selecting *Agent suggestions* for a reported vulnerability, which opens the *Suggested action* pane. On the suggested action pane, there's a new section of information titled **Configurations**.

If the Intune settings catalog contains relevant settings for the reported vulnerability, the Configurations section provides information to help you configure device policies. These policies can help minimize future risk from that vulnerability, including:

- A list of the settings that are relevant to the current vulnerability, which can be deployed through an Intune settings catalog policy. Only the specific settings that are relevant to the vulnerability are listed.
- Each setting is presented with a recommended configuration.
- Selecting the citation icon next to a setting displays that settings description. The description can also include a link to content for the Configuration Service Provider (CSP) that the setting represents.

If there are no recommended device configuration settings to deploy, the Configurations section indicates that no recommended settings catalog policy configurations are available.

To learn more about Agent suggestions, remediation guidance, and the new recommended configurations, see [Agent suggestions](../../copilot/agents/manage-vulnerability-remediation-agent.md#manage-agent-suggestions) in *Use the Vulnerability Remediation Agent*.


## Week of August 25, 2025

### App management

#### Offline Mode and App access without sign in for Android Enterprise Dedicated Devices on Managed Home Screen<!-- 30303710, 25476290 -->

Managed Home Screen (MHS) for Android Enterprise dedicated devices now supports two new features: **Offline mode** and **App access without sign in**.

- **Offline mode** – Lets users access designated apps when the device is offline or unable to connect to the network. You can configure a grace period before requiring users to sign in once connectivity is restored.
- **App access without sign in** – Lets users launch specific apps from the MHS sign-in screen via the MHS top bar, regardless of network status. This feature is useful for apps that need to be available immediately, such as help desk or emergency tools.

These features are designed for dedicated devices enrolled in Microsoft Entra shared device mode and can be configured via device configuration policy.

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise dedicated devices

## Week of August 18, 2025 (Service release 2508)

### App management

#### Android app configuration policies support new variable values<!-- 32843208 -->

Android Enterprise app configuration policies in Intune now support more variable values. The new values include account name, device name, employee ID, MEID, serial number, and the last four digits of the serial number.

For more information, see [Supported variables for configuration values](../../app-management/configuration/configure-managed-android.md#supported-variables-for-configuration-values).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

### Device configuration

#### Managed Installer support for user and device groups <!-- 30293237 -->

Our Managed Installer policy is updated to add the capability to target individual groups of users and devices, using one or more individual policies. Until now, a Managed Installer policy was a tenant-wide configuration that applied to all Windows devices. With this update, separate policies can now be assigned to different device groups providing you with more flexibility.

If you previously had a tenant-wide managed installer policy in effect, that policy remains available with a group assignment to all your devices. This reconfiguration is equivalent to the previous tenant-wide configuration it had before. You can choose to use that converted policy or implement new policies with more granular control.

For more information about configuring and using managed installers, see [Get started with managed installers](../../device-configuration/endpoint-security/manage-app-control.md#get-started-with-managed-installers).

> [!div class="checklist"]
> Applies to:
>
> - Windows

#### New Windows settings in the settings catalog <!-- 34345586 34545262-->

The Intune [settings catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure, and all in one place. There are new settings in the Windows settings catalog (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type).

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

  The following legacy settings are deprecated, and shouldn't be used:

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

  The following legacy settings are deprecated, and shouldn't be used:

  | Setting | CSP |
  | --- | --- |
  | **Microsoft Edge** > **Controls whether the new HTML parser behavior for the `<select>` element is enabled** | SelectParserRelaxationEnabled |
  | **Microsoft Edge** > **Enable keyboard focusable scrollers** | KeyboardFocusableScrollersEnabled |

- Some existing policies have string updates that reflect the latest browser behavior and terminology.

**OneDrive**:

- **Disable a toast and activity center message to encourage a user to sign in OneDrive using an existing credential that is made available to Microsoft applications** - This setting allows IT admins to prevent detection of new accounts in OneDrive, helping enforce organizational sync and access controls.

**Administrative Templates\Windows Components\Sync your settings**:

- **Enable Windows Backup** - This setting allows IT admins to manage syncing behavior for Windows Backup features. Specifically, this policy controls whether language preferences are included in backup sync, which helps organizations tailor backup configurations to their needs.

> [!div class="checklist"]
> Applies to:
>
> - Windows

#### New day zero settings available in the Apple settings catalog<!-- 33437616 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

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

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

There's a new **Hide organization name** setting (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type). When set to **True**, the enterprise name isn't shown on the device, such as lock screen.

For a list of existing settings you can configure in the settings catalog, see [Android Enterprise device settings list in the Intune settings catalog](../../device-configuration/settings-catalog/ref-android-settings.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned devices with a work profile (COPE)
> - Android Enterprise corporate owned fully managed (COBO)

### Device enrollment

#### Intune supports Ubuntu 22.04 and later<!-- 32756619 -->

Microsoft Intune and the Microsoft Intune app for Linux now support Ubuntu 22.04 LTS and Ubuntu 24.04 LTS. Support ended for Ubuntu 20.04 LTS. Devices that are currently enrolled on Ubuntu 20.04 LTS remain enrolled even though the version is no longer supported. New devices are unable to enroll if they're running Ubuntu 20.04 LTS. To see what devices or users might be affected, check your Intune reporting. In the admin center, go to **Devices **> **All devices** and filter OS by Linux. You can add more columns to help identify who in your organization has devices running Ubuntu 20.04 LTS. Notify your users to upgrade their devices to a supported Ubuntu version.

For more information about Linux enrollment, see [Linux device enrollment guide for Microsoft Intune](../../device-enrollment/guide-linux.md).


### Device management

#### Wipe remote action supports Multi Admin Approval<!-- 27043113 -->

When you use the Multi Admin Approval feature, you require a second admin account to approve a change before the change is applied.

The **[Wipe](../../device-management/actions/wipe.md)** remote action supports Multi Admin Approval. Use Multi Admin Approval with the **Wipe** action to help mitigate the risk of unauthorized or compromised remote actions by a single admin account.

For more information on Multi Admin Approval, see [Use Multi Admin Approval in Intune](../../fundamentals/role-based-access-control/multi-admin-approval.md).

#### Configure Windows Backup for Organizations (public preview)<!-- 33829628 -->

Intune administrators can configure a new feature in public preview called Windows Backup for Organizations. With this feature, you can back up your organization's Windows 10 or Windows 11 settings and restore them on a Microsoft Entra joined device. Backup settings are configurable in the Microsoft Intune admin center settings catalog, while a tenant-wide setting that lets you restore a device is available in the admin center under **Enrollment**. The backup setting is available now in public preview, while the restore setting will be available for public preview beginning August 26.

For more information about this feature, see [Windows Backup for Organizations in Microsoft Intune](../../device-enrollment/windows/enable-backup-restore.md).

#### New resolution button improves compliance remediation experience<!-- 31370959 -->

We improved the Just in Time (JIT) compliance remediation experience for device users in Microsoft Intune. Intune collaborated with Microsoft Defender to:

- Remove user clicks required to view and learn remediation steps.
- Add a **Resolve** button to reduce time-to-remediation.

When a user opens a productivity app and sees they're marked noncompliant due to Microsoft Defender, the user can now select **Resolve.** This action redirects them to Microsoft Defender, where Microsoft Defender takes steps to remediate the user and then redirect the user back to their productivity app.

Even if you aren't using Microsoft Defender, if you have Conditional Access turned on your users can have an improved experience. With JIT compliance remediation, users go through an embedded flow that shows them their compliance status, noncompliance reasoning, and a list of actions right within a productivity app. This flow eliminates extra steps, the need to switch between apps, and reduces the number of authentications.

As an admin, if you have JIT registration and compliance remediation set up already, you have no action items. If you don't, set it up today to support this new functionality. For more information, see:

- [Set up just-in-time registration](../../device-enrollment/apple/setup-just-in-time-registration.md).
- [Update iOS device settings](../../user-help/compliance/device-settings-ios.md).

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

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

### Monitor and troubleshoot

#### Declarative software update reports for Apple devices<!-- 25207078, 31557946 -->

You can now use several new [software update reports for Apple devices](../../device-updates/apple/monitor-reports.md) that are powered by Apples built-in declarative reporting infrastructure. The declarative reporting infrastructure provides Intune with a near real-time view of the software update status of managed devices. The following Apple software update reports are now available:

- A *per-device software update report* - Per-device software update reports are available in the Intune Admin center by going to *Devices* and then selecting an applicable device. In the Devices Overview pane for that device, below Monitor, you see the report listed as **iOS software updates** for iOS or iPadOS devices, and as **macOS software updates** for macOS devices.

  With these per-device reports available, the previously available macOS per-device **Software updates** report is now deprecated. While the deprecated report remains available in the admin center and can still be used while viewing a device, the report will be removed from Intune with a future update.

- **Apple software update failures** - With this operational report, you can view details across your entire managed Apple device fleet. Details include why the update failed to install and the timestamp of the last failure. To find this report, in the admin center go to *Devices* > *Monitor*, and then select the report's name to view the report details.

- **Apple software update report** - This report is an organizational report that displays details about pending and current software update information across your entire managed Apple device fleet. To find this report, in the admin center go to *Reports* > *Device management* > *Apple updates*, select the *Reports* tab, and then select the report tile.

- **Apple software update summary report** - View the Apple software update summary report, in the admin center go to *Reports* > *Device management* > *Apple updates*, and then select the *Summary* tab. You see a roll-up of update status from macOS, iOS, and iPadOS devices. This status includes the version of the latest update that's available for each platform, and the date that update became available.

The following Apple devices support these new reports:

- iOS 17 and later
- iPadOS 17 and later
- macOS 14 and later

For more information about the changes behind these reports, see [Support tip: Move to declarative device management for Apple software updates](https://techcommunity.microsoft.com/blog/IntuneCustomerSuccess/support-tip-move-to-declarative-device-management-for-apple-software-updates/4432177).

### Role-based access control

#### Multi Admin Approval support for role-based access control<!-- 26838684 -->

Multi Admin Approval now supports role-based access control. When enabled, any changes to roles, including modifications to role permissions, admin groups, or member group assignments, require a second administrator to approve the change before it's applied. This dual authorization process helps protect your organization from unauthorized or accidental role-based access control changes.

For more information, see [Role-based access control in Microsoft Intune](../../fundamentals/role-based-access-control/overview.md).




## Week of August 11, 2025

### Device management

#### Platform SSO is generally available (GA) and also supports custom TGT<!-- 33990050 -->

Platform SSO is a feature in Microsoft Entra that enables single sign-on (SSO) using a Microsoft Entra ID on macOS devices. Using the Intune settings catalog, you can configure Platform SSO and use Intune to deploy the Platform SSO configuration to your macOS devices.

- Microsoft Entra announced that Platform SSO for macOS devices is generally available (GA). For more information on this Microsoft Entra feature, see [Microsoft Enterprise SSO plug-in for Apple devices](/entra/identity-platform/apple-sso-plugin).
- Microsoft Entra supports Kerberos Ticket Granting Tickets (TGTs) to access on-premises Active Directory and Microsoft Entra ID using [Apple's Kerberos SSO extension](https://support.apple.com/guide/deployment/depe6a1cda64/web).

  On the Company Portal version 5.2508.0 and newer, you can use the Intune settings catalog Platform SSO policy to enable Kerberos SSO to on-premises and cloud resources using the TGTs.

To configure Platform SSO in Intune, see:

- [Configure Platform SSO for macOS devices in Intune](../../device-configuration/settings-catalog/configure-platform-sso-macos.md)
- [Common Platform SSO scenarios for macOS devices in Intune](../../device-configuration/settings-catalog/configure-platform-sso-scenarios-macos.md)

> [!div class="checklist"]
> Applies to:
>
> - macOS

### Device security

#### Update required for Microsoft Tunnel endpoints<!-- 32817331 -->

As part of our ongoing improvements to the Microsoft Tunnel infrastructure, we introduced new endpoints with the [March 19, 2025 release](../../device-security/microsoft-tunnel/upgrade.md). You must upgrade your Microsoft Tunnel to the March 19, 2025 release version or later to ensure you're using the new endpoints. Once you upgrade to this version or later, you can't downgrade to an earlier version. Earlier releases that rely on legacy endpoints aren't supported and might cause service disruptions. To continue with uninterrupted service, we recommend upgrading to the latest supported build and avoiding rollback to unsupported versions.

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

For more information, see [How to use Microsoft Entra ID to access the Intune APIs in Microsoft Graph](../../developer/configure-graph-api-access.md).

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

For more information, see [Use variables in elevation rules](../../epm/create-elevation-rules.md#use-variables-in-elevation-rules) in Configure policies for Endpoint Privilege Management.

### App management

#### Newly available OEMConfig apps in Intune <!-- 5306739 -->

The following OEMConfig app is now available in Intune for Android Enterprise:

- RugGear

For more information about OEMConfig, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../../device-configuration/templates/configure-oemconfig-android.md).

### Device configuration

#### New settings available in the Apple settings catalog <!-- 33064192 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

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

Using cleanup rules, you can configure Intune to automatically clean up devices that appear to be inactive, stale, or unresponsive.

With this feature, you can:

- Configure individual device cleanup rules per platform, like Windows, iOS/iPadOS, macOS, and Android.
- Use the [Audit logs](../../governance/monitor-audit-logs.md) to see the devices that the device cleanup rules conceal from the Intune reports.
- Use [role-based access control (RBAC)](../../fundamentals/role-based-access-control/overview.md) to customize the user roles that can create device cleanup rules.

For more information, see [device cleanup rules](../../governance/configure-cleanup-rules.md).

### Device security

#### macOS support for local administrator account configuration with password solution - GA <!-- 25385731 -->

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

To learn about all the details for this new capability, see [Configure support for macOS ADE local account configuration with LAPS in Microsoft Intune](../../device-security/laps/setup-macos.md).

### Intune apps

#### Newly available protected apps for Intune<!-- 33015811, 33016789 -->

The following protected apps are now available for Microsoft Intune:

- Vault CRM by Veeva Systems Inc. (iOS)
- Workvivo by Workvivo

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

## Week of July 14, 2025

### Device management

#### Experience Microsoft Copilot in Intune<!-- 29339619, 31192897 -->

You can now use Microsoft Copilot in Intune to explore your Intune data using natural language, take action on the results, manage policies and settings, understand your security posture, troubleshoot device issues, and view insights about enrolled Surface devices.

- **Explore your Intune data** - Use natural language to explore your Intune data and take action based on the results. Admins can run queries against Intune resource data, including questions about devices, apps, policies, updates, and compliance. When a query runs, a Copilot summary helps you understand the results and offers suggestions. You can add devices or users from the query results to a group to target apps and policies. There are also example queries that you can filter to find an example that best matches your request or use to help you create your own request.

  Data coverage, querying capabilities, and actionability will evolve over time as we make improvements to how you explore your data.

  To learn more about this feature, see [Explore Intune data with natural language and take action](../../copilot/explorer.md).

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

  To learn more about this feature, see [Security Copilot in Microsoft Surface Management Portal](/surface/security-copilot-surface-management-portal).

### Monitor and troubleshoot

#### Export device query results to CSV file <!-- 27967896 -->

Now after running a multiple-device query, you can export up to 50,000 query results to a CSV file. For more information, see [How to use device query for multiple devices](../../advanced-analytics/device-query-multiple-devices.md#use-device-query-for-multiple-devices).

## Week of June 23, 2025 (Service release 2506)

### App management

#### Microsoft Intune support for Apple AI features<!-- 12792722, 30550110, 30220799 -->

Intune app protection policies have new standalone settings for Apple AI features (Genmojis, Writing tools, and screen capture). Apps running the following Intune App SDK and App Wrapping Tool versions support the standalone settings:

- Xcode 15 version 19.7.12 or later
- Xcode 16 version 20.4.0 or later

Previously, these Apple AI features were blocked when the app protection policy **Send Org data to other apps** setting is configured to a value other than **All apps**.

For more information about Intune's related app protection policies, see [iOS app protection policy settings](../../app-management/protection/ref-settings-ios.md).

#### Add Enterprise App Catalog apps to ESP blocking apps list<!-- 29846319 -->

Windows Autopilot now supports Enterprise App Catalog apps. Microsoft Intune Enterprise App Management enables IT admins to easily manage applications from the Enterprise App Catalog. Using Windows Autopilot, you can select apps from the Enterprise App Catalog as blocking apps in the Enrollment Status Page (ESP) and the Device Preparation Page (DPP) profiles. This feature allows you to ensure those apps are delivered before the user can access the desktop.

For related information, see [Set up the Enrollment Status Page](../../device-enrollment/windows/setup-status-page.md), [Overview of Windows Autopilot device preparation](/autopilot/device-preparation/overview), and [Add an Enterprise App Catalog app to Microsoft Intune](../../app-management/deployment/add-enterprise-catalog-app.md).

> [!div class="checklist"]
> Applies to:
>
> - Windows

#### Managed Home Screen orientation changes with Android 16<!-- 30316862 -->

Starting with Android 16, Android stops enforcing screen orientation on devices with 600 dp and larger display settings. This change impacts the Managed Home Screen (MHS) on devices with larger form factors, like tablets.

On these Android 16 devices, orientation is determined by the device's orientation setting, not the MHS settings you configure.

To learn more about Android 16 changes, see [Behavior changes: Apps targeting Android 16 or higher](https://developer.android.com/about/versions/16/behavior-changes-16) (opens Android website).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

### Device configuration

#### New settings available in the Apple settings catalog<!-- 32498293 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

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

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

There's a new **Block Bluetooth** setting (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type). When set to **True**, Bluetooth is disabled on the device.

There's also a **Block Bluetooth Configuration** setting that prevents end users from changing the Bluetooth setting on the device.

These settings are different and have different results. Some examples include:

- **Scenario**: An end user turned on the Bluetooth setting on their device. The admin creates an Intune policy that sets the **Block Bluetooth** setting to **True**.

  In this situation, Bluetooth is blocked on the device, even though the end user turned it on.

- **Scenario**: An end user turned on the Bluetooth setting on their device. The admin creates an Intune policy that sets the **Block Bluetooth Configuration** setting to **True**.

  In this situation, Bluetooth is turned on since the end user previously turned it on. The end user can't turn off Bluetooth. If the end user previously turned Bluetooth off, and then the **Block Bluetooth Configuration** policy applies, then Bluetooth is turned off and the end user can't turn it back on.

For a list of existing settings you can configure in the settings catalog, see [Android Enterprise device settings list in the Intune settings catalog](../../device-configuration/settings-catalog/ref-android-settings.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned devices with a work profile (COPE)
> - Android Enterprise corporate owned fully managed (COBO)
> - Android Enterprise corporate owned dedicated devices (COSU)

### Device management

#### New reporting system for improved performance and data consistency <!-- 31823383, 33812267 -->

Microsoft Intune is rolling out the new Policy Reporting Service (PRS) V3. The new system brings faster report generation, improved reliability, and better data consistency.

In the first phase, some high-traffic compliance and device configuration reports are transitioning to the new system.

Users notice quicker updates in the Intune admin center and fewer issues with stale data. No action is required from users, as your reports transition automatically.

With (PRS) V3, device reports only update when a device checks in. This behavior is an intentional change from previous versions.

If a policy is removed but the device hasn't checked in, the report continues to show the last known status. The policy is removed during the next check-in, at which point the report is updated. This behavior improves accuracy but can differ from what customers experienced with (PRS) V1.

To learn more about the Intune reports you can use, see [Intune reports](../../device-management/reports/overview.md).

### Device security

#### New attributes and S/MIME baseline requirements for SCEP certificate profiles <!-- 33116047 -->

Intune supports two new attributes for subject name settings in SCEP and PKCS device configuration profiles. They include:

- G={{GivenName}}
- SN={{SurName}}

Beginning July 16, if you're using a third party public certificate authority (CA) integrated with the Intune SCEP API for issuing S\MIME (encryption or signing) certificates anchored up to a public root CA, then you must use these attributes in the subject name format. After that date, a public CA won't issue or sign S\MIME certificates that omit these attributes.

For more information, see [S/MIME certificate requirements for third party public CA](../../device-configuration/certificates/scep-profiles.md#smime-certificate-requirements-for-third-party-public-ca).

### Intune apps

#### Newly available protected apps for Intune<!-- 32647747, 32692741, 32775449, 32920017 -->

The following protected apps are now available for Microsoft Intune:

- Datasite for Intune by Datasite (iOS)
- Mijn InPlanning by Intus Workforce Solutions (iOS)
- Nitro PDF Pro by Nitro Software, Inc. (iOS)
- SMART TeamWorks by SMART Technologies ULC (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

### Monitor and troubleshoot

#### New status column in Windows hardware attestation report<!-- 26527908 -->

We added a new column, **Attest Status**, to the Windows hardware attestation report to improve visibility into attestation errors. This column shows error messages received during the attestation process, helping you identify issues from both the service and client sides. Error types shown in this column include:

- WinINet errors
- HTTP bad request errors
- Other attestation-related failures

For more information about the report, see [Windows hardware attestation report](../../device-management/reports/overview.md#windows-hardware-attestation-report-organizational).

## Week of June 9, 2025

### App management

#### ARM64 support for Win32 apps<!-- 28475401 -->

When adding a Win32 app to Intune, you can select an option to check and install the app on Windows devices running ARM64 operating systems. This capability is available from the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **All apps** > **Create**. The ARM64 option is available by selecting the **Operating system architecture** option under the **Requirements** step. To ensure that you don't have any impact to any Win32 applications that you previously targeted to 64-bit devices, your existing 64-bit Win32 applications also have ARM64 selected. After the availability of being able to specifically target ARM64 operating system architectures, selecting x64 won't target ARM64 devices.

For related information, see [Win32 app management in Microsoft Intune](../../app-management/deployment/win32.md).

> [!div class="checklist"]
> Applies to:
>
> - Windows devices

## Week of June 2, 2025

### Device security

#### Vulnerability Remediation Agent for Intune (public preview)<!-- 33475311 -->

The Vulnerability Remediation Agent is currently in a limited public preview and available to only a select group of customers. If you're interested in gaining access or would like to learn more, please reach out to your sales team for further details and next steps.

When run, this agent uses data from Microsoft Defender Vulnerability Management to identify and then provide remediation guidance for vulnerabilities on your managed devices. You run and access the agent and view its results from within the Intune admin center where you see suggestions prioritized by the agent for remediation. Each suggestion includes key information like associated CVEs, severity, exploitability, affected systems, organizational exposure, business impact, and remediation guidance.

This information empowers you with a current assessment of potential risk to your environment and guidance to help you decide which risk to address first.

For more information about this agent including prerequisites, see [Vulnerability Remediation Agent for Security Copilot in Microsoft Intune](../../copilot/agents/vulnerability-remediation-agent.md).

## Week of May 26, 2025 (Service release 2505)

### Microsoft Intune Suite

#### Endpoint Privilege Management rules explicitly deny elevation<!-- 30225542 -->

Endpoint Privilege Management (EPM) elevation rules now include a new file elevation type of **Deny**. An EPM elevation rule set to *Deny* blocks the specified file from running in an elevated context. We recommend using file elevation rules to allow users to elevate specific files. But, a deny rule can help you ensure that certain files like known and potentially malicious software can't be run in an elevated context.

*Deny* rules support the same configuration options as other [elevation types](../../epm/create-elevation-rules.md#creating-elevation-rules-with-endpoint-privilege-management) except for child processes, which aren't used.

For more information about EPM, which is available as an [Intune Suite add-on-capability](../../fundamentals/add-ons.md), see [Endpoint Privilege Management overview](../../epm/overview.md).

### App management

#### Newly available protected apps for Intune<!-- 31844143, 31974161, 32037902, 32038043 -->

The following protected apps are now available for Microsoft Intune:

- Windows App by Microsoft Corporation (Android)
- Microsoft Clipchamp by Microsoft Corporation (iOS)
- 4CEE Connect by 4CEE Development
- Mobile Helix Link for Intune by Mobile Helix

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

### Device configuration

### Manage DFCI profiles for Windows devices<!-- 30305262 -->

You can use DFCI profiles to manage UEFI (BIOS) settings for NEC devices that run Windows 10 or Windows 11. Not all NEC devices running Windows are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

You can manage DFCI profiles from within the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by going to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type. For more information about DFCI profiles, see:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../../device-configuration/templates/configure-dfci-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](/autopilot/dfci-management)

> [!div class="checklist"]
> Applies to:
>
> - Windows

### Device enrollment

#### Custom naming template for AOSP devices <!-- 31707864 -->

Use a custom template for naming AOSP user-affiliated and userless devices when they enroll with Intune. The template is available to configure in the enrollment profile. It can contain a combination of free text and predefined variables (like device serial number, device type), and for user-affiliated devices, the owner's username. For more information about how to configure the template, see:

- [Set up Intune enrollment for Android (AOSP) corporate-owned userless devices](../../device-enrollment/android/setup-aosp-corporate-userless.md)
- [Set up Intune enrollment for Android (AOSP) corporate-owned user-associated devices](../../device-enrollment/android/setup-aosp-corporate-user-associated.md)


#### Change to role-based access control for device enrollment limits<!-- 27115176 -->

We updated role-based access control (RBAC) for device limits. If you're currently assigned the [policy and profile manager](../../fundamentals/role-based-access-control/ref-built-in-roles.md#policy-and-profile-manager) role, or the *device configurations* permissions that are built-in to the role, you now have read-only access to device enrollment limit policies. To create and edit these policies, you must be an Intune Administrator.

### Device management

#### Cross Platform Device Inventory<!-- 25964936 -->

Android, iOS, and Mac devices are added to device inventory. Intune now collects a default set of inventory data including 74 Apple properties and 32 Android properties.

For more information, see [View device details with Microsoft Intune](../../device-management/inventory-and-status/device-details.md).

#### Enhanced security during unattended Remote Help sessions on Android devices<!--25977108 -->

During an unattended Remote Help sessions on Android devices, the screen of the device is blocked and users are notified if they interact with it. This feature enhances the security and user awareness during remote assistance.

This feature is for Zebra and Samsung devices that enrolled as Android Enterprise corporate owned dedicated devices.

For more information on Remote Help, see [Remote Help](../../remote-help/index.md).

### Device security

#### Detect rooted corporate-owned Android Enterprise devices<!--31672848 -->

Configure compliance policies to detect if a corporate-owned Android Enterprise device is rooted. If Microsoft Intune detects that a device is rooted, you can mark it as noncompliant. This feature is now available for devices enrolled as fully managed, dedicated, or corporate-owned with a work profile. For more information, see [Device compliance settings for Android Enterprise in Intune](../../device-security/compliance/ref-android-enterprise-settings.md).

To learn about root detection support for Microsoft Defender on Android, see Key capabilities in [Microsoft Defender for Endpoint](/defender-endpoint/mtd) in the Defender documentation, and the Defender for Endpoint blog [Native root detection support for Microsoft Defender on Android](https://techcommunity.microsoft.com/blog/microsoftdefenderatpblog/native-root-detection-support-for-microsoft-defender-on-android/4461576).

> [!div class="checklist"]
> Applies to:
>
> - Android

#### New endpoint security profile for configuring Endpoint detection and response and Antivirus exclusion settings on Linux devices <!-- 26549863 -->

As part of the Intune scenario for [Microsoft Defender for Endpoint security settings management](../../device-security/microsoft-defender/security-settings-management.md), you can use a new *Endpoint detection and response* profile for Linux named [**Microsoft Defender Global Exclusions (AV+EDR)**](../../device-configuration/endpoint-security/deploy-edr.md#create-a-linux-global-exclusions-policy) that you can now use to manage Linux device exclusions for both Microsoft Defender *Endpoint detection and response* (EDR) and *Antivirus* (AV).

This profile supports settings related to global exclusion settings as detailed in [Configure and validate exclusions on Linux](/defender-endpoint/linux-exclusions) in the Microsoft Defender documentation. These exclusion configurations can apply to both the antivirus and EDR engines on the Linux client to stop associated real time protection EDR alerts for excluded items. Exclusions can be defined by the file path, folder, or process explicitly defined by the admin in the policy.

The new Intune profile:

- Is available in addition to the existing endpoint security Antivirus policy for Microsoft Defender Antivirus.
- Is supported for devices you manage through the [Microsoft Defender for Endpoint security settings management](../../device-security/microsoft-defender/security-settings-management.md) scenario.
- Isn't supported for Linux devices managed directly by Intune.

For details about the available Defender settings, see [Configure security settings in Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint](/defender-endpoint/linux-preferences) in the Defender for Endpoint documentation.

> [!div class="checklist"]
> Applies to:
>
> - Linux

### Tenant administration

#### Data collection from SimInfo entity on Windows devices<!--30120558 -->

You can now collect data from the SimInfo entity on Windows devices with enhanced device inventory.
For more information, see [Intune Data Platform](../../advanced-analytics/ref-data-platform-schema.md).

> [!div class="checklist"]
> Applies to:
>
> - Windows

## Week of April 28, 2025

### App management

#### Intune support for Apple specialty devices<!-- 32486291 -->

App protection policies (APP) support Microsoft Edge (v136 or later), OneDrive (v16.8.4 or later), and Outlook (v4.2513.0 or later). To enable this setting for these specific apps on visionOS devices, you must set `com.microsoft.intune.mam.visionOSAllowiPadCompatApps` to `Enabled` in your app configuration policy. Once you assign your app configuration policy, you can create and assign your app protection policy for your VisionOS devices. For more information, see [Protect data on VisionOS devices](../../app-management/configuration/configure-managed-apps.md#protect-data-on-visionos-devices).

### Tenant administration

#### New icon for Microsoft Intune<!-- 29148691 -->

Microsoft Intune has a new icon. The Intune icon is being updated across platforms and apps associated with Intune, such as the Intune admin center and Intune Company Portal app. The new icon will gradually be implemented over the next few months.

## Week of April 21, 2025

### Microsoft Intune Suite

#### Endpoint Privilege Management elevation rule support for file arguments and parameters<!-- 28077130 -->

File elevation rules for Endpoint Privilege Management (EPM) now support [command line file arguments](../../epm/create-elevation-rules.md#use-file-arguments-for-elevation-rules). When an elevation rule is configured to define one or more file arguments, EPM allows that file to run in an elevated request only when one of the defined arguments is used. EPM blocks elevation of the file should a command line argument be used that isn't defined by the elevation rule. Use of file arguments in your file elevation rules can help you refine how and for what intent different files are successfully run in an elevated context by Endpoint Privilege Management.

EPM is available as an [Intune Suite add-on-capability](../../fundamentals/add-ons.md).

### App management

#### Relationship viewer available for Intune apps<!-- 17644546 -->

The relationship viewer provides a graphical depiction of the relationships between different applications in the system, including superseding and dependent applications. Admins can find relationship viewer in Intune by selecting **Apps** > **All apps** > *a Win32 app* > **Relationship viewer**. The relationship viewer supports both Win32 apps and Enterprise App Catalog apps. For more information, see [App relationship viewer](../../app-management/deployment/win32.md#app-relationship-viewer).

#### Apple VPP using new API v2.0<!-- 29567109 -->

Apple recently updated the API for their volume purchase program (VPP), which is used to manage apps and books. Apple's related API is now version 2.0. Version 1.0 is deprecated. To support the Apple updates, Microsoft Intune uses the new API, which is faster and more scalable than the previous version.

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

#### More org data storage service options for Android and iOS apps<!-- 29606862 -->

Intune now provides more storage services options when saving copies of org data using an app protection policy for Android or iOS. In addition to the existing org data storage options, you can also select **iManage** and **Egnyte** as storage options. You must select these services as exemptions from your block list by setting **Save copies of org data** to **Block**, then selecting the allowed storage services next to the **Allow user to save copies to selected services** setting. This setting doesn't apply to all applications.

For more information about data protection using app protection policies, see [iOS app protection policy settings - Data protection](../../app-management/protection/ref-settings-ios.md#data-protection) and [Android app protection policy settings - Data protection](../../app-management/protection/ref-settings-android.md#data-protection).

> [!div class="checklist"]
> Applies to:
>
> - iOS

### Device configuration

#### Updated device configuration template for Windows Delivery Optimization<!-- 32411831 -->

The device configuration template for Windows [Delivery Optimization](../../device-configuration/templates/configure-delivery-optimization-windows.md) is updated. The new template uses the settings format in the Settings Catalog. Settings are taken directly from the Windows Configuration Service Providers (CSPs) for Windows Delivery Optimization, as documented by Windows at [Policy CSP – DeliveryOptimization](/windows/client-management/mdm/policy-csp-DeliveryOptimization).

With this change, you can no longer create new versions of the old profile. However, your preexisting instances of the old profile remain available to use.

For more information about this change, see the Intune Customer Success blog at [Support tip: Windows device configuration policies migrating to unified settings platform in Intune](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-windows-device-configuration-policies-migrating-to-unified-settings-/4189665).

> [!div class="checklist"]
> Applies to:
>
> - Windows 10
> - Windows 11

#### New settings available in the Apple settings catalog<!-- 31523569 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

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
To get started with settings catalog, see [Use the settings catalog to configure settings on your devices](../../device-configuration/settings-catalog/index.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise
> - AOSP

### Device enrollment

#### Custom device naming template for Android Enterprise corporate-owned devices<!-- 3465701 -->

You can use a custom template for naming Android Enterprise corporate-owned devices when they enroll with Intune. The template is available to configure in the enrollment profile. It can contain a combination of custom text and predefined variables (like device serial number, device type), and for user-affiliated devices, the owner's username. For more information, see:

 - [Android Enterprise corporate-owned devices with work profile](../../device-enrollment/android/setup-corporate-work-profile.md#create-an-enrollment-profile)
 - [Android Enterprise dedicated devices](../../device-enrollment/android/setup-dedicated.md#create-an-enrollment-profile)
 - [Android Enterprise fully managed devices](../../device-enrollment/android/setup-fully-managed.md#step-2-create-new-enrollment-profile)

> [!div class="checklist"]
> Applies to:
>
> - Android

#### Enrollment-time grouping for Android Enterprise corporate devices <!-- 17530981 -->

Now available for Android Enterprise corporate-owned devices, *enrollment time grouping* enables you to assign a static Microsoft Entra group to devices at enrollment time. When a targeted Android device enrolls, it receives all assigned policies, apps, and settings, typically by the time the user lands on the home screen. You can configure one static Microsoft Entra group per enrollment profile under the **Device group** tab in the Microsoft Intune admin center. For more information, see [Enrollment time grouping](../../device-enrollment/setup-time-grouping.md).

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
[**Lanman Server**](../../device-security/security-baselines/ref-windows-mdm-settings.md?pivots=mdm-24h2#lanman-server)
- [Audit Client Does Not Support Encryption](/windows/client-management/mdm/policy-csp-lanmanserver#auditclientdoesnotsupportencryption) – Baseline default: *Enabled*
- [Audit Client Does Not Support Signing](/windows/client-management/mdm/policy-csp-lanmanserver#auditclientdoesnotsupportsigning) – Baseline default: *Enabled*
- [Audit Insecure Guest Logon](/windows/client-management/mdm/policy-csp-lanmanserver#auditinsecureguestlogon) – Baseline default: *Enabled*
- [Auth Rate Limiter Delay In Ms](/windows/client-management/mdm/policy-csp-lanmanserver#authratelimiterdelayinms) – Baseline default: *2000*
- [Enable Auth Rate Limiter](/windows/client-management/mdm/policy-csp-lanmanserver#enableauthratelimiter) – Baseline default: *Enabled*
- [Max SMB 2 Dialect](/windows/client-management/mdm/policy-csp-lanmanserver#maxsmb2dialect) – Baseline default: *SMB 3.1.1*
- [Min SMB 2 Dialect](/windows/client-management/mdm/policy-csp-lanmanserver#minsmb2dialect) – Baseline default: *SMB 3.0.0*
- [Enable Mailslots](/windows/client-management/mdm/policy-csp-lanmanserver#enablemailslots) - Baseline default: *Disabled*

[**Lanman Workstation**](../../device-security/security-baselines/ref-windows-mdm-settings.md?pivots=mdm-24h2#lanman-workstation)
- [Audit Insecure Guest Logon](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#auditinsecureguestlogon) – Baseline default: *Enabled*
- [Audit Server Does Not Support Encryption](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#auditserverdoesnotsupportencryption) – Baseline default: *Enabled*
- [Audit Server Does Not Support Signing](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#auditserverdoesnotsupportsigning) – Baseline default: *Enabled*
- [Max SMB 2 Dialect](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#maxsmb2dialect) – Baseline default: *SMB 3.1.1*
- [Min SMB 2 Dialect](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#minsmb2dialect) – Baseline default: *SMB 3.0.0*
- [Require Encryption](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#requireencryption) – Baseline default: *Disabled*
- [Enable Mailslots](/windows/client-management/mdm/policy-csp-LanmanWorkstation#enablemailslots) - Baseline default: *Disabled*

For more information, see [Intune security baselines](../../device-security/security-baselines/overview.md).

### Intune apps

#### Newly available protected apps for Intune<!-- 31436626, 31437166, 31494251 -->

The following protected apps are now available for Microsoft Intune:

- FileOrbis for Intune by FileOrbis FZ LLC
- PagerDuty for Intune by PagerDuty, Inc.
- Outreach.io by Outreach Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

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

The [Microsoft Tunnel readiness tool](../../device-security/microsoft-tunnel/prerequisites.md#run-the-readiness-tool) now includes a check for the **auditd** package for Linux System Auditing (LSA). The presence of *auditd* is optional and not a required prerequisite by Microsoft Tunnel for the Linux server.

When the mst-readiness tool runs, it now raises a non-blocking warning if the audit package isn't installed. By default, Red Hat Enterprise Linux versions 7 and later install this package by default. Ubuntu versions of Linux currently require this optional package to be installed.

For more information on *auditd* and how to install it on your Microsoft Tunnel server, see [Linux system auditing](../../device-security/microsoft-tunnel/prerequisites.md#linux-system-auditing).

## Week of March 17, 2025 (Service release 2503)

### Microsoft Intune Suite

#### Endpoint Privilege Management supports ARM 64-bit devices<!-- 28313554 -->

[Endpoint Protection Manager](../../epm/overview.md) (EPM) now supports managing file elevations on devices that run on ARM 64-bit architecture.

> [!div class="checklist"]
> Applies to:
>
> - Windows

### Device configuration

#### New settings available in the Apple settings catalog <!-- 31056047 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

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

Intune policies for [Windows Local Administrator Password Solution (LAPS)](../../device-security/laps/overview.md) now include several new settings and updates to two previously available settings. [LAPS](/windows-server/identity/laps/laps-overview) is a built-in Windows solution and can help you secure the built-in local administrator account that's present on each Windows device. All the settings that you can manage through Intune LAPS policy are described in the Windows [LAPS CSP](/windows/client-management/mdm/LAPS-csp).

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

> [!div class="checklist"]
> Applies to:
>
> - Windows

#### Configure devices to stay on the latest OS version using declarative device management (DDM)<!-- 28323647 -->

As part of the [Settings Catalog](../../device-configuration/settings-catalog/index.md), you can now configure devices to automatically update to the latest OS version using DDM. To use these new settings in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS**for platform > **Settings catalog** for profile type.

**Declarative device management > Software Update Enforce Latest**.

- **Enforce Latest Software Update Version**: If true, devices upgrade to the latest OS version that's available for that device model. This feature uses the Software Update Enforcement configuration and forces devices to restart and install the update after the deadline passes.
- **Delay In Days**: Specify the number of days that should pass before a deadline is enforced. This delay is based on either the posting date of the new update when released by Apple, or when the policy is configured.
- **Install Time**: Specify the local device time for when updates are enforced. This setting uses the 24-hour clock format where midnight is 00:00 and 11:59pm is 23:59. Ensure that you include the leading 0 on single digit hours. For example, 01:00, 02:00, 03:00.

Learn more about configuring managed updates through DDM at [Managed software updates](/intune/intune-service/protect/updates/apple).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

#### Remote Help supports Azure Virtual Desktop muti-session<!-- 24590822 -->

Remote Help now provides support for multi-session AVD with several users on a single virtual machine. Earlier, Remote Help was supporting Azure Virtual Desktop (AVD) sessions with one user on one virtual machine (VM).

For more information, see:

- [Remote Help](../../remote-help/index.md)
- [Remote Help on windows](../../remote-help/index.md)
- [Using Azure Virtual Desktop multi-session with Microsoft Intune](../../solutions/azure-virtual-desktop-multi-session.md)

#### Copilot assistant for device query<!-- 26933762 -->

You can now use Copilot to generate a KQL query to help you get data from across multiple devices in Intune. This capability is available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Device query** > **Query with Copilot**. For more information, see [Query with Copilot in device query](../../copilot/index.md#-use-copilot-to-create-kql-queries-to-get-device-details).

### Intune apps

#### Newly available protected apps for Intune<!-- 31070614, 31093579, 31093668, 31187306 -->

The following protected apps are now available for Microsoft Intune:

- FacilyLife by Apleona GmbH (iOS)
- Intapp 2.0 by Intapp, Inc. (Android)
- DealCloud by Intapp, Inc. (Android)
- Lemur Pro for Intune by Critigen LLC (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

## Week of March 03, 2025

### Monitor and troubleshoot

#### Updates to the Feature updates report<!--31305861 -->

We're introducing a new **Update Substate** in service-side data. This substate is displayed in the reports for devices that are invalid in Microsoft Entra and is known as **Not supported**.

For more information, see [Use Windows Update for Business reports](../../device-updates/windows/monitor-feature-updates.md)

## Week of February 24, 2025 (Service release 2502)

### App management

#### VPP token name more easily available in Apps workload<!-- 5479088 -->

The **VPP token name** column, available in the Apps workload, allows you to quickly determine the token and app association. This column is now available in the **All apps** list (**Apps** > **All apps**) and the app selection pane for **App configuration policies** (**Apps** > **App configuration policies**). For more information about VPP apps, see [Manage volume-purchased apps and books with Microsoft Intune](../../app-management/deployment/manage-volume-purchased.md).

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

The Intune Connector for Active Directory now uses a low privileged account, which helps increase the security of your environment. The old connector continues to work until deprecation in late May 2025.

For more information, see [Deploy Microsoft Entra hybrid joined devices by using Intune and Windows Autopilot](/autopilot/windows-autopilot-hybrid).

#### Managed Home Screen QR Code Authentication in public preview<!-- 25348926 -->

Managed Home Screen for Android devices natively supports QR Code Authentication in Microsoft Entra ID. Authentication involves both a QR code and PIN. This capability eliminates the need for users to enter and re-enter long UPNs and alphanumeric passwords. For more information, see [Sign in to Microsoft Teams or Managed Home Screen (MHS) with QR code](/entra/identity/authentication/how-to-authentication-qr-code#sign-in-to-microsoft-teams-or-managed-home-screen-mhs-with-qr-code).

Applies to:

- Android devices

#### More device details for Managed Home Screen<!-- 27006536 -->

Android **OS version**, **Security patch**, and **Last device reboot time** details are now available from the **Device Information** page of the Managed Home Screen app. For related information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../app-management/configuration/configure-managed-home-screen.md).

Applies to:

- Android Enterprise devices

#### Display ringtone selector for Managed Home Screen<!-- 26826233 -->

In Intune, you can choose to expose a setting in the Managed Home Screen app to allow users to select a ringtone. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../app-management/configuration/configure-managed-home-screen.md).

Applies to:

- Android devices

### Device security

#### Manage the DeviceControlEnabled configuration for Microsoft Defender Device Control on Windows devices<!-- 31171641 -->

You can now use Intune to manage the configuration of the Microsoft Defender CSP for [DeviceControlEnabled](/windows/client-management/mdm/defender-csp#configurationdevicecontrolenabled) for Device Control. DeviceControlEnabled is used to enable or disable support for the Microsoft Defender Device Control feature on Windows devices.

You can use the following two Microsoft Intune options to configure DeviceControlEnabled. With both options, the setting appears as **Device Control Enabled**, and is found in the *Defender* category:

- Configure a [**Device Control** template](../../device-configuration/endpoint-security/manage-policies.md#create-endpoint-security-policies), which is a profile for [Attack Surface Reduction](../../device-configuration/endpoint-security/attack-surface-reduction.md) policy.
- Configure a [**Settings Catalog** profile](../../device-configuration/settings-catalog/index.md#create-the-policy) for Windows.

Both the Device Control template and Settings Catalog support the following options for *Device Control Enabled*:

- Device Control is enabled
- Device Control is disabled (Default)

Applies to:

- Windows

#### Manage the DefaultEnforcement configuration for Microsoft Defender Device Control on Windows devices<!-- 30253799 -->

You can now use Intune to manage the configuration of the Microsoft Defender CSP for [DefaultEnforcement](/windows/client-management/mdm/defender-csp#configurationdefaultenforcement) for Device Control.

DefaultEnforcement manages the configuration of Device Control:

- On devices that don't receive Device Control policies
- For devices that receive and evaluate a policy for Device Control when no rules in the policy are matched

You can use the following two Microsoft Intune options to configure DefaultEnforcement. With both options, the setting appears as **Default Enforcement**, and is found in the *Defender* category:

- Configure a [**Device Control** template](../../device-configuration/endpoint-security/manage-policies.md#create-endpoint-security-policies), which is a profile for [Attack Surface Reduction](../../device-configuration/endpoint-security/attack-surface-reduction.md) policy.
- Configure a [**Settings Catalog** profile](../../device-configuration/settings-catalog/index.md#create-the-policy) for Windows.

Both the Device Control template and Settings Catalog support the following options for *Default Enforcement*:

- Default Allow Enforcement (Default)
- Default Deny Enforcement

Applies to:

- Windows

### Intune apps

#### Newly available protected app for Intune<!-- 30508606 -->

The following protected app is now available for Microsoft Intune:

- Applications Manager - Intune by ManageEngine

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

### Device configuration

#### New settings available in the Apple settings catalog<!-- 30457000 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

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

You can now deploy the Intune security baseline for **Windows version 24H2** to your Windows 10 and Windows 11 devices. The new baseline version uses the unified settings platform seen in the Settings Catalog. This change features an improved user interface and reporting experience, more consist and accurate improvements with setting tattooing, and supports profile assignment filters.

Use of [Intune security baselines](../../device-security/security-baselines/overview.md) can help you maintain best-practice configurations for your Windows devices. It can also help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline represents the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows

### Monitor and troubleshoot

#### Device Query for Multiple Devices<!--25234456 -->

Device query for multiple devices is available. This feature allows you to gain comprehensive insights about your entire fleet of devices using Kusto Query Language (KQL) to query across collected inventory data for your devices.

Device query for multiple devices is now supported for devices running Windows 10 or later. This feature is now included as part of Advanced Analytics.

Applies to:

- Windows

## Week of February 5, 2025 (Service release 2501)

### Microsoft Intune Suite

#### Use Microsoft Security Copilot with Endpoint Privilege Management to help identify potential elevation risks<!-- 27265509 -->

When your Azure Tenant is licensed for Microsoft Security Copilot, you can now use Security Copilot to help you investigate Endpoint Privilege Management (EPM) file elevation requests from within the EPM [support approved](../../epm/manage-support-approvals.md#use-microsoft-security-copilot-to-analyze-file-elevation-requests) work flow.

With this capability, while reviewing the properties of a file elevation request, you see the **Analyze with Copilot** option. This option directs Security Copilot to use the files hash in a prompt Microsoft Defender Threat Intelligence to evaluate the file for potential indicators of compromise. You can then make a more informed decision to either approve or deny that file elevation request. Some of the results that are returned to your current view in the admin center include:

- The files' reputation
- Information about the trust of the publisher
- The risk score for the user requesting the file elevation
- The risk score of the device from which the elevation was submitted

EPM is available as an [Intune Suite add-on-capability](../../fundamentals/add-ons.md). To learn more about how you can currently use Copilot in Intune, see [Microsoft Copilot in Intune](../../copilot/index.md).

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

[View the default configuration of settings in the updated baseline](../../device-security/security-baselines/ref-v2-edge-settings.md?pivots=edge-v128).

For information about security baselines with Intune, see [Use security baselines to configure Windows devices in Intune](../../device-security/security-baselines/overview.md).

Applies to:

- Windows

### Intune apps

#### Newly available protected app for Intune<!-- 30061339 -->

The following protected app is now available for Microsoft Intune:

- MoveInSync by MoveInSync Technologies

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

Applies to:

- Windows 10 and later (Corporate owned devices managed by Intune)

## Week of January 27, 2025

### Device security

#### Security baselines for HoloLens 2<!-- 24914095 -->

You can now deploy two distinct instances of the security baseline for HoloLens 2. These baselines represent Microsoft's best practice guidelines and experience from deploying and supporting HoloLens 2 devices to customers across various industries. The two baselines instances:

- **Standard Security Baseline for HoloLens 2**:
  The standard security baseline for HoloLens 2 represents the recommendations for configuring security settings that are applicable to all types of customers irrespective of HoloLens 2 use case scenarios. [View the default configuration of settings in the standard security baseline](../../device-security/security-baselines/ref-hololens2-standard-settings.md).

- **Advanced Security Baseline for HoloLens 2**:
  The advanced security baseline for HoloLens 2 represents the recommendations for configuring security settings for the customers who have strict security controls of their environment and require stringent security policies to be applied to any device used in their environment. [View the default configuration of settings in the advanced security baseline](../../device-security/security-baselines/ref-hololens2-advanced-settings.md).

To learn more about security baselines with Intune, see [Use security baselines to configure Windows devices in Intune](../../device-security/security-baselines/overview.md).

Applies to:

- Windows

## Week of January 20, 2025

### Monitor and troubleshoot

#### Use Support Assistant to resolve issues<!-- 29084113 -->

Support Assistant is now available in Intune. It leverages AI to enhance your help and support experience, ensuring more efficient issue resolution. Support Assistant is available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshoot + support** > **Help and Support**, or by selecting the question mark near your profile pic. Currently, the Support Assistant is in preview. You can enable and disable Support Assistant by choosing to opt in and opt out at any time. For related information, see [How to get support in the Microsoft Intune admin center](../../fundamentals/it-pro-support/get-support-admin-center.md).

## Week of December 30, 2024

### Device enrollment

#### Intune ends support for Android device administrator on devices with access to Google Mobile Services<!-- 24563742 -->
As of December 31, 2024, Microsoft Intune no longer supports Android device administrator management on devices with access to Google Mobile Services (GMS). This change comes after Google deprecated Android device administrator management and ceased support. Intune support and help documentation remains for devices without access to GMS running Android 15 or earlier, and Microsoft Teams devices migrating to Android Open Source Project (AOSP) management. For more information about how this change impacts your tenant, see [Intune ending support for Android device administrator on devices with GMS access in December 2024](https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-ending-support-for-android-device-administrator-on-devices-with-gms-in-de/3915443).


## Week of December 16, 2024 (Service release 2412)

### App management

#### Increased scale for Customization policies<!-- 25308499 -->

You can now create up to 25 policies that customize the Company Portal and Intune app experience. The previous maximum number of Customization policies was 10. Navigate to the Intune admin center, and select **Tenant administration** > **Customization**.

For more information about customizing the Company Portal and Intune apps, see [Customizing the user experience](../../app-management/configuration/configure-company-portal.md#customizing-the-user-experience).

### Device security

#### Support for tamper protection in policies for Security settings management for Microsoft Defender for Endpoint<!-- 13204113 -->

You can now manage the Microsoft Defender for Endpoint CSP setting for [tamper protection](/windows/client-management/mdm/defender-csp) on unenrolled devices you manage as part of the [Defender for Endpoint security settings management](../../device-security/microsoft-defender/security-settings-management.md#which-solution-should-i-use) scenario.

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

For more information, see [Use ADMX templates on Windows devices in Microsoft Intune](../../device-configuration/settings-catalog/configure-admx-templates-windows.md).

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

For more information, see [Wi-Fi settings for personally-owned work profile devices.](../../device-configuration/templates/ref-wifi-settings-android-enterprise.md).

Applies to:

- Android Enterprise

## Week of December 9, 2024

### Tenant administration

#### Intune now supports Ubuntu 24.04 LTS for Linux management.<!--28363586 -->

We're now supporting device management for Ubuntu 24.04 LTS. You can enroll and manage Linux devices running Ubuntu 24.04, and assign standard compliance policies, custom configuration scripts, and compliance scripts.

For more information, see the following in Intune documentation:

- [Deployment guide: Manage Linux devices in Microsoft Intune](../../fundamentals/platform-guide-linux.md)
- [Enrollment guide: Enroll Linux desktop devices in Microsoft Intune](../../device-enrollment/guide-linux.md). To enroll Linux devices, ensure that they're running Ubuntu 20.04 LTS or higher.

Applies to:

- Linux Ubuntu Desktops

## Week of December 2, 2024

### Device enrollment

#### Change to enrollment behavior for iOS enrollment profile type<!-- 29068674 -->

At Apple WWDC 2024, Apple ended support for profile-based Apple user enrollment. For more information, see [Support has ended for profile-based user enrollment with Company Portal](./index.md#support-has-ended-for-apple-profile-based-user-enrollment-with-company-portal). As a result of this change, we updated the behavior that occurs when you select **Determine based on user choice** as the enrollment profile type for bring-your-own-device (BYOD) enrollments.

Now when users select **I own this device** during a BYOD enrollment, Microsoft Intune enrolls them via account-driven user enrollment, rather than profile-based user enrollment, and then secures only work-related apps. Less than one percent of Apple devices across all Intune tenants are currently enrolled this way, so this change doesn't affect most enrolled devices. There is no change for iOS users who select **My company owns this device** during a BYOD enrollment. Intune enrolls them via device enrollment with Intune Company Portal, and then secures their entire device.

If you currently allow users in BYOD scenarios to determine their enrollment profile type, you must take action to ensure account-driven user enrollment works by completing all prerequisites. For more information, see [Set up account driven Apple user enrollment](../../device-enrollment/apple/setup-account-driven-user.md). If you don't give users the option to choose their enrollment profile type, there are no action items.

### Device management

#### Device Inventory for Windows<!-- 24853010 -->

Device inventory lets you collect and view additional hardware properties from your managed devices to help you better understand the state of your devices and make business decisions.

You can now choose what you want to collect from your devices, using the catalog of properties and then view the collected properties in the Resource Explorer view.

For more information, see:

- [Properties catalog](../../device-configuration/collect-device-properties.md)
- [Data collection platform](../../advanced-analytics/ref-data-platform-schema.md)

## Week of November 18, 2024 (Service release 2411)

### App management

#### Configuration values for specific managed applications on Intune enrolled iOS devices<!-- 30293382 -->

Starting with Intune's September (2409) service release, the **IntuneMAMUPN**, **IntuneMAMOID**, and **IntuneMAMDeviceID** app configuration values are automatically sent to managed applications on Intune enrolled iOS devices for the following apps:

- Microsoft Excel
- Microsoft Outlook
- Microsoft PowerPoint
- Microsoft Teams
- Microsoft Word

For more information, see Intune [Support tip: Intune MAM users on iOS/iPadOS userless devices may be blocked in rare cases](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-intune-mam-users-on-iosipados-userless-devices-may-be-blocked-in-rar/4254335).

#### Additional installation error reporting for LOB apps on AOSP devices<!-- 27157460 -->

Additional details are now provided for app installation reporting of Line of Business (LOB) apps on Android Open Source Project (AOSP) devices. You can view installation error codes and detailed error messages for LOB apps in Intune.

For information about app installation error details, see [Monitor app information and assignments with Microsoft Intune](../../app-management/monitor-assignments.md#app-installation-error-reporting).

Applies to:

- Android Open Source Project (AOSP) devices

#### Microsoft Teams app protection on VisionOS devices (preview)<!-- 29913431 -->

Microsoft Intune app protection policies (APP) are now supported on the Microsoft Teams app on VisionOS devices.

To learn more about how to target policies to VisionOS devices, see [Managed app properties](../../fundamentals/filters/ref-device-properties.md#available-properties) for more information about filters for managed app properties.

Applies to:

- Microsoft Teams for iOS on VisionOS devices

## Week of October 28, 2024

### Device security

#### Defender for Endpoint security settings support in government cloud environments (generally available)<!-- 30064299 -->

Now generally available, customer tenants in the Government Community Cloud (GCC), US Government Community High (GCC High), and Department of Defense (DoD) environments can use Intune to manage the Defender security settings on the devices you've onboarded to Defender without enrolling those devices with Intune. Previously, support for Defender security settings was in public preview.

This capability is known as [Defender for Endpoint security settings management](../../device-security/microsoft-defender/security-settings-management.md).

## Week of October 14, 2024 (Service release 2410)

### App management

#### Updates to app configuration policies for Android Enterprise devices<!-- 26711672 -->

App configuration policies for Android Enterprise devices now support overriding the following permissions:

- Access background location
- Bluetooth (connect)

For more information about app configuration policies for Android Enterprise devices, see [Add app configuration policies for managed Android Enterprise devices](../../app-management/configuration/configure-managed-android.md).

Applies to:

- Android Enterprise devices

### Device configuration

#### Windows Autopilot device preparation support in Intune operated by 21Vianet in China<!-- MAXADO-9313795 / INADO-28687730 -->

Intune now supports *Windows Autopilot device preparation* policy for [Intune operated by 21Vianet in China](../../fundamentals/china.md) cloud. Customers with tenants located in China can now use *Windows Autopilot device preparation* with Intune to provision devices.

For information about this Windows Autopilot device preparation support, see the following in the Windows Autopilot device preparation documentation:

- Overview: [Overview of Windows Autopilot device preparation](/autopilot/device-preparation/overview)
- Tutorial: [Windows Autopilot device preparation scenarios](/autopilot/device-preparation/tutorial/scenarios)

### Device management

#### Minimum OS version for Android devices is Android 10 and later for user-based management methods<!-- 14755802 -->

Beginning in October 2024, Android 10 and later is the [minimum Android OS version that is supported for user-based management methods](../../fundamentals/ref-supported-platforms.md#android), which includes:

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

Intune now collects additional files and registry keys to assist in troubleshooting the [Device Hardware Inventory](../../device-management/actions/collect-diagnostics.md) feature.

Applies to:

- Windows

## Week of October 7, 2024

### App management

#### New UI for Intune Company Portal app for Windows<!-- 27219294 -->

The UI for the Intune Company Portal app for Windows is updated. Users now see an improved experience for their desktop app without changing the functionality they've used in the past. Specific UI improvements are focused on the **Home**, **Devices**, and **Downloads & updates** pages. The new design is more intuitive and highlights areas where users need to take action.

For more information, see [New look for Intune Company Portal app for Windows](https://techcommunity.microsoft.com/t5/intune-customer-success/new-look-for-intune-company-portal-app-for-windows/ba-p/4158755). For end user details, see [Install and share apps on your device](../../user-help/apps/install-apps-windows.md).

### Device security

#### New strong mapping requirements for SCEP certificates authenticating with KDC<!-- 29005591 -->

The Key Distribution Center (KDC) requires user or device objects to be strongly mapped to Active Directory for certificate-based authentication. This means that a Simple Certificate Enrollment Protocol (SCEP) certificate's subject alternative name (SAN) must have a security identifier (SID) extension that maps to the user or device SID in Active Directory. The mapping requirement protects against certificate spoofing and ensures that certificate-based authentication against the KDC continues working.

To meet requirements, modify or create a SCEP certificate profile in Microsoft Intune. Then add a `URI` attribute and the `OnPremisesSecurityIdentifier` variable to the SAN. After you do that, Microsoft Intune appends a tag with the SID extension to the SAN and issues new certificates to targeted users and devices. If the user or device has a SID on premises that's synced to Microsoft Entra ID, the certificate shows the SID. If they don't have a SID, a new certificate is issued without the SID.

For more information and steps, see [Update certificate connector: Strong mapping requirements for KB5014754](../../device-configuration/certificates/scep-profiles.md).

Applies to:

- Windows, iOS/iPadOS, and macOS user certificates
- Windows device certificates

This requirement isn't applicable to device certificates used with Microsoft Entra joined users or devices, because the SID attribute is an on-premises identifier.

#### Defender for Endpoint security settings support in government cloud environments (public preview)<!-- 24191406 -->

In public preview, customer tenants in US Government Community (GCC) High, and Department of Defense (DoD) environments can now use Intune to manage the Defender security settings on the devices that onboarded to Defender without enrolling those devices with Intune. This capability is known as [Defender for Endpoint security settings management](../../device-security/microsoft-defender/security-settings-management.md).

For more information about the Intune features supported in GCC High and DoD environments, see [Intune US Government service description](../../fundamentals/government-service.md).

## Week of September 30, 2024

### Device security

#### Updates to PKCS certificate issuance process in Microsoft Intune Certificate Connector, version 6.2406.0.1001 <!-- 24186560 -->

We updated the process for Public Key Cryptography Standards (PKCS) certificate issuance in Microsoft Intune to support the security identifiers (SID) information requirements described in [KB5014754](https://support.microsoft.com/topic/kb5014754-certificate-based-authentication-changes-on-windows-domain-controllers-ad2c23b0-15d8-4340-a468-4d4f3b188f16). As part of this update, an OID attribute containing the user or device SID is added to the certificate. This change is available with the Certificate Connector for Microsoft Intune, version 6.2406.0.1001, and applies to users and devices synced from Active Directory on-premises to Microsoft Entra ID.

The SID update is available for user certificates across all platforms, and for device certificates specifically on Microsoft Entra hybrid joined Windows devices.

For more information, see:

- [What's new for the certificate connector](../../fundamentals/certificates/connector/overview.md#september-19-2024)

- [Apply PFX changes to certificate](../../device-configuration/certificates/pkcs-profiles.md)

## Week of September 23, 2024 (Service release 2409)

### App management

#### Working Time settings for app protection policies<!-- 14631539 -->

Working time settings allow you to enforce policies that limit access to apps and mute message notifications received from apps during non-working time. The limit access setting is now available for the Microsoft Teams and Microsoft Edge apps. You can limit access by using App Protection Policies (APP) to block or warn end users from using the iOS/iPadOS or Android Teams and Microsoft Edge apps during non-working time by setting the **Non-working time** conditional launch setting. Also, you can create a non-working time policy to mute notifications from the Teams app to end users during non-working time.

For more information, see:

- [Android app protection policy settings](../../app-management/protection/ref-settings-android.md#conditional-launch)
- [iOS app protection policy settings](../../app-management/protection/ref-settings-ios.md#conditional-launch)
- [Quiet time policies for iOS/iPadOS and Android apps](../../app-management/protection/configure-quiet-time.md#quiet-time-policy-types)

Applies to:

- Android
- iOS/iPadOS

#### Streamlined app creation experience for apps from Enterprise App Catalog<!-- 29411991 -->

We've streamlined the way apps from [Enterprise App Catalog](../../app-management/deployment/add-enterprise-catalog-app.md) are added to Intune. We now provide a direct app link rather than duplicating the app binaries and metadata. App contents now download from a `*.manage.microsoft.com` subdomain. This update helps to improve the latency when adding an app to Intune. When you add an app from Enterprise App Catalog, it syncs immediately and is ready for additional action from within Intune.

#### Update Enterprise App Catalog apps<!-- 24875279 -->

Enterprise App Management is enhanced to allow you to update an **Enterprise App Catalog** app. This capability guides you through a wizard that allows you to add a new application and use supersedence to update the previous application.

For more information, see [Guided update supersedence for Enterprise App Management](../../app-management/deployment/update-enterprise-supersedence.md).

### Device configuration

#### Samsung ended support for multiple Android device administrator (DA) settings <!-- 24990472 -->

On Android device administrator managed (DA) devices, Samsung has deprecated many [Samsung Knox APIs](https://docs.samsungknox.com/dev/knox-sdk/api-reference/deprecated-api-methods/) (opens Samsung's web site) configuration settings.

In Intune, this deprecation impacts the following device restrictions settings, compliance settings, and trusted certificate profiles:

- [Device restriction settings for Android in Microsoft Intune](../../device-configuration/templates/ref-device-restrictions-android.md)
- [View the Android device administrator compliance settings for Microsoft Intune compliance policies](../../device-security/compliance/ref-android-administrator-settings.md)
- [Create trusted certificate profiles in Microsoft Intune](../../device-configuration/certificates/trusted-root-profiles.md#trusted-certificate-profiles-for-android-device-administrator)

In the Intune admin center, when you create or update a profile with these settings, the impacted settings are noted.

Though the functionality might continue to work, there's no guarantee that it will continue working for any or all Android DA versions supported by Intune. For more information on Samsung support for deprecated APIs, see [What kind of support is offered after an API is deprecated?](https://docs.samsungknox.com/dev/knox-sdk/faqs/general/deprecated-api-support-change.htm) (opens Samsung's web site).

Instead, you can manage Android devices with Intune using one of the following Android Enterprise options:

- [Set up enrollment of Android Enterprise personally owned work profile devices](../../device-enrollment/android/setup-personal-work-profile.md)
- [Set up Intune enrollment of Android Enterprise corporate-owned devices with work profile](../../device-enrollment/android/setup-corporate-work-profile.md)
- [Set up enrollment for Android Enterprise fully managed devices](../../device-enrollment/android/setup-fully-managed.md)
- [Set up Intune enrollment of Android Enterprise dedicated devices](../../device-enrollment/android/setup-dedicated.md)
- [App protection policies overview](../../app-management/protection/overview.md)

Applies to:

- Android device administrator (DA)

#### Device Firmware Configuration Interface (DFCI) supports VAIO devices <!-- 28186944 -->

For Windows devices, you can create a DFCI profile to manage UEFI (BIOS) settings. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type.

Some VAIO devices running Windows are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

For more information about DFCI profiles, see:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../../device-configuration/templates/configure-dfci-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](/autopilot/dfci-management)

Applies to:

- Windows 10
- Windows 11

#### New settings available in the Apple settings catalog <!-- 28672633 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Declarative Device Management (DDM) > Math Settings**:

- Calculator
  - Basic Mode
  - Math Notes Mode
  - Scientific Mode

- System Behavior
  - Keyboard Suggestions
  - Math Notes

**Web Content Filter**:

- Hide Deny List URLs

##### macOS

**Declarative Device Management (DDM) > Math Settings**:

- Calculator
  - Basic Mode
  - Math Notes Mode
  - Programmer Mode
  - Scientific Mode

- System Behavior
  - Keyboard Suggestions
  - Math Notes

**System Configuration > System Extensions**:

- Non Removable From UI System Extensions
- Non Removable System Extensions

#### Consent prompt update for remote log collection<!-- 28072852 -->

End users might see a different consent experience for remote log collection after the Android APP SDK 10.4.0 and iOS APP SDK 19.6.0 updates. End users no longer see a common prompt from Intune and only see a prompt from the application, if it has one.

Adoption of this change is per-application and is subject to each applications release schedule.

Applies to:

- Android
- iOS/iPadOS

### Device enrollment

#### New Setup Assistant screens available for configuration for ADE <!-- 26607203, 2532989 -->

New Setup Assistant screens are available to configure in the Microsoft Intune admin center. You can hide or show these screens during automated device enrollment (ADE).

For macOS:

- **Wallpaper**: Show or hide the macOS Sonoma wallpaper setup pane that appears after an upgrade on devices running macOS 14.1 and later.
- **Lockdown mode**: Show or hide the lockdown mode setup pane on devices running macOS 14.1 and later.
- **Intelligence**: Show or hide the Apple Intelligence setup pane on devices running macOS 15 and later.

For iOS/iPadOS:

- **Emergency SOS**: Show or hide the safety setup pane on devices running iOS/iPadOS 16 and later.
- **Action button**: Show or hide the setup pane for the action button on devices running iOS/iPadOS 17 and later.
- **Intelligence**: Show or hide the Apple Intelligence setup pane on devices running iOS/iPadOS 18 and later.

You can configure these screens in new and existing enrollment policies. For more information and additional resources, see:

- [Set up Apple automated device enrollment for iOS/iPadOS](../../device-enrollment/apple/setup-automated-ios.md)
- [Set up Apple automated device enrollment for Macs](../../device-enrollment/apple/setup-automated-macos.md)

#### Extended expiration date for corporate-owned, user-associated AOSP enrollment tokens<!-- 25782149 -->

Now when you create an enrollment token for Android Open Source Project (AOSP) corporate-owned, user-associated devices, you can select an expiration date that's up to 65 years into the future, an improvement over the previous 90 day expiration date. You can also modify the expiration date of existing enrollment tokens for Android Open Source Project (AOSP) corporate-owned, user-associated devices.

### Device security

#### New disk encryption template for Personal Data Encryption<!-- 28677934 -->

You can now use the new *Personal Data Encryption* (PDE) template that is available through endpoint security [*disk encryption* policy](../../device-configuration/endpoint-security/encrypt-bitlocker-windows.md). This new template configures the Windows [PDE configuration service provider](/windows/client-management/mdm/personaldataencryption-csp) (CSP), which was introduced in Windows 11 22H2. The PDE CSP is also available through the settings catalog.

PDE differs from BitLocker in that it encrypts files instead of whole volumes and disks. PDE occurs in addition to other encryption methods such as BitLocker. Unlike BitLocker that releases data encryption keys at boot, PDE doesn't release data encryption keys until a user signs in using Windows Hello for Business.

Applies to:

- Windows 11 version 22h2 or later

For more information about PDE, including prerequisites, related requirements, and recommendations, see the following articles in the Windows security documentation:

- [PDE overview](/windows/security/operating-system-security/data-protection/personal-data-encryption/)
- [Configure PDE](/windows/security/operating-system-security/data-protection/personal-data-encryption/configure)
- [PDE frequently asked questions (FAQ)](/windows/security/operating-system-security/data-protection/personal-data-encryption/faq)

### Intune Apps

#### Newly available protected app for Intune<!-- 28730764 -->

The following protected app is now available for Microsoft Intune:

- Notate for Intune by Shafer Systems, LLC

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

## Week of September 9, 2024

### App management

#### Managed Home Screen user experience update<!-- 28232751 -->

All Android devices automatically migrate to the updated Managed Home Screen (MHS) user experience. For more information, see [Updates to the Managed Home Screen experience](https://techcommunity.microsoft.com/t5/intune-customer-success/updates-to-the-managed-home-screen-experience/bc-p/3997842).

### Device enrollment

#### Support has ended for Apple profile-based user enrollment with Company Portal<!-- 28361917 -->

Apple supports two types of manual enrollment methods for users and devices in bring-your-own-device (BYOD) scenarios: *profile-based enrollment* and *account-driven enrollment*. Apple ended support for profile-based user enrollment, known in Intune as *user enrollment with Company Portal*. This method was their privacy-focused BYOD enrollment flow that used managed Apple IDs. As a result of this change, Intune has ended support for [profile-based user enrollment with Company Portal](../../device-enrollment/apple/setup-user-company-portal.md). Users can no longer enroll devices targeted with this enrollment profile type. This change doesn't affect devices that are already enrolled with this profile type, so you can continue to manage them in the admin center and receive Microsoft Intune technical support. Less than 1% of Apple devices across all Intune tenants are currently enrolled this way, so this change doesn't affect most enrolled devices.

There's no change to profile-based device enrollment with Company Portal, the default enrollment method for BYOD scenarios. Devices enrolled via Apple automated device enrollment also remain unaffected.

We recommend account-driven user enrollment as a replacement method for devices. For more information about your BYOD enrollment options in Intune, see:

- [Account-driven user enrollment](../../device-enrollment/apple/setup-account-driven-user.md)
- [Web-based device enrollment](../../device-enrollment/apple/setup-web-based-ios.md)
- [Device enrollment with Company Portal](../../device-enrollment/apple/personal-device-options-ios.md#app-or-web-based-enrollment) (default enrollment method for BYOD scenarios)

For more information about the device enrollment types supported by Apple, see [Intro to Apple device enrollment types](https://support.apple.com/en-mide/guide/deployment/dep08f54fcf6/web) in the Apple Platform Deployment guide.

### Device management

#### Intune now supports iOS/iPadOS 16.x as the minimum version<!-- 28391935 -->

With the release of iOS 18 and iPadOS 18, Microsoft Intune, including the Intune Company Portal and Intune app protection policies (APP, also known as MAM), will now require iOS/iPadOS 16 and higher.

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

Applies to:

- iOS/iPadOS

#### Intune now supports macOS 13.x as the minimum version<!-- 28391869 -->

With Apple's release of macOS 15 Sequoia, Microsoft Intune, the Company Portal app, and the Intune MDM agent will now require macOS 13 (Ventura) and later.

> [!NOTE]
> macOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement](https://aka.ms/Intune/macOS/ADE-DE-support).

Applies to:

- macOS

## Week of August 19, 2024 (Service release 2408)

### Microsoft Intune Suite

#### Easy creation of Endpoint Privilege Management elevation rules from support approval requests and reports<!-- 28196775 -->

You can now create Endpoint Privilege Management (EPM) elevation rules directly from a support approved elevation request or from details found in the EPM Elevation report. With this new capability, you won't need to manually identify specific file detection details for elevation rules. Instead, for files that appear in the Elevation report or a support approved elevation request, you can select that file to open its elevation detail pane, and then select the option to **Create a rule with these file details**.

When you use this option, you can then choose to add the new rule to one of your existing elevation policies, or create a new policy with only the new rule.

Applies to:

- Windows 10
- Windows 11

For information about this new capability, see [Windows elevation rules policy](../../epm/create-elevation-rules.md) in the *Configure policies for Endpoint Privilege management* article.

#### Introducing the Resource performance report for physical devices in Advanced Analytics<!-- 12659827 -->

We're introducing the Resource performance report for Windows physical devices in Intune Advanced Analytics. The report is included as an Intune-add on under Microsoft Intune Suite.

The resource performance scores and insights for physical devices are aimed to help IT admins make CPU/RAM asset management and purchase decisions that improve the user experience while balancing hardware costs.

For more information, see:

- [Resource performance report](../../advanced-analytics/resource-performance.md)
- [Microsoft Intune Suite](../../fundamentals/add-ons.md)

### App management

#### Managed Home Screen for Android Enterprise Fully Managed devices<!-- 15603355 -->

Managed Home Screen (MHS) is now supported on Android Enterprise Fully Managed devices. This capability offers organizations the ability to leverage MHS in scenarios where a device is associated with a single user.

For related information, see:

- [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../app-management/configuration/configure-managed-home-screen.md)
- [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../../device-configuration/templates/ref-device-restrictions-android-enterprise.md)
- [Configure permissions for the Managed Home Screen (MHS) on Android Enterprise devices using Microsoft Intune](../../device-configuration/templates/configure-managed-home-screen-permissions-android.md)

#### Updates to the Discovered Apps report<!-- 28898418 -->

The **Discovered Apps** report, which provides a list of detected apps that are on Intune enrolled devices for your tenant, now provides publisher data for Win32 apps, in addition to Store apps. Rather than providing publisher information only in the exported report data, we're including it as a column in the **Discovered Apps** report.

For more information, see [Intune Discovered apps](../../app-management/discovered-apps.md#monitor-discovered-apps-with-intune).

#### Improvements to Intune Management Extension logs<!-- 26113668 -->

We have updated how log activities and events are made for Win32 apps and the Intune Management Extension (IME) logs. A new log file (*AppWorkload.log*) contains all logging information related to app deployment activities conducted by the IME. These improvements provide better troubleshooting and analysis of app management events on the client.

For more information, see [Intune management extension logs](../../device-management/tools/management-extension-windows.md#intune-management-extension-logs).

### Device configuration

#### New settings available in the Apple settings catalog <!-- 28308531 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

There are new settings in the Apple Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Declarative Device Management (DDM) > Safari Extension Settings**:

- Managed Extensions
  - Allowed Domains
  - Denied Domains
  - Private Browsing
  - State

**Declarative Device Management (DDM) > Software Update Settings**:

- Automatic Actions
  - Download
  - Install OS Updates

- Deferrals
  - Combined Period In Days

- Notifications

- Rapid Security Response
  - Enable
  - Enable Rollback

- Recommended Cadence

**Restrictions**:

- Allow ESIM Outgoing Transfers
- Allow Genmoji
- Allow Image Playground
- Allow Image Wand
- Allow iPhone Mirroring
- Allow Personalized Handwriting Results
- Allow Video Conferencing Remote Control
- Allow Writing Tools

##### macOS

**Authentication > Extensible Single Sign On (SSO)**:

- Platform SSO
  - Authentication Grace Period
  - FileVault Policy
  - Non Platform SSO Accounts
  - Offline Grace Period
  - Unlock Policy

**Authentication > Extensible Single Sign On Kerberos**:

- Allow Password
- Allow SmartCard
- Identity Issuer Auto Select Filter
- Start In Smart Card Mode

**Declarative Device Management (DDM) > Disk Management**:

- External Storage
- Network Storage

**Declarative Device Management (DDM) > Safari Extension Settings**:

- Managed Extensions
  - Allowed Domains
  - Denied Domains
  - Private Browsing
  - State

**Declarative Device Management (DDM) > Software Update Settings**:

- Allow Standard User OS Updates

- Automatic Actions
  - Download
  - Install OS Updates
  - Install Security Update

- Deferrals
  - Major Period In Days
  - Minor Period In Days
  - System Period In Days

- Notifications

- Rapid Security Response
  - Enable
  - Enable Rollback

**Restrictions**:

- Allow Genmoji
- Allow Image Playground
- Allow iPhone Mirroring
- Allow Writing Tools

**System Policy > System Policy Control**:

- Enable XProtect Malware Upload

#### Enhancements to multi administrative approval<!-- 25174473 -->

Multi administrative approval adds the ability to limit application access policies to Windows applications or all non-Windows applications or both. We're adding a new access policy to the multiple administrative approval feature to allow approvals for changes to multiple administrative approval.

For more information, see [Multi admin approval](../../fundamentals/role-based-access-control/multi-admin-approval.md).

### Device enrollment

#### Account-driven Apple User Enrollment now generally available for iOS/iPadOS 15+<!-- 10277062 -->

Intune now supports account-driven Apple User Enrollment, the new, and improved version of Apple User Enrollment, for devices running iOS/iPadOS 15 and later. This new enrollment method utilizes just-in-time registration, removing the Company Portal app for iOS as an enrollment requirement. Device users can initiate enrollment directly in the Settings app, resulting in a shorter and more efficient onboarding experience.

For more information, see [Set up account driven Apple User Enrollment](../../device-enrollment/apple/setup-account-driven-user.md) on Microsoft Learn.

Apple announced they are ending support for profile-based Apple User Enrollment. As a result, Microsoft Intune will end support for Apple User Enrollment with Company Portal shortly after the release of iOS/iPadOS 18. We recommend enrolling devices with account-driven Apple User Enrollment for similar functionality and an improved user experience.

#### Use corporate Microsoft Entra account to enable Android Enterprise management options in Intune<!-- 25231452 -->

Managing Intune-enrolled devices with Android Enterprise management options previously required you to connect your Intune tenant to your managed Google Play account using an enterprise Gmail account. Now you can use a corporate Microsoft Entra account to establish the connection. This change is happening in new tenants, and doesn't affect tenants that have already established a connection.

For more information, see [Connect Intune account to Managed Google Play account - Microsoft Intune | Microsoft Learn](../../device-enrollment/android/connect-managed-google-play.md).

### Device management

#### 21Vianet support for Mobile Threat Defense connectors<!-- 10355489 -->

Intune operated by 21Vianet now supports Mobile Threat Defense (MTD) connectors for Android and iOS/iPadOS devices for MTD vendors that also have support in that environment. When an MTD partner is supported and you sign in to a 21Vianet tenant, the supported connectors are available.

Applies to:

- Android
- iOS/iPadOS

For more information, see:

- [Intune operated by 21Vianet in China](../../fundamentals/china.md)
- [Mobile Threat Defense integration with Intune](../../device-security/mobile-threat-defense/overview.md)

#### New `cpuArchitecture` filter device property for app and policy assignments<!-- 7423106 -->

When you assign an app, compliance policy, or configuration profile, you can filter the assignment using different device properties, such as device manufacturer, operating system SKU, and more.

A new `cpuArchitecture` device filter property is available for Windows and macOS devices. With this property, you can filter app and policy assignments depending on the processor architecture.

For more information on filters and the device properties you can use, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](../../fundamentals/filters/overview.md)
- [Filter properties](../../fundamentals/filters/ref-device-properties.md)
- [Supported workloads](../../fundamentals/filters/ref-supported-workloads.md)

Applies to:

- Windows 10
- Windows 11
- macOS

### Device security

#### Windows platform name change for endpoint security policies<!-- 16104088 -->

When you create an endpoint security policy in Intune, you can select the Windows platform. For multiple templates in endpoint security, there are now only two options to choose for the Windows platform: **Windows** and **Windows (ConfigMgr)**.

Specifically, the platform name changes are:

| Original | New |
| --- | --- |
| Windows 10 and later​ | Windows |
| Windows 10 and later (ConfigMgr)​ | Windows (ConfigMgr)​ |
| Windows 10, Windows 11, and Windows Server | Windows |
| Windows 10, Windows 11, and Windows Server​ (ConfigMgr) | Windows (ConfigMgr)​ |

These changes apply to the following policies:

- Antivirus
- Disk encryption
- Firewall
- Endpoint Privilege Management
- Endpoint detection and response
- Attack surface reduction
- Account protection

##### What you need to know

- This change is only in the user experience (UX) that admins see when they create a new policy. There is no effect on devices.
- The functionality is the same as the previous platform names.
- There are no additional tasks or actions for existing policies.

For more information on endpoint security features in Intune, see [Manage endpoint security in Microsoft Intune](../../device-security/endpoint-security-policies.md).

Applies to:

- Windows

#### Target Date Time setting for Apple software update enforcement schedules updates using the local time on devices <!-- 28865232 -->

You can specify the time that OS updates are enforced on devices in their local time zone. For example, configuring an OS update to be enforced at 5pm schedules the update for 5pm in the device's local time zone. Previously, this setting used the time zone of the browser where the policy was configured.

This change only applies to new policies that are created in the August 2408 release and later. The **Target Date Time** setting is in the [settings catalog](../../device-configuration/settings-catalog/index.md) at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type > **Declarative Device Management** > Software Update.

In a future release, the **UTC** text will be removed from the **Target Date Time** setting.

For more information on using the settings catalog to configure software updates, see [Managed software updates with the settings catalog](../../device-updates/apple/index.md).

Applies to:

- iOS/iPadOS
- macOS

### Intune Apps

#### Newly available protected apps for Intune<!-- 28676100, 28442762, 28421791, 28441819, 28618264 -->

The following protected apps are now available for Microsoft Intune:

- Singletrack for Intune (iOS) by Singletrack
- 365Pay by 365 Retail Markets
- Island Browser for Intune (Android) by Island Technology, Inc.
- Recruitment.Exchange by Spire Innovations, Inc.
- Talent.Exchange by Spire Innovations, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

### Tenant administration

#### Organizational messages now in Microsoft 365 admin center<!-- 27711197 -->

The organizational message feature has moved out of the Microsoft Intune admin center and into its new home in the Microsoft 365 admin center. All organizational messages you created in Microsoft Intune are now in the Microsoft 365 admin center, where you can continue to view and manage them. The new experience includes highly requested features such as the ability to author custom messages, and deliver messages on Microsoft 365 apps.

For more information, see:

- [Introducing organizational messages (preview) in the Microsoft 365 admin center](https://techcommunity.microsoft.com/t5/microsoft-365-blog/introducing-organizational-messages-preview-in-the-microsoft-365/ba-p/4123890)
- [Organizational messages in the Microsoft 365 admin center](/microsoft-365/admin/misc/organizational-messages-microsoft-365)
- [Support tip: Organizational messages is moving to Microsoft 365 admin center - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-organizational-messages-is-moving-to-microsoft-365/ba-p/4148332)

## Week of July 29, 2024

### Microsoft Intune Suite

#### Endpoint Privilege Management, Advanced Analytics, and Intune Plan 2 are available for GCC High and DoD<!-- 25230811, 25300700, 27030977, 27234960 -->

We are excited to announce that the following capabilities from the Microsoft Intune Suite are now supported in U.S. Government Community Cloud (GCC) High and U.S. Department of Defense (DoD) environments.

Add-on capabilities:

- [Endpoint Privilege Management](../../epm/overview.md)
- [Advanced Analytics](../../advanced-analytics/index.md) - With this release, GCC High and DoD support for Advanced Endpoint Analytics doesn't include the [*Device query*](../../advanced-analytics/device-query.md) functionality.

Plan 2 capabilities:

- [Microsoft Tunnel for Mobile Application Management](../../device-security/microsoft-tunnel/mam.md)
- [Firmware-over-the-air update](../../device-updates/android/setup-zebra-lifeguard.md)
- [Specialty devices management](../../device-management/specialty-devices.md)

For more information, see:

- [Use Microsoft Intune Suite add-on capabilities](../../fundamentals/add-ons.md)
- [Microsoft Intune for US Government GCC service description](../../fundamentals/government-service.md)

### Device enrollment

#### ACME protocol support for iOS/iPadOS and macOS enrollment<!-- 25140355 -->

As we prepare to support managed device attestation in Intune, we are starting a phased rollout of an infrastructure change for new enrollments that includes support for the *Automated Certificate Management Environment (ACME) protocol*. Now when new Apple devices enroll, the management profile from Intune receives an ACME certificate instead of a SCEP certificate. ACME provides better protection than SCEP against unauthorized certificate issuance through robust validation mechanisms and automated processes, which helps reduce errors in certificate management.

Existing OS and hardware eligible devices do not get the ACME certificate unless they re-enroll. There is no change to the end user's enrollment experience, and no changes to the Microsoft Intune admin center. This change only impacts enrollment certificates and has no impact on any device configuration policies.

ACME is supported for Apple Device Enrollment, Apple Configurator enrollment, and Automated device enrollment (ADE) methods. Eligible OS versions include:

- iOS 16.0 or later
- iPadOS 16.1 or later
- macOS 13.1 or later

This capability is also supported in [GCC High tenants](../../fundamentals/government-service.md).

## Week of July 22, 2024 (Service release 2407)

### Microsoft Intune Suite

#### New actions for Microsoft Cloud PKI<!-- 24231040 -->

The following actions have been added for Microsoft Cloud PKI issuing and root certification authorities (CA):

- Delete: Delete a CA.
- Pause: Temporarily suspend use of a CA.
- Revoke: Revoke a CA certificate.

You can access all new actions in the Microsoft Intune admin center and Graph API. For more information, see [Delete Microsoft Cloud PKI certification authority](../../cloud-pki/delete-ca.md).

### App management

#### Intune support for additional macOS app types from the Company Portal<!-- 26133163 -->

Intune supports the capability to deploy DMG and PKG apps as **Available** in the Intune macOS Company Portal. This capability enables end users to browse and install agent-deployed applications using Company Portal for macOS. This capability requires a minimum version of the Intune agent for macOS v2407.005 and Intune Company Portal for macOS v5.2406.2.

#### Newly available Enterprise App Catalog apps for Intune<!-- 28691663 -->

The Enterprise App Catalog has updated to include additional apps. For a complete list of supported apps, see [Apps available in the Enterprise App Catalog](../../app-management/deployment/enterprise-app-management.md#apps-available-in-the-enterprise-app-catalog).

#### The Intune App SDK and Intune App Wrapping Tool are now in a different GitHub repo<!-- 27264674, 27264632 -->

The Intune App SDK and Intune App Wrapping Tool have moved to a different GitHub repository and a new account. There are redirects in place for all existing repositories. In addition, the Intune sample applications are also included in this move. This change relates to both Android and iOS platforms.

### Device configuration

#### New clipboard transfer direction settings available in the Windows settings catalog <!-- 28748086 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type.

**Administrative Templates > Windows Components > Remote Desktop Services > Remote Desktop Session Host > Device and Resource Redirection**:

- Restrict clipboard transfer from server to client
- Restrict clipboard transfer from server to client (User)
- Restrict clipboard transfer from client to server
- Restrict clipboard transfer from client to server (User)

For more information on configuring the clipboard transfer direction in Azure Virtual Desktop, see [Configure the clipboard transfer direction and types of data that can be copied in Azure Virtual Desktop](/azure/virtual-desktop/clipboard-transfer-direction-data-types).

Applies to:

- Windows 11
- Windows 10

#### New settings available in the Apple settings catalog <!-- 28052449 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Restrictions**:

- Allow Auto Dim

##### macOS

**Privacy > Privacy Preferences Policy Control**:

- Bluetooth Always

#### Android Enterprise has new values for the Allow access to all apps in Google Play store setting<!-- 28367525 -->

In an Intune device restrictions configuration policy, you can configure the **Allow access to all apps in Google Play store** setting using the **Allow** and **Not configured** options (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully managed, dedicated and corporate-owned work profile > Device restrictions** for profile type > **Applications**).

The available options are updated to **Allow**, **Block**, and **Not configured**.

There's no impact to existing profiles using this setting.

For more information on this setting and the values you can currently configure, see [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../../device-configuration/templates/ref-device-restrictions-android-enterprise.md).

Applies to:

- Android Enterprise Fully managed, dedicated and corporate-owned work profile

### Device enrollment

#### New support for Red Hat Enterprise Linux<!-- 25160548 -->

Microsoft Intune now supports device management for Red Hat Enterprise Linux. You can enroll and manage Red Hat Enterprise Linux devices, and assign standard compliance policies, custom configuration scripts, and compliance scripts. For more information, see [Deployment guide: Manage Linux devices in Microsoft Intune](../../fundamentals/platform-guide-linux.md) and [Enrollment guide: Enroll Linux desktop devices in Microsoft Intune](../../device-enrollment/guide-linux.md).

Applies to:

- Red Hat Enterprise Linux 9
- Red Hat Enterprise Linux 8

#### New Intune report and device action for Windows enrollment attestation (public preview)<!-- 12581956 -->

Use the new device attestation status report in Microsoft Intune to find out if a device has attested and enrolled securely while being hardware-backed. From the report, you can attempt remote attestation via a new device action.

For more information, see:

- [Windows enrollment attestation](../../device-enrollment/windows/attestation.md)
- [Intune Reports](../../device-management/reports/overview.md#device-attestation-status-report)

#### Just-in-time registration and compliance remediation available for all iOS/iPadOS enrollments<!-- 27759589 -->

You can now configure just-in-time (JIT) registration and JIT compliance remediation for all Apple iOS and iPadOS enrollments. These Intune-supported features improve the enrollment experience because they can take the place of the Intune Company Portal app for device registration and compliance checks. We recommend setting up JIT registration and compliance remediation for new enrollments, and to improve the experience for existing enrolled devices. For more information, see [Set up just in time registration in Microsoft Intune](../../device-enrollment/apple/setup-just-in-time-registration.md).

### Device management

#### Consolidation of Intune profiles for identity protection and account protection <!-- 24810271 -->

We have consolidated the Intune profiles that were related to identity and account protection, into a single new profile named *Account protection*. This new profile is found in the [account protection policy node of endpoint security](../../device-configuration/endpoint-security/account-protection.md), and is now the only profile template that remains available when creating new policy instances for identity and account protection. The new profile includes Windows Hello for Business settings for both users and devices, and settings for Windows Credential Guard.

Because this new profile uses Intune's unified settings format for device management, the profiles settings are also available through the [settings catalog](../../device-configuration/settings-catalog/index.md), and help to improve the reporting experience in the Intune admin center.

You can continue to use any instances of the following profile templates that you already have in place, but Intune no longer supports creating new instances of these profiles:

- **Identity protection** – previously available from *Devices* > *Configuration* > *Create* > *New Policy* > *Windows 10 and later* > *Templates* > *Identity Protection*
- **Account protection (Preview)** – previously available from *Endpoint Security* > *Account protection* > *Windows 10 and later* > *Account protection (Preview)*

Applies to:

- Windows 10
- Windows 11

#### New `operatingSystemVersion` filter property with new comparison operators (preview) <!-- 10033345 -->

There's a new `operatingSystemVersion` filter property. This property:

- Is in [public preview](../../fundamentals/public-preview.md) and still being developed. So, some features, like **Preview devices**, don't work yet.

- Should be used instead of the existing `OSVersion` property. The `OSVersion` property is being deprecated.

  When `operatingSystemVersion` is generally available (GA), the `OSVersion` property will retire, and you won't be able to create new filters using this property. Existing filters that use `OSVersion` continue to work.

- Has new comparison operators:

  - `GreaterThan`: Use for version value types.

    - Allowed values: `-gt` | `gt`
    - Example: `(device.operatingSystemVersion -gt 10.0.22000.1000)`

  - `GreaterThanOrEquals`: Use for version value types.

    - Allowed values: `-ge` | `ge`
    - Example: `(device.operatingSystemVersion -ge 10.0.22000.1000)`

  - `LessThan`: Use for version value types.

    - Allowed values: `-lt | lt`
    - Example: `(device.operatingSystemVersion -lt 10.0.22000.1000)`

  - `LessThanOrEquals`: Use for version value types.

    - Allowed values: `-le` | `le`
    - Example: `(device.operatingSystemVersion -le 10.0.22000.1000)`

For managed devices, `operatingSystemVersion` applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

For managed apps, `operatingSystemVersion` applies to:

- Android
- iOS/iPadOS
- Windows

For more information on filters and the device properties you can use, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](../../fundamentals/filters/overview.md)
- [Filter properties](../../fundamentals/filters/ref-device-properties.md)

#### Government community cloud (GCC) support for Remote Help for macOS devices<!-- 25568551 -->

GCC customers can now use Remote Help for macOS devices on both web app and native application.

Applies to:

- macOS 12, 13 and 14

For more information, see:

- [Remote Help on macOS](../../remote-help/index.md)
- [Microsoft Intune for US Government GCC service description](../../fundamentals/government-service.md)

### Device security

#### Updated security baseline for Windows 365 Cloud PC<!-- 26504698 -->

You can now deploy the Intune security baseline for **Windows 365 Cloud PC**. This new baseline is based on Windows **version 24H1**. This new baseline version uses the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../../device-security/security-baselines/overview.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline represents the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

To view the new baselines included settings with their default configurations, see, [Windows 365 baseline settings version 24H1](../../device-security/security-baselines/ref-windows-365-settings.md?pivots=win365-24h1).

### Intune apps

#### Newly available protected apps for Intune<!-- 28334000, 28157519, 28311088, 28156655, 28246919, 28246936, 28100886 -->

The following protected apps are now available for Microsoft Intune:

- Asana: Work in one place (Android) by Asana, Inc.
- Goodnotes 6 (iOS) by Time Base Technology Limited
- Riskonnect Resilience by Riskonnect, Inc.
- Beakon Mobile App by Beakon Mobile Team
- HCSS Plans: Revision control (iOS) by Heavy Construction Systems Specialists, Inc.
- HCSS Field: Time, cost, safety (iOS) by Heavy Construction Systems Specialists, Inc.
- Synchrotab for Intune (iOS) by Synchrotab, LLC

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

## Week of July 15, 2024

### Device management

#### New setting in the Device Control profile for Attack surface reduction policy<!-- 28761508 -->

We've added a new category and setting to the Device Control profile for the *Windows 10, Windows 11, and Windows Server* platform of Intune [Attack surface reduction policy](../../device-configuration/endpoint-security/attack-surface-reduction.md).

The new setting is **Allow Storage Card**, and found in the new **System** category of the profile. This setting is also available from the Intune [settings catalog](../../device-configuration/settings-catalog/index.md) for the Windows devices.

This setting controls whether the user is allowed to use the storage card for device storage, and can prevent programmatic access to the storage card. For more information on this new setting, see [AllowStorageCard](/windows/client-management/mdm/policy-csp-system?branch=main&branchFallbackFrom=pr-en-us-15655&WT.mc_id=Portal-fx#allowstoragecard) in the Windows documentation.

## Week of July 8, 2024

### Device management

#### Copilot in Intune now has the device query feature using Kusto Query Language (KQL) (public preview)<!-- 24874816 -->

When you use Copilot in Intune, there's a new device query feature that uses KQL.
Use this feature to ask questions about your devices using a natural language. If device query can answer your question, Copilot generates the KQL query you can run to get the data you want.

To learn more about how you can currently use Copilot in Intune, see [Microsoft Copilot in Intune](../../copilot/index.md).

### Monitor and Troubleshoot

#### New actions for policies, profiles, and apps<!-- 15283153 -->

You can now remove, reinstall, and reapply individual policies, profiles, and apps for iOS/iPadOS devices and Android corporate owned devices. You can apply these actions without changing assignments or group membership. These actions are intended to help resolve customer challenges that are external to Intune. Also, these actions can help to quickly restore end user productivity.

For more information, see [Remove apps and configuration](../../device-management/actions/remove-apps-config.md)

### App management

#### MAC address available from the Managed Home Screen app<!-- 25994454 -->

MAC address details are now available from the **Device Information** page of the Managed Home Screen (MHS) app. For information about MHS, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../app-management/configuration/configure-managed-home-screen.md).

#### New configuration capabilities for Managed Home Screen<!-- 25013268 -->

You can now configure Managed Home Screen (MHS) to enable a virtual app-switcher button that allows end users to easily navigate between apps on their kiosk devices from MHS. You can select between a floating or swipe-up app-switcher button. The configuration key is `virtual_app_switcher_type` and the possible values are `none`, `float`, and `swipe_up`. For information related to configuring the Managed Home Screen app, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../app-management/configuration/configure-managed-home-screen.md).

### Device enrollment

#### Update for Apple user and device enrollments with Company Portal <!-- 27557088 -->

We've made changes to the device registration process for Apple devices enrolling with Intune Company Portal. Previously, Microsoft Entra device registration occurred during enrollment. With this change, registration occurs after enrollment.

Existing enrolled devices aren't affected by this change. For new user or device enrollments that utilize Company Portal, users must return to Company Portal to complete registration:

- For iOS users: Users with notifications enabled are prompted to return to the Company Portal app for iOS. If they disable notifications, they aren't alerted, but still need to return to Company Portal to complete registration.

- For macOS devices: The Company Portal app for macOS detects the installation of the management profile and automatically register the device, unless the user closes the app. If they close the app, they must reopen it to complete registration.

If you're using dynamic groups, which rely on device registration to work, it's important for users to complete device registration. Update your user guidance and admin documentation as needed. If you're using Conditional Access (CA) policies, no action is required. When users attempt to sign in to a CA-protected app, they are prompted to return to Company Portal to complete registration.

These changes are currently rolling out and will be made available to all Microsoft Intune tenants by the end of July. There's no change to the Company Portal user interface. For more information about device enrollment for Apple devices, see:

- [Enrollment guide: Enroll macOS devices in Microsoft Intune](../../device-enrollment/apple/guide-macos.md#device-enrollment-end-user-tasks)
- [Enrollment guide: Enroll iOS and iPadOS devices in Microsoft Intune](../../device-enrollment/apple/guide-ios-ipados.md)

## Week of June 24, 2024

### Device enrollment

#### Add corporate device identifiers for Windows<!-- 25873757 -->

Microsoft Intune now supports corporate device identifiers for devices running Windows 11, version 22H2 and later so that you can identify corporate machines ahead of enrollment. When a device that matches the model, manufacturer, and serial number criteria enrolls, Microsoft Intune marks it as a corporate device and enable the appropriate management capabilities. For more information, see [Add corporate identifiers](../../device-enrollment/add-corporate-identifiers.md).

### Microsoft Intune Suite

#### Remote Help

Version 5.1.1419.0

- Resolve issue where the screen may be blank on first launch.

## Week of June 17, 2024 (Service release 2406)

### Microsoft Intune Suite

#### Endpoint Privilege Management support for MSI and PowerShell file types<!-- 25230336 -->

Endpoint Privilege Management (EPM) *elevation rules* now support the elevation of Windows Installer and PowerShell files in addition to executable files that were previously supported. The new file extensions that EPM supports include:

- .msi
- .ps1

For information about using EPM, see [Endpoint Privilege Management](../../epm/overview.md).

#### View the certification authority key type in Microsoft Cloud PKI properties<!-- 27032276 -->

A new Microsoft Cloud PKI property called *CA keys* is available in the admin center and shows the type of certification authority keys used for signing and encryption. The property displays one of the following values:

- HSM: Indicates the use of a hardware security module-backed key.
- SW: Indicates the use of a software-backed key.

Certification authorities created with a licensed Intune Suite or Cloud PKI standalone add-on use HSM signing and encryption keys. Certification authorities created during a trial period use software-backed signing and encryption keys. For more information about Microsoft Cloud PKI, see [Overview of Microsoft Cloud PKI for Microsoft Intune](../../cloud-pki/index.md).

### App management

#### US GCC and GCC High support for Managed Home Screen<!-- 25827679 -->

Managed Home Screen (MHS) now supports sign-in for the US Government Community (GCC), US Government Community (GCC) High, and U.S. Department of Defense (DoD) environments. For more information, see [Configure the Managed Home Screen](../../app-management/configuration/configure-managed-home-screen.md) and [Microsoft Intune for US Government GCC service description](../../fundamentals/government-service.md).

Applies to:

- Android Enterprise

#### Updates to the Managed Apps report<!-- 26711898 -->

The Managed Apps report now provides details about Enterprise App Catalog apps for a specific device. For more information about this report, see [Managed Apps report](../../device-management/reports/overview.md#managed-apps-report-operational).

### Device configuration

#### New settings available in the Apple settings catalog <!--27175914 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Restrictions**:

- Allow Web Distribution App Installation

**System Configuration > Font**:

- Font
- Name

##### macOS

**Privacy > Privacy Preferences Policy Control**:

- Bluetooth Always

Applies to:

- iOS/iPadOS
- macOS

#### OS Version picker available for configuring managed iOS/iPadOS DDM software updates using the settings catalog<!-- 27565292 -->

Using the [Intune settings catalog](../../device-configuration/settings-catalog/index.md), you can configure Apple's declarative device management (DDM) feature to manage software updates on iOS/iPadOS devices.

When you configure a managed software update policy using the settings catalog, you can:

- Select a target OS version from a list of updates made available by Apple.
- Manually enter the target OS version, if needed.

For more information about configuring managed software update profiles in Intune, see [Use the settings catalog to configure managed software updates](../../device-updates/apple/index.md).

Applies to:

- iOS/iPadOS

#### Intune admin center UI updates at Devices > By platform<!-- 25104008 -->

In the Intune admin center, you can select **Devices** > **By platform**, and view the policy options for the platform you select. These platform-specific pages are updated and include tabs for navigation.

For a walkthrough of the Intune admin center, see [Tutorial: Walkthrough Microsoft Intune admin center](../../fundamentals/tutorial-admin-center-walkthrough.md).

### Device enrollment

### RBAC changes to enrollment platform restrictions for Windows<!-- 25036419 -->

We've updated role-based access controls (RBAC) for all enrollment platform restrictions in the Microsoft Intune admin center. The Intune Service Administrator roles can create, edit, delete, and reprioritize enrollment platform restrictions. For all other built-in Intune roles, restrictions are read-only.

**Applies to:**

- Android
- Apple
- Windows

It's important to know that with these changes:

- Scope tag behavior doesn't change. You can apply and use scope tags as usual.
- If an assigned role or permission is currently preventing a user from viewing enrollment platform restrictions, nothing changes. The user will still be unable to view enrollment platform restrictions in the admin center.

For more information, see [Create device platform restrictions](../../device-enrollment/create-platform-restrictions.md).

### Device management

### Updates to replace Wandera with Jamf is complete in the Intune admin center<!-- 26525211 -->

We've completed a rebrand in the Microsoft Intune admin center to support replacing Wandera with Jamf. This includes updates to the name of the Mobile Threat Defense connector, which is now *Jamf*, and changes to the minimum required platforms to use the Jamf connector:

- Android 11 and later
- iOS / iPadOS 15.6 and later

For information about Jamf and other Mobile Threat Defense (MTD) vendors that Intune supports, see [Mobile Threat Defense partners](../../device-security/mobile-threat-defense/overview.md).

### Intune apps

#### Newly available protected apps for Intune<!-- 28033401, 28035558, 27795962, 27795905, 27831146, 27795905 -->

The following protected apps are now available for Microsoft Intune:

- Atom Edge (iOS) by Arlanto GmbH
- HP Advance for Intune by HP Inc.
- IntraActive by Fellowmind
- Microsoft Azure (Android) by Microsoft Corporation
- Mobile Helix Link for Intune by Mobile Helix
- VPSX Print for Intune by Levi, Ray & Shoup, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md)

### Monitor and troubleshoot

#### View BitLocker recovery key in Company Portal apps for iOS and macOS<!-- 26615990 -->

End users can view the BitLocker recovery key for an enrolled Windows device and the FileVault recovery key for an enrolled Mac in the Company Portal app for iOS and Company Portal app for macOS. This capability will reduce helpdesk calls in the event the end user gets locked out of their corporate machines. End users can access the recovery key for an enrolled device by signing into the Company Portal app and selecting **Get recovery key**. This experience is similar to the recovery process on the Company Portal website, which also allows end users to see recovery keys.

You can prevent end users within your organization from accessing BitLocker recovery keys by configuring the **Restrict non-admin users from recovering the BitLocker keys for their owned device** setting in Microsoft Entra ID.

Applies to:

- macOS
- Windows

For more information, see:

- [Manage BitLocker policy for Windows devices with Intune](../../device-configuration/endpoint-security/encrypt-bitlocker-windows.md)
- [Get recovery key for Windows](../../user-help/security/collect-recovery-key-windows.md)
- [Use FileVault disk encryption for macOS with Intune](../../device-configuration/endpoint-security/encrypt-filevault-macos.md)
- [Get recovery key for Mac](../../user-help/security/collect-recovery-key-company-portal-website.md)
- [Manage device identities using the Microsoft Entra admin center](/entra/identity/devices/manage-device-identities#configure-device-settings)

### Role-based access control

#### New granular RBAC controls for Intune endpoint security<!-- 5475572 -->

We've begun to replace the role-based access control (RBAC) rights to endpoint security policies that are granted by the *Security baselines* permission with a series of more granular permissions for specific endpoint security tasks. This change can help you assign the specific rights your Intune admins require to do specific jobs instead of relying on either the [built-in](../../fundamentals/role-based-access-control/overview.md#built-in-roles) *Endpoint Security Manager* role or a [custom role](../../fundamentals/role-based-access-control/create-custom-role.md) that includes the *Security baseline* permission. Prior to this change, the *Security baseline* permission grants rights across all endpoint security policies.

The following new RBAC permissions are available for endpoint security workloads:

- App Control for Business
- Attack surface reduction
- Endpoint detection and response

Each new permission supports the following rights for the related policy:

- Assign
- Create
- Delete
- Read
- Update
- View Reports

Each time we add a new granular permission for an endpoint security policy to Intune, those same rights are removed from the *Security baselines* permission. If you use custom roles with the *Security baselines* permission, the new RBAC permission is assigned automatically to your custom roles with the same rights that were granted through the *Security baseline* permission. This autoassignment ensures your admins continue to have the same permissions they have today.

For more information about current RBAC permissions and built-in roles, see:

- [Role-based access control (RBAC) with Microsoft Intune](../../fundamentals/role-based-access-control/overview.md)
- [Built-in role permissions for Microsoft Intune](../../fundamentals/role-based-access-control/ref-built-in-roles.md)
- [Role-based access control for endpoint security](../../device-configuration/endpoint-security/manage-policies.md#role-based-access-control-for-endpoint-security) in *Manage device security with endpoint security policies in Microsoft Intune*.

> [!IMPORTANT]
>
> With this release, the granular permission of **Antivirus** for endpoint security policies might be temporarily visible in some Tenants. This permission is not released and isn't supported for use. Configurations of the *Antivirus* permission are ignored by Intune. When *Antivirus* becomes available to use as a granular permission, its availability will be announced in this [What's new in Microsoft Intune](../index.md) article.

## Week of June 3, 2024

### Device enrollment

#### New enrollment time grouping feature for devices <!-- 16902437 -->

Enrollment time grouping is a new, faster way to group devices during enrollment. When configured, Intune adds devices to the appropriate group without requiring inventory discovery and dynamic membership evaluations. To set up enrollment time grouping, you must configure a static Microsoft Entra security group in each enrollment profile. After a device enrolls, Intune adds it to the static security group and delivers assigned apps and policies.

This feature is available for Windows 11 devices enrolling via Windows Autopilot device preparation. For more information, see [Enrollment time grouping in Microsoft Intune](../../device-enrollment/setup-time-grouping.md).

## Week of May 27, 2024

### Microsoft Intune Suite

#### New primary endpoint for Remote Help

To improve the experience for [Remote Help](../../remote-help/index.md) on Windows, Web, and macOS devices, we have updated the primary endpoint for Remote Help:

- Old primary endpoint: `https://remoteassistance.support.services.microsoft.com`
- New primary endpoint: `https://remotehelp.microsoft.com`

If you use Remote Help and have firewall rules that block the new primary endpoint, admins and users might experience connectivity issues or disruptions when using Remove Help.

To support the new primary endpoint on Windows devices, upgrade Remote Help to version 5.1.124.0. Web and macOS devices don't require an updated version of Remote Help to make use of the new primary endpoint.

Applies to:

- macOS 11, 12, 13 and 14
- Windows
- Windows 11 on ARM64 devices
- Windows 10 on ARM64 devices
- Windows 365

For information on the newest version of Remote Help, see [Week of March 13, 2024](#week-of-march-13-2024). For information about Intune endpoints for Remote Help, see [Remote Help](../../fundamentals/endpoints.md#remote-help) in *Network endpoints for Microsoft Intune*.

### Device management

### Evaluate compliance of Windows Subsystem for Linux (public preview)<!-- 24557103 -->

Now in a public preview, Microsoft Intune supports compliance checks for instances of Windows Subsystem for Linux (WSL) running on a Windows host device.

With this preview you can create a custom compliance script that evaluates the required distribution and version of WSL. WSL compliance results are included in the overall compliance state of the host device.

Applies to:

- Windows 10
- Windows 11

For information about this capability, see [Evaluate compliance of Windows Subsystem for Linux (public preview)](../../device-security/compliance/configure-wsl.md).

## Week of May 20, 2024 (Service release 2405)

### Device configuration

#### New settings available in the macOS settings catalog<!-- 26970197 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the macOS Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

**Microsoft AutoUpdate (MAU)**:

- Microsoft Teams (work or school)
- Microsoft Teams classic

**Microsoft Defender > Features**:

- Use Data Loss Prevention
- Use System Extensions

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

Applies to:

- macOS

### Device enrollment

#### Stage Android device enrollment to reduce end-user steps<!-- 15503468 -->

To reduce the enrollment time for end users, Microsoft Intune supports device staging for Android Enterprise devices. With *device staging*, you can stage an enrollment profile and complete all related enrollment steps for workers receiving these devices:

- Corporate-owned fully managed devices
- Corporate-owned devices with a work profile

When frontline workers receive the devices, all they have to do is connect to Wi-Fi and sign in to their work account. A new *device staging token* is required to enable this feature. For more information, see [Device staging overview](../../device-enrollment/android/device-staging.md).

### Device management

#### End user access to BitLocker Recovery Keys for enrolled Windows devices<!-- 8077173 -->

End users can now view the BitLocker Recovery Key for enrolled Windows devices from the Company Portal website. This capability can reduce helpdesk calls in the event the end user gets locked out of their corporate machines. End users can access the recovery key for an enrolled device by signing into the Company Portal website and selecting **Show recovery key**. This experience is similar to the MyAccount website, which also allows end users to see recovery keys.

You can prevent end users within your organization from accessing BitLocker recovery keys by configuring the Microsoft Entra toggle **Restrict non-admin users from recovering the BitLocker key(s) for their owned device**.

For more information, see:

- [Manage device identities using the Microsoft Entra admin center](/entra/identity/devices/manage-device-identities#configure-device-settings)
- [Get recovery key for Windows](../../user-help/security/collect-recovery-key-windows.md)
- [Manage BitLocker policy for Windows devices with Intune](../../device-configuration/endpoint-security/encrypt-bitlocker-windows.md)

#### New version of Windows hardware attestation report<!-- 15425680 -->

We've released a new version of the Windows hardware attestation report that shows the value of settings attested by Device Health Attestation and Microsoft Azure Attestation for Windows. The Windows hardware attestation report is built on a new reporting infrastructure, and reports on new settings added to Microsoft Azure Attestation. The report is available in the admin center under **Reports** > **Device Compliance** > **Reports**.

For more information, see [Intune reports](../../device-management/reports/overview.md#windows-hardware-attestation-report-organizational).

The Windows health attestation report previously available under **Devices** > **Monitor** has been retired.

Applies to:

- Windows 10
- Windows 11

#### Optional Feature updates<!--12769586 -->

Feature updates can now be made available to end users as **Optional** updates, with the introduction of **Optional** Feature updates. End users see the update in the **Windows Update** settings page in the same way that it's shown for consumer devices.

End users can easily opt in to try out the next Feature update and provide feedback. When it's time to roll out the feature as a **Required** update, admins can change the setting on the policy and update the rollout settings so that the update is deployed as a **Required** update to devices that don't yet have it installed.

For more information about optional feature updates, see [Feature updates policy in Intune](../../device-updates/windows/manage-feature-updates.md).

Applies to:

- Windows 10
- Windows 11

### Device security

#### Updated security baseline for Microsoft Defender for Endpoint<!-- 26504935 -->

You can now deploy the Intune security baseline for **Microsoft Defender for Endpoint**. The new baseline, **version 24H1**, uses the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../../device-security/security-baselines/overview.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline represents the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

### Intune apps

#### Newly available protected apps for Intune<!-- 27575008, 27575336 -->

The following protected apps are now available for Microsoft Intune:

- Fellow.app by Fellow Insights Inc
- Unique Moments by Unique AG

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

## Week of May 6, 2024

### Device management

#### Intune and the macOS Company Portal app support Platform SSO (public preview)<!-- 24325427 -->

On Apple devices, you can use Microsoft Intune and the Microsoft Enterprise SSO plug-in to configure single sign-on (SSO) for apps and websites that support Microsoft Entra authentication, including Microsoft 365.

On macOS devices, Platform SSO is available in public preview. Platform SSO expands the SSO app extension by allowing you to configure different authentication methods, simplify the sign-in process for users, and reduce the number of passwords they need to remember.

Platform SSO is included in the Company Portal app version 5.2404.0 and newer.

For more information on Platform SSO and to get started, see:

- [Configure Platform SSO for macOS devices in Microsoft Intune](../../device-configuration/settings-catalog/configure-platform-sso-macos.md)
- [Single sign-on (SSO) overview and options for Apple devices in Microsoft Intune](../../device-configuration/enterprise-sso-plugin.md)

Applies to:

- macOS 13 and later

### Tenant administration

#### Customize your Intune admin center experience<!-- 24155584 -->

You can now customize your Intune admin center experience by using collapsible navigation and favorites. The left navigation menus in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) are updated to support expanding and collapsing each subsection of the menu. In addition, you can set admin center pages as favorites. This portal capability will gradually roll out over the next week.

By default, menu sections are expanded. You can choose your portal menu behavior by selecting the **Settings** gear icon at the top right to display the **Portal settings**. Then, select **Appearance + startup views** and set the **Service menu behavior** to **Collapsed** or **Expanded** as the default portal option. Each menu section retains the expanded or collapsed state that you choose. Additionally, selecting the star icon next to a page on the left navigation adds the page to a **Favorites** section near the top of the menu.

For related information, see [Change the Portal settings](../../fundamentals/tutorial-admin-center-walkthrough.md#change-the-portal-settings).

## Week of April 29, 2024

### App management

#### Updates to the Managed Home Screen experience<!-- 24990268 -->

We recently released and improved the Managed Home Screen experience, which is now Generally Available. The app is redesigned to improve the core workflows throughout the application. The updated design offers a more usable and supportable experience.

With the release, we stop investing in previous Managed Home Screen workflows. New features and fixes for Managed Home Screen are only added to the new experience. During August 2024, the new experience is automatically enabled for all devices.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../app-management/configuration/configure-managed-home-screen.md) and [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../../device-configuration/templates/ref-device-restrictions-android-enterprise.md).

#### Require end users to enter PIN to resume activity on Managed Home Screen<!-- 9322838 -->

In Intune, you can require end users to enter their session PIN to resume activity on Managed Home Screen after the device is inactive for a specified period of time. Set the **Minimum inactive time before session PIN is required** setting to the number of seconds the device is inactive before the end user must input their session PIN.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../app-management/configuration/configure-managed-home-screen.md).

#### Device IPv4 and IPv6 details available from Managed Home Screen<!-- 25994445 -->

IPv4 and IPv6 connectivity details are now both available from the **Device Information** page of the Managed Home Screen app. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../device-management/actions/collect-diagnostics.md).

#### Updates to Managed Home Screen sign-in support<!-- 25597636 -->

Managed Home Screen now supports domainless sign-in. Admins can configure a domain name, which will be automatically appended to usernames upon sign-in. Also, Managed Home Screen supports a custom login hint text to be displayed to users during the sign-in process.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../app-management/configuration/configure-managed-home-screen.md) and [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../../device-configuration/templates/ref-device-restrictions-android-enterprise.md).

#### Allow end users to control Android Enterprise device auto-rotation<!-- 9322838 -->

In Intune, you can now expose a setting in the Managed Home Screen app that allows the end user to turn on and off the device's auto-rotation. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../app-management/configuration/configure-managed-home-screen.md).

#### Allow end users to adjust Android Enterprise device screen brightness<!-- 9322834 -->

In Intune, you can expose settings in the Managed Home Screen app to adjust screen brightness for Android Enterprise devices. You can choose to expose a setting in the app to allow end users to access a brightness slider to adjust the device screen brightness. Also, you can expose a setting to allow end users to toggle adaptive brightness.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../app-management/configuration/configure-managed-home-screen.md).

#### Migrated to .NET MAUI from Xamarin<!-- 27143739 -->

Xamarin.Forms has evolved into .NET Multi-platform App UI (MAUI). Existing Xamarin projects should be migrated to .NET MAUI. For more information about upgrading Xamarin projects to .NET, see the [Upgrade from Xamarin to .NET & .NET MAUI](/dotnet/maui/migration/?WT.mc_id=dotnet-35129-website) documentation.

Xamarin support ended as of May 1, 2024 for all Xamarin SDKs including Xamarin.Forms and Intune App SDK Xamarin Bindings. For Intune support on Android and iOS platforms, see [Intune App SDK for .NET MAUI - Android](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android)and [Microsoft Intune App SDK for MAUI.iOS](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS).

## Week of April 22, 2024 (Service release 2404)

### App management

#### Auto update available with Win32 app supersedence<!-- 17644510 -->

Win32 app supersedence provides the capability to supersede apps deployed as available with **auto-update** intent. For example, if you deploy a Win32 app (app A) as available and installed by users on their device, you can create a new Win32 app (app B) to supersede app A using **auto-update**. All targeted devices and users with app A installed as available from the Company Portal are superseded with app B. Also, only app B shows in the Company Portal. You can find the **auto-update** feature for available app supersedence as a toggle under the **Available assignment** in the **Assignments** tab.

For more information about app supersedence, see [Add Win32 app supersedence](../../app-management/deployment/configure-win32-supersedence.md).

### Device configuration

#### Error message is shown when OEMConfig policy exceeds 500 KB on Android Enterprise devices<!-- 15326924 -->

On Android Enterprise devices, you can use an OEMConfig device configuration profile to add, create and/or customize OEM specific settings.

When you create an OEMConfig policy that exceeds 500 KB, then the following error is shown in the Intune admin center:

`Profile is larger than 500KB. Adjust profile settings to decrease the size.`

Previously, OEMConfig policies that exceeded 500 KB were shown as pending.

For more information on OEMConfig profiles, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../../device-configuration/templates/configure-oemconfig-android.md).

Applies to:

- Android Enterprise

### Device security

#### Windows Firewall CSP changes for processing Firewall Rules<!-- 10734904 -->

Windows changed how the Firewall configuration service provider (CSP) enforces rules from Atomic blocks of firewall rules. The Windows Firewall CSP on a device implements the firewall rule settings from your [Intune endpoint security Firewall policies](../../device-configuration/endpoint-security/firewall.md). The change of CSP behavior now enforces an all-or-nothing application of firewall rules from each Atomic block of rules.

- Previously, the CSP on a device would go through the firewall rules in an Atomic block of rules - one rule (or setting) at a time with the goal of applying all the rules in that Atomic block, or none of them. If the CSP encountered any issue with applying any rule from the block to the device, the CSP wouldn't only stop that rule, but also cease to process subsequent rules without trying to apply them. However, rules that applied successfully before a rule failed, would remain applied to the device. This behavior can lead to a partial deployment of firewall rules on a device, since the rules that were applied before a rule failed to apply aren't reversed.

- With the change to the Firewall CSP, when any rule in the block is unsuccessful in applying to the device, all the rules from that same Atomic block that were applied successfully are rolled back. This behavior ensures the desired all-or-nothing behavior is implemented and prevents a partial deployment of firewall rules from that block. For example, if a device receives an Atomic block of firewall rules that has a misconfigured rule that can't apply, or has a rule that isn't compatible with the devices operating system, then the CSP fails all the rules from that block, And, it rolls back any rules that applied to that device.

This change of Firewall CSP behavior is available on devices that run the following Windows versions or later:

- Windows 11 21H2
- Windows 11 22H2
- Windows 10 21H2

For more information on the subject of how the Windows Firewall CSP uses Atomic blocks to contain firewall rules, see the note near the top of [Firewall CSP](/windows/client-management/mdm/firewall-csp) in the Windows documentation.

For troubleshooting guidance, see the Intune support blog [How to trace and troubleshoot the Intune Endpoint Security Firewall rule creation process](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-trace-and-troubleshoot-the-intune-endpoint-security/ba-p/3261452).

#### CrowdStrike – New mobile threat defense partner<!-- 16882021 -->

We added [CrowdStrike Falcon](../../device-security/mobile-threat-defense/crowdstrike-falcon.md) as an integrated Mobile Threat Defense (MTD) partner with Intune. By configuring the CrowdStrike connector in Intune, you can control mobile device access to corporate resources using Conditional Access that's based on risk assessment in your compliance policies.

With the Intune 2404 service release, the CrowdStrike connector is now available in the admin center. However, it isn't useable until CrowdStrike publishes the required App Configuration profile details necessary to support iOS and Android devices. The profile details are expected sometime after second week of May.

### Intune apps

#### Newly available protected apps for Intune<!-- 26825160, 26954999, 26891466, 27184602 -->

The following protected apps are now available for Microsoft Intune:

- Asana: Work in one place by Asana, Inc.
- Freshservice for Intune by Freshworks, Inc.
- Kofax Power PDF Mobile by Tungsten Automation Corporation
- Remote Desktop by Microsoft Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

### Monitor and troubleshoot

#### Windows update distribution report<!--16579592 -->

The Windows update distribution report in Intune provides a summarized report. This report shows:

- The number of devices that are on each quality update level.
- The percentage of coverage for each update across Intune managed devices, including co-managed devices.

You can drill down further in the report for each quality update that aggregates devices based on the Windows feature version and the update statuses.

Finally, the admins can get the list of devices that aggregate to the numbers shown in the previous two reports, which can also be exported and used for troubleshooting and analysis along with the Windows Update for business reports.

For more information see [Windows update distribution report](../../device-updates/windows/monitor-quality-updates.md#windows-update-distribution-report).

Applies to:

- Windows 10
- Windows 11

#### Intune support of Microsoft 365 remote application diagnostics<!-- 17409991 -->

The Microsoft 365 remote application diagnostics allows Intune admins to request Intune app protection logs and Microsoft 365 application logs (where applicable) directly from the Intune console. You can find this report in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Troubleshoot** > *select a user* > **Summary** > *App protection**. This feature is exclusive to applications that are under Intune app protection management. If supported, the application specific logs are gathered and stored within dedicated storage solutions for each application.

For more information, see [Collect diagnostics from an Intune managed device](../../device-management/actions/collect-diagnostics.md).

#### Remote Help supports full control of a macOS device<!--22985205 -->

Remote Help now supports helpdesk connecting to a user's device and requesting full control of the macOS device.

For more information, see:

- [Remote Help on macOS](../../remote-help/index.md)
- [Remote Help Web App](../../remote-help/index.md)

Applies to:

- macOS 12, 13 and 14

## Week of April 15, 2024

### Intune apps

#### Newly available protected app for Intune<!-- 26740168 -->

The following protected app is now available for Microsoft Intune:

- Atom Edge by Arlanto Apps

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

## Week of April 1, 2024

### Device management

#### Copilot in Intune is available in the Intune admin center (public preview)<!-- 24105429 26122887 24205474 24205510 24205460 26113632-->

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

- [Microsoft Copilot in Intune](../../copilot/index.md)
- [Access your Microsoft Intune data in Copilot for Security](../../copilot/security-copilot.md)

Applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

#### GCC customers can use Remote Help for Windows and Android devices<!-- 10613615 25825071-->

The [Microsoft Intune Suite](../../fundamentals/add-ons.md) includes advanced endpoint management and security features, including Remote Help.

On Windows and enrolled Android Enterprise dedicated devices, you can use remote help on US Government GCC environments.

For more information on these features, see:

- [Microsoft Intune for US Government GCC service description](../../fundamentals/government-service.md)
- [Use Remote Help with Microsoft Intune](../../remote-help/index.md)

Applies to:

- Windows
- Windows on ARM64 devices
- Windows 365
- Samsung and Zebra devices enrolled as Android Enterprise dedicated devices

### Device configuration

#### New BIOS device configuration profile for OEMs<!-- 9278502 -->

There's a new **BIOS configuration and other settings** device configuration policy for OEMs. Admins can use this new policy to enable or disable different BIOS features that secure device. In the Intune device configuration policy, you add the BIOS configuration file, deploy a Win32 app, and then assign the policy to your devices.

For example, admins can use the [Dell Command tool](https://www.dell.com/support/kbdoc/000108963/how-to-use-and-troubleshoot-dell-command-update-to-update-all-drivers-bios-and-firmware-for-your-system) (opens Dell's website) to create the BIOS configuration file. Then, they add this file to the new Intune policy.

For more information on this feature, see [Use BIOS configuration profiles on Windows devices in Microsoft Intune](../../device-configuration/templates/configure-bios-windows.md).

Applies to

- Windows 10 and later

## Week of March 25, 2024 (Service release 2403)

### Microsoft Intune Suite

#### New elevation type for Endpoint Privilege Management<!-- 25230692 -->

Endpoint Privilege Management has a new file elevation type, **support approved**. Endpoint Privilege Management is a feature component of the Microsoft Intune Suite and is also available as a standalone [Intune add-on](../../fundamentals/add-ons.md).

A support-approved elevation gives you a third option for both the default elevation response and the elevation type for each rule. Unlike automatic or user confirmed, a support-approved elevation request requires Intune administrators to manage which files can run as elevated on a case-by-case basis.

With support approved elevations, users can request approval to elevate an application that isn't explicitly allowed for elevation by automatic or user approved rules. This takes the form of an elevation request that must be reviewed by an Intune administrator who can approve or deny the elevation request.

When the request is approved, users are notified that the application can now be run as elevated, and they have 24 hours from the time of approval to do so before the elevation approval expires.

Applies to:

- Windows 10
- Windows 11

For more information on this new capability, see [Support approved elevation requests](../../epm/manage-support-approvals.md).

### App management

#### Extended capabilities for Managed Google Play apps on personally owned Android devices with a work profile<!-- 26554642 -->

There are new capabilities extended to work profile devices. The following capabilities were previously available only on corporate-owned devices:

- **Available apps for device groups**: You can use Intune to make apps available for device groups through the Managed Google Play store. Previously, apps could only be made available to user groups.

- **Update priority setting**: You can use Intune to configure the app update priority on devices with a work profile. To learn more about this setting, see [Update a Managed Google Play app](../../app-management/deployment/add-managed-google-play.md#update-a-managed-google-play-app).

- **Required apps display as available in Managed Google Play**: You can use Intune to make required apps available for users through the Managed Google Play store. Apps that are part of existing policies now display as available.

These new capabilities will follow a phased rollout over multiple months.

Applies to:

- Android Enterprise personally owned devices with a work profile

### Device configuration

#### New settings available in the Apple settings catalog<!-- 26551582 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

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

#### New settings available in the Windows settings catalog<!-- 26763724, 26170998, + 26801723 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type.

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

#### New archive file scan settings added to Antivirus policy for Windows devices<!-- 26801723 -->

We added the following two settings to the *Microsoft Defender Antivirus* profile for [endpoint security Antivirus policy](../../device-configuration/endpoint-security/antivirus.md#antivirus-profiles) that apply to Windows 10 and Windows 11 devices:

- [Specify the maximum depth to scan archive files](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#scan_archivemaxdepth) - This setting allows you to configure the maximum directory depth level into which archive files such as .ZIP or .CAB are unpacked during scanning.
- [Specify the maximum size of archive files to be scanned](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#scan_archivemaxsize) - This setting allows you to configure the maximum size of archive files such as .ZIP or .CAB that are scanned. The value represents file size in kilobytes (KB).

With Antivirus policy, you can manage these settings on devices enrolled by Intune and on devices managed through the [Defender for Endpoint security settings management](../../device-security/microsoft-defender/security-settings-management.md) scenario.

Both settings are also available in the [settings catalog](../../device-configuration/settings-catalog/index.md) at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type > **Defender**.

Applies to:

- Windows 10
- Windows 11

#### Updates to assignment filters<!-- 12798031, 24801139 -->

You can use [Intune assignment filters](../../fundamentals/filters/overview.md) to assign a policy based on rules you create.

Now, you can:

- Use managed app assignment filters for Window MAM app protection policies and app configuration policies.
- Filter your existing assignment filters by **Platform**, and by the **Managed apps** or **Managed devices** filter type. When you have many filters, this feature makes it easier to find specific filters you created.

For more information on these features, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](../../fundamentals/filters/overview.md)
- [Data protection for Windows MAM](../../app-management/protection/enable-mam-windows.md)

This feature applies to:

- **Managed devices** on the following platforms:

  - Android device administrator
  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - macOS
  - Windows

- **Managed apps** on the following platforms:

  - Android
  - iOS/iPadOS
  - Windows

### Device management

#### New compliance setting lets you verify device integrity using hardware-backed security features<!-- 12391862 -->

A new compliance setting called **Check strong integrity using hardware-backed security features** lets you verify device integrity using hardware-backed key attestation. If you configure this setting, strong integrity attestation is added to Google Play's integrity verdict evaluation. Devices must meet device integrity to remain compliant. Microsoft Intune marks devices that don't support this type of integrity check as noncompliant.

This setting is available in profiles for Android Enterprise fully managed, dedicated, and corporate-owned work profile, under **Device Health** > **Google Play Protect**. It only becomes available when the Play integrity verdict policy in your profile is set to **Check basic integrity** or **Check basic integrity & device integrity**.

Applies to:

- Android Enterprise

For more information, see [Device compliance - Google Play Protect](../../device-security/compliance/ref-android-enterprise-settings.md#google-play-protect).

#### New compliance settings for Android work profile, personal devices<!-- 24743927 -->

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

For more information, see [Compliance settings - Android Enterprise](../../device-security/compliance/ref-android-enterprise-settings.md#personally-owned-work-profile).

#### Windows quality updates support for expediting non-security updates<!-- 17614146 -->

Windows quality updates now support expediting non-security updates for those times when a quality fix needs to be deployed faster than the normal quality update settings.

Applies to:

- Windows 11 devices

For more information about installing an expedited update, see [Expedite Windows quality updates in Microsoft Intune](../../device-updates/windows/manage-quality-updates.md).

#### Introducing a remote action to pause the config refresh enforcement interval<!--24249019 -->

In the Windows Settings Catalog, you can configure **Configuration Refresh**. This feature lets you set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check in to Intune. The device will replay and re-enforce settings based on previously received policy to minimize the chance for configuration drift.

To support this feature, a remote action is added to allow a pause in action. If an admin needs to make changes or run remediation on a device for troubleshooting or maintenance, they can issue a pause from Intune for a specified period. When the period expires, settings are enforced again.

The remote action **Pause configuration refresh** can be accessed from the device summary page.

For more information, see:

- [Remote actions](../../device-management/actions/index.md)
- [Pause Config Refresh Remote action](../../device-management/actions/pause-config-refresh.md)

### Device security

#### Updated security baseline for Windows version 23H2<!-- 25021947 -->

You can now deploy the Intune security baseline for Windows version 23H2. This new baseline is based on the **version 23H2** of the Group Policy security baseline found in the [Security Compliance Toolkit and Baselines](https://www.microsoft.com/en-us/download/details.aspx?id=55319) from the Microsoft Download Center, and includes only the settings that are applicable to devices managed through Intune. Use of this updated baseline can help you maintain best-practice configurations for your Windows devices.

This baseline uses the unified settings platform seen in the Settings Catalog. It features an improved user interface and reporting experience, consistency and accuracy improvements related to setting tattooing, and can support assignment filters for profiles.

Use of [Intune security baselines](../../device-security/security-baselines/overview.md) can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft. As with all baselines, the default baseline represents the recommended configurations, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

To view the new baselines included settings with their default configurations, see, [Windows MDM security baseline version 23H2](../../device-security/security-baselines/ref-windows-mdm-settings.md?pivots=mdm-23h2).

#### Use a rootless implementation of Podman to host Microsoft Tunnel<!-- 24836716 -->

When prerequisites are met, you can use a rootless Podman container to host a Microsoft Tunnel server. This capability is available when you use [Podman for Red Hat Enterprise Linux (RHEL)](../../device-security/microsoft-tunnel/prerequisites.md#linux-server) version 8.8 or later, to host Microsoft Tunnel.

When using a rootless Podman container, the mstunnel services run under a non-privileged service user. This implementation can help limit impact from a container escape. To use a rootless Podman container, you must start the tunnel installation script using a modified command line.

For more information about this Microsoft Tunnel install option, see [Use a rootless Podman container](../../device-security/microsoft-tunnel/install.md#use-a-rootless-podman-container).

#### Improvements for Intune deployments of Microsoft Defender for Endpoint<!-- 26314441 -->

We improved and simplified the experience, workflow, and report details for onboarding devices to Microsoft Defender when using Intune's endpoint detection and response (EDR) policy. These changes apply for Windows devices managed by Intune and by the tenant-attach scenario. These improvements include:

- Changes to the EDR node, dashboards, and reports to improve the visibility of your Defender EDR deployment numbers. See [About the endpoint detection and response node](../../device-configuration/endpoint-security/deploy-edr.md#deploy-edr-policy).

- A new tenant-wide option to deploy a preconfigured EDR policy that streamlines the deployment of Defender for Endpoint to applicable Windows devices. See [Use a preconfigured EDR policy](../../device-configuration/endpoint-security/deploy-edr.md#deploy-the-preconfigured-windows-edr-policy).

- Changes to Intune's the Overview page of the endpoint security node. These changes provide a consolidated view of reports for the device signals from Defender for Endpoint on your managed devices. See [Use a preconfigured EDR policy](../../device-configuration/endpoint-security/deploy-edr.md#deploy-the-preconfigured-windows-edr-policy).

These changes apply to the Endpoint security and endpoint detection and response nodes of the admin center, and the following device platforms:

- Windows 10
- Windows 11

#### Windows quality updates support expediting non-security updates<!-- 17614146 -->

Windows quality updates now support expediting non-security updates for those times when a quality fix needs to be deployed faster than the normal quality update settings.

Applies to:

- Windows 11 devices

For more information about installing an expedited update, see [Expedite Windows quality updates in Microsoft Intune](../../device-updates/windows/manage-quality-updates.md).

### Intune apps

#### Newly available protected apps for Intune<!-- 26677733, 26711918, 26763096, 26763121 -->

The following protected apps are now available for Microsoft Intune:

- Cerby by Cerby, Inc.
- OfficeMail Go by 9Folders, Inc.
- DealCloud by Intapp, Inc.
- Intapp 2.0 by Intapp, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

## Week of March 13, 2024

### Microsoft Intune Suite

#### Remote Help

Version: 5.1.1214.0

- Changed the primary endpoint for Remote Help from https://remoteassistance.support.services.microsoft.com to https://remotehelp.microsoft.com.

  > [!NOTE]
  > This could cause a breaking change for some organizations that have not yet allowed remotehelp.microsoft.com through their firewall after 5/30/2024.

- Resolved various bugs including an issue with Conditional Access. If a tenant had a **Terms of Use** policy enabled for Office 365, Remote Help wouldn't know how to respond and would instead present an authentication error message to the user.
- Enabled a shortcut to open context menus with the keyboard shortcut 'Alt + Space'

## Week of March 3, 2024

### Device enrollment

#### Role-based access control changes to enrollment settings for Windows Hello for Business<!-- 25661866 -->

We updated Role-based access control (RBAC) in the enrollment area for Windows Hello for Business. Enrollment settings related to Windows Hello for Business are read-only for all roles except the Intune Service Administrator. The Intune Service Administrator can create and edit Windows Hello for Business enrollment settings.

For more information, see [Role-based access control](../../device-security/identity-protection/configure-tenant-wide-policy.md#role-based-access-control) in the *Windows Hello at device enrollment* article.

### Device security

#### New enrollment configuration for Windows Hello for Business<!-- 9601416 -->

A new Windows Hello for Business enrollment setting, **Enable enhanced sign in security** is available in the Intune admin center. Enhanced sign-in security is a Windows Hello feature that prevents malicious users from gaining access to a user's biometrics through external peripherals.

For more information about this setting, see [Create a Windows Hello for Business policy](../../device-security/identity-protection/configure-tenant-wide-policy.md).

#### HTML formatting supported in noncompliance email notifications<!-- 24197255 -->

Intune now supports HTML formatting in noncompliance email notifications for all platforms. You can use supported HTML tags to add formatting such as italics, URL links, and bulleted lists to your organization's messages.

For more information, see [Create a notification message template](../../device-security/compliance/configure-noncompliance-actions.md#create-a-notification-message-template).

## Week of February 26, 2024

### Microsoft Intune Suite

#### New Microsoft Cloud PKI service<!-- 17272901 -->

Use the Microsoft Cloud PKI service to simplify and automate certificate lifecycle management for Intune-managed devices. ​Microsoft Cloud PKI is a feature component of the Microsoft Intune Suite and is also available as a standalone [Intune add-on](../../fundamentals/add-ons.md). The cloud-based service provides a dedicated PKI infrastructure for your organization, and doesn't require on-premises servers, connectors, or hardware. Microsoft Cloud PKI automatically issues, renews, and revokes certificates for all OS platforms supporting the SCEP certificate device configuration profile. Issued certificates can be used for certificate-based authentication for Wi-Fi, VPN, and other services supporting certificate-based authentication. For more information, see [Overview of Microsoft Cloud PKI](../../cloud-pki/index.md).

Applies to:

- Windows
- Android
- iOS/iPadOS
- macOS

### Intune apps

#### Newly available protected app for Intune<!-- 26607121 -->

The following protected app is now available for Microsoft Intune:

- Cinebody by Super 6 LLC

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

## Week of February 19, 2024 (Service release 2402)

### App management

#### More app configuration permissions for Android apps<!-- 25115278 -->

There are six new permissions that can be configured for an Android app using an app configuration policy. They are:

- Allow background body sensor data
- Media Video (read)
- Media Images (read)
- Media Audio (read)
- Nearby Wifi Devices
- Nearby Devices

For more information about how to use app config policies for Android apps, see [Add app configuration policies for managed Android Enterprise devices](../../app-management/configuration/configure-managed-android.md).

#### Newly available protected apps for Intune<!-- 26607067, 26607087, 26632132 -->

The following protected apps are now available for Microsoft Intune:

- Bob HR by Hi Bob Ltd
- ePRINTit SaaS by ePRINTit USA LLC
- Microsoft Copilot by Microsoft Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

#### Update to Intune Management Extension on Windows<!-- 26472055 -->

To support expanded functionality and bug fixes, use .NET Framework 4.7.2 or higher with the Intune Management Extension on Windows clients. If a Windows client continues to use an earlier version of the .NET Framework, the Intune Management Extension continues to function. The .NET Framework 4.7.2 is available from Windows Update as of July 10, 2018, which is included in Windows 10 1809 (RS5) and newer. Multiple versions of the .NET Framework can coexist on a device.

Applies to:

- Windows 10
- Windows 11

### Device configuration

#### Use assignment filters on Endpoint Privilege Management (EPM) policies<!-- 25230705 -->

You can use assignment filters to assign a policy based on rules you create. A filter allows you to narrow the assignment scope of a policy, like targeting devices with a specific OS version or a specific manufacturer.

You can use filters on Endpoint Privilege Management (EPM) policies.

For more information, see:

- [Use filters when assigning your apps, policies, and profiles in Intune](../../fundamentals/filters/overview.md)
- [List of platforms, policies, and app types supported by filters in Intune](../../fundamentals/filters/ref-supported-workloads.md)

Applies to:

- Windows 10
- Windows 11

#### New settings available in the Apple settings catalog<!-- 25280353 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

- **Restrictions**

  - Allow Live Voicemail
  - Force Classroom Unprompted Screen Observation
  - Force Preserve ESIM On Erase

##### macOS

- **Full Disk Encryption > FileVault** > Force Enable In Setup Assistant
- **Restrictions** > Force Classroom Unprompted Screen Observation

For more information, see:

- [Use FileVault disk encryption for macOS with Intune](../../device-configuration/endpoint-security/encrypt-filevault-macos.md)
- [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md)

#### Import up to 20 custom ADMX and ADML administrative templates<!-- 25780608 -->

You can import custom ADMX and ADML administrative templates in Microsoft Intune. Previously, you could import up to 10 files. Now, you can upload up to 20 files.

Applies to:

- Windows 10
- Windows 11

For more information on this feature, see [Import custom ADMX and ADML administrative templates into Microsoft Intune (public preview)](../../device-configuration/settings-catalog/import-custom-admx-templates.md).

#### New setting for updating MAC address randomization on Android Enterprise devices<!-- 24259789 -->

There's a new **MAC address randomization** setting on Android Enterprise devices (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Wi-Fi** for profile type).

Starting with Android 10, when connecting to a network, devices present a randomized MAC address instead of the physical MAC address. Using randomized MAC addresses is recommended for privacy, as it's harder to track a device by its MAC address. However, randomized MAC addresses break functionality that relies on a static MAC address, including network access control (NAC).

Your options:

- **Use device default**: Intune doesn't change or update this setting. By default, when connecting to a network, devices present a randomized MAC address instead of the physical MAC address. Any updates made by the user to the setting persist.

- **Use randomized MAC**: Enables MAC address randomization on devices. When devices connect to a new network, devices present a randomized MAC address, instead of the physical MAC address. If the user changes this value on their device, it resets to **Use randomized MAC** on the next Intune sync.

- **Use device MAC**: Forces devices to present their actual Wi-Fi MAC address instead of a random MAC address. This setting allows devices to be tracked by their MAC address. Only use this value when necessary, such as for network access control (NAC) support. If the user changes this value on their device, it resets to **Use device MAC** on the next Intune sync.

Applies to:

- Android 13 and newer

For more information on the Wi-Fi settings you can configure, see [Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices in Microsoft Intune](../../device-configuration/templates/ref-wifi-settings-android-enterprise.md).

#### Turn Off Copilot in Windows setting in the Windows settings catalog<!-- 26725574 -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place.

There's a new setting in the Settings Catalog. To see this setting, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows** for platform > **Settings catalog** for profile type.

- **Windows AI > Turn Off Copilot in Windows (User)**

  - If you enable this policy setting, users can't use Copilot. The Copilot icon won't appear on the taskbar.
  - If you disable or don't configure this policy setting, users can use Copilot when it's available to them.

This setting uses the [Policy CSP - WindowsAI](/windows/client-management/mdm/policy-csp-windowsai).

For more information about configuring Settings Catalog policies in Intune, including user scope vs. device scope, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

Applies to:

- Windows 10 and later

#### Windows Autopilot self-deploying mode is now generally available<!-- 26780755 -->

Windows Autopilot self-deploying mode is now generally available and out of preview. Windows Autopilot self-deploying mode enables you to deploy Windows devices with little to no user interaction. Once the device connects to network, the device provisioning process starts automatically: the device joins Microsoft Entra ID, enrolls in Intune, and syncs all device-based configurations targeted to the device. Self-deploying mode ensures that the user can't access desktop until all device-based configuration is applied. The Enrollment Status Page (ESP) is displayed during OOBE so users can track the status of the deployment. For more information, see:

- [Windows Autopilot self-deploying mode](/autopilot/self-deploying)
- [Step by step tutorial for Windows Autopilot self-deploying mode in Intune](/autopilot/tutorial/self-deploying/self-deploying-workflow)

This information is also published in [Windows Autopilot: What's new](/autopilot/whats-new).

#### Windows Autopilot for pre-provisioned deployment is now generally available<!-- 26780755 -->

Windows Autopilot for pre-provisioned deployment is now generally available and out of preview. Windows Autopilot for pre-provisioned deployment is used by organizations that want to ensure devices are business-ready before the user accesses them. With pre-provisioning, admins, partners, or OEMs can access a technician flow from the Out-of-box experience (OOBE) and kick off device setup. Next, the device is sent to the user who completes provisioning in the user phase. Pre-provisioning delivers most the configuration in advance so the end user can get to the desktop faster. For more information, see:

- [Windows Autopilot for pre-provisioned deployment](/autopilot/pre-provision).
- [Step by step tutorial for Windows Autopilot for pre-provisioned deployment Microsoft Entra join in Intune](/autopilot/tutorial/pre-provisioning/azure-ad-join-workflow)
- [Step by step tutorial for Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join in Intune](/autopilot/tutorial/pre-provisioning/hybrid-azure-ad-join-workflow).

This information is also published in [Windows Autopilot: What's new](/autopilot/whats-new).

### Device enrollment

#### ESP setting to install required apps during Windows Autopilot pre-provisioning<!-- 26583413 -->

The setting **Only fail selected blocking apps in technician phase** is now generally available to configure in Enrollment Status Page (ESP) profiles. This setting only appears in ESP profiles that have *blocking apps* selected.

For more information, see [Set up the Enrollment Status Page](../../device-enrollment/windows/setup-status-page.md#create-new-profile).

#### New local primary account configuration for macOS automated device enrollment<!-- 5877061 -->

Configure local primary account settings for Macs enrolling in Intune via Apple automated device enrollment. These settings, supported on devices running macOS 10.11 and later, are available in new and existing enrollment profiles under the new **Account Settings** tab. For this feature to work, the enrollment profile must be configured with user-device affinity and one of the following authentication methods:

- Setup Assistant with modern authentication
- Setup Assistant (legacy)

Applies to:

- macOS 10.11 and later

For more information about macOS account settings, see [Create an Apple enrollment profile in Intune](../../device-enrollment/apple/setup-automated-macos.md#create-an-enrollment-policy).

#### Await final configuration for macOS automated device enrollment now generally available<!-- 24973562 -->

Now generally available, *await final configuration* enables a locked experience at the end of Setup Assistant to ensure that critical device configuration policies are installed on devices. The locked experience works on devices targeted with new and existing enrollment profiles, enrolling via one of these authentication methods:

- Setup Assistant with modern authentication
- Setup Assistant (legacy)
- Without user device affinity

Applies to:

- macOS 10.11 and later

For information about how to enable await final configuration, see [Create an Apple enrollment policy](../../device-enrollment/apple/setup-automated-macos.md#create-an-enrollment-policy).

### Device management

#### AOSP devices check for new tasks and notifications approximately every 15 minutes<!-- 8506468 -->

On devices enrolled with Android (AOSP) management, Intune attempts to check for new tasks and notifications approximately every 15 minutes. To use this feature, devices must be using the Intune app version 24.02.4 or newer.

Applies to:

- Android (AOSP)

For more information, see:

- [How to use Intune in environments without Google Mobile Services](../../app-management/manage-without-gms.md#some-tasks-can-be-delayed)
- [Policy refresh intervals in Intune](../../device-configuration/troubleshoot-device-profiles.md#policy-refresh-intervals)

#### New device management experience for Government clouds in Microsoft Intune<!-- 17585897 23692982 -->

In government clouds, there's a new device management experience in the Intune admin center. The **Devices** area now has a more consistent UI, with more capable controls and an improved navigation structure so you can find what you need faster.

If you want to try the new experience before your tenant is updated, go to **Devices** > **Overview**, select the **Preview upcoming changes to Devices and provide feedback** notification banner, and select **Try it now**.

#### Bulk approval of drivers<!-- 14723288 -->

Bulk actions are now available for Windows Driver update policies. With bulk actions, multiple driver updates can be approved, paused, or declined at the same time, saving time and effort.

When you bulk approve drivers, the date for when the drivers become available to applicable devices can also be set, enabling drivers to be installed together.

Applies to:

- Windows 10
- Windows 11

For more information, see [Bulk driver updates](../../device-updates/windows/configure-driver-update-policy.md#bulk-driver-updates).

#### App Control for Business policy limitation is resolved<!-- 19548950 -->

A previously documented limitation for App Control for Business policy (WDAC), that limited the number of active policies per device to 32, is resolved by Windows. The issue involves a potential [Boot stop failure when more than 32 policies are active](/windows/security/application-security/application-control/windows-defender-application-control/operations/known-issues#boot-stop-failure-blue-screen-occurs-if-more-than-32-policies-are-active) on a device.

This issue is resolved for devices that run Windows 10 1903 or later with a Windows security update released on or after March 12, 2024. Older versions of Windows can expect to receive this fix in future Windows security updates.

Applies to:

- Windows 10 version 1903 and later

To learn more about App Control for Business policy for Intune, see [Manage approved apps for Windows devices with App Control for Business policy and Managed Installers for Microsoft Intune](../../device-configuration/endpoint-security/manage-app-control.md).

### Tenant administration

#### Customization pane support for excluding groups<!-- 17654599 -->

The Customization pane now supports selecting groups to exclude when assigning policies. You can find this setting in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Customization**.

For more information, see [Assign policies in Microsoft Intune](../../device-configuration/assign-device-profile.md).

## Week of January 29, 2024

### Microsoft Intune Suite

#### Microsoft Intune Enterprise Application Management<!-- 10986080 -->

Enterprise Application Management provides an Enterprise App Catalog of Win32 applications that are easily accessible in Intune. You can add these applications to your tenant by selecting them from the Enterprise App Catalog. When you add an Enterprise App Catalog app to your Intune tenant, default installation, requirements, and detection settings are automatically provided. You can modify these settings as well. Intune hosts Enterprise App Catalog apps in Microsoft storage.

For more information, see:

- [Use Intune Suite add-on capabilities](../../fundamentals/add-ons.md)
- [Microsoft Intune Enterprise Application Management](../../app-management/deployment/enterprise-app-management.md)
- [Add an Enterprise App Catalog app to Microsoft Intune](../../app-management/deployment/add-enterprise-catalog-app.md)

#### Microsoft Intune Advanced Analytics<!--25194145 -->

Intune Advanced Analytics provides comprehensive visibility of the end-user experience in your organization and optimizes it with data driven insights. It includes near real-time data about your devices with Device query, increased visibility with custom device scopes, a battery health report and a detailed device timeline for troubleshooting device issues, and anomaly detection to help identify potential vulnerabilities or risks across your device estate.

- **Battery health report**<!-- 9747162 -->

  The battery health report provides visibility into the health of batteries in your organization's devices and its influence on user experience. The scores and insights in this report are aimed to help IT admins with asset management and purchase decisions that improve user experience while balancing hardware costs.

- **Run on-demand device queries on single devices**<!-- 16719466 -->

  Intune allows you to quickly gain on-demand information about the state of your device. When you enter a query on a selected device, Intune runs a query in real time.

  The data returned can then be used to respond to security threats, troubleshoot the device, or make business decisions.

  Applies to:

  - Windows devices

Intune Advanced Analytics is part of the Microsoft Intune Suite. For added flexibility, this new set of capabilities, together with the existing Advanced Analytics features, is also now available as an individual add-on to Microsoft subscriptions that include Intune.

To use Device query and battery health report in your tenant, or any of the existing Advanced Analytics capabilities, you must have a license for either:

- The Intune Advanced Analytics add-on
- The Microsoft Intune Suite add-on

For more information, see:

- [Use Intune Suite add-on capabilities](../../fundamentals/add-ons.md)
- [Microsoft Intune Advanced Analytics](../../advanced-analytics/index.md)
- [Battery health](../../advanced-analytics/battery-health.md)
- [Device query](../../advanced-analytics/device-query.md)

## Week of January 22, 2024 (Service release 2401)

### App management

#### Install DMG and PKG apps up to 8 GB in size on managed Macs<!-- 25766031 -->

The size-limit of DMG and PKG apps that can be installed using Intune on managed Macs has been increased. The new limit is 8 GB and is applicable to apps (DMG and unmanaged PKG) that are installed using the Microsoft Intune management agent for macOS.

For more information about DMG and PKG apps, see [Add a macOS DMG app to Microsoft Intune](../../app-management/deployment/add-dmg-macos.md) and [Add an unmanaged macOS PKG app to Microsoft Intune](../../app-management/deployment/add-unmanaged-pkg-macos.md).

#### Intune support of store-signed LOB apps for Surface Hub devices<!-- 25865620 -->

Intune now supports the deployment of store-signed LOB apps (single file `.appx`, `.msix`, `.appxbundle`, and `.msixbundle`) to Surface Hub devices. The support for store-signed LOB apps enables offline store apps to be deployed to Surface Hub devices following the retirement of the Microsoft Store for Business.

#### Route SMS/MMS messages to specific app<!-- 24594466 -->

You can configure an app protection policy to determine which SMS/MMS app must be used when the end user intends to send a SMS/MMS message after getting redirected from a policy managed app. When the end user selects on a number with the intent of sending an SMS/MMS message, the app protection settings are used to redirect to the configured SMS/MMS app. This capability relates to the **Transfer messaging data to** setting and applies to both iOS/iPadOS and Android platforms.

For more information, see [iOS app protection policy settings](../../app-management/protection/ref-settings-ios.md) and [Android app protection policy settings](../../app-management/protection/ref-settings-android.md).

#### End user app PIN reset<!-- 24605159 -->

For managed apps that require a PIN to access, allowed end users can now reset the app PIN at any time. You can require an app PIN in Intune by selecting the **PIN for access** setting in iOS/iPadOS and Android app protection policies.

For more information about app protection policies, see [App protection policies overview](../../app-management/protection/overview.md).

#### Maximum app package size<!-- 17546826 -->

The maximum package size for uploading apps to Intune is changed from 8 GB to 30 GB for paid customers. Trial tenants are still restricted to 8 GB.

For more information, see [Win32 app management in Microsoft Intune](../../app-management/deployment/win32.md#prerequisites).

### Device configuration

#### New setting that disables location on Android Enterprise devices<!-- 21060837 -->

On Android Enterprise devices, there's a new setting that allows admins to control the location (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile > Device Restrictions** for profile type > **General**):

- **Location**: **Block** disables the **Location** setting on the device and prevents users from turning it on. When this setting is disabled, then any other setting that depends on the device location is affected, including the **Locate device** remote action. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using location on the device.

Applies to:

- Android Enterprise

For more information on the settings you can configure, see [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../../device-configuration/templates/ref-device-restrictions-android-enterprise.md).

#### Date and time picker for managed software updates in the settings catalog on iOS/iPadOS and macOS devices<!-- 26015175 -->

Using the settings catalog, you can enforce managed updates on iOS/iPadOS and macOS devices by entering a date and time (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type > **Declarative Device Management > Software Update**).

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

For more information about configuring Managed software updates in Intune, see [Use the settings catalog to configure managed software updates](../../device-updates/apple/index.md).

### Device management

#### New device management experience in Microsoft Intune<!-- 17585897 23692982 -->

We're rolling out an update to the device management experience in the Intune admin center. The **Devices** area now has a more consistent UI, with more capable controls and an improved navigation structure so you can find what you need faster. The new experience, previously in public preview, will gradually roll out for general availability over the coming weeks. The public preview experience continues to be available until your tenant receives the update.

The availability of this new admin center experience varies tenant by tenant. While a few will see this update immediately, many might not see the new experience for several weeks. For Government clouds, the availability of this experience is estimated around late February 2024.

Due to the rollout timelines, we're updating our documentation to the new experience as soon as possible to help ease the transition to the new admin center layout. We're unable to provide a side-by-side content experience during this transition and believe providing documentation that aligns to the newer experience brings more value to more customers. If you want to try the new experience and align with doc procedures before your tenant is updated, go to **Devices** > **Overview**, select the notification banner that reads **Preview upcoming changes to Devices and provide feedback**, and select **Try it now**.

#### BlackBerry Protect Mobile now supports app protection policies<!-- 13357196  -->

You can now use Intune app protection policies with *BlackBerry Protect Mobile* (powered by Cylance AI). With this change, Intune supports BlackBerry Protect Mobile for mobile application management (MAM) scenarios for [unenrolled devices](../../device-security/mobile-threat-defense/add-apps-unenrolled-devices.md). This support includes the use of risk assessment with Conditional Access and configuration of Conditional Launch settings for unenrolled devices.

While configuring the CylancePROTECT Mobile connector (formerly BlackBerry Mobile), you now can select options to turn on *App protection policy evaluation* for both Android and iOS/iPadOS devices.

For more information, see [Set up BlackBerry Protect Mobile](../../device-security/mobile-threat-defense/blackberry.md), and [Create Mobile Threat Defense app protection policy with Intune](../../device-security/mobile-threat-defense/create-app-protection-policy.md).

### Device security

#### Support for Intune Defender Update control policies for devices managed by Microsoft Defender for Endpoint<!--25470154 -->

You can now use the endpoint security policy for *Defender Update control* (Antivirus policy) from the Microsoft Intune admin center with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../../device-security/microsoft-defender/security-settings-management.md) capability.

- **Defender Update control** policies are part of endpoint security [Antivirus policy](../../device-configuration/endpoint-security/antivirus.md).

Applies to the following when you use the *Windows 10, Windows 11, and Windows Server* platform:

- Windows 10
- Windows 11

With this support available, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive the policy will get it.

### Intune apps

#### Newly available protected apps for Intune<!-- 25765585, 26137219 -->

The following protected apps are now available for Microsoft Intune:

- PrinterOn Print by PrinterOn, Inc. (iOS/iPadOS)
- Align for Intune by MFB Technologies, Inc. (iOS/iPadOS)

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

### Monitor and troubleshoot

#### Monitoring reports for devices<!-- 17744651 -->

In Intune, you can view a new list of all device monitoring reports. You can find these reports in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Monitor**. The **Monitor** pane provides reports related to configuration, compliance, enrollment, and software updates. Additionally, there are other reports that you can view, such as **Device actions**.

For more information, see [Intune reports](../../device-management/reports/overview.md).

#### Exported report data maintains search results<!-- 17723620 -->

Intune can now maintain your report search and filter results when exporting report data. For example, when you use the [Noncompliant devices and settings](../../device-management/reports/overview.md#noncompliant-devices-report-organizational) report, set the OS filter to "Windows", and search for "PC", the exported data will only contain Windows devices with "PC" in their name. This capability is also available when calling the `ExportJobs` API directly.

#### Easy upload of diagnostic logs for Microsoft Tunnel servers<!-- 15728481 -->

You can now use a single click within the Intune admin center to have Intune enable, collect, and submit eight hours of verbose logs for a Tunnel Gateway Server to Microsoft. The verbose logs can then be referenced while working with Microsoft to identify or resolve issues with a Tunnel server.

In contrast, the collection of verbose logs previously required you to sign on to the server, run manual tasks and scripts to enable and collect verbose logs, and then copy them to a location from which you can transfer them to Microsoft.

To find this new capability, in the admin center go to **Tenant administration** > **Microsoft Tunnel Gateway** > select a server > select the **Logs** tab. On this tab, is a new section named **Send verbose server logs** with button labeled **Send logs**, and a list view that displays the various log sets that have been collected and submitted to Microsoft.

When you select the **Send logs** button:

- Intune captures and submits the current server logs as a baseline, prior to collecting verbose logs.
- Verbose logging is automatically enabled at level 4, and runs for eight hours to provide time to reproduce an issue for capture in those logs.
- After eight hours, Intune submits the verbose logs and then restores the server to its default verbosity level of zero (0), for normal operations. If you previously set logs to run at a higher verbosity level, you can restore your custom verbosity level after log collection and upload is complete.
- Each time Intune collects and submits logs, it updates the list view below the button.
- Below the button is a list of past log submissions, displaying their verbosity level and an Incident ID that you can use when working with Microsoft to reference a specific set of logs.

For more information about this capability, see [Easy upload of diagnostic logs for Tunnel servers](../../device-security/microsoft-tunnel/monitor.md#easy-upload-of-diagnostic-logs-for-tunnel-servers).

## Week of December 11, 2023 (Service release 2312)

### App management

#### Support to add unmanaged PKG-type applications to managed macOS devices is now generally available<!-- 17296091   -->

You can now upload and deploy unmanaged PKG-type applications to managed macOS devices using the Intune MDM agent for macOS devices. This feature enables you to deploy custom PKG installers, such as unsigned apps and component packages. You can add a PKG app in the Intune admin center by selecting **Apps** > **macOS** > **Add** > **macOS app (PKG)** for app type.

Applies to:

- macOS

For more information, see [Add an unmanaged macOS PKG app to Microsoft Intune](../../app-management/deployment/add-unmanaged-pkg-macos.md). To deploy managed PKG-type app, you can continue to [add macOS line-of-business (LOB) apps to Microsoft Intune](../../app-management/deployment/add-lob-macos.md). For more information about the Intune MDM agent for macOS devices, see [Microsoft Intune management agent for macOS](../../app-management/deployment/management-agent-macos.md).

#### Windows MAM supported in government cloud environments and in 21 Vianet in China<!-- 25273622  -->

Customer tenants in US Government Community (GCC), US Government Community (GCC) High, and Department of Defense (DoD) environments are now able to use Windows MAM. For related information, see [Deploying apps using Intune on the GCC High and DoD Environments](../../app-management/deployment/deploy-gcc-dod.md) and [Data protection for Windows MAM](../../app-management/protection/enable-mam-windows.md).

In addition, Windows MAM is available for Intune operated by 21Vianet in China. For more information, see [Intune operated by 21Vianet in China](../../fundamentals/china.md).

### Device configuration

#### Updated security baseline for Microsoft Edge v117<!-- 25021903 -->

We released a new version of the Intune security baseline for **Microsoft Edge**, version [**v117**](../../device-security/security-baselines/overview.md#available-security-baselines). This update brings support for recent settings so you can continue to maintain best-practice configurations for Microsoft Edge.

We also updated our [reference article](../../device-security/security-baselines/ref-v2-edge-settings.md?pivots=edge-v117) for this baseline where you can view the default configuration of the settings this baseline version includes.

### Device management

#### Support for variables in noncompliant email notifications<!-- 6111965  -->

Use variables to personalize email notifications that are sent when a user's device becomes noncompliant. The variables included in the template, such as `{{username}}` and `{{devicename}}`, are replaced by the actual username or device name in the email that users receive. Variables are supported with all platforms.

For more information and a list of supported variables, see [Create a notification message template](../../device-security/compliance/configure-noncompliance-actions.md#create-a-notification-message-template).

#### Updated report visualization for Microsoft Defender for Endpoint connector<!--  24762035  -->

We updated the reporting visualization for the Microsoft Defender for Endpoint connector. This [report visualization](../../device-security/microsoft-defender/configure-integration.md#monitor-device-onboarding-status) displays the count of devices that are onboarded to Defender for Endpoint based on status from the Defender CSP, and visually aligns to other recent report views that use a bar to represent the percentage of devices with different status values.

### Device security

#### New settings for scheduling Antivirus scans added to Antivirus policy for Windows devices<!-- 26013546  -->

We added two settings to the *Microsoft Defender Antivirus* profile for [endpoint security Antivirus policy](../../device-configuration/endpoint-security/antivirus.md#antivirus-profiles) that applies to Windows 10 and Windows 11 devices. These two settings work together to first enable support for a random start time of a device's antivirus scan, and to then define a range of time during which the randomized scan start can begin. These settings are supported with devices managed by Intune and devices managed through the [Defender for Endpoint security settings management](../../device-security/microsoft-defender/security-settings-management.md) scenario.

- [**RandomizeScheduleTaskTimes**](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#admx-microsoftdefenderantivirus-randomizescheduletasktimes) – This setting enables randomization of the scan start time on devices.
- [**SchedulerRandomizationTime**](/windows/client-management/mdm/defender-csp?WT.mc_id=Portal-fx#configurationschedulerrandomizationtime) – With this setting, you can set boundaries for the random start time.

In addition to being added to the Microsoft Defender Antivirus profile, both settings are now available from the [settings catalog](../../device-configuration/settings-catalog/index.md).

Applies to:

- Windows 10
- Windows 11

#### Microsoft Tunnel support for direct proxy exclusion list in VPN profiles for Android Enterprise<!-- 24139621 -->

Intune now supports configuration of a *Proxy exclusion list* when you [configure a VPN profile for Microsoft Tunnel](../../device-security/microsoft-tunnel/install.md#create-a-vpn-profile) for Android devices. With an exclusion list, you can exclude specific domains from your proxy setup without requiring the use of a Proxy Auto-Configuration (PAC) file. The proxy exclusion list is available with both Microsoft Tunnel and Microsoft Tunnel for MAM.

The proxy exclusion list is supported in environments that use a single proxy. The exclusion list isn't suitable or supported when you use multiple proxy servers, for which you should continue to use a `.PAC` file.

Applies to:

- Android Enterprise

#### Microsoft Tunnel server health metric to report on TLS certificate revocation<!-- 25853648  -->

We added a new health metric for Microsoft Tunnel named **TLS certificate revocation**. This new health metric report on the status of the Tunnel Servers TLS certificate by accessing the Online Certificate Status Protocol (OCSP) or CRL address as defined in the TLS certificate. You can view the status of this new check with all the health checks in the Microsoft Intune admin center by navigating to **Tenant administration** > **Microsoft Tunnel Gateway** > **Health status**, selecting a server, and then selecting that servers **Health check** tab.

This metric runs as part of the existing Tunnel Health checks, and supports the following status:

- *Healthy*: The TLS certificate isn't revoked
- *Warning*: Unable to check if the TLS certificate is revoked
- *Unhealthy*: The TLS certificate is revoked, and should be updated

For more information about the TLS certificate revocation check, see [Monitor Microsoft Tunnel](../../device-security/microsoft-tunnel/monitor.md).

### Intune apps

#### Newly available protected app for Intune<!-- 25636619  -->

The following protected app is now available for Microsoft Intune:

- Akumina EXP by Akumina Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

## Week of November 27, 2023

### App management

#### Configure offline caching in Microsoft 365 (Office) for Android devices<!-- 25008682 -->

When the **Save As to Local Storage** setting is set to **blocked** in an [app protection policy](../../app-management/protection/create-policy.md), you can use a configuration key in an app configuration policy to enable or disable offline caching. This setting is only applicable to the Microsoft 365 (Office) app on Android.

For more information, see [Data protection settings in Microsoft 365 (Office)](../../app-management/configuration/configure-microsoft-365-mobile.md#data-protection-settings-in-microsoft-365-office).

#### Win32 app grace period settings on a device<!-- 17644728 -->

On a device where a Win32 app with grace period settings is deployed, low-rights users without administrative privileges can now interact with the grace period UX. Admins on the device continue to be able to interact with the grace period UX on the device.

For more information about grace period behavior, see [Set Win32 app availability and notifications](../../app-management/deployment/win32.md#set-win32-app-availability-and-notifications).

#### Managed Home Screen app configuration additions<!-- 25374056 -->

Now in public preview, Microsoft Managed Home Screen (MHS) is updated to improve the core workflows and user experience. In addition to some user interface changes, there's a new top bar navigation where admins can configure device identifying attributes to be displayed. Additionally, users can access settings, sign in/out, and view notifications when permissions are requested on the top bar.

You can add more settings to configure the Managed Home Screen app for Android Enterprise. Intune now supports the following settings in your Android Enterprise app configuration policy:

- Enable updated user experience
- Top Bar Primary Element
- Top Bar Secondary Element
- Top Bar User Name Style

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../app-management/configuration/configure-managed-home-screen.md).

#### Intune APP SDK for .NET MAUI<!-- 17696301 -->

Using the Intune APP SDK for .NET MAUI, you can develop Android or iOS apps for Intune that incorporate the [.NET Multi-platform App UI](https://dotnet.microsoft.com/apps/maui). Apps developed using this framework allow you to enforce [Intune mobile application management](../../app-management/overview.md). For .NET MAUI support on Android, see [Intune App SDK for .NET MAUI - Android](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android). For .NET MAUI support on iOS, see [Intune App SDK for .NET MAUI - iOS](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS).

## Week of November 13, 2023 (Service release 2311)

### App management

#### New grace period status added in apps for Android, Android AOSP<!-- 13498172 13498291  -->

The Intune Company Portal app for Android and Microsoft Intune app for Android AOSP now show a grace period status for devices that don't meet compliance requirements but are still within their given grace period. Users can see the date by which devices must be compliant, and the instructions for how to become compliant. If users don't update their device by the given date, the device is marked as noncompliant.

For more information, see the following articles:

- [Configure compliance policies with actions for noncompliance](../../device-security/compliance/configure-noncompliance-actions.md#available-actions-for-noncompliance)
- [Check compliance in Intune app for AOSP](../../user-help/compliance/validate-compliance-aosp.md)
- [Check compliance in Company Portal for Android](../../user-help/compliance/validate-compliance-android.md)

### Device configuration

#### New settings available in the Apple settings catalog<!-- 25189345  -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

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

#### Settings to manage Windows Subsystem for Linux are now available in the Windows settings catalog<!-- 17757930  -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place.

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

#### Enrollment for iOS/iPadOS devices in shared device mode now generally available<!-- 25199565   -->

Now generally available to configure in the Microsoft Intune admin center, set up automated device enrollment for iOS/iPadOS devices that are in shared device mode. Shared device mode is a feature of Microsoft Entra that enables your frontline workers to share a single device throughout the day, signing in and out as needed.

For more information, see [Set up enrollment for devices in shared device mode](../../device-enrollment/apple/setup-automated-shared-device-mode.md).

### Device management

#### Improvements to new device experience in admin center (public preview)<!-- 24155098, 25103808, 17705028   -->

We made the following changes to the new Devices experience in the Microsoft Intune admin center:

- More entry points to platform-specific options: Access the platform pages from the **Devices** navigation menu.
- Quick entry to monitoring reports: Select the titles of the metrics cards to go to the corresponding monitoring report.
- Improved navigation menu: We added icons back in to provide more color and context as you navigate.

Flip the toggle in the Microsoft Intune admin center to try out the new experience while it's in public preview and share your feedback.

For more information, see:

- [New Microsoft Intune Devices experience - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/intune-customer-success/new-microsoft-intune-devices-experience/ba-p/3777342)
- [Try new Devices experience - Microsoft Learn](../../fundamentals/public-preview.md)

### Device security

#### Additional settings for the Linux Antivirus policy template<!-- 24191424 -->

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

The Microsoft Defender Antivirus template for Linux is supported for devices [managed by Intune](../../device-configuration/endpoint-security/antivirus.md), and devices managed only by Defender through the [Defender for Endpoint security settings management](../../device-security/microsoft-defender/security-settings-management.md) scenario.

#### Updated security baseline for Microsoft 365 Apps for Enterprise<!-- 25021846   -->

We released a new version of the Intune security baseline for **Microsoft 365 Apps for Enterprise**, version [**2306**](../../device-security/security-baselines/overview.md#available-security-baselines).

The Microsoft 365 Office Apps baseline can help you rapidly deploy configurations to your Office Apps that meet the security recommendations of the Office and security teams at Microsoft. As with all baselines, the default baseline represents the recommended configurations. You can modify the default baseline to meet the requirements of your organization.

We also updated our [reference article](../../device-security/security-baselines/ref-v2-office-settings.md?pivots=v2306) for this baseline where you can view the default configuration of the settings this baseline version includes.

#### Deprecation and replacement of two settings found in the Linux and macOS endpoint security Antivirus policies<!-- 25234740  -->

There are two deprecated settings that in the *Antivirus engine* category of [Microsoft Defender Antivirus](../../device-configuration/endpoint-security/antivirus.md) profiles of both macOS and Linux. These profiles are available as part of Intune's endpoint security Antivirus policies.

For each platform, a single setting replaces the two deprecated settings. This new setting aligns with how Microsoft Defender for Endpoint manages the device configurations.

The following are the two deprecated settings:

- *Enable real-time protection* now appears as *Enable real-time protection (deprecated)*
- *Enable passive mode* now appears as *Enable passive mode (deprecated)*

The new setting that replaces the two deprecated settings:

- *Enforcement level* - By default, Enforcement level is set to *Passive* and supports options of *Real time* and *On demand*.

These settings are also available from the Intune [settings catalog](../../device-configuration/settings-catalog/index.md) for each platform, where the old settings are also marked as deprecated and replaced by the new setting.

With this change, a device that has either of the *deprecated* settings configured will continue to apply that configuration until the device is targeted by the new setting *Enforcement level*. Once targeted by Enforcement Level, the deprecated settings no longer are applied to the device.

The *deprecated* settings will be removed from the Antivirus profiles and the settings catalog in a future update to Intune.

> [!NOTE]
> The changes for Linux are now available. The macOS settings are marked as deprecated, but the *Enforcement level* setting will not be available until December.

Applies to:

- Linux
- macOS

#### Microsoft Defender Firewall profiles are renamed to Windows Firewall<!-- 25171457 -->

To align to Firewall branding changes in Windows, we are updating the names of Intune profiles for endpoint security Firewall policies. In profiles that have *Microsoft Defender Firewall* in the name we're replacing that with *Windows Firewall*.

The following platforms have profiles that are affected, with only the profile names being affected by this change:

- Windows 10 and later (ConfigMgr)
- Windows 10, Windows 11, and Windows Server

#### Endpoint security Firewall policy for Windows Firewall to manage firewall settings for Windows Hyper-V<!--  25767542  -->

We added new settings to the *Windows Firewall* profile (formerly *Microsoft Defender Firewall*) for endpoint security [Firewall policy](../../device-configuration/endpoint-security/firewall.md). The new settings can be used to manage Windows Hyper-V settings. To configure the new settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Endpoint security** > **Firewall** > Platform: **Windows 10, Windows 11, and Windows Server** > Profile: **Windows Firewall**.

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

#### New Endpoint Security Firewall policy profile for Windows Hyper-V Firewall Rules<!-- 10946486  -->

We released a new profile named *Windows Hyper-V Firewall Rules* that you can find through the *Windows 10, Windows 11, and Windows Server* platform path for endpoint security [Firewall policy](../../device-configuration/endpoint-security/firewall.md#devices-managed-by-intune). Use this profile to manage the firewall settings and rules that apply to specific Hyper-V containers on Windows, including applications like the Windows Subsystem for Linux (WSL) and the Windows Subsystem for Android (WSA).

Applies to:

- Windows 10
- Windows 11

### Intune apps

#### Newly available protected apps for Intune<!-- 25417889, 25161990, 25174019  -->

The following protected apps are now available for Microsoft Intune:

- Hey DAN for Intune by Civicom, Inc.
- Microsoft Azure by Microsoft Corporation (iOS)
- KeePassium for Intune by KeePassium Labs (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

## Week of November 6, 2023

### App management

#### Minimum version update for iOS Company Portal<!-- 17964541 -->

Users are required to update to v5.2311.1 of the iOS Company Portal. If you enabled the **[Block installing apps using App Store](../../device-configuration/templates/ref-device-restrictions-apple.md)** device restriction setting, you'll likely need to push an update to the related devices that use this setting. Otherwise, no action is needed.

If you have a helpdesk, you might want to make them aware of the prompt to update the Company Portal app. In most cases, users have app updates set to automatic, so they receive the updated Company Portal app without taking any action. Users that have an earlier app version are prompted to update to the latest Company Portal app.

### Device security

#### Defender for Endpoint security settings management enhancements and support for Linux and macOS are generally available<!-- 24190967 -->

The improvements that were introduced in the Defender for Endpoint security settings management opt-in public preview are now generally available.

With this change, the default behavior for security settings management includes all the behavior added for the opt-in preview – without having to enable support for preview features in Microsoft Defender for Endpoint. This includes the general availability and support for the following endpoint security profiles for Linux and macOS:

**Linux**:

- Microsoft Defender Antivirus
- Microsoft Defender Antivirus exclusions
- Endpoint detection and response

**MacOS**:

- Microsoft Defender Antivirus
- Microsoft Defender Antivirus exclusions
- Endpoint detection and response

For more information, see [Microsoft Defender for Endpoint Security settings management](../../device-security/microsoft-defender/security-settings-management.md) in the Intune documentation.

### Device management

### Feature updates and reports support Windows 11 policies<!--17614166 -->

The new setting on Feature update policies enables an organization to deploy Windows 11 to those devices that are eligible for the upgrade, while ensuring devices not eligible for the upgrade are on the latest Windows 10 feature update with a single policy. As a result, admins don't need to create or manage groups of eligible and non-eligible devices.

For more information on feature updates, see [Feature updates for Windows 10 and later](../../device-updates/windows/manage-feature-updates.md).

## Week of October 30, 2023

### Device security

#### Strict Tunnel Mode in Microsoft Edge available for Microsoft Tunnel for MAM on Android and iOS/iPadOS devices<!--24045412-->

In Intune, you can use the Microsoft Tunnel for mobile application management (MAM) on Android and iOS/iPadOS devices. With the MAM tunnel, unmanaged devices (devices not enrolled in Intune) can access on-premises apps and resources.

There's a new **Strict Tunnel Mode** feature you can configure for Microsoft Edge. When users sign into Microsoft Edge with an organization account, if the VPN isn't connected, then **Strict Tunnel Mode** blocks internet traffic. When the VPN reconnects, internet browsing is available again.

To configure this feature, create a Microsoft Edge app configuration policy, and add the following setting:

- **Key**: `com.microsoft.intune.mam.managedbrowser.StrictTunnelMode`
- **Value**: `True`

Applies to:

- Android Enterprise version 10 and later
- iOS/iPadOS version 14 and later

For more information, see:

- [Microsoft Tunnel for Mobile Application Management](../../device-security/microsoft-tunnel/mam.md)
- [Microsoft Tunnel for MAM - Android](../../device-security/microsoft-tunnel/mam-android.md)
- [Microsoft Tunnel for MAM - iOS/iPadOS](../../device-security/microsoft-tunnel/mam-ios.md)

## Week of October 23, 2023 (Service release 2310)

### App management

#### Update for users of Android Company Portal app<!-- 25109006   -->

If users launch a version of the Android Company Portal app below version 5.0.5333.0 (released November 2021), they'll see a prompt encouraging them to update their Android Company Portal app. If a user with an older Android Company Portal version attempts a new device registration using a recent version of the Authenticator app, the process will likely fail. To resolve this behavior, update the Android Company Portal app.

#### Minimum SDK version warning for iOS devices<!-- 9410239  -->

The **Min SDK version** for the iOS Conditional Launch setting on iOS devices now includes a **warn** action. This action warns end users if the min SDK version requirement isn't met.

For more information, see [iOS app protection policy settings](../../app-management/protection/ref-settings-ios.md).

#### Minimum OS for Apple LOB and store apps<!-- 24623225  -->

You can configure the minimum operating system to be the latest Apple OS releases for both Apple line-of-business apps and iOS/iPadOS store apps. You can set the minimum operating system for Apple apps as follows:

- iOS/iPadOS 17.0 for iOS/iPadOS line-of-business apps
- macOS 14.0 for macOS line-of-business apps
- iOS/iPadOS 17.0 for iOS/iPadOS store apps

Applies to:

- iOS/iPadOS
- macOS

#### Android (AOSP) supports line-of-business (LOB) apps<!-- 24823138   -->

You can install and uninstall mandatory LOB apps on AOSP devices by using the **Required** and **Uninstall** group assignments.

Applies to:

- Android

To learn more about managing LOB apps, see [Add an Android line-of-business app to Microsoft Intune](../../app-management/deployment/add-lob-android.md).

#### Configuration scripts for unmanaged macOS PKG apps<!-- 17745891  -->

You can now configure pre-install and post-install scripts in unmanaged macOS PKG apps. This feature gives you greater flexibility over custom PKG installers. Configuring these scripts is optional and requires the Intune agent for macOS devices v2309.007 or higher.

For more information about adding scripts to unmanaged macOS PKG apps, see [Add an unmanaged macOS PKG app](../../app-management/deployment/add-unmanaged-pkg-macos.md).

### Device configuration

#### FSLogix settings are available in the Settings Catalog and Administrative Templates<!-- 10946920  -->

The [FSLogix settings](/fslogix/reference-configuration-settings) are available in the Settings Catalog and in Administrative Templates (ADMX) for you to configure.

Previously, to configure FSLogix settings on Windows devices, you imported them using the ADMX import feature in Intune.

Applies to:

- Windows 10
- Windows 11

For more information on these features, see:

- [Use the settings catalog to configure settings](../../device-configuration/settings-catalog/index.md)
- [Use Windows templates to configure group policy settings in Microsoft Intune](../../device-configuration/settings-catalog/configure-admx-templates-windows.md)
- [What is FSLogix?](/fslogix/overview-what-is-fslogix)

#### Use delegated scopes in your Managed Google Play apps that configure enhanced permissions on Android Enterprise devices<!-- 14029609  -->

In your Managed Google Play apps, you can give apps enhanced permissions using delegated scopes.

When your apps include delegated scopes, you can configure the following settings in a device configuration profile (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Device Restrictions** for profile type > **Applications**):

- **Allow other apps to install and manage certificates**: Admins can select multiple apps for this permission. The selected apps are granted access to certificate installation and management.
- **Allow this app to access Android security logs**: Admins can select one app for this permission. The selected app is granted access to security logs.
- **Allow this app to access Android network activity logs**: Admins can select one app for this permission. The selected app is granted access to network activity logs.

To use these settings, your Managed Google Play app must use delegated scopes.

Applies to:

- Android Enterprise fully managed devices
- Android Enterprise dedicated devices
- Android Enterprise corporate-owned devices with a work profile

For more information on this feature, see:

- [Android's built-in app configurations](../../developer/app-sdk/android-phase-6.md#androids-built-in-app-configurations)
- [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune > Applications](../../device-configuration/templates/ref-device-restrictions-android-enterprise.md)

#### Samsung ended support for kiosk mode on Android device administrator (DA) devices<!-- 24810356  -->

Samsung marked the Samsung Knox kiosk APIs used on Android device administrator as deprecated in Knox 3.7 (Android 11).

Though the functionality might continue to work, there's no guarantee that it will continue working. Samsung won't fix bugs that might arise. For more information on Samsung support for deprecated APIs, see [What kind of support is offered after an API is deprecated?](https://docs.samsungknox.com/dev/knox-sdk/faqs/general/deprecated-api-support-change.htm) (opens Samsung's web site).

Instead, you can manage kiosk devices with Intune using [dedicated device management](../../device-enrollment/android/setup-dedicated.md).

Applies to:

- Android device administrator (DA)

#### Import and export settings catalog policies<!-- 3470151  -->

The Intune [settings catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure, and all in one place (**Devices** > **Manage devices** > **Configuration** > **Create** > **New Policy** > Select your **platform** > For **Profile type**, select **Settings catalog**).

The settings catalog policies can be imported and exported:

- To export an existing policy, select the profile > select the ellipsis > **Export JSON**.
- To import a previously exported settings catalog policy, select **Create** > **Import policy** > select the previously exported JSON file.

For more information about the settings catalog, see [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../../device-configuration/settings-catalog/index.md).

> [!NOTE]
>
> This feature is continuing to roll out. It may be a couple of weeks before it's available in your tenant.

#### New setting to block users from using the same password to unlock the device and access the work profile on Android Enterprise personally owned devices with a work profile<!-- 6167371  -->

On Android Enterprise personally owned devices with a work profile, users can use the same password to unlock the device and access the work profile.

There's a new setting that can enforce different passwords to unlock the device and access the work profile (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** > **Personally Owned Work Profile** for platform > **Device Restrictions** for profile type):

- **One lock for device and work profile**: **Block** prevents users from using the same password for the lock screen on the device and work profile. End users are required to enter the device password to unlock the device and enter their work profile password to access their work profile. When set to **Not Configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to access their work profile using a single password.

This setting is optional and doesn't impact existing configuration profiles.

Currently, if the work profile password doesn't meet the policy requirements, then device users see a notification. The device isn't marked as non-compliant. A separate compliance policy for the work profile is being created and will be available in a future release.

Applies to:

- Android Enterprise personally owned devices with a work profile (BYOD)

For a list of settings you can configure on personally owned devices with a work profile, see [Android template device settings list to restrict features using Intune](../../device-configuration/templates/ref-device-restrictions-android-enterprise.md).

#### New settings available in the macOS settings catalog<!-- 24950434  -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** > **Settings catalog** for profile type.

**Privacy > Privacy Preferences Policy Control**:

- System Policy App Data

**Restrictions**:

- Force On Device Only Dictation

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

### Device enrollment

#### Web based device enrollment with JIT registration for personal iOS/iPadOS devices<!-- 15412485  -->

Intune supports web-based device enrollment with just in time (JIT) registration for personal devices set up via Apple device enrollment. JIT registration reduces the number of authentication prompts shown to users throughout the enrollment experience and establishes SSO across the device. Enrollment takes place on the web version of Intune Company Portal, eliminating need for the Company Portal app. Also, this enrollment method enables employees and students without managed Apple IDs to enroll devices and access volume-purchased apps.

For more information, see [Set up web based device enrollment for iOS](../../device-enrollment/apple/setup-web-based-ios.md).

### Device management

#### Updates to the Intune add-ons page<!--17395941 -->

The Intune add-ons page under **Tenant administration** includes **Your add-ons**, **All add-ons**, and **Capabilities**. It provides an enhanced view into your trial or purchased licenses, the add-on capabilities you're licensed to use in your tenant, and support for new billing experiences in Microsoft admin center.

For more information, see [Use Intune Suite add-ons capabilities](../../fundamentals/add-ons.md).

#### Remote Help for Android is now Generally available<!--17675897 -->

Remote Help is generally available for Android Enterprise Dedicated devices from Zebra and Samsung.

With Remote Help, IT Pros can remotely view the device screen and take full control in both attended and unattended scenarios, to diagnose and resolve issues quickly and efficiently.

Applies to:

- Android Enterprise Dedicated devices, manufactured by Zebra or Samsung

For more information, see [Remote Help on Android](../../remote-help/index.md).

### Device security

#### Configure declarative software updates and passcode policies for Apple devices in the Settings Catalog<!-- 24989083  -->

You can manage software updates and passcode using Apple's declarative device management (DDM) configuration using the settings catalog (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type > **Declarative device management**).

For more information about DDM, see [Apple's declarative device management (DDM)](https://developer.apple.com/documentation/devicemanagement/leveraging_the_declarative_management_data_model_to_scale_devices) (opens Apple's website).

DDM allows you to install a specific update by an enforced deadline. The autonomous nature of DDM provides an improved user experience as the device handles the entire software update lifecycle. It prompts users that an update is available and also downloads, prepares the device for the installation, & installs the update.

In the settings catalog, the following declarative software update settings are available at **Declarative device management > Software Update**:

- **Details URL**: The web page URL that shows the update details. Typically, this URL is a web page hosted by your organization that users can select if they need organization-specific help with the update.
- **Target Build Version**: The target build version to update the device to, like `20A242`. The build version can include a supplemental version identifier, like `20A242a`. If the build version you enter isn't consistent with the **Target OS Version** value you enter, then the **Target OS Version** value takes precedence.
- **Target Local Date Time**: The local date time value that specifies when to force install the software update. If the user doesn't trigger the software update before this time, then the device force installs it.
- **Target OS Version**: The target OS version to update the device to. This value is the OS version number, like `16.1`. You can also include a supplemental version identifier, like `16.1.1`.

For more information on this feature, see [Manage software updates with the settings catalog](../../device-updates/apple/index.md).

In the settings catalog, the following declarative passcode settings are available at **Declarative device management > Passcode**:

- **Automatic Device Lock**: Enter the maximum time period that a user can be idle before the system automatically locks the device.
- **Maximum Grace Period**: Enter the maximum time period that a user can unlock the device without a passcode.
- **Maximum Number of Failed Attempts**: Enter the maximum number of wrong passcode attempts before:
  - iOS/iPadOS wipes the device
  - macOS locks the device
- **Minimum Passcode Length**: Enter the minimum number of characters a passcode must have.
- **Passcode Reuse Limit**: Enter the number of previously used passcodes that can't be used.
- **Require Complex Passcode**: When set to **True**, a complex passcode is required. A complex passcode doesn't have repeated characters, and doesn't have increasing or decreasing characters, like `123` or `CBA`.
- **Require Passcode on Device**: When set to **True**, the user must set a passcode to access the device. If you don't set other passcode restrictions, then there aren't any requirements about the length or quality of the passcode.

Applies to:

- iOS/iPadOS 17.0 and later
- macOS 14.0 and later

For information about the settings catalog, see [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../../device-configuration/settings-catalog/index.md).

#### Mvision Mobile is now Trellix Mobile Security<!-- 16208061 -->

The Intune [Mobile Threat Defense partner](../../device-security/mobile-threat-defense/overview.md) **Mvision Mobile** has transitioned to **Trellix Mobile Security**. With this change, we've updated our documentation and the Intune admin center UI. For example, the *Mvision Mobile connector* is now *Trellix Mobile Security*. Existing installs of the Mvision Mobile connector also update to Trellix Mobile Security.

If you have questions about this change, reach out to your Trellix Mobile Security representative.

### Intune apps

#### Newly available protected app for Intune<!-- 24920511, 24950232  -->

The following protected app is now available for Microsoft Intune:

- BuddyBoard by Brother Industries, LTD
- Microsoft Loop by Microsoft Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

### Monitor and troubleshoot

#### Updated reports for Policy compliance and Setting compliance are now generally available<!-- 24299948, 24299945  -->

The following device compliance reports are out of public preview and are now generally available:

- [Policy compliance](../../device-management/reports/overview.md#policy-compliance-report-organizational)
- [Setting compliance](../../device-management/reports/overview.md#settings-compliance--organizational)

With this move to general availability, the older versions of both reports have been retired from the Intune admin center and are no longer available.

For more information about these changes, see the Intune Support Team blog at [https://aka.ms/Intune/device_compl_report](https://aka.ms/Intune/device_compl_report).

### Tenant administration

#### Intune admin center home page update<!-- 16950040  -->

The Intune admin center home page has been redesigned with a fresh new look and more dynamic content. The **Status** section has been simplified. You can explore Intune related capabilities in the **Spotlight** section. The **Get more out of Intune** section provides links to the Intune community and blog, and Intune customer success. Also, the **Documentation and training** section provides links to **What's New in Intune**, **Feature in development**, and more training. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Home**.

### Microsoft Intune Suite

#### Remote Help

Version: 5.0.1311.0

- Disabled the relaying of system audio from the Sharer device to the Helper device, which caused an echo when both users were using another app to communicate (such as Teams).
- Added the capability for Helpers that have elevation permissions to also be able to elevate apps on devices where the Sharer is an Administrator.

## Week of October 16, 2023

### Tenant administration

#### `endpoint.microsoft.com` URL redirects to `intune.microsoft.com`<!-- 25169925 -->

Previously, it was announced that the Microsoft Intune admin center has a new URL (`https://intune.microsoft.com`).

The `https://endpoint.microsoft.com` URL now redirects to `https://intune.microsoft.com`.

## Week of September 18, 2023 (Service release 2309)

### App management

#### MAM for Windows general availability<!-- 12394345, 12394352 -->

You can now enable protected MAM access to org data via Microsoft Edge on personal Windows devices. This capability uses the following functionality:
- Intune Application Configuration Policies (ACP) to customize the org user experience in Microsoft Edge
- Intune Application Protection Policies (APP) to secure org data and ensure the client device is healthy when using Microsoft Edge
- Windows Security Center threat defense integrated with Intune APP to detect local health threats on personal Windows devices
- Application Protection Conditional Access to ensure the device is protected and healthy before granting protected service access via Microsoft Entra ID.

Intune Mobile Application Management (MAM) for Windows is available for Windows 11, build 10.0.22621 (22H2) or later. This feature includes the supporting changes for Microsoft Intune (2309 release), Microsoft Edge (v117 stable branch and later) and Windows Security Center (v 1.0.2309.xxxxx and later). App Protection Conditional Access is in Public Preview.

Sovereign cloud support is expected in the future. For more information, see [App protection policy settings for Windows](../../app-management/protection/ref-settings-windows.md).

### Device configuration

#### OEMConfig profiles that don't deploy successfully aren't shown as "pending"<!-- 24284049 -->

For Android Enterprise devices, you can create a configuration policy that configures the OEMConfig app (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **OEMConfig** for profile type).

Previously, OEMConfig profiles that exceed 350 KB show a "pending" state. This behavior changed. An OEMConfig profile that exceeds 350 KB isn't deployed to the device. Profiles in a pending state or profiles larger that 350 KB aren't shown. Only profiles that successfully deploy are shown.

This change is a UI change only. No changes are made to the corresponding Microsoft Graph APIs.

To monitor the profile pending status in the Intune admin center, go to **Devices** > **Manage devices** > **Configuration** > Select the profile > **Device status**.

Applies to:

- Android Enterprise

For more information on OEM Configuration, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../../device-configuration/templates/configure-oemconfig-android.md).

#### Config Refresh settings are in the settings catalog for Windows Insiders<!-- 15060174  -->

In the Windows Settings Catalog, you can configure **Config Refresh**. This feature lets you set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check in to Intune.

Config Refresh:

- Enable config refresh
- Refresh cadence (minutes)

Applies to:

- Windows 11

For more information on the Settings Catalog, see [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../../device-configuration/settings-catalog/index.md).

#### Managed Settings now available in the Apple settings catalog<!-- 21083384  -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place.

The settings within the Managed Settings command are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** > **Settings catalog** for profile type.

**Managed Settings > App Analytics**:

- Enabled: If true, enable sharing app analytics with app developers. If false, disable sharing app analytics.

Applies to:

- Shared iPad

**Managed Settings > Accessibility Settings**:

- Bold Text Enabled
- Grayscale Enabled
- Increase Contrast Enabled
- Reduce Motion Enabled
- Reduce Transparency Enabled
- Text Size
- Touch Accommodations Enabled
- Voice Over Enabled
- Zoom Enabled

**Managed Settings > Software Update Settings**:

- Recommendation Cadence: This value defines how the system presents software updates to the user.

**Managed Settings > Time Zone**:

- Time Zone: The Internet Assigned Numbers Authority (IANA) time zone database name.

Applies to:

- iOS/iPadOS

**Managed Settings > Bluetooth**:

- Enabled: If true, enable the Bluetooth setting. If false, disable the Bluetooth setting.

**Managed Settings > MDM Options**:

- Activation Lock Allowed While Supervised: If true, a supervised device registers itself with Activation Lock when the user enables Find My.

Applies to:

- iOS/iPadOS
- macOS

For more information on these settings, see [Apple's developer website](https://developer.apple.com/documentation/devicemanagement/settingscommand/command/settings). For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

#### New settings available in the macOS settings catalog<!-- 24809885  -->

The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place.

There's a new setting in the Settings Catalog. To see this setting, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** > **Settings catalog** for profile type.

**Microsoft Defender > Cloud delivered protection preferences**:

- Cloud Block Level

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

#### Intune integration with the Zebra Lifeguard Over-the-Air service is generally available<!-- 16238201  -->

Microsoft Intune supports integration with Zebra Lifeguard Over-the-Air service, which allows you to deliver OS updates and security patches over-the-air to eligible Zebra devices that are enrolled with Intune. You can select the firmware version you want to deploy, set a schedule, and stagger update downloads and installs. You can also set minimum battery, charging status, and network conditions requirements for when the update can happen.

This integration is now generally available for Android Enterprise Dedicated and Fully Managed Zebra devices that are running Android 8 or later. It also requires a Zebra account and Intune Plan 2 or Microsoft Intune Suite.

Previously, this feature was in public preview and free for use. With this release as generally available, this solution now requires an add-on license for its use.

For licensing details, see [Intune add-ons](../../fundamentals/add-ons.md).

### Device enrollment

#### SSO support during enrollment for Android Enterprise fully managed and corporate-owned devices with a work profile<!-- 8080357 -->

Intune supports single sign-on (SSO) on Android Enterprise devices that are fully managed or corporate-owned with a work profile.  With the addition of SSO during enrollment, end users enrolling their devices only need to sign in once with their work or school account.


Applies to:

- Android Enterprise corporate owned devices with a work profile
- Android Enterprise fully managed

For more information on these enrollment methods, see:

- [Set up Intune enrollment of Android Enterprise corporate-owned devices with work profile](../../device-enrollment/android/setup-corporate-work-profile.md)
- [Set up enrollment for Android Enterprise fully managed devices](../../device-enrollment/android/setup-fully-managed.md)

### Device management

#### Introducing Remote Help on macOS<!--12454029 -->

The Remote Help web app allows users to connect to macOS devices and join a view-only remote assistance session.

Applies to:

- 11 Big Sur
- 12 Monterey
- 13 Ventura

For more information on Remote Help on macOS, see [Remote Help](../../remote-help/index.md).

#### Management certificate expiration date<!-- 17648747  -->

Management certificate expiration date is available as a column in the **Devices** workload. You can filter on a range of expiration dates for the management certificate and also export a list of devices with an expiration date matching the filter.

This information is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **All devices**.

#### Windows Defender Application Control (WDAC) references are updated to App Control for Business<!-- 24863807  -->

Windows renamed *Windows Defender Application Control* (WDAC) as *App Control for Business*. With this change, the references in Intune docs and the Intune admin center are updated to reflect this new name.

#### Intune supports iOS/iPadOS 15.x as the minimum version<!-- 24161619 -->

Apple released iOS/iPadOS version 17. Now, the minimum version supported by Intune is iOS/iPadOS 15.x.

Applies to:

- iOS/iPadOS

> [!NOTE]
>
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

#### Government tenant support for endpoint security Application Control policy and managed installer<!-- 24850055   -->

We've added support to use endpoint security [Application Control policies](../../device-configuration/endpoint-security/manage-app-control.md), and to configure a managed installer, to the following sovereign cloud environments:

- US Government clouds
- 21Vianet in China

Support for Application Control policy and managed installers was originally released in preview in June 2023. Application Control policies in Intune are an implementation of Defender Application Control (WDAC).

### Device security

#### Endpoint Privilege Management support for Windows 365 devices<!-- 17016794  -->

You can now use [Endpoint Privilege Management](../../epm/overview.md) to manage application elevations on Windows 365 devices (also known as Cloud PCs).

This support doesn't include Azure Virtual Desktop.

#### Elevation report by Publisher for Endpoint Privilege Management<!--  24593400  -->

We've released a new report named **Elevation report by Publisher** for Endpoint Privilege Management (EPM). With [this new report](../../epm/monitor-reports.md#elevation-report-by-publisher) you can view all managed and unmanaged elevations, which are aggregated by the publisher of the app that is elevated.

You'll find the report in the Report node for EPM in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Navigate to **Endpoint security** > **Endpoint Privilege Management** and then select the **Reports** tab.

#### macOS support with Intune Endpoint security policies for Endpoint detection and response<!--  17757981 -->

Intune Endpoint security policies for *Endpoint detection and response* (EDR) now support macOS. To enable this support, we've added a new [EDR template profile for macOS](../../device-configuration/endpoint-security/deploy-edr.md#supported-platforms-and-profiles). Use this profile with macOS devices enrolled with Intune and macOS devices managed through the opt-in public preview of the [Defender for Endpoint security settings management](../../device-security/microsoft-defender/security-settings-management.md?pivots=mdssc-preview) scenario.

The EDR template for macOS includes the following settings for the *Device tags* category from Defender for Endpoint:

- **Type of  tag** – The GROUP tag, tags the device with the specified value. The tag is reflected in the admin center on the device page and can be used for filtering and grouping devices.
- **Value of tag** - Only one value per tag can be set. The Type of a tag is unique and shouldn't be repeated in the same profile.

To learn more about Defender for Endpoint settings that are available for macOS, see [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences#device-tags) in the Defender documentation.

#### Linux support with Intune Endpoint security policies for Endpoint detection and response<!--  17757972  -->

Intune Endpoint security policies for *Endpoint detection and response* (EDR) now support Linux. To enable this support, we've added a new [EDR template profile for Linux](../../device-configuration/endpoint-security/deploy-edr.md#supported-platforms-and-profiles). Use this profile with Linux devices enrolled with Intune and Linux devices managed through the opt-in public preview of the [Defender for Endpoint security settings management](../../device-security/microsoft-defender/security-settings-management.md?pivots=mdssc-preview) scenario.

The EDR template for Linux includes the following settings for the *Device tags* category from Defender for Endpoint:

- **Value of tag** - Only one value per tag can be set. The Type of a tag is unique and shouldn't be repeated in the same profile.
- **Type of tag** – The GROUP tag, tags the device with the specified value. The tag is reflected in the admin center on the device page and can be used for filtering and grouping devices.

You can learn more about Defender for Endpoint settings that are available for Linux in [Set preferences for Microsoft Defender for Endpoint on Linux](/microsoft-365/security/defender-endpoint/linux-preferences#device-tags) in the Defender documentation.

### Monitor and troubleshoot

#### Updated reports for Windows update rings policies<!-- 10159960 -->

Reporting for Windows update rings policies has been updated to use Intune's improved reporting infrastructure. These changes align to similar improvements introduced for other Intune features.

With this change for reports for Windows update rings, when you select an update rings policy in the Intune admin center, there isn't a left-pane navigation for *Overview*, *Manage*, or *Monitor* options. Instead, the policy view opens to a single pane that includes the following policy details:

- **Essentials**: including the policy name, created and modified dates, and more details.
- **Device and user check-in status**: This view is the default report view and includes:
  - A high-level overview of device status for this policy, and a *View report* button to open a more comprehensive report view.
  - A streamlined representation and count of the different device status values returned by devices assigned to the policy. The simplified bar and chart replace former doughnut charts seen in the prior reporting representation.
- Two other report tiles to open more reports. These tiles include:
  - **Device assignment status**: This report combines the same information as the previous Device status and User status reports, which are no longer available. However, with this change, pivots and drill-in through based on the user name is no longer available.
  - **Per setting status**: This new report provides success metrics for each setting configured differently than the defaults, allowing for new insight to which settings might not be successfully deploying to your organization.
- **Properties**: View details for each configuration page of the policy, including an option to **Edit** each areas profile details.

For more information, see [Reports for update rings policies](../../device-updates/windows/monitor-update-rings.md).

### Role-based access

#### Updating the scope of UpdateEnrollment<!--25077072 -->

With the introduction of a new role **UpdateEnrollment**, the scope of **UpdateOnboarding** is getting updated.

The **UpdateOnboarding** setting for custom and built-in roles is modified to only manage or change the Android Enterprise binding to Managed Google Play and other account-wide configurations. Any built-in roles that used **UpdateOnboarding** will now have **UpdateEnrollmentProfiles** included.

The resource name is being updated from **Android for work** to **Android Enterprise**.

For more information, see [Role-based access control (RBAC) with Microsoft Intune](../../fundamentals/role-based-access-control/overview.md).

## Week of September 11, 2023

### Device configuration

#### Introducing Remote Launch on Remote Help<!--9843475 -->

With Remote Launch, the helper can launch Remote Help seamlessly on the helper and user's device from Intune by sending a notification to the user's device. This feature allows both helpdesk and the sharer to be connected to a session quickly without exchanging session codes.

Applies to:

- Windows

For more information, see [Remote Help](../../remote-help/index.md).

## Week of September 4, 2023

### Microsoft Intune Suite

#### Remote Help

Version: 5.0.1045.0

With Remote Launch, the helper can launch Remote Help seamlessly on the helper and sharer's device from Intune by sending a notification to the sharer's device.

### Device management

#### Microsoft Intune ending support for Android device administrator on devices with GMS access in August 2024<!--13891824 -->

Microsoft Intune is ending support for [Android device administrator management](../../device-enrollment/android/manage-device-administrator.md) on devices with access to Google Mobile Services (GMS) on August 30, 2024. After that date, device enrollment, technical support, bug fixes, and security fixes will be unavailable.

If you currently use device administrator management, we recommend switching to another Android management option in Intune before support ends.

For more information, see [Ending support for Android device administrator on GMS devices](https://aka.ms/Intune-Android-DA-blog).

## Week of August 28, 2023

### Device configuration

#### Windows and Android support for 4096-bit key size for SCEP and PFX certificate profiles<!--16314561  -->

Intune [SCEP certificate profiles](../../device-configuration/certificates/scep-profiles.md) and [PKCS certificate profiles](../../device-configuration/certificates/pkcs-profiles.md) for Windows and Android devices now support a **Key size (bits)** of **4096**. This key size is available for new profiles and existing profiles you choose to edit.

- SCEP profiles have always included the *Key size (bits)* setting and now support 4096 as an available configuration option.
- PKCS profiles don't include the *Key size (bits)* setting directly. Instead, an admin must [modify the certificate template on the Certification Authority](../../device-configuration/certificates/pkcs-profiles.md#configure-certificate-templates-on-the-ca) to set the *Minimum key size* to 4096.

If you use a third-party Certificate Authority (CA), you might need to contact your vendor for assistance with implementing the 4096-bit key size.

When updating or deploying new certificate profiles to take advantage of this new key size, we recommend using a staggered deployment approach. This approach can help avoid creating excessive demand for new certificates across a large number of devices at the same time.

With this update, be aware of the following limitations on Windows devices:

- 4096-bit key storage is supported only in the *Software Key Storage Provider* (KSP). The following don't support storing keys of this size:
  - The hardware TPM (Trusted Platform Module). As a workaround you can use the Software KSP for key storage.
  - Windows Hello for Business. There isn't a workaround at this time.

### Tenant administration

#### Access policies for multiple Administrator Approval are now generally available<!-- 24936423   -->

Access policies for multiple Administrator Approval are out of public preview and are now generally available. With these policies, you can protect a resource, like App deployments, by requiring any change to the deployment to be approved by one of a group of users who are *approvers* for the resource, before that change is applied.

For more information, see [Use Access policies to require multiple administrative approval](../../fundamentals/role-based-access-control/multi-admin-approval.md).

## Week of August 21, 2023 (Service release 2308)

### App management

#### Managed Home Screen end-users prompted to grant exact alarm permission<!-- 19804494 -->
Managed Home Screen uses the exact alarm permission to do the following actions:

- Automatically sign out users after a set time of inactivity on the device
- Launch a screen saver after a set period of inactivity
- Automatically relaunch MHS after a certain period of time when a user exits kiosk mode

For devices running Android 14 and higher, by default, the exact alarm permission will be denied. To make sure critical user functionality isn't impacted, end-users are prompted to grant exact alarm permission upon first launch of Managed Home Screen. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../app-management/configuration/configure-managed-home-screen.md) and [Android's developer documentation]( https://developer.android.com/about/versions/14/changes/schedule-exact-alarms).

#### Managed Home Screen notifications<!-- 19805777  -->
For Android devices running Android 13 or higher that target API level 33, by default, applications don't have permission to send notifications. In previous versions of Managed Home Screen, when an admin had enabled automatic relaunch of Managed Home Screen, a notification was displayed to alert users of the relaunch. To accommodate change to notification permission, in the scenario when an admin has enabled auto-relaunch of Managed Home Screen, the application will now display a toast message alerting users of the relaunch. Managed Home Screen is able to auto-grant permission for this notification, so no change is required for admins configuring Managed Home Screen to accommodate the change in notification permission with API level 33. For more information about Android 13 (API level 33) notification messages, see the [Android developer documentation](https://developer.android.com/develop/ui/views/notifications/notification-permission). For more information about Managed Home Screen, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../../app-management/configuration/configure-managed-home-screen.md).

#### New macOS web clip app type<!-- 24128407  -->
In Intune, end users can pin web apps to the dock on your macOS devices (**Apps** > **macOS** > **Add** > **macOS web clip**).

Applies to:

- macOS

For related information about the settings you can configure, see [Add web apps to Microsoft Intune](../../app-management/deployment/add-web.md).

#### Win32 app configurable installation time<!-- 17644704  -->
In Intune, you can set a configurable installation time to deploy Win32 apps. This time is expressed in minutes. If the app takes longer to install than the set installation time, the system will fail the app install. Max timeout value is 1440 minutes (1 day). For more information about Win32 apps, see [Win32 app management in Microsoft Intune](../../app-management/deployment/add-win32.md#step-2-program).

#### Samsung Knox conditional launch check<!-- 8610063   -->
You can add more detection of device health compromises on Samsung Knox devices. Using a conditional launch check within a new Intune App Protection Policy, you can require that hardware-level device tamper detection and device attestation be performed on compatible Samsung devices. For more information, see the **Samsung Knox device attestation** setting in the **Conditional launch** section of [Android app protection policy settings in Microsoft Intune](../../app-management/protection/ref-settings-android.md#device-conditions).

### Device configuration

#### Remote Help for Android in public preview<!-- 16238217 -->
Remote Help is available in public preview for Android Enterprise Dedicated devices from Zebra and Samsung. With Remote Help, IT Pros can remotely view the device screen and take full control in both attended and unattended scenarios, to diagnose and resolve issues quickly and efficiently.

Applies to:

- Android Enterprise Dedicated devices, manufactured by Zebra or Samsung

For more information, see [Remote Help on Android](../../remote-help/index.md).

#### Group Policy analytics is generally available<!-- 24249203  -->
Group Policy analytics is generally available (GA). Use Group Policy analytics to analyze your on-premises group policy objects (GPOs) for their migration to Intune policy settings.

Applies to:

- Windows 11
- Windows 10

For more information about Group Policy analytics, see [Analyze your on-premises GPOs using Group Policy analytics in Microsoft Intune](../../device-configuration/import-group-policy-analytics.md).

#### New SSO, login, restrictions, passcode, and tamper protection settings available in the Apple settings catalog<!-- 24335541  -->
The [Settings Catalog](../../device-configuration/settings-catalog/index.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../../device-configuration/settings-catalog/index.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** > **Settings catalog** for profile type.

##### iOS/iPadOS 17.0 and later

**Restrictions**:

- Allow iPhone Widgets On Mac

##### macOS

**Microsoft Defender > Tamper protection**:

- Process's arguments
- Process path
- Process's Signing Identifier
- Process's Team Identifier
- Process exclusions

##### macOS 13.0 and later

**Authentication > Extensible Single Sign On (SSO)**:

- Account Display Name
- Additional Groups
- Administrator Groups
- Authentication Method
- Authorization Right
- Group
- Authorization Group
- Enable Authorization
- Enable Create User At Login
- Login Frequency
- New User Authorization Mode
- Account Name
- Full Name
- Token To User Mapping
- User Authorization Mode
- Use Shared Device Keys

##### macOS 14.0 and later

**Login > Login Window Behavior**:

- Autologin Password
- Autologin Username

**Restrictions**:

- Allow ARD Remote Management Modification
- Allow Bluetooth Sharing Modification
- Allow Cloud Freeform
- Allow File Sharing Modification
- Allow Internet Sharing Modification
- Allow Local User Creation
- Allow Printer Sharing Modification
- Allow Remote Apple Events Modification
- Allow Startup Disk Modification
- Allow Time Machine Backup

**Security > Passcode**:

- Password Content Description
- Password Content Regex

### Device enrollment

#### Just-in-time registration and compliance remediation for iOS/iPadOS Setup Assistant with modern authentication now generally available<!-- 16276610 -->

Just in time (JIT) registration and compliance remediation for Setup Assistant with modern authentication are now out of preview and generally available. With just in time registration, the device user doesn't need to use the Company Portal app for Microsoft Entra registration and compliance checking. JIT registration and compliance remediation are embedded into the user's provisioning experience, so they can view their compliance status and take action within the work app they're trying to access. Also, this establishes single-sign on across the device. For more information about how to set up JIT registration, see [Set up Just in Time Registration](../../device-enrollment/apple/ref-automated-authentication-methods.md).

#### Awaiting final configuration for iOS/iPadOS automated device enrollment now generally available<!-- 17473384  -->
Now generally available, *awaiting final configuration* enables a locked experience at the end of Setup Assistant to ensure that critical device configuration policies install on devices. The locked experience works on devices targeted with new and existing enrollment profiles. Supported devices include:

- iOS/iPadOS 13+ devices enrolling with Setup Assistant with modern authentication
- iOS/iPadOS 13+ devices enrolling without user affinity
- iOS/iPadOS 13+ devices enrolling with Microsoft Entra ID shared mode

This setting is applied once during the out-of-box automated device enrollment experience in Setup Assistant. The device user doesn't experience it again unless they re-enroll their device.  Awaiting final configuration is enabled by default for new enrollment profiles. For information about how to enable awaiting final configuration, see [Create an Apple enrollment policy](../../device-enrollment/apple/setup-automated-ios.md#create-an-apple-enrollment-policy).

### Device management

#### Changes to Android notification permission prompt behavior<!-- 19783177  -->
We've updated how our Android apps handle notification permissions to align with recent changes made by Google to the Android platform.  As a result of Google changes, notification permissions are granted to apps as follows:

- **On devices running Android 12 and earlier**: Apps are permitted to send notifications to users by default.
- **On devices running Android 13 and later**: Notification permissions vary depending on the API the app targets.
  - *Apps targeting API 32 and lower*: Google has added a notification permission prompt that appears when the user opens the app. Management apps can still configure apps so that they're automatically granted notification permissions.
  - *Apps targeting API 33 and higher*: App developers define when the notification permission prompts appear. Management apps can still configure apps so that they're automatically granted notification permissions.

You and your device users can expect to see the following changes now that our apps target API 33:

- **Company Portal used for work profile management**: Users see a notification permission prompt in the personal instance of the Company Portal when they first open it. Users don't see a notification permission prompt in the work profile instance of Company Portal because notification permissions are automatically permitted for Company Portal in the work profile. Users can silence app notifications in the Settings app.
- **Company Portal used for device administrator management**: Users see a notification permission prompt when they first open the Company Portal app.  Users can adjust app notification settings in the Settings app.
- **Microsoft Intune app**: No changes to existing behavior. Users don't see a prompt because notifications are automatically permitted for the Microsoft Intune app.  Users can adjust some app notification settings in the Settings app.
- **Microsoft Intune app for AOSP**: No changes to existing behavior. Users don't see a prompt because notifications are automatically permitted for the Microsoft Intune app.  Users can't adjust app notification settings in the Settings app.

### Device security

#### Defender Update controls to deploy updates for Defender is now generally available<!-- 24666660 -->
The profile **Defender Update controls** for Intune Endpoint security Antivirus policy, which manages update settings for Microsoft Defender, is now generally available. This profile is available for the *Windows 10, Windows 11, and Windows Server* platform. While in public preview, this profile was available for the *Windows 10 and later* platform.

The profile includes settings for the rollout release channel by which devices and users receive Defender Updates that are related to daily security intelligence updates, monthly platform updates, and monthly engine updates.

This profile includes the following settings, which are all directly taken from [Defender CSP - Windows Client Management](/windows/client-management/mdm/policy-csp-Defender).

- Engine Updates Channel
- Platform Updates Channel
- Security Intelligence Updates Channel

These settings are also available from the [settings catalog](../../device-configuration/settings-catalog/index.md) for the *Windows 10 and later* profile.

#### Elevation report by applications for Endpoint Privilege Management<!-- 24593324 -->
We've released a new report named **Elevation report by applications** for Endpoint Privilege Management (EPM). With [this new report](../../epm/monitor-reports.md#elevation-report-by-applications) you can view all managed and unmanaged elevations, which are aggregated by the application that elevated. This report can aid you in identifying applications that might require elevation rules to function properly, including rules for child processes.

You'll find the report in the Report node for EPM in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Navigate to **Endpoint security** > **Endpoint Privilege Management** and then select the **Reports** tab.

#### New settings available for macOS Antivirus policy<!-- 24191427 -->
The [Microsoft Defender Antivirus](../../device-configuration/endpoint-security/antivirus.md) profile for macOS devices has been updated with nine more settings, and three new settings categories:

**Antivirus engine** – The following settings are new in this category:

- **Degree of parallelism for on-demand scans** – Specifies the degree of parallelism for on-demand scans. This setting corresponds to the number of threads used to perform the scan and impacts the CPU usage, and the duration of the on-demand scan.
- **Enable file hash computation** – Enables or disables file hash computation feature. When this feature is enabled, Windows Defender computes hashes for files it scans. This setting helps improve the accuracy of Custom Indicator matches. However, enabling Enable file hash computation can impact device performance.
- **Run a scan after definitions are updated** – Specifies whether to start a process scan after new security intelligence updates are downloaded on the device. Enabling this setting triggers an antivirus scan on the running processes of the device.
- **Scanning inside archive files** – If true, Defender unpacks archives and scan files inside them. Otherwise archive content is skipped, which improves scanning performance.

**Network protection** – A new category that includes the following setting:

- **Enforcement level** – Configure this setting to specify if network protection is *disabled*, *in audit mode*, or *enforced*.

**Tamper  protection** - A new category that includes the following setting:

- **Enforcement level** - Specify whether tamper protection is *disabled*, in *audit mode*, or *enforced*.

**User interface preferences** – A new category that includes the following settings:

- **Control sign-in to consumer version** - Specify whether users can sign into the consumer version of Microsoft Defender.
- **Show / hide status menu icon** – Specify whether the status menu icon (shown in the top-right corner of the screen) is hidden or not.
- **User initiated feedback** – Specify whether users can submit feedback to Microsoft by going to *Help* > *Send Feedback*.

New profiles that you create include the original settings and the new settings. Your existing profiles automatically update to include the new settings, with each new setting set to *Not configured* until you choose to edit that profile to change it.

For more information about how to set preferences for Microsoft Defender for Endpoint on macOS in enterprise organizations, see [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences?view=o365-worldwide&preserve-view=true).

### Intune apps

#### Newly available protected app for Intune<!-- 24400497  -->
The following protected app is now available for Microsoft Intune:

- VerityRMS by Mackey LLC (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../../app-management/ref-protected-apps.md).

### Monitor and troubleshoot

#### CloudDesktop log now collected with Windows diagnostics data<!-- 24541366 -->
The Intune remote action to [collect diagnostics](../../device-management/actions/collect-diagnostics.md) from a Windows device now includes data in a log file.

Log file:
- %temp%\CloudDesktop\*.log

#### Anomaly detection device cohorts in Intune Endpoint analytics is generally available<!-- 24577118  -->
Anomaly detection device cohorts in Intune Endpoint analytics is now generally available.

Device cohorts are identified in devices associated with a high or medium severity anomaly. Devices are correlated into groups based on one or more factors they have in common like an app version, driver update, OS version, device model. A correlation group will contain a detailed view with key information about the common factors between all affected devices in that group. You can also view a breakdown of devices currently affected by the anomaly and 'at risk' devices. "At risk" devices haven't yet shown symptoms of the anomaly.

For more information, see [Anomalies report](../../advanced-analytics/anomalies.md).

#### Improved user experience for device timeline in Endpoint Analytics<!-- 24604944 -->
The user interface (UI) for device timeline in Endpoint analytics is improved and includes more advanced capabilities (support for sorting, searching, filtering, and exports). When viewing a specific device timeline in Endpoint analytics, you can search by event name or details. You can also filter the events and choose the source and level of events that appear on the device timeline and select a time range of interest.

For more information, see [Device timeline](../../advanced-analytics/device-timeline.md).

#### Updates for compliance policies and reports<!--15425771  -->
We've made several improvements to the Intune compliance policies and reports. With these changes, the reports more closely align to the experience in use for device configuration profiles and reports. We've updated our [compliance report documentation](../../device-security/compliance/monitor-policy.md) to reflect the available compliance report improvements.

Compliance report improvements include:

- Compliance details for Linux devices.
- Redesigned reports that are up-to-date and simplified, with newer report versions beginning to replace older report versions, which will remain available for some time.
- When viewing a policy for compliance, there isn't a left-pane navigation. Instead, the policy view opens to a single pane that defaults to the Monitor tab and its Device status view.
  - This view provides a high-level overview of device status for this policy, supports drilling in to review the full report, and a per-setting status view of the same policy.
  - The doughnut chart is replaced by a streamlined representation and count of the different device status values returned by devices assigned the policy.
  - You can select the Properties tab to view the policy details, and review and edit its configuration and assignments.
  - The *Essentials* section is removed with those details appearing in the policy's *Properties* tab.
- The updated status reports support sorting by columns, the use of filters, and search. Combined, these enhancements enable you to pivot the report to display specific subsets of details you want to view at that time. With these enhancements, we have removed the *User status* report as it has become redundant. Now, while viewing the default *Device status* report you can focus the report to display the same information that was available from *User status* by sorting on the *User Principal Name* column, or searching for a specific username in the search box.
- When viewing status reports, the count of devices that Intune displays now remains consistent between different report views as you drill in for deeper insights or details.

For more information about these changes, see the Intune Support Team blog at [https://aka.ms/Intune/device_compl_report](https://aka.ms/Intune/device_compl_report).

## Week of August 14, 2023

### App management

#### Use the Turn off the Store application setting to disable end user access to Store apps, and allow managed Intune Store apps<!-- 16544362 -->
In Intune, you can use the new **Store app** type to deploy Store apps to your devices.

Now, you can use the **Turn off the Store application** policy to disable end users' direct access to Store apps. When it's disabled, end users can still access and install Store apps from the Windows Company Portal app and through Intune app management. If you want to allow random store app installs outside of Intune, then don't configure this policy.

The previous **Only display the private store within the Microsoft Store app** policy doesn't prevent end users from directly accessing the store using the Windows Package Manager `winget` APIs. So, if your goal is to block random unmanaged Store application installs on client devices, then it's recommended to use the **Turn off the Store application** policy. Don't use the **Only display the private store within the Microsoft Store app** policy.
Applies to:

- Windows 10 and later

For more information, see [Add Microsoft Store Apps to Microsoft Intune](../../app-management/deployment/add-microsoft-store.md).

## Week of August 7, 2023

### Role-based access control

#### Introducing a new role-based access control (RBAC) permission under the resource Android for work<!--11298214 -->
Introducing a new RBAC **Permission** for creating a custom role in Intune, under the resource **Android for work**. The permission **Update Enrollment Profile** allows the admin to manage or change both AOSP and Android Enterprise Device Owner enrollment profiles that are used to enroll devices.

For more information, see [Create custom role](../../fundamentals/role-based-access-control/create-custom-role.md).

## Week of July 31, 2023

### Device security

### New BitLocker profile for Intune's endpoint security Disk encryption policy<!-- 24631986   -->
We have released a new experience creating new *BitLocker* profiles for endpoint security Disk Encryption policy. The experience for editing your previously created BitLocker policy remains the same, and you can continue to use them. This update applies only for the new [BitLocker](../../device-configuration/endpoint-security/disk-encryption.md) policies you create for the *Windows 10 and later* platform.

This update is part of the continuing rollout of new profiles for endpoint security policies, which began in April 2022.

### App management

#### Uninstall Win32 and Microsoft store apps using the Windows Company Portal<!-- 4664389 -->
End-users can uninstall Win32 apps and Microsoft store apps using the Windows Company Portal if the apps were assigned as available and were installed on-demand by the end-users. For Win32 apps, you have the option to enable or disable this feature (off by default). For Microsoft store apps, this feature is always on and available for your end-users. If an app can be uninstalled by the end-user, the end-user will be able to select **Uninstall** for the app in the Windows Company Portal. For related information, see [Add apps to Microsoft Intune](../../app-management/deployment/index.md).