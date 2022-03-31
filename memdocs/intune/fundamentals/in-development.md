---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 03/31/2022
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
  - M365-identity-device-management
  - highpri
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
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

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

### Enterprise feedback policies for Web Company Portal<!-- 9846764 -->
Feedback settings will be provided to address M365 enterprise feedback policies for the currently logged in user via the Microsoft 365 Apps Admin Center. The settings are used to determine whether feedback can be enabled or must be disabled for a user in the Web Company Portal.

### iOS Company Portal minimum required version<!-- 13016075 -->
With an upcoming release of the MS Authenticator app, users will be required to update to v5.2204 of the iOS Company Portal. If you have enabled the **[Block installing apps using App Store](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised)** device restriction setting, you will likely need to push an update to the related devices that use this setting. Otherwise, no action is needed. If you have a helpdesk, you may want to make them aware of the prompt to update the Company Portal app. In most cases, users have app updates set to automatic, so they receive the updated Company Portal app without taking any action. Users that have an earlier app version will be prompted to update to the latest Company Portal app.

### Password complexity for Android devices<!-- 9321870 -->
The **Require device lock** setting in Intune will be extended to include values (**Low Complexity**, **Medium Complexity**, and **High Complexity**). If the device lock doesn't meet the minimum password requirement, you'll be able to **warn**, **wipe data**, or **block** the end user from accessing a managed account in a managed app. 

This feature targets devices that operate on Android 11+. For devices that operate on Android 10 and earlier, setting a complexity value of **Low**, **Medium**, or **High** will default to the expected behavior for **Low Complexity**. For related information, see [Android app protection policy settings in Microsoft Intune](..\apps\app-protection-policy-settings-android.md).

### Improvements to Win32 App Log collection<!-- 9978316 -->
Win32 App Log collection via Intune Management Extension has moved to the Windows 10 device diagnostic platform, reducing time to collect logs from 1-2 hours to 20 minutes.  We've also increased the size from 60mb to 250mb.  Along with performance improvements, the app logs will also be available under the **Device diagnostics monitor** action for each device, as well as the managed app monitor. For information about how to collect diagnostics, see [Collect diagnostics from a Windows device](..\remote-actions\collect-diagnostics.md) and [Troubleshooting Win32 app installations with Intune](/troubleshoot/mem/intune/troubleshoot-win32-app-install).

### Uninstall DMG-type applications on managed macOS devices (Public preview)<!-- 13155022 -->
You will be able to use the Uninstall assignment type to remove DMG-type applications on managed macOS devices from Microsoft Endpoint Manager. You can find macOS DMG apps in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **macOS** > **macOS app (.DMG)**. For related information, [Add a macOS DMG app to Microsoft Intune](../apps/lob-apps-macos-dmg.md).

### Update to the App configuration policies list<!-- 13903969 -->
In Intune, the **Assigned** column in the **App configuration policies** list will be removed. To view the assigned groups for an app configuration policy, navigate to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apps** > **App configuration policies** > *select a policy* > **Overview**.

<!-- ***********************************************-->

## Device enrollment

### Improvements for enrollment profiles for Apple’s Automated Device Enrollment (Public preview)<!-- 10111795 -->
As a public preview, we’re adding new Setup Assistant screens you can configure when [creating enrollment profiles](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile) for Apple’s Automated Device Enrollment (ADE). The following new screens will be available on the *Setup Assistant* tab for both iOS/iPadOS and macOS as follows:  
 
- iOS/iPadOS 13 and later - **Get Started (preview)**
  - Default – Show
  - Admin can configure to hide the Get Started pane (Setup Assistant screen) during ADE enrollment.
 
- macOS 12 and later - **Auto Unlock with Apple Watch (preview)**
  - Default – Show
  - Admin can configure to hide the Unlock Your Mac with your Apple Watch pane (Setup Assistant screen) during ADE enrollment.

<!-- ***********************************************-->

## Device management

### Device actions available to Android (AOSP) users in Microsoft Intune app<!-- 12645718 -->
AOSP device users will be able to delete, wipe, and rename their enrolled devices in the Microsoft Intune app. This feature will be available on devices enrolled in Intune as user-associated (Android) AOSP devices. 

### Updating the device diagnostics folder structure<!-- 8504019 -->
We’re updating how Intune exports [Windows Device Diagnostic data](../remote-actions/collect-diagnostics.md). Today, the zip file is flat structure of numbered folders that doesn’t identify their contents. Once updated, the logs collected will be named to match the data that was collected, and if multiple files are collected a folder will be created.

To take advantage of this diagnostic logging update, devices must install one of the following updates:
- Windows 11 - KB5011563
- Windows 10 - KB5011543

These updates are expected to be made available through Windows Updates on April 12, 2022.

