---
title: What's new in Microsoft Intune
description: Find out what's new in Microsoft Intune.
ms.date: 06/23/2026
ms.topic: whats-new
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
> Each monthly [service update](../fundamentals/servicing-information.md) is rolled out gradually to help ensure quality and reliability. Updates are first validated in Microsoft internal environments, then to a small set of customer datacenters before expanding worldwide over the course of several days to a week. Some tenants might see changes before other tenants. The rollout is carefully monitored and might be paused or delayed to protect customers, which can affect timing.
>
> Some features may gradually roll out over several weeks.
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

### Advanced capabilities (formerly "Microsoft Intune Suite")
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

## Week of June 22, 2026

### App management

#### Microsoft Intune app for Android requires version 2025.11.01 or later<!-- 30154210 -->

The minimum supported version of the Microsoft Intune app for Android is now version `2025.11.01`. This change took effect on May 1, 2026. Users running an older version might experience sign-in failures.

Most users have app updates set to automatic and receive the updated app without taking any action. Users not running a supported version should update the Microsoft Intune app to the latest version to resolve any sign-in issues.

To check which devices are affected, go to **Apps** > **Monitor** > **Discovered apps** and find the Microsoft Intune app to identify devices running older versions.

> [!div class="checklist"]
> Applies to:
>
> - Android

## Tenant administration

#### Multi Admin Approval now enforces on API calls made by automation<!-- 37629074 -->

Multi Admin Approval (MAA) now applies to API calls made by automation through the Microsoft Graph API, not just interactive admin actions. If your tenant has MAA access policies configured and you use service principals, automation scripts, or third-party applications to modify protected Intune resources, those calls are now subject to the same approval workflow as interactive operations.

Calls that don't include the required approval headers return an HTTP 403 error. To maintain your automation, update your scripts to follow the MAA approval workflow. If an immediate code change isn't feasible for applications that use app-auth tokens, you can exclude specific applications from enforcement using the new Exclusions tab in the access policy wizard.

For more information, see [Use Multi Admin Approval with the Microsoft Graph API](../fundamentals/role-based-access-control/multi-admin-approval-graph-api.md).

## Week of June 15, 2026

### App management

#### Managed Win32 app content now requires HTTPS delivery <!-- 32909316 -->

Intune now requires HTTPS delivery for managed Win32 app content. This change primarily affects organizations that use Microsoft Connected Cache and haven't configured their cache nodes for HTTPS delivery. Clients that previously pulled content from Connected Cache can still download Intune Win32 apps, but those requests bypass the cache nodes and fall back to the content delivery network (CDN). This behavior can increase internet traffic and bandwidth usage.

