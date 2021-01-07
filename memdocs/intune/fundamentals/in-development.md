---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dou/geby
ms.date: 01/08/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1

# optional metadata

#audience:

ms.reviewer: cacampbell
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
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## App management

### Configure whether a required iOS app is removable<!-- 8391462  -->
You'll be able to configure whether a required iOS app is installed as a removable app by end users. The new setting will apply to iOS store, LOB and built-in apps. You'll be able to find this setting in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** > **Add**. When setting the app assignments, you'll be able to select **Install as removable**. The default value is **yes**, which means the app is removable. Existing required installs on iOS 14 will be updated to the default (removable) setting value when this setting is implemented. For more information about iOS apps, see [Microsoft Intune app management](..\apps\app-management.md).

### Scope tag support for customization policies<!--6182440  -->
You'll be able to assign scope tags to Customization policies. To do so, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration**> **Customization** where you'll see **Scope tags** configuration options.

### Android Enterprise system app support in work profiles<!-- 5291507  -->
You'll be able to deploy Android Enterprise system apps for Android Enterprise Work Profile devices. System apps are apps that do not appear in the Managed Google Play Store and come pre-installed on the device. Once a system app is deployed, you'll be unable to uninstall, hide, or otherwise remove the system app. Note that this feature is planned to be released on or near the 2101 release timeframe. For related information about system apps, see [Add Android Enterprise system apps to Microsoft Intune](../apps/apps-ae-system.md).

### New app categories to target app protection policies more easily<!-- 4802581  -->
We've improved the UX of Microsoft Endpoint Manager by creating categories of apps that you can use to more easily and quickly target app protection policies. These categories are **All public apps**, **Microsoft apps**, and **Core Microsoft apps**. After you have created the targeted app protection policy, you can select **View a list of the apps that will be targeted** to view a list of the apps that will be affected by this policy. As new apps are supported, we'll dynamically update these categories to include those apps as appropriate, and your policies will be automatically apply to all apps in your selected category. If needed, you can continue to target policies for individual apps as well. For more information, see [How to create and assign app protection policies](../apps/app-protection-policies.md) and [Create and deploy Windows Information Protection (WIP) policy with Intune](../apps/windows-information-protection-policy-create.md).

### Line-of-business apps supported on Shared iPad devices<!-- 8834566 idready -->
You'll be able to deploy line-of-business (LOB) apps to Shared iPad devices. The line-of-business app must be assigned as **required** to a device group containing Shared iPad devices from the Microsoft Endpoint Manager admin center. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > **Add**. For related information, see [Add an iOS/iPadOS line-of-business app to Microsoft Intune](../apps/lob-apps-ios.md).

<!-- ***********************************************-->
## Device configuration

### Use NetMotion Mobility as a VPN connection type for Android Enterprise devices<!-- 7764263 -->
When you create a VPN profile, NetMotion Mobility is available as a VPN connection type (**Devices** > **Device configuration** > **Create profile** > **Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile** or **Android Enterprise Work Profile** for platform > **VPN** for profile > **NetMotion** for connection type).

For more information on VPN profiles in Intune, see [Create VPN profiles to connect to VPN servers](../configuration/vpn-settings-configure.md).

Applies to:
- Android Enterprise Work Profile
- Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile

### Use the settings catalog to configure Microsoft Edge browser on macOS devices - public preview <!-- 4552197  -->
Currently on macOS devices, you configure the Microsoft Edge browser using a .plist preference file (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Preference file** for profile).

There's an updated UI to configure the Microsoft Edge browser: **Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog (preview)** for profile. Select the settings you want, and then configure them. In your profile, you can also add more settings, or remove existing settings.

To see a list of the settings you can configure, go to [Microsoft Edge - Policies](/DeployEdge/microsoft-edge-policies). Be sure macOS is listed as a supported version. If some settings aren't available in the settings catalog, then it's recommended to continue using the preference file only. 

