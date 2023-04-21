---
# required metadata
title: What's new in Microsoft Intune
titleSuffix:
description: Find out what's new in Microsoft Intune
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/19/2023
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
> Each [monthly update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) may take up to three days to rollout and will be in the following order:
>
> - Day 1: Asia Pacific (APAC)
> - Day 2: Europe, Middle East, Africa (EMEA)
> - Day 3: North America
> - Day 4+: Intune for Government
>
> Some features may roll out over several weeks and might not be available to all customers in the first week.
>
> For a list of upcoming Intune feature releases, see [In development for Microsoft Intune](../fundamentals/in-development.md). For new information about Autopilot, see [Windows Autopilot What's new](../../autopilot/windows-autopilot-whats-new.md).

You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Get notified when this page is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us` -->

<!-- Common categories:
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

## Week of April 17, 2023 (Service release 2304)

### App management

#### Changes to iCloud app backup and restore behavior on iOS/iPadOS and macOS devices<!-- 16261392  -->  
As an app setting, you can select to **Prevent iCloud app backup** for iOS/iPadOS and macOS devices. You have the option to *not* back up managed App Store apps and line-of-business (LOB) apps on iOS/iPadOS, as well as managed App Store apps on macOS devices (macOS LOB apps won’t support this feature), for both user and device licensed VPP/non-VPP apps. This update includes both new and existing App Store/LOB apps sent with and without VPP that are being added to Intune and targeted to users and devices.

Preventing the backup of the specified managed apps will ensure that these apps can be properly deployed via Intune when the device is enrolled and restored from backup. If the admin configures this new setting for new or existing apps in their tenant, managed apps can and will be re-installed for devices, but Intune will no longer allow them to be backed up.

This new setting appears in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by modifying the properties of an app. For an existing app, you can select **Apps** > **iOS/iPadOS** or **macOS** > *select the app* > **Properties** > Assignment **Edit**. If no group assignment has been set, click **Add group** to add a group. Modify either the setting under **VPN**, **Uninstall on device removal**, or **Install as removable**. Then, select **Prevent iCloud app backup**. The **Prevent iCloud app backup** setting is used to prevent backup of app data for the application. Set to **No** to allow the app to be backed up by iCloud.

For more information, see [Changes to applications’ backup and restore behavior on iOS/iPadOS and macOS devices](https://techcommunity.microsoft.com/t5/intune-customer-success/changes-to-applications-backup-and-restore-behavior-on-ios/ba-p/3692064) and [Assign apps to groups with Microsoft Intune](../apps/apps-deploy.md).

#### Prevent automatic updates for Apple VPP apps<!-- 16876430   -->  
You can control the automatic update behavior for Apple VPP at the per-app assignment level using the **Prevent automatic updates** setting. This setting is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** or **macOS** > *Select a volume purchase program app* > **Properties** > **Assignments** > *Select an AAD group* > **App settings**.

Applies to:

- iOS/iPadOS
- macOS

### Device configuration

#### Updates to the macOS Settings Catalog <!-- 17673709  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type.

The new setting is located under:

**Microsoft AutoUpdate (MAU) > [targeted app]**:

- Update channel override

The following settings have been deprecated:

**Microsoft AutoUpdate (MAU) > [targeted app]**:

- Channel Name (Deprecated)

**Privacy > Privacy Preferences Policy Control > Services > Listen Event or Screen Capture**:

- Allowed

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### The Microsoft Enterprise SSO plug-in for Apple devices is now generally available<!-- 17826329  -->  
In Microsoft Intune, there's a Microsoft Enterprise SSO plug-in. This plug-in provides single sign-on (SSO) to iOS/iPadOS and macOS apps and websites that use Microsoft Azure AD for authentication.

This plug-in is now generally available (GA).

For more information about configuring the Microsoft Enterprise SSO plug-in for Apple devices in Intune, go to [Microsoft Enterprise SSO plug-in in Microsoft Intune](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md).

Applies to:

- iOS/iPadOS
- macOS

#### Disable Activation Lock device action for supervised macOS devices<!-- 16813146  -->  

You can now use the **Disable Activation Lock** device action in Intune to bypass Activation Lock on Mac devices without requiring the current username or password. This new action is available in **Devices** > **macOS** > select one of your listed devices > **Disable Activation Lock**.

More information on managing Activation Lock is available at [Bypass iOS/iPadOS Activation Lock with Intune](../remote-actions/device-activation-lock-disable.md) or on Apple's website at [Activation Lock for iPhone, iPad, and iPod touch - Apple Support](https://support.apple.com/en-us/HT201365).

Applies to:

- macOS 10.15 or later

#### ServiceNow Integration is now Generally Available (GA)<!-- 18163832  -->  
Now generally available, you can view a list of ServiceNow incidents associated with the user you've selected in the Intune Troubleshooting workspace.  This new feature will be available under **Troubleshooting + Support** > select a user > **ServiceNow Incidents**.  The list of incidents shown have a direct link back to the source incident and show key information from the incident.  All incidents listed will link the "Caller" identified in the incident with the user selected for Troubleshooting.

For more information go to [Use the troubleshooting portal to help users at your company](service-now-integration.md).

#### Additional permissions to support administrators in controlling delivery of organization messages<!-- 16982298  -->  

With additional permissions administrators can control delivery of content created and deployed from Organizational messages as well as the delivery of content from Microsoft to users.

The **Update organizational message control** RBAC permission for organizational messages, determines who can change the Organizational Messages toggle to allow or block Microsoft direct messages. This permission is also added to the **Organizational Messages Manager** built-in role.

Existing custom roles for managing Organizational Messages must be modified to add this permission for users to modify this setting.

- For more information, about role-based access control (RBAC), see [RBAC with Microsoft Intune](../fundamentals/role-based-access-control.md).
- For more information, about prerequisites for organization messages, see [Organizational messages prerequisites](../remote-actions/organizational-messages-prerequisites.md#role-based-access-control-requirements).

### Device management

#### Endpoint security firewall rules support for ICMP type<!-- 5653356  -->  
You can now use the **IcmpTypesAndCodes** setting to configure inbound and outbound rules for [Internet Control Message Protocol](/windows/security/threat-protection/windows-firewall/create-an-inbound-icmp-rule) (ICMP) as part of a firewall rule. This setting is available in the [*Microsoft Defender Firewall rules*](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune) profile for the *Windows 10, Windows 11, and Windows Server* platform.

Applies to:

- Windows 11 and later

#### Manage Windows LAPS with Intune polices (public preview)<!-- 11890571  -->  
Now available in a public preview, manage Windows Local Administrator Password Solution (Windows LAPS) with Microsoft Intune [Account protection policies](../protect/endpoint-security-account-protection-policy.md). To get started, see [Intune support for Windows LAPS](../protect/windows-laps-overview.md).

[Windows LAPS](/windows-server/identity/laps/laps-overview) is a Windows feature that allows you to manage and backs up the password of a local administrator account on your Azure Active Directory-joined or Windows Server Active Directory-joined devices.

To manage LAPS, Intune configures the Windows [LAPS configuration service provider](/windows/client-management/mdm/LAPS-csp) (CSP) that is built-in to Windows devices, and which takes precedence over other sources of Windows LAPS configurations, like GPOs or the Microsoft Legacy LAPS tool. Some of the capabilities you can use when Intune to manages Windows LAPS include:

- Define password requirements like complexity and length that apply to the local administrator accounts on a device.
- Configure devices to rotate their local admin account passwords on a schedule, and backup the account and password in your Azure Active Directory or on-premises Active Directory.
- Use an Intune device action from the admin center to manually rotate the password for an account on your own schedule.
- View account details from within the Intune admin center, like the account name and password. This can help you recover devices that are otherwise inaccessible.
- Use Intune reports to monitor your LAPS policies, and when devices last rotated passwords manually or by schedule.  

Applies to:

- Windows 10
- Windows 11

#### New settings available for macOS software update policies<!-- 16646756  -->  
MacOS software update policies now include the following settings to help manage when updates install on a device. These are available when the *All other updates* update type is configured to *Install later*:

- **Max User Deferrals**:  When the *All other updates* update type is configured to *Install later*, this setting allows you to specify the maximum number of times a user can postpone a minor OS update before it’s installed. The system prompts the user once a day. Available for devices running macOS 12 and later.

- **Priority**: When the *All other updates* update type is configured to *Install later*, this setting allows you to specify values of *Low* or *High* for the scheduling priority for downloading and preparing minor OS updates. Available for devices running macOS 12.3 and later.

For more information, see [Use Microsoft Intune policies to manage macOS software updates](../protect/software-updates-macos.md).

Applies to:

- macOS

#### Introducing the new partner portals page<!-- 17829024  -->  
You can now manage hardware specific information on your HP or Surface devices from our partner portals page.

The HP link will take you to HP Connect where you can update, configure, and secure the BIOS on your HP devices.
The Microsoft Surface link will take you to the Surface Management Portal where you can get insights into device compliance, support activity, and warranty coverage.

To access the Partner portals page, you must enable the Devices pane preview and then navigate to **Devices** > **Partner Portals**.

#### Windows Update compatibility reports for Apps and Drivers are now generally available<!-- 17917026  -->  
The following Microsoft Intune reports for [Windows Update compatibility](../protect/windows-update-compatibility-reports.md) are out of preview and now generally available:

- **Windows feature update device readiness report** - This report provides per-device information about compatibility risks that are associated with an upgrade or update to a chosen version of Windows.

- **Windows feature update compatibility risks report** - This report provides a summary view of the top compatibility risks across your organization for a chosen version of Windows. You can use this report to understand which compatibility risks impact the greatest number of devices in your organization.

These reports can help you plan an upgrade from Windows 10 to 11, or for installing the latest Windows feature update.

### Device security

#### Support for WDAC Application ID tagging with Intune Firewall Rules policy<!-- 17224780  -->  
Intune's *Microsoft Defender Firewall Rules* profiles, which are available as part of [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md), now include the Policy App Id setting. This setting is described by the [*MdmStore/FirewallRules/{FirewallRuleName}/PolicyAppId*](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx#mdmstorefirewallrulesfirewallrulenamepolicyappid) CSP and supports specifying a Windows Defender Application Control (WDAC) Application ID tag.

With this capability, you’ll be able to scope your firewall rules to an application or a group of applications and rely on your WDAC policies to define those applications. By using tags to link to and rely on WDAC policies, your Firewall Rules policy won’t need to rely on the firewall rules option of an absolute file path or use of a variable file path that can reduce security of the rule.

Use of this capability requires you to have WDAC policies in place that include *AppId* tags that you can then specify in your Intune Microsoft Defender Firewall Rules.

For more information, see the following articles in the Windows Defender Application Control documentation:

- [About application control for Windows](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)
- [WDAC Application ID (AppId) Tagging guide](/windows/security/threat-protection/windows-defender-application-control/appidtagging/windows-defender-application-control-appid-tagging-guide)

Applies to:

- Windows 10/11

#### New App and browser isolation profile for Intune’s endpoint security Attack Surface Reduction policy<!-- 17392386  -->  
We have released a new experience creating new *App and Browser Isolation* profiles for endpoint security Attack Surface Reduction policy. The experience for editing your previously created App and Browser isolation policies remains the same, and you can continue to use them. This update applies only for the new [App and Browser Isolation](../protect/endpoint-security-asr-policy.md#attack-surface-reduction-profiles) policies you create for the *Windows 10 and later* platform.

This update is part of the continuing [rollout of new profiles for endpoint security policies](../fundamentals/whats-new-archive.md#new-profile-templates-and-settings-structure-for-endpoint-security-policies), which began in April 2022.

Additionally, the new profile includes the following changes for the settings it includes:

- **Block external content from non-enterprise approved sites** - This setting is removed from the updated profile as it was supported only by Microsoft Edge Legacy. Microsoft Edge Legacy support ended in March 2021. [Microsoft 365 apps say farewell to Internet Explorer 11 and Windows 10 sunsets Microsoft Edge Legacy - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/microsoft-365-blog/microsoft-365-apps-say-farewell-to-internet-explorer-11-and/ba-p/1591666).

- **Clipboard file type** – This setting is added to the updated profile and determines the type of content that can be copied from the host to Application Guard environment and vice versa. You can view the CSP for this new setting at [Settings/ClipboardFileType](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#settingsclipboardfiletype) in the WindowsDefenderApplicationGuard CSP documentation.

### Intune apps

#### Newly available protected apps for Intune<!-- 17318943, 17319737, 17457189, 17624650  -->
The following protected apps are now available for Microsoft Intune:
- ixArma by INAX-APPS (iOS)
- myBLDNG by Bldng.ai (iOS)
- RICOH Spaces V2 by Ricoh Digital Services
- Firstup - Intune by Firstup, Inc. (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Role-based access control

#### New Assign (RBAC) permissions for organizational messages<!-- 16872833  -->  
The **Assign** RBAC permissions for organizational messages determines who can assign target Azure AD groups to an organizational message. To access RBAC permissions, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Roles**.

This permission is also added to the **Organizational Messages Manager** built-in role.  Existing custom roles for managing Organizational Messages must be modified to add this permission for users to modify this setting.

- For more information, about role-based access control (RBAC), see [RBAC with Microsoft Intune](../fundamentals/role-based-access-control.md).
- For more information, about prerequisites for organization messages, see [Organizational messages prerequisites](../remote-actions/organizational-messages-prerequisites.md#role-based-access-control-requirements).

### Tenant administration

#### Delete organizational messages<!-- 15273028  -->  
You can now delete organizational messages from Microsoft Intune.  After you delete a message, it's removed from Intune and no longer appears in the admin center. You can delete a message anytime, regardless of its status. Intune automatically cancels active messages after you delete them. For more information, see [Delete organizational messages](../remote-actions/organizational-messages-cancel.md#delete-message).

## Week of April 10, 2023

### Device configuration

#### User configuration support for Windows 10 multi-session VMs is now GA<!-- 17060455 -->

User configuration support for Windows 10 multi-session VMs is now GA. With this, you can:

- Configure user scope policies using **Settings catalog** and assign to groups of users.
- Configure user certificates and assign to users.
- Configure PowerShell scripts to install in the user context and assign to users.

Applies to:

- **Windows 10**
- Virtual machines created in [Azure Public and Azure Government clouds](../fundamentals/intune-govt-service-description.md)

## Week of April 3, 2023

### Device configuration

#### Add Google accounts to Android Enterprise personally owned devices with a work profile<!-- 9113561 -->

On Android Enterprise personally owned devices with a work profile, you can configure settings that restrict device features and settings. Currently, there's an **Add and remove accounts** setting. This setting prevents accounts from being added in the work profile, including preventing Google accounts.

This setting changed. You can now add Google accounts. The **Add and remove accounts** setting options are:

- **Block all accounts types**: Prevents users from manually adding or removing accounts in the work profile. For example, when you deploy the Gmail app into the work profile, you can prevent users from adding or removing accounts in this work profile.
- **Allow all accounts types**: Allows all accounts, including Google accounts. These Google accounts are blocked from installing apps from the **Managed Google Play Store**.

  This setting requires:

  - Google Play app version 80970100 or higher

- **Allow all accounts types, except Google accounts** (default): Intune doesn't change or update this setting. By default, the OS might allow adding accounts in the work profile.

For more information on the settings you can configure, go to [Android Enterprise device settings list to allow or restrict features on personally owned devices using Intune](../configuration/device-restrictions-android-enterprise-personal.md).

Applies to:

- Android Enterprise personally owned devices with a work profile

## Week of March 27, 2023

### App management

#### Update macOS DMG apps<!-- 13155074 -->
You can now update apps of type **macOS apps (DMG)** deployed using Intune. Edit a DMG app that is already created in Intune by uploading the update for the app with the same bundle identifier as the original DMG app. For related information, see [Add a macOS DMG app to Microsoft Intune](../apps/lob-apps-macos-dmg.md).

#### Install required apps during pre-provisioning<!-- 12716381 -->
A new toggle is available in the Enrollment Status Page (ESP) profile that allows you to select whether you want to attempt to install required applications during the pre-provisioning (white glove) technician phase. We understand that installing as many applications as possible during pre-provisioning is desired to reduce the end user setup time. If there's an app install failure, ESP continues except for the apps specified in the ESP profile. To enable this function, you need to edit your Enrollment Status Page profile by selecting **Yes** on the new setting entitled **Only fail selected apps in technician phase**. This setting only appears if you have blocking apps selected. For information about ESP, go to [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).

## Week of March 20, 2023 (Service release 2303) 

### App management

### Additional minimum OS versions for Win32 apps<!-- 16842404  -->  
Intune supports additional minimum operating system versions for Windows 10 and 11 when installing Win32 apps. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **Windows** > **Add** > **Windows app (Win32)**. In the **Requirements** tab next to **Minimum operating system**, select one of the available operating systems. Additional OS options include:

- Windows 10 21H2
- Windows 10 22H2
- Windows 11 21H2
- Windows 11 22H2

#### Managed apps permission is no longer required to manage VPP apps<!-- 17205644  -->  
You can view and manage VPP apps with only the **Mobile apps** permission assigned. Previously, the **Managed apps** permission was required to view and manage VPP apps. This change doesn't apply to Intune for Education tenants who still need to assign the **Managed apps** permission. More information about permissions in Intune is available at [Custom role permissions](../fundamentals/create-custom-role.md#custom-role-permissions).

### Device configuration

#### New settings and setting options available in the macOS Settings Catalog <!-- 16813395  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Microsoft Defender > Tamper protection**:

- Enforcement level

**Microsoft Office > Microsoft OneDrive**:

- Automatic upload bandwidth percentage
- Automatically and silently enable the Folder Backup feature (aka Known Folder Move)
- Block apps from downloading online-only files
- Block external sync
- Disable automatic sign in
- Disable download toasts
- Disable personal accounts
- Disable tutorial
- Display a notification to users once their folders have been redirected
- Enable Files On-Demand
- Enable simultaneous edits for Office apps
- Force users to use the Folder Backup feature (aka Known Folder Move)
- Hide dock icon
- Ignore named files
- Include ~/Desktop in Folder Backup (aka Known Folder Move)
- Include ~/Documents in Folder Backup (aka Known Folder Move)
- Open at login
- Prevent users from using the Folder Backup feature (aka Known Folder Move)
- Prompt users to enable the Folder Backup feature (aka Known Folder Move)
- Set maximum download throughput
- Set maximum upload throughput
- SharePoint Prioritization
- SharePoint Server Front Door URL
- SharePoint Server Tenant Name

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### Add custom Bash scripts to configure Linux devices<!-- 12508999  -->  
In Intune, you can add existing Bash scripts to configure Linux devices (**Devices** > **Linux** > **Configuration Scripts**).

When you create this script policy, you can set the context that the script runs in (user or root), how frequently the script runs, and how many times execution should retry.

For more information on this feature, go to [Use custom Bash scripts to configure Linux devices in Microsoft Intune](../configuration/custom-settings-linux.md).

Applies to:

- Linux Ubuntu Desktops

### Device enrollment

#### Support for the await final configuration setting for iOS/iPadOS Automated device enrollment (public preview)<!-- 13156553  -->  
Now in public preview, Intune supports a new setting called **Await final configuration** in eligible new and existing iOS/iPadOS automated device enrollment profiles. This setting enables an out-of-the-box locked experience in Setup Assistant to prevent device users from accessing restricted content or changing settings on the device until most Intune device configuration policies are installed. You can configure the setting in an existing automated device enrollment profile, or in a new profile (**Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment program tokens** > **Create profile**). For more information, see [Create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).  

#### New setting gives Intune admins control over device-to-category mapping<!-- 15029839 -->  
Control visibility of the device category prompt in Intune Company Portal. You can now hide the prompt from end users and leave the device-to-category mapping up to Intune admins. The new setting is available in the admin center under **Tenant Administration** > **Customization** > **Device Categories**. For more information, see [Device categories](../apps/company-portal-app.md#device-categories).

#### Support for multiple enrollment profiles and tokens for fully managed devices <!-- 14205233  -->  
Create and manage multiple enrollment profiles and tokens for Android Enterprise fully managed devices. With this new functionality, you can now use the *EnrollmentProfileName* dynamic device property to automatically assign enrollment profiles to fully managed devices. The enrollment token that came with your tenant remains in a default profile. For more information, see [Set up Intune enrollment of Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md).

#### New Azure AD frontline worker experience for iPad (public preview)<!-- 6367427  -->  
*This capability will begin to roll out to tenants in mid-April.*

Intune now supports a frontline worker experience for iPhones and iPads using Apple automated device enrollment. You can now enroll devices that are enabled in Azure AD shared mode via zero-touch. For more information about how to configure automated device enrollment for shared device mode, see [Set up enrollment for devices in Azure AD shared device mode](../enrollment/automated-device-enrollment-shared-device-mode.md).  

Applies to:

- iOS/iPadOS

### Device management

#### Endpoint security firewall policy support for log configurations<!-- 16730565   -->  
You can now configure settings in [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune) that configure firewall logging options. These settings can be found in the *Microsoft Defender Firewall* profile template for the *Windows 10 and later* platform, and are available for the *Domain*, *Private*, and *Public* profiles in that template.

Following are the new settings, all found in the [Firewall configuration service provider (CSP)](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx):

- Enable Log Success Connections
- Log File Path
- Enable Log Dropped Packets
- Enable Log Ignored Rules

Applies to:

- Windows 10
- Windows 11

#### Endpoint security firewall rules support for Mobile Broadband (MBB)<!-- 16730577  -->  
The **Interface Types** setting in [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune) now include the option for **Mobile Broadband**. Interface Types is available in the **Microsoft Defender Firewall Rules** profile for all platforms that support Windows. For information about the use of this setting and option, see [Firewall configuration service provider (CSP)](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx).

Applies to:  

- Windows 10
- Windows 11

#### Endpoint security firewall policy support for network list manager settings<!-- 9803477  -->  
We've added a pair of network list manager settings to [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune). You can use the network list manager settings to help determine when an Azure AD device is or isn't on your on-premises domain subnets so firewall rules can properly apply.

The following settings are found in a new category named *Network List Manager*, that's available in the *Microsoft Defender Firewall* profile template for the *Windows 10, Windows 11, and Windows Server* platform:

- Allowed Tls Authentication Endpoints
- Configured Tls Authentication Network Name

For information about Network Categorization settings, see [NetworkListManager CSP](/windows/client-management/mdm/policy-csp-networklistmanager).

Applies to:  

- Windows 10
- Windows 11

#### Improvements to Devices area in admin center (public preview) <!-- 12775837 -->  
The Devices area in the admin center now has a more consistent UI, with more capable controls and an improved navigation structure so you can find the information you need faster. To opt in to the public preview and try out the new experience, go to **Devices** and flip the toggle at the top of the page. Improvements include:

* A new scenario-focused navigation structure.
* New location for platform pivots to create a more consistent navigation model.
* A reduction in journey, helping you get to your destination faster.
* Monitoring and reports are within the management workflows, giving you easy access to key metrics and reports without having to leave the workflow.
* A consistent way across list views to search, sort, and filter data.

For more information about the updated UI, see [Try new Devices experience in Microsoft Intune](microsoft-intune-admin-center-devices.md).

### Device security

#### Microsoft Intune Endpoint Privilege Management (public preview)<!-- 15654169   -->  
As a public preview, you can now use Microsoft Intune Endpoint Privilege Management. With Endpoint Privilege Management, admins can set policies that allow standard users to perform tasks normally reserved for an administrator. Endpoint Privilege Management can be configured in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) at **Endpoint security** > **Endpoint Privilege Management**.

With the public preview, you can configure policies for *automatic* and *user-confirmed* workflows that elevate the run-time permissions for apps or processes you select. You then assign these policies to users or devices that have end users running without Administrator privileges. Once policy is received, Endpoint Privilege Management will broker the elevation on behalf of the user, allowing them to elevate approved applications without needing full administrator privileges. The preview also includes built-in insights and reporting for Endpoint Privilege Management.

To learn how to activate the public preview and use Endpoint Privilege Management policies, start with [Use Endpoint Privilege Management with Microsoft Intune](../protect/epm-overview.md). Endpoint Privilege Management is part of the [Intune Suite](../fundamentals/intune-add-ons.md) offering, and free to try while it remains in public preview.

### Intune apps

#### Newly available protected apps for Intune<!-- 16927438, 17030201, 17074872 17103353 -->  
The following protected apps are now available for Microsoft Intune:

- EVALARM by GroupKom GmbH (iOS)
- ixArma by INAX-APPS (Android)
- Seismic | Intune by Seismic Software, Inc.
- Microsoft Viva Engage by Microsoft (formally Microsoft Yammer)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Diagnostic data collection for Endpoint Privilege Management<!-- 17392824   -->  
To support the release of Endpoint Privilege Management, we've updated [Collect diagnostics from a Windows device](../remote-actions/collect-diagnostics.md) to include the following data, which is collected from devices enabled for Endpoint Privilege Management:

- Registry keys:  
  - HKLM\SOFTWARE\Microsoft\EPMAgent

- Commands:  
  - %windir%\system32\pnputil.exe /enum-drivers
 
- Log files:  
  - %ProgramFiles%\Microsoft EPM Agent\Logs\\\*.*
  - %windir%\system32\config\systemprofile\AppData\Local\mdm\\\*.log

#### View status for pending and failed organizational messages<!-- 17017707  -->  
We've added two more states to organizational message reporting details to make it easier to track pending and failed messages in the admin center.

- **Pending**: The message has not been scheduled yet and is currently in progress.
- **Failed**: The message failed to schedule due to a service error.

For information about reporting details, see [View reporting details for organizational messages](../remote-actions/organizational-messages-reporting.md).  


#### Additional reporting information related to tenant attach devices<!-- 9220597  -->  
You can now view information for tenant attach devices in the existing antivirus reports under the Endpoint Security workload. A new column differentiates between devices managed by Intune and devices managed by Configuration Manager. This reporting information is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Endpoint security** > **Antivirus**.

## Week of March 13, 2023

### Device management

#### Meta Quest 2 and Quest Pro are now in Open Beta (US only) on Microsoft Intune for Android Open Source Devices

Microsoft Intune for Android open source project devices (AOSP) has welcomed Meta Quest 2 and Quest Pro into Open Beta for the US market.

For more information, go to [Operating systems and browsers supported by Microsoft Intune](../fundamentals/supported-devices-browsers.md)

Applies to:

- Microsoft Intune (AOSP)  

### App management

#### Trusted Root Certificates Management for Intune App SDK for Android<!-- 15135752 -->
If your Android application requires SSL/TLS certificates issued by an on-premises or private certificate authority to provide secure access to internal websites and applications, the Intune App SDK for Android now has support for certificate trust management. For more information and examples, see [Trusted Root Certificates Management](../developer/app-sdk-android-phase7.md#trusted-root-certificates-management).

#### System context support for UWP apps<!-- 16544103 -->
In addition to user context, you can deploy Universal Windows Platform (UWP) apps from the **Microsoft Store app (new)** in system context. If a provisioned *.appx* app is deployed in system context, the app auto-installs for each user that logs in. If an individual end user uninstalls the user context app, the app still shows as installed because it's still provisioned. In addition, the app must not already be installed for any users on the device. Our general recommendation is to not mix install contexts when deploying apps. Win32 apps from the **Microsoft Store app (new)** already support system context.

## Week of March 6, 2023  

### App management

#### Deploy Win32 apps to device groups<!-- 7359954 -->
You can now deploy Win32 apps with **Available** intent to device groups. For more information, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md). 

### Device management  

#### New URL for Microsoft Intune admin center<!-- 17441426 -->  
The Microsoft Intune admin center has a new URL: [https://intune.microsoft.com](https://intune.microsoft.com). The previously used URL, [https://endpoint.microsoft.com](https://endpoint.microsoft.com), continues to work but will redirect to the new URL in late 2023. We recommend taking the following actions to avoid issues with Intune access and automated scripts: 

* Update login or automation to point to `https://intune.microsoft.com`. 
* Update your firewalls, as needed, to allow access to the new URL. 
* Add the new URL to your favorites and bookmarks. 
* Notify your helpdesk and update IT administrator documentation.  

### Tenant administration

#### Add CMPivot queries to Favorites folder<!-- 16702226 -->
You can add your frequently used queries to a **Favorites** folder in CMPivot. CMPivot allows you to quickly assess the state of a device managed by Configuration Manager via Tenant Attach and take action. The functionality is similar to one already present in the Configuration Manager console. This addition helps you keep all your most used queries in one place. You can also add tags to your queries to help search and find queries. The queries saved in the Configuration Manager console aren't automatically added to your **Favorites** folder. You need to create new queries and add them to this folder. For more information about CMPivot, see [Tenant attach: CMPivot usage overview](../../configmgr/tenant-attach/cmpivot-start.md).

### Device enrollment

#### New Microsoft Store apps now supported with the Enrollment Status Page<!-- 16280325 -->
The Enrollment Status Page (ESP) now supports the new Microsoft store applications during Windows Autopilot. This update enables better support for the new Microsoft Store experience and should be rolling out to all tenants starting with Intune 2303. For related information, see [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).

## Week of February 27, 2023

### Device configuration

#### Support for Locate device on Android Enterprise corporate owned fully managed and Android Enterprise corporate owned work profile devices<!--12391424 -->

You can now use "Locate device" on Android Enterprise corporate owned fully managed and Android Enterprise corporate owned work profile devices. With this feature, admins are able to locate lost or stolen corporate devices on-demand.

In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you need to turn the feature on using **Device Restrictions** in **Device Configuration** for Android Enterprise.

Select **Allow** on the **Locate device** toggle for fully managed and corporate owned work profile devices and select applicable groups. **Locate device** is available when you select **Devices**, and then select **All devices**. From the list of devices you manage, select a supported device, and choose the **Locate device** remote action.

For information on locating lost or stolen devices with Intune, go to:

- [Locate lost or stolen devices with Intune](../remote-actions/device-locate.md)

Applies to:

- Android Enterprise corporate owned fully managed
- Android Enterprise corporate owned dedicated devices
- Android Enterprise corporate owned work profile

#### Intune add-ons <!-- 13817801 -->

Microsoft Intune Suite provides mission-critical advanced endpoint management and security capabilities into Microsoft Intune. 

You can find add-ons to Intune in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) under **Tenant administration** > **Intune add-ons**.