### Support for Audio Alert on Andriod corporate owned work profiles and fully managed (COBO and COPE) devices<!-- 13499471 -->
You'll be able to use the **Play lost device sound** device action to trigger an alarm sound on the device to assist in locating the lost or stolen Android Enterprise corporate owned work profiles and fully managed devices.

For more information, see [Locate lost or stolen devices](../remote-actions/device-locate.md).

<!-- ***********************************************-->

## Device configuration

### New wired networks device configuration profile for Windows devices<!-- 1746923 -->
There will be a new **Wired Networks** device configuration profile (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Wired networks** for profile type).

Use this profile to configure common wired network settings, including authentication, EAP type, server trust, and more.

Applies to:
- Windows 11
- Windows 10

### Create a Settings Catalog policy using your imported GPOs with Group Policy analytics (public preview)<!-- 6379751 -->
Using Group Policy analytics, you can import your on-premises GPO, and see the settings that are supported in Microsoft Intune. It also shows any deprecated settings, or settings not available to MDM providers.

When the analysis runs, you'll see the settings that are ready for migration. There will be a **Migrate** option (public preview) that creates a Settings Catalog profile using these settings. Then, you can assign the profile to your groups.

For more information on what you can do now, see [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Endpoint Manager](../configuration/group-policy-analytics.md).

Applies to:
- Windows 11
- Windows 10

### Use the Settings Catalog to create a Universal Print policy on Windows 11 devices<!-- 5513123 -->
Many organizations are moving their printer infrastructure to the cloud. [Universal Print](/universal-print/fundamentals/universal-print-whatis) is a cloud-based printing solution for Microsoft 365 customers. It uses built-in cloud printers, built-in legacy printers, and runs entirely in Microsoft Azure. When Universal Print is deployed with Universal Print-compatible printers, it doesn't require any on-premises infrastructure. 

In the Endpoint Manager admin center, you'll be able to use the Settings Catalog to create a printer policy (**Device configuration** > **Create profile** > **Windows 10 and later** for platform > **Settings catalog** for profile type > **Printer provisioning**). When you deploy the policy, users select the printer from a list of registered Universal Print printers, and can also select a default printer.

Currently, you must use the [Universal Print printer provisioning tool](/universal-print/fundamentals/universal-print-intune-tool), which requires more manual steps, and has some limitations.

Applies to:
- Windows 11

### New macOS settings in Setting Catalog<!-- 13654614 -->
The Settings Catalog has new macOS settings you can configure (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform >**Settings catalog (preview)** for profile type):

**Accounts > Mobile Accounts**:

- Ask For Secure Token Auth Bypass
- Create At Login
- Expiry Delete Disused Seconds
- Warn On Create
- Warn On Create Allow Never

**App Management > Autonomous Single App Mode**:

- Bundle Identifier
- Team Identifier

**App Management > NS Extension Management**: 

- Allowed Extensions
- Denied Extension Points
- Denied Extensions

**App Store**: 

- Disable Software Update Notifications
- Restrict Store Software Update Only
- restrict-store-disable-app-adoption

**Authentication > Directory Service**: 

- AD Allow Multi Domain Auth
- AD Allow Multi Domain Auth Flag
- AD Create Mobile Account At Login
- AD Create Mobile Account At Login Flag
- AD Default User Shell
- AD Default User Shell Flag
- AD Domain Admin Group List
- AD Domain Admin Group List Flag
- AD Force Home Local 
- AD Force Home Local Flag
- AD Map GGID Attribute
- AD Map GGID Attribute Flag
- AD Map GID Attribute
- AD Map GID Attribute Flag
- AD Map UID Attribute
- AD Map UID Attribute Flag
- AD Mount Style
- AD Namespace
- AD Namespace Flag
- AD Organizational Unit
- AD Packet Encrypt
- AD Packet Encrypt Flag
- AD Packet Sign
- AD Packet Sign Flag
- AD Preferred DC Server
- AD Preferred DC Server Flag
- AD Restrict DDNS
- AD Restrict DDNS Flag
- AD Trust Change Pass Interval Days
- AD Trust Change Pass Interval Days Flag
- AD Use Windows UNC Path
- AD Use Windows UNC Path Flag
- AD Warn User Before Creating MA Flag
- Client ID
- Description
- Password
- User Name

**Authentication > Identification**: 

- Prompt
- Prompt Message

**Login > Login Window Login Items**:

- Disable Login Items Suppression

**Media Management Disc Burning**:

- Burn Support

**Parental Controls > Parental Controls Application Restrictions**:

- Family Controls Enabled

**Parental Controls > Parental Controls Content Filter**:

- Allowlist Enabled
- Filter Allowlist
- Filter Blocklist
- Site Allowlist
- Address
- Page Title
- Use Content Filter

**Parental Controls > Parental Controls Dictionary**:

- Parental Control

**Parental Controls > Parental Controls Game Center**:

- GK Feature Account Modification Allowed

**System Configuration > File Provider**:

- Allow Managed File Providers To Request Attribution

