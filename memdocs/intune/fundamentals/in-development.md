---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 08/06/2020
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


<!-- ***********************************************-->
## Device configuration

### Create PKCS certificate profiles for Android Enterprise Fully Managed devices (COBO)<!-- 4839686 -->
You can create PKCS certificate profiles to deploy certificates to Android Enterprise Device owner and Work profile devices (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise > Device owner only**, or **Android Enterprise > Work profile only** for platform > **PKCS** for profile).

Soon you'll be able to create PKCS certificate profiles for Android Enterprise Fully Managed devices. The Intune PFX certificate connector is required. If you don't use SCEP, and only use PKCS, you can remove the NDES connector after you install the new PFX connector. The new PFX connector imports PFX files, and deploys PKCS certificates to all platforms.

For more information on PKCS certificates, see [Configure and use PKCS certificates with Intune](../protect/certficates-pfx-configure.md).

Applies to:
- Android Enterprise fully managed (COBO)

### Support for certificates with a key size of 4096 on iOS and macOS devices<!-- 7659175   -->
Intune will soon support use of a key size of 4096 bits for SCEP certificate profiles. (**Devices** > **Configuration profiles** > **Create profile** > *select a platform* > *Profile* = **SCEP certificate**)

Support for 4096-bit keys will be for the following platforms: 
- iOS 14 and later
- macOS 11 and later    

### New setting for Password complexity for Android 10 and later<!-- 7992114  -->
To support new options for Android 10 and later, we're adding a new setting called **Password complexity** to both *Device compliance* policy and *Device restriction* policy. (**Devices** > **Configuration profiles** > **Create profile** > **Device restrictions** and **Devices** > **Compliance policies** > **Create Policy**)  With this setting you'll be able to manage a measure of password strength that factors in password type, length, and quality. 

The following complexity levels will be supported:
- **None** - No password
- **Low** - The password satisfies one of the following:
  - Pattern
  - PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences
- **Medium** - The password satisfies one of the following:
  - PIN with no repeating (4444) or ordered (1234, 4321, 2468) sequences, length at least 4
  - Alphabetic, length at least 4
  - Alphanumeric, length at least 4
- **High** - The Password satisfies one of the following:
  - PIN with no repeating (4444) or ordered (1234, 4321, 2468) sequences, length at least 8
  - Alphabetic, length at least 6
  - Alphanumeric, length at least 6

Password Complexity doesn’t apply to Samsung Knox devices running Android 10 and later. On these devices, Password Length and/or Password Type settings override Password Complexity.

### COPE preview update: New settings to create requirements for the work profile password for Android Enterprise corporate-owned devices with a work profile<!--7088355 -->
Future settings will give admins the ability to set requirements for the work profile password for Android Enterprise corporate-owned devices with a work profile.  (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work profile** > **Device restrictions** for profile > **Work profile password**):

- Required password type
- Minimum password length
- Number of days until password expires
- Number of passwords required before user can reuse a password
- Number of sign-in failures before wiping device


### New settings using per-app VPN or on-demand VPN on iOS/iPadOS and macOS devices<!-- 7758772 7758837 7758886  -->
- **Prevent users from disabling automatic VPN**: When creating an automatic **Per-app VPN** or **On-demand VPN** connection, you can force users to keep the automatic VPN enabled and running.
- **Associated domains**: When creating an automatic **Per-app VPN** connection, you can specify associated domains in the VPN profile that automatically start the VPN connection. 
- **Excluded domains**: When creating an automatic **Per-app VPN** connection, you can create a list of domains that can bypass the VPN connection when per-app VPN is connected.

You can configure automatic VPN profiles in **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **VPN** for profile > **Automatic VPN**.

