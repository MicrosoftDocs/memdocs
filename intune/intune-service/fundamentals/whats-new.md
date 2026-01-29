---
title: What's new in Microsoft Intune
description: Find out what's new in Microsoft Intune.
author: brenduns
ms.author: brenduns
ms.date: 02/02/2026
ms.topic: whats-new
ms.reviewer: intuner
ms.collection:
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

## Week of February 2, 2026 (Service release 2601)

### Microsoft Intune Suite

#### Endpoint Privilege Management support on Azure Virtual Desktop<!-- 26079227 -->

Endpoint Privilege Management (EPM) elevation policies now support deployment to users on Azure Virtual Desktop (AVD) single-session virtual machines.

For information about using EPM, which is available as an [Intune Suite add-on-capability](../fundamentals/intune-add-ons.md), see [Plan and Prepare for Endpoint Privilege Management Deployment](../protect/epm-plan.md).

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

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

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

To learn more about the settings catalog, see [Use the Intune settings catalog to configure settings](../configuration/settings-catalog.md).

#### New supported OEMConfig apps for Android Enterprise<!-- 35178386 -->

The following OEMConfig apps are available in Intune for Android Enterprise:

- FCNT - Senior Care | `com.fcnt.mobile_phone.seniorcareconfig`
- FCNT - Schema | `com.fcnt.mobile_phone.schematest`
- Sonim | `com.sonim.oemappconfig`

For more information about OEMConfig, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

#### Filter by Android management mode in the settings catalog<!-- 31844205 -->

The [settings catalog](../configuration/settings-catalog.md) includes hundreds of settings that you can configure. There are built-in features that help filter the available settings.

When you create an Android settings catalog policy, there's a management mode filter option that filters the available settings by their enrollment type, including:

- Fully managed
- Corporate-owned work profile
- Dedicated

To learn more about the settings catalog, see:

- [Use the Intune settings catalog to configure settings](../configuration/settings-catalog.md)
- [Android Intune settings catalog settings list](../configuration/settings-catalog-android.md)

#### New updates to the Apple settings catalog<!-- 35787099 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There is a new setting in the Settings Catalog. To see this setting, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Restrictions**:

- Rating Apps Exempted Bundle IDs: This setting lets admins specify apps that can bypass the 17 and older restriction.

  For example, a device can have its content restricted to ages 9 and below. With this restriction, apps with an age-based rating of 17 and older are automatically blocked. Admins can use this setting to allow specific apps to bypass this restriction.