For more information, see the blog post [How to enable HTTPS support for Microsoft Connected Cache for Enterprise and Education](https://techcommunity.microsoft.com/blog/intunecustomersuccess/how-to-enable-https-support-for-microsoft-connected-cache-for-enterprise-and-edu/4496173).

For setup and validation guidance, see:

- [HTTPS support for Microsoft Connected Cache overview](/windows/deployment/do/mcc-ent-https-overview)
- [HTTPS setup on Windows](/windows/deployment/do/mcc-ent-https-windows-guide)
- [HTTPS setup on Linux](/windows/deployment/do/mcc-ent-https-linux-guide)

### Device enrollment

#### Enrollment time grouping for new Apple ADE enrollment policies generally available<!-- 17474465, 28230551 -->

Enrollment time grouping is now generally available for Apple automated device enrollment (ADE) on iOS/iPadOS and macOS. With enrollment time grouping, you can identify a device's Microsoft Entra security group during enrollment, so policies, apps, and settings can be applied earlier in the setup process.

Enrollment time grouping is supported in new Apple ADE enrollment policies. For requirements and setup details, see [Set up enrollment time grouping](../device-enrollment/setup-time-grouping.md).  

### Device management

#### Android Enterprise personally owned devices with a work profile uses Android Management API (AMAPI)<!-- 36840128 -->

When users enroll their personally owned Android devices in Intune, a work profile is created with a separate partition on the device for the user's work account. These devices are referred to as *personally owned devices with a work profile*.    

As part of the Intune move to the [Android Management API](https://developers.google.com/android/management) (opens Android's web site), there are some updates for personally owned devices that enroll in Intune:

- Web based enrollment for an improved enrollment flow and experience - Users don't have to install an app to enroll in Intune. Web enrollment is tenant wide.
- New implementation for how Intune delivers policies - Modern update on how Intune delivers and monitors policies on Android personally owned devices with a work profile. This change also aligns with how Intune manages policies on corporate owned devices with a work profile, fully managed, and dedicated devices. You can scale your migration to targeted groups.

To use these features, opt in through the Microsoft Intune admin center:

- Web based enrollment: **Devices** > **Device Onboarding** > **Enrollment** > **Android**> **Personally owned devices with a work profile** > **Use web enrollment for all users enrolling into Android personally-owned work profile management**
- Policy: **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** > **Move to Android Management API**

To learn more, see:

- [New policy implementation and web enrollment for Android personally owned work profile blog](https://techcommunity.microsoft.com/blog/intunecustomersuccess/new-policy-implementation-and-web-enrollment-for-android-personally-owned-work-p/4370417)
- [Use Android Management API for personally owned devices with work profiles](../device-enrollment/android/android-management-api-overview.md)  

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise personally owned devices with a work profile

#### Improvements to the new Intune single device page (public preview) <!-- 38223856 -->

In the Intune admin center, the **Devices** > **All Devices** > select a device page is redesigned and available for you to preview. This feature was available in the [2604 service release](#preview-the-new-device-page-in-the-intune-admin-center-public-preview).

After the initial 2604 release, we made the following improvements:

- After you select one of the following device actions, you can temporarily view passcodes and PINs in the **Device action status** table:

  - Reset passcode
  - Recover passcode
  - Remote Lock
  - Rotate BitLocker Keys

- Updates to Device actions:

  - Device actions work as expected when [multi admin approval](../fundamentals/role-based-access-control/multi-admin-approval.md) policies are enabled.
  - Device actions for supervised iOS devices are available when the action is supported.
  - Admins can enable and disable **Lost mode**.

- Updates to navigation:

  - Tools and reports have been moved to the left navigation menu.
  - The monitor tab is now the default landing tab.

- In the **Essentials** section:

  - The **Copy** button and the **User** and **Compliance** links are available.
  - Supervised iOS devices show a badge to help identify these devices.

- When preview is disabled, the feedback pane shows the correct text.
- Comanagement information is available.
- Admins can remove the primary user from an Azure domain joined device.

### Device security

#### Microsoft Windows 11 STIG SCAP Benchmark audit baseline<!-- 31532934 -->

Intune now includes a STIG audit baseline that assesses Windows devices against the recommended configurations defined in the Security Technical Implementation Guides (STIGs) published by the Defense Information Systems Agency (DISA). The initial baseline audits against the **Microsoft Windows 11 STIG SCAP Benchmark** *Version 2, Release 7  (benchmark date: January 5, 2026)*.

Unlike other Intune security baselines that configure and enforce settings, the STIG audit baseline is audit-only. It evaluates the current state of a device's configuration and generates detailed audit reports without changing any configured settings, helping organizations demonstrate compliance with DoD security recommendations. Audit results have a documented mapping to NIST XCCDF result categories for formal DISA compliance reporting, and Graph API support enables programmatic data retrieval and cross-tenant assessment aggregation.

The STIG audit baseline is available for [US Government Community Cloud High (GCC High)](../fundamentals/government-service.md) tenants and requires
[Advanced Analytics](../advanced-analytics/index.md) licensing.

For more information, see [Use STIG audit baselines to assess Windows device compliance](../device-security/security-baselines/stig-audit-baseline.md).

> [!div class="checklist"]
> Applies to:
>
> - Windows 10
> - Windows 11  

## Week of June 8, 2026 (Service release 2605)

### App management

#### Newly available protected apps for Intune<!-- 36990464, 37246057, 37348844, 37366700, 37401822, 37401836 -->

The following protected apps are now available for Microsoft Intune:

- Caju AI by Caju AI
- eYACHO for Biz 7 Intune by MetaMoJi Corporation (iOS)
- eYACHO Viewer 7 Intune by MetaMoJi Corporation (iOS)
- Harvey AI by Harvey AI (Android)
- Notta for Intune by Notta
- SwiftConnect Mobile by SwiftConnect

For more information about protected apps, see [Microsoft Intune protected apps](../app-management/ref-protected-apps.md).

#### APP Multiple Managed Accounts <!-- 3182632 -->

Microsoft Intune mobile application management now supports Multiple Managed Accounts, letting users add and manage more than one managed account within the same app. App protection policies apply separately to each account, so you can tailor protection based on the account's organization or tenant. This capability helps consultants, acquisition teams, or users with multiple mailboxes stay productive without switching devices.

Currently we support Multiple Managed Accounts in Microsoft Teams on iOS/iPadOS (v8.10.0 or later). Support for additional apps and platforms is coming soon.

> [!NOTE]
> This feature is gradually rolling out and may not yet be available in your tenant.

To learn more, see [Multiple managed accounts for app protection policies](../app-management/protection/multiple-managed-accounts.md).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS

### Device configuration

### Custom top bar elements on Managed Home Screen <!-- 25008744 -->

You have the option to display custom text in the top bar of the Managed Home Screen (MHS). In addition to the existing choices (serial number, device name, tenant name), you can now select **Custom** and enter a free-text string of up to 63 characters. Custom strings support dynamic variables: `{{SerialNumber}}`, `{{DeviceName}}`, and `{{TenantName}}`. This is useful for kiosk scenarios such as checkout devices, departmental tagging, or any case where staff need a quick visual identifier.

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise dedicated devices (COSU)
> - Android Enterprise fully managed devices (COBO)

#### Managed Home Screen exit lock task mode password now requires a device configuration profile<!-- 31846021 -->

You can no longer configure the Managed Home Screen exit lock task mode password by using an app configuration policy. To set or update the lock task mode password for Managed Home Screen, create or update a device configuration profile that defines the lock task mode password policy.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../app-management/configuration/configure-managed-home-screen.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned Fully Managed (COBO)
> - Android Enterprise corporate-owned Dedicated (COSU)

#### New Block Bluetooth sharing setting in the Android Enterprise settings catalog<!-- 35027842 -->

There's a new **Block Bluetooth sharing** setting in the [settings catalog](../device-configuration/settings-catalog/index.md) (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Settings catalog** for profile type > **General**). When set to **True**, the device can't share content over Bluetooth. When set to **False**, Intune doesn't change or update this setting. By default, the OS has the following behavior:

- Fully managed and dedicated devices allow Bluetooth sharing.
- Corporate-owned devices with a work profile block Bluetooth sharing.

For a list of existing settings you can configure in the settings catalog, see [Android Enterprise device settings list in the Intune settings catalog](../device-configuration/settings-catalog/ref-android-settings.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned devices with a work profile (COPE)
> - Android Enterprise corporate-owned fully managed (COBO)
> - Android Enterprise corporate-owned dedicated devices (COSU)

#### Use DDM to manage Apple Intelligence settings on devices running 26.4 and later<!-- 37011037 -->

With the release of 26.4, Apple deprecated several intelligence-related settings in the MDM restrictions payload. To manage these settings, use the [DDM configurations released in March 2026](#new-updates-to-the-apple-settings-catalog-) instead.

In the [settings catalog](../device-configuration/settings-catalog/index.md), the following **Restrictions** are now deprecated:

- Allow Apple Intelligence Report
- Allow Assistant
- Allow Assistant User Generated Content
- Allow Assistant While Locked
- Allow Auto Correction
- Allow Continuous Path Keyboard
- Allow Definition Lookup
- Allow Dictation
- Allowed External Intelligence Workspace IDs
- Allow External Intelligence Integrations
- Allow External Intelligence Integrations Sign In
- Allow Genmoji
- Allow Image Playground
- Allow Image Wand
- Allow Keyboard Shortcuts
- Allow Mail Smart Replies
- Allow Mail Summary
- Allow Notes Transcription
- Allow Notes Transcription Summary
- Allow Personalized Handwriting Results
- Allow Predictive Keyboard
- Allow Safari Summary
- Allow Spell Check
- Allow Visual Intelligence Summary
- Allow Writing Tools
- Force Assistant Profanity Filter
- Force On Device Only Dictation
- Force On Device Only Translation

In the [device restrictions template](../device-configuration/templates/ref-device-restrictions-apple.md), the following settings are deprecated.

**Built-in apps**:

- Block Siri
- Block Siri while device is locked
- Block Siri for dictation
- Block Siri for translation
- Require Siri profanity filters
- Block user-generated content in Siri

**Keyboard and dictionary**:

- Block word definition lookup
- Block predictive keyboards
- Block auto-correction
- Block spell check
- Block keyboard shortcuts
- Block dictation

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS
> - macOS

#### Silence apps on Managed Home Screen to prevent session PIN bypass<!-- 34929486 -->

For devices using Managed Home Screen (MHS), you can now silence apps whenever MHS prompts the user for authentication, such as during sign-in or at the session PIN screen. When silenced, apps can't start activities, display notifications, appear in recent apps, or trigger toasts, dialogs, or device ringing. You can configure an allowlist of apps that remain unsilenced during the locked state, ensuring that critical communications like calls aren't interrupted. This feature is opt-in and configurable, allowing your organization to tailor the experience to its operational needs. Once the device is unlocked, all apps automatically return to their normal state.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../app-management/configuration/configure-managed-home-screen.md).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise

#### New Microsoft Edge settings in the Windows settings catalog<!-- 38051713 -->

There are new Microsoft Edge 148 settings in the Windows settings catalog. To see and configure these settings in Intune, create a Windows settings catalog profile (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type).

The new policies include:

- **Microsoft Edge > Startup, home page and new tab page > Configure whether the Discover or Work feed tabs are shown on the New Tab Page**

  This policy configures whether the Discover or Work feed tabs are shown on the New Tab Page. By default, both Work and Discover tabs are enabled. Your options:

  - `EnableBothWorkDiscover`: If you set this value or don't configure this policy, Microsoft Edge shows both the Work and Discover feed tabs on the new tab page.
  - `EnableOnlyWork`: Microsoft Edge shows only the Work feed tab on the new tab page.
  - `EnableOnlyDiscover`: Microsoft Edge shows only the Discover feed tab on the new tab page.

  This policy works with the **[Set the default New Tab Page feed tab to Work or Discover](/deployedge/microsoft-edge-policies/SetNTPDefaultFeedTab)** policy, which controls which feed tab is selected by default when both tabs are available.

  [ConfigureNTPFeedTabVisibility](/deployedge/microsoft-edge-policies/ConfigureNTPFeedTabVisibility)

- **Microsoft Edge - Default Settings (users can override) > Set the default New Tab Page feed tab to Work or Discover**

  This policy sets the default feed tab on the New Tab Page to Work or Discover. Your options:

  - `Work`: If you set this value or don't configure this policy, Microsoft Edge sets the default feed tab to Work.
  - `Discover`: Microsoft Edge sets the default feed tab to Discover.

  This policy only takes effect when **[Configure whether the Discover or Work feed tabs are shown on the New Tab Page](/deployedge/microsoft-edge-policies/ConfigureNTPFeedTabVisibility)** is set to `EnableBothWorkDiscover` or is not configured. If only one tab is visible, this policy has no effect.

  [SetNTPDefaultFeedTab](/deployedge/microsoft-edge-policies/SetNTPDefaultFeedTab)

- **Microsoft Edge > Identity and sign-in > Allow M365 authentication popups in work profiles**

  This policy controls whether Microsoft Edge allows Microsoft 365 authentication pop-ups to bypass the pop-up blocker in work profiles. When users are signed in with a work account, some Microsoft 365 sites, like `microsoft.com`, `cloud.microsoft.com`, and `visualstudio.com`, might open authentication pop-ups to `login.microsoftonline.com`, `login.live.com`, or `login.microsoft.com`. These pop-ups are required to complete sign-in.

  Your options:

  - If you enable this policy or don't configure it, Microsoft 365 authentication pop-ups are allowed in work profiles.
  - If you disable this policy, Microsoft 365 authentication pop-ups follow the default settings like other pop-ups. Users can choose to allow or block them, but they aren't automatically allowed.

  This policy only applies to work profiles. In personal profiles, Microsoft 365 authentication pop-ups are always allowed regardless of this policy's configuration.

  [M365AuthPopupsInWorkEnabled](/deployedge/microsoft-edge-policies/m365authpopupsinworkenabled)

- **Microsoft Edge > Automatically open Copilot side pane with contextual insights for links opened from Outlook**

  This policy controls whether Microsoft Edge automatically opens the Microsoft Copilot side pane when users open web links from Outlook emails sent from the same tenant. Starting in Microsoft Edge version 148, when users open eligible links from Outlook emails sent from the same tenant, Microsoft Edge automatically opens the Copilot side pane with contextual insights. Copilot can use the originating Outlook email as context to surface relevant insights and suggested next steps alongside the web content.

  Your options:

  - If you enable this policy or don't configure it, the Copilot side pane opens automatically when users open links from Outlook emails sent from the same tenant.
  - If you disable this policy, the Copilot side pane doesn't open automatically when users open links from Outlook emails sent from the same tenant.

  This feature applies only to links opened from Outlook emails sent from the same tenant and requires Microsoft Copilot to be available for the user in Microsoft Edge. This feature is disabled if the **[Control Copilot access to page context for Microsoft Entra ID profiles](/deployedge/microsoft-edge-policies/CopilotPageContext)** policy or the **[Control Copilot access to Microsoft Edge page content for Entra account user profiles when using Copilot in the Microsoft Edge sidepane](/deployedge/microsoft-edge-policies/EdgeEntraCopilotPageContext)** policy is disabled, regardless of this policy's configuration. Copilot requires access to page content to provide contextual insights.

  [M365LinksAutoOpenCopilotEnabled](/deployedge/microsoft-edge-policies/M365LinksAutoOpenCopilotEnabled)

- **Microsoft Edge > Enable the extended lifetime option for SharedWorkers**

  Controls whether Microsoft Edge keeps a SharedWorker running briefly after all tabs using it are closed, allowing background tasks to finish.

  Your options:

  - If you enable or don't configure this policy, SharedWorkers can use the extended lifetime option.
  - If you disable this policy, the extended lifetime option is ignored, even if it is requested by the page.

  This policy is temporary and will be removed in a future release.

  [SharedWorkerExtendedLifetimeEnabled](/deployedge/microsoft-edge-policies/sharedworkerextendedlifetimeenabled)

- **Microsoft Edge > List of URL patterns for which developer tools are allowed to be opened**

  This policy controls where developer tools can be used in Microsoft Edge by specifying an allowlist of URL patterns. URL patterns are matched against the URL of every frame on the page being inspected.

  Your options:

  - If you configure this policy and don't configure the **[List of URL patterns for which developer tools are blocked](/deployedge/microsoft-edge-policies/DeveloperToolsAvailabilityBlocklist)** policy, developer tools are available only when every frame on the page matches a pattern in this allowlist. If any frame doesn't match, developer tools are blocked for the entire page. For information on the URL format, see [Filter formats for URL list-based policies](https://go.microsoft.com/fwlink/?linkid=2095322).
  - If you configure both this policy and the **[List of URL patterns for which developer tools are blocked](/deployedge/microsoft-edge-policies/DeveloperToolsAvailabilityBlocklist)** policy, this allowlist takes precedence. URLs that match this allowlist are allowed even if they also match the blocklist. URLs that match the blocklist but not this allowlist are blocked. URLs that match neither are governed by the **[Control where developer tools can be used](/deployedge/microsoft-edge-policies/DeveloperToolsAvailability)** policy.
  - If you disable or don't configure this policy, developer tools availability is determined by the **[List of URL patterns for which developer tools are blocked](/deployedge/microsoft-edge-policies/DeveloperToolsAvailabilityBlocklist)** and **[Control where developer tools can be used](/deployedge/microsoft-edge-policies/DeveloperToolsAvailability)** policies.

  This policy applies to developer tools opened for websites, extensions, and web applications. It supports up to 1,000 entries. Example value:

  ```text
  contoso.com
  https://ssl.server.com
  contoso.com/good_path
  https://server.contoso.com:8080/path
  .exact.hostname.com
  file://*
  ```

  [DeveloperToolsAvailabilityAllowlist](/deployedge/microsoft-edge-policies/developertoolsavailabilityallowlist)

- **Microsoft Edge > List of URL patterns for which developer tools are blocked**

  This policy specifies URL patterns where developer tools are blocked. For information on the URL format, see [Filter formats for URL list-based policies](https://go.microsoft.com/fwlink/?linkid=2095322). URL patterns are evaluated against the URL of every frame on the page being inspected. If any frame matches a pattern in this policy, developer tools are blocked for the entire page.

  Your options:

  - If you configure this policy and don't configure the **[List of URL patterns for which developer tools are allowed to be opened](/deployedge/microsoft-edge-policies/developertoolsavailabilityallowlist)** policy, developer tools are blocked when any frame matches a pattern in this policy. If no frames match, availability is determined by the **[Control where developer tools can be used](/deployedge/microsoft-edge-policies/DeveloperToolsAvailability)** policy.
  - If you configure both this policy and the **[List of URL patterns for which developer tools are allowed to be opened](/deployedge/microsoft-edge-policies/developertoolsavailabilityallowlist)** policy, the allowlist takes precedence. URLs that match the allowlist are allowed, even if they also match this policy. URLs that match this policy (but not the allowlist) are blocked. If a URL matches neither, the **[Control where developer tools can be used](/deployedge/microsoft-edge-policies/DeveloperToolsAvailability)** policy determines availability.
  - If you disable or don't configure this policy, developer tools availability is determined by the **[List of URL patterns for which developer tools are allowed to be opened](/deployedge/microsoft-edge-policies/developertoolsavailabilityallowlist)** and **[Control where developer tools can be used](/deployedge/microsoft-edge-policies/DeveloperToolsAvailability)** policies.

  This policy supports up to 1,000 entries. Example value:

  ```text
  https://contoso.com
  contoso.com
  https://ssl.server.com
  contoso.com/bad_path
  https://server.contoso.com:8080/path
  .exact.hostname.com
  *
  file://*
  ```

  [DeveloperToolsAvailabilityBlocklist](/deployedge/microsoft-edge-policies/DeveloperToolsAvailabilityBlocklist)

- **Microsoft Edge > Maximum number of concurrent connections to the proxy server for WebSocket requests**

  Specifies the maximum number of simultaneous connections to a proxy server for WebSocket requests. To configure limits for non-WebSocket requests, see the **[MaxConnectionsPerProxy](/deployedge/microsoft-edge-policies/MaxConnectionsPerProxy)** policy.

  If you don't configure this policy, the default value of 32 is used. Some web applications maintain multiple concurrent connections, like long-lived or hanging requests. Setting a value lower than the default may cause networking delays when many such applications are open. Some proxy servers can't handle a high number of concurrent connections per client. In these cases, reducing the value of this policy might improve reliability. The supported range is 6 to 256:

  - Values less than 6 are treated as 6.
  - Values greater than 256 are treated as 256.

  Modify this value only if required by your proxy server configuration or network environment.

  [MaxConnectionsPerProxyForWebSocket](/deployedge/microsoft-edge-policies/MaxConnectionsPerProxyForWebSocket)

- **Microsoft Edge > Controls the availability of browsing with Copilot in Microsoft Edge**

  When browsing with Copilot is enabled, users can explicitly invoke it for a query. It isn't invoked automatically. Browsing with Copilot is available only on domains specified in the **[Browsing with Copilot Allowed URLs](/deployedge/microsoft-edge-policies/BrowsingWithCopilotAllowList)** policy and is blocked on domains specified in the **[Browsing with Copilot Blocked URLs](/deployedge/microsoft-edge-policies/BrowsingWithCopilotBlockList)** policy. If no domains are configured in the allow list, browsing with Copilot is effectively disabled.

  This feature is available only to users with an active Microsoft 365 Copilot subscription. For more information about configuring browsing with Copilot, see [Configure browsing with Copilot](https://go.microsoft.com/fwlink/?LinkId=2341535).

  Your options:

  - If you enable this policy, browsing with Copilot is turned on for all users who receive the policy, and users can't turn it off.
  - If you disable this policy, browsing with Copilot is turned off for all users who receive the policy, and users can't turn it on.
  - If you don't configure this policy, browsing with Copilot is off by default, and users can turn it on.

  [AllowBrowsingWithCopilot policy](/deployedge/microsoft-edge-policies/allowbrowsingwithcopilot)

- **Microsoft Edge > Browsing with Copilot Allowed URLs**

  Allows you to define a list of URLs where browsing with Copilot is available. Users can't modify this list.

  Your options:

  - If you enable this policy, browsing with Copilot is available only on the sites specified in the list. To allow a broader set of sites while blocking specific exceptions, configure this policy together with the **[Browsing with Copilot Blocked URLs](/deployedge/microsoft-edge-policies/BrowsingWithCopilotBlockList)** policy. For example, you can include `*` to allow all sites, and then use the block list to restrict access to specific URLs. You can define exceptions based on schemes, subdomains, ports, or origins. When multiple filters apply, the most specific match determines whether a URL is allowed or blocked. The block list takes precedence over the allow list.
  - If you disable or don't configure this policy, browsing with Copilot is unavailable on all sites, even if the **[Controls the availability of browsing with Copilot in Microsoft Edge](/deployedge/microsoft-edge-policies/allowbrowsingwithcopilot)** policy is enabled.

  Browsing with Copilot supports only HTTP and HTTPS protocols. Wildcards (`*`) are supported, and subdomains are matched even without wildcards. This policy applies only to the site origin; any path specified in the URL pattern is ignored. For guidance on formatting URL patterns, see [Filter formats for URL list-based policies](https://go.microsoft.com/fwlink/?linkid=2095322). Example value:

  ```text
  https://www.contoso.com
  [*.]contoso.edu
  contoso.net
  login.contoso.us
  ```

  [BrowsingWithCopilotAllowList](/deployedge/microsoft-edge-policies/BrowsingWithCopilotAllowList)

- **Microsoft Edge > Browsing with Copilot Blocked URLs**

  Controls the list of URLs where browsing with Copilot is blocked. Users can't modify this list. Use this policy to define exceptions to broader allowlists. For example, you can set **[Browsing with Copilot Allowed URLs](/deployedge/microsoft-edge-policies/BrowsingWithCopilotAllowList)** to `*` to allow all sites, and then use this policy to block access to specific URLs. This policy supports blocking by scheme, subdomain, or port. When multiple URL patterns apply, the most specific match determines whether access is allowed or blocked. Blocklist entries take precedence over allowlist entries.

  If you don't configure this policy, no exceptions are applied to **[Browsing with Copilot Allowed URLs](/deployedge/microsoft-edge-policies/BrowsingWithCopilotAllowList)**. Browsing with Copilot supports only HTTP and HTTPS protocols. Wildcards (`*`) are supported, and subdomains are matched even without wildcards. URL matching is based on the site origin only; any path specified in the pattern is ignored. For information about URL pattern format, see [Filter formats for URL list-based policies](https://go.microsoft.com/fwlink/?linkid=2095322). Example value:

  ```text
  https://www.contoso.com
  [*.]contoso.edu
  contoso.net
  login.contoso.us
  ```

  [BrowsingWithCopilotBlockList](/deployedge/microsoft-edge-policies/BrowsingWithCopilotBlockList)

- **Microsoft Edge > Enable the Copilot new tab page**

  This policy configures the availability of the Copilot new tab page in Microsoft Edge for Business. The Copilot new tab page combines search and chat into a single input box and includes personalized cards that provide quick access to relevant files, calendar events, and suggested Copilot prompts. Users who don't have a Microsoft 365 Copilot license might experience limited relevance in Copilot prompt card content.

  Most policies that customize the New Tab Page are supported on the Copilot new tab page. For a complete list of supported and unsupported policies, see [Configure the Copilot new tab page](https://go.microsoft.com/fwlink/?linkid=2330462). This policy applies only to Microsoft Entra ID profiles and controls the Copilot new tab page experience in Microsoft Edge for Business. This policy doesn't apply to the Copilot new tab page on personal Microsoft account profiles.

  Your options:

  - If you enable this policy, the Copilot new tab page is turned on.
  - If you disable or don't configure this policy, the Copilot new tab page is turned off. When the policy isn't configured, users can turn it on via user settings.

  [CopilotNewTabPageEnabled](/deployedge/microsoft-edge-policies/CopilotNewTabPageEnabled)

- **Microsoft Edge > Manageability > Allow MAM enrollment when managed device has Purview DLP policy configured**

  Controls whether Microsoft Edge allows Mobile Application Management (MAM) enrollment on managed devices when Microsoft Purview Data Loss Prevention (DLP) is configured.

  Your options:

  - If you enable this policy, MAM enrollment is allowed even when Purview DLP is detected on the device.
  - If you disable or don't configure this policy, MAM enrollment is blocked when Purview DLP is detected on the device.

  [MAMWithDeviceDLPEnabled](/deployedge/microsoft-edge-policies/MAMWithDeviceDLPEnabled)

To learn more about the settings catalog, see [Use the Intune settings catalog to configure settings](../device-configuration/settings-catalog/index.md).

> [!div class="checklist"]
> Applies to:
>
> - Windows

#### New Wired Networks device configuration profile for iOS/iPadOS<!-- 31880672 -->

There's a new **802.1x Wired Networks** device configuration profile for iOS/iPadOS devices. The feature supports 802.1x Ethernet access controls, which is ideal for M-series iPads that support native resolution screen extension. It allows iPads to securely connect to hot desk docks and monitors using wired access.

This profile:

- Supports EAP protocols, like TLS, PEAP, and TTLS
- Is similar to the macOS wired network profile experience

This feature helps with secure enterprise deployments for iPads in education, finance, and other regulated industries.

To learn more about wired networks, see [Add and use wired networks settings on your devices](../device-configuration/templates/configure-wired-networks.md).

> [!div class="checklist"]
> Applies to:
>
> - iOS/iPadOS 17 and newer  

### Device management

#### Detect and block Shadow AI using the properties catalog, device query, and a security baseline (public preview)<!-- 37141378 -->

Using Intune, you can detect and block a Local AI Agent, like OpenClaw, on Windows devices enrolled in Intune. Specifically, you can:

- Use a [Properties catalog](../device-configuration/collect-device-properties.md) policy to collect the Local AI Agent entity. Admins can use this information to identify devices where OpenClaw is present or active.
- Use [Device Query](../advanced-analytics/device-query-multiple-devices.md) to view devices with a Local AI Agent, like OpenClaw.
- Use the [Local AI Agent Baseline - OpenClaw (Preview)](../device-security/security-baselines/ref-openclaw-settings.md) to block users from using OpenClaw.

This feature is in [public preview](../fundamentals/public-preview.md).

> [!div class="checklist"]
> Applies to:
>
> - Windows

### Device security

#### In-place renewal of Cloud PKI issuing certification authorities (CAs)<!-- 25850620 -->

Microsoft Intune now supports in-place renewal of eligible Cloud PKI issuing certification authorities (CAs). Previously, renewing an issuing CA required creating a new CA and manually updating dependent SCEP certificate profiles, which increased operational overhead and configuration risk. With in-place renewal, certificate issuance continues uninterrupted for scenarios such as Wi-Fi, VPN, and email, without changes to existing SCEP profiles or device assignments.

For more information, see [Renew a certification authority in Cloud PKI](../cloud-pki/renew-ca.md).

#### Strict Tunnel Mode for Microsoft Tunnel on Android<!-- 17373449 -->

Microsoft Tunnel now supports Strict Tunnel Mode on Android Enterprise devices. When Strict Tunnel Mode is enabled, all network traffic is forced through the VPN tunnel. If the VPN connection is unavailable or drops, all network traffic on the device is blocked until the VPN reconnects, preventing apps from accessing the public internet outside of the tunnel.

Strict Tunnel Mode is available when a Microsoft Tunnel VPN profile is configured with Always-on VPN. Admins can configure an app exclusion list to allow specific apps to bypass the tunnel and connect directly to the network, regardless of VPN connection status.

Strict Tunnel Mode requires devices enrolled through Android Management API (AM API). For unenrolled devices using Microsoft Tunnel for Mobile Application Management (MAM), Strict Tunnel Mode is available through the Microsoft Edge app configuration policy.

For more information about Microsoft Tunnel capabilities, see [Overview of Microsoft Tunnel](../device-security/microsoft-tunnel/overview.md#capabilities).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned fully managed
> - Android Enterprise corporate-owned work profile
> - Android Enterprise personally owned work profile
> - Android (MAM, unenrolled devices)

#### Grant enhanced security permissions to a Mobile Threat Defense app on Android<!-- 33745497 -->

A new **Mobile Threat Defense role** category is available on the Mobile Threat Defense connector configuration page in the Microsoft Intune admin center. The **Grant MTD role permissions to *\<MTD partner name\>* on enrolled Android COBO and COPE devices** toggle lets you grant enhanced security permissions to one Mobile Threat Defense partner app, such as Microsoft Defender for Endpoint or a supported third-party partner, on enrolled Android Enterprise corporate-owned fully managed (COBO) and Android Enterprise corporate-owned work profile (COPE) devices.

When you turn on this toggle, the selected MTD app receives the following exemptions on targeted devices:

- **Suspension** — The app is prevented from being suspended.
- **Hibernation** — The app is prevented from entering hibernation.
- **Power restrictions** — The app is exempt from power-related restrictions such as app standby, and can start foreground services from the background.
- **User controls** — Users can't clear app data or force-stop the app.

These exemptions help the MTD app maintain continuous threat protection without interruption from system or user actions. Only one MTD partner can hold these permissions per tenant.

For Microsoft Defender for Endpoint, a second toggle is also available: **Automatically launch Microsoft Defender for Endpoint during setup on Android COBO and COPE devices**. When enabled, the Defender for Endpoint app automatically launches during device setup, allowing it to complete its initial configuration without requiring the user to manually open it.

For more information, see [Mobile Threat Defense role](../device-security/mobile-threat-defense/enable-connector.md#mobile-threat-defense-toggle-options).

> [!div class="checklist"]
> Applies to:
>
> - Android Enterprise corporate-owned fully managed
> - Android Enterprise corporate-owned work profile

#### Vulnerability Remediation Agent now uses Microsoft Entra agentic identity (public preview)<!-- 36632198 -->

*This feature is rolling out to tenants gradually and may take several weeks to become available in your environment.*

**The Vulnerability Remediation Agent is now available to all customers in public preview.** Previously, the agent was available only to a select group of customers in a limited preview.

The [Vulnerability Remediation Agent](../copilot/agents/vulnerability-remediation-agent.md) now uses [Microsoft Entra agentic identity](/entra/agent-id/) instead of a human user identity. When you set up a new agent instance, the setup process automatically provisions an agentic identity in your tenant's Entra directory. The agent runs under the permissions delegated to this agentic user, providing a more secure and scalable identity model.

**What this means for existing agents:** If you already have a Vulnerability Remediation Agent instance that uses a human user identity, your agent continues to work as-is for now. Human user identity support expires 90 days after this release, after which you must transition to an agentic identity. A banner on the agent page notifies you when agentic identity is available for your agent. For transition steps and details, see [Transition existing agents to agentic identity](../copilot/agents/vulnerability-remediation-agent.md#transition-existing-agents-to-agentic-identity).

**What's new for agentic identity:**

- New agent instances are provisioned with an agentic identity during setup.
- After setup, you must delegate the required permissions to the agentic user in the Microsoft Entra and Microsoft Defender admin centers.
- Use the **Run Readiness Check** button to verify that all required permissions are in place before running the agent.

For more information, see [Agent identity](../copilot/agents/vulnerability-remediation-agent.md#agent-identity).

## Week of June 1, 2026  

### Device management  

#### Remote Help for Windows updated with performance improvements  

The latest version of Remote Help for Windows (version 5.2.1037.0) includes general bug fixes and performance improvements to enhance reliability.  

## Week of May 26, 2026

### Role-based access control

#### Intune RBAC roles have access to Copilot in Intune<!-- 37153212 -->

When Microsoft Intune is enabled as a data source in Security Copilot, by default:

- The Microsoft Entra ID **Intune Administrator** role automatically inherits **Security Copilot owner** access to Copilot in Intune.
- All the other built-in and custom Intune role-based access (RBAC) roles automatically inherit **Security Copilot contributor** access to Copilot in Intune.

Intune admins can use Security Copilot capabilities in Intune without requiring more role assignments.

Previously, access to Copilot in Intune required a separate role assignment in Security Copilot or a Microsoft Entra ID role, like the Intune Administrator role.

This update reduces access friction and simplifies Copilot onboarding for organizations.

To learn more, see:

- [Microsoft Copilot in Intune](../copilot/index.md)
- [Roles and authentication in Microsoft Security Copilot](/copilot/security/authentication)

## Week of May 18, 2026

### Device security

#### Guidance for device-reported values in compliance reports<!-- 37725884 -->

We updated documentation to clarify how to interpret device-reported values in compliance reports. Some compliance reports include a **Setting** column with values reported directly by the device, providing additional context for noncompliance in scenarios such as custom compliance and Android app configuration reporting. This update adds guidance on treating these values as informational only and highlights security considerations for reviewing device-reported data. For more information, see [Device-reported values in compliance reports](../device-security/compliance/monitor-policy.md#device-reported-values-in-compliance-reports).

## Week of May 11, 2026

### Device enrollment

#### Complete Platform SSO registration during macOS Automated Device Enrollment <!-- 36767290 -->

On macOS devices enrolled with Automated Device Enrollment (ADE), you can run Platform SSO during device registration. Before you enroll, you:

1. Create an Intune [settings catalog policy](../device-configuration/settings-catalog/index.md) and configure the **Enable Registration During Setup** setting.
1. Deploy the Company Portal (5.2604.0 and newer) as a line-of-business app.
1. Configure the Automated Device Enrollment policy to use Setup Assistant with modern authentication and enable await final configuration.

When this feature is enabled, users have access to Microsoft Entra ID resources immediately when they arrive at desktop.

To learn more, see [Configure Platform Single Sign-On (PSSO) during Automated Device Enrollment for macOS devices](../device-configuration/settings-catalog/configure-platform-sso-during-enrollment.md).

> [!div class="checklist"]
> Applies to:
>
> - macOS 26 and newer
> - Company Portal 5.2604.0 and newer

## Week of May 4, 2026

### Monitor and troubleshoot

#### Enhanced app inventory with faster data updates<!-- 27117584 -->

Intune enhanced app inventory brings faster, more detailed visibility into the apps in your environment to support identification of outdated or risky software. Improved data freshness and richer app metadata provide clearer insight into installed applications, while new controls let you specify which devices are included in inventory collection.

This feature is initially available for Windows, with additional platforms to follow.

> [!div class="checklist"]
> Applies to:
>
> - Windows 10/11

## Week of April 27, 2026 (Service release 2604)

### Advanced capabilities

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

1. In the [Microsoft Intune admin center], go to **Devices** > **All Devices**.
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

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center], go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type. 

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

- **Disable Internet Explorer 11 launch via COM automation** - This setting isn't included at release due to a known issue. The Windows client team is addressing the issue, and the setting will be added in a future baseline update.
- **Configure NetBIOS settings** - This setting is pending availability in the Settings Catalog and will be added to the baseline in a future update.

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

  For information about valid URL patterns and examples, see [Filter formats for URL list-based policies](https://go.microsoft.com/fwlink/?linkid=2095322). Wildcards (*) are supported.

- **Block geolocation on these sites**: When **Enabled**, enter a list of URL patterns for sites that are blocked from requesting or accessing the user's geolocation. These sites can't prompt the user for location permissions. When **Disabled** or not configured, the default geolocation setting applies to all sites (if configured) or the user's personal browser setting is used.

  For information about valid URL patterns and examples, see [Filter formats for URL list-based policies](https://go.microsoft.com/fwlink/?linkid=2095322). Wildcards (*) are supported.

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

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center], go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

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

### Advanced capabilities

#### Endpoint Privilege Management support on Azure Virtual Desktop<!-- 26079227 -->

Endpoint Privilege Management (EPM) elevation policies now support deployment to users on Azure Virtual Desktop (AVD) single-session virtual machines.

For information about using EPM, see [Plan and Prepare for Endpoint Privilege Management Deployment](../epm/deployment-planning.md).

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

There is a new setting in the Settings Catalog. To see this setting, in the [Microsoft Intune admin center], go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** for platform > **Settings catalog** for profile type.

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

For previous months, see the [What's new archive](archive/index.md).

<!-- Past announcements that are older than six months will be moved to the archive -->

## Notices

[!INCLUDE [Intune notices](./includes/intune-notices.md)]

<!--links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