For more information on associated domains, see [Associated domains](../configuration/device-features-configure.md#associated-domains).

To see the settings you can configure, see [Set up per-app Virtual Private Network (VPN) for iOS/iPadOS devices](../configuration/vpn-setting-configure-per-app.md#create-a-per-app-vpn-profile).

Applies to:
- iOS/iPadOS 14 and newer
- macOS Big Sur (macOS 11)

### COPE preview update: New settings to configure the personal profile for Android Enterprise corporate-owned devices with a work profile<!-- 7086356  -->
For Android Enterprise corporate-owned devices with a work profile, there are new settings you can configure that only apply to the personal profile (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work profile** > **Device restrictions** for profile > **Personal profile**):

- **Camera**: Use this setting to block access to the camera during personal usage.
- **Screen capture**: Use this setting to block screen captures during personal usage.
- **Allow users to enable app installation from unknown sources in the personal profile**: Use this setting to allow users to install apps from unknown sources in the personal profile. 

To see the current settings you can configure, go to [Android Enterprise device settings to allow or restrict features](../configuration/device-restrictions-android-for-work.md).

### Block App Clips on iOS/iPadOS, and Defer non-OS software updates on macOS devices<!-- 7518422  -->
When you create a Device Restrictions profiles on iOS/iPadOS and macOS devices, there are some new settings:

**iOS/iPadOS 14.0+ Block App Clips**
- Applies to iOS/iPadOS 14.0 and newer.
- Devices must be enrolled with device enrollment or automated device enrollment (supervised devices).
- The **Block App Clips** setting blocks App Clips on managed devices (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile > **General**). When blocked, users can't add any App Clips, and any existing App Clips are removed from the device.  

**macOS 11+ Defer software updates**
- Applies to macOS 11 and newer. On supervised macOS devices, the device must have user approved device enrollment, or enrolled through automated device enrollment.
- The **Defer software updates** setting delays user visibility of non-OS software updates (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device restrictions** for profile > **General**). If you defer these updates, newly released updates aren't visible to users until after the deferral period, which is configured using the **Delay visibility of software updates** settings. Deferring non-operating system software updates doesn't impact scheduled updates.
- The existing **Defer software updates** setting is combined with this new setting. Using the new setting, you can defer OS software updates, and non-OS software updates. You continue to use the **Delay visibility of software updates** setting to set the number of days, which will apply to both settings that defer software updates.
- The behavior of existing policies isn't changed, affected, or deleted. Existing policies will automatically migrate to the new setting with your same configuration.

### Disable MAC address randomization on Wi-Fi networks on iOS/iPadOS devices<!-- 7758689  -->
Starting with iOS/iPadOS 14, by default, devices present a randomized MAC address when connecting to a network instead of the physical MAC address. This behavior is recommended for privacy, as it's harder to track a device by its MAC address. This feature also breaks functionality that relies on a static MAC address, including network access control (NAC). 

You can disable MAC address randomization on a per-network basis in Wi-Fi profiles (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Wi-Fi** for profile > **Basic** or **Enterprise** for Wi-Fi type).

To see the settings you can currently configure, go to [Add Wi-Fi settings for iOS and iPadOS devices](../configuration/wi-fi-settings-ios.md).

Applies to:
- iOS/iPadOS 14 and newer

### Set maximum transmission unit for IKEv2 VPN connections on iOS/iPadOS devices<!-- 7758937  -->
Starting with iOS/iPadOS 14 and newer devices, you can configure a custom maximum transmission unit (MTU) when using IKEv2 VPN connections (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **VPN** for profile -> IKEv2 for connection type).

For more information on the settings you can configure, see [IKEv2 settings](../configuration/vpn-settings-ios.md#ikev2-settings).

Applies to:
- iOS/iPadOS 14 and newer

### Per-account VPN connection for email profiles on iOS/iPadOS devices<!-- 7759116  -->
Starting with iOS/iPadOS 14, email traffic for the native Mail app can be routed through a VPN based on the account the user is using. Now, you can specify a per-app VPN profile to use for this account-based VPN connection.  The per-app VPN connection automatically turns on when users use their organization account in the Mail app.

To see the settings you can currently configure, go to [Add e-mail settings for iOS and iPadOS devices](../configuration/email-settings-ios.md).

Applies to:
- iOS/iPadOS 14 and newer

### Use NetMotion as a VPN connection type for Android Enterprise work profile devices<!-- 7764263 -->
When you create a VPN profile, NetMotion is available as a VPN connection type (**Devices** > **Device configuration** > **Create profile** > **Android Enterprise work profile** for platform > **VPN** for profile > **NetMotion** for connection type).

For more information on VPN profiles in Intune, see [Create VPN profiles to connect to VPN servers](../configuration/vpn-settings-configure.md).

Applies to:
- Android Enterprise work profile

### Changes for Password settings in Device restriction profiles for Android device administrator<!-- 7662279  --> 
We’re introducing a few changes for password settings for *Device restriction* and *compliance* policies for *Android device administrator*. (**Devices** > **Configuration profiles** > **Create profile** > **Device restrictions** and **Devices** > **Compliance policies** > **Create Policy**) These changes help Intune accommodate changes in Android version 10 and later, to ensure settings for passwords continue to apply to devices as expected.
 
Changes include:
- Removal of the lop-level option for **Password**.  
- Settings will be reorganized into sections that are based on which devices they apply to.
- The **Minimum password length** will be disabled for use unless **Password type** is configured to a value where the password length applies.
- Additional updates to labels and example text.

These changes apply to the UI for settings, and won’t affect existing profiles. 

<!-- ***********************************************-->
## Device enrollment

### Ending support for iOS 11<!--7327321 -->
After iOS 14 releases, Intune enrollment and the Company Portal app will support iOS versions 12 and later. Older versions won't be supported but will continue to receive policies.

### Ending support for macOS 10.12<!--7327321 -->
After macOS 11 releases, Intune enrollment and the Company Portal will support macOS versions 10.13 and later. Older versions won't be supported.


<!-- ***********************************************-->
## Device management

### PowerShell scripts support for BYOD devices<!-- 1862833  -->
PowerShell scripts will support Azure AD registered devices in Intune. For more information about PowerShell, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md). This functionality does not support devices running Windows 10 Home edition.

### Log Analytics will include device details log<!--6014987  -->
Intune device detail logs will be available in **Reports** > **Log analytics**. You can correlate device details to build custom queries and Azure workbooks.

### Tenant attach: Device timeline in the admin center<!--7220536, CM7141381 -->
When Configuration Manager synchronizes a device to Microsoft Endpoint Manager through tenant attach, you'll be able to see a timeline of events. This timeline shows past activity on the device that can help you troubleshoot problems. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### Tenant attach: Install an application from the admin center<!-- 7220536, CM6024389 -->
You'll be able to initiate an application install in real time for a tenant attached device from the Microsoft Endpoint Management admin center. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### Tenant attach: CMPivot from the admin center<!--7220536, CM6024392 -->
You'll be able to bring the power of [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to be able to initiate real-time queries from the cloud against an individual ConfigMgr managed device and return the results back to the admin center. This gives all the traditional benefits of CMPivot, which allows IT Admins and other designated personas the ability to quickly assess the state of devices in their environment and take action. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### Tenant attach: Run Scripts from the admin center<!--7220536, CM6234688 -->
You'll be able to bring the power of the Configuration Manager on-premises [Run Scripts](../../configmgr/apps/deploy-use/create-deploy-scripts.md) feature to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to run PowerShell scripts from the cloud against an individual Configuration Manager managed device. This gives all the traditional benefits of PowerShell scripts that have already been defined and approved by the Configuration Manager admin to this new environment. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### Deploy Software Updates to macOS devices <!-- 3194876 -->
You'll be able to deploy Software Updates to groups of macOS devices. This feature includes critical, firmware, configuration file, and other updates. You'll be able to send updates on the next device check-in or select a weekly schedule to deploy updates in or out of time windows that you set. This helps when you want to update devices outside standard work hours or when your help desk is fully staffed. You'll also get a detailed report of all macOS devices with updates deployed. You can drill into the report on a per-device basis to see the statuses of particular updates.

### COPE preview update: Reset work profile password for Android Enterprise corporate-owned devices with a work profile <!--7217228 -->
A future admin action will let admins reset the work profile password on Android Enterprise corporate-owned devices with a work profile.

### Rename a co-managed device that is Azure Active Directory joined<!--7728043 -->
You'll be able to rename a co-managed device that is Azure AD joined. To do so, go to MEM > **Devices** > **All devices** > choose a device > **...** > **Rename device**.

### Support for PowerPrecision and PowerPrecision+ Batteries for Zebra devices<!--3724987 -->
On a device's hardware details page, you'll be able to see the following information about Zebra devices using PowerPrecision and PowerPrecision+ batteries:
- State-of-Health rating as determined by Zebra (PowerPrecision+ batteries only)
- Number of full charge cycles consumed
- Date of last check-in for battery last found in the device
- Serial number of the battery pack last found in the device

<!-- ***********************************************-->
## Intune apps

### Unified delivery of Azure AD Enterprise and Office Online applications in the Windows Company Portal<!-- 1817861  -->
In the 2006 release, we announced [Unified delivery of Azure AD Enterprise and Office Online applications in the Company Portal](../fundamentals/whats-new.md#unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal). This feature will be supported in the Windows Company Portal. On the **Customization** pane of Intune, you will be able to select to **Hide** or **Show** both **Azure AD Enterprise applications** and **Office Online applications** in the Windows Company Portal. Each end-user will see their entire application catalog from the chosen Microsoft service. By default, each additional app source will be set to **Hide**. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you will select **Tenant administration** > **Customization** to find this configuration setting. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Power BI compliance report template V2.0<!-- 636958  -->
Admins will be able to update the Power BI compliance report template version from V1.0 to V2.0. V2.0 will include an improved design, as well as changes to the calculations and data that are being surfaced as part of the template. For related information, see [Connect to the Data Warehouse with Power BI](../developer/reports-proc-get-a-link-powerbi.md).


### New and improved Microsoft Defender Antivirus reporting for Windows 10 and newer<!-- 6018169  -->
We're adding four new reports Microsoft Defender Antivirus on Windows 10, under **Endpoint Security** > **Antivirus**.
- Two operational reports, *Devices with detected malware* and *Agent status*.
- Two organizational reports, *Detected malware* and *Agent status*.

As an example, the operational report *Agent status* will show at a glance the device name, user name, user email and UPN, and if real-time protection and network protection are enabled. We’ll share more details when these reports are available for use.

For more information on Endpoint security in Intune, see [Manage endpoint security in Microsoft Intune](../protect/endpoint-security.md).

### Analyze your on-premises GPOs using Group Policy analytics (preview)<!--7200950 -->
In **Devices** > **Group Policy analytics (preview)**, you can import your group policy objects (GPOs) in the Endpoint Manager admin center. When you import, Intune automatically analyzes the GPO, and shows the policies that have equivalent settings in Intune. It also shows GPOs that are deprecated, or aren't supported anymore.

Applies to:
- Windows 10 and newer

#### New Windows 10 feature update report<!-- 6473121   -->
The **Feature update failures** report will provide failure details for devices that are targeted with a **Windows 10 feature updates** policy and have attempted an update. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you will select **Devices** > **Monitor** > **Feature update failures** to view this report."

#### New Windows 10 feature update report<!-- 6473128  -->
The **Windows feature updates** report will provide an overall view of compliance for devices that are targeted with a **Windows 10 feature updates** policy. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you will select **Reports** > **Windows updates (Preview)** > **Feature update failures** to view the summary for this report. To see reports for specific policies, select the **Reports** tab and open the **Windows Feature Update Report**. 

<!-- ***********************************************-->
<!--
## Role-based access control
-->

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

### Improved certificate deployment for Android Enterprise <!-- 6296499  -->
Devices that run Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profiles will soon be able to use of S/MIME certificates for Outlook without a device user having to allow access. S/MIME certificates are deployed by using PKCS imported certificate profile for Device configuration. (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** > **PKCS imported certificate** from the category for *Fully Managed, Dedicated, and Corporate-Owned Work Profile*).

### Tri-state options for settings are coming to Endpoint Security Firewall policy<!-- 6586159   -->
We’re adding a third state of configuration for settings in Endpoint security Firewall policies, where the platform (Windows or macOS) can support the additional option (**Endpoint security** > **Firewall**).

For example, where a setting currently offers **Not configured** and **Yes**, if supported by the platform, we’ll be adding the option **No**.

### New Security baseline for Office<!-- 3150261  -->
We're adding a new security baseline (**Endpoint security** > **Security baselines**) to manage settings for *Microsoft Office O365*. Settings in the baseline will include configurations for Office apps like *Add-on Management*,  *MIME handling*, and more.

### Improved status details in security baseline reports<!-- 7221051    -->
We’re improving the status details you’ll see when viewing the results of your deployed security baselines. (**Endpoint security** > **Security baselines** >  *select a security baseline type,  like* **Windows 10 Security Baselines** > **Profiles** > *select an instance of that profile to view status* > *select a profile report, like* **Device status**)

The improvements will revise the common labels and definitions we use for status to better fit the intent of the status. For example:
- **Matches baseline**  will update to **Matches default settings**, which better describes the intent to identify when a devices configuration matches the default (unmodified) baseline configuration.
- **Misconfigured** will be broken into more specific details, like **Error**, **Conflict**, and **Pending**. The new states will bring consistency to other areas of the console.

### Expanded RBAC permissions for the Endpoint Security role<!--7312374  idstaged -->
The **Endpoint Security Manager** role for Intune is receiving addition role-based access control (RBAC) permissions for remote tasks.This role grants access to the Microsoft Endpoint Manager admin center and can be used by individuals who manage security and compliance features, including security baselines, device compliance, conditional access, and Microsoft Defender Advanced Threat Protection.

To view the permission for an Intune RBAC role, go to (**Tenant admin** > **Intune roles** > *select a role* > **Permissions**).

Expanded permissions for remote tasks include the following:

- Reboot now
- Remote lock
- Rotate BitLockerKeys (Preview)
- Rotate FileVault key
- Sync devices
- Microsoft Defender
- Initiate Configuration Manger action

### Updates for Security Baselines<!-- 7102146, 7103916  -->
We’ll soon release updates to the following security baselines (**Endpoint security** > **Security baselines**):
- **MDM Security baseline** (Windows 10 Security)
- **Microsoft Defender ATP baseline**

Updated baseline versions bring support for recent settings to help you maintain the best-practice configurations recommended by the respective product teams.

### Use Endpoint security configuration details to identify the source of policy conflicts for devices<!-- 7567503  idstaged  -->
To aid in conflict resolution, you’ll soon be able to drill-in through a security baseline profile to view the *Endpoint security configuration* for a selected device. From there, you can select settings that show a *Conflict* or *Error* and continue to drill-in further to view a list of details that includes the profiles and policies that are part of the conflict. If you then select a policy that is a source of a conflict, Intune opens that policies Overview pane from where you can review or modify the policies configuration. (**Devices** > *select a device* > **Endpoint security configuration** > *select a profile or baseline* > *Select a setting from the list of settings applied to the device*).

The following policy types can be identified as a source of conflict when you drill in through a security baseline:
- Device configuration policy
- Endpoint security policies

### New details in the Endpoint security configuration for a device<!-- 7745029   -->
We’re adding new details for devices that are available to view as part of a devices Endpoint security configuration. (**Endpoint security** > **Security baselines** > *selected baseline* > **Profiles** > *selected profile* > **Device status** > **Endpoint security configuration**). The new details:

- **UPN** (User Principle Name): The UPN identifies which endpoint security profile is assigned to a given user on the device. This is useful to help differentiate between multiple users on a device and multiple entries of a profile or baseline that’s assigned to the device. 
- **Worst status**: This detail identifies the least favorable status condition for the device. When this status is **Success**, the device has no policy conflicts or errors.

### Android 11 deprecates deployment of trusted root certificates to device administrator enrolled devices<!--7662775  -->
With Android 11, trusted root certificates can no longer be deployed to devices that are enrolled as *Android device administrator*. This change doesn’t affect Samsung Knox devices because of Intune’s integration with the Knox platform. For non-Samsung devices, users must manually install the trusted root certificate on the device. 

With the trusted root certificate manually installed on a device, you can then use SCEP to provision certificates to the device. In this scenario you must still create and deploy a *trusted certificate* policy to the device and link that policy to the *SCEP certificate* profile.

- If the trusted root certificate is on the device, then the SCEP certificate profile will install successfully. 
- If the trusted certificate cannot be found, the SCEP certificate profile will fail.

<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).