**System Configuration > Screensaver**:

- Ask For Password
- Ask For Password Delay
- Login Window Idle Time
- Login Window Module Path

**User Experience > Finder**:

- Prohibit Burn
- Prohibit Connect To
- Prohibit Eject
- Prohibit Go To Folder
- Show External Hard Drives On Desktop
- Show Hard Drives On Desktop
- Show Mounted Servers On Desktop
- Show Removable Media On Desktop
- Warn On Empty Trash

**User Experience > Managed Menu Extras**:

- AirPort
- Battery
- Bluetooth
- Clock
- CPU
- Delay Seconds
- Displays
- Eject
- Fax
- HomeSync
- iChat
- Ink
- IrDA
- Max Wait Seconds
- PCCard
- PPP
- PPPoE
- Remote Desktop
- Script Menu
- Spaces
- Sync
- Text Input
- TimeMachine
- Universal Access
- User
- Volume
- VPN
- WWAN

**User Experience > Notifications**:

- Alert Type
- Badges Enabled
- Critical Alert Enabled
- Notifications Enabled
- Show In Lock Screen
- Show In Notification Center
- Sounds Enabled

**User Experience > Time Machine**:

- Auto Backup
- Backup All Volumes
- Backup Size MB
- Backup Skip System
- Base Paths
- Mobile Backups
- Skip Paths

**Xsan**:

- San Auth Method

**Xsan > Xsan Preferences**:

- Deny DLC
- Deny Mount
- Only Mount
- Prefer DLC
- Use DLC

The following settings are also in Settings Catalog. Previously, they were only available in Templates:

**App Management > Associated Domains**:

- Enable Direct Downloads

**Networking > Content Caching**:

- Allow Cache Delete
- Allow Personal Caching
- Allow Shared Caching
- Auto Activation
- Auto Enable Tethered Caching
- Cache Limit
- Data Path
- Deny Tethered Caching
- Display Alerts
- Keep Awake
- Listen Ranges
- Listen Ranges Only
- Listen With Peers And Parents
- Local Subnets Only
- Log Client Identity
- Parent Selection Policy
- Parents
- Peer Filter Ranges
- Peer Listen Ranges
- Peer Local Subnets Only
- Port
- Public Range

**Restrictions**:

- Allow Activity Continuation
- Allow Adding Game Center Friends
- Allow Air Drop
- Allow Auto Unlock
- Allow Camera
- Allow Cloud Address Book
- Allow Cloud Bookmarks
- Allow Cloud Calendar
- Allow Cloud Desktop And Documents
- Allow Cloud Document Sync
- Allow Cloud Keychain Sync
- Allow Cloud Mail
- Allow Cloud Notes
- Allow Cloud Photo Library
- Allow Cloud Private Relay
- Allow Cloud Reminders
- Allow Content Caching
- Allow Diagnostic Submission
- Allow Dictation
- Allow Erase Content And Settings
- Allow Fingerprint For Unlock
- Allow Game Center
- Allow iTunes File Sharing
- Allow Multiplayer Gaming
- Allow Music Service
- Allow Passcode Modification
- Allow Password Auto Fill
- Allow Password Proximity Requests
- Allow Password Sharing
- Allow Remote Screen Observation
- Allow Screen Shot
- Allow Spotlight Internet Results
- Allow Wallpaper Modification
- Enforced Fingerprint Timeout
- Enforced Software Update Delay
- Enforced Software Update Major OS Deferred Install Delay
- Enforced Software Update Minor OS Deferred Install Delay
- Enforced Software Update Non OS Deferred Install Delay
- Force Classroom Automatically Join Classes
- Force Classroom Request Permission To Leave Classes
- Force Classroom Unprompted App And Device Lock
- Force Delayed App Software Updates
- Force Delayed Major Software Updates
- Force Delayed Software Updates
- Safari Allow Autofill

There isn't any conflict resolution between policies created using the Settings catalog and policies created using Templates. When creating new policies in the Settings Catalog, be sure there are no conflicting settings with your current policies.

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog in Microsoft Intune](../configuration/settings-catalog.md).

Applies to:
- macOS

<!-- ***********************************************-->

## Device security

### Microsoft Defender for Endpoint as the Tunnel client app for iOS will soon be out of Preview<!-- 9849514 --> 
The preview version of Microsoft Defender for Endpoint that supports [Microsoft Tunnel](../protect/microsoft-tunnel-overview.md) on iOS/iPadOS will soon be out of preview and become generally available.

When the Microsoft Defender for Endpoint app with support for Microsoft Tunnel becomes generally available for iOS, the standalone tunnel client app for iOS will be deprecated with support ending 60 days later.

If you are using the standalone tunnel app for iOS, prepare for this change by planning to [migrate to the Microsoft Defender for Endpoint app](../protect/microsoft-tunnel-migrate-app.md) before support for the standalone app ends.

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