For detailed information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

#### View ServiceNow Incidents in the Intune Troubleshooting workspace (Preview)<!-- 12508062 -->

In public preview, you can view a list of ServiceNow incidents associated with the user you've selected in the Intune Troubleshooting workspace. This new feature is available under **Troubleshooting + Support** > select a user > **ServiceNow Incidents**. The list of incidents shown have a direct link back to the source incident and show key information from the incident. All incidents listed link the "Caller" identified in the incident with the user selected for Troubleshooting.

For more information, go to [Use the troubleshooting portal to help users at your company](service-now-integration.md).

### Device security

#### Microsoft Tunnel for MAM is now generally available<!-- 16883728  -->

Now out of preview and generally available, you can add [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-overview.md) to your tenant. Tunnel for MAM supports connections from unenrolled [Android](../protect/microsoft-tunnel-mam-android.md) and [iOS](../protect/microsoft-tunnel-mam-ios.md) devices. This solution provides your tenant with a lightweight VPN solution that allows mobile devices access to corporate resources while adhering to your security policies.

In addition, MAM Tunnel for iOS now supports Microsoft Edge.

Previously, Tunnel for MAM for Android and iOS was in public preview and free for use. With this release as generally available, this solution now requires an add-on license for its use.

For licensing details, see [Intune add-ons](../fundamentals/intune-add-ons.md).

