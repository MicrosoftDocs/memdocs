---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 7/2/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1

# optional metadata

#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# In development for Microsoft Intune

To help in your readiness and planning, this page lists Intune UI updates and features that are in development but not yet released. In addition to the information on this page:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in Office message center.
- When a feature enters production, whether it's a preview or generally available, the feature description will move from this page to [What's new](whats-new.md).
- This page and the [What's new](whats-new.md) page are updated periodically. Check back for additional updates.
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

> [!NOTE]
> This page reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This page doesn't describe all features in development.

**RSS feed**: Find out when this page is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**This article was last updated on the date listed under the title above.**

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control

-->

<!-- ***********************************************-->
## App management

### Export underlying discovered apps list data<!-- 9370255  -->

In addition to exporting the summarized discovered apps list data, you will also be able export the more extensive underlying data. The current summarized export experience provides summarized aggregate data, however the additional new experience will also provide the raw data. The raw data export will give you the entire dataset, which is used to create the summarized aggregate report. The raw data will be a list of every device and each app discovered for that device. This functionality is being added to the Intune console to replace the Intune Data Warehouse Application Inventories dataset, which will be removed in the 2108 release. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **Monitor** > **Discovered apps** > **Export** to display the export options. For related information, see [Intune discovered apps](../apps/app-discovered-apps.md) and [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

### Maximum OS version setting for app conditional launch<!-- 9493137  -->

Using iOS app protection policies in Microsoft Intune app protection policies, you will be able to add a new conditional launch setting to ensure end users are not using a pre-release or beta OS build to access work or school account data. This setting ensures that you can vet all OS releases before end users are actively using new OS functionality. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you will be able to find this setting by selecting **Apps** > **App protection policies**. For related information, see [How to create and assign app protection policies](../apps/app-protection-policies.md).

### Update to Outlook S/MIME settings for iOS and Android devices<!-- 7882166  -->

You'll be able to enable Outlook S/MIME settings to always sign and/or always encrypt on iOS and Android devices when using the managed apps option. You will be able to find this setting in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) when using managed apps by selecting **Apps** > **App configuration policies**.  In addition, you can add a LDAP (Lightweight Directory Access Protocol) URL for Outlook S/MIME on iOS and Android devices for both managed apps and managed devices. For related information, see [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md).

### Unified delivery of Azure AD Enterprise and Office Online applications in the Android Company Portal<!-- 1817862  -->

Last year, we announced [Unified delivery of Azure AD Enterprise and Office Online applications in the Company Portal website](../fundamentals/whats-new.md#unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal). This feature will be supported for users who get their apps directly from the Android Company Portal. On the **Customization** pane of Intune, select to **Hide** or **Show** both **Azure AD Enterprise applications** and **Office Online applications** in the Company Portal. Each end user will see their entire application catalog from the chosen Microsoft service. By default, each additional app source will be set to **Hide**. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Customization** to find this configuration setting. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

### Content of macOS LOB apps will be displayed in Intune<!-- 6991005  -->

Intune will display the contents of macOS LOB apps ( .intunemac files) in the console. You will be able to review and edit the app detection details in the Intune console that are captured from the *.intunemac* file when adding a macOS LOB app. When uploading a PKG file, detection rules will be auto-created. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > **Add**. Continue by selecting the **Line-of-business** app type and the **App package file** containing the *.intunemac* file. For more information, see [How to add macOS line-of-business (LOB) apps to Microsoft Intune](../apps/lob-apps-macos.md).

<!-- ***********************************************-->
## Device configuration

### See policy compliance for a device in tenant attach in Endpoint Manager<!-- 9264837 -->

To manage your devices from the cloud, you can attach your Configuration Manager infrastructure to Endpoint Manager. When deploying Endpoint Security policy to tenant attached devices, you'll be able to see the overall compliance status for the policy. With device level reporting, you'll be able to see the compliance state for a policy at the device level in the Microsoft Endpoint Manager admin center.

For more information on what you can do in Endpoint Manager in a tenant attach setup, see [Microsoft Endpoint Manager tenant attach](../../configmgr/tenant-attach/device-sync-actions.md).

### Use a Settings Catalog policy in a policy set for Windows and macOS devices<!-- 8851701  -->

In Intune, you can create a policy using [Settings Catalog](../configuration/settings-catalog.md), which lists all the settings you can configure. Now, you can use the Settings Catalog policy within a policy set.

For more information, see [Use policy sets to group collections of management objects](policy-sets.md).

Applies to:

- macOS
- Windows 10 and newer

### Settings catalog policies for policy sets<!-- 8683467  -->

In addition to profiles based on templates, you will be able to add a profiles based on the **Settings catalog** to your policy sets. The **Settings catalog** is a list of all the settings you can configure. To create a policy set in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Policy sets** > **Policy sets** > **Create**. For more information, see [Use policy sets to group collections of management objects](../fundamentals/policy-sets.md) and [Use the settings catalog to configure settings on Windows and macOS devices - preview](../configuration/settings-catalog.md).

### New macOS device configuration profile settings, and iOS/iPadOS setting name is changing<!-- 9772945  -->

There are new settings you can configure on macOS 10.13 devices and newer (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Templates** > **Device restrictions** for profile type):

- **Block adding Game Center friends** (App Store, Doc Viewing, Gaming): Prevents users from adding friends to the Game Center.
- **Block Game Center** (App Store, Doc Viewing, Gaming): Disables the Game Center, and the Game Center icon is removed from the Home screen.
- **Block multiplayer gaming in the Game Center** (App Store, Doc Viewing, Gaming): Prevents multiplayer gaming when using the Game Center.
- **Block modification of wallpaper** (General): Prevents the wallpaper from being changed.

To see the settings you can currently configure, go to [macOS device settings to allow or restrict features](../configuration/device-restrictions-macos.md).

Also, the iOS/iPadOS **Block Multiplayer Gaming** setting name is changing to **Block multiplayer gaming in the Game Center** (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile type).

For more information about this setting, go to [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md).

Applies to:

- iOS/iPadOS
- macOS 10.13 and newer

### More iOS/iPadOS home screen layout grid size options<!-- 9569886  -->

On iOS/iPadOS devices, you can configure the grid size on the home screen (**Devices** > **Device Configuration** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **Home screen layout**). For example, you can set the grid size to 4 columns x 5 rows.

The grid size will have more options:

- 4 columns x 5 rows
- 4 columns x 6 rows
- 5 columns x 6 rows

To see the home screen layout settings you can currently configure, go to [device settings to use common iOS/iPadOS features in Intune](../configuration/ios-device-features-settings.md#home-screen-layout).

Applies to:

- iOS/iPadOS

### Use filters on DFCI configuration profiles on Windows 10 RS5+ devices<!-- 8817773  -->

In Endpoint Manager, you can create filters to target devices based on different properties. When you create a Device Firmware Configuration Interface (DFCI) profile, you'll be able to use filters when assigning the profile.

- For more information on filters, see [Use filters (preview) when assigning your apps, policies, and profiles](filters.md).
- For more information on the DFCI profile, see [Use Device Firmware Configuration Interface profiles on Windows devices](../configuration/device-firmware-configuration-interface-windows.md).

Applies to:

- Windows 10 RS5 (1809) and newer on supported UEFI

### Add certificate server names to enterprise Wi-Fi profiles on Android Enterprise personally-owned devices with a work profile<!-- 10285509  -->

On Android devices, you can use certificate-based authentication for Wi-Fi networks on personal devices with a work profile (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Personally-owned work profile** > **Wi-Fi**).

When you use the **Enterprise** Wi-Fi type, and select the **EAP type**, there's a new **Certificate server names** setting. Use this setting to add a list of the certificate server domain names used by your certificate. For example, enter `srv.contoso.com`.

On Android 11 and newer devices, if you use the **Enterprise** Wi-Fi type, then you **must** add the certificate server names. If you don't add the certificate server names, users will have connection issues.

For more information on the Wi-Fi settings you can configure on Android Enterprise devices, see [Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices in Microsoft Intune](..configuration/wi-fi-settings-android-enterprise.md).

Applies to:

- Android Enterprise personally owned devices with work profile

### Use filters to assign Endpoint analytics proactive remediations scripts and Endpoint Security policies in Endpoint Manager admin center - public preview<!-- 7566953 7591178  -->

In the Endpoint Manager admin center, you can create filters, and then use these filters when assigning apps and policies. You'll be able to use filters to assign the following policies:

- [Endpoint analytics proactive remediations Windows PowerShell scripts](/mem/analytics/proactive-remediations) (**Reports** > **Endpoint analytics** > **Proactive remediations**)
- [Endpoint Security policies](../protect/endpoint-security-policy.md), including Account protection, Antivirus, Attack surface reduction, and more.

For more information on filters, see [Use filters (preview) when assigning your apps, policies, and profiles](filters.md).

Applies to:

- macOS
- Windows 10 and newer

### Use filters to assign Endpoint analytics proactive remediations scripts and Endpoint Security policies in Endpoint Manager admin center - public preview<!-- 7566953 7591178  -->

In the Endpoint Manager admin center, you can create filters, and then use these filters when assigning apps and policies. You'll be able to use filters to assign the following policies:

- [Endpoint analytics proactive remediations Windows PowerShell scripts](/mem/analytics/proactive-remediations) (**Reports** > **Endpoint analytics** > **Proactive remediations**)
- [Endpoint Security policies](../protect/endpoint-security-policy.md), including Account protection, Antivirus, Attack surface reduction, and more.

For more information on filters, see [Use filters (preview) when assigning your apps, policies, and profiles](filters.md).

Applies to:

- macOS
- Windows 10 and newer

### Use filters on DFCI configuration profiles on Windows 10 RS5+ devices<!-- 8817773   -->

In Endpoint Manager, you can create filters to target devices based on different properties. When you create a Device Firmware Configuration Interface (DFCI) profile, you'll be able to use filters when assigning the profile.

- For more information on filters, see [Use filters (preview) when assigning your apps, policies, and profiles](filters.md).
- For more information on the DFCI profile, see [Use Device Firmware Configuration Interface profiles on Windows devices](../configuration/device-firmware-configuration-interface-windows.md).

Applies to:

- Windows 10 RS5 (1809) and newer on supported UEFI

### New Deployment Channel setting for custom device configuration profiles on macOS devices<!--9683731  -->

When creating a custom device restriction policy for macOS devices, there is a new Deployment Channel setting available (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Templates** > **Custom** for profile).

Use the **Deployment channel** setting to deploy the configuration profile to the user channel or the device channel. If you send the profile to the wrong channel, then deployment can fail. For more information on using a payload in a device profile or a user profile, see [Profile-Specific Payload Keys](https://developer.apple.com/documentation/devicemanagement/profile-specific_payload_keys) (opens Apple developer website).

For more information about custom macOS profiles in Intune, see [Use custom settings for macOS devices](../configuration/custom-settings-macos.md).

Applies to:

- macOS

### Use Wi-Fi networks set up using configuration profiles setting for iOS/iPadOS 14.5 devices and newer<!-- 9764167  -->

When creating a device restrictions policy for iOS/iPadOS devices, there's a new setting available (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile):

- **Require devices to use Wi-Fi networks set up via configuration profiles**: Set to **Yes**to require devices to only use Wi-Fi networks set up through configuration profiles.

To see the settings you can currently configure, go to [iOS and iPadOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-ios.md).

Applies to:

- iOS/iPadOS 14.5 and newer

<!-- ***********************************************-->
<!--
## Device enrollment
-->

<!-- ***********************************************-->
## Device management

### Tenant attach: Offboarding <!--9412904 -->

While we know customers get enormous value by enabling tenant attach with Configuration Manager, there are rare cases where you might need to offboard a hierarchy. For example, you may need to offboard from the cloud following a disaster recovery scenario where the on-premises environment was removed. You'll soon be able to offboard a Configuration Manager environment from the Microsoft Endpoint Manager admin center.

### Use filters to assign iOS/iPadOS software update policies in Endpoint Manager admin center - public preview<!-- 7423817 -->

In the Endpoint Manager admin center, you can create filters, and then use these filters when assigning apps and policies.

When assigning iOS/iPadOS software update policies to device groups, you'll be able to use filters. You can filter the devices that get the software update policy based on a device property, such as the OS version, device manufacturer, and more. After you create the filter, use the filter when you assign the software update policy.

To see the assignment filters that apply to your iOS/iPadOS devices, go to **Devices** > **iOS/iPadOS** > **iOS/iPadOS devices** > select a device > **Filter evaluation (preview)**.

For more information on filters, see [Use filters (preview) when assigning your apps, policies, and profiles in Microsoft Endpoint Manager](filters.md).

Applies to:

- iOS/iPadOS

### Improvements for managing Windows Updates for pre-release builds<!-- 10198684 -->

We’re improving the experience of managing Windows updates for pre-release builds. (**Devices** > **Windows** > **Windows 10 update rings**).

The improvements include the following:

- Devices assigned to Windows update rings will no longer have the *ManagePreviewBuilds* setting changed during Autopilot. When this setting changes during Autopilot it forces an additional reboot.
- There will be a new control named **Enable pre-release builds** added to Windows update rings to indicate whether to configure assigned devices to update to pre-release builds.
- The list of pre-release builds will update:
  - The default, non-prerelease **Semi-Annual Channel** will be removed.
  - The names of the pre-release builds will reflect the current names of **Dev Channel**, **Beta Channel**, and **Windows Insider - Release Preview**.

### Intune moving to support iOS/iPadOS 13 and higher later this year<!-- 9964998 idrady-->

Later this year, Apple is expected to release iOS 15. Microsoft Intune, including the Intune Company Portal and Intune app protection policies will require [iOS/iPadOS 13 and higher](supported-devices-browsers.md) shortly after the release of iOS 15.

### Intune moving to support  macOS 10.15 and later with the release of macOS 12<!-- 10154527 -->

Apple is expected to release macOS 12 (Monterey) in the fall of 2021. Microsoft Intune, including the Company Portal and Intune MDM agent, will require macOS 10.15 (Catalina) and later shortly after the release of macOS 12.

<!-- ***********************************************-->
## Intune apps

### End users can restart an app install from the Company Portal<!-- 652935  -->

Using the Company Portal, end users will be able to restart an app installation if the progress seems to have stalled or is frozen. This functionality is allowed if the app installation progress has not changed in two hours.

### Intune management agent for macOS devices will be a universal app<!-- 9294405  -->

When you deploy shell scripts or custom attributes for macOS devices from Microsoft Endpoint Manager, it will deploy the new universal version of the Intune management agent app that runs natively on Apple Silicon Mac machines. The same deployment will install the x64 version of the app on Intel Mac machines. For related information, see [Microsoft Intune management agent for macOS](../apps/macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Account protection policy changes in Endpoint security<!--  7492116   -->

We’re reworking the endpoint security Account protection policy to use the new APIs for Windows Hello for Business. The new APIs will result in a more consistent experience. The new API is *./Device/Vendor/MSFT/PassportForWork*, which includes more options that can help reduce conflicts.   This API replaces the use of  *./User/Vendor/MSFT/PassportForWork*.  (**Endpoint security** > **Account protection**)

After the change, only new policies you then create will use the new API. Your existing policies won’t be affected by this change and will continue to use the older API.

### Export capability for Enrollment failures report<!-- 5491082  -->

You will be able to export data from the Enrollment failures operational report. This report will allow you to quickly export reporting data generated from any size tenant. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Monitor** > **Enrollment failures** > **Export**. For more information about reports in Intune, see [Intune reports](../fundamentals/reports.md).

### Filter evaluation report will be improved<!-- 9974516   -->

The **Filter evaluation** page, which shows every app or policy that was filtered, will be improved to include results for available app assignments. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **All devices** > *select a device* > **Filter evaluation**.

### Confirm Tunnel Gateway servers can access your internal network from within the Microsoft Endpoint Manager admin center<!-- 9840576 -->

We're adding the capability to the Microsoft Endpoint Manager admin center to confirm that your Tunnel Gateway servers can access your internal network, without someone having to access the servers directly. To enable this, you'll configure a new option called **URL for internal network access check** in the properties of each Tunnel Gateway site (**Tenant administration** > **Microsoft Tunnel Gateway** > **Sites**).

After adding a URL from your internal network to a Tunnel Gateway site, each server in that site periodically attempts to access it, and then reports on the result.

The status for each server will be visible by selecting the server from **Tenant administration** > **Microsoft Tunnel Gateway** > **Health status**. Status values will include:

- **Healthy** - The server can access the URL specified in the site properties.
- **Unhealthy** - The server can't access the URL specified in the site properties.
- **Unknown** - This status appears when you haven't set a URL in the site properties, and doesn't effect the overall status of the site.

### Customize health status thresholds for Microsoft Tunnel Gateway servers<!--10464499 -->

You’ll soon be able to customize the thresholds that determine the health status for several metrics of Microsoft Tunnel Gateway servers.  (**Tenant administration** > **Microsoft Tunnel Gateway** > **Health status** > *Select a server* > **Health check**)

Each metric that appears on the **Health check** tab for Tunnel Gateway servers has a default value to determine whether the status is *healthy*, *warning*, or *unhealthy*. You’ll be able to customize the thresholds for the following metrics:

- CPU usage
- Memory usage
- Disk space usage
- Latency
- TLS certificate

When you update the thresholds, the values in the *Health check* tab will automatically update to reflect status based on the updated thresholds.

### View health status trends for Microsoft Tunnel Gateway servers<!-- 10464520 -->  

Soon you’ll be able to view health status trends for several Microsoft Tunnel Gateway health metrics in the form of a chart. The health status trend charts will be available for individual servers you select from the *Health status* page.  (**Tenant administration** > **Microsoft Tunnel Gateway** > **Health status** > *Select a server* > **Trends**)

The metrics that support the trend charts include:

- Connections
- CPU usage
- Disk space usage
- Memory usage
- Average latency
- Throughput

### Device configuration reporting will be updated<!-- 10005568  -->

All device configuration and endpoint security profiles will be merged into one report. You will be able to view all the policies applied to your device in a single report with improved data. You will be able to see the distinction of profile types in a new **Policy type** field. Also, selecting a policy will provide additional details about settings applied to the device and status of the device. Role-based access control (RBAC) permissions will be applied to filter the list of profiles based on your permissions. In Microsoft Endpoint Manger admin center, you will select **Devices** > **All devices** > *select a device* > **Device configuration** to see this report when it is available. For related information, see [Microsoft Intune reports](../fundamentals/reports.md).

### Export GPO XML file size increased to 4 MB when using group policy analytics (preview) on Windows 10 and later devices<!-- 9560131  -->

In Microsoft Endpoint Manager, you can use group policy analytics (preview) to analyze your on-premises GPOs, and determine how your GPOs translate in the cloud. To use this feature, you export your GPO as an XML file. The XML file size will be increased from 750 KB to 4 MB.

For more information on using group policy analytics, see [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Endpoint Manager - Preview](../configuration/group-policy-analytics.md).

Applies to:

- Windows 10 and later

### See the available apps that can be assigned in filter reports<!-- 9974516   -->

In the Endpoint Manager admin center, you can create filters, and then use these filters when assigning apps and policies. In **Devices** > **All Devices** > select a device > **Filter evaluation (preview)**, you can see the available apps that can be assigned to the device.

- For more information on filters, see [Use filters (preview) when assigning your apps, policies, and profiles in Microsoft Endpoint Manager](filters.md).
- For more information on filter reports, see [Filter reports and troubleshooting in Microsoft Endpoint Manager](filters-reports-troubleshoot).

Applies to:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10 and newer

### Endpoint analytics per device scoring <!--8462182  -->

[Endpoint analytics](../../analytics/overview.md) will soon have some scores per device. Reviewing scores per device may help you find and resolve end-user impacting issues before a call is made to the help desk. You'll be able to display and sort by the [Endpoint analytics](../../analytics/enroll-intune.md#bkmk_view), [Startup performance](../../analytics/startup-performance.md#bkmk_score), and [Application reliability](../../analytics/app-reliability.md#app-reliability-score) scores for each device.

<!-- ***********************************************-->
## Role-based access control

### Scope tags for Managed Google Play apps<!-- 6114508  -->

Scope tags determine which objects an admin with specific rights can view in Intune. Most newly-created items in Intune take on the scope tags of the creator. This is not the case for Managed Google Play Store apps. You will be able to optionally assign a scope tag to apply to all newly-synced Managed Google Play apps on the **Managed Google Play connector** pane. The chosen scope tag will only apply to new Managed Google Play apps, not Managed Google Play apps that have already been approved in the tenant. For related information see [Add Managed Google Play apps to Android Enterprise devices with Intune](../apps/apps-add-android-for-work.md) and [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

<!-- ***********************************************-->
## Scripting

### Update when exporting Intune reports using the Graph API<!-- 8764428  -->

When you use the Graph API to export Intune reports without selecting any columns for the devices report, you'll receive the default column set. To reduce confusion, we'll be removing columns from the default column set starting January 2021. The columns being removed are `PhoneNumberE164Format`, `_ComputedComplianceState`, `_OS`, and `OSDescription`. These columns will still be available for selection if you need them, but only explicitly, and not by default. If you have built automation around the default columns of the device export, and that automation uses any of these columns, you need to refactor your processes to explicitly select these and any other relevant columns. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

### Intune Data Warehouse updates<!-- 9370034 -->

The  `applicationInventory`  entity will be removed from the Intune Data Warehouse with the 2108 service update of Intune. We're introducing a more complete and accurate dataset that will be available in the UI and via our export API. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

<!-- ***********************************************-->
## Security

### New options for Tunnel Gateway server upgrades<!-- 8664465    -->

You'll soon be able to configure some aspects of Microsoft Tunnel Gateway server upgrades. (**Tenant administration** > **Microsoft Tunnel Gateway (preview)**)

Options include:

- Restrict the start of server upgrades to a specific time window.
- Configure servers at a site to upgrade manually, or require the admin to approve an upgrade before it can start.

We're also adding a new health check setting that helps you identify when a server is running the latest version of Tunnel Gateway.

### New details for the Intune antivirus reports<!-- 8504648 -->

We're adding two new columns of detail to both the Windows 10 unhealthy endpoints report and the Antivirus agent status report. The new details include:

- **MDE Onboarding status** - (HealthState/OnboardingState) Identifies the presence of the Microsoft Defender for Endpoint agent on the device.
- **MDE Sense running state** - (HealthState/SenseIsRunning) Reports on the operational status of the Microsoft Defender for Endpoint health sensor on a device.

You can view these reports at **Endpoint security** > **Antivirus** > **Windows 10 unhealthy endpoints**, and **Reports** > **Microsoft Defender Antivirus** > **Antivirus agent status**.

For more information about these settings, see  [WindowsAdvancedThreatProtection CSP](/windows/client-management/mdm/windowsadvancedthreatprotection-csp).

### Changes to settings the settings catalog for Microsoft Defender for Endpoint on macOS <!--9817140 -->

In public preview, we’re adding eight new settings to the settings catalog to help you manage Microsoft Defender for Endpoint on macOS. We are also removing one setting. (**Devices** > **Configuration profiles** > **Create profile** > **macOS**> **Settings catalog**)

The new settings by settings category:

- **Microsoft Defender - Antivirus engine**:
  - Disallowed threat actions
  - Exclusions merge
  - Scan history size
  - Scan Results Retention
  - Threat type settings merge

- **Microsoft Defender - Cloud delivered protection preferences**:
  - Automatic security intelligence updates

- **Microsoft Defender - User interface preferences**:
  - User initiated feedback

- **Microsoft Defender - Network protection** - This is a new category for Microsoft Defender for Endpoint in the catalog:
  - Enforcement level

### Additional Android SafetyNet evaluation type support for conditional launch policies<!-- 9076664  -->

Conditional launch will support a sub-setting of **SafetyNet device attestation**. If  you select **SafetyNet device attestation** as required for conditional launch, you can specify that a specific SafetyNet evaluation type is used. An additional supported evaluation type will be a hardware-backed key. The presence of a hardware-backed key as the evaluation type will indicate greater integrity of a device. Devices that do not support hardware-backed keys will be blocked by the MAM policy if they are targeted with this setting. For more information about SafetyNet evaluation and hardware-backed key support, see [Evaluation types](https://developer.android.com/training/safetynet/attestation#evaluation-types) in the Android developer documentation. For more information about current Android conditional launch settings, see [Conditional launch](../apps/app-protection-policy-settings-android.md#conditional-launch).

<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
