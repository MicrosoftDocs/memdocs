---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 10/12/2020
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

### Update to device icons in Company Portal and Intune apps on Android<!-- 6057023  -->
We're updating the device icons in the Company Portal and Intune apps on Android devices to create a more modern look and feel and to align with the Microsoft Fluent Design System. For related information, see [Update to icons in Company Portal app for iOS/iPadOS and macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

### iOS Company Portal will support Apple's Automated Device Enrollment without user affinity<!-- 7282707  --> 
iOS Company Portal will be supported on devices enrolled using Apple's Automated Device Enrollment without requiring an assigned user. An end user can sign in to the iOS Company Portal to establish themselves as the primary user on an iOS/iPadOS device enrolled without device affinity. For more information about Automated Device Enrollment, see [Automatically enroll iOS/iPadOS devices with Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md).

### Rolling minimum Company Portal (CP) version for Android devices<!-- 5151625  -->
You'll have the ability to set a rolling minimum Company Portal (CP) version for Android devices. This Intune setting will ensure that end users are within a certain range of CP releases (in days). Admins will no longer have to re-visit the conditional launch settings when a new CP update is released. You'll be able to find this setting in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **App protection policies** > **Create policy**. The **Min Company Portal version** setting will be available in the **App conditions** section of the **Conditional launch** value setting step. For more information about Intune app protection policies, see [How to create and assign app protection policies](../apps/app-protection-policies.md).

### Android app protection policies (MAM) on COPE devices<!-- 7088497  -->
Newly added Mobile Application Management (MAM) support will enable Android app protection policies on Android Enterprise corporate-owned​ devices with a work profile (COPE). 

### Mac LOB apps will be supported as managed apps on macOS 11 and higher<!-- 7750527  -->
Intune will support the **Install as managed** app property that can be configured for Mac line-of-business (LOB) apps deployed to macOS 11 and higher. When this setting is on, the Mac LOB app will be installed as a managed app on supported devices (macOS 11 and higher). Managed line-of-business apps will be able to be removed using the **uninstall** assignment type on supported devices (macOS 11 and higher). In addition, removing the MDM profile removes all managed apps from the device. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **macOS** > **Add**. For more information about adding apps, see [Add apps to Microsoft Intune](../apps/apps-add.md).

### Enable Outlook S/MIME emails to be always signed or encrypted<!-- 8375748  -->
You'll be able to enable Outlook S/MIME emails to be always signed or encrypted when you create an Outlook email profile under app configuration for iOS/iPadOS and Android Enterprise devices.  The setting is available when you choose **Managed devices** when creating an Outlook app configuration policy. You'll be able to find this setting in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **App configuration policies** > **Add** > **Managed devices**. For related information, see [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md). 

<!-- ***********************************************-->
## Device configuration

### Use NetMotion as a VPN connection type for Android Enterprise devices<!-- 7764263 -->
When you create a VPN profile, NetMotion is available as a VPN connection type (**Devices** > **Device configuration** > **Create profile** > **Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile** or **Android Enterprise Work Profile** for platform > **VPN** for profile > **NetMotion** for connection type).

For more information on VPN profiles in Intune, see [Create VPN profiles to connect to VPN servers](../configuration/vpn-settings-configure.md).

Applies to:
- Android Enterprise Work Profile
- Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile

### Changes for Password settings in Device restriction profiles for Android device administrator<!-- 7662279   --> 

We’re introducing a few changes for password settings for *Device restriction* and *compliance* policies for *Android device administrator*. (**Devices** > **Configuration profiles** > **Create profile** > **Device restrictions** and **Devices** > **Compliance policies** > **Create Policy**) 

These changes help Intune accommodate changes in Android version 10 and later, to ensure settings for passwords continue to apply to devices as expected. Changes include:

- Settings will be reorganized into sections that are based on which devices they apply to.
- Additional updates to labels and example text.

These changes apply to the UI for settings, and won’t affect existing profiles.

Applies to:
- Android device administrator

### Required password type default setting is changing on Android Enterprise devices<!-- 8092655  -->
On Android Enterprise devices, you can create a device password profile that sets the **Required password type** (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Device restrictions** > **Device password**).

The **Required password type** setting default is changing from **Numeric** to **Device default**.

Existing profiles aren't impacted. New profiles will automatically use **Device default**. 

Most devices don't require a password when **Device default** is selected. If you want to require your users to set up a passcode on their devices, configure the **Required password type** setting to something more secure than **Device default**.