Applies to:  
- Android
- iOS  

### Tenant administration  

#### Organizational messages now support custom destination URLs <!-- 16576068  -->

You can now add any custom destination URL to organizational messages in the taskbar, notifications area, and Get Started app. This feature applies to Windows 11. Messages created with Azure AD-registered domains that are in a scheduled or active state are still supported. For more information, see [Create organizational messages](../remote-actions/organizational-messages-create.md?tabs=taskbar#step-1-create-a-message). 

## Week of February 20, 2023 (Service release 2302)

### App management

#### Latest iOS/iPadOS version available as minimum OS requirement for LOB and store apps<!-- 16433620  -->  
You can specify iOS/iPadOS 16.0 as the minimum operating system for line-of-business and store app deployments. This setting option is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** > *iOS store app or Line-of-business app*. For more information about managing apps, see [Add apps to Microsoft Intune](../apps/apps-add.md).

#### Newly available protected app for Intune<!-- 16655639  -->  
The following protected app is now available for Microsoft Intune:

- Egnyte for Intune by Egnyte

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Device configuration

#### Endpoint Manager admin center is renamed to Intune admin center<!-- 15560662   -->  
The Microsoft Endpoint Manager admin center is now called the **Microsoft Intune admin center**.

#### A new Associated Assignments tab for your filters<!-- 7538503  -->  
When you assign an app or policy, you can filter the assignment using different device properties, such as device manufacturer, model, and ownership. You can create and associate a filter with the assignment.

After you create a filter, there's a new **Associated Assignments tab**. This tab shows all the policy assignments, the groups that receive the filter assignments, and if the filter is using **Exclude** or **Include**:

1. Sign in to the Microsoft Intune admin center.
2. Go to **Devices** > **Filters** > Select an existing filter > **Associated Assignments tab**.
 
For more information on filters, go to:

- [Use filters when assigning your apps, policies, and profiles in Intune](filters.md)
- [Device properties, operators, and rule editing when creating filters in Intune](filters-device-properties.md)

#### Size and generation included in iOS/iPadOS model information<!-- 16406692  -->  
You can view the size and generation for enrolled iOS/iPadOS devices as part of the **Model** attribute in **Hardware device details**.

Go to **Devices > All devices** > select one of your listed devices and select **Hardware** to open its details. For example, iPad Pro 11-inch (3rd generation) displays for the device model instead of iPad Pro 3. For more information, go to: [See device details in Intune](../remote-actions/device-inventory.md#hardware-device-details)

Applies to:  
- **iOS/iPadOS**

#### Disable Activation Lock device action for supervised iOS/iPadOS devices<!-- 15571509 -->  
You can use the **Disable Activation Lock** device action in Intune to bypass Activation Lock on iOS/iPadOS devices without requiring the current username or password.

This new action is available under  **Devices > iOS/iPadOS >** *select one of your listed devices* **> Disable Activation Lock**.

More information on managing Activation Lock is available at [Bypass iOS/iPadOS Activation Lock with Intune](../remote-actions/device-activation-lock-disable.md) or on Apple's website at [Activation Lock for iPhone, iPad, and iPod touch - Apple Support.](https://support.apple.com/en-us/HT201365)

Applies to:  
- **iOS/iPadOS**

#### Allow Temporary Enterprise Feature Control is available in the Settings Catalog<!-- 15752120  -->  
In on-premises group policy, there's an **Enable features introduced via servicing that are off by default** setting.

In Intune, this setting is known as **Allow Temporary Enterprise Feature Control** and is available in the Settings Catalog. This servicing adds features that off by default. When set to **Allowed**, these features are enabled and turned on.

For more information on this feature, go to:

- [AllowTemporaryEnterpriseFeatureControl](/windows/client-management/mdm/policy-csp-Update#allowtemporaryenterprisefeaturecontrol) policy CSP
- [Blog: Commercial control for continuous innovation](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/commercial-control-for-continuous-innovation/ba-p/3737575)

The Windows features that enabled by this policy setting will be released later in 2023. Intune is releasing this policy setting now for your awareness and preparation, which is before any need to use the setting with future Windows 11 releases.

For more information on the settings catalog, go to [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md).

Applies to:

- Windows 11

### Device management

#### Device Control support for Printer Protection (Preview)<!-- 12355154  -->  
In public preview, Device Control profiles for Attack Surface Reduction policy now support [reusable settings groups for Printer Protection](../protect/reusable-settings-groups.md#add-reusable-groups-to-a-device-control-profile).

Microsoft Defender for Endpoint Device Control [Printer Protection](/microsoft-365/security/defender-endpoint/printer-protection-overview) enables you to audit, allow, or prevent printer with or without exclusions within Intune. It allows you to block users from printing via a non-corporate network printer or non-approved USB printer. This feature adds an additional layer of security and data protection for work from home and remote work scenarios.

Applies to:  
- Windows 10
- Windows 11

#### Support to delete stale devices that are managed through Security Management for Microsoft Defender for Endpoint<!--14729617  -->   
You can now **Delete** a device that's managed through the [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md) solution from within the Microsoft Intune admin center. The delete option appears along with other device management options when you view the device's Overview details. To locate a device managed by this solution, in the admin center go to **Devices** > **All devices**, and then select a device that displays either *MDEJoined* or *MDEManaged* in the *Managed by* column.

#### New settings and setting options available in the Apple Settings Catalog<!-- 16813380  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Login > Service Management - Managed Login Items**:

- Team Identifier

**Microsoft Office > Microsoft Office**:

- Office Activation Email Address

Applies to:  
- macOS

**Networking > Domains**:

- Cross Site Tracking Prevention Relaxed Domains

Applies to:  
- iOS/iPadOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Device security
 
#### Use Endpoint security Antivirus policy to manage Microsoft Defender update behavior (Preview)<!-- 11890335 -->  
As part of a public preview for Endpoint security [Antivirus policy](../protect/endpoint-security-antivirus-policy.md), you can use the new profile **Defender Update controls** for the *Windows 10 and later* platform to manage update settings for Microsoft Defender. The new profile includes settings for the rollout release channel by which devices and users receive Defender Updates that are related to daily security intelligence updates, monthly platform updates, and monthly engine updates.

This profile includes the following settings, which are all directly taken from [Defender CSP - Windows Client Management](/windows/client-management/mdm/policy-csp-Defender).

- Engine Updates Channel
- Platform Updates Channel
- Security Intelligence Updates Channel

These settings are also available from the [settings catalog](../configuration/settings-catalog.md) for the *Windows 10 and later* profile.

Applies to:  
- Windows 10
- Windows 11

## Week of February 6, 2023

### Tenant administration

#### Apply recommendations and insights to enrich the Configuration Manager site health and device management experience<!--16957774 -->

You can now use the Microsoft Intune admin center to view recommendations and insights for your Configuration Manager sites. These recommendations can help you improve the site health and infrastructure and enrich the device management experience.

Recommendations include:  

- How to simplify your infrastructure
- Enhance device management
- Provide device insights
- Improve the health of the site

To view recommendations, open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Connectors and tokens** > **Microsoft Endpoint Configuration Manager**,  and select a *site* to view recommendations for that site.  Once selected, the *Recommendations* tab displays each insight along with a *Learn more* link. This link opens details on how to apply that recommendation.

For more information, see [Enable Microsoft Intune tenant attach - Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md).

## Week of January 30, 2023

### Device management

#### HTC Vive Focus 3 supported on Microsoft Intune for Android Open Source Devices<!--15670082--> 

Microsoft Intune for Android open source project devices (AOSP) now supports HTC Vive Focus 3. 

For more information, go to [Operating systems and browsers supported by Microsoft Intune](../fundamentals/supported-devices-browsers.md)

Applies to:

- Microsoft Intune (AOSP)
#### Introducing support for laser pointers in Remote Help<!-- 16108312 -->

In Remote Help, you can now use a laser pointer when you're providing assistance on Windows.

For more information on Remote Help, go to [Remote Help](/mem/intune/fundamentals/remote-help).

Applies to:

 - Windows 10/11
## Week of January 23, 2023 (Service release 2301)

### App management

#### Configure whether to show Configuration Manager apps in Windows Company Portal<!-- 9135109 -->
In Intune, you can choose whether to show or hide Configuration Manager apps from appearing in the Windows Company Portal. This option is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Customization**. Next to **Settings**, select **Edit**. The option to **Show** or **Hide** the Configuration Manager applications are located in the **App Sources** section of the pane. For related information about configuring the Company Portal app, see [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

#### Block pinning web pages to Managed Home Screen app<!-- 15593458 -->
On Android Enterprise dedicated devices using Managed Home Screen, you can now use app configuration to configure the Managed Home Screen app to block pinning browser web pages to Managed Home Screen. The new `key` value is `block_pinning_browser_web_pages_to_MHS`. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

### Device management

#### Grace period status visible in Microsoft Intune app for Android<!-- 13498225 -->  
The Microsoft Intune app for Android now shows a grace period status to account for devices that don't meet compliance requirements but are still within their given grace period. Users can see the date by which devices must be compliant, and the instructions for how to become compliant. If they don't update their device by the given date, the device is marked as noncompliant. For more information, see the following docs:  
- [Configure compliance policies with actions for noncompliance](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance)    
- [Check compliance status](../user-help/check-compliance-microsoft-intune-app-android.md)  


#### Software update policies for macOS are now generally available<!-- 12393100 -->   
Software update policies for macOS devices are now generally available. This general availability applies to supervised devices running macOS 12 (Monterey) and later. We will continue to add improvements to this feature going forward.  

For more information, see [Use Microsoft Intune policies to manage macOS software updates](../protect/software-updates-macos.md).

#### Windows Autopilot device diagnostics<!-- 16697347 -->
Windows Autopilot diagnostics is available to download in Microsoft Intune admin center from either in the Autopilot deployments monitor or Device Diagnostics monitor for an individual device.

### Device enrollment

#### Enrollment notifications now generally available<!-- 16545401 -->
Enrollment notifications are now generally available, and are supported on Windows, Apple, and Android devices. This feature is only supported with user-driven enrollment methods. For more information, see [Set up enrollment notifications](../enrollment/enrollment-notifications.md).  

#### Skip or show Terms of Address pane in Setup Assistant<!-- 14661838 -->  
Configure Microsoft Intune to skip or show a new Setup Assistant pane called **Terms of Address** during Apple Automated Device Enrollment. The Terms of Address pane lets users on iOS/iPadOS and macOS devices personalize their device by selecting how the system addresses them: feminine, neutral, or masculine.  The pane is visible during enrollment by default, and is available for select languages.  You can hide it on devices running iOS/iPadOS 16 and later, and macOS 13 and later. For more information about the Setup Assistant screens supported in Intune, see:  

- [Setup Assistant screens for Macs](../enrollment/device-enrollment-program-enroll-macos.md#setup-assistant-screen-reference)
- [Setup Assistant screens for iOS/iPadOS](../enrollment/device-enrollment-program-enroll-ios.md#setup-assistant-screen-reference)

### Device security

#### Microsoft Tunnel for Mobile Application Management for iOS/iPadOS (Preview)<!-- 15769204, 9851288 -->  

As a public preview, you can use the Mobile Application Management (MAM) to the Microsoft Tunnel VPN gateway for iOS/iPadOS. With this preview for iOS devices that haven't enrolled with Intune, supported apps on those unenrolled devices can use Microsoft Tunnel to connect to your organization when working with corporate data and resources. This feature includes VPN gateway support for:

- Secure access to on-premises apps and resources using modern authentication
- Single Sign On and conditional access

For more information, go to:

- [Microsoft Tunnel for Mobile Application Management for iOS/iPadOS admin guide (public preview)](../protect/microsoft-tunnel-mam-ios.md)
- [Microsoft Tunnel for MAM iOS SDK developer guide](../developer/tunnel-mam-ios-sdk.md)

Applies to:

- iOS/iPadOS

####  Attack surface reduction policy support for Security settings management for Microsoft Defender for Endpoint <!-- 13816760 -->  
Attack surface reduction policy is supported by devices managed through the [MDE Security configuration](../protect/mde-security-integration.md#which-solution-should-i-use) scenario. To use this policy with devices that use Microsoft Defender for Endpoint but aren't enrolled with Intune:

1. In the Endpoint Security node, create a new *Attack surface reduction* policy.
2. Select **Windows 10, Windows 11, and Windows Server** as the *Platform*.
3. Select **Attack Surface Reduction Rules** for the *Profile*.  

Applies to:  
- Windows 10
- Windows 11

#### SentinelOne – New mobile threat defense partner<!-- 13911932 -->
You can now use [SentinelOne](../protect/sentinelone-mobile-threat-defense-connector.md) as an integrated Mobile Threat Defense (MTD) partner with Intune. By configuring the SentinelOne connector in Intune, you can control mobile device access to corporate resources using conditional access that's based on risk assessment in your compliance policy. The SentinelOne connector can also send risk levels to app protection policies.

### Device configuration

#### Device Firmware Configuration Interface (DFCI) supports Fujitsu devices<!--10249866 -->

For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type).

Some Fujitsu devices running Windows 10/11 are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

For more information about DFCI profiles, go to:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](../../autopilot/dfci-management.md)

Applies to:

- Windows 10
- Windows 11

#### Support for Bulk Device Actions on devices running Android AOSP<!--15397458 -->
You can now complete "Bulk Device Actions" for devices running Android AOSP. The bulk device actions supported on devices running AOSP are Delete, Wipe and Restart.

Applies to:  
- AOSP

#### Updated descriptions for iOS/iPadOS and macOS settings in the settings catalog<!-- 16360170 -->
The settings catalog lists all the settings you can configure, and all in one place. For the iOS/iPadOS and macOS settings, for each setting category, the descriptions are updated to include more detailed information.

For more information on the settings catalog, go to:
- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md)
- [Common tasks you can complete using the Settings Catalog in Intune](../configuration/settings-catalog-common-features.md)

Applies to:
- iOS/iPadOS
- macOS

#### New settings available in the Apple Settings Catalog<!--16237513  -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Accounts > Subscribed Calendars**:
- Account Description
- Account Host Name
- Account Password
- Account Use SSL
- Account Username

Applies to:
- iOS/iPadOS

**Networking > Domains**:
- Cross Site Tracking Prevention Relaxed Domains

Applies to:
- macOS

The following settings are also in Settings Catalog. Previously, they were only available in Templates:

**File Vault**:
- User Enters Missing Info 

Applies to:
- macOS

**Restrictions**:
- Rating Region

Applies to:
- iOS/iPadOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).


#### Filter app and policy assignments by the device's Azure AD Join type (`deviceTrustType`)<!-- 8110331 -->
When you assign an app or policy, you can filter the assignment using different device properties, such as device manufacturer, operating system SKU, and more.

A new device filter property `deviceTrustType` is available for Windows 10 and later devices. With this property, you can filter app and policy assignments depending on the Azure AD Join type, with values of "Azure AD Joined", "Hybrid Azure AD Joined", and "Azure AD registered".

For more information on filters and the device properties you can use, go to:
- [Use filters when assigning your apps, policies, and profiles in Intune](filters.md)
- [Device properties, operators, and rule editing when creating filters in Intune](filters-device-properties.md)

Applies to:

- Windows 10 and later

### Monitor and troubleshoot

#### Download mobile app diagnostics in the Microsoft Intune admin center (public preview)<!-- 9353471 -->  
Now in public preview, access user-submitted mobile app diagnostics in the admin center, including app logs sent through Company Portal app for Android, AOSP, or Windows, with support for iOS, macOS, and Microsoft Edge for iOS coming at a later date. For more information about accessing mobile app diagnostics for Company Portal, see [Configure Company Portal](../apps/company-portal-app.md#app-logs).

#### WinGet troubleshooting using diagnostic files<!-- 16724699 -->
[WinGet](/windows/package-manager/winget/) is a command line tool that enables you to discover, install, upgrade, remove, and configure applications on Windows 10 and Windows 11 devices. When working with [Win32 app management in Intune](../apps/apps-win32-app-management.md), you can now use the following file locations to help troubleshoot WinGet:
- *%TEMP%\winget\defaultstate\*.log*
- *Microsoft-Windows-AppXDeployment/Operational*
- *Microsoft-Windows-AppXDeploymentServer/Operational*

#### Intune troubleshooting pane update<!-- 4442647 -->  
A new experience for the Intune Troubleshooting pane provides details about user's devices, policies, applications, and status. The troubleshooting pane includes the following information:

- A summary of policy, compliance, and application deployment status.
- Support for exporting, filtering, and sorting all reports.
- Support to filter by excluding policies and applications.
- Support to filter to a user's single device.
- Details about available device diagnostics and disabled devices.
- Details about offline devices that haven't checked-in to the service for three or more days.

You can find the troubleshooting pane in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Troubleshoot**. To view the new experience during preview, select **Preview upcoming changes to Troubleshooting and provide feedback** to display the **Troubleshooting preview** pane, then select **Try it now**.

#### New report for devices without compliance policy (preview)<!--14911124 --> 
We've added a new report named **Devices without compliance policy** to the Device compliance reports you can access through the *Reports* node of the Microsoft Intune admin center.  This report, which is in preview, uses a  newer reporting format that provides for more capabilities.

To learn about this new organizational report, see [Devices without compliance policy (preview) (Organizational)](../fundamentals/reports.md#devices-without-compliance-policy-preview-organizational).

An older version of this report remains available through the *Devices > Monitor* page of the admin center. Eventually, that older report version will be retired, though it remains available for now.  

#### Service health messages for tenant issues that require administrative attention<!-- 14791676 -->  
The *Service health and message center page* in the Microsoft Intune admin center can now display messages for **Issues in your environment that require action**. These messages are important communications that are sent to a tenant to alert administrators about issues in their environment that might require action to resolve. 

You can view messages for *Issues in your environment that require action* in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by going to **Tenant administration** > **Tenant status** and then selecting the **Service health and message center** tab.

For more information about this page of the admin center, see [View details about your Tenant on the Intune tenant status page](../fundamentals/tenant-status.md).

### Tenant administration

#### Improved UI experience for multiple certificate connectors<!-- 16263248 -->
We've added pagination controls to the *Certificate connectors* view to help improve the experience when you have more than 25 certificate connectors configured. With the new controls, you can see the total number of connector records and easily navigate to a specific page when viewing your certificate connectors.

To view certificate connectors, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Tenant administration** > **Connectors and tokens** > **Certificate connectors**.

### Intune apps

#### Newly available protected app for Intune<!-- 16620158 -->
The following protected app is now available for Microsoft Intune:
- Voltage SecureMail by Voltage Security

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Scripts

#### Preview PowerShell script package content in Endpoint Analytics<!-- 12930245 -->
Admins can now see a preview of a PowerShell script's content for proactive remediations. The content is displayed in a grayed-out box with scrolling capability. Admins can't edit the content of the script in the preview. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports** > **Endpoint analytics** > **Proactive remediations**. For related information, see [PowerShell scripts for Proactive remediations](../../analytics/powershell-scripts.md).

## Week of January 16, 2023

### App management

#### Win32 app supersedence GA<!-- 9318154 -->
We have rolled out the feature set for Win32 app supersedence GA, which adds support for apps with supersedence during ESP and also allows supersedence and dependency relationships to be added in the same app subgraph. For more information, see [Win32 app supersedence improvements](https://aka.ms/Intune/Win32-Supersedence). For information about Win32 app supersedence, see [Add Win32 app supersedence](../apps/apps-win32-supersedence.md).

## Week of January 9, 2023

### Device configuration

#### The Company Portal app enforces Password Complexity setting on Android Enterprise 12+ personally owned devices with a work profile<!-- 16211313  -->  

On Android Enterprise 12+ personally owned devices with a work profile, you can create a compliance policy and/or device configuration profile that sets the password complexity. Starting with the 2211 release, this setting is available in the Intune admin center:

- **Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > Personally owned with a work profile
- **Devices** > **Compliance policies** > **Create policy** > **Android Enterprise** for platform > Personally owned with a work profile

The Company Portal app enforces the **Password complexity** setting.

For more information on this setting and the other settings you can configure on personally owned devices with a work profile, go to:

- [Device compliance settings for Android Enterprise in Intune](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile)
- [Device restriction settings list for Android Enterprise in Intune](../configuration/device-restrictions-android-enterprise-personal.md)

Applies to:

- Android Enterprise 12+ personally owned devices with a work profile

## Week of December 19, 2022

### Intune apps

#### Newly available protected app for Intune<!-- 15448654 -->
The following protected app is now available for Microsoft Intune:
- Appian for Intune by Appian Corporation (Android)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of December 12, 2022 (Service release 2212)

### Device configuration

#### Remote Help client app includes a new option to disable chat functionality in the Tenant level setting<!-- 14685052 -->  
In the Remote Help app, admins can disable chat functionality from the new tenant level setting. Turning on the disable chat feature removes the chat button in the Remote Help app. This setting can be found in the Remote Help **Settings** tab under **Tenant Administration** in Microsoft Intune.

For more information, see [Configure Remote Help for your tenant](/mem/intune/fundamentals/remote-help#configure-remote-help-for-your-tenant).

**Applies to**: Windows 10/11

#### New settings available in the macOS Settings Catalog<!-- 16069006 -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**File Vault > File Vault Options**:

- Block FV From Being Disabled
- Block FV From Being Enabled

**Restrictions**:

- Allow Bluetooth Modification

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### There are default settings for SSO extension requests on iOS, iPadOS, and macOS devices<!-- 15082414-15084030 -->  

When you create a single sign-on app extension configuration profile, there are some settings you configure. The following settings use the following default values for all SSO extension requests:

- **AppPrefixAllowList** key
  - macOS default value: `com.microsoft.,com.apple.`
  - iOS/iPadOS default value: `com.apple.`

- **browser_sso_interaction_enabled** key
  - macOS default value: `1`
  - iOS/iPadOS default value: `1`

- **disable_explicit_app_prompt** key
  - macOS default value: `1`
  - iOS/iPadOS default value: `1`

If you configure a value other than the default value, then the configured value overwrites the default value. 

For example, you don't configure the `AppPrefixAllowList` key. By default, all Microsoft apps (`com.microsoft.`) and all Apple apps (`com.apple.`) are enabled for SSO on macOS devices. You can overwrite this behavior by adding a different prefix to the list, such as `com.contoso.`.

For more information on the Enterprise SSO plug-in, go to [Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS and macOS devices in Microsoft Intune](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)

Applies to:

- iOS/iPadOS
- macOS

### Device enrollment

#### Enrollment token lifetime increases to 65 years for Android Enterprise dedicated devices<!-- 15094454  -->  
Now you can create an enrollment profile for Android Enterprise dedicated devices that's valid for up to 65 years.  If you have an existing profile, the enrollment token still expires at whatever date you chose when you created the profile, but during renewal you can extend the lifetime. For more information about creating an enrollment profile, see [Set up Intune enrollment for Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md#create-an-enrollment-profile).

### Device management

#### Update policies for macOS now available for all supervised devices<!-- 16141990  -->  
Software update policies for macOS devices now apply to all macOS supervised devices. Previously, only those devices that enrolled through Automated Device Enrollment (ADE) would qualify to receive updates. For more information on configuring update policies for macOS, see [Use Microsoft Intune policies to manage macOS software updates](../protect/software-updates-macos.md).

Applies to:  
- macOS

#### Policy and reports for Windows feature updates and expedited quality updates are now Generally Available<!-- 15738456 -->  
Both the policies and reports for managing feature updates and quality updates (expedited updates) for Windows 10 and later, are out of preview and now generally available.

For more information about these policies and reports, see:

- [Feature updates policy](../protect/windows-10-feature-updates.md)
- [Expedite quality updates policy](../protect/windows-10-expedite-updates.md)
- [Windows Update compliance reports](../protect/windows-update-compliance-reports.md)

Applies to:  
-  Windows 10/11

## Week of November 28, 2022

### App management

#### Microsoft Store apps in Intune<!-- 12708346 -->  
You can now search, browse, configure, and deploy Microsoft Store apps within Intune. The new Microsoft Store app type is implemented using the Windows Package Manager. This app type features an expanded catalog of apps, which includes both UWP apps and Win32 apps. Roll out of this feature is expected to complete by December 2, 2022.  For more information, see [Add Microsoft Store apps to Microsoft Intune](../apps/store-apps-microsoft.md).

### Tenant administration

#### Access policies for multiple Administrator Approval (public preview)<!-- 9348867  -->
In public preview, you can use Intune *access policies* to require that a second Administrator Approval account be used to approve a change before the change is applied. This capability is known as multiple Administrator Approval (MAA).

You create an access policy to protect a type of resource, like App deployments. Each access policy also includes a group of users who are *approvers* for the changes protected by the policy. When a resource like an app deployment configuration is protected by an access policy, any changes that are made to the deployment, including creating, deleting, or modifying an existing deployment won't apply until a member of the approvers group for that access policy reviews and approves that change.

Approvers can also reject requests, and both the individual requesting a change and the approver can provide notes about the change, or why it was approved or rejected.

Access policies are supported for the following resources:

- **Apps** – Applies to [app deployments](../apps/apps-add.md), but doesn't apply to app protection policies.
- **Scripts** – Applies to deploying scripts to devices that run [macOS](../apps/macos-shell-scripts.md) or [Windows](../apps/intune-management-extension.md).

For more information, see [Use Access policies to require multiple administrative approval](../fundamentals/multi-admin-approval.md).  

### Device security

#### Microsoft Tunnel for Mobile Application Management for Android (Preview)<!-- 15769204 -->  
As a public preview, you can now use Microsoft Tunnel with unenrolled devices. This capability is called [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-mam.md) (MAM). This preview supports Android, and without any changes to your existing Tunnel infrastructure, supports the Tunnel VPN gateway for:

- Secure access to on-premises apps and resources using modern authentication
- Single Sign On and conditional access

To use Tunnel MAM, unenrolled devices must install Microsoft Edge, Microsoft Defender for Endpoint, and the Company Portal. You can then use the Microsoft Intune admin center to configure the following profiles for the unenrolled devices:

- An App configuration profile for managed apps, to configure Microsoft Defender on devices for use as the Tunnel client app.
- A second App configuration profile for managed apps, to configure Microsoft Edge to connect to Tunnel.
- An App protection profile to enable automatic start of the Microsoft Tunnel connection.

Applies to:  
- Android Enterprise

## Week of November 14, 2022 (Service release 2211)

### App management

#### Control the display of Managed Google Play apps<!-- 621615   -->  
You can group Managed Google Play apps into collections and control the order that collections are displayed when selecting apps in Intune. You can also make apps visible via search only. This capability is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **All apps** > **Add** > **Managed Google Play app**. For related information, see [Add a Managed Google Play store app directly in the Intune admin center](../apps/apps-add-android-for-work.md#add-a-managed-google-play-store-app-directly-in-the-microsoft-intune-admin-center).

### Device configuration

#### New password complexity setting for Android Enterprise 12+ personally owned devices with a work profile<!-- 12436068  -->  
On Android Enterprise 11 and older personally owned devices with a work profile, you can set the following password settings:

- **Compliance policies** > **Android Enterprise for platform** > **Personally owned work profile** > **System security** > **Required password type**, **Minimum password length**
- **Device configuration profiles** > **Android Enterprise for platform** > **Personally owned work profile** > **Device restrictions** > **Work profile settings** > **Required password type**, **Minimum password length**
- **Device configuration profiles** > **Android Enterprise for platform** > **Personally owned work profile** > **Device restrictions** > **Password** > **Required password type**, **Minimum password length**

Google is deprecating the **Required password type** and **Minimum password length** settings for Android 12+ personally owned devices with a work profile and replacing them with new password complexity requirements. For more information about this change, go to [Day zero support for Android 13](https://aka.ms/Intune/Android13).

The new **Password complexity** setting has the following options:

- **None**: Intune doesn't change or update this setting. By default, the OS may not require a password.
- **Low**: Pattern or PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked.
- **Medium**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length, alphabetic length, or alphanumeric length must be at least 4 characters.
- **High**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length must be at least 8 characters. The alphabetic or alphanumeric length must be at least 6 characters.

On Android 12+, if you currently use the **Required password type** and **Minimum password length** settings in a compliance policy or device configuration profile, then we recommend using the new **Password complexity** setting instead.

If you continue to use the **Required password type** and **Minimum password length** settings, and don't configure the **Password complexity** setting, then new devices running Android 12+ might default to the **High** password complexity.

For more information on these settings and what happens to existing devices with the deprecated settings configured, go to:

- [Android Enterprise personally owned devices with a work profile - configuration profile settings list](../configuration/device-restrictions-android-enterprise-personal.md)
- [Android Enterprise personally owned devices with a work profile - compliance policy settings list](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile)

Applies to:

- Android Enterprise 12.0 and newer personally owned devices with a work profile

#### New settings available in the iOS/iPadOS and macOS Settings Catalog<!-- 16068756 -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Networking > DNS Settings**:

- DNS Protocol
- Server Addresses
- Server Name
- Server URL
- Supplemental Match Domains
- On Demand Rules
- Action
- Action Parameters
- DNS Domain Match
- DNS Server Address Match
- Interface Type Match
- SSID Match
- URL String Probe
- Prohibit Disablement

**File Vault**:

- Defer
- Defer Don't Ask At User Logout
- Defer Force At User Login Max Bypass Attempts
- Enable
- Show Recovery Key
- Use Recovery Key

**File Vault > File Vault Recovery Key Escrow**:

- Device Key
- Location

**Restrictions**:

- Allow Air Play Incoming Requests

Applies to:

- macOS

**Web > Web Content Filter**:

- Allow List Bookmarks
- Auto Filter Enabled
- Deny List URLs
- Filter Browsers
- Filter Data Provider Bundle Identifier
- Filter Data Provider Designated Requirement
- Filter Grade
- Filter Packet Provider Bundle Identifier
- Filter Packet Provider Designated Requirement
- Filter Packets
- Filter Sockets
- Filter Type
- Organization
- Password
- Permitted URLs
- Plugin Bundle ID
- Server Address
- User Defined Name
- User Name
- Vendor Config

Applies to:

- iOS/iPadOS
- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### Device Firmware Configuration Interface (DFCI) supports Panasonic devices<!-- 15729353 -->  
For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type).

New Panasonic devices running Windows 10/11 are being enabled for DFCI starting Fall 2022. So, admins can create DFCI profiles to manage the BIOS and then deploy the profiles to these Panasonic devices.

Contact your device vendor or device manufacturer to ensure you get eligible devices.

For more information about DFCI profiles, go to:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](/mem/autopilot/dfci-management)

Applies to:

- Windows 10
- Windows 11

#### Login and background item management support on macOS devices using the settings catalog<!-- 15751007  -->  
On macOS devices, you can create a policy that automatically opens items when users sign in to their macOS devices. For example, you can open apps, documents, and folders.

In Intune, the settings catalog includes new Service Management settings at **Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** > **Login** > **Service Management**. These settings can prevent users from disabling the managed login and background items on their devices.

For more information on the settings catalog, go to:

- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)
- [Common tasks you can complete using the Settings Catalog](../configuration/settings-catalog-common-features.md)

Applies to:

- macOS 13 and newer

### Intune apps

#### Newly available protected apps for Intune<!-- 16118715, 16118848, 16135107, 16027039, 15658466, 15658598  -->  
The following protected apps are now available for Microsoft Intune:

- Varicent by Varicent US OpCo Corporation
- myBLDNG by Bldng.ai
- Enterprise Files for Intune by Stratospherix Ltd
- ArcGIS Indoors for Intune by ESRI
- Meetings by Decisions by Decisions AS
- Idenprotect Go by Apply Mobile Ltd

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Review Cloud PC connectivity health checks and errors in Microsoft Intune admin center<!-- 13811774 -->  
You can now review connectivity health checks and errors in the Microsoft Intune admin center to help you understand if your users are experiencing connectivity issues. There's also a troubleshooting tool to help resolve connectivity issues. To see the checks, select **Devices** > **Windows 365** > **Azure network connections** > *select a connection in the list* > **Overview**.  

### Tenant administration

#### Deliver organizational messages for Windows 11 (public preview)<!-- 15314747  -->  
Use Microsoft Intune to deliver important messages and call-to-actions to employees on their devices.  Organizational messages are preconfigured messages intended to improve employee communication in remote and hybrid-work scenarios. They can be used to help employees adapt to new roles, learn more about their organization, and stay informed of new updates and trainings. You can deliver messages  just above the taskbar, in the notifications area, or in the Get Started app on Windows 11 devices.

During public preview, you can:

* Select from various preconfigured, common messages to assign to Azure AD user groups.
* Add your organization's logo. 
* Include a custom destination URL in the message that redirects device users to a specific place.
* Preview messages in 15 supported languages, in dark and light theme.
* Schedule a delivery window and message frequency.
* Track the status of messages and the number of views and clicks they receive. Views and clicks are aggregated by messages.
* Cancel scheduled or active messages.  
* Configure a new built-in role in Intune called *Organizational Messages Manager*, which allows assigned admins to view and configure messages.  

All configurations need to be done in the Microsoft Intune admin center. The Microsoft Graph API isn't available to use with organizational messages. For more information, see [Overview of organizational messages](../remote-actions/organizational-messages-overview.md).

## Week of November 7, 2022

### App management

#### Ending support for Windows Information Protection<!-- 15991481 -->
Windows Information Protection (WIP) policies without enrollment is being deprecated. You can no longer create new WIP policies without enrollment. Until December of 2022, you can modify existing policies until the deprecation of the *without enrollment* scenario is complete. For related information, go to [Plan for Change: Ending support for Windows Information Protection](../fundamentals/whats-new.md#plan-for-change-ending-support-for-windows-information-protection).

### Device Configuration

#### User configuration support for Windows 11 multi-session VMs is now generally available

You can now:
 - Configure user scope policies using **Settings catalog** and assign to groups of users, including ADMX-ingested policies
 - Configure user certificates and assign to users
 - Configure PowerShell scripts to install in the user context and assign to users

Applies to:
 - **Windows 11**
 - **Virtual machines** created in [Azure Public and Azure Government clouds](/enterprise-mobility-security/solutions/ems-intune-govt-service-description)
## Week of October 31, 2022

### App management

#### Primary MTD service app protection policy setting for Intune<!-- 13222514 -->
Intune now supports both Microsoft Defender for Endpoint and one non-Mobile Threat Defense (MTD) connector to be turned "On" for App Protection Policy evaluation per platform. This feature enables scenarios where a customer may want to migrate between Microsoft Defender for Endpoint and non-Microsoft MTD service without a pause in protection via risk scores in App Protection Policy. A new setting has been introduced under Conditional Launch health checks titled "Primary MTD service" to specify which service should be enforced for the end user. For more information, see [Android app protection policy settings](../apps/app-protection-policy-settings-android.md) and [iOS app protection policy settings](../apps/app-protection-policy-settings-ios.md).

## Week of October 24, 2022 (Service release 2210)

### App management

#### Use filters with app configuration policies for managed devices<!-- 7423842  -->  
You can use filters to refine the assignment scope when deploying app configuration policies for managed devices. You must first [create a filter](../fundamentals/filters.md#create-a-filter) using any of the available properties for iOS and Android. Then, in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) you can assign your managed app configuration policy by selecting **Apps** > **App configuration policies** > **Add** > **Managed devices** and go to the assignment page. After selecting a group, you can refine the applicability of the policy by choosing a filter and deciding to use it in **Include** or **Exclude** mode. For related information about filters, see [Use filters when assigning your apps, policies, and profiles in Microsoft Intune admin center](../fundamentals/filters.md).

### Device configuration

#### Group Policy analytics automatically applies scope tags assigned to admins when they import Group Policy objects<!-- 16017499 -->  
In Group Policy analytics, you can import your on-premises GPOs to see the policy settings that support cloud-based MDM providers, including Microsoft Intune. You can also see any deprecated settings or settings not available.

Now, scope tags assigned to admins are automatically applied when these admins import GPOs into Group Policy analytics.

For example, admins have "Charlotte", "London", or "Boston" scope tags assigned to their role:

- An admin with the "Charlotte" scope tag imports a GPO. 
- The "Charlotte" scope tag is automatically applied to the imported GPO.
- All admins with the "Charlotte" scope tag can see the imported object.
- Admins with only the "London" or only the "Boston" scope tags can't see the imported object from the "Charlotte" admin.

For admins to see the analytics or migrate the imported GPO to an Intune policy, these admins must have one of the same scope tags as the admin that did the import.

For more information on these features, go to:

- [Analyze your on-premises GPOs using Group Policy analytics in Microsoft Intune](../configuration/group-policy-analytics.md)
- [Use role-based access control (RBAC) and scope tags for distributed IT](scope-tags.md)

Applies to:

- Windows 11
- Windows 10

#### New network endpoints for Microsoft Intune<!--15847055 -->

New network endpoints have been added to our documentation to accommodate new Azure Scale Units (ASU) that are added to the Intune service. We recommend updating your firewall rules with the latest list of IP addresses to ensure that all network endpoints for Microsoft Intune are up-to-date.

For the full list, go to  [Network endpoints for Microsoft Intune](intune-endpoints.md).

#### Filter app and group policy assignments using Windows 11 SE operating system SKUs<!-- 10588651  -->  
When you assign an app or policy, you can filter the assignment using different device properties, such as device manufacturer, operating system SKU, and more.

Two new Windows 11 SE operating system SKUs are available. You can use these SKUs in your assignment filters to include or exclude Windows 11 SE devices from applying group-targeted policies and applications. 

For more information on filters and the device properties you can use, go to:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [Device properties, operators, and rule editing when creating filters in Microsoft Intune](filters-device-properties.md)

Applies to:

- Windows 11 SE

#### New settings available in the iOS/iPadOS and macOS settings catalog <!-- 15514929  -->  
The [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the settings catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Networking > Cellular**:

- Enable XLAT464

Applies to:

- iOS/iPadOS

**Privacy > Privacy Preferences Policy Control**:

- System Policy App Bundles

Applies to:

- macOS

**Restrictions**:

- Allow Rapid Security Response Installation
- Allow Rapid Security Response Removal

Applies to:

- iOS/iPadOS
- macOS

For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### New settings for Device Firmware Configuration Interface (DFCI) profiles on Windows devices<!-- 15511597  -->  
You can create a DFCI profile that enables the Windows OS to pass management commands from Intune to UEFI (Unified Extensible Firmware Interface) (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates > Device Firmware Configuration Interface**)

You can use this feature to control BIOS settings. There are new settings you can configure in the DFCI policy:

- Cameras:
  - Front camera
  - Infrared camera
  - Rear camera

- Radios:
  - WWAN
  - NFC

- Ports
  - SD Card

For more information on DFCI profiles, go to:

- [Use Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [DFCI profile settings list](../configuration/device-firmware-configuration-interface-windows-settings.md)

Applies to:

- Windows 11 on supported UEFI
- Windows 10 RS5 (1809) and later on supported UEFI

### Device enrollment

#### iOS/iPadOS Setup Assistant with modern authentication supports Just in Time Registration (public preview)<!-- 15515188 -->  
Intune supports Just in Time (JIT) Registration for iOS/iPadOS enrollment scenarios that use Setup Assistant with modern authentication. JIT Registration reduces the number of authentication prompts shown to users throughout the provisioning experience, giving them a more seamless onboarding experience. It eliminates the need to have the Company Portal app for Azure AD registration and compliance checks, and establishes single sign-on across the device. JIT Registration is available in public preview for devices enrolling through Apple automated device enrollment and running iOS/iPadOS 13.0 or later. For more information, see [Authentication methods for automated device enrollment](../enrollment/automated-device-enrollment-authentication.md). 

### Device management

#### Connect Chrome OS devices in Intune (public preview)<!-- 14273312 -->  
View company or school-owned devices that run on Chrome OS in the Microsoft Intune admin center.  Now in public preview, you can establish a connection between the Google Admin console and Microsoft Intune admin center.  Device information about your Chrome OS endpoints is synced into Intune and viewable in your device inventory list. Basic remote actions, such as restart, wipe, and lost mode are also available in the admin center. For more information about how to set up a connection, see [Configure Chrome Enterprise connector](../enrollment/chrome-enterprise-connector-configure.md).  

#### Manage macOS software updates with Intune<!-- 9801186 -->  
You can now use Intune policies to manage macOS software updates for devices that enrolled using Automated Device Enrollment (ADE).  See [Manage macOS software update policies in Intune](../protect/software-updates-macos.md).

Intune supports the following macOS update types:

- Critical updates
- Firmware updates
- Configuration file updates
- All other updates (OS, built-in apps)

In addition to scheduling when a device updates, you can manage behaviors, like:

- Download and install: Download or install the update, depending on the current state.
- Download only: Download the software update without installing it.
- Install immediately: Download the software update and trigger the restart countdown notification.
- Notify only:  Download the software update and notify the user through the App Store.
- Install later: Download the software update and install it at a later time.
- Not configured: No action taken on the software update.

For information from Apple about managing macOS software updates, see [Manage software updates for Apple devices - Apple Support](https://support.apple.com/guide/deployment/manage-software-updates-depc4c80847a/web) in the Apple's Platform Deployment documentation.
Apple maintains a list of security updates at [Apple security updates - Apple Support](https://support.apple.com/en-us/HT201222).

#### Deprovision Jamf Pro from within the Microsoft Intune admin center<!-- 3485465  -->  
You can now [deprovision your Jamf Pro to Intune integration](../protect/conditional-access-jamf-cloud-connector.md#deprovision-jamf-pro-from-within-the-microsoft-intune-admin-center) from within the Microsoft Intune admin center. This feature can be useful should you no longer have access to the Jamf Pro console, through which you can also deprovision integration.

This capability functions similarly to disconnecting Jamf Pro from within the Jamf Pro console. So, after you remove the integration, your organization's Mac devices are removed from Intune after 90 days.

#### New hardware details available for individual devices running on iOS/iPadOS<!-- 15038076  -->  
Select **Devices** > **All devices** > *select one of your listed devices* and open it's **Hardware** details. The following new details are available in the **Hardware** pane of individual devices:

- **Battery level**: Shows the battery level of the device anywhere between 0 and 100, or defaults to null if the battery level cannot be determined. This feature is available for devices running iOS/iPadOS 5.0 and later.
- **Resident users**: Shows the number of users currently on the shared iPad device, or defaults to null if the number of users cannot be determined. This feature is available for devices running iOS/iPadOS 13.4 and later.

For more information, go to [View device details with Microsoft Intune](../remote-actions/device-inventory.md).

Applies to

- iOS/iPadOS

#### Use the `$null` value in filters<!-- 11030128  -->  
When you assign apps and policies to groups, you can use filters to assign a policy based on rules you create (**Tenant administration** > **Filters** > **Create**). These rules use different device properties, such as category or the enrollment profile.

Now, you can use the `$null` value with the `-Equals` and `-NotEquals` operators.

For example, use the `$null` value in the following scenarios:

- You want to target all devices that don't have a category assigned to the device.
- You want to target devices that don't have an enrollment profile property assigned to the device.

For more information on filters and the rules you can create, go to:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [Device properties, operators, and rule editing when creating filters in Microsoft Intune](filters-device-properties.md)

Applies to:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10/11

### Device security

#### Reusable groups of settings for removable storage in Device Control profiles (preview) <!-- 7351534 -->  
In public preview, you can use [reusable groups of settings](../protect/reusable-settings-groups.md) with [device control profiles](../protect/endpoint-security-asr-policy.md#add-reusable-settings-groups-to-profiles-for-device-control) in your attack surface reduction policies.

The reusable groups for device control profiles include a collection of settings that support managing *read*, *write*, and *execute* access for removable storage. Examples of common scenarios include:

- Prevent write and execute access to all but allow specific approved USBs
- Audit write and execute access to all but block specific unapproved USBs
- Only allow specific user groups to access specific removable storage on a shared PC

Applies to:  
- Windows 10 or later

#### Reusable groups of settings for Microsoft Defender Firewall Rules (preview) <!-- 5653346, 6009541 -->  
In public preview, you can use [reusable groups of settings](../protect/reusable-settings-groups.md) that you can use with [profiles for Microsoft Defender Firewall Rules](../protect/endpoint-security-firewall-policy.md#add-reusable-settings-groups-to-profiles-for-firewall-rules). The reusable groups are collections of remote IP addresses and FQDNs that you define one time and can then use with one or more firewall rule profiles. You don't need to reconfigure the same group of IP addresses in each individual profile that might require them.

Features of the reusable settings groups include:

- Add one or more remote IP addresses.

- Add one or more FQDNs that can auto resolve to the remote IP address, or for one or more simple keywords when auto resolve for the group is off.

- Use each settings group with one or more firewall rule profiles and the different  profiles can support different access configurations for the group.

  For example, you can create two firewall rule profiles that reference the same reusable settings group and assign each profile to a different group of devices. The first profile can block access to all the remote IP addresses in the reusable settings group, while the second profile can be configured to allow access.

- Edits to a settings group that's in use are automatically applied to all Firewall Rules profiles that use that group.  

#### Attack surface reduction rule exclusions on a per-rule basis<!-- 13385644   -->  
You can now [configure per-rule exclusions for Attack surface reduction rules policies](../protect/endpoint-security-asr-policy.md#exclusions-for-attack-surface-reduction-rules). Per-rule exclusions are enabled through a new per-rule setting **ASR Only Per Rule Exclusions**.

When you create or edit attack surface reduction rule policies and change a setting that supports exclusions from the default of *Not configured* to any of the other available options, the new per-setting exclusion option becomes available. Any configurations for that settings instance of *ASR Only Per Rule Exclusions* apply to only that setting.

You can continue to configure global exclusions that apply to all attack surface reduction rules on the device
by using the setting **Attack Surface Reduction Only Exclusions**.

Applies to:

- Windows 10/11

> [!NOTE]  
> ASR polices do not support merge functionality for *ASR Only Per Rule Exclusions* and a policy conflict can result when multiple polices that configure *ASR Only Per Rule Exclusions* for the same device conflict. To avoid conflicts, combine the configurations for *ASR Only Per Rule Exclusions* into a single ASR policy. We are investigating adding policy merge for *ASR Only Per Rule Exclusions* in a future update.

#### Grant apps permission to silently use certificates on Android Enterprise devices<!-- 12441244    -->  
You can now configure silent use of certificates by apps on Android Enterprise devices that enrolled as **Fully Managed, Dedicated, and Corporate-Owned work Profile**.

This capability is available on a new **Apps** page in the certificate profile configuration workflow by setting **Certificate access** to  **Grant silently for specific apps (require user approval for other apps)**.  With this configuration, the apps you then select silently use the certificate. All other apps continue to use the default behavior, which is to require user approval.

This capability is supported for the following certificate profiles for only Android Enterprise Fully Managed, Dedicated, and Corporate-Owned work Profiles:

- [Derived credentials](../protect/derived-credentials.md#use-derived-credentials-for-app-authentication)
- [Imported PKCS](../protect/certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
- [PKCS](../protect/certificates-pfx-configure.md#create-a-pkcs-certificate-profile)
- [SCEP](../protect/certificates-profile-scep.md#create-a-scep-certificate-profile)

#### In-app notifications for Microsoft Intune app<!-- 13110609  -->  
Android Open Source Project(AOSP) device users can now receive compliance notifications in the Microsoft Intune app. This capability is only available on AOSP user-based devices. For more information, see [AOSP compliance notifications](../user-help/check-compliance-aosp.md#compliance-notifications).

### Intune apps

#### Newly available protected apps for Intune<!-- 15287512, 15448552   -->  
The following protected apps are now available for Microsoft Intune:

- MyITOps for Intune by MyITOps, Ltd
- MURAL - Visual Collaboration by Tactivos, Inc

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of October 17, 2022

### App management

#### Enhanced app picker for managed apps on Android devices<!-- 14531483 -->

Android device users can select, view, and remove their default app selections in the Intune Company Portal app. Company Portal securely stores the device user's default choices for managed apps. Users can view and remove their selections in the Company Portal app by going to **Settings** > **Default Apps** > **See defaults**. This feature is an enhancement to the Android custom app picker for managed apps, which is a part of the Android MAM SDK. For more information about how to view default apps, see [View and edit default apps](../user-help/use-managed-apps-on-your-device-android.md#view-and-edit-default-apps). 

## Week of October 10, 2022

### Device management

#### Microsoft Endpoint Manager branding change<!-- 15812021 -->  
As of October 12, 2022, the name Microsoft Endpoint Manager will no longer be used. Going forward, we refer to cloud-based unified endpoint management as Microsoft Intune and on-premises management as Microsoft Configuration Manager. With the launch of advanced management, Microsoft Intune is the name of our growing product family for endpoint management solutions at Microsoft.  For details, see [the official announcement](https://aka.ms/itsintune) on the endpoint management Tech Community blog. Documentation changes are ongoing to remove Microsoft Endpoint Manager.

For related information, see [Intune documentation]( ../../index.yml).

#### Grace period status visible in Windows Company Portal<!-- 14746606 -->  
Windows Company Portal now displays a grace period status to account for devices that don't meet compliance requirements but are still within their given grace period. Users are shown the date by which they need to become compliant and the instructions for how to become compliant. If users don't update their device by the given date, their device status changes to noncompliant. For more information about setting grace periods, see [Configure compliance policies with actions for noncompliance](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) and [Check access from Device details page](../user-help/check-device-access-windows-cpapp.md#check-access-from-device-details-page).

#### Linux device management available in Microsoft Intune<!-- 14616038 -->  
Microsoft Intune now supports Linux device management for devices running Ubuntu Desktop 22.04 or 20.04 LTS. Intune admins don't need to do anything to enable Linux enrollment in the Microsoft Intune admin center.  Linux users can [enroll supported Linux devices](../user-help/enroll-device-linux.md) on their own and use the Microsoft Edge browser to access corporate resources online.

In the admin center, you can:

- Enforce Conditional Access policies in Microsoft Edge.  
- [Create a Linux device compliance policy](../protect/device-compliance-get-started.md#device-compliance-policies) with rules about:  
  - Allowed distributions
  - Custom compliance
  - Device encryption
  - Password policy
- [Apply custom compliance settings](../protect/compliance-use-custom-settings.md) using POSIX-compliant shell scripts for discovery, and JSON files to define the custom settings you want to use.

## Week of October 03, 2022

### Device Security

#### Non-compliance warning message includes a link<!--13694184  -->  
In Remote Help, a link has been added to the non-compliance warning notification **View device compliance information** and it allows a helper to learn more about why the device isn't compliant in Microsoft Intune.

For more information, go to:

- [Microsoft Intune Remote Help](/mem/intune/fundamentals/remote-help)

- [Monitor Device compliance](../protect/compliance-policy-monitor.md)

Applies to:
**Windows 10/11**

## Week of September 26, 2022

### Monitor and troubleshoot

#### Open Help and Support without losing your context in the Microsoft Intune admin center<!-- 12469338 -->  
You can now use the `?` icon in the Microsoft Intune admin center to open a [help and support](../../get-support.md) session without losing your current node of focus in the admin center. The `?` icon is always available in the upper right of the title bar of the admin center. This change adds an additional method for accessing *Help and support*.

When you select `?`, the admin center opens the help and support view in a new and separate side-by-side pane. By opening this separate pane, you're free to navigate the support experience without affecting your original location and focus on the admin center.

## Week of September 19, 2022 (Service release 2209)

### App management

#### New app types for Microsoft Intune<!-- 7210233 -->
As an admin, you can create and assign two new types of Intune apps:
- **iOS/iPadOS web clip** 
- **Windows web link**

These new app types work in a similar way to the existing **web link** application type, however they apply only for their specific platform, whereas web link applications apply across all platforms. With these new app types, you can assign to groups and also use assignment filters to limit the scope of assignment. This functionality is in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apps** > **All Apps** > **Add**.

### Device management

#### Microsoft Intune is ending support for Windows 8.1<!-- 14740233 -->
Microsoft Intune is ending support on October 21, 2022 for devices running Windows 8.1. After that date, technical assistance and automatic updates that help protect your devices running Windows 8.1 will no longer be available. Additionally, because the sideloading scenario for line-of-business apps is only applicable to Windows 8.1 devices, Intune no longer supports Windows 8.1 sideloading. Sideloading is installing, and then running or testing an app that isn't certified by the Microsoft Store. In Windows 10/11, "sideloading" is simply setting a device config policy to include "Trusted app installation". For more information, see [Plan for Change: Ending support for Windows 8.1](../fundamentals/whats-new.md#plan-for-change-ending-support-for-windows-81-).

#### Group member count visible in assignments<!-- 13434676 -->
When assigning policies in the admin center, you can now see the number of users and devices in a group. Having both counts help you pinpoint the right group and understand the impact the assignment has before you apply it.

### Device configuration

#### New lock screen message when adding custom support information to Android Enterprise devices<!-- 13158348 -->
On Android Enterprise devices, you can create a device restrictions configuration profile that shows a custom support message on the devices (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** > **Fully managed, dedicated, and corporate-owned work profile** for platform > **Device restrictions** for profile type > **Custom support information**).

There's a new setting you can configure:
- **Lock screen message**: Add a message that's shown on the device lock screen. 

When you configure the **Lock screen message**, you can also use the following device tokens to show device-specific information:
- `{{AADDeviceId}}`: Azure AD device ID
- `{{AccountId}}`: Intune tenant ID or account ID
- `{{DeviceId}}`: Intune device ID
- `{{DeviceName}}`: Intune device name
- `{{domain}}`: Domain name
- `{{EASID}}`: Exchange Active Sync ID
- `{{IMEI}}`: IMEI of the device
- `{{mail}}`: Email address of the user
- `{{MEID}}`: MEID of the device
- `{{partialUPN}}`: UPN prefix before the `@` symbol
- `{{SerialNumber}}`: Device serial number
- `{{SerialNumberLast4Digits}}`: Last four digits of the device serial number
- `{{UserId}}`: Intune user ID
- `{{UserName}}`: User name
- `{{userPrincipalName}}`: UPN of the user

> [!NOTE]
> Variables aren't validated in the UI and are case sensitive. As a result, you may see profiles saved with incorrect input. For example, if you enter `{{DeviceID}}`, instead of `{{deviceid}}` or `{{DEVICEID}}`, then the literal string is shown instead of the device's unique ID. Be sure to enter the correct information. All lowercase or all uppercase variables are supported, but not a mix.

For more information on this setting, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md#custom-support-information).

Applies to:
- Android 7.0 and newer
- Android Enterprise corporate owned fully managed
- Android Enterprise corporate owned dedicated devices
- Android Enterprise corporate owned work profile

#### Filter on the user scope or device scope in the settings catalog for Windows devices<!-- 13949975 -->
When you create a settings catalog policy, you can use **Add settings** > **Add filter** to filter settings based on the Windows OS edition (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Settings catalog** for profile type).

When you **Add filter**, you can also filter on the settings by user scope or device scope.

For more information on the settings catalog, go to [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md).

Applies to:
- Windows 10
- Windows 11

#### Android Open Source Project (AOSP) platform is generally available<!-- 15027949 -->
Microsoft Intune management of corporate-owned devices that run on the Android Open Source Project (AOSP) platform is now generally available (GA). This feature includes the full suite of capabilities that are available as part of the public preview.

Currently, Microsoft Intune only supports the new Android (AOSP) management option for RealWear devices.
- [Deployment guide: Manage Android devices in Microsoft Intune](deployment-guide-platform-android.md)
- [Deployment guide: Enroll Android devices in Microsoft Intune](deployment-guide-enrollment-android.md)

Applies to:
- Android Open Source Project (AOSP)

#### Device Firmware Configuration Interface (DFCI) now supports Acer devices<!-- 15240661 -->
For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type).

New Acer devices running Windows 10/11 will be enabled for DFCI in later 2022. So, admins can create DFCI profiles to manage the BIOS and then deploy the profiles to these Acer devices.

Contact your device vendor or device manufacturer to ensure you get eligible devices.

For more information about DFCI profiles in Intune, go to [Use Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md).

Applies to:
- Windows 10
- Windows 11

#### New settings available in the iOS/iPadOS and macOS settings catalog<!-- 15349701 -->
The [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. 

There are new settings available in the settings catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Accounts > LDAP**:

- LDAP Account Description
- LDAP Account Host Name
- LDAP Account Password
- LDAP Account Use SSL
- LDAP Account User Name
- LDAP Search Settings

Applies to:
- iOS/iPadOS
- macOS

The following settings are also in settings catalog. Previously, they were only available in Templates:

**Privacy > Privacy Preferences Policy Control**:

- Accessibility
- Address Book
- Apple Events
- Calendar
- Camera
- File Provider Presence
- Listen Event
- Media Library
- Microphone
- Photos
- Post Event
- Reminders
- Screen Capture
- Speech Recognition
- System Policy All Files
- System Policy Desktop Folder
- System Policy Documents Folder
- System Policy Downloads Folder
- System Policy Network Volumes
- System Policy Removable Volumes
- System Policy Sys Admin Files

Applies to:

- macOS

For more information about configuring settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Device enrollment

#### Set up enrollment notifications (public preview)<!-- 9283605 -->
Enrollment notifications inform device users, via email or push notification, when a new device has been enrolled in Microsoft Intune. You can use enrollment notifications for security purposes to notify users and help them report devices enrolled in error, or for communicating to employees during the hiring or onboarding process. Enrollment notifications are available to try now in public preview for Windows, Apple, and Android devices. This feature is only supported with user-driven enrollment methods.

### Device security

#### Assign compliance policies to the All devices group<!-- 2213410 -->
The **All devices** option is now available for [compliance policy](../protect/create-compliance-policy.md) assignments. With this option, you can assign a compliance policy to all enrolled devices in your organization that match the policy's platform, without needing to create an Azure Active Directory group that contains all devices. 
 
When you include the *All devices* group you can then exclude individual groups of devices to further refine the assignment scope.

#### Trend Micro – New mobile threat defense partner<!-- 11017779 -->
You can now use [Trend Micro Mobile Security as a Service](../protect/trend-micro-mobile-threat-defense-connector.md) as an integrated mobile threat defense (MTD) partner with Intune. By configuring the Trend MTD connector in Intune, you can control mobile device access to corporate resources using conditional access that's based on risk assessment.
 
For more information, see:
- [Mobile threat defense integration with Intune](../protect/mobile-threat-defense.md)

<!-- - [Trend Micro Mobile Security documentation](https://docs.trendmicro.com/en-us/enterprise/trend-micro-vision-one/mobile-security/getting-started-with_003.aspx) -->

#### Grace period status visible on Intune Company Portal website<!-- 15025900 -->
The Intune Company Portal website now shows a grace period status to account for devices that don't meet compliance requirements but are still within their given grace period. Users are shown the date by which they need to become compliant and the instructions for how to become compliant. If they don't update their device by the given date, their status changes to noncompliant. For more information about setting grace periods, see [Configure compliance policies with actions for noncompliance](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance).

### Intune apps

#### Newly available protected apps for Intune<!-- 15007580, 15235927 -->
The following protected apps are now available for Microsoft Intune:
- RingCentral for Intune by RingCentral, Inc.
- MangoApps, Work from Anywhere by MangoSpring, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## What's new archive
<!-- Past announcements that are older than six months will be moved to the archive -->

For previous months, see the [What's new archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