Apple rebranded **Rapid Security Responses** to **Background Security Improvements**. This change is updated in the settings catalog. For more information on Background Security Improvements, see [Background Security Improvements on Apple devices](https://support.apple.com/guide/deployment/background-security-improvements-dep93ff7ea78/web) (opens Apple's web site).

### Device management

#### More options for assignment filters > Device Management Type property for managed apps on Android and iOS/iPadOS<!-- 25040926 -->

When you create policies for your managed apps, you can use [assignment filters](filters.md) to assign policies based on rules you create. In these rules, you can use different device and app properties, including the **Device Management Type** property on Android and iOS/iPadOS.

For Android, the **Device Management Type** property for managed apps is adding the following options:

- Corporate-owned with work profile
- Corporate-owned fully managed
- Corporate-owned dedicated devices without Entra ID Shared mode

For iOS/iPadOS, the **Device Management Type** property for managed apps is adding the following options:

- Automated Device Enrollment user-associated devices
- Automated Device Enrollment userless devices
- Account Driven User Enrollment
- Device Enrollment with Company Portal and Web Enrollment

To learn more about filters, see:

- [Use assignment filters to assign your apps, policies, and profiles in Microsoft Intune](filters.md)
- [App and device properties, operators, and rule editing when creating assignment filters in Microsoft Intune
](filters-device-properties.md)

> [!div class="checklist"]
> Applies to:
>
> - Android
> - iOS/iPadOS

#### Intune certificate inventory integration with Zimperium mobile threat defense<!-- 35519603 -->

You can now configure the Zimperium Mobile Threat Defense (MTD) connector to synchronize certificate inventory from your managed iOS devices. This enhancement helps you identify when a device threat level is elevated due to approved but potentially malicious certificates on the device. The following settings are now available when configuring the connector:

- **Enable Certificate Sync for iOS/iPadOS devices** - Allows this Mobile Threat Defense partner to request a list of installed certificates on iOS/iPadOS devices from Intune to use for threat analysis purposes.
- **Send full certificate inventory data on personally-owned iOS/iPadOS devices** - This setting controls the certificate inventory data that Intune shares with this Mobile Threat Defense partner for personally-owned devices. Data is shared when the partner syncs certificate data and requests the certificate inventory list.

When certificate sync is enabled, the following data is shared:

- Account ID
- Entra ID Device ID
- Device Owner
- Certificate List
  - Common Name
  - Data
  - Is Identity

For more information, see [Mobile Threat Defense toggle options](../protect/mtd-connector-enable.md#mobile-threat-defense-toggle-options).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

### Device security

#### Update firewall configurations for new Intune network endpoints<!-- 34445623 -->

As part of Microsoft’s ongoing [Secure Future Initiative (SFI)]( https://www.microsoft.com/trust-center/security/secure-future-initiative), Microsoft Intune has begun using Azure Front Door (AFD) IP addresses in addition to the existing Intune service IPs.

Starting December 2, 2025, this change supports improved service resiliency and security. As a result, you might need to review and update network (firewall, proxy, or VPN) configurations in third-party applications to ensure proper function of Intune device and app management. This change primarily affects customers who restrict outbound traffic using IP-based allowlists or Azure service tags.

- **If your organization uses FQDN-based rules or does not restrict outbound traffic**, no changes are typically required. However, you should verify that the appropriate wildcard rules are configured, specifically `*.manage.microsoft.com`, to ensure all Intune services remain reachable. Microsoft continues to recommend using FQDN-based rules whenever possible to reduce ongoing administrative overhead.
- **If your organization uses IP-based allowlists** (like firewall, proxy, or VPN rules), you must ensure that the Azure Front Door IP ranges are included to avoid potential connectivity issues for managed devices.

The following IP addresses comprise the current list of Azure Front Door endpoints that should be allowed:

- 13.107.219.0/24
- 13.107.227.0/24
- 13.107.228.0/23
- 150.171.97.0/24
- 2620:1ec:40::/48
- 2620:1ec:49::/48
- 2620:1ec:4a::/47

For the authoritative and up-to-date list of network endpoints required by Intune client and host services, see [Intune core service](../fundamentals/intune-endpoints.md#intune-core-service) in *Network endpoints for Microsoft Intune*.

For additional context on this change, see [Support Tip: Upcoming Microsoft Intune Network Changes](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-upcoming-microsoft-intune-network-changes/4452738).

### Tenant administration

#### Admin tasks in Microsoft Intune are now generally available<!-- 32978931 -->

**Admin tasks** in the Intune admin center are out of public preview and now generally available. Admin tasks provide a centralized view where admins can discover, organize, and act on common tasks that are otherwise spread throughout the Intune admin center. Located under **Tenant Administration**, this unified experience supports search, filtering, and sorting to help you focus on what needs attention, without navigating across multiple nodes.

The following task types are supported:

- Endpoint Privilege Management file elevation requests
- Microsoft Defender security tasks
- Multi Admin Approval requests

Intune only shows tasks you have permission to manage. When you select a task, Intune opens the same interface and workflow you'd use if managing the task from its original location. This ensures a consistent experience whether you're working from the admin tasks node or directly within the source capability.

To learn more, see:

- [Admin tasks](../fundamentals/admin-tasks.md)

## Week of January 12, 2026

### App management

#### PowerShell script installer for Win32 apps <!-- 34496511 -->

When adding a Win32 app, you can upload a PowerShell script to serve as the installer instead of specifying a command line. Intune packages the script with the app content and runs it in the same context as the app installer, enabling richer setup workflows like prerequisite checks, configuration changes, and post-install actions. Installation results appear in the Intune admin center based on the script's return code.

For more information, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

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
   - **Get Started** (macOS 15+)

For more information about available Setup Assistant skipkeys, see:

- [Set up automated device enrollment for iOS/iPadOS]( ../enrollment/device-enrollment-program-enroll-ios.md#setup-assistant-screen-reference)  
- [Set up automated device enrollment for macOS]( ../enrollment/device-enrollment-program-enroll-macos.md#setup-assistant-screen-reference)

## Week of December 1, 2025

### App management

#### Secure enterprise browser managed by Intune (public preview) <!-- 31609121 -->

Microsoft Intune now supports policy management for Microsoft Edge for Business as a secure enterprise browser. By implementing policies through Intune, admins can confidently transition from Windows-based desktop environments to secure, browser-based workflows for accessing corporate resources without requiring device enrollment.

For more information, see [Secure Your Corporate Data in Intune with Microsoft Edge for Business](../apps/mamedge-overview.md).

## Week of November 17, 2025  

### Device enrollment  

#### Configure Windows Backup for Organizations <!--29202026 -->  

*Windows Backup for Organizations* is generally available in Microsoft Intune. With this feature, you can back up your organization's Windows settings and restore them on a Microsoft Entra joined device. Backup settings are configurable in the Microsoft Intune admin center settings catalog, while a tenant-wide setting that lets you restore a device is available in the admin center under **Enrollment**. For more information about this feature, see [Windows Backup for Organizations in Microsoft Intune](../enrollment/windows-backup-restore.md). 

### Device management

#### Security Copilot in Intune agents are available for public preview <!-- 32766422 35360466 35100315 35320958 -->

Security Copilot agents in Intune are AI-powered assistants that specialize in specific scenarios. The Intune agents are available in the Intune admin center > **Agents**, and are available for Security Copilot users.

The following Intune agents are available:

- The **[Change Review Agent](../../agents/change-review-agent.md)** evaluates Multi Admin Approval requests for Windows PowerShell scripts on Windows devices. It provides risk-based recommendations and contextual insights to help admins understand script behavior and associated risks.

  These insights can help Intune admins make informed decisions more quickly about whether to approve or deny requests. This agent supports Intune-managed devices running Windows.

- The **[Device Offboarding Agent](../../agents/device-offboarding-agent.md)** identifies stale or misaligned devices across Intune and Microsoft Entra ID. It provides actionable insights and requires admin approval before offboarding any devices. This agent complements existing Intune automation by showing insights and handling ambiguous cases where automated cleanup isn't enough.

  The agent supports Intune-managed devices running Windows, iOS/iPadOS, macOS, Android, and Linux. During public preview, admins can directly disable Microsoft Entra ID objects, with additional remediation steps provided as guidance.

- The **[Policy Configuration Agent](../../agents/policy-configuration-agent.md)** analyzes uploaded documents or industry benchmarks and automatically identifies matching Intune settings. Admins can upload their requirements, like compliance standards or internal policy documents, and the agent intelligently shows relevant settings from the Intune settings catalog.

  The agent also guides you through policy creation and helps you configure each setting that best suits your organization's needs. This agent supports devices running Windows.

To learn more, see:

- [Security Copilot agents in Intune](../../agents/index.md)

#### Intune support for iVerify as a mobile threat defense partner<!-- 35838315 -->

You can now use iVerify Enterprise as a mobile threat defense partner (MTD) for enrolled devices that run the following platforms:  

- Android 9.0 and later
- iOS/iPadOS 15.0 and later

To learn more about this support, see [Set up iVerify Mobile Threat Defense Connector](../protect/iverify-mobile-threat-defense-connector.md).

### Tenant administration

#### Manage tasks and requests from the centralized Admin tasks node in Microsoft Intune (public preview)<!-- 3542038 -->

The new **Admin tasks** node in the Intune admin center provides a centralized view to discover, organize, and act on security tasks and user elevation requests. Located under **Tenant Administration**, this unified experience supports search, filtering, and sorting to help you focus on what needs attention—without navigating across multiple nodes.

The following task types are supported:

- Endpoint Privilege Management file elevation requests
- Microsoft Defender security tasks
- Multi Admin Approval requests

Intune only shows tasks you have permission to manage. When you select a task, Intune opens the same interface and workflow you'd use if managing the task from its original location. This ensures a consistent experience whether you're working from the admin tasks node or directly within the source capability.

For more information, see [Admin tasks](../fundamentals/admin-tasks.md).

## Week of November 10, 2025 (Service release 2511)

### Microsoft Intune Suite

#### Scope tag enforcement for Endpoint Privilege Management elevation requests<!-- 33479826  -->

When viewing Endpoint Privilege Management [elevation requests](/intune/intune-service/protect/epm-support-approved#about-support-approved-elevations), applicable scope tags are now enforced. This means administrators can view and manage only the requests for devices and users that fall within their assigned scope. This change helps maintain administrative boundaries and strengthen security. Previously, admins with permissions to manage elevation requests could view all elevation requests, regardless of scope.

### App management

#### More volume options available in Managed Home Screen <!-- 16462284 -->

Admins can now enable more volume controls in the Managed Home Screen (MHS) app for Android Enterprise dedicated and fully managed devices. In addition to the existing media volume control, this update introduces configuration settings to show or hide sliders for **call**, **ring and notification**, and **alarm** volumes.

Each new option can be independently enabled through app configuration policies. When turned on, users can adjust these specific volume levels directly from the Managed Settings page within MHS, without leaving kiosk mode. This enhancement provides task workers greater flexibility to manage sound levels for different environments while keeping the device securely locked down.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise (dedicated and fully managed devices)

#### Reset Managed Google Play store mode to Basic <!-- 33632857 -->

You can now reset the Managed Google Play store layout from **Custom** back to **Basic** in the Intune admin center (**Apps** > **All apps** > **Create Managed Google Play app**).

In **Basic** mode, all approved apps are automatically visible to users. In **Custom** mode, newly approved apps must be manually added to collections before they appear in the store. The new **Reset to Basic** button lets admins quickly revert to Basic mode without needing to contact support. When selected, Intune deletes all existing collections and immediately displays a success or failure message.

For more information about Managed Google Play store layout options, see [Approve and deploy Android Enterprise apps in Intune](../apps/apps-add-android-for-work.md).

> [!div class="checklist"]
> Applies to:
>
> - Android

#### Updated Service Level Objectives for Enterprise App Management <!-- 30049867 -->

**Service Level Objectives (SLOs)** are now available in Enterprise App Management (EAM) to provide clearer expectations for when app updates become available in the Enterprise App Catalog. SLO processing timelines begin when Intune first receives the updated app package.

Most app updates complete automated validation within 24 hours. Updates that require manual vendor testing or approval typically complete within seven days.

For more information, see [Enterprise App Management overview](../apps/apps-enterprise-app-management.md).

#### New cut, copy, and paste options for Windows app protection <!-- 25427327 -->

Intune adds two new values to the **Allow cut, copy and paste for** setting in Windows app protection policies (starting with Microsoft Edge) to give admins more control over data movement:

- Org data destinations and any source: Users can paste from any source into the org context, and can cut/copy only to org destinations.  
- Org data destinations and org data sources: Users can cut/copy/paste only within the org context.

These options extend familiar mobile APP data-transfer controls to Windows, helping prevent data leaks on unmanaged devices while preserving productivity. For more information, see [App protection policies overview](../apps/app-protection-policy.md).

> [!div class="checklist"]
> Applies to:
>
>- Windows

### Device configuration

#### Settings available in both Templates and Settings Catalog for Android Enterprise <!-- 34876806 -->

Some settings that were only available in Templates are now also supported in the settings catalog.

The [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

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

To learn more about these settings, see [Android Intune settings catalog settings list](../configuration/settings-catalog-android.md).

Applies to:

- Android Enterprise

#### New Assist Content Sharing setting in the Android Enterprise settings catalog<!-- 31479342 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type):

- **Block assist content sharing with privileged apps**: If **True**, this setting blocks assist content, like screenshots and app details, from being sent to a privileged app, like an assistant app. The setting can be used to block the **Circle to Search** AI feature.

For some guidance on managing AI features on Android devices, see [Manage AI on Android with Intune - A Guide for IT Admins](/intune/solutions/ai/manage-ai-android).

Applies to:

- Android Enterprise corporate-owned devices with a work profile (COPE) > Work profile level
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)

### Device enrollment  

#### New opt-in upgrade allows existing customers to move from managed Google Play accounts to Microsoft Entra ID accounts<!-- 30675087 --> 

Microsoft Intune offers a new opt-in upgrade that allows existing Android Enterprise customers to move from using managed Google Play accounts to using Microsoft Entra ID accounts for Android device management. You are eligible for upgrade if you previously used a consumer Gmail account. This change streamlines the onboarding process by eliminating the need for a separate Gmail account and by leveraging your work account. This change is not required. To learn more about this change, see:

- [New onboarding flow to managing Android Enterprise devices with Microsoft Intune](https://techcommunity.microsoft.com/blog/intunecustomersuccess/new-onboarding-flow-to-managing-android-enterprise-devices-with-microsoft-intune/4206602)
- [Connect your Intune account to your managed Google Play account](../enrollment/connect-intune-android-enterprise.md#upgrade-to-a-managed-google-domain)

#### Incomplete user enrollment report removed <!-- 26395805 -->

The incomplete user enrollments report has been removed and is no longer functional in the Microsoft Intune admin center. The following corresponding APIs have also been removed from Microsoft Intune:  

- getEnrollmentAbandonmentDetailsReport
- getEnrollmentAbandonmentSummaryReport
- getEnrollmentFailureDetailsReport

Scripts or automation using these Graph APIs will stop working now that the report has been removed. In place of this report, we recommend using the enrollment failures report. For more information, see [View enrollment reports](../enrollment/view-enrollment-reports.md#enrollment-failures-report).  

### Device management 

#### Query and results improvements to Explorer feature with Security Copilot in Intune <!--33987602-->

With your Security Copilot license, you can query your Intune data using the **[Explorer in Intune](../copilot/copilot-intune-explorer.md)** feature. 

When you create your queries, you have more filter options. For example:

- Queries with a number operator let you choose equal, greater than, and less than values.
- Queries that forced you to choose one option, like platform, allow you to select multiple options.

In the query results, there are also more columns available to view your data.

To learn more about this feature, see [Explore Intune data with natural language and take action](../copilot/copilot-intune-explorer.md).

#### Device Management Type assignment filter property supports Android enrollment options for Managed Devices<!-- 33016364 -->

When you create a policy in Intune, you can use [assignment filters](filters.md) to assign a policy based on rules you create. You can create a rule using different [properties](filters-device-properties.md), like `deviceManagementType`.

For managed devices, the Device Management Type property supports the following Android enrollment options:

- Corporate-owned dedicated devices with Entra ID Shared mode
- Corporate-owned dedicated devices without Entra ID Shared mode
- Corporate-owned with work profile
- Corporate-owned fully managed
- Personally-owned device with a work profile
- AOSP user-associated devices
- AOSP userless devices

To learn more about assignment filters and the properties you can currently use, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [App and device properties, operators, and rule editing when creating filters in Microsoft Intune](filters-device-properties.md)

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

To learn more, see [Explore Intune data with natural language and take action](../copilot/copilot-intune-explorer.md).

### Device security

#### Microsoft Tunnel access by rooted Android devices is blocked by the Microsoft Defender client<!-- 30336962 -->

Microsoft Tunnel uses the Microsoft Defender client app to provide Android devices access to tunnel. The latest version of the Defender for Endpoint client can now detect when a device is rooted. If a device is determined to be rooted, Defender:

- Marks the device's risk category as *High*
- Immediately drops active Tunnel connections
- Prevents further use of Tunnel until the device is determined to no longer be rooted
- Sends a notification to the device user about the device status

This capability is a feature of the Defender client on Android and doesn't replace the use of Intune compliance policies for Android to manage the settings like *Rooted devices*, *Play Integrity Verdict*, and *Require the device to be at or under the Device Threat Level*.

For more information about features of Microsoft Tunnel, see [Overview of Microsoft Tunnel](/intune/intune-service/protect/microsoft-tunnel-overview#capabiltities).

### Tenant administration

#### Soft-deleted Microsoft Entra groups now visible in Intune <!-- 30035949 -->

This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).

Microsoft Intune now displays soft-deleted Microsoft Entra groups in the Intune admin center. When a group is soft-deleted, its assignments no longer apply. However, if the group is restored, its previous assignments are automatically reinstated.

For more information, see [Include and exclude app assignments in Microsoft Intune](../apps/apps-inc-exl-assignments.md).

## Week of October 20, 2025 (Service release 2510)

### Microsoft Intune Suite

#### Support for user account context in Endpoint Privilege Management Elevation Rules<!-- 25617968 -->

Endpoint Privilege Management (EPM) has a new option for elevation rules that runs the elevated file using the user's context instead of a virtual account. The option is **Elevate as current user**.

With the *Elevate as current user* elevation type, files or processes that are elevated run under the signed-in user's own account, rather than a virtual account. This preserves the user's profile paths, environment variables, and personalized settings, helping to ensure that installers and tools that rely on the active user profile function correctly. Because the elevated process maintains the same user identity before and after elevation, audit trails remain consistent and accurate. Prior to elevation, the user is required to enter their credentials for Windows Authentication. This process supports multifactor authentication (MFA) for enhanced security.

For more information, see [Use Endpoint Privilege Management with Microsoft Intune](../protect/epm-plan.md#important-concepts-for-endpoint-privilege-management).

####  Endpoint Privilege Management Dashboard for user readiness and elevation trends<!-- 26123334 -->

You can now use an Endpoint Privilege Management (EPM) dashboard that presents insights about file elevations and trends in your organization and help identify users that might be ready to be moved to run as standard users in place of running with local admin permissions.

Insights provided by the dashboard include:

- Users who have only unmanaged file elevations
- Users who have both managed and unmanaged file elevations
- User with only managed elevations
- Frequently unmanaged elevations
- Frequently approved by support
- Frequently denied elevations

For more information about the dashboard and these new insights, see [Overview dashboard](../protect/epm-reports.md#elevation-report-by-user) in Reports for Endpoint Privilege Management.

### Device configuration

#### System Info property available in properties catalog for device inventory<!-- 30326613 -->

You can create a [properties catalog](../configuration/properties-catalog.md) policy that lets you collect and view hardware properties from your managed Windows devices. There's a **System Info** category that shows system-level device insights, like OS version, hardware details, and configuration state.

To learn more and get started, see [properties catalog](../configuration/properties-catalog.md).

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

To learn more about these settings, see [Android Intune settings catalog settings list](../configuration/settings-catalog-android.md).

The [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

### Device enrollment

#### Edit managed Google Play organization name<!--32268351 -->

Now you can edit the managed Google Play organization name directly in the Microsoft Intune admin center under **Devices** > **Android** > **Enrollment** > **Managed Google Play**. The updated name, which is validated on input, appears in the admin center. It might also appear on Android device lock screens within a message like, *This device is managed by [organization name]*. For more information, see [Connect Intune account to managed Google Play account](../enrollment/connect-intune-android-enterprise.md).

### Device management

#### Settings catalog supports Windows 11 25H2 settings <!--35412243-->

The release of Windows 11 25H2 includes new policy configuration service providers (CSPs). These settings are available in the [settings catalog](../configuration/settings-catalog-common-features.md) for you to configure.

To learn more, see the [Microsoft Intune Settings Catalog Updated to Support New Windows 11, version 25H2 Settings](https://aka.ms/Intune/Windows25H2-settings) blog post.

To get started with the settings catalog, see:

- [Use the Intune settings catalog to configure settings](../configuration/settings-catalog.md)
- [Common tasks you can complete using the settings catalog](../configuration/settings-catalog-common-features.md)

> [!div class="checklist"]
> Applies to:
>
> - Windows

#### New client version for Remote Help for macOS <!-- 35620986 -->

With the new Remote Help client, version 1.0.2510071, Microsoft Intune now supports macOS 26. Earlier versions of the Remote Help client aren't compatible with macOS 26. The app is automatically updated through Microsoft AutoUpdate (MAU) if opted-in, so no action is required from you or your users. The latest client version resolves an issue that previously caused the screen to appear blank on first launch and fail to connect. For more information, see [Use Remote Help with Microsoft Intune](remote-help.md?tabs=macos).

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

These functionalities [are now available through declarative device management (DDM)](/intune/intune-service/protect/managed-software-updates-ios-macos), which provides a more modern and reliable approach to managing Apple software updates. For more information about this transition, see the Intune Customer Success blog [Move to declarative device management for Apple software updates](https://aka.ms/Intune/Apple-DDM-software-updates).

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

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Enrollment time grouping failure report generally available for Android and Windows <!-- 33290045 -->

Now generally available in the Microsoft Intune admin center, the enrollment time grouping failures report shows failures, which include devices that failed to become a member of the specified static device group during one of the following processes:

- Windows Autopilot device preparation provisioning
- Enrollment of Android Enterprise fully managed devices
- Enrollment of Android corporate-owned work profile devices 
- Enrollment of Android Enterprise dedicated devices 

The enrollment time grouping failures report is available in the admin center under **Devices** > **Monitor** > **Enrollment time grouping failures**. Recently updated information could take up to 20 minutes to appear in the report. For more information, see [Enrollment time grouping in Microsoft Intune](../enrollment/enrollment-time-grouping.md#reporting).

## Week of October 13, 2025

### Device management

#### Windows 10 support in Intune <!-- 34754868 -->

[!INCLUDE [Windows 10 support](../includes/windows-10-support.md)]

For more information, see [Support statement for Windows 10 in Intune](#update-to-support-statement-for-windows-10-in-intune).

> [!div class="checklist"]
> Applies to:
>
> - Windows 10

<!-- *********************************************** -->

## Week of September 29, 2025

### App management

#### PowerShell script installer support for Enterprise App Catalog apps<!--29857395-->

You can now upload a PowerShell script to install Enterprise App Catalog apps as an alternative to using a command line. This option gives you more flexibility when deploying apps.

For more information, see [Add an Enterprise App Catalog app to Microsoft Intune](../apps/apps-add-enterprise-app.md).

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

- **Role-based access control (RBAC) for Microsoft Defender** - We've updated the [RBAC guidance](../../agents/vulnerability-remediation-agent.md#prerequisites) to reflect how RBAC is implemented in Microsoft Defender XDR. Guidance is now provided for configurations that use [**Unified RBAC**](/defender-xdr/manage-rbac) (a single set of permissions across services) and for [**granular RBAC**](/defender-endpoint/rbac) (customized permissions per service).

  When using granular RBAC configurations, ensure the agent's identity is scoped in Microsoft Defender to include all relevant device groups. The agent can't access or report on devices outside its assigned scope.

- **Agent Identity** – You can now [manually change the account that the agent uses as its identity](../../agents/vulnerability-remediation-agent.md#change-the-agent-identity). From the agents *Settings* tab, select **Choose another identity** to open a sign-in prompt. Enter and authenticate the new account. Ensure the new account has sufficient permission to access the Microsoft Defender Vulnerability Remediation data.

  Changes to the agent's identity won't affect the agent's run history, which remains available.

These updates provide greater flexibility and control for organizations using the Vulnerability Remediation Agent in preview. To learn more about this Agent, see [Vulnerability Remediation Agent for Security Copilot in Microsoft Intune](../../agents/vulnerability-remediation-agent.md).

## Week of September 15, 2025 (Service release 2509)

### Device configuration

#### Filter device configuration profiles by the policy type<!-- 33223685 -->

In the Intune admin center > **Devices** > **Configuration** > **Policies** tab, you can use the **Add filters** feature to filter your list of policies by platform, scope tags, and the last modified date.

**Policy type** is available in the **Add filters** feature. So, you can filter your list of policies by their type, like the settings catalog, custom, device restrictions, and the other policy types.

To learn more about viewing and monitoring existing profiles, see [View and monitor device configuration policies in Microsoft Intune](../configuration/device-profile-monitor.md).

#### New day zero settings available in the Apple settings catalog <!-- 33806647 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

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

The [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

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

To learn more about these settings, see [Android Intune settings catalog settings list](../configuration/settings-catalog-android.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

### Device management

#### Device category management supports Multi Admin Approval<!-- 26838632 -->

Intune [device categories](../enrollment/device-group-mapping.md) support Multi Admin Approval. When Multi Admin Approval is enabled, changes to device categories, including creating a new one, editing or deleting one, require a second administrator to approve the change before it's applied. This dual authorization process helps protect your organization from unauthorized or accidental role-based access control changes.

For more information on multiple administrative approval, see [Use multiple administrative approvals in Intune](../fundamentals/multi-admin-approval.md).

#### New Private Space and USB access settings in the Android Enterprise settings catalog <!-- 30802944 24213820 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

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

For a list of existing settings you can configure in the settings catalog, see [Android Enterprise device settings list in the Intune settings catalog](../configuration/settings-catalog-android.md).

#### New prompts available to explore your Intune data<!-- 34601881 -->

You can use Microsoft Copilot in Intune to explore new prompts related to your Intune data using natural language. Use these new prompts to view data on:

- Android and Apple device updates
- Windows Autopilot
- [Endpoint Privilege Management](../protect/epm-overview.md)
- [Advanced Analytics](../../advanced-analytics/index.md)

When you start typing your request, a list of prompts that best match your request are shown. You can also continue typing for more suggestions.

Each query returns a Copilot summary to help you understand the results and offers suggestions. With this information, you can also:

- Add devices or users from the results to a group so you can target apps and policies to this group.
- Filter example queries to find or build requests that match your needs.

To learn more, see [Explore Intune data with natural language and take action](../copilot/copilot-intune-explorer.md).

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
> The **Resource explorer** pane that displays Configuration Manager data via [tenant attach](/intune/configmgr/tenant-attach/resource-explorer) still retains its original name.

#### New features in Copilot for Microsoft Intune <!-- 32549162 -->

- **Easier access to Copilot Chat** - Copilot Chat is embedded directly into the Intune admin center header. So, IT admins can access Copilot Chat from any screen in the admin center. This feature helps admins get faster insights and support.

- **Context-aware conversations with Copilot Chat** - As you type, a dynamic prompt box provides real-time suggestions and recommends prompts relevant to what you're trying to ask. You can troubleshoot devices, manage policies, explore Windows 365 features, and more. You can also directly access the Microsoft docs to learn more.

  Copilot Chat retains your conversation history and remains context aware as you move through the admin center. This continuity helps minimize repetitive prompts.

- **Expanded support for Windows 365 Cloud PC** - With this general availability update, Copilot now supports Windows 365 Cloud PC management. IT admins can access important info, like licensing status, connection quality, configuration details, and performance metrics. This feature makes it easier for admins to monitor and manage Cloud PCs directly from the Intune admin center.

To learn more about Copilot in Intune and to get started, see [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md).

#### Intune supports iOS/iPadOS 17.x as the minimum version<!--33405397-->

Apple released iOS 26 and iPadOS 26. With this release, Microsoft Intune—including the Intune Company Portal and app protection policies (APP, also known as MAM)—now requires iOS/iPadOS 17 or later.

For more information on this change, see [Plan for change: Intune is moving to support iOS/iPadOS 17 and later](#plan-for-change-intune-is-moving-to-support-iosipados-17-and-later).

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

> [!div class="checklist"]
> Applies to:
> - iOS/iPadOS

#### Intune supports macOS 14.x as the minimum version<!--33412147 -->

Apple released macOS 26 (Tahoe). With this release, Microsoft Intune, the Company Portal app, and the Intune MDM agent now require macOS 14 (Sonoma) or later.

For more information on this change, see [Plan for change:  Intune is moving to support macOS 14 and later](#plan-for-change-intune-is-moving-to-support-macos-14-and-higher-later-this-year).

> [!NOTE]
> macOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement](https://aka.ms/Intune/macOS/ADE-DE-support).

For a list of supported OS version, see [Supported operating systems and browsers in Intune](supported-devices-browsers.md).

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

For more information, see [Update a baseline profile to the latest version](../protect/security-baselines-configure.md#update-a-baseline-profile-to-the-latest-version)  in Manage security baseline profiles in Microsoft Intune.

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

For more information, see [Microsoft Tunnel for Mobile Application Management for iOS/iPadOS admin guide](../protect/microsoft-tunnel-mam-ios.md).

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

For more information about the Intune enrollment status page, see [Set up Enrollment Status Page](/intune/intune-service/enrollment/windows-enrollment-status). For information about Windows quality updates, see [Windows quality update policy](/intune/intune-service/protect/windows-quality-update-policy).

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

To learn more about Agent suggestions, remediation guidance, and the new recommended configurations, see [Agent suggestions](../../agents/vulnerability-remediation-agent-use.md#manage-agent-suggestions) in *Use the Vulnerability Remediation Agent*.


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

For more information, see [Supported variables for configuration values](../apps/app-configuration-policies-use-android.md#supported-variables-for-configuration-values).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

### Device configuration

#### Managed Installer support for user and device groups <!-- 30293237 -->

Our Managed Installer policy is updated to add the capability to target individual groups of users and devices, using one or more individual policies. Until now, a Managed Installer policy was a tenant-wide configuration that applied to all Windows devices. With this update, separate policies can now be assigned to different device groups providing you with more flexibility.

If you previously had a tenant-wide managed installer policy in effect, that policy remains available with a group assignment to all your devices. This reconfiguration is equivalent to the previous tenant-wide configuration it had before. You can choose to use that converted policy or implement new policies with more granular control.

For more information about configuring and using managed installers, see [Get started with managed installers](../protect/endpoint-security-app-control-policy.md#get-started-with-managed-installers).

> [!div class="checklist"]
> Applies to:
>
> - Windows

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

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned devices with a work profile (COPE)
> - Android Enterprise corporate owned fully managed (COBO)

### Device enrollment

#### Intune supports Ubuntu 22.04 and later<!-- 32756619 -->

Microsoft Intune and the Microsoft Intune app for Linux now support Ubuntu 22.04 LTS and Ubuntu 24.04 LTS. Support ended for Ubuntu 20.04 LTS. Devices that are currently enrolled on Ubuntu 20.04 LTS remain enrolled even though the version is no longer supported. New devices are unable to enroll if they're running Ubuntu 20.04 LTS. To see what devices or users might be affected, check your Intune reporting. In the admin center, go to **Devices **> **All devices** and filter OS by Linux. You can add more columns to help identify who in your organization has devices running Ubuntu 20.04 LTS. Notify your users to upgrade their devices to a supported Ubuntu version.

For more information about Linux enrollment, see [Linux device enrollment guide for Microsoft Intune](deployment-guide-enrollment-linux.md).


### Device management

#### Wipe remote action supports Multi Admin Approval<!-- 27043113 -->

When you use the Multi Admin Approval feature, you require a second admin account to approve a change before the change is applied.

The **[Wipe](../remote-actions/device-wipe.md)** remote action supports Multi Admin Approval. Use Multi Admin Approval with the **Wipe** action to help mitigate the risk of unauthorized or compromised remote actions by a single admin account.

For more information on Multi Admin Approval, see [Use Multi Admin Approval in Intune](../fundamentals/multi-admin-approval.md).

#### Configure Windows Backup for Organizations (public preview)<!-- 33829628 -->

Intune administrators can configure a new feature in public preview called Windows Backup for Organizations. With this feature, you can back up your organization's Windows 10 or Windows 11 settings and restore them on a Microsoft Entra joined device. Backup settings are configurable in the Microsoft Intune admin center settings catalog, while a tenant-wide setting that lets you restore a device is available in the admin center under **Enrollment**. The backup setting is available now in public preview, while the restore setting will be available for public preview beginning August 26.

For more information about this feature, see [Windows Backup for Organizations in Microsoft Intune](../enrollment/windows-backup-restore.md).

#### New resolution button improves compliance remediation experience<!-- 31370959 -->

We improved the Just in Time (JIT) compliance remediation experience for device users in Microsoft Intune. Intune collaborated with Microsoft Defender to:

- Remove user clicks required to view and learn remediation steps.
- Add a **Resolve** button to reduce time-to-remediation.

When a user opens a productivity app and sees they're marked noncompliant due to Microsoft Defender, the user can now select **Resolve.** This action redirects them to Microsoft Defender, where Microsoft Defender takes steps to remediate the user and then redirect the user back to their productivity app.

Even if you aren't using Microsoft Defender, if you have Conditional Access turned on your users can have an improved experience. With JIT compliance remediation, users go through an embedded flow that shows them their compliance status, noncompliance reasoning, and a list of actions right within a productivity app. This flow eliminates extra steps, the need to switch between apps, and reduces the number of authentications.

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

You can now use several new [software update reports for Apple devices](../../device-updates/apple/reports.md) that are powered by Apples built-in declarative reporting infrastructure. The declarative reporting infrastructure provides Intune with a near real-time view of the software update status of managed devices. The following Apple software update reports are now available:

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

> [!div class="checklist"]
> Applies to:
>
> - macOS

### Device security

#### Update required for Microsoft Tunnel endpoints<!-- 32817331 -->

As part of our ongoing improvements to the Microsoft Tunnel infrastructure, we introduced new endpoints with the [March 19, 2025 release](../protect/microsoft-tunnel-upgrade.md). You must upgrade your Microsoft Tunnel to the March 19, 2025 release version or later to ensure you're using the new endpoints. Once you upgrade to this version or later, you can't downgrade to an earlier version. Earlier releases that rely on legacy endpoints aren't supported and might cause service disruptions. To continue with uninterrupted service, we recommend upgrading to the latest supported build and avoiding rollback to unsupported versions.

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

## What's new archive
<!-- Past announcements that are older than six months will be moved to the archive -->

For previous months, see the [What's new archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