For more information on .plist files, see [Add a property list file to macOS devices using Intune](../configuration/preference-file-settings-macos.md)

To see the policies you have configured, open Microsoft Edge, and go to `edge://policy`.

Applies to:
- Microsoft Edge browser on macOS

### Settings catalog and Templates when creating device configuration profiles for macOS and Windows 10 devices<!-- 8673623 8254609  -->

There are UI updates when creating device configuration profiles for macOS and Windows 10 devices (**Devices** > **Configuration profiles** > **Create profile** > **macOS** or **Windows 10 and later** for platform).

The profile shows **Settings catalog - preview** and **Templates**:

- **Settings catalog - preview**: Use this option to start from scratch and select settings you want from the library of available settings. For macOS, the Settings catalog contains settings to configure the Microsoft Edge browser. Settings catalog for Windows 10 includes many existing settings, and some new settings, all in one place.
- **Templates**: Use this option to configure all the existing profiles, such as device restrictions, device features, VPN, Wi-Fi, and more.

This is only a UI change, and doesn't impact existing profiles.

Applies to:
- macOS device configuration
- Windows 10 device configuration

### Home screen layout updates on supervised iOS/iPadOS devices<!-- 8710594 7978976  -->

On iOS/iPadOS devices, you can configure the Home Screen layout (**Devices** > **Device Configuration** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **Home screen layout**). In Intune, the Home Screen Layout feature is updated. You can:

- <!-- 8710594 --> You'll see an updated design for the home screen layout feature. This feature allows admins to see in real time how the apps you add look on pages, the dock, and within folders. You can also see the app icons for the apps you add. You can't have multiple separate pages within a folder from the control itself. But, you can add 9 or more apps to a folder and then those apps will go on the next page. 

  Existing policies are not impacted, and don't need to be changed. The setting values are transferred to the new UI without any negative effects. The setting behavior on devices is the same. 

- <!-- 7978976 -->Add URLs as web apps to pages, or to the dock. Be sure you add a specific URL only once. Existing policies are not impacted, and don't need to be changed. This new URL setting is blank for new and existing policies until it's configured.

Applies to:
- iOS/iPadOS supervised devices

### Limit Apple's personalized advertising on iOS/iPadOS devices<!-- 8518601  -->
On iOS/iPadOS devices, you can configure Apple's personalized advertising. When enabled, personalized ads are limited in the App Store, Apple News, and Stocks apps (**Devices** > **Device Configuration** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile > **General** > **Limit Apple personalized advertising**).

