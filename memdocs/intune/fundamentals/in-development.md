---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 03/02/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals

# optional metadata

#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. In addition to the information in this article:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description will move from this article to [What's new](whats-new.md).  
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](whats-new.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Tenant administration
## Notices
-->

<!-- ***********************************************-->
 
## App management

### Changes to app backup and restore behavior on iOS/iPadOS and macOS devices<!-- 16261392 -->  
As an app setting, you can select to **Prevent iCloud app backup** for iOS/iPadOS and macOS devices. You will have the option to *not* back up managed App Store apps and line-of-business (LOB) apps on iOS/iPadOS, as well as managed App Store apps on macOS devices (macOS LOB apps won’t support this feature), for both user and device licensed VPP/non-VPP apps. This will include both new and existing App Store/LOB apps sent with and without VPP that are being added to Intune and targeted to users and devices.

Preventing the backup of the specified managed apps will ensure that these apps can be properly deployed via Intune when the device is enrolled and restored from backup. If the admin configures the new setting for new or existing apps in their tenant, managed apps can and will be re-installed for devices, but Intune will no longer allow them to be backed up.
 
The new setting will appear in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by modifying the properties of an app. For an existing app, you can select **Apps** > **iOS/iPadOS** or **macOS** > *select the app* > **Properties** > Assignment **Edit**. If no group assignment has been set, click **Add group** to add a group. Modify either the setting under **VPN**, **Uninstall on device removal**, or **Install as removable**. Then, select **Prevent iCloud app backup**. The **Prevent iCloud app backup** setting is used to prevent backup of app data for the application. Set to **No** to allow the app to be backed up by iCloud.

For more information, see [Changes to applications’ backup and restore behavior on iOS/iPadOS and macOS devices](https://techcommunity.microsoft.com/t5/intune-customer-success/changes-to-applications-backup-and-restore-behavior-on-ios/ba-p/3692064).

### Managed apps permission is no longer required to manage VPP apps<!-- 17205644  -->  
You'll soon be able to view and manage VPP apps with only the **Mobile apps** permission assigned. Previously, the **Managed apps** permission was required to view and manage VPP apps. More information on permissions in Intune is available at [Custom role permissions](../fundamentals/create-custom-role.md#custom-role-permissions).

### Install required apps during pre-provisioning<!-- 12716381   -->  
A new toggle will be available in the Enrollment Status Page (ESP) profile that allows you to select whether you want to attempt to install required applications during pre-provisioning (white glove) technician phase. We understand that installing as many applications as possible during pre-provisioning is desired to reduce the end user set up time. To help you achieve this, we have implemented an option to attempt the installation of all the required apps assigned to a device during technician phase. In case of app install failure, ESP will continue except for the apps specified in ESP profile. To enable this function, you will need to edit your Enrollment Status Page profile by selecting **Yes** on the new setting entitled **Only fail selected apps in technician phase**. This setting will only appear if you have blocking apps selected. For information about ESP, go to [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).

### Company Portal automatically installed on Android Enterprise dedicated devices<!-- 6423852  -->  
Intune Company Portal will now be automatically installed on all Android Enterprise dedicated devices to ensure the appropriate handling of app protection policies. Users will not be able to see or launch the Company Portal, and there are no requirements for users to interact with it. Admins will notice that the Company Portal is automatically installed on their Android Enterprise dedicated devices, without the ability to uninstall.

### Uninstall Win32 apps in the Company Portal<!-- 5145748 -->  
*The time frame for the release of this update is still being determined.*

Users will be able to uninstall Win32 apps in the Company Portal. If a Win32 app can be uninstalled by the user, the user will be able to select **Uninstall** for the Win32 app in the Company Portal. For more information about Win32 apps, go to [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

### Global quiet time app policy settings<!-- 15424417 -->  
The global quiet time settings will allow you to create policies to schedule quiet time for your end users, which will automatically mute Microsoft Outlook email and Teams notifications on iOS/iPadOS and Android platforms. These policies can be used to limit end user notifications received after work hours. When this feature is available, you will be able to find it in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Quiet Time** > **Policies**.

## Device configuration

### New settings and setting options available in the macOS Settings Catalog <!-- 16813395  -->  
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

### Support for multi-SIM iOS/iPadOS device inventory<!--16360290-->

You'll soon be able to view the service subscription fields on devices that have multiple SIM cards installed under the per-device Hardware section. The inventory fields that are capable of reporting multiple values to Intune are:

- **ICCID**
- **IMEI**
- **MEID**
- **Phone number**

These fields will default to using labels returned by the device, such as:  *Primary*, *Secondary*, *CTSubscriptionSlotOne*, and *CTSubscriptionSlotTwo*. These returned labels may be displayed in the language of the local device that is reporting its inventory to Intune.

Applies to:  
- **iOS/iPadOS**

<!-- *********************************************** -->

## Device enrollment

#### Intune's AAD frontline worker iPad experience<!-- 6367427  -->  
Intune will support a frontline worker (FLW) experience for iPhones and iPads. The foundation for this experience is based on support for both the Azure Active Directory (AAD) shared device mode and the Microsoft Enterprise SSO plug-in (Microsoft Azure AD SSO extension). We also will release ZTP (Zero Touch Provisioning) which allows user enrollment without any user action.

### Install Intune policies during Setup Assistant with awaiting final configuration command (public preview)<!-- 13156553  -->  
Intune will support a new setting called **Await final configuration** in specific iOS/iPadOS automated device enrollment profiles. This setting enables a locked experience in Setup Assistant to prevent device users from accessing restricted content or changing settings until the majority of Intune device configuration policies are installed. Just before the home screen loads, Setup Assistant will pause and let Intune finish installing critical device configuration policies. Device users will be locked into the experience on the **Awaiting final configuration** screen, and won't be able to access the home screen until the device is released with the [release device from await configuration](https://developer.apple.com/documentation/devicemanagement/release_device_from_await_configuration) command. The amount of time the device is on that screen until it is released to the home screen will vary depending on the number of policies and apps applied to the device.

This setting is applied once during the out-of-box automated device enrollment experience.  The device user won't experience it again unless they re-enroll their device. You'll be able to utilize the locked experience on devices targeted with new and existing enrollment profiles. Supported devices include:  

* iOS/iPadOS 13+ devices enrolling with Setup Assistant with modern authentication
* iOS/iPadOS 13+ devices enrolling without user affinity
* iOS/iPadOS 13+ devices enrolling with Azure AD shared mode

You will be able to enable or disable this feature in new and existing enrollment profiles with the new setting.

### New setting gives Intune admins control over device-to-category mapping<!-- 15029839  -->  
Control visibility of the device category prompt in Intune Company Portal. Instead of making device users select the category, like they currently do, you'll be able to hide the prompt and leave the device-to-category mapping up to Intune admins. The new setting will be available in the admin center under **Tenant Administration** > **Customization** > **Device Categories**.

<!-- *********************************************** -->

## Device management

### Add Google accounts to Android Enterprise personally owned devices with a work profile<!-- 9113561  -->  
On Android Enterprise personally owned devices with a work profile, you can configure settings that restrict device features and settings. Currently, there is an **Add and remove accounts** setting. This setting prevents accounts from being added in the work profile, including preventing Google accounts.

This setting is changing, and you will be able to add Google accounts. The **Add and remove accounts** setting options will be:

- **Block all accounts types**: Prevents users from manually adding or removing accounts in the work profile. For example, when you deploy the Gmail app into the work profile, you can prevent users from adding or removing accounts in this work profile.
- **Allow all accounts types**: Allows all accounts, including Google accounts. These Google accounts are blocked from installing apps from the **Managed Google Play Store**. This option requires Google Play app version 80970100 or higher.
- **Allow all accounts types, except Google accounts** (default): Intune doesn't change or update this setting. By default, the OS might allow adding accounts in the work profile.

For more information on the settings you can configure, go to [Android Enterprise device settings list to allow or restrict features on personally owned devices using Intune](../configuration/device-restrictions-android-enterprise-personal.md).

Applies to:

- Android Enterprise personally owned devices with a work profile

### Improvements to Devices area in admin center (public preview) <!-- 12775837  -->  
The **Devices** area in the admin center will be updated to provide a more consistent UI, with more capable controls and an improved navigation structure so you can find the information you need faster. You will be able to opt in to the public preview to try out the new experience. Changes will include:  

* A new scenario-focused navigation structure that brings monitoring in line with management workflows.
* New in-line monitoring pages with easy access to key metrics and reports.
* Reduction in journey, helping you get to your destination faster.
* New location for platform pivots that help to create a more consistent navigation model.
* A consistent way across list views to search, sort, and filter data.

The following device pages will be updated:  

* Overview
* All devices
* Compliance
* Configuration
* Windows 10 updates
* Apple updates
* Enrollment

### View status for pending and failed organizational messages<!-- 17017707 -->  
We're adding two more states to organizational message reporting details to make it easier to track pending and failed messages in the admin center.

- Pending: The message has not been scheduled yet and is currently in progress.
- Failed: The message failed to schedule due to a service error.  

### View ServiceNow Incidents in the Intune Troubleshooting workspace<!-- 12508062  -->  
You'll soon be able to view a list of ServiceNow incidents associated with the user you've selected in the Intune Troubleshooting workspace. This new feature will be available under **Troubleshooting + Support** > select a user > **ServiceNow Incidents**. The list of incidents shown have a direct link back to the source incident and show key information from the incident. All incidents listed will link the "Caller" identified in the incident with the user selected for Troubleshooting.

For more information go to [Use the troubleshooting portal to help users at your company](help-desk-operators.md).

### On-demand proactive remediation for a Windows device<!-- 14783338  -->  
A new device action that is in public preview allows you to run a proactive remediation on-demand to a single Windows device. The **Run** remediation device action will allow you to resolve issues without having to wait for a proactive remediation to run on its assigned schedule. You will also be able to view the status of proactive remediations under **Remediations** in the **Monitor** section of a device.

### Endpoint security firewall rules support for ICMP type<!-- 5653356 -->  
We’re adding a new setting named **IcmpTypesAndCodes** to the endpoint security firewall rules template for Windows 10. To configure this in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Endpoint security** > **Firewall** > **Create Policy** > Platform: *Windows 10, Windows 11, and Windows Server*  > Profile: *Microsoft Defender Firewall Rules*).

With this new setting, you’ll be able to configure inbound and outbound rules for [Internet Control Message Protocol](/windows/security/threat-protection/windows-firewall/create-an-inbound-icmp-rule) (ICMP) as part of a firewall rule.

Applies to:  
- Windows 10, Windows 11, and Windows Server

<!-- ***********************************************-->

## Device security

### Microsoft Intune Endpoint Privilege Management (public preview)<!-- 15654169 -->  
As a public preview, we’ll be introducing Microsoft Intune Endpoint Privilege Management. With Endpoint Privilege Management, admins can set policies that allow standard users to perform tasks normally reserved for an administrator. Endpoint Privilege Management can be configured in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) at **Endpoint security** > **Endpoint Privilege Management**.

With the public preview you’ll be able to configure policies for *automatic* and *user-confirmed* workflows that elevate the run-time permissions for apps or processes you select. You then assign these policies to users or devices that have end users running without Administrator privileges. Once policy is received, Endpoint Privilege Management will broker the elevation on behalf of the user, allowing them to elevate approved applications without needing full administrator privileges. The preview also includes built-in insights and reporting for Endpoint Privilege Management.

Endpoint Privilege Management is part of the [Intune Suite](../fundamentals/intune-add-ons.md) offering, and free to try while it remains in public preview.

### Support for tamper protection in policies for Security settings management for Microsoft Defender for Endpoint <!-- 13204113 -->  
You’ll soon be able to manage Tamper protection for Microsoft Defender for Endpoint on unenrolled devices as part of the [MDE Security configuration](../protect/mde-security-integration.md#which-solution-should-i-use) scenario.

When this support is available, your tamper protection configurations from *Windows Security Experience* profiles for *Antivirus* policies can apply to all devices instead of only to those that are enrolled with Intune.

Applies to:  
- Windows 10
- Windows 11

<!-- ***********************************************-->

## Tenant administration

### Add CMPivot queries to Favorites folder<!-- 16702226  -->  
You will be able to add your frequently used queries to a **Favorites** folder in CMPivot. CMPivot allows you to quickly assess the state of a device managed by Configuration Manager via Tenant Attach and take action. The functionality is similar to one already present in the Configuration Manager console. This addition will help you keep all your most used queries in one place. You can also add tags to your queries to help search and find queries. The queries saved in the Configuration Manager console will not automatically be added to your **Favorites** folder. You will need to create new queries and add them to this folder. For more information about CMPivot, see [Tenant attach: CMPivot usage overview](../../configmgr/tenant-attach/cmpivot-overview-attached.md).

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