To see the settings you can restrict, go to [Android Enterprise device settings to allow or restrict features](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android Enterprise

### New lockout password settings on macOS devices<!-- 7780272  -->
New settings are available when you create a macOS password profile (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device restrictions** for profile > **Password**):

- **Maximum allowed sign-in attempts**: The maximum number of times users can try to consecutively sign in before the device locks them out, from 2-11. Set this value to a higher number. Setting this value to `2` or `3` isn't recommended, as mistakes are common. Applies to all enrollment types.
- **Lockout duration**: Choose how long the lockout lasts, in minutes. During a device lockout, the sign-in screen is inactive, and users can't sign in. When the lockout durations ends, user can sign in again. To use this setting, configure the **Maximum allowed sign-in attempts** setting. Applies to macOS 10.10 and newer, and all enrollment types.

For the current password settings, see [macOS password device restrictions](../configuration/device-restrictions-macos.md#password).

Applies to:
- macOS

### New user experience and new Enable direct download setting on macOS devices using associated domains<!-- 7739958  -->
When you create an Associated Domain configuration profile on macOS devices, the user experience is updated (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device features** for profile > **Associated domains**). You still enter your App ID and Domains. 

On macOS 11+ supervised devices enrolled with user approved device enrollment or automated device enrollment, you can use the **Enable direct download** setting. Enabling direct downloads allows domain data to downloaded directly, instead of downloading through a content delivery network (CDN).

For more information, see [Associated domains on macOS devices](../configuration/macos-device-features-settings.md#associated-domains).

Applies to:
- macOS 11+ (supervised)

### Use the Connect Automatically setting on Android Enterprise basic Wi-Fi profiles<!-- 6329130  -->
On Android Enterprise devices, you can create basic Wi-Fi profiles that include common Wi-Fi settings, such as the connection name. You can configure the **Connect automatically** setting that automatically connects to your Wi-Fi network when devices are in range.

To see the current settings you can configure, go to [Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices](../configuration/wi-fi-settings-android-enterprise.md).

Applies to:
- Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile

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

### PowerShell scripts support for BYOD devices<!-- 1862833  -->
PowerShell scripts will support Azure AD registered devices in Intune. For more information about PowerShell, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md). This functionality doesn't support devices running Windows 10 Home edition.

### Log Analytics will include device details log<!--6014987  -->
Intune device detail logs will be available in **Reports** > **Log analytics**. You can correlate device details to build custom queries and Azure workbooks.

### Tenant attach: Run Scripts from the admin center<!--7220536, CM6234688 -->
You'll be able to bring the power of the Configuration Manager on-premises [Run Scripts](../../configmgr/apps/deploy-use/create-deploy-scripts.md) feature to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to run PowerShell scripts from the cloud against an individual Configuration Manager managed device. This gives all the traditional benefits of PowerShell scripts that have already been defined and approved by the Configuration Manager admin to this new environment. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### Deploy Software Updates to macOS devices <!-- 3194876 -->
You'll be able to deploy Software Updates to groups of macOS devices. This feature includes critical, firmware, configuration file, and other updates. You'll be able to send updates on the next device check-in or select a weekly schedule to deploy updates in or out of time windows that you set. This helps when you want to update devices outside standard work hours or when your help desk is fully staffed. You'll also get a detailed report of all macOS devices with updates deployed. You can drill into the report on a per-device basis to see the statuses of particular updates.

### Subnet ID and IP addresses on Properties page for corporate-owned Windows devices<!--5265589 -->
Subnet ID and IP addresses will be displayed on the **Properties** page for corporate-owned Windows devices. To see them, go to [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices** > choose a corporate-owned Windows device > **Properties**.


<!-- ***********************************************-->
## Intune apps

### Unified delivery of Azure AD Enterprise and Office Online applications in the Windows Company Portal<!-- 1817861  -->
In the 2006 release, we announced [Unified delivery of Azure AD Enterprise and Office Online applications in the Company Portal](../fundamentals/whats-new.md). This feature will be supported in the Windows Company Portal. On the **Customization** pane of Intune, you'll be able to select to **Hide** or **Show** both **Azure AD Enterprise applications** and **Office Online applications** in the Windows Company Portal. Each end-user will see their entire application catalog from the chosen Microsoft service. By default, each additional app source will be set to **Hide**. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you'll select **Tenant administration** > **Customization** to find this configuration setting. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).
 
 #### Improvements to iOS Company Portal privacy message customization<!-- 7006929 -->
You will have greater ability to customize the privacy messaging in the iOS Company Portal. In addition to the previous support for being able to customize what your organization *can't see*, you will now also be able to customize what your organization's *can see* in the privacy message displayed to end users in the iOS Company Portal. When this feature is release, devices will need to be running at least Company Portal version 4.11 to see the customized messaging about what can be seen. This feature will be available in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Customization**. For related information, see the Company Portal [Privacy](../apps/company-portal-app.md#privacy) message. 

#### Improved notification experience in the iOS/iPadOS Company Portal app<!-- 7219429  -->
The Company Portal app will store, as well as display, push notifications sent to your users' iOS/iPadOS devices from the Microsoft Endpoint Manager console. Users who have opted in to receive Company Portal push notifications will be able to view and manage the customized stored messages that you send to their devices in the **Notifications** tab of the Company Portal. For related information, see [Device ownership notifications](../apps/company-portal-app.md#device-ownership-notification).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Noncompliant policies report to troubleshoot devices in error or noncompliant<!-- 6471368  -->
There's a new operational report to help troubleshoot errors and conflicts for compliance policies targeting devices. The "Noncompliant policies" report will show the list of compliance policies and the number of devices in an error or noncompliant state.

Administrators can use this report to:

- Drill down in a policy to see the list of devices and users in a failed state.
- Drill down to see the list of settings and setting information causing a failure.
- Filter, sort, and search across all records in the report.
- Identify when issues are occurring, and streamline troubleshooting.

For more information on monitoring and reporting, see [Monitor device compliance policies](../protect/compliance-policy-monitor.md) and [Intune reports](../fundamentals/reports.md).

### Manage allowed or blocked hardware devices with endpoint security Attack surface reduction policy<!-- 7339038   -->
We’re adding two new settings to the *Device control* profile for the endpoint security Attack surface reduction policy. (**Endpoint security** > **Attack surface reduction** > **Create Policy** > **Platform** select *Windows 10 and later* > **Device control**).

The new settings:

- Allow matching hardware devices
- Block matching hardware devices

Both new settings will have values of *Yes*, *No*, and *Not configured*. If set to Yes, you’ll be able to create a list of hardware devices that will be allowed or blocked for installation. 

### Account protection policy changes in Endpoint security<!--  7492116   --> 
We’re reworking the endpoint security Account protection policy to use the new APIs for Windows Hello for Business. The new APIs will result in a more consistent experience. The new API is *./Device/Vendor/MSFT/PassportForWork*, which includes more options that can help reduce conflicts.   This API replaces the use of  *./User/Vendor/MSFT/PassportForWork*.  (**Endpoint security** > **Account protection**)
 
After the change, only new policies you then create will use the new API. Your existing policies won’t be affected by this change and will continue to use the older API.

### Policy merge support for USB device ID’s in Device control profiles for endpoint security Attack surface reduction policy<!-- 7339038   -->
We’re expanding support for *policy merge* of Windows Defender Antivirus exclusions to support USB device ID’s. This support will be added to the *Device control* profile for the endpoint security Attack surface reduction policy. (**Endpoint security** > **Attack surface reduction** > **Create Policy** > *for Platform select Windows 10 and later* > **Device control**).

With policy merge, the device ID's that are listed as part of different Device control profiles will merge into a single list for each device or user. That list is based on the individual policies that apply to a specific user or device. This merge will help to prevent conflicts between profiles and policies, and existing policies that were in conflict will no longer be in conflict for the device ID lists. 

### Improvements to endpoint security Firewall rules<!-- 7732448   -->
We're making several changes to improve the experience of configuring firewall rules in the *Microsoft Defender Firewall rules* profile for endpoint security Firewall policy.  (**Endpoint security** > **Firewall** > **Create Policy** > platform - *Windows 10 or later* > **Microsoft Defender Firewall rules**)  

Improvements include:

- Improved layout in the UI, including section headers to organize the view.
- Increasing the character limit for the description field 
- Validation of IP address entries.
- Sorting of IP address lists.
- Option to *select all* when clearing entries from an IP address list.

### Use Microsoft Defender for Endpoint in compliance policies for iOS<!-- 7895451  -->
As a public preview, you’ll soon be able to use Intune device compliance policy to onboard iOS devices to Microsoft Defender for Advanced Threat Protection. (**Devices** > **Compliance policies** > **Create Policy** > *for Platform select iOS/iPad OS*)
 
After you onboard your enrolled devices, your compliance polices for iOS will be able to use the *threat level* signals from Microsoft Defender. These are the same signals that you can use today for Android and Windows 10 devices. The Defender for iOS app is moving from public preview to generally availability by the end of the year.

### New co-management eligibility organizational report<!-- 7854306  -->
The **Co-management eligibility** report provides an eligibility evaluation for devices that can be co-managed. Co-management enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune. You'll be able to view a summary for this report in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Reports** > **Co-management eligibility**. For related report information, see [Intune reports](../fundamentals/reports.md).

### New co-management device workloads organizational report<!-- 7854306  -->
The **Co-management device workloads** report provides a report of devices that are currently co-managed. Co-management enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune. You'll be able to view a summary for this report in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Reports** > **Co-management device workloads**. For related report information, see [Intune reports](../fundamentals/reports.md).

### New Intune operational report to help troubleshoot configuration profile issues<!-- 6471222  -->
A new operational report will be available in public preview to help troubleshoot errors and conflicts for configuration profiles that have been targeted to devices. The **Assignment failures** report will show a list of configuration profiles for the tenant and the number of devices in a state of error or conflict. Using this information, you can drill down to a profile to see a list of devices and users in a failure state related to the profile. Additionally, you can drill down even further to view a list of settings and setting details related to the cause of the failure. You have the ability to filter, sort, and search across all of the records throughout the report. This report will be available in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Monitor** > **Assignment failures (preview)**. For more information about reports in Intune, see [Intune reports](../fundamentals/reports.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## Scripting

### Collect custom device or user properties using shell scripts on managed Macs<!-- 8099433  -->
You'll be able to create a custom attribute profile which will enable you to collect custom properties from a managed macOS device using shell scripts. This feature will be available in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **macOS** > **Custom attributes**.  For related information, see [Use shell scripts on macOS devices in Intune](../apps/macos-shell-scripts.md).

<!-- ***********************************************-->
## Security

### App protection policy support for Symantec Endpoint Security and Check Point Sandblast<!--  4452423, 4731168 -->

In October of 2019, Intune app protection policy added the capability to use data from some of our Microsoft Threat Defense partners (MTD partners). We are adding support for the following partners, to use an app protection policy to block, or selectively wipe the user's corporate data based on the health of a device:

- **Check Point Sandblast** on Android, iOS and iPadOS
- **Symantec Endpoint Security** on Android, iOS and iPadOS

For information about using app protection policy with MTD partners, see [Create Mobile Threat Defense app protection policy with Intune](../protect/mtd-app-protection-policy.md).

### Microsoft Defender ATP creates Endpoint Manager Security task with vulnerability details<!-- 5568193  -->
Threat and Vulnerability Management (TVM) in Microsoft Defender ATP discovers misconfigured security settings on devices. Administrators use this information to update vulnerable devices.

Soon, Microsoft Defender ATP can raise an Endpoint Manager Security task (**Endpoint Manager** > **Endpoint Security** > **Security tasks**) with the vulnerability details, and show the affected devices. IT administrators can accept the security task, and deploy the required configuration. 

For more information on security tasks, see [Use Intune to remediate vulnerabilities identified by Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md).

### Endpoint security Firewall policies for tenant attached devices <!--  7323417     -->
As a public preview, you’ll soon be able to use Endpoint security in Intune to manage Firewall settings on your tenant attached devices. (**Endpoint security** > **Firewall** > **Create Policy** > **Windows 10 and Windows Server (configMgr)**.  Use of endpoint security policies from Intune with tenant attached devices requires you to first configure Configuration Manager tenant attach. For more information, see [Tenant attach](../protect/tenant-attach-intune.md) in the Intune documentation. 

### Tri-state options for settings are coming to Endpoint Security Antivirus Security Experience policy<!-- 8082161  -->
We’re adding a third state of configuration for settings in Endpoint security Antivirus Security Experience policies, where the platform (Windows or macOS) can support the additional option (**Endpoint security** > **Antivirus Security Experience**).

For example, where a setting currently offers **Not configured** and **Yes**, if supported by the platform, we’ll be adding the option **No**.

### Updated version for the Edge security baseline<!-- 8230830   -->
We'll soon release a new version of the security baseline for *Microsoft Edge*. The updated baseline will align to Microsoft Edge version 85.  (**Endpoint security** > **Security baselines** > **Microsoft Edge baseline**).

<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