This setting only impacts personalized ads. Configuring this setting sets Settings > Privacy > Apple Advertising to off. It doesn't impact non-personalized ads in the App Store, Apple News, and Stocks apps. For more information on Apple's advertising policy, see [Apple Advertising & Privacy](https://support.apple.com/HT205223) (opens Apple's web site).

To see the current settings you can configure in Intune, go to [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md).

Applies to:
- iOS/iPadOS 14.0 and newer, devices enrolled with device enrollment or automated device enrollment
 
<!-- ***********************************************-->
## Device enrollment

### Ending support for iOS 11<!--7327321 -->
After iOS 14 releases, Intune enrollment and the Company Portal app will support iOS versions 12 and later. Older versions won't be supported but will continue to receive policies.

### Ending support for macOS 10.12<!--7327326 -->
After macOS 11 releases, Intune enrollment and the Company Portal will support macOS versions 10.13 and later. Older versions won't be supported.

### Hide more Apple Automated Device Enrollment Setup Assistant Screens<!--7786092 -->
You'll be able to set Automated Device Enrollment (ADE) profiles to hide these Setup Assistant Screens for iOS/iPadOS 14.0+ and macOS 11+ devices:
- Restore Completed, for iOS/iPadOS 14.0+.
- Software Update Completed, for iOS/iPadOS 14.0+.
- Accessibility, for macOS 11+ (the mac device must be connected to an Ethernet).

<!-- ***********************************************-->
## Device management

### Log Analytics will include device details log<!--6014987  -->
Intune device detail logs will be available in **Reports** > **Log analytics**. You can correlate device details to build custom queries and Azure workbooks.


### Subnet ID and IP addresses on Properties page for corporate-owned Windows devices<!--5265589 -->
Subnet ID and IP addresses will be displayed on the **Properties** page for corporate-owned Windows devices. To see them, go to [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices** > choose a corporate-owned Windows device > **Properties**.

### Windows 10 Enterprise multi-session support (public preview)<!--8666391 -->
This support will give users a familiar Windows 10 experience while you get the cost advantages of multi-session and existing per-user M365 licensing. This upcoming support will let you:

- Host multiple concurrent user sessions using the  new Remote Desktop Session Host exclusive to Windows Virtual Desktop on Azure.
- Manage multi-session remote desktops with device-based configurations like a shared, user-less Windows 10 Enterprise client.
- Automatically enroll Hybrid Azure AD joined virtual machines in Intune and target them with OS scope policies and apps.

<!-- ***********************************************-->
## Intune apps

 
### Improved notification experience in the iOS/iPadOS Company Portal app<!-- 7219429  -->
The Company Portal app will store, as well as display, push notifications sent to your users' iOS/iPadOS devices from the Microsoft Endpoint Manager console. Users who have opted in to receive Company Portal push notifications will be able to view and manage the customized stored messages that you send to their devices in the **Notifications** tab of the Company Portal. For related information, see [Device ownership notifications](../apps/company-portal-app.md#device-ownership-notification).

### Win32 app download progress bar<!-- 5145837  -->
End users will see a progress bar in the Windows Company Portal while a Win32 app is being downloaded. This feature will help customer better understand the app installation progress.

### Update to Android Company Portal app icon<!-- 7114401  -->
We'll be updating the Android Company Portal app icon to create a more modern look and feel. For more information about the Company Portal, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

### End users can restart an app install from the Company Portal<!-- 652935  -->
Using the Company Portal, end users will be able to restart an app installation if the progress seems to have stalled or is frozen. This functionality is allowed if the app installation progress has not changed in two hours.

### Application icon update for iOS, macOS, and web Company Portal<!-- 7113985 -->
We'll be updating the app icon used by the Company Portal for iOS, macOS, and web. This new icon is currently used by the Company Portal for Windows. End users will see the new icon in their device's application launcher and home screen, in Apple's App Store, and experiences within the Company Portal apps.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Account protection policy changes in Endpoint security<!--  7492116   --> 
We’re reworking the endpoint security Account protection policy to use the new APIs for Windows Hello for Business. The new APIs will result in a more consistent experience. The new API is *./Device/Vendor/MSFT/PassportForWork*, which includes more options that can help reduce conflicts.   This API replaces the use of  *./User/Vendor/MSFT/PassportForWork*.  (**Endpoint security** > **Account protection**)
 
After the change, only new policies you then create will use the new API. Your existing policies won’t be affected by this change and will continue to use the older API.

### New co-management eligibility organizational report<!-- 7854306  -->
The **Co-management eligibility** report provides an eligibility evaluation for devices that can be co-managed. Co-management enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune. You'll be able to view a summary for this report in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Reports** > **Co-management eligibility**. For related report information, see [Intune reports](../fundamentals/reports.md).

### New co-management device workloads organizational report<!-- 7854306  -->
The **Co-management device workloads** report provides a report of devices that are currently co-managed. Co-management enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune. You'll be able to view a summary for this report in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Reports** > **Co-management device workloads**. For related report information, see [Intune reports](../fundamentals/reports.md).

### Summary view for Windows Defender Antivirus reports<!-- 8846877  -->
We’re adding a **Summary** tab to the Windows Defender Antivirus reports. (**Endpoint security** > **Reports** > **Microsoft defender antivirus** ).

The new Summary view:
- Displays aggregate details for the Antivirus reports. 
- Includes a *Refresh* option that updates the counts of devices in each antivirus state. 
- Reflects the same data as found in the [Agent Status organizational](../fundamentals/reports.md#antivirus-agent-status-report-organizational) report. 


<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## Scripting

### Update when exporting Intune reports using the Graph API<!-- 8764428  -->
When you use the Graph API to export Intune reports without selecting any columns for the devices report, you'll receive the default column set. To reduce confusion, we'll be removing columns from the default column set starting January 2021. The columns being removed are `PhoneNumberE164Format`, `_ComputedComplianceState`, `_OS`, and `OSDescription`. These columns will still be available for selection if you need them, but only explicitly, and not by default. If you have built automation around the default columns of the device export, and that automation uses any of these columns, you need to refactor your processes to explicitly select these and any other relevant columns. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

### Additional Data Warehouse beta properties<!-- 8612282 -->
Additional properties will be available using the Intune Data Warehouse beta API. The following properties will be exposed via the [devices](../developer/reports-ref-devices.md) entity in the beta API:

- `SubnetAddressV4Wifi` - The subnet address for IPV4 Wi-Fi connection.
- `IpAddressV4Wifi` - The IP address for IPV4 Wi-Fi connection.

For related information, see [Microsoft Intune Data Warehouse API](../developer/reports-nav-intune-data-warehouse.md).

### Export localized Intune report data using Graph APIs<!-- 8612346 -->
You'll be able to specify that the report data that you export from the Microsoft Endpoint Manager reporting export [API](../fundamentals/reports-export-graph-apis.md) can contain localized columns only, or localized and non-localized columns. The localized and non-localized columns option will be selected by default for most reports, which will prevent breaking changes. For more information about reports, see [Intune reports](../fundamentals/reports.md) and [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

<!-- ***********************************************-->
## Security

### New Endpoint Security Firewall reports <!-- 5653366   -->
We're adding two new reports that are dedicated to Firewall policies in Endpoint Security:

- The first, under Endpoint security, will show the list of Windows 10 devices with Firewall turned off. This report will show for each device the device name, device ID, user information, and the Firewall status. (**Endpoint security** > **Firewall** > ***Windows 10 MDM devices with firewall off***).
- The second, under Reports, will be an organizational report which lists Windows 10 devices with their firewall status. This report will display status information about device firewalls that include if the firewall is enabled, disabled, limited, or temporarily disabled.  (**Reports** > **Firewall** > ***Windows 10 MDM Firewall status***).

### Locale support in email notifications for non-compliance<!--7604191    -->
Soon, you'll be able to use a single email template in a compliance policy that supports multiple locales for sending email notifications for non-compliance.

(**Devices** > **Compliance policies** > **Notifications** > **Create notification** > **Notification message templates**). 

Supporting multiple languages won't require separate templates and policies for each locale. Non-compliant end-users will receive the appropriate localized email notification based on their O365 preferred language. If the preferred language isn't specified by the end-user you can use the *Is Default* checkbox to send the appropriate localized message.  

### Migrate device security polices from Basic Mobility and Security to Intune<!--6306140 -->
The policy migration tool will let you permanently move Mobile Device Management (MDM) device security policies deployed by Basic Mobility and Security (formerly MDM for Office 365 or Office MDM) to standard Intune MDM configuration profiles and compliance policies. Using this tool will disable all future policy creation and edits in Basic Mobility and Security device security policies.

To use the tool, you must:
- Already have purchased (but not yet assigned) Intune licenses for all the users of devices managed by Basic Mobility.
- Contact support to check eligibility if you have purchased an Intune for Education subscription. 

### Increased certificate validity period for SCEP and PKCS profiles<!-- 8629805   -->
You'll soon be able to use a **Certificate validity period** of up to **24** months in certificate profiles for Simple Certificate Enrollment Protocol (SCEP) and 
Public Key Cryptography Standards (PKCS). This is an increase from the current support  for a period of up to 12 months.  This support is coming to Windows and Android. Certificate validity periods are ignored by iOS/iPad OS and macOS.  (**Devices** > **Configuration profiles** > **Create profile** > *SCEP certificate* or *PKCS certificate*).

### Improved flow for conditional access on Surface Duo devices<!-- 7552043  -->
We’re streamlining the conditional access flow on Surface Duo devices. These changes happen automatically and won't require any configuration updates by administrators. (**Endpoint security** > **Conditional access**)

- We’re improving the redirection to the Company Portal app when access to a resource is blocked by conditional access. Instead of being sent to the Google Play store listing of the Company Portal app, users will be sent directly to the Company Portal app that’s preinstalled on their Duo device.
- For devices that are enrolled as personally-owned work profile, when a user tries to sign in to a personal version of an app using their work credentials, they will be sent to the work version of Company Portal where guidance messaging is shown. Currently, the user is sent to the Google Play store listing of the personal version of the Company Portal app, where they must reenable the personal Company Portal to see the guidance messaging.

### New setting for Attack surface reduction rules to block malware from gaining persistence through WMI<!-- 8902661  -->
We're adding a new setting to the Attack surface reduction rule profile, part of Attack surface reduction policy, to help prevent malware from abusing WMI to gain persistence on a device. (**Endpoint security** > **Attack surface reduction** > **Create Policy** > **Attack surface reduction rule**)

This new setting can help protect against fileless malware threats that abuse the WMI repository and event model to stay hidden. For more information see [Block persistence through MI event subscription](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-persistence-through-wmi-event-subscription) in the Windows security documentation.

### New Application Guard settings in Attack surface reduction policy<!-- 8274336 -->
We'll be adding two new settings to the App and browser isolation profile of Intune’s [Endpoint security Attack surface reduction policy](../protect/endpoint-security-asr-policy.md):

- **Application Guard allow camera and microphone access** – Manage access by Application Guard apps to a devices camera and microphone.
- **Application Guard allow use of Root Certificate Authorities from the user's device** – When you specify one or more root certificate thumbprints, the matching certificates are transferred to the Microsoft Defender Application Guard container.

### Update to MDATP and MDM baseline settings<!-- 8391335, 8377369 -->
As part of endpoint security in Intune, we'll be updating the Microsoft Defender Advanced Threat Protection and Mobile Device Management (MDM) protection baselines settings to the latest version. For related information, see [Microsoft Defender Advanced Threat Protection baseline settings for Intune](../protect/security-baseline-settings-defender-atp.md?pivots=atp-sept-2020).

### App protection policy support on Android and iOS/iPadOS for additional Mobile Threat Defense partners<!-- 8846351 idready-->
In October of 2019, Intune app protection policy added the capability to use data from our Microsoft Threat Defense partners. We'll be expanding this support to the following partner for using an app protection policy to block or selectively wipe a user’s corporate data based on the health of the device:

- **McAfee MVision Mobile** on Android, iOS and iPadOS

### Intune support for Microsoft Defender Application Guard to include isolated Windows environments<!-- 8274282  -->
In the future, when you configure **Turn on Application Guard**  in an Intune [App and browser isolation profile](../protect/endpoint-security-asr-profile-settings.md#app-and-browser-isolation) in Endpoint security Attack surface reduction policy, you'll be able to choose from the following options when you enable Application Guard:

- **Microsoft Edge** - *Currently available*
- **Isolated Windows environments** - *Available in a future update*
- **Microsoft Edge** ***and*** **isolated Windows environments** - *Available in a future update*

The setting is currently named *Turn on Application Guard for Edge (Options)*.

The new options for this setting expand Application Guard support beyond just URL’s for Edge. You can also enable Application Guard to help protect devices by opening potential threats in a hardware isolated Windows VM environment (container). For example, with support for isolated Windows environments, Application Guard can open untrusted Office documents in an isolated Windows VM. 

<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
