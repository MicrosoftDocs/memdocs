---
# required metadata
title: What's new in Microsoft Intune
titleSuffix:
description: Find out what's new in Microsoft Intune
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/27/2022
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
  - M365-identity-device-management
  - highpri
---

# What's new in Microsoft Intune

Learn what's new each week in Microsoft Intune. You can also find [important notices](#notices), [past releases](whats-new-archive.md), and information about [how Intune service updates are released](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728).

> [!Note]
> Each [monthly update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) may take up to three days to rollout and will be in the following order:
>
> - Day 1: Asia Pacific (APAC)
> - Day 2: Europe, Middle East, Africa (EMEA)
> - Day 3: North America
> - Day 4+: Intune for Government
>
> Some features may roll out over several weeks and might not be available to all customers in the first week.
>
> For a list of upcoming Intune feature releases, see [In development for Microsoft Intune](../fundamentals/in-development.md). For new information about Autopilot, see [Windows Autopilot What's New](../../autopilot/windows-autopilot-whats-new.md).

You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Get notified when this page is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us` -->

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
-->

## Week of July 25, 2022 (Service release 2207)

### Device management

#### Initiate compliance checks for your AOSP devices from the Microsoft Intune app<!--12645739 -->
You can now initiate a compliance check for your AOSP devices from the Microsoft Intune app. Go to **Device details**. This feature is available on devices that are enrolled via the Microsoft Intune app as user-associated (Android) AOSP devices.

#### Monitor bootstrap escrow status on a Mac<!-- 12404441 -->  
Monitor the bootstrap token escrow status for an enrolled Mac in the admin center. A new hardware property in Intune, called *Bootstrap token escrowed*, reports whether or not a bootstrap token has been escrowed in Intune. For more information about bootstrap token support for macOS, see [Bootstrap tokens](../enrollment/macos-enroll.md#bootstrap-tokens).

#### Enable Common Criteria mode for Android Enterprise devices<!-- 13158881 -->
For Android Enterprise devices, you can use a new setting, **Common Criteria mode**, to enable an elevated set of security standards that are typically used by only highly sensitive organizations, such as government establishments.

Applies to:
- Android 5.0 and newer
- Android Enterprise corporate owned fully managed
- Android Enterprise corporate owned dedicated devices
- Android Enterprise corporate owned work profile

The new setting, *Common Criteria mode*, is found in the *System security* category when you configure a [Device restrictions](../configuration/device-restrictions-configure.md) template for the *Android Enterprise - Fully Managed, Dedicated, and Corporate-Owned Work Profile*.
 
Devices that receive a policy with *Common Criteria mode* set to **Require**, elevate security components that include but are not limited to:  
- AES-GCM encryption of Bluetooth Long Term Keys
- Wi-Fi configuration stores
- Blocks bootloader download mode, the manual method for software updates
- Mandates additional key zeroization on key deletion
- Prevents non-authenticated Bluetooth connections
- Requires that FOTA updates have 2048-bit RSA-PSS signature

Learn more about Common Criteria:
- [Common Criteria for Information Technology Security Evaluation](https://www.commoncriteriaportal.org) at commoncriteriaportal.org
- [CommonCriteriaMode](https://developers.google.com/android/management/reference/rest/v1/enterprises.policies#commoncriteriamode) in the Android Management API documentation
- [Knox Deep Dive: Common Criteria Mode](https://www.samsungknox.com/blog/knox-deep-dive-common-criteria-mode) at samsungknox.com

#### New hardware detail available for individual devices running on iOS/iPadOS and macOS<!-- 9598434 -->
Select **Devices** > **All devices** > *select one of your listed devices* and open it's **Hardware** details. The following new detail is available in the **Hardware** pane of individual devices:
 - **Product name**: Shows the product name of the device, such as iPad8,12. Available for iOS/iPadOS and macOS devices. 

For more information, see [View device details with Microsoft Intune](../remote-actions/device-inventory.md).

Applies to:
- iOS/iPadOS, macOS

#### Remote help Version: 4.0.1.12 release<!-- 14999203 -->
With Remote help 4.0.1.12 various fixes were introduced to address the 'Try again later' message that appears when not authenticated. The fixes also include an improved auto-update capability. 

For more information, see [Use remote help with Intune and Microsoft Endpoint Manager](../remote-actions/remote-help.md)

### Device enrollment

#### Intune supports sign-in from another device during iOS/iPadOS Setup Assistant with modern authentication<!-- 12377183 -->  
Users going through automated device enrollment (ADE) can now authenticate by signing in from another device.  This option is available for iOS/iPadOS devices enrolling via Setup Assistant with modern authentication. The screen that prompts device users to sign in from another device is embedded into Setup Assistant and shown to them during enrollment. For more information about the sign-in process for users, see [Get the Intune Company Portal app (../user-help/sign-in-to-the-company-portal.md#sign-in-via-another-device).  

#### Detect and manage hardware changes on Windows Autopilot devices<!-- 12795465 --> 
Microsoft Intune will now alert you when it detects a hardware change on an Autopilot-registered device. You can view and manage all affected devices in the admin center. Additionally, you have the option to remove the affected device from Windows Autopilot and register it again so that the hardware change is accounted for.

### Device configuration

#### New macOS Microsoft AutoUpdate (MAU) settings in the Settings Catalog<!-- 14873468 -->
The Settings Catalog supports settings for Microsoft AutoUpdate (MAU) (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform >**Settings catalog (preview)** for profile type).

The following settings are now available:

**Microsoft Auto Update**:

- Automatically acknowledge data collection policy
- Days before forced updates
- Deferred updates
- Disable Office Insider membership
- Enable AutoUpdate
- Enable check for updates
- Enable extended logging
- Register app on launch
- Update cache server
- Update channel
- Update check frequency (mins)
- Updater optimization technique

The settings can be used to configure preferences for the following applications:

- Company Portal
- Microsoft Auto Update
- Microsoft Defender
- Microsoft Defender ATP
- Microsoft Edge
- Microsoft Edge Beta
- Microsoft Edge Canary
- Microsoft Edge Dev
- Microsoft Excel
- Microsoft OneNote
- Microsoft Outlook
- Microsoft PowerPoint
- Microsoft Remote Desktop
- Microsoft Teams
- Microsoft Word
- OneDrive
- Skype for Business

For more information about the Settings Catalog, go to:
- [Tasks you can complete using the Settings Catalog in Intune](../configuration/settings-catalog-common-features.md)
- [Create a policy using settings catalog in Microsoft Intune](../configuration/settings-catalog.md)

For more information about Microsoft AutoUpdate settings you can configure, go to:
- [Use preferences to manage privacy controls for Office for Mac - Deploy Office](/deployoffice/privacy/mac-privacy-preferences#preference-setting-for-connected-experiences-that-download-online-content).
- [Set a deadline for updates from Microsoft AutoUpdate](/deployoffice/mac/mau-deadline)

Applies to:
- macOS

#### New iOS/iPadOS settings in the Settings Catalog<!-- 14875716 -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. There are new iOS/iPadOS settings available in the Settings Catalog (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Settings catalog** for profile type).

New settings include:

**Networking > Cellular**:
- Allowed Protocol Mask
- Allowed Protocol Mask In Domestic Roaming
- Allowed Protocol Mask In Roaming
- Authentication Type
- Name
- Password
- Proxy Port
- Proxy Server
- Username

The following settings are also in Settings Catalog. Previously, they were only available in Templates:

**User experience > Notifications**:
- Grouping type
- Preview type
- Show In Car Play

**Printing > Air Print**:
- Force TLS
- Port

**App Management > App Lock**:
- Disable Auto Lock
- Disable Device Rotation
- Disable Ringer Switch
- Disable Sleep Wake Button
- Disable Touch
- Disable Volume Buttons
- Enable Assistive Touch
- Enable Invert Colors
- Enable Mono Audio
- Enable Speak Selection
- Enable Voice Control
- Enable Voice Over
- Enable Zoom
- Assistive Touch
- Invert Colors
- Voice Control
- Voice Over
- Zoom

**Networking > Domains**:
- Safari Password Auto Fill Domain

**Networking > Network Usage Rules**:
- Application Rules
- Allow Cellular Data
- Allow Roaming Cellular Data
- App Identifier Matches

**Restrictions**:
- Allow Account Modification
- Allow Activity Continuation
- Allow Adding Game Center Friends
- Allow Air Drop
- Allow Air Print
- Allow Air Print Credentials Storage
- Allow Air Print iBeacon Discovery
- Allow App Cellular Data Modification
- Allow App Clips
- Allow App Installation
- Allow App Removal
- Allow Apple Personalized Advertising
- Allow Assistant
- Allow Assistant User Generated Content
- Allow Assistant While Locked
- Allow Auto Correction
- Allow Auto Unlock
- Allow Automatic App Downloads
- Allow Bluetooth Modification
- Allow Bookstore
- Allow Bookstore Erotica
- Allow Camera
- Allow Cellular Plan Modification
- Allow Chat
- Allow Cloud Backup
- Allow Cloud Document Sync
- Allow Cloud Keychain Sync
- Allow Cloud Photo Library
- Allow Cloud Private Relay
- Allow Continuous Path Keyboard
- Allow Definition Lookup
- Allow Device Name Modification
- Allow Diagnostic Submission
- Allow Diagnostic Submission Modification
- Allow Dictation
- Allow Enabling Restrictions
- Allow Enterprise App Trust
- Allow Enterprise Book Backup
- Allow Enterprise Book Metadata Sync
- Allow Erase Content And Settings
- Allow ESIM Modification
- Allow Explicit Content
- Allow Files Network Drive Access
- Allow Files USB Drive Access
- Allow Find My Device
- Allow Find My Friends
- Allow Find My Friends Modification
- Allow Fingerprint For Unlock
- Allow Fingerprint Modification
- Allow Game Center
- Allow Global Background Fetch When Roaming
- Allow Host Pairing
- Allow In App Purchases
- Allow iTunes
- Allow Keyboard Shortcuts
- Allow Listed App Bundle IDs
- Allow Lock Screen Control Center
- Allow Lock Screen Notifications View
- Allow Lock Screen Today View
- Allow Mail Privacy Protection
- Allow Managed Apps Cloud Sync
- Allow Managed To Write Unmanaged Contacts
- Allow Multiplayer Gaming
- Allow Music Service
- Allow News
- Allow NFC
- Allow Notifications Modification
- Allow Open From Managed To Unmanaged
- Allow Open From Unmanaged To Managed
- Allow OTAPKI Updates
- Allow Paired Watch
- Allow Passbook While Locked
- Allow Passcode Modification
- Allow Password Auto Fill
- Allow Password Proximity Requests
- Allow Password Sharing
- Allow Personal Hotspot Modification
- Allow Photo Stream
- Allow Podcasts
- Allow Predictive Keyboard
- Allow Proximity Setup To New Device
- Allow Radio Service
- Allow Remote Screen Observation
- Allow Safari
- Allow Screen Shot
- Allow Shared Device Temporary Session
- Allow Shared Stream
- Allow Spell Check
- Allow Spotlight Internet Results
- Allow System App Removal
- Allow UI App Installation
- Allow UI Configuration Profile Installation
- Allow Unmanaged To Read Managed Contacts
- Allow Unpaired External Boot To Recovery
- Allow Untrusted TLS Prompt
- Allow USB Restricted Mode
- Allow Video Conferencing
- Allow Voice Dialing
- Allow VPN Creation
- Allow Wallpaper Modification
- Autonomous Single App Mode Permitted App IDs
- Blocked App Bundle IDs
- Enforced Software Update Delay
- Force Air Drop Unmanaged
- Force Air Play Outgoing Requests Pairing Password
- Force Air Print Trusted TLS Requirement
- Force Assistant Profanity Filter
- Force Authentication Before Auto Fill
- Force Automatic Date And Time
- Force Classroom Automatically Join Classes
- Force Classroom Request Permission To Leave Classes
- Force Classroom Unprompted App And Device Lock
- Force Delayed Software Updates
- Force Encrypted Backup
- Force iTunes Store Password Entry
- Force Limit Ad Tracking
- Force On Device Only Dictation
- Force On Device Only Translation
- Force Watch Wrist Detection
- Force WiFi Power On
- Force WiFi To Allowed Networks Only
- Require Managed Pasteboard
- Safari Accept Cookies
- Safari Allow Autofill
- Safari Allow Java Script
- Safari Allow Popups
- Safari Force Fraud Warning

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:
- iOS/iPadOS

#### New macOS settings available in the Settings Catalog<!-- 14875745 -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. There are new settings are available in the Settings Catalog (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type).

New settings include:

**System configuration > System extensions**:

- Removable System Extensions

The following settings are also in Settings Catalog. Previously, they were only available in Templates:

**System configuration > System extensions**:
- Allow User Overrides
- Allowed System Extension Types
- Allowed System Extensions
- Allowed Team Identifiers

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:
- macOS

#### New search feature in Preview devices when creating a filter<!-- 14921046 -->
In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can create filters, and then use these filters when assigning apps and policies (**Devices** > **Filters** > **Create**).

When you create a filter, you can select **Preview devices** to see a list of enrolled devices that match your filter criteria. In **Preview devices**, you can also search through the list using the device name, OS version, device model, device manufacturer, user principal name of the primary user, and device ID.

For more information on filters, go to [Use filters when assigning your apps, policies, and profiles in Microsoft Endpoint Manager](../fundamentals/filters.md).

## Week of July 18, 2022

### Device management

#### New event viewers to assist in debugging WMI issues<!-- 14712854  -->
Intune’s remote action to [collect diagnostics](../remote-actions/collect-diagnostics.md#collect-diagnostics) has been expanded to collect details about Windows Management Instrumentation (WMI) app issues.

The new event viewers include the following:
- Microsoft-Windows-WMI-Activity/Operational
- Microsoft-Windows-WinRM/Operational

For more information about Windows device diagnostics, see [Collect diagnostics from a Windows device](../remote-actions/collect-diagnostics.md).

## Week of July 4, 2022

### Device management

#### Endpoint analytics scores per device model<!-- 14439211 -->

Endpoint analytics now displays [scores by device model](../../analytics/scores.md#bkmk_model). These scores help admins contextualize the user experience across device models in the environment. Scores per model and per device are available in all Endpoint analytics reports, including the [Work from anywhere](../../analytics/work-from-anywhere.md) report.

### Monitor and troubleshoot

#### Use Collect diagnostics to collect details about Windows expedited updates<!--  14337387 -->

Intune’s remote action to [Collect diagnostics](../remote-actions/collect-diagnostics.md) now collects additional details about [Windows expedited updates](../protect/windows-10-expedite-updates.md) that you deploy to devices. This information can be of use when troubleshooting problems with expedited updates.

The new details that are collected include:  
- Files: `C:\Program Files\Microsoft Update Health Tools\Logs\*.etl`
- Registry Keys: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CloudManagedUpdate`


## Week of June 27, 2022 (Service release 2206)

### App management

#### Enterprise feedback policies for Web Company Portal<!-- 9846764 -->
Feedback settings are now available to address M365 enterprise feedback policies for the currently logged in user via the [Microsoft 365 Apps admin center](https://config.office.com/). The settings are used to determine whether feedback can be enabled or must be disabled for a user in the Web Company Portal. For related information, see [Configure feedback settings for Company Portal and Microsoft Intune apps](../apps/company-portal-app.md#configure-feedback-settings-for-company-portal-and-microsoft-intune-apps).

#### App Protection Policies with Android Enterprise dedicated devices and Android (AOSP) devices<!-- 13819227 -->
Intune-managed Android Enterprise dedicated devices enrolled with Azure Active Directory (Azure AD) shared mode and Android (AOSP) devices can now receive app protection policies and can be targeted separately from other Android device types. For related information, see [Add Managed Google Play apps to Android Enterprise devices with Intune](../apps/apps-add-android-for-work.md). For more information about Android Enterprise dedicated devices and Android (AOSP), see [Android Enterprise dedicated devices](../fundamentals/deployment-guide-enrollment-android.md#android-enterprise-dedicated-devices).

### Device security

#### Users assigned the Endpoint Security Manager admin role can modify Mobile Threat Defense connector settings<!-- 14179885 -->
We’ve updated the permissions of the built-in [Endpoint Security Manager](../fundamentals/role-based-access-control.md#built-in-roles) admin role. The role now has the **Modify** permission for the **Mobile Threat Defense** category set to **Yes**. With this change, users assigned this role have permission to change the [Mobile Threat Defense connector](../protect/mtd-connector-enable.md) (MTD connector) settings for your Tenant. Previously, this permission was set to *No*.

If you missed the previous notice about this coming change, now is a good time to review the users that are assigned the *Endpoint Security Manager* role for your tenant. If any should not have permissions to edit the MTD connector settings, update their role permissions or [create a custom role](../fundamentals/create-custom-role.md) that includes only *Read* permissions for Mobile Threat Defense.

View the full list of permissions for the built-in [Endpoint Security Manager role](../protect/endpoint-security.md#permissions-granted-by-the-endpoint-security-manager-role).

#### Improved certificate profile support for Android Enterprise Fully Managed devices<!-- 14217083  -->
We’ve improved our [PKCS](../protect/certificates-pfx-configure.md) and [SCEP](../protect/certificates-profile-scep.md) certificate profile support for Android Enterprise Fully Managed (Device Owner) devices. You can now use the Intune device ID variable, **CN={{DeviceID}}**, as the subject alternative name (SAN) in your certificates for these devices. 

### Device configuration

### Certificate profiles support for Android (ASOP) devices<!-- 8506319, 8506363 -->
You can now use the following [certificate profiles](../protect/certificates-configure.md) with corporate-owned and userless devices that run the Android Open Source Project (AOSP) platform: 
- Trusted certificate profile
- PKCS certificate profile

#### New settings for DFCI profiles on Windows 10/11 devices<!-- 6039135 -->
On Windows 10/11 devices, you can create a Device Firmware Configuration Interface (DFCI) profile (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type).

DFCI profiles let Intune pass management commands to UEFI (Unified Extensible Firmware Interface) using the DFCI firmware layer. This additional firmware layer makes configuration more resilient to malicious attacks. DFCI also limits end users' control over the BIOS by graying out managed settings.

There are new settings you can configure:
- **Microphones and Speakers**:
  - Microphones

- **Radios**:
  - Bluetooth
  - Wi-Fi

- **Ports**:
  - USB type A

- **Wake settings**:
  - Wake on LAN
  - Wake on power

For more information, see the following resources:
- [Use Device Firmware Configuration Interface profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) profile settings in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows-settings.md)

Applies to:
- Windows 10/11

#### Add custom support information to Android Enterprise devices<!-- 7913128 -->
On Android Enterprise devices, you can create a device restrictions configuration profile that manages device settings (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** > **Fully managed, dedicated, and corporate-owned work profile** for platform > **Device restrictions** for profile type > **Custom support information**).

There are some new settings you can configure:
- **Short support message**: When users try to change a managed setting, you can add a short message that's shown to users in a system dialog window.
- **Long support message**: You can add a long message that's shown in **Settings** > **Security** > **Device admin apps** > **Device Policy**.

By default, the OEM default messages are shown. When you deploy a custom message, the Intune default message is also deployed. If you don't enter a custom message for the device's default language, then the Intune default message is shown. 

For example, you deploy a custom message for English and French. The user changes the device's default language to Spanish. Since you didn't deploy a custom message to the Spanish language, the Intune default message is shown.

The Intune default message is translated for all languages in the Endpoint Manger admin center (**Settings** > **Language + Region**). The **Language** setting value determines the default language used by Intune. By default, it's set to **English**.

In the policy, you can customize the messages for the following languages:
- Czech
- German
- English (United States)
- Spanish (Spain)
- French (France)
- Hungarian
- Indonesian
- Italian
- Japanese
- Korean
- Dutch
- Polish
- Portuguese (Brazil)
- Portuguese (Portugal)
- Russian
- Swedish
- Turkish
- Chinese (Simplified)
- Chinese (Traditional)

For more information on these settings and the other settings you can configure, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android 7.0 and newer
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)
- Android Enterprise corporate owned work profile (COPE)

#### Create and deploy Wi-Fi profiles to Android AOSP devices<!-- 8506299 -->
You create configure and deploy a Wi-Fi profile to your Android AOSP devices.

For more information on these settings, go to [Add Wi-Fi settings for Android (AOSP) devices in Microsoft Intune](../configuration/wi-fi-settings-android-aosp.md).

Applies to:
- Android (AOSP)

#### Settings catalog is generally available (GA) for Windows and macOS devices<!-- 9558656 -->
The settings catalog is generally available (GA). For more information, go to:
- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)
- [Tasks you can complete using the Settings Catalog in Intune](../configuration/settings-catalog-common-features.md)

Applies to:
- macOS
- Windows 10/11

#### Migrate feature in Group policy analytics supports sovereign clouds<!-- 13927582 -->
Using Group Policy analytics, you can import your on-premises GPOs, and create a settings catalog policy using these GPOs. Previously, this Migrate feature wasn't supported on Sovereign Clouds.

The Migrate feature is now supported on Sovereign Clouds.

For more information on these features, go to:
- [Analyze your on-premises GPOs using Group Policy analytics in Microsoft Endpoint Manager](../configuration/group-policy-analytics.md)
- [Create a Settings Catalog policy using your imported GPOs in Microsoft Endpoint Manager](../configuration/group-policy-analytics-migrate.md)

#### iOS/iPadOS platform is in Settings Catalog<!-- 13934066 -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. The iOS/iPadOS platform and some settings are now available in the Settings Catalog (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Settings catalog** for profile type).

New settings include:

**Accounts > Caldav**:

- Card DAV Account Description
- Card DAV Host Name
- Card DAV Password
- Card DAV Port
- Card DAV Principal URL
- Card DAV Use SSL
- Card DAV Username

**Accounts > Carddav**:

- Card DAV Account Description
- Card DAV Host Name
- Card DAV Password
- Card DAV Port
- Card DAV Principal URL
- Card DAV Use SSL
- Card DAV Username

**AirPlay**:

- Allow List
- Password

- **Profile Removal Password**:

- Removal Password

**Proxies > Global HTTP Proxy**:

- Proxy Captive Login Allowed
- Proxy PAC Fallback Allowed
- Proxy PAC URL
- Proxy Password
- Proxy Server
- Proxy Server Port
- Proxy Type
- Proxy Username

The following settings are also in Settings Catalog. Previously, they were only available in Templates:

**Networking > Domains**:

- Email Domains

**Printing > Air Print**:

- Printers
- IP Address
- Resource Path

**Restrictions**:

- Allow Activity Continuation
- Allow Adding Game Center Friends
- Allow Air Drop
- Allow Auto Unlock
- Allow Camera
- Allow Cloud Document Sync
- Allow Cloud Keychain Sync
- Allow Cloud Photo Library
- Allow Cloud Private Relay
- Allow Diagnostic Submission
- Allow Dictation
- Allow Erase Content And Settings
- Allow Fingerprint For Unlock
- Allow Game Center
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
- Enforced Software Update Delay
- Force Classroom Automatically Join Classes
- Force Classroom Request Permission To Leave Classes
- Force Classroom Unprompted App And Device Lock
- Force Delayed Software Updates
- Safari Allow Autofill

**Security > Passcode**:

- Allow Simple Passcode
- Force PIN
- Max Failed Attempts
- Max Grace Period
- Max Inactivity
- Max PIN Age In Days
- Min Complex Characters
- Min Length
- PIN History
- Require Alphanumeric Passcode

**User Experience > Notifications**:

- Alert Type
- Badges Enabled
- Bundle Identifier
- Critical Alert Enabled
- Notifications Enabled
- Show In Lock Screen
- Show In Notification Center
- Sounds Enabled

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:
- iOS/iPadOS

#### Use TEAP authentication in wired networks device configuration profiles for Windows devices<!-- 14042602 -->
On Windows devices, you can create a **Wired Networks** device configuration profile that supports the Extensible Authentication Protocol (EAP) (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Wired networks** for profile type).

When you create the profile, you can use the Tunnel Extensible Authentication Protocol (TEAP).

For more information on wired networks, go to [Add and use wired networks settings on your macOS and Windows devices in Microsoft Intune](../configuration/wired-networks-configure.md).

Applies to:
- Windows 11
- Windows 10

#### Unlock the work profile on Android Enterprise corporate owned work profile (COPE) devices after a set time using password, PIN, or pattern<!-- 14133548 -->

On Android Enterprise devices, you can create a device restrictions configuration profile that manages device settings (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** > **Fully managed, dedicated, and corporate-owned work profile** for platform > **Device restrictions** for profile type).

On Android Enterprise COPE devices, you can configure the **Work profile password** > **Required unlock frequency** setting. Use this setting to select how long users have before they're required to unlock the work profile using a strong authentication method.

For more information on this setting, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android 8.0 and newer
- Android Enterprise corporate owned work profile (COPE)

#### New macOS settings in Settings Catalog<!-- 14158964 -->
The Settings Catalog has new macOS settings you can configure (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform >**Settings catalog** for profile type):

**Accounts > Caldav**:

- Cal DAV Account Description
- Cal DAV Host Name
- Cal DAV Password
- Cal DAV Port
- Cal DAV Principal URL
- Cal DAV Use SSL
- Cal DAV Username

**Accounts > Carddav**:

- Card DAV Account Description
- Card DAV Host Name
- Card DAV Password
- Card DAV Port
- Card DAV Principal URL
- Card DAV Use SSL
- Card DAV Username

**User Experience > Dock**:

- Allow Dock Fixup Override
- Auto Hide
- Auto Hide Immutable
- Contents Immutable
- Double Click Behavior
- Double Click Behavior Immutable
- Large Size
- Launch Animation
- Launch Animation Immutable
- Magnification
- Magnification Size Immutable
- Magnify Immutable
- MCX Dock Special Folders
- Minimize Effect
- Minimize Effect Immutable
- Minimize Into Application Immutable
- Minimize To Application
- Orientation
- Persistent Apps
- Persistent Others
- Position Immutable
- Show Indicators Immutable
- Show Process Indicators
- Show Recents
- Show Recents Immutable
- Size Immutable
- Static Apps
- Static Only
- Static Others
- Tile Size
- Window Tabbing
- Window Tabbing Immutable

**System Configuration > Energy Saver**:

- Desktop Power
- Desktop Schedule
- Destroy FV Key On Standby
- Laptop Battery Power
- Laptop Power
- Sleep Disabled

**System Configuration > System Logging**:

- Enable Private Data

**System Configuration > Time Server**:

- Time Server
- Time Zone

The following settings are also in Settings Catalog. Previously, they were only available in Templates:

**Security > Passcode**:

- Allow Simple Passcode
- Change At Next Auth
- Force PIN
- Max Failed Attempts
- Max Grace Period
- Max Inactivity
- Max PIN Age In Days
- Min Complex Characters
- Min Length
- Minutes Until Failed Login Reset
- PIN History
- Require Alphanumeric Passcode

There isn't any conflict resolution between policies created using the Settings catalog and policies created using Templates. When creating new policies in the Settings Catalog, be sure there are no conflicting settings with your current policies.

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog in Microsoft Intune](../configuration/settings-catalog.md).

Applies to:
- macOS

#### New Microsoft Office and Microsoft Outlook preference settings in the macOS Settings Catalog<!-- 14193331 -->
The Settings Catalog supports preference settings for Microsoft Office and Microsoft Outlook (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform >**Settings catalog (preview)** for profile type). 

The following settings are available:

**Microsoft Office > Microsoft Office**:

- Allow experiences and functionality that analyzes user content
- Allow experiences and functionality that downloads user content
- Allow macros to modify Visual Basic projects
- Allow optional connected experiences
- Allow Visual Basic macros to use system APIs
- Background accessibility checking
- Default to local files for open - save
- Diagnostic data level
- Disable cloud fonts
- Disable third-party store add-in catalog
- Disable user surveys
- Enable automatic sign-in
- Prevent all Visual Basic macros from executing
- Prevent Visual Basic macros from using external dynamic libraries
- Prevent Visual Basic macros from using legacy MacScript
- Prevent Visual Basic macros from using pipes to communicate
- Show Template Gallery on app launch
- Show Whats New dialog
- Visual Basic macro policy

**Microsoft Office > Microsoft Outlook**:

- Allow S - MIME certificates without a matching email address
- Allowed Email Domains
- Default domain name
- Default weather location
- Disable 'Do Not Forward' options
- Disable automatic updating of weather location
- Disable email signatures
- Disable export to OLM files
- Disable import from OLM and PST files
- Disable Junk settings
- Disable Microsoft 365 encryption options
- Disable Microsoft Teams meeting support
- Disable S - MIME
- Disable Skype for Business meeting support
- Download embedded images
- Enable New Outlook
- Hide On My Computer folders
- Hide the 'Get started with Outlook' control in the task pane
- Hide the 'Personalize the new Outlook' dialog
- Set the order in which S - MIME certificates are considered
- Set theme
- Specify first day of the week
- Trust Office 365 autodiscover redirects
- Use domain-based autodiscover instead of Office 365

For more information about the Settings Catalog, go to:

- [Tasks you can complete using the Settings Catalog in Intune](../configuration/settings-catalog-common-features.md)
- [Create a policy using settings catalog in Microsoft Intune](../configuration/settings-catalog.md)

For more information about Microsoft Office and Outlook settings you can configure, go to:

- [Use preferences to manage privacy controls for Office for Mac - Deploy Office](/deployoffice/privacy/mac-privacy-preferences#preference-setting-for-connected-experiences-that-download-online-content).
- [Set preferences for Outlook for Mac - Deploy Office](/deployoffice/mac/preferences-outlook)

Applies to:
- macOS

### Device management

#### Remotely restart and shut down macOS device<!-- 12472418 -->
You'll be able to remotely restart or shutdown a macOS device using device actions. These device actions are available for devices running macOS 10.13 and later. 

For more information, see [Restart devices with Microsoft Intune](../remote-actions/device-restart.md). 

#### Additional Remote actions for Android (AOSP) Corporate devices<!-- 8504019 -->
For Android Open Source Project (AOSP) Corporate devices, you can soon leverage additional remote actions from the Microsoft Endpoint Manager admin center - Reboot and Remote lock. 

For information about these features, see:
 - [Remotely restart devices with Intune](../remote-actions/device-restart.md)
 - [Remotely lock devices with Intune](../remote-actions/device-remote-lock.md).

Applies to:
- Android Open Source Project (AOSP)

#### User configuration support for  Windows 11 multi-session VMs is in public preview<!-- 7231329 -->

You'll be able to:
- Configure user scope policies using **Settings catalog** and assign to groups of users
- Configure user certificates and assign to users
- Configure PowerShell scripts to install in the user context and assign to users

Applies to: 
 - Windows 11

> [!Note]
> User support for Windows 10 multi-session builds will be available later this year.

For more information, go to
[Using Azure Virtual Desktop multi-session with Microsoft Intune](../fundamentals/azure-virtual-desktop-multi-session.md)

#### View a managed device's group membership<!-- 4100067 -->
In the monitor section of the **Devices** workload of Intune, you can view the group membership of all Azure AD groups for a managed device. You can select **Group Membership** by signing in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and selecting **Devices** > **Monitor** > *select a device* > **Group Membership**. For more information, see [Device group membership report](../fundamentals/reports.md#device-group-membership-report-organizational).

#### Improved certificate reporting details<!-- 13316515 -->
We’ve changed what Intune displays when you view certificate details for devices and certificate profiles. To view the report, in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to > **Devices** > **Monitor** > **Certificates**.

With the improved reporting view, Intune displays information for the following:

- Valid certificates
- Certificates that were revoked within the last 30 days
- Certificates that expired within the last 30 days

The report no longer displays details for certificates that are not valid or that are no longer on a device.

### Device enrollment

### Utilize bootstrap tokens on macOS devices<!-- 12693392 -->
Bootstrap token support, previously in public preview, is now generally available to all Microsoft Intune customers, including GCC High and Microsoft Azure Government Cloud tenants. Intune supports the use of bootstrap tokens on enrolled devices running macOS, version 10.15 or later.

Bootstrap tokens allow for non-admin users to have increased MDM permissions, and perform specific software functions on behalf of the IT admin.  Bootstrap tokens is supported on:  

- Supervised devices (in Intune, that's all user-approved enrollments)  
- Devices enrolled in Intune via Apple automated device enrollment   

For more information about how bootstrap tokens work with Intune, see [Set up enrollment for macOS devices](../enrollment/macos-enroll.md#bootstrap-tokens).

### Intune apps

#### Newly available protected apps for Intune<!-- 14469921, 14645753 -->
The following protected apps are now available for Microsoft Intune:

- Condeco by Condeco Limited
- RICOH Spaces by Ricoh Digital Services

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of June 13, 2022

### Device security

#### Microsoft Tunnel support for Red Hat Enterprise Linux 8.6<!-- 14642908  -->

You can now use Red Hat Enterprise Linux (RHEL) 8.6 with [Microsoft Tunnel](../protect/microsoft-tunnel-overview.md). There are no additional requirements beyond those that are needed for RHEL 8.5 support.
 
Like RHEL 8.5, you can use the [readiness tool](../protect/microsoft-tunnel-prerequisites.md#run-the-readiness-tool) (mst-readiness) to check for the presence of the ip_tables module in the Linux kernel. By default, RHEL 8.6 doesn’t load the ip_tables module.

For Linux servers that don't load the module, we've provided [instructions](../protect/microsoft-tunnel-prerequisites.md#manually-load-ip_tables) to load them immediately, and to configure the Linux server to automatically load them at boot.

## Week of June 6, 2022  

### App management  

#### Photo library data transfer support via app protection policies<!-- 9450163, 14062176 -->
You can now select to include **Photo Library** as a supported application storage service. By selecting **Photo Library** from the **Allow users to open data from selected services** or the **Allow users to save data to selected services** setting within Intune, you can allow managed accounts to allow *incoming* and *outgoing* data to and from their device's photo library to their managed apps on iOS and Android platforms. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App protection policies** > **Create Policy**. Choose either **iOS/iPadOS** or **Android**. This setting is available as part of the **Data protection** step and specifically for **Policy managed apps**. For related information, see [Data protection](../apps/app-protection-framework.md#data-protection-2).

#### UI improvements show Android enrollment is available, not required<!-- 8764312 -->

We updated the iconography in the Company Portal for Android app to make it easier for users to recognize when device enrollment is available to them but not required. The new iconography appears in scenarios where the device enrollment availability is set to **Available, no prompts** in the admin center (**Tenant admin** > **Customization** > **Create** or **Edit** a policy > **Settings**).      

Changes include:  

 - On the Devices screen, users will no longer see a red exclamation point next to a non-enrolled device.  
 - On the Device Details screen, users will no longer see a red exclamation point next to the enrollment message. Instead, they will see the info **(i)** icon.    

To view screenshots of the changes, see [UI updates for Intune end-user apps](../fundamentals/whats-new-app-ui.md). 

### Device management

#### Windows Update compatibility reports for Apps and Drivers (public preview)<!-- 11019842 -->

In public preview, two Windows Update compatibility reports are now available to help you prepare for a Windows upgrade or update. These reports fill a gap that is currently covered by Desktop Analytics, which is [scheduled to be retired](https://aka.ms/DANextSteps) on November 30, 2022.

Use these reports to help you plan for an upgrade from Windows 10 to 11 or for installing the latest Windows feature update:

- **Windows feature update device readiness report (Preview)** - This report provides per-device information about compatibility risks that are associated with an upgrade or update to a chosen version of Windows.
- **Windows feature update compatibility risks report (Preview)** - This report provides a summary view of the top compatibility risks across your organization for a chosen version of Windows. You can use this report to understand which compatibility risks impact the greatest number of devices in your organization.

These reports are rolling out to tenants over the next week. If you don't see them yet, check back again in a day or so. To learn about prerequisites, licensing, and what information is available with these reports, see [Windows Update compatibility reports](../protect/windows-update-compatibility-reports.md).


## Week of May 30, 2022 (Service release 2205)

### App management

#### iOS Company Portal minimum required version<!-- 13016075 -->
Starting June 1, 2022, the minimum supported version of the iOS Company Portal app will be v5.2205. If your users are running v5.2204 or below, they will be prompted for an update at login. If you have enabled the **[Block installing apps using App Store](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised)** device restriction setting, you will likely need to push an update to the related devices that use this setting. Otherwise, no action is needed. If you have a helpdesk, you may want to make them aware of the prompt to update the Company Portal app. In most cases, users have app updates set to automatic, so they receive the updated Company Portal app without taking any action. For related information, see [Intune Company Portal](../apps/company-portal-app.md).

#### Push notifications are automatically sent when device ownership changes from Personal to Corporate<!-- 12390037 -->
For iOS/iPad and Android devices, a push notification is now automatically sent when a device's [ownership type is changed from Personal to Corporate](../enrollment/corporate-identifiers-add.md#change-device-ownership). The notification is pushed through the Company Portal app on the device.

With this change, we've removed the Company Portal configuration setting that was previously used to manage this notification behavior.

#### iOS/iPadOS notifications require March Company Portal or newer<!-- 14131757 -->
With Intune's May (2205) service release, we have made service side updates to iOS/iPadOS notifications that require users to have the March Company Portal app (version 5.2203.0) or newer. If you are using functionality that could generate iOS/iPadOS Company Portal push notifications, you must ensure your users update the iOS/iPadOS Company Portal to continue receiving push notifications. There is no additional change in functionality. For related information, see [Update the Company Portal app](../user-help/install-a-new-version-of-the-company-portal-app.md).

#### Deployment of macOS LOB apps by uploading PKG-type installer files is now generally available<!-- 10671861 -->  
You can now deploy macOS line-of-business (LOB) apps by uploading PKG-type installer files to Intune. This capability is out of public preview and is now generally available. 

To add a macOS LOB app from [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **macOS** > **Add** > **Line-of-business app**. Additionally, the App Wrapping Tool for macOS will no longer be required to deploy macOS LOB apps. For related information, see [How to add macOS line-of-business (LOB) apps to Microsoft Intune](../apps/lob-apps-macos.md).

#### Improved report experience on the Managed Apps pane<!-- 10147133 -->
The **Managed Apps** pane has been updated to better display managed app details for a device. You can switch between displaying managed app details for the primary user and other users on a device, or display app details for the device without any user. The generated app details will be displayed using the primary user of the device when the report is initially loaded, or displayed with no primary user if none exists. For more information, see [Managed Apps report](../fundamentals/reports.md#managed-apps-report-organizational).

#### MSfB licenses and Apple VPP licenses<!-- 10742713a -->
Removing an Intune license from a user will no longer revoke app licenses granted through the Microsoft Store for Business or through Apple VPP. For related information, see [How to manage volume purchased apps from the Microsoft Store for Business with Microsoft Intune](../apps/windows-store-for-business.md), [Revoking iOS app licenses](../apps/vpp-apps-ios.md#revoking-app-licenses), and [Microsoft Intune licensing](../fundamentals/licenses.md).

#### Reporting for unlicensed users<!-- 10742713b -->
Intune will no longer remove users from all Intune reports when they are unlicensed. Until the user is deleted from Azure AD, Intune will continue to report the user in most common scenarios. For related information about reporting, see [Intune reports](../fundamentals/reports.md).

### Device security

#### New Device Control profile for Intune’s endpoint security Attack Surface Reduction policy<!-- 8844611 -->

As part of the continuing [rollout of new profiles for endpoint security policies](#new-profile-templates-and-settings-structure-for-endpoint-security-policies), which began in April 2022, we’ve released a new Device Control profile template for [Attack Surface Reduction](../protect/endpoint-security-asr-policy.md) policy for endpoint security in Intune. This profile replaces the previous profile of the same name for the *Windows 10 and later* platform.

With this replacement, only instances of the new profile can be created. However, any profiles you’ve previously created that use the old profile structure remain available to use, edit, and deploy.

The new Device Control profile:
- Includes all the settings that were available in the original profile.
- Introduces five new settings that are not available in the older profile.

The five new settings focus on removable devices, like USB devices:
- [Prevent installation of removable devices](/windows/client-management/mdm/policy-csp-admx-deviceinstallation?WT.mc_id=Portal-fx#admx-deviceinstallation-deviceinstall-removable-deny)
- [WPD Devices: Deny read access](/windows/client-management/mdm/policy-csp-admx-removablestorage?WT.mc_id=Portal-fx#admx-removablestorage-wpddevices-denyread-access-2)
- [WPD Devices: Deny read access (User)](/windows/client-management/mdm/policy-csp-admx-removablestorage?WT.mc_id=Portal-fx#admx-removablestorage-wpddevices-denyread-access-1)
- [WPD Devices: Deny write access](/windows/client-management/mdm/policy-csp-admx-removablestorage?WT.mc_id=Portal-fx#admx-removablestorage-wpddevices-denywrite-access-2)
- [WPD Devices: Deny write access (User)](/windows/client-management/mdm/policy-csp-admx-removablestorage?WT.mc_id=Portal-fx#admx-removablestorage-wpddevices-denywrite-access-1)

### Device configuration

#### Unlock Android Enterprise devices after a set time using password, PIN, or pattern<!-- 7913163 -->
On Android Enterprise devices, you can create a device restrictions configuration profile that manages device settings (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** > **Fully managed, dedicated, and corporate-owned work profile** for platform > **Device restrictions** for profile type).

In **Device password** and **Work profile password**, there's a new **Required unlock frequency** setting. Select how long users must unlock the device using a strong authentication method (password, PIN, or pattern). Your options:

- **24 hours since last pin, password, or pattern unlock**: The screen locks 24 hours after users last used a strong authentication method to unlock the device or work profile.
- **Device default** (default): The screen locks using the device's default time.

[2.3.4. Advanced passcode management](https://developers.google.com/android/work/requirements#2.3.-advanced-passcode-management_1) (opens Android's web site)

For a list of the settings you can configure, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android 8.0 and newer
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)
- Android Enterprise corporate owned work profile (COPE)

#### Use the Settings Catalog to create a Universal Print policy on Windows 11 devices<!-- 5513123 -->
Many organizations are moving their printer infrastructure to the cloud using [Universal Print](/universal-print/fundamentals/universal-print-whatis).

In the Endpoint Manager admin center, you can use the Settings Catalog to create a universal print policy (**Device configuration** > **Create profile** > **Windows 10 and later** for platform > **Settings catalog** for profile type > **Printer provisioning**). When you deploy the policy, users select the printer from a list of registered Universal Print printers.

For more information, go to [Create a Universal Print policy in Microsoft Intune](../configuration/settings-catalog-printer-provisioning.md).

Applies to:
- Windows 11

#### New macOS settings in the Settings Catalog<!-- 13923348 -->
The Settings Catalog has new macOS settings you can configure (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform >**Settings catalog** for profile type):

**Accounts > Accounts**:
- Disable Guest Account
- Enable Guest Account

**Networking > Firewall**:
- Allow Signed
- Allow Signed App
- Enable Logging
- Logging Option

**Parental Controls > Parental Controls Time Limits**:
- Family Controls Enabled
- Time Limits

**Proxies > Network Proxy Configuration**:
- Proxies
- Exceptions List
- Fall Back Allowed
- FTP Enable
- FTP Passive
- FTP Port
- FTP Proxy
- Gopher Enable
- Gopher Port
- Gopher Proxy
- HTTP Enable
- HTTP Port
- HTTP Proxy
- HTTPS Enable
- HTTPS Port
- HTTPS Proxy
- Proxy Auto Config Enable
- Proxy Auto Config URL String
- Proxy Captive Login Allowed
- RTSP Enable
- RTSP Port
- RTSP Proxy
- SOCKS Enable
- SOCKS Port Integer
- SOCKS Proxy

**Security > Smart Card**:
- Allow Smart Card
- Check Certificate Trust
- Enforce Smart Card
- One Card Per User
- Token Removal Action
- User Pairing

**Software Update**:
- Allow Pre Release Installation
- Automatic Check Enabled
- Automatic Download
- Automatically Install App Updates
- Automatically Install Mac OS Updates
- Config Data Install
- Critical Update Install
- Restrict Software Update Require Admin To Install

**User Experience > Screensaver User**:
- Idle Time
- Module Name
- Module Path

There isn't any conflict resolution between policies created using the Settings catalog and policies created using Templates. When creating new policies in the Settings Catalog, be sure there are no conflicting settings with your current policies.

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog in Microsoft Intune](../configuration/settings-catalog.md).

Applies to:
- macOS

### Intune apps

#### Newly available protected apps for Intune<!-- 13867257, 13867471, 13922181, 13983022, 14064381, 14121805 -->
The following protected apps are now available for Microsoft Intune:

- F2 Manager Intune by cBrain A/S
- F2 Touch Intune (Android) by cBrain A/S
- Microsoft Lists (Android) by Microsoft
- Microsoft Lens - PDF Scanner by Microsoft
- Diligent Boards by Diligent Corporation
- Secure Contacts by Provectus Technologies GmbH
- My Portal by MangoApps by MangoSpring Inc

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Device management

#### Software updates page for tenant attached devices<!-- 13089257, 13035723 -->
There's a new **Software updates** page for tenant attached devices. This page displays the status for software updates on a device. You can review which updates are successfully installed, failed, and are assigned but not yet installed. Using the timestamp for the update status assists with troubleshooting. For more information, see [Tenant attach: Software updates in the admin center](../../configmgr/tenant-attach/software-updates.md).

#### Microsoft Defender for Endpoint support for App Sync on iOS/iPadOS<!-- 9768396 -->
*Before you can use this capability you must opt in to an MDE Preview. To opt in, contact `mdatpmobile@microsoft.com`.* 

When you use Microsoft Defender for Endpoint (MDE) as your Mobile Threat Defense application, as part of a preview from MDE, you can [configure MDE to request Application Inventory data](../protect/advanced-threat-protection-configure.md#enable-microsoft-defender-for-endpoint-in-intune) from Intune from iOS/iPadOS devices. The following two settings are now available:

- **Enable App Sync for iOS Devices**:  Set to **On** to allow MDE to request metadata of iOS applications from Intune to use for threat analysis purposes. The iOS device must be MDM-enrolled and will provide updated app data during device check-in.

- **Send full application inventory data on personally owned iOS/iPadOS Devices**: This setting controls the application inventory data that Intune shares with MDE when MDE syncs app data and requests the app inventory list.

  When set to **On**, MDE can request a list of applications from Intune for personally owned iOS/iPadOS devices. This includes unmanaged apps as well as apps that were deployed through Intune.

  When set to **Off**, data about unmanaged apps isn’t provided. Intune does share data for the apps that were deployed through Intune.

#### Support for Retire on Android Enterprise corporate-owned work-profiles devices<!-- 10216870 -->
You can now use the **Retire** admin action in the **Microsoft Endpoint Manager admin center**  to remove the work profile including all corporate apps, data, and policies from an Android Enterprise corporate-owned work profile device. Go to **Endpoint Manager admin center** > **Devices** pane > **All Devices** > then select the name of the device you want to retire and select **Retire**.  

When you select **Retire**, the device is unenrolled from Intune management. However, all the data and apps associated with your personal profile will remain untouched on the device.
For more information, see [Retire or wipe devices using Microsoft Intune](../remote-actions/devices-wipe.md).

### Device enrollment

#### Improvements for enrollment profiles for Apple Automated Device Enrollment<!-- 13165752 -->
Two Setup Assistant skip panes, previously released in Intune for public preview, are now generally available to use in Intune. These screens typically appear in Setup Assistant during Apple Automated Device Enrollment (ADE).  You can configure screen visibility while you're setting up an enrollment profile in Intune.  Intune-supported screen settings are available in the device enrollment profile under the **Setup Assistant** tab.  The new skip panes are: 
 
- Pane name: **Get Started** 
  - Available for iOS/iPadOS 13 and later.
  - This pane is visible in Setup Assistant during ADE by default.  
  
- Pane name: **Auto Unlock with Apple Watch**
  - Available for macOS 12 and later. 
  - This pane is visible in Setup Assistant during ADE by default.  

There is no change to functionality from the public preview release.

#### Enroll to co-management from Windows Autopilot<!-- 11300628 -->
You can configure device enrollment in Intune to enable co-management, which happens during the [Windows Autopilot](../../autopilot/windows-autopilot.md) process. This behavior directs the workload authority in an orchestrated manner between Configuration Manager and Intune.

If the device is targeted with an [Autopilot enrollment status page (ESP) policy](../enrollment/windows-enrollment-status.md), the device will wait for Configuration Manager. The Configuration Manager client installs, registers with the site, and applies the production co-management policy. Then the Autopilot ESP continues.

For more information, see [How to enroll to co-management with Autopilot](../../configmgr/comanage/autopilot-enrollment.md).

## Week of May 9, 2022

### Device security

#### Security Management with Defender for Endpoint is generally available<!-- 13816763 -->

The Microsoft Endpoint Manager and Microsoft Defender for Endpoint (MDE) team are excited to announce the general availability of Security Management for MDE devices. As part of this general availability, support for Antivirus, Endpoint Detection and Response, as well as Firewall and Firewall rules are now generally available. This general availability applies to Windows Server 2012 R2 and Later, as well as Windows 10 and Windows 11 clients. In the future we will be adding support for additional platforms and profiles in a preview capacity.

For more information, see [Manage Microsoft Defender for Endpoint on devices with Microsoft Endpoint Manager](../protect/mde-security-integration.md).

### Device management


#### Elevation enhancements to Remote help<!-- 12453415 -->

Elevation permissions will no longer be assigned when a session is started. Elevation permissions will now apply only when JIT (just in time) access is requested.  The access is requested with the click of a button on the toolbar. 
When elevation permissions are assigned, the log off behavior for the sharer has been modified as follows:
 - If the admin (helper) ends the remote help session, the user (sharer) will not be logged off.
 - If the sharer tries to end the session, they will be prompted that they will be logged off if they continue.
 - If the sharer is a local admin on their device, the access UAC prompt option will not be available to the helper as they can guide the sharer to perform elevated actions under their own profile.
For more information about remote help, see [Use Remote help](../remote-actions/remote-help.md)

## Week of May 2, 2022

### App management

#### Update priority of Managed Google Play apps<!-- 11050956 -->
You can set the update priority of Managed Google Play apps on Android Enterprise devices that are dedicated, fully managed, or corporate-owned with a work profile. By selecting **Postpone** as the **Update Priority** app setting, the device will wait for 90 days after a new version of the app is detected before installing the app update. For related information, see [Add Managed Google Play apps to Android Enterprise devices with Intune](..\apps\apps-add-android-for-work.md).

## Week of April 25, 2022 (Service release 2204)

### App management

#### Updated app configuration policies list<!-- 13903969 -->
The **App configuration policies** list has been modified in Intune. This list will no longer contain the **Assigned** column. To view whether an app configuration policy has been assigned, navigate to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apps** > **App configuration policies** > *select a policy* > **Properties**.

#### Password complexity for Android devices<!-- 9321870 -->
The **Require device lock** setting in Intune has been extended to include values (**Low Complexity**, **Medium Complexity**, and **High Complexity**). If the device lock doesn’t meet the minimum password requirement, you can **warn**, **wipe data**, or **block** the end user from accessing a managed account in a managed app. This feature targets devices that operate on Android 11+. For devices operating on Android 11 and earlier, setting a complexity value of **Low**, **Medium**, or **High** will default to the expected behavior for **Low Complexity**. For related information, see [Android app protection policy settings in Microsoft Intune](..\apps\app-protection-policy-settings-android.md).
management
### Improvements to Win32 App Log collection<!-- 9978316 -->
Win32 App Log collection via Intune Management Extension has moved to the Windows 10 device diagnostic platform, reducing time to collect logs from 1-2 hours to 15 minutes. We've also increased the log size from 60mb to 250mb.  Along with performance improvements, the app logs are available under the **Device diagnostics monitor** action for each device, as well as the managed app monitor. For information about how to collect diagnostics, see [Collect diagnostics from a Windows device](..\remote-actions\collect-diagnostics.md) and [Troubleshooting Win32 app installations with Intune](/troubleshoot/mem/intune/troubleshoot-win32-app-install).

### Device management

#### Windows 10 and Windows 11 Enterprise multi-session is generally available<!-- 14012240-->

In addition to the existing functionality, you can now: 

 - Configure profiles under Endpoint Security when you select **Platform** Windows 10, Windows 11, and Windows Server.
 - Manage **Windows 10** and **Windows 11 Enterprise multi-session** VMs created in Azure Government Cloud in US Government Community (GCC) High and DoD. 

For more information, see [Windows 10/11 Enterprise multi-session remote desktops](../fundamentals/azure-virtual-desktop-multi-session.md).

#### Device actions available to Android (AOSP) users in Microsoft Intune app<!-- 12645718 -->
AOSP device users can now rename their enrolled devices in the Microsoft Intune app. This feature is available on devices enrolled in Intune as user-associated (Android) AOSP devices. For more information about Android (AOSP) management, see [Set up Intune enrollment for Android (AOSP) corporate-owned user-associated devices](../enrollment/android-aosp-corporate-owned-user-associated-enroll.md).  

#### Support for Audio Alert on Android corporate owned work profiles and fully managed (COBO and COPE) devices<!-- 13499471 -->
You can now use the device action **Play lost device sound**  to trigger an alarm sound on the device to assist in locating the lost or stolen Android Enterprise corporate owned work profile and fully managed devices. For more information, see [Locate lost or stolen devices](../remote-actions/device-locate.md).

### Device enrollment

#### New enrollment profile settings for Apple Automated Device Enrollment (public preview)<!-- 10111795 -->
We've added two new Setup Assistant settings that you can use with Apple Automated Device Enrollment. Each setting controls the visibility of a Setup Assistant pane shown during enrollment. Setup Assistant panes are shown during enrollment by default, so you have to adjust the settings in Microsoft Intune if you want to hide them. The new Setup Assistant settings are the following:<p>
- **Get Started** (preview):  Show or hide the Get Started pane during enrollment. For devices running iOS/iPadOS 13 and later. 
- **Auto Unlock with Apple Watch** (preview):  Show or hide the Unlock Your Mac with your Apple Watch pane during enrollment. For devices running macOS 12 and later.

 To configure Setup Assistant settings for Automated Device Enrollment, [create an iOS/iPadOS enrollment profile](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile) or [macOS enrollment profile](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile) in Microsoft Intune.  

### Device security

### Microsoft Defender for Endpoint as the Tunnel client app for iOS is now Generally Available<!-- 9849514  --> 

Use of Microsoft Defender for Endpoint that supports [Microsoft Tunnel](../protect/microsoft-tunnel-overview.md) on iOS/iPadOS is now out of preview and is generally available. With general availability, a new version of the Defender for Endpoint app for iOS is available from the App store to download and deploy. If you’ve been using the preview version as your Tunnel client app for iOS, we recommend you upgrade to the latest Defender for Endpoint app for iOS soon to gain the benefits of the latest updates and fixes.

As of August 30, 2022, the connection type is named **Microsoft Tunnel**.

With this release, by the end of June both the standalone Tunnel client app and the preview version of Defender for Endpoint as the Tunnel client app for iOS will be deprecated and be dropped from support. Soon after that deprecation, the standalone Tunnel client app will no longer function and will no longer support opening connections to Microsoft Tunnel.

If you're still using the standalone tunnel app for iOS, plan to [migrate to the Microsoft Defender for Endpoint app](../protect/microsoft-tunnel-migrate-app.md) before support for the standalone app ends and it’s support to connect to Tunnel no longer functions.


#### Attack surface reduction rules profile<!-- 8858871 -->
The **Attack Surface Reduction Rules (ConfigMgr)** profile for tenant attached devices is now in public preview. For more information, see [Tenant attach: Create and deploy attack surface reduction policies](../../configmgr/tenant-attach/deploy-asr-policy.md#bkmk_asr).

### Device configuration

#### Endpoint security profiles support filters<!-- 11889620 -->
There are some new features when using filters:
- When you create a device configuration profile for Windows devices, a per-policy report shows reporting information in the **Device and user check-in status** (**Devices** > **Configuration profiles** > Select an existing policy).

  When you select **View report**, the report has an **Assignment Filter** column. Use this column to determine if a filter successfully applied to your policy.

- Endpoint Security policies support filters. So, when you assign an endpoint security policy, you can use filters to assign the policy based on rules you create.

- When you create a new endpoint security policy, it automatically uses the [new device configuration profile reporting](#new-reporting-experience-for-device-configuration-profiles). When you look at the per-policy report, it also has an **Assignment Filter** column (**Devices** > **Configuration profiles** > Select an existing endpoint security policy > **View report**). Use this column to determine if a filter successfully applied to your policy.

For more information on filters, see:
- [Use filters when assigning your apps, policies, and profiles](filters.md)
- [List of platforms, policies, and app types supported by filters](filters-supported-workloads.md)

Applies to:
- All platforms

Does not apply to:
- Administrative Templates (Windows 10/11)
- Device Firmware Configuration Interface (DFCI) (Windows 10/11)
- OEMConfig (Android Enterprise)

#### Create a Settings Catalog policy using your imported GPOs with Group Policy analytics (public preview)<!-- 6379751 -->
Using Group Policy analytics, you can import your on-premises GPO, and see the settings that are supported in Microsoft Intune. It also shows any deprecated settings, or settings not available to MDM providers.

When the analysis runs, you see the settings that are ready for migration. There is a **Migrate** option that creates a Settings Catalog profile using your imported settings. Then, you can assign this profile to your groups.

For more information, go to [Create a Settings Catalog policy using your imported GPOs in Microsoft Endpoint Manager](../configuration/group-policy-analytics-migrate.md).

Applies to:
- Windows 11
- Windows 10

#### New wired networks device configuration profile for Windows devices<!-- 1746923 -->
There is a new **Wired Networks** device configuration profile for Windows 10/11 devices (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Wired networks** for profile type).

Use this profile to configure common wired network settings, including authentication, EAP type, server trust, and more. For more information on the settings you can configure, go to [Add wired network settings for Windows devices in Microsoft Intune](../configuration/wired-network-settings-windows.md).

Applies to:
- Windows 11
- Windows 10

#### "ADMX_" Policy CSP settings in Administrative Templates and Settings Catalog apply to Windows Professional editions<!-- 13812105 -->
The [Windows Policy CSP settings](/windows/client-management/mdm/policy-configuration-service-provider) that begin with "ADMX_" apply to Windows devices running Windows Professional edition. Previously, these settings were shown as **Not applicable** on devices running Windows Professional edition.

You can use Administrative Templates and Settings Catalog to configure these "ADMX_" settings in a policy, and deploy the policy to your devices (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Settings catalog** or **Administrative Templates** or for profile type).

To use this set of "ADMX_" settings, the following updates must be installed on your Windows 10/11 devices:
- **Windows 11**: [March 28, 2022—KB5011563 (OS Build 22000.593) Preview](https://support.microsoft.com/topic/march-28-2022-kb5011563-os-build-22000-593-preview-40df54c9-b5a9-42e5-ae1c-9a33ff91ca91)

- **Windows 10** (20H1, 20H2, 21H1, 21H2): [March 22, 2022—KB5011543 (OS Builds 19042.1620, 19043.1620, and 19044.1620) Preview
](https://support.microsoft.com/topic/march-22-2022-kb5011543-os-builds-19042-1620-19043-1620-and-19044-1620-preview-4fe2d1c0-720f-47fe-9523-75339bc107a1)

To learn more about these features, go to:
-  [Use Windows 10/11 templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md)
- [Use the settings catalog to configure settings on Windows and macOS devices](../configuration/settings-catalog.md)
- [The latest in Group Policy settings parity in Mobile Device Management blog post](https://techcommunity.microsoft.com/t5/intune-customer-success/the-latest-in-group-policy-settings-parity-in-mobile-device/ba-p/2269167)

To see a list of all the ADMX settings that support Windows Professional edition, go to [Windows Policy CSP settings](/windows/client-management/mdm/policy-configuration-service-provider). Any setting that begins with "ADMX_" supports Windows Professional edition.

Applies to:
- Windows 11
- Windows 10

#### New macOS settings in Setting Catalog<!-- 13654614 -->
The Settings Catalog has new macOS settings you can configure (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type):

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

## Week of April, 11, 2022

### Device Management

#### Updating the device diagnostics folder structure<!-- 8637490 -->

Intune now exports [Windows Device Diagnostic data](../remote-actions/collect-diagnostics.md) in an updated format. With the updated format, the logs collected are named to match the data collected, and when multiple files are collected a folder is created. With the earlier format, the zip file used a flat structure of numbered folders that did not identify their contents.

To take advantage of this diagnostic logging update, devices must install one of the following updates:
- **Windows 11** - KB5011563
- **Windows 10** - KB5011543

These updates are available through the Windows Updates on April 12, 2022.

### App management

#### Uninstall DMG-type applications on managed macOS devices (Public preview)<!-- 13155022 -->
You can use the **Uninstall** assignment type to remove DMG-type applications on managed macOS devices from Microsoft Endpoint Manager. You can find macOS DMG apps in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **macOS** > **macOS app (.DMG)**. For related information, see [Add a macOS DMG app to Microsoft Intune](../apps/lob-apps-macos-dmg.md). 

## Week of April 4, 2022

### Device security

#### New profile templates and settings structure for endpoint security policies<!-- 13742640 -->

We’ve begun to release new [endpoint security profile templates](../protect/endpoint-security-policy.md) that use the settings format as found in the Settings Catalog. Each new profile template includes the same settings as the older profile it replaces, while bringing the following improvements:

- **Setting names match the Windows CSP name**: In most cases, each setting name in the new profiles is a match to the name of the CSP that the setting configures. However, in the Intune UI we’ve added spaces to that name to make the setting name easier to read. For example, a setting in the Intune UI that’s named *Allow USB Connection* configures the CSP named [AllowUSBConnection](/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowusbconnection).

- **Setting options align to those of the Windows CSP**: Options for settings now align directly to those options as described and supported by the Windows CSP, with one addition. The addition is that we’ve included the option of Not configured. When a setting is set to Not configured, that Intune profile does not actively manage that setting. When a profile is changed to go from active configuration of  setting Not configured, Intune stops actively enforcing the configuration for that setting on the device.

- **Setting guidance is taken from the Windows CSP**: The information about the setting found in the Intune UI is taken directly from the Windows CSP content, with Learn more links opening the documentation for the relevant CSP, or the content page that includes that CSP. The CSP defines and manages the settings behavior.

When a new platform and profile template is available for a policy type, the older profile of the same name will no longer be available to create new profiles. Instead, new profiles must use the new profiles and settings format. Eventually, your old profiles will be supported for conversion to the new profile format.  Until that conversion is available, you can still use, edit, and deploy your existing profiles.  

The following profile templates are now available in the new settings format:

| Policy type  | Platform  | Profile (template) name  |
|-----------------|-----------------|-----------------|
| Antivirus | Windows 10, Windows 11, and Windows Server | Windows Security experience |
| Antivirus | Windows 10, Windows 11, and Windows Server | Windows Defender Antivirus    |
| Antivirus | Windows 10, Windows 11, and Windows Server | Windows Defender Antivirus Exclusions
| Firewall | Windows 10, Windows 11, and Windows Server | Microsoft Defender Firewall |
| Firewall | Windows 10, Windows 11, and Windows Server | Microsoft Defender Firewall Rules |
| Endpoint detection and response | Windows 10, Windows 11, and Windows Server | Endpoint detection and response |
| Attack surface reduction | Windows 10 and Later | Attack surface reduction rules |
| Attack surface reduction | Windows 10 and Later | Exploit protection |

<!-- To learn more about this change, see the Device Management team blog at [](). -->

### Device management

#### Microsoft Endpoint Manager premium add-ons<!-- 12953253  -->

Microsoft Endpoint Manager is introducing a new centralized experience to help IT admins identify premium add-on capabilities. These capabilities can be added for an additional licensing cost available for Microsoft Endpoint Manager using Intune. The first premium add-on is Remote Help.

You can find premium add-ons in Intune under **Tenant administration** > **Premium add-ons**. The **Summary** blade shows all premium add-ons that have been released, a short description, and the status of the add-on. You can view the status of each add-on as either **Active** or **Available for trial or purchase**. The premium add-ons capability can be used by Global and Billing administrators to start trials or purchase licenses for premium add-ons.

For more information about Premium add-ons, see [Use Premium add-ons capabilities with Intune](../fundamentals/premium-add-ons.md).

## Week of March 28, 2022

### App management

#### Newly available protected app for Intune<!-- 13157367 -->
The following protected app is now available for Microsoft Intune:
- CAPTOR&trade; for Intune by Inkscreen LLC

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of March 21, 2022 (Service release 2203)

### App management

#### iOS/iPadOS notifications will require March Company Portal update<!-- 9819536 -->
If you are using a functionality that could generate iOS/iPadOS Company Portal push notifications, you will want to ensure your users update the iOS/iPadOS Company Portal in March or April 2022. There is no additional change in functionality. We will be making service side updates to iOS/iPadOS notifications expected in Intune's May (2205) service release. The Company Portal update will be released prior to the service change, so most users will likely have updated the app and will not be impacted. However, you may want to notify users of this change to ensure all users continue to receive push notifications sent by your organization. For related information, see [Update the Company Portal app](../user-help/install-a-new-version-of-the-company-portal-app.md).

#### Feedback settings for Company Portal and Microsoft Intune apps<!-- 10012370 -->
Feedback settings are provided to address M365 enterprise feedback policies for the currently logged in user via the [Microsoft 365 Apps admin center](https://config.office.com/). The settings are used to determine whether feedback can be enabled or must be disabled for a user. This feature is available for Intune Company Portal and Microsoft Intune apps. For more information, see [Configure feedback settings for Company Portal and Microsoft Intune apps](../apps/company-portal-app.md#configure-feedback-settings-for-company-portal-and-microsoft-intune-apps).

#### Deploy macOS LOB apps by uploading PKG-type installer files (Public preview)<!-- 13155147 -->
You can now upload and deploy PKG-type installer files as macOS line-of-business apps. You can add a macOS LOB app from [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **macOS** > **Add** > **Line-of-business app**. For more information about macOS LOB apps, see [How to add macOS line-of-business apps to Microsoft Intune](../apps/lob-apps-macos.md).

### Device management

#### See the IPv4 address and Wi-Fi subnet ID on Android Enterprise devices<!-- 12396463 -->
Customers can view the IPv4 address and Wi-Fi subnet ID reported for Android Enterprise corporate-owned fully managed, dedicated, and work profile devices. 

#### Android (AOSP) users can view all devices in Intune app<!-- 10454654 -->
AOSP device users can now view a list of their managed devices and device properties in the Microsoft Intune app. This feature is available on devices enrolled in Intune as user-associated (Android) AOSP devices.

#### Update eSim cellular data plan in bulk for iOS/iPadOS (public preview)<!-- 13139261a -->  
You can now perform a Bulk device action (**Devices** > **Bulk device action** > **Update cellular data**) to remotely activate or update the cellular data plan on iOS/iPadOS devices that support it. This feature is currently in public preview. For related information, see [Use bulk device actions](..\remote-actions\bulk-device-actions.md).

#### Preserve cellular data plan when bulk wiping iOS/iPadOS devices<!-- 13139261b --> 
When you perform a Bulk device action (**Devices** > **Bulk device action** > **Wipe**) to remotely wipe iOS/iPadOS devices from Intune, any cellular data plan on the device will be preserved. However, if you would like to have the devices' data plan removed, then you have the option to select a checkbox and remove the cellular data plan when wiping the devices. For related information, see [Use bulk device actions](..\remote-actions\bulk-device-actions.md).

#### Freeze the install of system updates for Android Enterprise corporate-owned devices<!-- 7912819  -->
For Android Enterprise corporate-owned devices that run version 9.0 and later, you can configure freeze periods during which no system or security updates can install.

To configure a freeze, use Intune device restriction profiles to set one or more blocks that can recur each year. Each block can be for up to 90 days, but you must have a minimum of 60 days between freeze periods, when system updates are allowed to install.

For information about configuring a freeze period, see **Freeze periods for system updates** in [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

For information about Android requirements for implementing a freeze, see [FreezePeriod](https://developers.google.com/android/management/reference/rest/v1/enterprises.policies#freezeperiod) in the Google developer documentation.

### Device security

#### Tenant attach: Antivirus profile<!-- 13425641 -->
The Endpoint Security Microsoft Defender Anti-virus profile is now generally available. For more information, see [Tenant attach: Create and deploy Antivirus policies from the admin center](../../configmgr/tenant-attach/endpoint-security-get-started.md).

### Monitor and troubleshoot

#### AppxPackaging event viewer is part of collect diagnostics<!-- 12809781 -->
 Intune's remote action to [Collect diagnostics](../remote-actions/collect-diagnostics.md) will collect additional details from Windows devices.  (**Devices** > **Windows** > *select a Windows device* > **Collect diagnostics**)
 
The new details include the **Microsoft-Windows-AppxPackaging/Operational** Event Viewer and the following office log files to assist in troubleshooting office installation issues:

`%windir%\temp\%computername%*.log`</br>
`%windir%\temp\officeclicktorun*.log`  

### Device enrollment

#### Utilize bootstrap tokens on enrolled macOS devices (public preview)<!-- 9539461 -->
Intune now supports the use of bootstrap tokens on enrolled devices running macOS, version 10.15 or later. Bootstrap tokens allow for non-admin users to have increased MDM permissions, and perform specific software functions on behalf of the IT admin.  Tokens are supported on:  

- Supervised devices (in Intune, that's all user-approved enrollments)  
- Devices enrolled in Intune via Apple automated device enrollment   

Bootstrap tokens will begin to function no sooner than March 26, 2022, and it could take longer before they begin to function in all tenants.

For more information about how bootstrap tokens work with Intune, see [Set up enrollment for macOS devices](../enrollment/macos-enroll.md).  

### Enroll macOS virtual machines running Apple silicon<!-- 13242738 -->
Use the Company Portal app for macOS to enroll virtual machines running on Apple silicon. Intune supports using macOS virtual machines for testing purposes only. For more information about enrolling virtual machines in Intune, see [Set up enrollment for macOS devices](../enrollment/macos-enroll.md).

### Device configuration

#### New reporting experience for device configuration profiles<!-- 8466004 -->
There is now a new reporting experience for device configuration profiles. This reporting experience excludes Windows administrative template (ADMX), Android Enterprise devices with OEMConfig, and Device Firmware Configuration Interface (DFCI) profile types. 

We are continuing to update Intune's report experience to enhance consistency, accuracy, organization, and data representation, which gives an overall "facelift" of Intune's per policy reporting. The new experience updates the per policy overview page to shift away from donut charts to a sleeker overview chart that quickly updates as devices/users check-in. 

There are three reports available from the per policy view:
- **Device and user check-in status** - This report combines information that was previously split into separate device status and user status reports. This report shows the list of device and user check-ins for the device configuration profile, with the check-in status and last check-in time. When you open the report, the aggregate chart will remain at the top of the page, and the data will be consistent with the list data. Use the filter column to view assignment filter options.
- **Device assignment status** - This report surfaces data on the latest status for assigned devices from the device configuration profile. Intune reporting will include pending state information.
- **Per setting status** - This report surfaces the summary of device and user check-ins that are in **Success**, **Conflict**, **Error** states at the granular setting level within the device configuration profile. This report leverages the same consistency and performance updates as well as navigation tools we’ve made available to other reports.

More drilldowns are available and additional assignment filters are supported for each report. For more information about each of these reports, see [Intune reports](../fundamentals/reports.md).

#### Google Chrome settings are in Settings Catalog and Administrative Templates<!-- 6198569 -->
Google Chrome settings are included in the Settings Catalog and Administrative Templates (ADMX). Previously, to configure Google Chrome settings on Windows devices, you created a custom OMA-URI device configuration policy.

For more information on these policy types, see:
- [Use the settings catalog to configure settings on Windows and macOS devices](../configuration/settings-catalog.md)
- [Use ADMX templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md)

Applies to:
- Windows 10/11

#### New macOS settings in the Settings Catalog<!-- 13111526 -->
The Settings Catalog has new macOS settings you can configure (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type):

**User Experience > Accessibility**:
- Close View Far Point
- Close View Hotkeys Enabled
- Close View Near Point
- Close View Scroll Wheel Toggle
- Close View Smooth Images
- Contrast
- Flash Screen
- Mouse Driver
- Mouse Driver Cursor Size
- Mouse Driver Ignore Trackpad
- Mouse Driver Initial Delay
- Mouse Driver Max Speed
- Slow Key
- Slow Key Beep On
- Slow Key Delay
- Stereo as Mono
- Sticky Key
- Sticky Key Beep On Modifier
- Sticky Key Show Window
- Voice Over On Off Key
- White On Black

**Air Play**:
- Allow List
- Password

**User Experience > Desktop**: 
-  Override Picture Path

**Preferences > Global Preferences**: 
- Auto Log Out Delay
- Multiple Session Enabled

**Printing > Printing**: 
- Require Admin To Print Locally

**Security > Security Preferences**: 
- Do Not Allow Firewall UI
- Do Not Allow Lock Message UI
- Do Not Allow Password Reset UI

**Preferences > System Preferences**:
- Disabled Preference Panes
- Enabled Preference Panes

**Preferences > User Preferences**: 
- Disable Using Cloud Password

The following settings are also in Settings Catalog. Previously, they were only available in Templates:

**Printing > Air Print**:
- IP Address
- Resource Path

**Networking > Firewall**:
- Allowed
- Bundle ID
- Block All Incoming
- Enable Firewall
- Enable Stealth Mode

**Login > Login Items**:
- Hide

**Login > Login Window Behavior**:
- Admin Host Info
- Allow List
- Deny List
- Disable Console Access
- Disable Screen Lock Immediate
- Hide Admin Users
- Hide Local Users
- Include Network User
- Log Out Disabled While Logged In
- Login Window Text
- Power Off Disabled While Logged In
- Restart Disabled
- Restart Disabled While Logged In
- Show Full Name
- Show Other Users Managed
- Shut Down Disabled
- Shut Down Disabled While Logged In
- Sleep Disabled

**System Policy > System Policy Control**:
- Allow Identified Developers
- Enable Assessment

**System Policy** > **System Policy Managed**:
- Disable Override

There isn't any conflict resolution between policies created using the Settings catalog and policies created using Templates. When creating new policies in the Settings Catalog, be sure there are no conflicting settings with your current policies.

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog in Microsoft Intune](../configuration/settings-catalog.md).

Applies to:
- macOS

### Role-based access control

#### Android (AOSP) will support scope tags and RBAC settings<!-- 8503981 -->
When you create a policy for Android (AOSP), you can use role-based access control (RBAC) and scope tags. 

For more information on these features, see:
- [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md)
- [Use RBAC and scope tags for distributed IT](scope-tags.md)

Applies to:
- Android Open Source Project (AOSP)

## Week of March 14, 2022

### App management

#### Apps UI when using Android 12L OS<!-- 12536901 -->
The Android 12L OS contains new features designed to improve the Android 12 experience on large and folding dual-screen devices. Intune apps now supports Android 12L OS on Android dual-screen devices.

#### Display Android Enterprise device serial number using Managed Home Screen app<!-- 11020860 -->
On Android Enterprise dedicated devices using Managed Home Screen, customers can now use app configuration to configure the Managed Home Screen app to show the serial number for the device on all supported OS versions (8 and above). For information related to the Managed Home Screen app, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

## Week of February 28, 2022

### Device configuration

#### Cellular data plan for Apple's Automated Device Enrollment<!-- 13729221 -->
As part of an iOS/iPadOS enrollment profile when configuring Automated Device Enrollment (ADE), you can now configure devices to activate cellular data. Configuring this option will send a command to activate cellular data plans for your organization's eSim-enabled cellular devices. Your carrier must provision activations for your devices before you can activate data plans using this command. This setting applies to devices running iOS/iPadOS 13.0 and later that are enrolling with ADE. For more information, see [Automatically enroll iOS/iPadOS devices by using Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

## Week of February 21, 2022 (Service release 2202)

### Device security

#### Mobile Threat Defense partner Zimperium is now available in GCC High tenants<!-- 10013537 -->
Zimperium is now available as a Mobile Threat Defense (MTD) partner in US GCC High environments.
 
With this support, you’ll find the Intune [connector for Zimperium](../protect/zimperium-mobile-threat-defense-connector.md) as available in the list of [MTD connectors that you can enable](../protect/mtd-connector-enable.md#to-enable-the-mobile-threat-defense-connector) in your GCC High tenant.
 
The GCC High environment is a more regulated environment, and only connectors for those MTD partners that are supported for the GCC High environment are available in it. For more information about support in GCC High tenants, [Microsoft Intune for US Government GCC High and DoD service description](/enterprise-mobility-security/solutions/ems-intune-govt-service-description).

#### Manage the app inventory data for iOS/iPadOS devices that Intune sends to third-party MTD partners<!-- 10722315 -->
You can now configure the type of application inventory data for personally owned iOS/iPadOS devices that Intune sends to your chosen third-party Mobile Threat Defense (MTD) partner.
 
To control the app inventory data, configure the following setting as part of the *MDM Compliance Policy Settings* on the [Mobile Threat Defense connector](../protect/mtd-connector-enable.md#to-enable-the-mobile-threat-defense-connector) for your partner:
 
- **Send full application inventory data on personally owned iOS/iPadOS Devices**
 
  Options for this setting include:
  - **On** - If your MTD partner syncs app data and requests a list of the iOS/iPadOS applications from Intune, that list includes unmanage apps (those not deployed through Intune) in addition to those deployed through Intune. This is the current behavior.
  - **Off** - Data about unmanaged apps won’t be provided, and the MTD partner only receives details about apps that were deployed through Intune.
 
For corporate devices, data about managed and unmanaged apps continues to be included with requests for app data by your MTD vendor.

### Device management

#### Support for Audio Alert on Android Dedicated (COSU) devices<!-- 10567852 -->
You can now use the **Play lost device sound** device action to trigger an alarm sound on the device to assist in locating the lost or stolen Android Enterprise dedicated device.
For more information, see [Locate lost or stolen devices](../remote-actions/device-locate.md).

#### UI updates when creating an on-demand VPN device configuration policy on iOS/iPadOS devices<!-- 13092960 -->
You can create an on-demand VPN connection for your iOS/iPadOS devices (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **VPN** for profile type > **Automatic VPN** > **On-demand VPN**).

The UI is updated to closer match Apple's technical naming. To see the on-demand VPN settings you can configure, go to [Automatic VPN settings on iOS and iPadOS devices](../configuration/vpn-settings-ios.md#automatic-vpn).

Applies to:
- iOS/iPadOS

#### On Android Enterprise, use the Connect Automatically setting on enterprise Wi-Fi profiles<!-- 10697036 -->
On Android Enterprise devices, you can create Wi-Fi profiles that include common enterprise Wi-Fi settings (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned work profile** > **Wi-Fi** for profile type > **Enterprise** for Wi-Fi type).

You can configure the **Connect automatically** setting that automatically connects to your Wi-Fi network when devices are in range.

To see the settings you can configure, go to [Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices](../configuration/wi-fi-settings-android-enterprise.md).

Applies to:
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)

#### Deprecated status in Group Policy Analytics migration readiness report automatically reevaluates your GPOs<!-- 7983435 -->
Using Group Policy Analytics, you can import your Group Policy Objects (GPOs) to see the settings that are supported in MDM providers, including Microsoft Intune. It also shows any deprecated settings, or settings not available to MDM providers.

The Intune product team updates the mapping logic. When the updates happen, the deprecated settings are automatically reevaluated. Previously, you had to reimport your GPOs.

For more information on Group Policy Analytics and the reporting, see [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Endpoint Manager](../configuration/group-policy-analytics.md).

Applies to:
- Windows 11
- Windows 10

#### Create terms of use for Android (AOSP) user-associated devices<!-- 8506575 -->
Require Android (AOSP) users to accept your terms and conditions in the Intune Company Portal app before they enroll their devices. This feature is available for corporate-owned, user-associated devices only. For more information about creating terms of use in Intune, see [Terms and conditions for user access](../enrollment/terms-and-conditions-create.md).

### Enforce Azure AD terms of use with Microsoft Intune or Microsoft Intune Enrollment cloud apps<!-- 12522105 -->
Use the Microsoft Intune cloud app and/or Microsoft Intune Enrollment cloud app to enforce a conditional access, Azure AD Terms of Use acceptance policy on iOS and iPadOS devices during automated device enrollment. This functionality is available when you select Setup Assistant with modern authentication as your authentication method.  Both cloud apps now ensure that users accept the terms of use during enrollment and/or during Company Portal sign-in if required by your conditional access policy.

#### New macOS settings in the Settings Catalog<!-- 12987685 -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. When you create a Settings Catalog policy, there are new settings available for macOS devices (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type).

New settings include:

- Domains > Email Domains

- Printing > Printing:
  - Allow Local Printers
  - Default Printer
    - Device URI
    - Display Name
  - Footer Font Name
  - Footer Font Size
  - Print Footer
  - Print MAC Address
  - Require Admin To Add Printers
  - Show Only Managed Printers
  - User Printer List
    - Device URI
    - Display Name
    - Location
    - Model
    - PPD URL
    - Printer Locked

- Profile Removal Password > Removal Password

- Global HTTP Proxy:
  - Proxy Captive Login Allowed
  - Proxy PAC Fallback Allowed
  - Proxy PAC URL
  - Proxy Password
  - Proxy Server
  - Proxy Server Port
  - Proxy Type
  - Proxy Username

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Monitor and troubleshoot

#### Remote help is moving in the Microsoft Endpoint Manager admin center<!-- 12868177 -->
The remote help page in the Microsoft Endpoint Manager admin center has moved and its now available directly under **Tenant administration** instead of **Connectors and tokens**. 
For more information about remote help, see [Use remote help](../remote-actions/remote-help.md).





## Week of February 7, 2022

### Device security

#### Microsoft Tunnel support for Red Hat Enterprise Linux 8.5<!-- 13182253  -->

You can now use Red Hat Enterprise Linux (RHEL) 8.5 with [Microsoft Tunnel](../protect/microsoft-tunnel-overview.md).

To support RHEL 8.5, we’ve also updated the [readiness tool](../protect/microsoft-tunnel-prerequisites.md#run-the-readiness-tool) (mst-readiness) with a new check for the presence of the ip_tables module in the Linux kernel. By default, RHEL 8.5 doesn’t load the ip_tables module.

For Linux servers that don't load the module, we've provided [instructions](../protect/microsoft-tunnel-prerequisites.md#manually-load-ip_tables) to load them immediately, and to configure the Linux server to automatically load them at boot.

### App management

#### Advanced logging setting in Company Portal app<!-- 12859998  -->
The **Enable Advanced Logging** setting is available in the Intune Company Portal app versions v5.2202 and higher for iOS/iPadOS and macOS. Device users can able to enable or disable advanced logging on a device. By turning on advanced logging, detailed log reports will be sent to Microsoft to troubleshoot issues. By default, the **Enable Advanced Logging** setting will be off. Device users should keep this setting off unless otherwise instructed by their organization's IT admin. For related information, see [Share Company Portal usage data with Microsoft](../user-help/turn-off-microsoft-usage-data-collection-ios.md) and [Manage Company Portal preferences for macOS](../user-help/intune-company-portal-preferences-macos.md).

## Week of January 31, 2022

### Device security

#### Public preview of Tunnel client functionality in Microsoft Defender for Endpoint app for iOS/iPadOS<!-- 9851681  -->

Microsoft Tunnel client functionality for iOS/iPadOS is migrating into the Microsoft Defender for Endpoint app. With this preview, you can start to use a preview version of Microsoft Defender for Endpoint as the Tunnel app for supported devices. The existing Tunnel client remains available, but will eventually be phased out in favor of the Defender for Endpoint app.

This public preview applies to:  

- iOS/iPadOS

For this preview, you download a preview version of Microsoft Defender for Endpoint from the Apple app store, and then migrate supported devices from the standalone Tunnel client app to the preview app. For details, see [Migrate to the Microsoft Defender for Endpoint app](../protect/microsoft-tunnel-migrate-app.md).

### Scripts/Developer

#### Intune Data Warehouse updates<!-- 9370034 -->
The  `applicationInventory` entity has been removed from the Intune Data Warehouse. A new dataset is now available in the UI and via Intune's export API. For more information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

## Week of January 24, 2022 (Service release 2201)

### App management

#### Deploy DMG-type applications to managed macOS devices<!-- 1171356 -->
You can upload and deploy DMG-type applications to managed Macs from Microsoft Endpoint Manager using the **required** assignment type. DMG is the file extension for Apple disk image files. DMG-type apps are deployed using the [Microsoft Intune MDM agent for macOS](..\apps\lob-apps-macos-agent.md). You can add a DMG app from [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **macOS** > **Add** > **macOS app (DMG)**.  For more information, see [Add a macOS DMG app to Microsoft Intune](../apps/lob-apps-macos-dmg.md).

### Device management

#### Choose either user or device scope when creating Windows VPN profiles<!-- 10685553 -->
You can create a VPN profile for Windows devices that configures VPN settings (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **VPN** for profile).

When you create a profile, use the **Use this VPN profile with a user/device scope** setting to apply the profile to the user scope or the device scope:
- **User scope**: The VPN profile is installed within the user's account on the device.
- **Device scope**: The VPN profile is installed in the device context and applies to all users on the device.

Existing VPN profiles will apply to their existing scope, and aren't impacted by this change. All VPN profiles are installed in the user scope *except* for the profiles with device tunnel enabled, which requires device scope.

For more information on VPN settings you can currently configure, see [Windows device settings to add VPN connections using Intune](../configuration/vpn-settings-windows-10.md).

Applies to:
- Windows 11
- Windows 10

#### Filters are Generally Available (GA)<!-- 12466893 -->
You can use filters to include or exclude devices in workload assignments (like policies and apps) based on different device properties. Filters is now generally available (GA).

For more information on filters, see [Use filters when assigning your apps, policies, and profiles](../fundamentals/filters.md).

#### Automatic device clean-up rules support for Android Enterprise devices<!-- 9797532 -->
Intune supports the creation of rules to automatically remove devices that appear to be inactive, stale, or unresponsive. You can now use these clean-up rules with Android Enterprise devices that previously did not support them. These rules are now supported for:
- Android Enterprise Fully Managed
- Android Enterprise Dedicated
- Android Enterprise Corporate-Owned with Work Profile

To learn more about clean-up rules, see [Automatically delete devices with cleanup rules](../remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules).

#### Use Collect diagnostics to collect additional details from Windows 365 devices through Intune remote actions<!-- 12636207 -->
Intune’s remote action to [*Collect diagnostics*](../remote-actions/collect-diagnostics.md) now collects additional details from Windows 365 (Coud-PC) devices. The new details for Windows 365 devices include the following registry data: 
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\AddIns\WebRTC Redirector 
- HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Teams\

For information about remote actions supported for Windows 365 devices, see [Remotely manage Windows 365 devices](/windows-365/enterprise/remotely-manage-cloud-pc).

#### Tenant attach features are Generally Available (GA)<!--12976713 -->
The following [tenant attach](../../configmgr/tenant-attach/index.yml) features are now generally available:
- Client details
- Applications
- Device timeline
- Resource explorer
- CMPivot
- Scripts
- BitLocker Recovery Keys
- Collections

### Device security

#### New Account protection policy to configure users in local groups on devices in public preview<!--5663034 -->
In public preview, you can use a new profile for Intune Account protection policies to manage the membership of the built-in local groups on Windows 10 and 11 devices. 

Each Windows device comes with a set of built-in local groups. Each local group contains a set of users that have rights within that group. With the new Local user group membership (preview) profile for endpoint security Account protection policies, you can manage which users are members of those local groups.  

To configure local group memberships, you select the built-in local account to modify and then choose the users to add, remove, or replace in the group with other users. Each device that receives the policy the updates the membership of those local groups. Modification of the group membership on each device is done by using the [Policy CSP - LocalUsersAndGroups](/windows/client-management/mdm/policy-csp-localusersandgroups?WT.mc_id=Portal-fx).

To learn more, see [Manage local groups on Windows devices](../protect/endpoint-security-account-protection-policy.md#manage-local-groups-on-windows-devices). 

## Week of January 3, 2022

### Device management
 
#### Preview filtered device list before deployment<!-- 7541587 -->
Now as you create or edit a filter in Microsoft Intune, you can preview the list of filtered devices. The new view eliminates the need to apply test filters, because you can immediately preview the impact a filter has on devices and adjust filter rules to achieve your desired outcome. For more information about using filters in Microsoft Intune, see [Create a filter](../fundamentals/filters.md).  

## Week of December 13, 2021 (Service release 2112)

### Device management

#### Launch Remote help from within the admin center<!-- 12773983 -->
You can now [launch remote help from within the Microsoft Endpoint Manager admin center](../remote-actions/remote-help.md#how-to-use-remote-help). To do so, in the admin center go to **All devices** and select the device on which assistance is needed. Then select **New remote help session**, which is available from the remote actions bar across the top of the devices view. 

#### Endpoint analytics filtering<!--7207888 -->
You can now [add filters](../../analytics/scores.md#filter-reports) to the tables in [Endpoint analytics](../../analytics/overview.md) reports. Using filters enables you to discover trends in your environment or spot potential issues.  

### Use filters to assign Endpoint analytics proactive remediations scripts in admin center - public preview<!-- 7566953 -->

In the Endpoint Manager admin center, you can create filters, and then use these filters when assigning apps and policies. You'll be able to use filters to assign the following policy:

* [Endpoint analytics proactive remediations Windows PowerShell scripts](../../analytics/proactive-remediations.md) (**Reports** > **Endpoint analytics** > **Proactive remediations**)   

For more information on filters, see [Use filters when assigning your apps, policies, and profiles](../fundamentals/filters.md).  

Applies to:

- Windows 11
- Windows 10

### Device configuration

#### New option to see the number of profiles with an error or conflict in device configuration profiles<!-- 9142810 -->
In the Endpoint Manager admin center, there's a new "X policies with error or conflict" option. When you select this option, you automatically go to the **Devices** > **Monitor** > **Assignment Failures** report. This report helps you troubleshoot errors and conflicts.

This new option is available in the following locations in the Endpoint Manager admin center:
- Home page
- Dashboard

For more information, see [Monitor device profiles in Microsoft Intune](../configuration/device-profile-monitor.md) and [Assignment failures report](reports.md#assignment-failures-report-operational).

Applies to:

- Windows 11
- Windows 10

#### New Timeout and Block iCloud Private Relay settings for iOS/iPadOS and macOS devices<!-- 10370284 -->
On iOS/iPadOS and macOS devices, you can create a device restrictions policy that manages features on the device (**Devices** > **Configuration Profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Device restrictions**).

There are new settings:
- iOS/iPadOS: 
  - **Block iCloud Private Relay**: On supervised devices, this setting prevents users from using the [iCloud Private Relay](https://support.apple.com/HT212614) (opens Apple's web site).
- macOS
  - **Block iCloud Private Relay**: On supervised devices, this setting prevents users from using the [iCloud Private Relay](https://support.apple.com/HT212614) (opens Apple's web site).
  - **Timeout**: Users can unlock their devices using a Touch ID, such as a fingerprint. Use this setting to require users to enter their password after a period of inactivity. The default inactivity period is 48 hours. After 48 hours of inactivity, the device prompts for the password, instead of Touch ID.

Applies to:
- iOS/iPadOS 15 and newer
- macOS 12 and newer

#### New device restrictions settings for Android Enterprise corporate-owned devices with a work profile<!-- 10982232 -->
On Android Enterprise devices, you can configure settings that control features on devices (**Devices** > **Configuration Profiles** > **Create profile** > **Android Enterprise** for platform > **Device restrictions** for profile type > **General**).

For Android Enterprise corporate-owned devices with a work profile, there are new settings:
- Search work contacts and display work contact caller-id in personal profile
- Copy and paste between work and personal profiles
- Data sharing between work and personal profiles

For more information on the settings you can currently configure, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android Enterprise corporate-owned work profile (COPE)

#### Settings Catalog is supported on U.S. Government GCC High and DoD<!-- 12389409 -->
Settings Catalog is available and supported on U.S. Government GCC High and DoD.

For more information on Settings Catalog, and what it is, see [Use the settings catalog to configure settings on Windows and macOS devices](../configuration/settings-catalog.md).

Applies to:

- macOS
- Windows 11
- Windows 10

#### Enter the certificate common name in Wi-Fi profiles for Android Enterprise fully managed, dedicated, and corporate-owned work profile devices<!-- 12439458 -->

On Android Enterprise devices, you can create a Wi-Fi profile that configures enterprise Wi-Fi settings (**Devices** > **Configuration Profiles** > **Create profile** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Wi-Fi** for profile type).

When you select **Enterprise**, there's a new **Radius server name** setting. This setting is the DNS name used in the certificate presented by the Radius Server during client authentication to the Wi-Fi access point. For example, enter `Contoso.com`, `uk.contoso.com`, or `jp.contoso.com`.

If you have multiple Radius servers with the same DNS suffix in their fully qualified domain name, then you can enter only the suffix. For example, you can enter `contoso.com`.

When you enter this value, user devices can bypass the dynamic trust dialog that's sometimes shown when connecting to the Wi-Fi network.

**What you need to know**:
- New Wi-Fi profiles targeting Android 11 or later may require this setting to be configured. Otherwise, the devices may not connect to your Wi-Fi network.

For more information on the settings you can currently configure, see [Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile Wi-Fi settings](../configuration/wi-fi-settings-android-enterprise.md#fully-managed-dedicated-and-corporate-owned-work-profile).

Applies to:
- Android Enterprise corporate-owned work profile (COPE)
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise dedicated devices (COSU)

#### New Administrative Templates settings for Microsoft Edge 96, 97, and Microsoft Edge updater on Windows devices<!-- 12442597 -->
In Intune, you can use Administrative Templates to configure Microsoft Edge settings (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Administrative Templates** for profile type).

There are new Administrative Templates settings for Microsoft Edge 96, 97, and the Microsoft  Edge updater, including **Target Channel override** support. Use **Target Channel override** so users get the **Extended Stable** release cycle option, which can be set using Group Policy or through Intune.

For related information, see:
- [Configure Microsoft Edge policy settings in Microsoft Intune](../configuration/administrative-templates-configure-edge.md)
- [Overview of the Microsoft Edge channels](/deployedge/microsoft-edge-channels)
- [Microsoft Edge Browser Policy Documentation](/deployedge/microsoft-edge-policies)

Applies to:

- Windows 11
- Windows 10
- Microsoft Edge

### Intune apps

#### Newly available protected apps for Intune<!-- 12425933 -->
The following protected app is now available for Microsoft Intune:

- Groupdolists by Centrallo LLC

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).  

#### BlackBerry – New mobile threat defense partner<!-- 7822722 -->
You can now use [BlackBerry Protect Mobile (powered by Cylance AI)](../protect/blackberry-mobile-threat-defense-connector.md) as an integrated mobile threat defense (MTD) partner with Intune. By connecting the BlackBerry Protect Mobile MTD connector in Intune, you can control mobile device access to corporate resources using conditional access that's based on risk assessment.

For more information, see: 
- [Mobile threat defense integration with Intune](../protect/mobile-threat-defense.md)  
- [BlackBerry UES documentation](https://docs.blackberry.com/en/unified-endpoint-security/blackberry-ues) 

## Week of December 6, 2021  

### Device enrollment

#### Apply device type filters to Windows and Apple enrollment restriction policies (preview)<!-- 9284419 -->  
Use the new assignment filters in **Enrollment Restrictions** to include or exclude devices based on device type. For example, you can allow personal devices, while also blocking devices running Windows 10 Home, by applying the **operatingsystemSKU** assignment filter. Filters can be applied to Windows, macOS, and iOS enrollment policies, with Android support coming at a later date. Filters also enable a new setup experience for enrollment restrictions. For more information about how to create filters, see [Create a filter](../fundamentals/filters.md). For more information about using filters with enrollment restrictions, see [Set enrollment restrictions](../enrollment/enrollment-restrictions-set.md). 

#### Use filters on Windows Enrollment Status Page profile assignments<!-- 7423484 -->
Filters allow you to include or exclude devices in policy or app assignments based on different device properties. When you create an Enrollment Status Page (ESP) profile, you'll be able to use filters when assigning the profile. The **All users** and **All devices** assignment options will also be available. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Enroll devices** > **Enrollment Status Page** > **Create**. For more information about filters, see [Use filters when assigning your apps, policies, and profiles](../fundamentals/filters.md). For more information about ESP profiles, see [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md). 

### App management

#### Additional Session PIN restrictions available for the Microsoft Managed Home Screen app<!-- 9843535 -->
The Managed Home Screen app for Android Enterprise now has the option to enforce additional restrictions on user's Session PINs. Specifically, Managed Home Screen now offers the following: 
- The ability to define a minimum length for Session PIN.
- The ability to define a maximum number of tries a user has to successfully enter their Session PIN before getting logged out from Managed Home Screen.
- The ability to define complexity values that restrict users from creating PINs with repeating (444) or ordered (123, 321, 246) patterns.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md) and [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

### Monitor and troubleshoot  

#### New event viewer for Windows 10 diagnostics<!-- 10741116 -->
We've added a new event viewer to Windows device diagnostics called *Microsoft-Windows-Windows Firewall with Advanced Security/Firewall*. The event viewer can assist you in troubleshooting issues with the firewall. For more information about Windows device diagnostics, see [Collect diagnostics from a Windows device](../remote-actions/collect-diagnostics.md).   

#### Device compliance status in Company Portal website<!-- 8782968 -->
End users can more easily see the compliance status of their devices from the Company Portal website. End users can navigate to the [Company Portal](https://portal.manage.microsoft.com/devices) website and select the **Devices** page to see device status. Devices will be listed with a status of **Can access company resources**, **Checking access**, or **Can't access company resources**. For related information, see [Manage apps from the Company Portal website](../user-help/manage-apps-cpweb.md) and [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

## Week of November 22, 2021  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### Monitor and troubleshoot

#### Remote help app is available as a public preview<!-- 9843480 -->

As a public preview, you can use of the remote help app with your Intune tenant. With remote help, users who authenticate to your Azure Active directly can remotely assist others by connecting a remote help session between devices.

With permissions in remote help managed by Intune role-based access controls, you control who has permissions to help others and the actions they can take while assisting. The capabilities of remote help include:

- **Enable remote help for your tenant** –If you choose to turn on remote help, its use is enabled tenant-wide.
- **Requires Organization login** - To use remote help, both the helper and the sharer must sign in with an Azure Active Directory (Azure AD) account from your organization.
- **Use remote help with unenrolled devices** – You can choose to allow help to devices that aren't enrolled with Intune.
- **Compliance Warnings** - Before connecting to device, a helper will see a non-compliance warning about that device if it’s not compliant to its assigned policies. This warning doesn’t block access but provides transparency about the risk of using sensitive data like administrative credentials during the session.
- **Role-based access control** – Admins can set RBAC rules that determine the scope of a helper’s access and what the actions they can take while providing assistance.
- **Elevation of privilege** - When needed, a helper with the correct RBAC permissions can interact with the UAC prompt on the sharer's machine to enter credentials.
- **Monitor active remote help sessions, and view details about past sessions** – In the Microsoft Endpoint Manager admin center you can view reports that include details about who helped who, on what device, and for how long. You’ll also find details about active sessions.

This feature is rolling out over the next week and should soon be available for your tenant. For more information, see [Use remote help](../remote-actions/remote-help.md).

## Week of November 15, 2021 (Service release 2111)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management  

#### Enable app update priority for Managed Google Play apps<!-- 7810180 -->
You can set the update priority of Managed Google Play apps on dedicated, fully managed, and corporate-owned with a work profile Android Enterprise devices. Select **High Priority** to update an app as soon as the developer has published the update, regardless of charge status, Wi-Fi capability, or end user activity on the device. For related information, see [Add Managed Google Play apps to Android Enterprise devices with Intune](..\apps\apps-add-android-for-work.md).

#### Clear app data between sessions for Android Enterprise dedicated devices enrolled with shared device mode (public preview)<!-- 8663319 -->
Using Intune, you can choose to clear app data for applications that have not integrated with Shared device mode to ensure user privacy between sign-in sessions. Users will be required to initiate a sign-out from an application that has integrated with Azure AD's Shared device mode in order for IT-specified apps to have their data cleared. This functionality will be available for Android Enterprise dedicated devices enrolled with shared device mode on Android 9 or later.

#### Export underlying discovered apps list data<!-- 9370255 -->
In addition to exporting the summarized discovered apps list data, you can export the more extensive underlying data. The current summarized export experience provides summarized aggregate data, however the additional new experience also provides the raw data. The raw data export will give you the entire dataset, which is used to create the summarized aggregate report. The raw data is a list of every device and each app discovered for that device. This functionality has been added to the Intune console to replace the Intune Data Warehouse Application Inventories dataset. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **Monitor** > **Discovered apps** > **Export** to display the export options. For related information, see [Intune discovered apps](../apps/app-discovered-apps.md) and [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

#### Filter improvements when displaying platform-specific app lists<!-- 10994275 -->
Filters have been improved when displaying platform-specific app lists in the Microsoft Endpoint Manager admin center. Previously, when navigating to a platform-specific app list, you could not use the **App type** filter on the list. With this change, you  can apply filters (including the **App Type** and **Assignment status** filters) on the platform-specific list of apps. For related information, see [Intune reports](../fundamentals/reports.md).

#### Newly available protected apps for Intune<!-- 11030094 -->
The following protected app is now available for Microsoft Intune:
- PenPoint by Pen-Link, Ltd.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

#### New RBAC permission for Win32 app supersedence and dependency relationships<!-- 11126374 -->
A new Microsoft Endpoint Manager permission has been added to create and edit Win32 app supersedence and dependency relationships with other apps. The permission is available under the **Mobile apps** category by selecting **Relate**. Starting in the **2202** service release, MEM admins will need this permission to add supersedence and dependency apps when creating or editing a Win32 app in Microsoft Endpoint Manager admin center. To find this permission in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Roles** > **All roles** > **Create**. This permission has been added to the following built-in roles:
- Application Manager
- School administrator

For related information, see [Create a custom role in Intune](..\fundamentals\create-custom-role.md).

#### Non-applicable status entries are no longer shown in the **Device Install Status** report<!-- 12419387 -->
Based on a selected app, the **Device Install Status** report provides a list of devices and status information for the selected app. App installation details related to the device includes **UPN**, **Platform**, **Version**, **Status**, **Status details**, and **Last check-in**. If the device's platform differs from the application's platform, rather than showing **Not Applicable** for the **Status details** of the entry, the entry will no longer be provided. For example, if an Android app has been select and the app is targeted to an iOS device, rather than providing a **Not Applicable** device status value, the device status for that entry will not be shown in the **Device Install Status** report.  To find this report, in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All Apps** > *Select an app* > **Device Install status**. For related information, see [Device Install Status report for apps (Operational)](../fundamentals/reports.md#device-install-status-report-for-apps-operational).

#### New ADMX settings for Edge 95 and Edge updater<!-- 12426698 -->
New ADMX settings for Edge 95 and Edge updater have been added to Administrative Templates. This includes support for "Target Channel override" which allows customers to opt into the **[Extended Stable](https://blogs.windows.com/msedgedev/2021/07/15/opt-in-extended-stable-release-cycle/)** release cycle option at any point using Group Policy or through Intune. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Configuration profiles** > **Create profile**. Then, select **Platform** > **Windows 10 and later** and **Profile** > **Templates** > **Administrative Templates**. For related information, see [Overview of the Microsoft Edge channels](/deployedge/microsoft-edge-channels), [Microsoft Edge Browser Policy Documentation](/deployedge/microsoft-edge-policies), and [Configure Microsoft Edge policy settings in Microsoft Intune](../configuration/administrative-templates-configure-edge.md).  

#### New privacy consent screen during Company Portal installation<!-- 6600502 -->  

We've added a new privacy consent screen to Company Portal for Android to meet privacy requirements for certain app stores, such as those in China. People installing Company Portal for the first time from those stores will see the new screen during installation. The screen explains what information Microsoft collects and how it's used. A person must agree to the terms before they can use the app. Users who installed Company Portal prior to this release will not see the new screen.  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Endpoint analytics per device scoring<!--8462182 -->
 [Per device scores](../../analytics/scores.md#bkmk_per-device) in [Endpoint analytics](../../analytics/overview.md) are now out of preview and generally available. Per device scores help you identify devices that could be impacting user experience. Reviewing scores per device may help you find and resolve end-user impacting issues before a call is made to the help desk.

#### Safeguard holds are now visible in the Feature update failures report<!-- 10948779 -->
When a device is blocked from installing a Windows update due to a [safeguard hold](/windows/deployment/update/safeguard-holds), you’ll now be able to view details about that hold in [Feature update failures report](../protect/windows-update-compliance-reports.md#use-the-feature-update-failures-operational-report) in the Microsoft Endpoint Manager admin center.

A device with a safeguard hold appears as a device with an error in the report. When you view details for such a device, the *Alert Message* column displays **Safeguard Hold**, and the *Deployment Error Code* column displays the ID of the safeguard hold.

Microsoft occasionally places safeguard holds to block installation of an update on a device when something detected on that device is known to result in a poor post-update experience. For example, software or drivers are common reasons to place a safeguard hold. The hold remains in place until the underlying issue is resolved, and the update is safe to install.

To learn more about active safeguard holds and expectations for their resolution, go to the Windows release health dashboard at [https://aka.ms/WindowsReleaseHealth](/windows/release-health/).  

#### Improvements for managing Windows Updates for pre-release builds<!-- 9231846 -->
We've improved the experience of using [Update rings for Windows 10 and later](../protect/windows-10-update-rings.md) to manage  Windows updates for pre-release builds. The improvements include the following: 
- We've added **Enable pre-release builds** as a new control in on the *Update ring settings* page for update rings. Use this setting to configure assigned devices to update to a pre-release build. You can select the following list of pre-release builds:
  - **Beta Channel**
  - **Dev Channel**
  - **Windows Insider - Release Preview**
  For more information about pre-release builds, see the [Windows Insider](https://insider.windows.com/understand-flighting) website.
- Devices assigned *Update rings for Windows 10 and later* policies will no longer have the *ManagePreviewBuilds* setting changed during Autopilot. When this setting changed during Autopilot, it forced an additional device reboot.

#### Use Update Rings for Windows 10 and later to upgrade to Windows 11<!-- 10753015 -->
We’ve added a [new setting](../protect/windows-update-settings.md#update-settings) to *Update Rings for Windows 10 and later* that you can use to upgrade eligible devices from Windows 10 to Windows 11, when you are ready to do so.
- **Upgrade Windows 10 devices to Latest Windows 11 release**
By default, this setting is set to No. When set to *Yes*, eligible Windows 10 devices that receive this policy will update to the latest build of Windows 11.

When set to *Yes*, Intune displays an information box that confirms that by deploying this setting you are accepting the Microsoft License Terms for devices that upgrade. The information box also contains a link to the [Microsoft License Terms](https://go.microsoft.com/fwlink/?linkid=2171206).

For more information about update rings, see [Update Rings for Windows 10 and later](../protect/windows-10-update-rings.md).

#### Disable Activation Lock remote device action for iOS/iPadOS has been removed from UI<!-- 10606548 -->
The remote device action to *Disable Activation Lock* is no longer available in Intune. You can bypass Activation Lock as detailed at [Disable Activation Lock on Supervised iOS/iPadOS devices with Intune](../remote-actions/device-activation-lock-disable.md).

This remote action is removed because the action to disable the [iOS/iPadOS Activation Lock](https://support.apple.com/en-us/HT201365) feature did not function as intended.

#### Updates for Security Baselines<!-- 9549108,  10873848 -->
We have a pair of updates for [security baselines​](../protect/security-baselines.md), which add the following settings:
- **Security baseline for Windows 10 and later** (Applies to Windows 10 and Windows 11) 
  The new baseline version is [November 2021](../protect/security-baseline-settings-mdm-all.md) and adds **Scan scripts that are used in Microsoft browsers** to the *Microsoft Defender* category. This baseline has no other changes.

- **Windows 365 Security Baseline (Preview)**
  The new baseline version is [Version 2110](../protect/security-baseline-settings-windows-365.md) and adds the following two settings, with no other changes:
  - **Scan scripts that are used in Microsoft browsers** is added to the *Microsoft Defender* category.
  - **Enable tamper protection to prevent Microsoft Defender being disabled** is added to *Windows Security*, which is a new category added with this baseline version.

Plan to [update your baselines](../protect/security-baselines-configure.md#change-the-baseline-version-for-a-profile) to the latest version. To understand what's changed between versions, see [Compare baseline versions](../protect/security-baselines.md#compare-baseline-versions) to learn how to export a .CSV file that shows the changes.

#### Use custom settings for Device Compliance for Windows 10/11 devices (public preview)<!-- 7536730 -->
As a public preview, device compliance policy for Windows 10 and Windows 11 devices supports the addition of custom settings to a device compliance policy. Results from custom settings appear in the Microsoft Endpoint Manager admin center along with other compliance policy details.

To use custom settings, you create and add the following to the admin center to power custom compliance settings:
- **JSON file** – The JSON file details the custom settings and their compliance values. The JSON also includes information you provide to your users on how to remediate the settings when noncompliant.
- **PowerShell script** – The PowerShell script will deploy to devices where it runs to determine the state of the settings defined in your JSON file, and reports them back to Intune.

With the JSON and script ready, you can then create a standard compliance policy that includes your custom settings. The option to include custom settings is found in a new compliance settings category named *Custom Compliance*.

To learn more, including examples for the .JSON and PowerShell script, see [Custom compliance settings](../protect/compliance-use-custom-settings.md).

#### New scheduling options for Feature updates for Windows 10 and later<!-- 6286037 -->
We’ve added a trio of *Rollout options* to support improved scheduling of when the updates from a policy for *Feature updates for Windows 10 and later* are made available for your devices to install. These new options include:
- **Make update available as soon as possible** - There is no delay in making the update available, which has been the previous behavior.
- **Make update available on a specific date** - With this option you then select the first day that this update will be offered by Windows Update to the devices that receive this policy.
- **Make update available gradually** - With this option Windows Update divides the devices that receive this policy into a number of groups that are calculated based on a start group time, end group time, and days to wait between groups. Windows update then offers the update to those groups one at a time, until the last group is offered the update. This process helps distribute the availability of the update across the time you’ve configured and can reduce the impact to your network when compared to offering the update to all devices at the same time.

For more information including details for gradual availability, see [Rollout options for Windows Updates](../protect/windows-update-rollout-options.md).

#### New details for Windows devices available in the Microsoft Endpoint Manager admin center<!-- 6208666 -->
The following details for Windows 10 and Windows 11 devices are now collected and can be viewed on a devices details pane of the Microsoft Endpoint Manager admin center: 
- System Management BIOS version
- TPM Manufacturer version
- TPM Manufacturer ID

These details are also included when you *Export* the details from the *All devices* pane.  

#### Settings for Shared iPad now generally available<!-- 10975827  -->  
Four Shared iPad settings are now out of preview and generally available to use when creating an Apple enrollment profile. These settings are applied during automated device enrollment (ADE).

For iPadOS 14.5 and later in Shared iPad mode:  
  - **Require Shared iPad temporary setting only**: Configures the device so that users only see the guest version of the sign-in experience, and must sign in as guest users. They can't sign in with a Managed Apple ID.
  - **Maximum seconds of inactivity until temporary session logs out**: If there isn't any activity after the specified time, the temporary session automatically signs out.
  - **Maximum seconds of inactivity until user session logs out**: If there isn't any activity after the specified time, the user session automatically signs out.  

For iPadOS 13.0 and later in Shared iPad mode:  
  - **Maximum seconds after screen lock before password is required for Shared iPad**: If the screen lock exceeds this amount of time, a device password will be required to unlock the device.

For more information about setting up devices in Shared iPad mode, see [Create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

#### Duplicate a settings catalog profile<!-- 9666635 -->      
Settings catalog profiles now support duplication. To create a copy of an existing profile, simply select **Duplicate**.  The copy contains the same setting configurations and scope tags as the original profile, but doesn't have any assignments attached to it. For more information about the settings catalog, see [Use the settings catalog to configure settings on Windows and macOS devices](../configuration/settings-catalog.md).

#### Work from anywhere report<!-- 7207657 -->
The **Work from anywhere** report has replaced the **Recommended software** report in [Endpoint analytics](../../analytics/overview.md). The **Work from anywhere** report contains metrics for Windows, cloud management, cloud identity, and cloud provisioning. For more information, see the [Work from anywhere report](../../analytics/work-from-anywhere.md) article.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### View BitLocker recovery keys for tenant attached devices<!-- 8509415 -->
You can now [view the BitLocker recovery key for tenant-attached devices](../protect/encrypt-devices.md#view-details-for-recovery-keys) in the Microsoft Endpoint Manager admin center. The recovery keys continue to be stored on-premises for tenant-attached devices, but the visibility in the admin center is intended to assist your Helpdesk scenarios from within the admin center. 

To view the keys, your Intune account must have the Intune RBAC permissions to view BitLocker keys, and must be associated with an on-premises user that has the related on-premises permissions in Configuration Manager of Collection Role, with the permission **Read BitLocker Recovery Key Permission**.

Users with the correct permissions can view keys by going to **Devices** > **Windows devices** > *select a device* > **Recovery keys**.

This capability is supported with Configuration Manager sites that run version 2107 or later. For sites that run version 2107, you’ll need to install an update rollup to support Azure AD joined devices. For more information, see [KB11121541](../../configmgr/hotfix/2107/11121541.md).

#### BitLocker settings added to settings catalog<!-- 10956191 -->  
We have added 9 [BitLocker settings that were previously only available in Group Policy (GP)](/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) to the Microsoft Intune settings catalog. To access the settings, go to **Devices** > **Configuration profiles** and create a settings catalog profile for devices running Windows 10 and later. Then search **BitLocker** in the settings catalog to view all settings related to BitLocker. For more information about the settings catalog, see [Create a policy using settings catalog](../configuration/settings-catalog.md). The added settings include:  

- **Provide the unique identifiers for your organization** 
- **Enforce drive encryption type on fixed data drives** 
- **Allow devices compliant with InstantGo or HSTI to opt out of preboot PIN** 
- **Allow enhanced PINs for startup** 
- **Disallow standard users from changing the PIN or password** 
- **Enable use of BitLocker authentication requiring preboot keyboard input on slates** 
- **Enforce drive encryption type on operating system drives** 
- **Control use of BitLocker on removable drives**
- **Enforce drive encryption type on removable data drives** 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### MDM support data to refresh automatically in Group Policy analytics tool<!-- 7852080 -->
Now whenever Microsoft makes changes to the mappings in Intune, the **MDM Support** column in the GP analytics tool automatically updates to reflect the changes. The automation is an improvement over the previous behavior, which required you to reimport your Group Policy object (GPO) to refresh the data. For more information about Group Policy analytics, see [Use Group Policy analytics](../configuration/group-policy-analytics.md).  

## Week of November 8, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### App management

#### Update Android Company Portal and Intune apps for custom notifications<!-- 12473860 -->
We have made service side updates to custom notifications for Intune's November (2111) service release, which requires users to have updated to recent versions of the Android Company Portal (version 5.0.5291.0, released in October 2021) or Android Intune app (version 2021.09.04, released in September 2021) for the best user experience. If users do not update prior to Intune's November (2111) service release and they are sent a custom notification, they will instead receive a notification telling them to update their app to view the notification. Once they update their app, they will see the message sent by your organization in the Notifications section in the app. For related information, see [Send custom notifications in Intune](../remote-actions/custom-notifications.md#receive-a-custom-notification).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### Device management

#### Locations deprecated for Android device administrator<!-- 9492223 -->

In October 2021, support for using locations in device compliance policy for devices enrolled as Android device administrator was deprecated. Use of locations is often referred to as network fencing.

For Android device administrator, the policies and dependences that relied on network fence capabilities no longer function. As previously announced, we are re-envisioning support for network fencing  and will share more information about those plans when it becomes available.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### Device security

#### Security Management with Defender for Endpoint (public preview)<!-- 5475445   -->

*This feature is in public preview and will roll out to tenants gradually over the next few weeks. You can confirm your tenant has received this capability when the relevant toggles show in both the Microsoft Endpoint Manager admin center and Microsoft Defender for Endpoint.*

*Security Management with Microsoft Defender for Endpoint* is a new configuration channel you use to manage the security configuration for Microsoft Defender for Endpoint (MDE) on devices that do not enroll into Microsoft Endpoint Manager. With this scenario, it’s Defender for Endpoint on a device that retrieves, enforces, and reports on the policies for MDE that you deploy from Microsoft Endpoint Manager. The devices are joined to your Azure AD and are also visible in the Microsoft Endpoint Manager admin center alongside other devices you manage with Intune and Configuration Manager.

For more information, see [Manage Microsoft Defender for Endpoint on devices with Microsoft Endpoint Manager](../protect/mde-security-integration.md).

## Week of October 25, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### Device security

#### MFA changes to Windows Autopilot enrollment flow<!-- 12376959 part 1 -->
To improve the baseline security for Azure Active Directory (Azure AD), we changed Azure AD behavior for multifactor authentication (MFA) during device registration. Previously, if a user completed MFA as part of their device registration, the MFA claim was carried over to the user state after registration was complete. Going forward, the MFA claim is not preserved after registration and users will be prompted to redo MFA for any apps that require MFA by policy. For more information, see [Windows Autopilot MFA changes to enrollment flow](https://techcommunity.microsoft.com/t5/intune-customer-success/windows-autopilot-mfa-changes-to-enrollment-flow/ba-p/2774687).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### User Assignment<!-- 12376959 part 2 -->
Last week we made a change to the authentication experience during user enrollment for Autopilot. This change impacts all Autopilot deployments where a user is assigned to a specific device prior to going through enrollment.

#### One-time self-deployment and pre-provisioning<!-- 12376959 part 3 -->
We made a change to the Windows Autopilot self-deployment mode and pre-provisioning mode experience, adding in a step to delete the device record as part of the device re-use process. This change impacts all Windows Autopilot deployments where the Autopilot profile is set to self-deployment or pre-provisioning mode. This change will only affect a device when it is re-used or when it is reset and attempts to redeploy. For more information, see [Updates to the Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/updates-to-the-windows-autopilot-sign-in-and-deployment/ba-p/2848452).  

### Device management

#### Introducing Microsoft Surface Management Portal in Microsoft Endpoint Manager<!--10874729 -->  
In light of our continued commitment to bring commercial customers the best possible experience, we partnered with teams across Microsoft to streamline Surface management into a single view within Microsoft Endpoint Manager. Whether you lead a large organization with thousands of devices or manage IT for a small-medium business, you can gain insights into the health of all your Surface devices and monitor device warranty and support requests in one location. Microsoft Surface management portal is available to U.S. customers now and will be rolling out globally later. For the latest information about Microsoft Surface and the new management portal, follow the [Surface IT Pro Blog](https://techcommunity.microsoft.com/t5/surface-it-pro-blog/bg-p/SurfaceITPro).  

## Week of October 18, 2021 (Service release 2110)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Manage iOS/iPadOS Universal Links using App Protection Policies<!-- 2850827 -->
You can configure both Managed Universal Links and Universal Link Exemptions for iOS/IPadOS apps via Application Protection Policy (APP) settings.  Managed Universal Links allows http/s links to open into the registered APP protected application instead of the protected browser.  Universal Link Exemptions allows http/s links to open into the registered unprotected application instead of the protected browser. For more information, see [Data Transfer](../apps/app-protection-policy-settings-ios.md#data-transfer) and [Universal Links](../apps/app-protection-policy-settings-ios.md#universal-links).

#### Newly available protected apps for Intune<!-- 10946933, 10952707, 10962244 -->
The following protected apps are now available for Microsoft Intune:

- Appian for Intune by Appian Corporation
- Space Connect by SpaceConnect Pty Ltd
- AssetScan For Intune by Align

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

#### Connected app support for Android personally owned and corporate-owned work profiles<!-- 9206112 -->
You can now allow users to turn on Connected apps experiences for supported apps. This app configuration setting enables users to connect the app information across the work and personal app instances. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Apps** > **App configuration policies** > **Add** > **Managed devices**. For more information, see [Add app configuration policies for managed Android Enterprise devices](../apps/app-configuration-policies-use-android.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management  

#### Block or allow personal apps for Android Enterprise corporate-owned work profile devices<!-- 8925033 -->
In device configuration, you can create a list of personal apps that will be blocked or allowed on the device. You can choose to leave the setting as not configured, or create a list of blocked or allowed apps in the personal profile. This setting is available in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Android** > **Configuration profiles** > **Create profile**. For information about Android Enterprise corporate-owned work profile device settings, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md#personal-profile).

#### New settings when configuring Kerberos single sign-on extension on iOS/iPadOS and macOS<!-- 10175092 -->
There are new device feature settings available when configuring the Kerberos SSO extension on iOS/iPadOS and macOS devices. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **iOS/iPadOS** or **macOS** > **Configuration profiles** > **Create profile** > select **Device features** for profile > **Single sign-on app extension** > **Kerberos** for SSO app extension type. For related information, see [iOS/iPadOS device feature settings](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) and [macOS device feature settings in Intune](../configuration/macos-device-features-settings.md#single-sign-on-app-extension).

### Four new shared iPad enrollment settings in public preview<!--9684925 -->
Four new shared iPad settings are available in Intune for public preview. These settings are applied at the time of automated device enrollment.  

For iPadOS 14.5 and later in Shared iPad mode:  
    - **Require Shared iPad temporary setting only**: Configures the device so that users only see the guest version of the sign-in experience, and must sign in as guest users. They can't sign in with a Managed Apple ID.
    - **Maximum seconds of inactivity until temporary session logs out**: If there isn't any activity after the specified time, the temporary session automatically signs out.
    - **Maximum seconds of inactivity until user session logs out**: If there isn't any activity after the specified time, the user session automatically signs out.  

For iPadOS 13.0 and later in Shared iPad mode:  
    - **Maximum seconds after screen lock before password is required for Shared iPad**: If the screen lock exceeds this amount of time, a device password will be required to unlock the device.

#### Introducing Android (AOSP) management for corporate devices (public preview)<!-- 8957094 -->  

Now in public preview, you can use Microsoft Intune to manage corporate-owned devices that run on the Android Open Source Project (AOSP) platform. Microsoft Intune currently supports the new *Android (AOSP)* management option for RealWear devices only. Management capabilities include:  

* Provision devices as user-associated devices or shared devices.  
* Deploy device configuration and compliance profiles.  

For more information about how to set up Android (AOSP) management, see [Enroll Android devices](../enrollment/android-enroll.md).  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Manage Windows 10 security updates for Windows 10 Enterprise multi-session VMs<!-- 8682461 -->
You can now use the [settings catalog](../configuration/settings-catalog.md) to manage Windows Update settings for quality (security) updates for Windows Enterprise [multi-session VMs](../fundamentals/azure-virtual-desktop-multi-session.md). To find the settings you can use with multi-session VMs in the settings catalog:

1. Create a device configuration policy for Windows 10 that uses the settings catalog, and configure [Settings filter](../fundamentals/azure-virtual-desktop-multi-session.md#to-configure-policies) for *Enterprise multi-session*.

2. Next, expand the *Windows Update for Business* category to select from the update settings that are available for multi-session VMs.

The settings include:

- **Active Hours End**  - See CSP: [Update/ActiveHoursEnd](/windows/client-management/mdm/policy-csp-Update#update-activehoursend)
- **Active Hours Max Range**- See CSP: [Update/ActiveHoursMaxRange](/windows/client-management/mdm/policy-csp-Update?#update-activehoursmaxrange)
- **Active Hours Start** - See CSP: [Update/ActiveHoursStart](/windows/client-management/mdm/policy-csp-Update#update-activehoursstart)
- **Block "Pause Updates" ability** - See CSP: [Update/SetDisablePauseUXAccess](/windows/client-management/mdm/policy-csp-Update#update-setdisablepauseuxaccess)
- **Configure Deadline Grace Period** - See CSP: [Update/ConfigureDeadlineGracePeriod](/windows/client-management/mdm/policy-csp-Update#update-configuredeadlinegraceperiod)
- **Defer Quality Updates Period (Days)** - See CSP: [Update/DeferQualityUpdatesPeriodInDays](/windows/client-management/mdm/policy-csp-Update#update-deferqualityupdatesperiodindays)
- **Pause Quality Updates Start Time** - See CSP: [Update/PauseQualityUpdatesStartTime](/windows/client-management/mdm/policy-csp-Update#update-pausequalityupdatesstarttime)
- **Quality Update Deadline Period (Days)** - See CSP: [Update/ConfigureDeadlineForQualityUpdates](/windows/client-management/mdm/policy-csp-Update?#update-configuredeadlineforqualityupdates)

<!-- ########################## -->
## Week of October 4, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Improved flow when saving logs in Android Company Portal app<!-- 10414688 -->
In the Android Company Portal app, when users download a copy of the Android Company Portal logs, they will now be able to choose which folder the logs will be saved in. To save Android Company Portal logs, users can select **Settings** > **Diagnostic logs** > **SAVE LOGS**.

#### Newly available protected apps for Intune<!-- 10489496, 10436733, 10494599, 10587268 -->
The following protected apps are now available for Microsoft Intune:

- iAnnotate for Intune/O365 by Branchfire, Inc.
- Dashflow for Intune by Intellect Automation International Pty Limited
- HowNow by Wonderush Limited

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Removal of Wi-Fi MAC address on specific Android Enterprise devices<!-- 11004658 -->
Intune will no longer display a Wi-Fi MAC address for newly enrolled personally owned work profile devices and devices managed with device administrator running Android 9 and above. Google is requiring all app updates to target [API 30 by November 2021](https://developer.android.com/distribute/play-policies#APILevel30). With this change, Android prevents apps from collecting the MAC address used by the device. For related information, see [Hardware device details](../remote-actions/device-inventory.md#hardware-device-details).

<!-- ########################## -->
#### Use Feature Updates to upgrade devices to Windows 11<!-- 10053623  -->

You can use *Feature updates for Windows 10 and later*
policy to upgrade devices that meet the Windows 11 minimum requirements to
Windows 11. It's as easy as configuring a new feature updates policy that
specifies the available Windows 11 version as the feature update you want to
deploy. 

For more information, see [Upgrade devices to Windows 11](../protect/windows-10-feature-updates.md#upgrade-devices-to-windows-11).

#### Windows 11 hardware readiness insights<!--9740163-->

The **Work from anywhere** report in [Endpoint analytics](../../analytics/overview.md) now provides [Windows 11 hardware readiness](../../analytics/work-from-anywhere.md#bkmk_windows11) insights. You can quickly determine how many of your enrolled devices meet the minimum system requirements for Windows 11 and which requirements are the top blockers within your organization. Drill in for a device-level view for Windows 11 hardware readiness status. For more information, see [Windows 11 hardware readiness](../../analytics/work-from-anywhere.md#bkmk_windows11).

## Week of September 27, 2021 (Service release 2109)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### New app categories available to better target app protection policies<!-- 4802581  -->

We have improved the UX of Microsoft Endpoint Manager by creating categories of apps that you can use to more easily and quickly target app protection policies. These categories are **All public apps**, **Microsoft apps**, and **Core Microsoft apps**. After you have created the targeted app protection policy, you can select **View a list of the apps that will be targeted** to view a list of the apps that will be affected by this policy. As new apps are supported, we will dynamically update these categories to include those apps as appropriate, and your policies will be automatically applied to all apps in your selected category. If needed, you can continue to target policies for individual apps as well. For more information, see [How to create and assign app protection policies](../apps/app-protection-policies.md) and [Create and deploy Windows Information Protection (WIP) policy with Intune](../apps/windows-information-protection-policy-create.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### New iOS device restriction settings for built-in apps, doc viewing<!--10119553 -->  

There are two new device restriction settings you can configure on iOS devices (**Devices** > **iOS/iPadOS** > **Configuration profiles** > **Create profile**  and select **Device restrictions** for profile) in Intune.  

- **Block Siri for translation** (Built-in Apps): Disables the connection to Siri servers so that users can't use Siri to translate text. Applies to iOS and iPadOS versions 15 and later.  
- **Allow copy/paste to be affected by managed open-in** (App Store, Doc Viewing, Gaming): Enforces copy/paste restrictions based on how you configured **Block viewing corporate documents in unmanaged apps**  and **Block viewing non-corporate documents in corporate apps**.  

For more information about iOS device restriction profiles in Intune, see [iOS and iPadOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-ios.md).

#### New macOS device restriction setting blocks users from erasing all content and settings on device<!--10131859 -->

There's a new macOS device restriction setting available (**Devices** > **macOS** > **Configuration profiles** > **Create profile** > and then select **Templates** > **Device restrictions** for profile) in Intune.  

 **Block users from erasing all content and settings on device** (General): Disables the reset option on supervised devices so that users can't reset their device to factory settings.  

For more information about macOS device restriction profiles in Intune, see [macOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-macos.md).  

Applies to:

- macOS version 12 and later

#### New software update restriction settings for macOS<!--10255184 -->

There are five new software update settings available when configuring a macOS device restriction profile (**Devices** > **macOS** > **Configuration profiles** > **Create profile** > and then select **Templates** > **Device restrictions** for profile) in Intune.  

- **Defer software updates** (General): Prevents users from seeing certain types of newly released updates until after a deferral period. Deferring software updates doesn't stop or change scheduled updates. Types of software updates you can defer include: **Major OS software updates**, **Minor OS software updates**, **Non-OS software updates**, or any combination of the three.
- **Delay default visibility of software updates** (General): Defers the default visibility of all software updates for up to 90 days.  After the deferral period, updates will become available to users. This value takes precedence over the default visibility value. Applies to macOS, version 10.13.4 and later.  
- **Delay visibility of major OS software updates** (General):  Delays visibility of major OS software updates for up to 90 days. After the deferral period, updates will become available to users. This value takes precedence over the default visibility value. Applies to macOS, version 11.3 and later.  
- **Delay visibility of minor OS software updates** (General): Delays visibility of minor OS software updates for up to 90 days. After the deferral period, updates will become available to users. This value takes precedence over the default visibility value. Applies to macOS, version 11.3 and later.  
- **Delay visibility of non OS software updates** (General): Delays visibility of non-OS software updates (such as Safari updates) for up to 90 days. After the deferral period, updates will become available to users. This value takes precedence over the default visibility value. Applies to macOS, version 11.0 and later.

For more information about macOS device restriction profiles in Intune, see [macOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-macos.md).  

#### New device restriction setting for Android Enterprise: Developer settings<!--10510385 -->

There is a new device restriction setting for Android Enterprise devices (**Devices** > **Android Enterprise** > **Configuration profiles** > **Create profile**  and select **Device restrictions** for profile) in Intune.  

- Developer settings: When set to **Allow**,  users can access the developer settings on their devices. By default, it's set to **Not configured**. Applies to fully managed, dedicated, and corporate-owned work profile devices.

For more information about Android Enterprise device restriction profiles, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

#### New device restrictions setting prevents sharing work profile contacts with paired Bluetooth devices<!-- 8630136 -->

A new device restrictions setting for corporate-owned work profile devices prevents users from sharing their work profile contacts with paired Bluetooth devices, such as cars or mobile devices.  To configure the setting, go to **Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Device restrictions** for profile.  

- Setting name:  **Contact sharing via Bluetooth (work profile-level)**
- Setting toggles:  
- **Block**: Blocks users from sharing work profile contacts via Bluetooth.
- **Not configured**:  Doesn't enforce any restrictions on the device, so users might be able to share their work profile contacts via Bluetooth.

### Device management

#### Intune now supports iOS/iPadOS 13 and higher<!-- 9964998 -->
Microsoft Intune, including the Intune Company Portal and Intune app protection policies now requires [iOS/iPadOS 13 and higher](../fundamentals/supported-devices-browsers.md).

#### Intune now supports macOS 10.15 and later<!-- 10154527 -->
Intune enrollment and the Company Portal now support [macOS 10.15 and later](../fundamentals/supported-devices-browsers.md). Older versions are not supported.

#### New Android device filtering options<!--7479654  -->

You can now choose the following Android enrollment types when filtering by **OS** in the **All devices** list in Intune:

- Android (personally owned work profile)
- Android (corporate-owned work profile)
- Android (fully managed)
- Android (dedicated)
- Android (device administrator)

In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **All devices** and view the **OS** column for specific Android enrollment types. For more information about Android enrollment types, see [Intune reports](../fundamentals/reports.md#all-devices-report-operational).

#### Settings catalog policies for policy sets<!-- 8683467  -->

In addition to profiles based on templates, you can add a profile based on the **Settings catalog** to your policy sets. The **Settings catalog** is a list of all the settings you can configure. To create a policy set in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Policy sets** > **Policy sets** > **Create**. For more information, see [Use policy sets to group collections of management objects](../fundamentals/policy-sets.md) and [Use the settings catalog to configure settings on Windows and macOS devices](../configuration/settings-catalog.md).

#### Configure Managed Home Screen sign-in settings for Android Enterprise dedicated devices<!-- 8684724  -->

You can now configure Managed Home Screen sign-in settings in device configuration when using Android Enterprise dedicated devices enrolled using Azure AD Shared device mode. You no longer need to use app configuration for these settings. For related information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Use Feature Updates to upgrade devices to Windows 11<!-- 10053623   -->

You can use *Feature updates for Windows 10 and later* policy to upgrade devices that meet the Windows 11 minimum requirements to Windows 11. It's as easy as configuring a new feature updates policy that specifies the available Windows 11 version as the feature update you want to deploy.

#### Use the Collect diagnostics remote action as a bulk device action for Windows devices<!-- 7554090    -->

We’ve added the **Collect diagnostics** [remote action](../remote-actions/collect-diagnostics.md#collect-diagnostics) as a *Bulk device action* that you can run for Windows devices.
As a [bulk device action](../remote-actions/bulk-device-actions.md) for Windows devices, use *Collect diagnostics* to collect Windows device logs from up to 25 devices at a time without interrupting device users.

#### Support for Locate device remote action on Android Enterprise dedicated devices<!--8589952  -->

You can use the **Locate device** remote action to get the current location of a lost or stolen Android Enterprise dedicated device that is online. If you attempt to locate a device that’s currently off-line, you’ll see its last known location instead, so long as that device was able to check in with Intune within the last seven days.

For more information, see [Locate lost or stolen devices](../remote-actions/device-locate.md).

#### Android Enterprise dedicated devices support the Rename remote action<!--8590028    -->

You can now use the *Rename* remote action on Android Enterprise dedicated devices. You can rename devices individually and in bulk. When using bulk Rename actions, the device name must include a variable that adds either a random number or the device's serial number.

For more information, see [Rename a device in Intune](../remote-actions/device-rename.md)

#### New Azure AD device ID and Intune device ID search parameters added<!--10510385 -->

When searching devices in **Devices** > **All devices**, you can now search by Azure AD device ID or Intune Device ID. For a list of available device details available in Intune, see [View device details with Microsoft Intune](../remote-actions/device-inventory.md).  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Tenant attach: Device status for endpoint security policies
<!--IN9264837 -->

You can review the status of endpoint security policies for tenant attached devices. The **Device Status** page can be accessed for all endpoint security policy types for tenant-attached clients. For more information, see [Device status](../../configmgr/tenant-attach/atp-onboard.md#device-status-preview) for the endpoint security policy types.

#### Attack surface reduction profiles for Configuration Manager tenant attach<!--7323386   -->

We’ve added two endpoint security profiles for *attack surface reduction* policy that you can use with devices you manage with [Configuration Manager tenant attach](../../configmgr/tenant-attach/deploy-asr-policy.md). These profiles are in preview and manage the same settings as the similarly  named profiles you use for devices managed by Intune. You'll find these new profiles when you configure attack surface reduction policy for the *Windows 10 and later (ConfigMgr)* platform.

The new profiles for tenant attach:

- **Exploit Protection(ConfigMgr)(preview)** - Exploit protection helps protect against malware that uses exploits to infect devices and spread. Exploit protection consists of a number of mitigations that can be applied to either the operating system or individual apps.
- **Web Protection (ConfigMgr)(preview)** - Web protection in Microsoft Defender for Endpoint uses network protection to secure your machines against web threats. Web protection stops web threats without a web proxy and can protect machines while they are away or on premises. Web protection stops access to phishing sites, malware vectors, exploit sites, untrusted or low-reputation sites, as well as sites that you have blocked in your custom indicator list.

#### Expanded support for Windows Defender Security Center  for tenant attach devices<!-- 7323443   -->

We’ve updated the *Windows Security experience (preview)* profile in endpoint security *Antivirus* policy to support additional settings for devices you manage with [Configuration Manager tenant attach](../../configmgr/tenant-attach/deploy-antivirus-policy.md). 

Previously, this profile was limited to Tamper Protection for your tenant attached devices. The updated profile now includes settings for the Windows Defender Security Center. You can [use these new settings](../protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md) to manage the same details for tenant attached devices that you already manage with the similarly named profile for Intune managed devices.

For more information about this profile, see [Endpoint security Antivirus policy](../protect/endpoint-security-antivirus-policy.md#devices-managed-by-configuration-manager).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Intune apps

#### Notifications from the iOS/iPadOS Company Portal app<!-- 10565849  -->

Notifications from the iOS/iPadOS Company Portal app are now delivered to devices using the default Apple sound, rather than being delivered silently. To turn the notification sound off from the iOS/iPadOS Company Portal app, select **Settings** > **Notifications** > **Comp Portal** and select the **Sound** toggle. For related information, see [Company Portal app notifications](../apps/company-portal-app.md#company-portal-app-notifications).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Organizational report focused on device configuration<!-- 8455708  --> 
We have released a new **Device configuration** organizational report. This report replaces the existing **Assignment status** report found in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) under **Devices** > **Monitor**. The **Device configuration** report allows you to generate a list of profiles in the tenant that have devices in a state of success, error, conflict, or not applicable. You can use filters for the profile type, OS, and state. The returned results will provide search, sort, filter, pagination, and export capabilities. In addition to device configuration details, this report provides resource access details, and new settings catalog profile details. For related information, see [Intune Reports](../fundamentals/reports.md).

#### Updated support experience in Microsoft Endpoint Manager admin center<!-- 8920053   -->

Available for Intune and co-management support flows, we’ve updated an improved [support experience](../../get-support.md#updated-support-experience) in the Microsoft Endpoint Manager admin center. The new experience guides you to issue-specific troubleshooting insights and web-based solutions, to get you a resolution faster.

To learn more about this change, see the [support blog post](https://aka.ms/EndpointManager-support-experience).

#### Safeguard holds are now visible in the Feature update failures report<!--10948779   -->

When a device is blocked from installing a Windows update due to a [safeguard hold](/windows/deployment/update/safeguard-holds), you’ll now be able to view details about that hold in [Feature update failures report](../protect/windows-update-compliance-reports.md#use-the-feature-update-failures-operational-report) in the Microsoft Endpoint Manager admin center.

A device with a safeguard hold appears as a device with an error in the report. When you view details for such a device, the *Alert Message* column displays **Safeguard Hold**, and the *Deployment Error Code* column displays the ID of the safeguard hold.

Microsoft occasionally places safeguard holds to block installation of an update on a device when something detected on that device is known to result in a poor post-update experience. For example, software or drivers are common reasons to place a safeguard hold. The hold remains in place until the underlying issue is resolved, and the update is safe to install.

To learn more about active safeguard holds and expectations for their resolution, go to the Windows release health dashboard at [https://aka.ms/WindowsReleaseHealth](/windows/release-health/).  

#### Update to the Assignment failures operational report<!-- 6473096  -->

[Security baselines](../protect/security-baselines.md) and endpoint security profiles have been added to the existing **Assignment failures** report. The profile types are differentiated using the **Policy type** column with the ability to filter. Role-based access control (RBAC) permissions have been applied to the report to filter on the set of policies that an admin can see. Those RBAC permissions include the Security Baseline permission, the Device Configuration permission, and the Device Compliance Policies permission. The report shows the number of devices in a state of error and conflict for a given profile, with the ability to drill down into a detailed list of those devices or users and further into the setting details. You can find the **Assignment failures** report in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Monitor**, or by selecting **Endpoint Security** > **Monitor**. For more information, see [Assignment failures report (Operational)](../fundamentals/reports.md#assignment-failures-report-operational).


<!-- ########################## -->
## Week of September 20, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Syncing the iOS/iPadOS/macOS Company Portal version<!-- 10535709 -->
The version of the iOS/iPadOS Company Portal and the macOS Company Portal are syncing to version 5.2019 for the next release. Going forward, the iOS/iPadOS and macOS Company Portal apps will have the same version number. For related information, see [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

<!-- ########################## -->
## Week of August 23, 2021 (Service release 2108)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Device filter evaluation reports now include filter results for assigned apps<!-- 9974516   -->

If you’re using filters for assigning apps as available, you can now use the filter evaluation report on a device to determine if an app has been made available for install. You can see this report per device, under **Devices > All Devices > select a device > Filter evaluation (preview)**.

- For more information on filters, see [Use filters when assigning your apps, policies, and profiles in Microsoft Endpoint Manager](filters.md).
- For more information on filter reports, see [Filter reports and troubleshooting in Microsoft Endpoint Manager](filters-reports-troubleshoot.md).

Applies to:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 11
- Windows 10

#### Additional Android SafetyNet evaluation type support for conditional launch policies<!-- 9076664  -->

Conditional launch now supports a sub-setting of **SafetyNet device attestation**. If  you select **SafetyNet device attestation** as required for conditional launch, you can specify that a specific SafetyNet evaluation type is used. This evaluation type is a hardware-backed key. The presence of a hardware-backed key as the evaluation type will indicate greater integrity of a device. Devices that do not support hardware-backed keys will be blocked by the MAM policy if they are targeted with this setting. For more information about SafetyNet evaluation and hardware-backed key support, see [Evaluation types](https://developer.android.com/training/safetynet/attestation#evaluation-types) in the Android developer documentation. For more information about Android conditional launch settings, see [Conditional launch](../apps/app-protection-policy-settings-android.md#conditional-launch).

#### Update to Outlook S/MIME settings for iOS and Android devices<!-- 7882166  -->

You can now enable Outlook S/MIME settings to always sign and/or always encrypt on iOS and Android devices when using the managed apps option. You can find this setting in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) when using managed apps by selecting **Apps** > **App configuration policies**.  In addition, you can add an LDAP (Lightweight Directory Access Protocol) URL for Outlook S/MIME on iOS and Android devices for both managed apps and managed devices. For related information, see [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md).

#### Scope tags for Managed Google Play apps<!-- 6114508  -->

Scope tags determine which objects an admin with specific rights can view in Intune. Most newly created items in Intune take on the scope tags of the creator. This is not the case for Managed Google Play Store apps. You can now optionally assign a scope tag to apply to all newly synced Managed Google Play apps on the **Managed Google Play connector** pane. The chosen scope tag will only apply to new Managed Google Play apps, not Managed Google Play apps that have already been approved in the tenant. For related information see [Add Managed Google Play apps to Android Enterprise devices with Intune](../apps/apps-add-android-for-work.md) and [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

#### Content of macOS LOB apps will be displayed in Intune<!-- 6991005  -->

Intune can now display the contents of macOS LOB apps (`.intunemac` files) in the console. You can review and edit the app detection details in the Intune console that are captured from the `.intunemac` file when adding a macOS LOB app. When uploading a PKG file, detection rules will be auto-created. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > **Add**. Continue by selecting the **Line-of-business** app type and the **App package file** containing the `.intunemac` file. For more information, see [How to add macOS line-of-business (LOB) apps to Microsoft Intune](../apps/lob-apps-macos.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Use filters on DFCI configuration profiles on Windows 10/11 devices<!-- 8817773 -->

In Endpoint Manager, you can create filters to target devices based on different properties. When you create a Device Firmware Configuration Interface (DFCI) profile, you'll be able to use filters when assigning the profile.

- For more information on filters, see [Use filters when assigning your apps, policies, and profiles](filters.md).
- For more information on the DFCI profile, see [Use Device Firmware Configuration Interface profiles on Windows devices](../configuration/device-firmware-configuration-interface-windows.md).

Applies to:

- Windows 11 on supported UEFI
- Windows 10 RS5 (1809) and newer on supported UEFI

#### New Deployment Channel setting for custom device configuration profiles on macOS devices<!--9683731 -->

When creating a custom device restriction policy for macOS devices, there is a new deployment channel setting available (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Templates** > **Custom** for profile).

Use the **Deployment channel** setting to deploy the configuration profile to the user channel or the device channel. If you send the profile to the wrong channel, then deployment can fail. For more information on using a payload in a device profile or a user profile, see [Profile-Specific Payload Keys](https://developer.apple.com/documentation/devicemanagement/profile-specific_payload_keys) (opens Apple developer website).

For more information about custom macOS profiles in Intune, see [Use custom settings for macOS devices](../configuration/custom-settings-macos.md).

Applies to:

- macOS

#### Use Wi-Fi networks set up using configuration profiles setting for iOS/iPadOS 14.5 devices and newer<!-- 9764167 -->

When creating a device restrictions policy for iOS/iPadOS devices, there's a new setting available (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile):

- **Require devices to use Wi-Fi networks set up via configuration profiles**: Set to **Yes** to require devices to only use Wi-Fi networks set up through configuration profiles.

To see the settings you can currently configure, go to [iOS and iPadOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-ios.md).

Applies to:

- iOS/iPadOS 14.5 and newer

#### New macOS device configuration profile settings, and change to iOS/iPadOS setting name<!-- 9772945  -->

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

#### More iOS/iPadOS home screen layout grid size options<!-- 9569886  -->

On iOS/iPadOS devices, you can configure the grid size on the home screen (**Devices** > **Device Configuration** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **Home screen layout**). For example, you can set the grid size to 4 columns x 5 rows.

The grid size will have more options:

- 4 columns x 5 rows
- 4 columns x 6 rows
- 5 columns x 6 rows

To see the home screen layout settings you can currently configure, go to [device settings to use common iOS/iPadOS features in Intune](../configuration/ios-device-features-settings.md#home-screen-layout).

Applies to:

- iOS/iPadOS

#### Add certificate server names to enterprise Wi-Fi profiles on Android Enterprise personally owned devices with a work profile<!-- 10285509 -->

On Android devices, you can use certificate-based authentication for Wi-Fi networks on personal devices with a work profile (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Personally owned work profile** > **Wi-Fi**).

When you use the **Enterprise** Wi-Fi type, and select the **EAP type**, there's a new **Certificate server names** setting. Use this setting to add a list of the certificate server domain names used by your certificate. For example, enter `srv.contoso.com`.

On Android 11 and newer devices, if you use the **Enterprise** Wi-Fi type, then you **must** add the certificate server names. If you don't add the certificate server names, users will have connection issues.

For more information on the Wi-Fi settings you can configure on Android Enterprise devices, see [Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices in Microsoft Intune](../configuration/wi-fi-settings-android-enterprise.md).

Applies to:

- Android Enterprise personally owned devices with work profile

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Modern authentication method with Apple Setup Assistant is out of preview for automated device enrollment<!--9579676 -->

The modern authentication method with Apple Setup Assistant is now out of preview and generally available for use for automated device enrollment.

For information on how to use this authentication method on iOS/iPadOS devices, see [Automatically enroll iOS/iPadOS devices by using Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

For information on how to use this authentication method on macOS devices, see [Automatically enroll macOS devices with the Apple Business Manager or Apple School Manager](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Endpoint analytics per device scoring<!--8462182 -->

To help you identify devices that could be impacting user experience, [Endpoint analytics](../../analytics/overview.md) shows some scores per device. Reviewing scores per device may help you find and resolve end-user impacting issues before a call is made to the help desk. You'll be able to display and sort by the Endpoint analytics, startup performance, and application reliability scores for each device. For more information, see [Per device scores](../../analytics/scores.md#bkmk_per-device).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Changes to settings in the settings catalog for Microsoft Defender for Endpoint on macOS<!--9817140  -->

We’ve added eight new settings to manage Microsoft Defender for Endpoint on macOS to the Intune [settings catalog](../configuration/settings-catalog.md). 

The new settings are found as follows under the following four categories in the settings catalog. For information about these settings, see [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences) in the *Microsoft Defender for Endpoint on Mac* documentation.

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


#### Confirm Tunnel Gateway servers can access your internal network from within the Microsoft Endpoint Manager admin center<!-- 9840576    -->

We've added the capability to the Microsoft Endpoint Manager admin center to confirm that your Tunnel Gateway servers can access your internal network, without someone having to access the servers directly. To enable this, you'll configure a new option called *URL for internal network access check* in the properties of each Tunnel Gateway site.

After adding a URL from your internal network to a Tunnel Gateway site, each server in that site periodically attempts to access it, and then reports on the result.

The status for this internal network access check is reported as *Internal network accessibility* on a server's [*Health check* tab](../protect/microsoft-tunnel-monitor.md#use-the-admin-center-ui). Status values for this check include:

- **Healthy** - The server can access the URL specified in the site properties.
- **Unhealthy** - The server can't access the URL specified in the site properties.
- **Unknown** - This status appears when you haven't set a URL in the site properties, and doesn't affect the overall status of the site.

Your servers will need to upgrade to the latest version of the Tunnel Gateway server software for this feature to work.

#### Compliance setting for SafetyNet hardware-backed key attestation for Android Enterprise personally owned work profile<!--8903071  -->

We’ve added a new device compliance setting for Android Enterprise personally owned work profile devices, [Required SafetyNet evaluation type](../protect/compliance-policy-create-android-for-work.md#google-play-protect---for-personally owned-work-profile). This new setting becomes available after you configure *SafetyNet device attestation* to either *Check basic integrity* or *Check basic integrity & certified devices*. The new setting:

**Required SafetyNet evaluation type**:

- **Not configured (defaults to basic evaluation)** – This is the setting default.
- **Hardware-backed key** – Require that hardware-backed key attestation is used for SafetyNet evaluation. Devices that don’t support hardware-backed key attestation are marked as not compliant.

For more information about SafetyNet and which devices support hardware-backed key attestation, see [Evaluation types](https://developer.android.com/training/safetynet/attestation#evaluation-types) in the SafetyNet documentation for Android.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Intune apps

#### Newly available protected app for Intune<!-- 10378153  -->

The following protected app is now available for Microsoft Intune:

- F2 Touch Intune by cBrain A/S

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Export GPO XML file size increased to 4 MB when using group policy analytics (preview) on Windows client devices<!-- 9560131 -->

In Microsoft Endpoint Manager, you can use group policy analytics to analyze your on-premises GPOs, and determine how your GPOs translate in the cloud. To use this feature, you export your GPO as an XML file. The XML file size has increased from 750 KB to 4 MB.

For more information on using group policy analytics, see [Analyze your on-premises group policy objects (GPO) using Group Policy analytics in Microsoft Endpoint Manager](../configuration/group-policy-analytics.md).

Applies to:
- Windows 11
- Windows 10

#### Device configuration reporting has been updated<!-- 10005568  -->

All device configuration and endpoint security profiles are now merged into one report. You can view all the policies applied to your device in the new single report that contains improved data. For instance, you can see the distinction of profile types in the new **Policy type** field. Also, selecting a policy will provide additional details about settings applied to the device and status of the device. Role-based access control (RBAC) permissions have been applied to filter the list of profiles based on your permissions. In Microsoft Endpoint Manger admin center, you will select **Devices** > **All devices** > *select a device* > **Device configuration** to see this report when it is available. For more information, see [Microsoft Intune reports](../fundamentals/reports.md).

#### New details for the Intune antivirus reports<!-- 8504648   -->

We've added two new columns of detail to both the [Windows 10 unhealthy endpoints](../protect/endpoint-security-antivirus-policy.md#unhealthy-endpoints) report and the [Antivirus agent status](../fundamentals/reports.md#antivirus-agent-status-report-organizational) report.

The new details include:

- **MDE Onboarding status** - (HealthState/OnboardingState) Identifies the presence of the Microsoft Defender for Endpoint agent on the device.
- **MDE Sense running state** - (HealthState/SenseIsRunning) Reports on the operational status of the Microsoft Defender for Endpoint health sensor on a device.

For more information about these settings, see [WindowsAdvancedThreatProtection CSP](/windows/client-management/mdm/windowsadvancedthreatprotection-csp).

#### Customize health status thresholds for Microsoft Tunnel Gateway servers<!--10464499  -->

You can now [customize the thresholds](../protect/microsoft-tunnel-monitor.md#manage-health-status-thresholds) that determine the health status for several metrics of Microsoft Tunnel Gateway.

Health status metrics have default values that determine whether the status reports as *healthy*,  *warning*, or *unhealthy*. When you customize a metric, you change the performance requirements for the metrics status. You can customize the following metrics:

- CPU usage
- Memory usage
- Disk space usage
- Latency

When you change a threshold value, the change applies to all Tunnel servers in your tenant. You can also select an option to reset all the metrics o their default value.

After you update the thresholds, the values in the *Health check* tab automatically update to reflect status based on the updated thresholds.

#### View health status trends for Microsoft Tunnel Gateway servers<!-- 10464520   -->  

You can [view health status trends](../protect/microsoft-tunnel-monitor.md#health-status-trends-for-tunnel-servers) for several Microsoft Tunnel Gateway health metrics in the form of a chart. The health status trend charts are available for individual servers you select from the *Health status* page.

The metrics that support trend charts include:

- Connections
- CPU usage
- Disk space usage
- Memory usage
- Average latency
- Throughput

<!-- ########################## -->
## Week of August 16, 2021

### App management

#### Intune Company Portal for macOS devices is now a universal app<!-- 10650481 -->
When you download Intune Company Portal for macOS devices version 2.18.2107 and later, it installs the new universal version of the app that runs natively on Apple Silicon Macs. The same app will install the x64 version of the app on Intel Mac machines. For related information, see [Add the Company Portal for macOS app](..\apps\apps-company-portal-macos.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### New version of the Certificate Connector for Microsoft Intune<!-- 10592539  -->

We’ve released a new version of the Certificate Connector for Microsoft Intune, version **6.2108.18.0**. This update includes:

- A fix to correctly display the current connector status in Microsoft Endpoint Manager admin center.
- A fix to correctly report on failures to deliver SCEP certificates.

For more information about the certificate connector, including a list of connector releases and updates, see [Certificate Connector for Microsoft Intune](../protect/certificate-connector-overview.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Adding Windows Hello for Business to Windows 10 Diagnostics<!-- 10184621  -->

We've added the information from the Operational Event Viewer for **Windows Hello for Business** to the data that’s collected for Windows 10 device diagnostics. See [Data collected](../remote-actions/collect-diagnostics.md#data-collected).

<!-- ########################## -->
## Week of August 2, 2021

### Windows 365 now generally available<!--10393594 -->

Windows 365 is a new service from Microsoft that automatically creates Cloud PCs for your end users. Cloud PCs are a new hybrid personal computing category that use the power of the cloud and the accessing device to provide a full and personalized Windows virtual machine. Admins can use Microsoft Endpoint Manager to define the configurations and applications that are provisioned for each user’s Cloud PC. End users can access their Cloud PC from any device and any location. Windows 365 stores the end user’s Cloud PC and data in the cloud, not on the device, providing a secure experience.

For more information about Windows 365, see [Windows 365](https://www.microsoft.com/windows-365?rtc=1).

For documentation on how to manage Windows 365 in your organization, see the [Windows 365 documentation](/windows-365/).

<!-- ########################## -->
## Week of July 26, 2021 (Service release 2107)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Improved policy support for iPadOS devices enrolled as Shared iPads for Business (public preview)<!-- 9779187   -->

We've added support for user-assigned device configuration policies for [Shared iPads for Business](../enrollment/device-enrollment-shared-ipad.md).

With this change, settings like the home screen layout and most device restrictions assigned to user groups apply to Shared iPad devices while a user from the assigned user groups is active on the device

#### Certificate Connector for Microsoft Intune combines separate certificate connectors<!-- 9843502  -->

We’ve released the [Certificate Connector for Microsoft Intune](../protect/certificate-connector-overview.md). This new connector replaces the use of separate certificate connectors for SCEP and PKCS, and includes the following features:

- Configure each instance of the connector to support one or more of the following capabilities:
  - SCEP
  - PKCS
  - PFX imported certificates
  - Certificate revocation
- Use a normal Active Directory account or the system account for the connector service.
- Based on your tenant location, select government vs. commercial environments.
- Removes the need to select a client certificate for SCEP integration with NDES.
- Auto-updates to the latest version of the connector. Manual update of this connector is also supported.
- Improved logging.

The previous connectors remain in support but are no longer available for download. If you need to install or reinstall a connector, install the new Certificate Connector for Microsoft Intune.

#### Windows Autopilot diagnostics page (public preview)

[Available settings](../enrollment/windows-enrollment-status.md) on the Enrollment Status Page are updated from **Allow users to collect logs about installation errors** to **Turn on log collection and diagnostics page for end users** to support the Windows Autopilot diagnostics page, available in Windows 11. For more information, see [Windows Autopilot: What's new](../../autopilot/windows-autopilot-whats-new.md#windows-autopilot-diagnostics-page). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Use filters to assign Windows client update rings in Endpoint Manager admin center - public preview<!-- 7423515   -->

In the Endpoint Manager admin center, you can create filters, and then use these filters when assigning apps and policies.

When assigning Windows client update ring policies, you can use filters (**Devices** > **Windows** > **Windows 10 Update Rings**). You can filter the devices that get the update rings policy based on a device property, such as the OS version, device manufacturer, and more. After you create the filter, use the filter when you assign the update rings policy.

- For more information on filters, see [Use filters when assigning your apps, policies, and profiles in Microsoft Endpoint Manager](filters.md).
- For more information on Windows 10 update rings policies, see [Windows 10 update rings policy in Intune](../protect/windows-10-update-rings.md).

Applies to:
- Windows 11
- Windows 10

#### Collect diagnostics remote action moved to general availability<!--10022807   -->

The **Collect diagnostics** remote action lets you collect diagnostics from corporate devices without interrupting or waiting for the end user. Collected diagnostics include MDM, Autopilot, event viewers, registry key, Configuration Manager client, networking, and other critical troubleshooting diagnostics. For more information see [Collect diagnostics from a Windows device](..\remote-actions\collect-diagnostics.md).

#### Autopilot support for Microsoft HoloLens is now generally available<!--9602654 -->

For more information, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Work from anywhere report<!-- 7207657  -->

[Endpoint analytics](../../analytics/overview.md) has a new report named **Work from anywhere**. The **Work from anywhere** report is an evolution of the **Recommended software** report. The new report contains metrics for Windows 10, cloud management, cloud identity, and cloud provisioning. For more information, see the [Work from anywhere report](../../analytics/work-from-anywhere.md) article.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Intune apps

#### Improvements to SSO app extension screen for Company Portal for macOS<!-- 9674212  -->

We've improved the Intune Company Portal authentication screen that prompts macOS users to log in to their account using single sign-on (SSO). Users can now:

- See the app that's requesting SSO.
- Select **Don't ask me again** to opt out of future SSO requests.
- Opt back in to SSO requests by going to Company Portal > **Preferences** and deselecting **Don't ask me to sign in with single sign-on for this account**.

#### Newly available protected apps for Intune<!-- 10078767, 10129082, 10172869  -->

The following protected apps are now available for Microsoft Intune:

- Webex for Intune by Cisco Systems, Inc.
- LumApps for Intune by LumApps
- ArchXtract (MDM) by CEGB CO., Ltd.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

<!-- ########################## -->
## Week of July 5, 2021

### Device security

#### Settings catalog support for Microsoft Defender for Endpoint on macOS<!-- 5520115 -->

We’ve added the settings to manage Microsoft Defender for Endpoint on macOS to the Intune [settings catalog](../configuration/settings-catalog.md) to configure Microsoft Defender for Endpoint on macOS.

The new settings can be found as follows under the following four categories in the settings catalog. For information about these settings, see [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences) in the *Microsoft Defender for Endpoint on Mac* documentation.

**Microsoft Defender - Antivirus engine**:  

- Allowed threats
- Enable passive mode
- Enable real-time protection
- Scan exclusions
- Threat type settings

**Microsoft Defender - Cloud delivered protection preferences**:  

- Diagnostic collection level
- Enable - disable automatic sample submissions
- Enable - disable cloud delivered protection

**Microsoft Defender - EDR preferences**:  

- Device tags
- Enable - disable early preview

**Microsoft Defender - User interface preferences**:

- Show - hide status menu icon

<!-- ########################## -->
## Week of June 28, 2021

### New iOS/iPadOS remote action lets you update the eSIM cellular plan  (public preview)<!--7119250 -->

The new **Update cellular data plan (preview)** action lets you remotely activate the eSIM cellular plan on iOS/iPadOS devices that support it. This feature is currently in public preview. For more information, see [Update cellular data plan](../remote-actions/update-cellular-data-plan.md).

<!-- ########################## -->
## Week of June 21, 2021 (Service release 2106)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Improvements for viewing managed apps status<!-- 9359228  -->

We've added some improvements to how [Intune displays status information about the managed apps](/troubleshoot/mem/intune/troubleshoot-app-install) that have deployed to users or devices.

Intune now displays only the apps that are specific to the platform of the device you’re viewing. We’ve also introduced performance enhancements and additional support for the Android and Windows platforms.

#### Updated default license type for Apple VPP apps<!-- 9914613  -->

When you create a new assignment for an Apple Volume Purchase Program (VPP) app, the default license type is now "device". Existing assignments remain unchanged. For more information about Apple VPP apps, see [How to manage iOS and macOS apps purchased through Apple Business Manager with Microsoft Intune](../apps/vpp-apps-ios.md).

#### Newly available protected apps for Intune<!-- 9766113, 9838907, 9916207, 9219639, 9779226, 9698578, 9731891, 9904508  -->

The following protected apps are now available for Microsoft Intune:

- Confidential File Viewer by Hitachi Solutions, Ltd.
- AventX Mobile Work Orders by STR Software
- Slack for Intune by Slack Technologies, Inc.
- Dynamics 365 Sales by Microsoft
- Leap Work for Intune by LeapXpert Limited
- iManage Work 10 For Intune by iManage, LLC
- Microsoft Whiteboard by Microsoft (Android version)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Manage cookies and cross site tracking in Safari on iOS/iPadOS devices<!-- 9771966  -->

When creating a device restriction policy for iOS/iPadOS devices, you can manage cookies in the Safari app (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile > **Built-in Apps**).

The **Safari cookies** setting is updated to help manage cookies and cross site tracking. For more information on this setting, see [Built-in Apps for iOS/iPadOS devices](../configuration/device-restrictions-ios.md#built-in-apps).

Applies to:

- iOS/iPadOS versions 4 and newer

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Browser access automatically enabled during corporate Android enrollment<!--6613616  -->

Browser access is now automatically turned on during new enrollments of the following devices:

- Android Enterprise dedicated devices enrolled with Azure AD Shared device mode
- Android Enterprise fully managed devices
- Android Enterprise corporate-owned work profile devices

Compliant devices can use the browser to access resources protected by conditional access.

This change has no impact on devices that are already enrolled.

#### Intune support for Android Enterprise corporate-owned devices with a work profile<!--9606159 -->

Intune support for Android Enterprise corporate-owned devices with a work profile is now generally available. For more information, see [Announcing general availability of Android Enterprise corporate-owned devices with a work profile](https://aka.ms/COPEGA)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Use filters on Settings Catalog configuration profiles, and Risk Score and Threat Level compliance policy settings<!-- 10023995 7556913   -->

When you use [filters](filters.md) to assign your policies, you can:

- Use filters on compliance policies that use the **Risk Score** and **Threat Level** settings.
- Use filters on configuration profiles that use the **Settings Catalog** profile type.

For more information on what you can do, see [List of platforms, policies, and app types supported by filters](filters-supported-workloads.md).

Applies to:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 11
- Windows 10

#### Use the EnrollmentProfileName property when creating a filter for Android Enterprise<!-- 10022750   -->

In Endpoint Manager, you can create [filters](filters.md) to target devices based on different properties, including device name, manufacturer, and more. On iOS/iPadOS and Windows 10/11 devices, you can create a filter using the enrollment profile name. The enrollment profile name property is available for Android Enterprise devices.

To see the filter properties you can configure, go to [Device properties, operators, and rule editing when creating filters](filters-device-properties.md).

Applies to:

- Android Enterprise

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Export option for Proactive remediations<!-- 10198545 -->

[Proactive remediations](../../analytics/proactive-remediations.md) are script packages that can detect and fix common support issues on a user's device before they even realize there's a problem. To help you easily analyze returned outputs, an **Export** option was added that allows you to save the output as a `.csv` file. For more information, see [Proactive remediations](../../analytics/proactive-remediations.md).

#### Updated certificates report<!-- 10034112  -->

The **Certificates** report, which shows the current device certificates in use, has been updated to include better capabilities to search, page, sort, and export the report. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Monitor** > **Certificates**. For more information about reports in Intune, see [Intune reports](../fundamentals/reports.md).

<!-- ########################## -->

## Week of June 14, 2021  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Microsoft Defender for Endpoint for Microsoft Tunnel on Android is out of preview<!-- 9370486 -->

The Microsoft Defender for Endpoint app that supports Microsoft Tunnel functionality on Android is now out of preview and [generally available for use](../protect/microsoft-tunnel-overview.md). With this change:

- You no longer need to opt in to use Defender of Endpoint as the tunnel app on Android.
- The standalone app for Android is now deprecated and will be removed from the Google app store when support ends on January 31, 2022.

Plan to download and use the updated Microsoft Defender for Endpoint app for Microsoft Tunnel app for Android. If you participated in the preview, update your devices with the new version of Defender for Endpoint from the Google Play store. If you are still using the standalone tunnel app, plan to [migrate to the Microsoft Defender for Endpoint app](../protect/microsoft-tunnel-migrate-app.md) before support for the standalone app ends.

The standalone tunnel app for iOS remains in preview.  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

### Tenant attach: Offboarding<!-- CMADO7043245 INADO9412904 -->

While we know customers get enormous value by enabling tenant attach, there are rare cases where you might need to offboard a hierarchy. For example, you may need to offboard following a disaster recovery scenario where the on-premises environment was removed. To remove your Configuration Manager hierarchy from the Microsoft Endpoint Manager admin center, select **Tenant administration**, **Connectors and tokens** then **Microsoft Endpoint Configuration Manager**. Choose the name of the site you would like to offboard, then select **Delete**. For more information, see [Enable tenant attach](../../configmgr/tenant-attach/device-sync-actions.md#bkmk_offboard).

<!-- ########################## -->
## Week of June 7, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Android Company Portal app and Intune app now include Portugal Portuguese support<!-- 9707888, 9707936 -->

The Android Company Portal app and the Android Intune app now support Portuguese from Portugal (language code pt-PT). Intune already supports Portuguese from Brazil.

<!-- ########################## -->
## Week of May 24, 2021 (Service release 2105)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### New Microsoft Tunnel Gateway version<!--10145583-->

We’ve released a [new version](../protect/microsoft-tunnel-upgrade.md#microsoft-tunnel-update-history) of the Microsoft Tunnel Gateway. It includes the following changes:

- Minor bug fixes.
- Image updates with security updates for all dependencies.

For sites that are configured to update automatically, the Tunnel Gateway server will automatically update to the new version. For sites that are configured to update manually, you'll need to approve the update.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### New tiles provided app install failure count<!-- 6381269  -->

The **Home**, **Dashboard**, and **Apps Overview** panes now provide updated tiles to show the number of app installation failures for the tenant. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Home** to view the Home pane, or **Dashboard** to view the Dashboard pane. Select **Apps** > **Overview** to view the **Apps Overview** pane. For related information, see [Intune reports](../fundamentals/reports.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Per setting status report in Settings Catalog<!-- 9061277  -->

When you create a **Settings Catalog** profile, you can see how many devices are in each state, including success, conflict, and error (**Devices** > **Configuration profiles** > select the policy). This report includes a **Per setting status** that:

- Shows the total number of devices impacted by a specific setting.
- Has controls to search, sort, filter, export, and go to the next/previous pages.

For more information on the settings catalog, see [Use the settings catalog to configure settings on Windows and macOS devices](../configuration/settings-catalog.md).

#### New settings for iOS/iPadOS 14.5 devices and newer<!-- 9428309   -->

When creating a device restrictions policy for iOS/iPadOS devices, there are new settings available (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile):

- **Block Apple Watch auto unlock**: Set to **Yes** to block users from unlocking their device with Apple Watch.
- **Allow users to boot devices into recovery mode with unpaired devices**: Set to **Yes** to allow users to boot their device into recovery with an unpaired device.
- **Block Siri for dictation**: Set to **Yes** to disable connections to Siri servers so that users can't use Siri to dictate text.

To see these settings, go to [iOS and iPadOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-ios.md).

Applies to:

- iOS/iPadOS 14.5 and newer

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Support has ended for Restart remote action on Android Enterprise corporate-owned devices with a work profile<!--9584646   -->

Support has ended for the **Restart** remote action on corporate-owned devices with a work profile. The **Restart** button has been removed from the **Device** page for corporate-owned devices with a work profile. If you try to restart devices using bulk device actions, the corporate-owned work profile devices won't restart and those device actions will be marked report as **Not supported**. Other device types that are included in the bulk device action will restart as normal for that action.

### Windows 10/11 Enterprise multi-session support (public preview)<!--8666391  -->

Windows 10/11 Enterprise multi-session is a new Remote Desktop Session Host exclusive to [Azure Virtual Desktop](/azure/virtual-desktop/) on Azure which allows multiple concurrent user sessions. This gives users a familiar Windows client experience while IT can benefit from the cost advantages of multi-session and use existing per-user Microsoft 365 licensing.

Microsoft Intune lets you manage multi-session remote desktops with device-based configurations like a shared, user-less Windows client. You can now enroll Hybrid Azure AD joined VMs in Intune automatically and target with OS scope policies and apps.

You can:

- Host multiple concurrent user sessions using the Windows 10/11 Enterprise multi-session SKU exclusive to Azure Virtual Desktop on Azure.
- Manage multi-session remote desktops with device-based configurations like a shared, user-less Windows 10/11 Enterprise client.
- Automatically enroll Hybrid Azure AD joined virtual machines in Intune and target them with device scope policies and apps.

For more information, see [Windows 10/11 Enterprise multi-session remote desktops](azure-virtual-desktop-multi-session.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Conditional access on Jamf-managed macOS devices for Government Cloud now available<!--9081124 -->

You can now use Intune's compliance engine to evaluate Jamf-managed macOS devices for Government Cloud. To do so, activate the compliance connector for Jamf. For more information, see [Integrate Jamf Pro with Intune for compliance](../protect/conditional-access-integrate-jamf.md).

#### Changes for the Microsoft Tunnel Gateway<!--6305140     -->

We have a pair of updates to announce for the Microsoft Tunnel Gateway this month:

- **Microsoft Tunnel Gateway is now generally available**  
  With this service release, [Microsoft Tunnel Gateway](../protect/microsoft-tunnel-overview.md) is now out of preview, and generally available. While the Microsoft Tunnel Gateway server component is out of preview, the following Microsoft Tunnel client apps remain in preview:

  - Microsoft Tunnel standalone app for Android
  - Microsoft Tunnel standalone app for iOS
  - Microsoft Defender for Endpoint with support for Microsoft Tunnel for Android

- **Custom setting support in VPN profiles for Microsoft Tunnel for Microsoft Defender for Endpoint for Android**

  When you use the Microsoft Defender for Endpoint as your Microsoft Tunnel client app for Android and as a mobile threat defense (MTD) app, you can now use [custom settings](../protect/microsoft-tunnel-configure.md#use-custom-settings-for-microsoft-defender-for-endpoint) in the VPN Profile for Microsoft Tunnel to configure Microsoft Defender for Endpoint.

  In this scenario, using custom settings to configure Microsoft Defender for Endpoint in the VPN profile removes the need to deploy a separate app configuration profile for Microsoft Defender for Endpoint.

  For the following platforms, you can choose to use either the custom settings in the VPN profile or to use a separate app configuration profile for Microsoft Defender for Endpoint:

  - Android Enterprise Fully Managed
  - Android Enterprise Corporate-Owned Work Profile

  However, for an Android Enterprise Personally Owned Work profile, use *only* the VPN profile with custom settings. Personally Owned Work Profile devices that receive a separate app configuration profile for Microsoft Defender for Endpoint in addition to a Microsoft Tunnel VPN profile may be unable to connect to the Microsoft Tunnel.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### New operational report providing app install status<!-- 6381268  -->

The new **App Install Status** report provides a list of apps with versions and installation details. App installation details are included as separate columns in the list. Additionally, the installation details provide the app install and failure totals for devices and users. You have the ability to sort and search this report as well. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **Monitor** > **App Install Status**. For more information about reports in Intune, see [Intune reports](../fundamentals/reports.md).

#### New operational report providing app install status based on device<!-- 6381269  -->

Based on a selected app, the new **Device Install Status** report provides a list of devices and status information related to the specific app. App installation details related to the device includes **UPN**, **Platform**, **Version**, **Status**, **Status details**, and **Last check-in**. You have the ability to sort, filter, and search this report as well. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All Apps** > *Select an app* > **Device Install status**. For more information about reports in Intune, see [Intune reports](../fundamentals/reports.md).

#### New operational report providing app install status based on user<!-- 6381273  -->

Based on a selected app, the new **User Install Status** report provides a list of users and status information related to the specific app. App installation details related to the user include **Name**, **UPN**, **Failures**, **Installs**, **Pending**, **Not Installed**, and **Not Applicable**. You have the ability to sort, filter, and search this report as well. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > *Select an app* > **User Install Status**. For more information about reports in Intune, see [Intune reports](../fundamentals/reports.md).

#### Export Intune reports using Graph API v1.0 or beta<!-- 8090911  -->

Intune reporting export API now is available in Graph v1.0, and continues to be available in Graph beta. For related information, see [Intune reports](../fundamentals/reports.md) and [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Scripts

#### New property value supported for Android Open Source Project devices<!-- 9749555  -->

The `IntuneAosp` property value is now supported in the `managementAgentType` enum. The `ManagementAgentTypeID` value for this property is `2048`.  It represents the device type that is managed by Intune's MDM for AOSP (Android Open Source Project) devices. For related information, see [managementAgentType](../developer/reports-ref-devices.md#managementagenttypes) in the beta section of the Intune Data Warehouse API.

<!-- ########################## -->
## Week of May 10, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Improved Conditional Access messaging for Android and iOS/iPadOS users<!-- 9908622 -->

Azure Active Directory has updated the wording on a Conditional Access screen to better explain access and setup requirements to users. Android and iOS/iPadOS users will see this screen when they try to access corporate resources from a device that's not enrolled in Intune management. For more information about this change, see [What's new in Azure Active Directory](/azure/active-directory/fundamentals/whats-new#improved-conditional-access-messaging-for-android-and-ios).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Windows Security experience profiles support tri-state settings<!-- 9741752  -->

For Windows 10 devices, we’ve updated the bi-state settings to be tri-state settings in the [Windows Security experience profile](../protect/antivirus-security-experience-windows-settings.md) for Endpoint security Antivirus policy.

Most settings in the profile previously supported only two options of **Yes** and **Not configured**.  Moving forward, those same settings now include **Yes**, **Not configured**, and a new option of **No**.

- For existing profiles, settings that are set to *Not configured* remain as *Not configured*. When you create new profiles or edit an existing profile, you can now choose to explicitly specify *No*.

In addition, the following applies to configuration of the *Hide the Virus and threat protection area in the Windows Security app* setting and its child *Hide the Ransomware data recovery option in the Windows Security app* setting:

- If the parent setting (Hide the Virus and threat protection area) was set to *Not configured* and the child setting was set to *Yes*, both the parent and child settings will be set to *Not configured*.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Use filters to assign policies in Endpoint Manager admin center<!-- 9518236 -->

There's a new **Filters** option that can be used when assigning apps or policies to groups. To create a filter, go to:

- **Devices** > **Filters** > **Create**
- **Apps** > **Filters** > **Create**
- **Tenant administration** > **Filters** > **Create**

You can filter the scope of affected devices using device properties. For example, you can filter on the OS version, device manufacturer, and more. After you create the filter, you can use the filter when you assign a policy or profile.

For more information, see [Use filters when assigning your apps, policies, and profiles in Microsoft Endpoint Manager](filters.md).

Applies to:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 11
- Windows 10

#### Use Intune policy to expedite installation of Windows 10/11 security updates<!-- 5584682    -->

In public preview, you can use Intune’s **Windows 10 quality updates** policy to [expedite the install of the most recent Windows 10/11 security updates](../protect/windows-10-expedite-updates.md) to devices you manage with Intune.

When you expedite an update, devices can start the download and install of the update as soon as possible, without having to wait for the device to check in for updates. Other than expediting the install of the update, use of this policy leaves your existing update deployment policies and processes untouched.

To help monitor expedited updates, you can use the following options:

- The [Windows Expedited Updates report](../protect/windows-10-expedite-updates.md#summary-report)
- [Expedited update failures](../protect/windows-10-expedite-updates.md#device-report) device report

<!-- ########################## -->
## Week of April 26, 2021 (Service release 2104)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Updated privacy screen in Company Portal for iOS<!-- 9746018  -->

We added additional text to the Company Portal privacy screen to clarify how Company Portal uses collected data. It assures users that the collected data is only used to verify that devices are compliant with their organization's policies.  

#### Installation status for device-assigned required apps<!-- 7283852  -->

From the **Installed apps** page of the Windows Company Portal or the Company Portal website, end users can view the installation status and details for device-assigned required apps. This functionality is provided in addition to the installation status and details of user-assigned required apps. For more information about the Company Portal, see [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

#### Win32 app version displayed in console<!-- 2617349  -->

The version of your Win32 app is now displayed in the Microsoft Endpoint Manager admin center. The app version is provided in the **All apps** list, where you can filter by Win32 apps and select the optional **version** column. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > **Columns** > **Version** to display the app version in the app list. For related information, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

#### Maximum OS version setting for app conditional launch on iOS devices<!-- 9493137 -->

Using Intune app protection policies, you can add a new conditional launch setting to ensure end users are not using any pre-release or beta OS build to access work or school account data on iOS devices. This setting ensures that you can vet all OS releases before end users are actively using new OS functionality on iOS devices. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App protection policies**. For related information, see [How to create and assign app protection policies](../apps/app-protection-policies.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### Device configuration

#### Updated OEMConfig policy reporting for Android Enterprise devices<!-- 5255334   -->

On Android Enterprise devices, you can create an OEMConfig policy to add, create, and customize OEM-specific settings. Now, the policy reporting is updated to also show success on a user, a device, and for each setting in the policy.

For more information, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Applies to:

- Android Enterprise

#### Disable NFC pairing on iOS/iPadOS devices running 14.2 and newer<!-- 9112701   -->

On supervised iOS/iPadOS devices, you can create a device restrictions profile that disables NFC (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile > **Connected devices** > **Disable near field communication (NFC)**). When you disable this feature, it prevents devices from pairing with other NFC-enabled devices, and disables NFC.

To see this setting, go to [iOS and iPadOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-ios.md).

Applies to:

- iOS/iPadOS 14.2 and newer

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Locate device remote action for Windows client devices<!--710717  -->

You can now use a new locate device remote action to get the geographical location of a device. Supported devices include:

- Windows 11
- Windows 10 version 20H2 (10.0.19042.789) or later
- Windows 10 version 2004 (10.0.19041.789) or later
- Windows 10 version 1909 (10.0.18363.1350) or later
- Windows 10 version 1809 (10.0.17763.1728) or later

To see the new action, sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Devices** > **Windows** > choose a device > **Locate device**.

This action will work in a similar manner as the current [Locate device action for Apple devices](..\remote-actions\device-locate.md) (but will not include any lost mode functionality).

Location services must be enabled on devices for this remote action to work. If Intune is unable to fetch the device's location and the user has set a default location in device settings, it will display the default location.

#### Microsoft Endpoint Manager ending support for Android 5.x<!--9058248  -->

Microsoft Endpoint Manager no longer supports Android 5.x devices.

#### Support to display phone numbers for corporate Android Enterprise devices<!--9086174  -->

For corporate Android Enterprise devices (Dedicated, Fully Managed, and Fully managed with work profile), the associated device phone numbers are now displayed in the Microsoft Endpoint Manager admin center. If multiple numbers are associated with the device, only one number will be displayed.

#### EID property support for iOS/iPadOS devices<!--9255367 -->

The eSIM identifier (EID) is a unique identifier for the embedded SIM (eSIM). The EID property now appears on the hardware details page for iOS/iPadOS devices.

### Intune support for provisioning Azure Active Directory shared devices<!--9585326 -->

The ability to provision Android Enterprise dedicated devices with Microsoft Authenticator automatically configured into Azure AD shared device mode is now Generally Available. For more info on how to use this enrollment type, see [Set up Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md).

#### View end of support details for your feature update profiles<!-- 9699729   -->

To help you plan for end-of-service for Windows 10 feature updates you deploy with Intune, we’ve added two new columns of information to [Feature Updates profiles](../protect/windows-10-feature-updates.md#manage-feature-updates-for-windows-10-and-later-policy) in the Microsoft Endpoint Manager admin center.

The first new column displays a status that identifies when the update in the profile is near or has reached its end of service, and the second column displays that end of service date. When an update reaches its end of service, it is no longer deployed to devices, and the policy can be removed from Intune.

The new columns and details include:

- **Support** – This column displays the status of the feature update:
  - **Supported** – The update is supported for distribution.
  - **Support ending** – The update is within two months of its end of service date.
  - **Not supported** – The update is no longer supported, having reached its end of service date.

- **Support End Date** – This column displays the end-of-service date for the feature update in the profile.

For information about end of service dates for Windows 10 releases, see [Windows 10 release information](/windows/release-health/release-information) in the Windows release health documentation.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Use Antivirus profiles to prevent or allow merger of Antivirus exclusion lists on devices<!-- 9070651  -->

You can now configure **Defender local admin merge** as a setting in a *Microsoft Defender Antivirus* profile to block merger of local exclusion lists for Microsoft Defender Antivirus on Windows 10 devices.

Exclusion lists for Microsoft Defender Antivirus can be configured locally on a device, and specified by Intune Antivirus policy:  

- When exclusion lists are merged, locally defined exclusions are merged with those from Intune.
- When merge is blocked, only exclusions from policy will be effective on the device.

For more information about this and related settings, see [Microsoft Defender Antivirus Exclusions](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions).

#### Improved flow for conditional access on Surface Duo devices<!-- 7552043    -->

We’ve streamlined the conditional access flow on Surface Duo devices. These changes happen automatically and don't require any configuration updates by administrators. (**Endpoint security** > **Conditional access**)

On a Duo device:

- When access to a resource is blocked by conditional access, users are now redirected to the Company Portal app that was preinstalled on the device. Previously, they were sent to the Google Play store listing of the Company Portal app.
- For devices that are enrolled as a personally owned work profile, when a user tries to sign in to a personal version of an app using their work credentials they are now sent to the work version of the Company Portal where guidance messaging is shown. Previously, the user was sent to the Google Play store listing of the personal version of the Company Portal app, where they would have had to reenable the personal Company Portal to see the guidance messaging.

#### Configure options that apply to Tunnel Gateway server upgrades<!-- 8664465   -->

We've added options to help you manage the [upgrade of your Microsoft Tunnel Gateway servers](../protect/microsoft-tunnel-configure.md#upgrade-microsoft-tunnel). The new options apply to the Sites configuration and include:

- Set a [maintenance window](../protect/microsoft-tunnel-configure.md) for each tunnel site. The window defines when the tunnel servers that assigned to that site can start to upgrade.  
- Configure the [server upgrade type](../protect/microsoft-tunnel-configure.md), which determines how all servers at the site proceed with upgrades. You can choose between:  
  - **Automatic** - All servers at the site will upgrade as soon as possible after a new server version becomes available.
  - **Manual** - Servers at the site will upgrade only after an admin explicitly chooses to allow the upgrade.  

- The [Health check tab](../protect/microsoft-tunnel-monitor.md#use-the-admin-center-ui) now displays status for the server's software version to help you understand when your tunnel server software is out of date. Status includes:
  - **Healthy** - up to date with the most recent software version.
  - **Warning** - one version behind
  - **Unhealthy** - two or more versions behind

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Intune apps

#### Newly available protected apps for Intune<!-- 9350479, 9449308, 9526437   -->

The following protected apps are now available for Microsoft Intune:

- Omnipresence Go by Omnipresence Technologies, Inc.
- Comfy by Building Robotics, Inc.
- M-Files for Intune by M-Files Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### New UI to filter data for new operational reports<!-- 9600112  -->

New operational reports will now support a new UI to add data filters. The new filter pill offers an improved experience to help slice, refine, and view report data. For more information about reports in Intune, see [Intune reports](../fundamentals/reports.md).

#### Windows restart frequency report in Endpoint analytics is generally available<!-- 9606273 -->

Endpoint analytics [startup performance](../../analytics/startup-performance.md) currently provides IT with insights to measure and optimize PC boot times. However, restart frequency can be just as impactful to the user experience since a device that reboots daily because of blue screens will have a poor user experience even if the boot times are fast. We have now included a report on restart frequencies within your organization to help you identify problematic devices. For more information, see [Restart frequency in endpoint analytics](../../analytics/restart-frequency.md).

## Week of April 12, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->

### Device configuration

### New modern authentication method with Apple Setup Assistant (public preview)<!--4843770 -->

When creating an Automated Device Enrollment profile, you can now choose a new authentication method: **Setup Assistant with modern authentication**. This method provides all the security from Setup Assistant but avoids the issue of leaving end users stuck on a device they can't use while the Company Portal installs on the device. The user has to authenticate using Azure AD Multi-Factor Authentication during the setup assistant screens. This will require an additional Azure AD login post-enrollment in the Company Portal app to gain access to corporate resources protected by Conditional Access. The correct Company Portal version will automatically be sent down as a required app to the device for iOS/iPadOS. For macOS, here are the options to get the Company Portal on the device - [Add the Company Portal for macOS app](../apps/apps-company-portal-macos.md).

Enrollment is completed once the user lands on the home screen, and users can freely use the device for resources not protected by Conditional Access. User affinity is established when the user lands on the home screen after the setup screens, however the device will not be fully registered with Azure AD until the Company Portal login. The device will not show up in a given user's device list in the Azure AD portal until the Company Portal login. If the tenant has multifactor  authentication turned on for these devices or users, the users will be asked to complete multifactor authentication during enrollment during Setup Assistant. Multifactor  authentication is not required, but it is available for this authentication method within Conditional Access if needed.

This method has the following options for installing the Company Portal:

- For iOS/iPadOS: The **Install Company Portal** setting will not be there when choosing this flow for iOS/iPadOS. The CP will be a required app on the device with the correct app configuration policy on it once the end user lands on the home screen. User must sign in with Azure AD credentials into the CP after enrollment to gain access to resources protected by Conditional Access and be fully Azure AD registered.
- For macOS: Users must sign into the Company Portal to complete Azure AD registration and gain access to resources protected by Conditional Access. The end user will not be locked to the CP after landing on the home page, but an additional login into the CP will be required to access corporate resources and be compliant.  For more information, see [Add the macOS Company Portal app](../apps/apps-company-portal-macos.md).

For information on how to use this authentication method on iOS/iPadOS devices, see [Automatically enroll iOS/iPadOS devices by using Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

For information on how to use this authentication method on macOS devices, see [Automatically enroll macOS devices with the Apple Business Manager or Apple School Manager](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile).

<!-- ########################## -->
## Week of March 29, 2021 (Service release 2103)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Intune management agent for macOS devices is now a universal app<!-- 9294405 -->

When you deploy shell scripts or custom attributes for macOS devices from Microsoft Endpoint Manager, it deploys the new universal version of the Intune management agent app that runs natively on Apple Silicon Mac machines. The same deployment will install the x64 version of the app on Intel Mac machines. Rosetta 2 is required to run x64 (Intel) version of apps on Apple Silicon Macs. To install Rosetta 2 on Apple Silicon Macs automatically, you can deploy a shell script in Endpoint Manager. For more information, see [Microsoft Intune management agent for macOS](../apps/lob-apps-macos-dmg.md).

### Device security

#### Update for Microsoft Tunnel<!-- 9574820 -->

We’ve released a [new version](../protect/microsoft-tunnel-upgrade.md#microsoft-tunnel-update-history) of the Microsoft Tunnel Gateway, which includes the following changes:

- Various bug fixes and enhancements.

The Tunnel Gateway server will automatically update to the new release.

<!-- ########################## -->
## Week of March 22, 2021 (Service release 2103)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Microsoft 365 Apps for macOS devices are now universal apps<!-- 9076318  -->

When you deploy Microsoft 365 Apps for macOS devices from Microsoft Endpoint Manager, it now deploys the new universal versions of the app that runs natively on Apple Silicon Macs. The same deployment will install the x64 versions of the app on Intel Macs running macOS 10.14 and higher. To add Microsoft 365 Apps for macOS, in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apps** > **All apps** > **Add**. Select **macOS** in the **App type** list under **Microsoft 365 Apps**. For related information, see [Assign Microsoft 365 to macOS devices with Microsoft Intune](../apps/apps-add-office365-macos.md).

#### Additional configuration keys for the Microsoft Launcher app<!-- 9364310  -->

You can now set folder configuration settings for Microsoft Launcher on Android Enterprise corporate owned fully managed devices. By using an app configuration policy and configuration key values, you can set values for folder shape, folder opened to full screen, and folder scroll direction. Also, you can position the folder on the home screen in addition to positioning apps and weblinks. Additionally, you can choose to allow end users to modify the folder style values within the app. For more information about Microsoft Launcher, see [Configure Microsoft Launcher for Android Enterprise with Intune](..\apps\configure-microsoft-launcher.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### More Microsoft Edge settings, and setting categories are removed in Settings Catalog for macOS<!-- 9220407   -->

On macOS devices, you can use the Settings Catalog to configure Microsoft Edge version 77 and newer (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings Catalog**).

In this release:

- More Microsoft Edge settings are added.
- Temporarily, the setting categories are removed. To find a specific setting, use the **Microsoft Edge - All** category, or search for the setting name. For a list of settings, see  [Microsoft Edge - Policies](/DeployEdge/microsoft-edge-policies).

For more information on the Settings Catalog, see [Use the settings catalog to configure settings](../configuration/settings-catalog.md).

Applies to:

- macOS
- Microsoft Edge

#### Windows 10/11 in cloud configuration is available as a Guided Scenario<!-- 9272086  -->

Windows 10/11 in cloud configuration is a Microsoft-recommended device configuration for Windows 10/11. Windows 10/11 in cloud configuration is optimized for the cloud and designed for users with focused workflow needs.

There's a guided scenario that automatically adds the apps, and creates the policies that configure your Windows 10/11 devices in a cloud configuration.

For more information, see [Guided scenario for Windows 10/11 in cloud configuration](../fundamentals/cloud-configuration.md).

Applies to:

- Windows 11
- Windows 10

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Increasing recommended maximum number of iOS/iPadOS and macOS devices per enrollment token<!--8568668  -->

Previously, we recommended that you don't exceed 60,000 iOS/iPadOS or macOS devices per Automated Device Enrollment (ADE) token. This recommended limit is now increased to 200,000 devices per token. For more information about ADE tokens, see [Automatically enroll iOS/iPadOS devices by using Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume).

#### Update of column names in All devices view and Export report<!-- 8854380  -->

To accurately reflect the data in the columns, we've updated the column names in the All devices view and the Export report to be "Primary User UPN", "Primary User email address", and "Primary User display name".

### End of support for Internet Explorer 11<!--9218996 -->

Intune will end support for Internet Explorer 11 admin access to the Admin Portal web app UI on March 31, 2021. Move to Edge or another [supported browser](supported-devices-browsers.md) before that time to administer any of your Microsoft services built on Azure.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Health status details for Microsoft Tunnel Gateway servers<!-- 8460911    -->

We've added the ability to see detailed heath status information for Tunnel Gateway servers within the Microsoft Endpoint Manager admin center.

On the new [*Health check* tab](../protect/microsoft-tunnel-monitor.md#use-the-admin-center-ui), you'll see the following information:

- Last check-in - When the server last checked-in with Intune.
- Number of current connections - The number of active connections at last check-in
- Throughput- The megabits per second that traverse the serves NIC at last check-in.
- CPU usage - The average CPU use.
- Memory usage - The average memory use.
- Latency - The average time for IP packets to traverse the NIC.
- TLS certificate expiration status and days before expiration - How long the TLS certificate that secures client to server communication for the tunnel remains valid.

#### Public preview of Tunnel client functionality in Microsoft Defender for Endpoint app for Android<!-- 9248143 -->

As announced at Ignite, Microsoft Tunnel client functionality is migrating into the Microsoft Defender for Endpoint app. With this preview, you can start to use a preview version of Microsoft Defender for Endpoint as the Tunnel app for supported devices. The existing Tunnel client remains available, but will eventually be phased out in favor of the Defender for Endpoint app.

This public preview applies to:  

- Android Enterprise
  - Fully managed
  - Corporate-owned work profile
  - Personally owned work profile

For this preview, you must opt in to gain access to the preview version of Microsoft Defender for Endpoint, and then migrate supported devices from the standalone Tunnel client app to the preview app. For details, see [Migrate to the Microsoft Defender for Endpoint app](../protect/microsoft-tunnel-migrate-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Intune apps

#### Microsoft Launcher configuration keys<!-- 8980621  -->

For Android Enterprise fully managed devices, the Microsoft Launcher for Intune app now provides additional customization. In Launcher, you can configure the set of displayed apps and weblinks, as well as the order of these apps and weblinks. The displayed app list and position (order) of app configurations have been merged together to simplify home screen customization. For more information, see [Configure Microsoft Launcher](../apps/configure-microsoft-launcher.md).

#### Microsoft Edge for macOS devices will be a universal app<!-- 9175989 9176098 9176466 9275782  -->

When you deploy the Microsoft Edge app for macOS devices from Microsoft Endpoint Manager, it now deploys the new universal version of the app that runs natively on Apple Silicon Macs. The same deployment will install the x64 version of the app on Intel Macs. To add Microsoft Edge for macOS, in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apps** > **All apps** > **Add**. Select **macOS** in the **App type** list under **Microsoft Edge, version 77 and later**. For related information, see [Add Microsoft Edge to macOS devices using Microsoft Intune](../apps/apps-edge-macos.md).

#### Newly available protected apps for Intune<!-- 9099719  -->

The following protected apps are now available for Microsoft Intune:

- FleetSafer by Cogosense Technology Inc.
- Senses by Mazrica Inc.
- Fuze Mobile for Intune by Fuze, Inc.
- MultiLine for Intune by Movius Interactive Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

#### Improved notification experience in the iOS/iPadOS Company Portal app<!-- 7219429  -->

The Company Portal app can now store, as well as display, push notifications sent to your users' iOS/iPadOS devices from the Microsoft Endpoint Manager admin center. Users who have opted in to receive Company Portal push notifications can view and manage the customized stored messages that you send to their devices in the **Notifications** tab of the Company Portal. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Scripting

#### Export localized Intune report data using Graph APIs<!-- 8612346  -->

You can now specify that the report data that you export using the Microsoft Endpoint Manager reporting export [API](../fundamentals/reports-export-graph-apis.md) can contain localized columns only, or localized and non-localized columns. The localized and non-localized columns option will be selected by default for most reports, which will prevent breaking changes. For related information about reports, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md) and [Intune reports and properties available using Graph API](../fundamentals/reports-export-graph-apis.md).

<!-- ########################## -->
## Week of March 8, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### New version of the PFX Certificate Connector<!-- 9494956-->

We’ve released a new version of the PFX Certificate Connector, version **6.2101.16.0**. This update adds improvements to the PFX Create flow to prevent duplication of Certificate Request files on on-premises servers that host the connector.

For more information about certificate connectors, including a list of connector releases for both certificate connectors, see [Certificate connectors](../protect/certificate-connectors.md).

<!-- ########################## -->
## Week of March 1, 2021 (Service release 2102)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Support for Win32 app supersedence in Intune<!-- 8517457-->

We've enabled a public preview of app supersedence in Intune. You can now create supersedence relationships between apps, which allows you to update and replace existing Win32 apps with newer versions of the same app, or entirely different Win32 apps. For more information, see [Win32 app supersedence](../apps/apps-win32-supersedence.md).

#### Maximum OS version setting for app conditional launch on Android devices<!-- 7764870  -->

Using Intune app protection policies, you can add a new conditional launch setting to ensure end users are not using any pre-release or beta OS build to access work or school account data on Android devices. This setting ensures that you can vet all OS releases before end users are actively using new OS functionality on Android devices. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you will be able to find this setting by selecting **Apps** > **App protection policies**. For related information, see [How to create and assign app protection policies](../apps/app-protection-policies.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Use Cisco AnyConnect as a VPN connection type for Windows 10/11 and Windows Holographic for Business<!-- 2605377 -->

You can create VPN profiles using Cisco AnyConnect as a connection type (**Devices** > **Device configuration** > **Create profile** > **Windows 10 and later** for platform > **VPN** for profile > **Cisco AnyConnect** for connection type) without needing to use custom profiles.

This policy uses the Cisco AnyConnect app available in the Microsoft store. It doesn't use the Cisco AnyConnect desktop application.

For more information on VPN profiles in Intune, see [Create VPN profiles to connect to VPN servers](../configuration/vpn-settings-configure.md).

Applies to:

- Windows 11
- Windows 10
- Windows Holographic for Business

#### Run Microsoft Edge version 87 and newer in single app kiosk mode on Windows 10/11 devices<!-- 8271248   -->

On Windows client devices, you configure a device to run as a kiosk that runs one app, or runs many apps (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Kiosk**). When you select single app mode, you can:

- Run Microsoft Edge version 87 and newer.
- Select **Add Microsoft Edge legacy browser** to run Microsoft Edge version 77 and older.

For more information on the settings you can configure in kiosk mode, see [Kiosk settings for Windows client devices](../configuration/kiosk-settings-windows.md).

Applies to:

- Windows 11 in single-app kiosk mode
- Windows 10 in single-app kiosk mode
- Microsoft Edge version 87 and newer
- Microsoft Edge version 77 and older

#### Administrative Templates is available in Settings Catalog, and has more settings<!-- 9262405 -->

In Intune, you can use Administrative Templates to create policies (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Administrative Templates** for profile).

In the Settings Catalog, Administrative Templates are also available, and have more settings (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Settings Catalog** for profile).

With this release, admins can configure additional settings that only existed in on-premises group policy, and weren't available in cloud-based MDM. These settings are available for **Windows Insider** client endpoint builds, and may be backported to in-market Windows versions, such as 1909, 2004, or 2010.

If you want to create Administrative Templates, and use all the available settings exposed by Windows, then use the Settings Catalog.

For more information, see:

- [Use Windows 10/11 templates to configure group policy settings](../configuration/administrative-templates-windows.md)
- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)

Applies to:

- Windows 11
- Windows 10

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Sync status of enrollment program tokens<!-- 9235108  -->

The sync status for automated device enrollment tokens listed on the **Enrollment program tokens** pane has been removed to minimize confusion. The per-token information continues to be displayed. Enrollment program tokens are used to manage automated device enrollment with Apple Business Manager and Apple School Manager. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) you can find the token list for iOS/iPadOS devices by selecting **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment program tokens**. To find the token list for macOS devices, select **Devices** > **macOS** > **macOS enrollment** > **Enrollment program tokens**. For related information, see [Automatically enroll iOS/iPadOS devices](../enrollment/device-enrollment-program-enroll-ios.md) and [Automatically enroll macOS devices](../enrollment/device-enrollment-program-enroll-macos.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Collect diagnostics remote action<!--2167272   -->

A new remote action, **Collect diagnostics**, lets you collect the logs from corporate devices without interrupting or waiting for the end user. Collected logs include MDM, Autopilot, event viewers, key, Configuration Manager client, networking, and other critical troubleshooting logs. For more information see [Collect diagnostics from a Windows device](..\remote-actions\collect-diagnostics.md).

#### New options for export device data<!--6330532   -->

The following new options are available when exporting device data:

- Only include selected columns in the exported file.
- Include all inventory data in the exported file.
To see these options, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices** > **Export**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Use the variable CN={{UserPrincipalName}} in the subject and SAN of SCEP and PKCS certificate profiles for Android Enterprise devices<!-- 9290978   -->

You can now use the User attribute **CN={{UserPrincipalName}}** variable in the subject or SAN of a [PKCS certificate profile](../protect/certificates-pfx-configure.md#create-a-trusted-certificate-profile) or [SCEP certificate profile](../protect/certificates-profile-scep.md#create-a-scep-certificate-profile) for Android devices. This support requires the device have a user, such as devices enrolled as:

- Android Enterprise fully managed
- Android Enterprise personally owned work profile

User attributes are not supported for devices that don’t have user associations, such as devices that are enrolled as Android Enterprise dedicated. For example, a profile that uses *CN={{UserPrincipalName}}* in the subject or SAN won’t be able to get the user principal name when there is no user on the device.

#### Use app protection policies for Defender for Endpoint on Android and iOS<!-- 6486982   7362746  -->

You can now use [Microsoft Defender for Endpoint in app protection policies for devices that run Android or iOS](../protect/advanced-threat-protection-configure.md#create-and-assign-app-protection-policy-to-set-device-risk-level).

- Configure your MAM conditional launch policy to include **Max allowed threat level** signals from Microsoft Defender for Endpoint on iOS devices and Android devices.
- Choose to **Block Access** or **Wipe Data** based on whether or not the device meets the expected threat level.

When configured, end users are prompted to install and set up the **Microsoft Defender for Endpoint** app from the applicable app store. As a prerequisite, you must set up your **Microsoft Defender for Endpoint** connector and switch on the toggle to send risk data to your app protection policies. For related information, see [App protection policies overview](../apps/app-protection-policy.md), and [Use Microsoft Defender for Endpoint in Microsoft Intune](..\protect\advanced-threat-protection.md).

#### Configure Attack surface reduction rules to block malware from gaining persistence through WMI<!-- 8902661   -->

You can now configure the rule named **Block persistence through WMI event subscription** as part of an [Attack surface reduction rules](../protect/endpoint-security-asr-policy.md#attack-surface-reduction-profiles) profile in Endpoint security.

This rule prevents malware from abusing WMI to attain persistence on a device. Fileless threats employ various tactics to stay hidden, to avoid being seen in the file system, and to gain periodic execution control. Some threats can abuse the WMI repository and event model to stay hidden.

When configured as [setting for *Attack surface reduction*](../protect/endpoint-security-asr-profile-settings.md#attack-surface-reduction-rules-profile) policy for Endpoint security, the following options are available:
- **Not configured** (default) – The setting returns to the Windows default, which is off and persistence is not blocked.
- **Block** – Persistence through WMI is blocked.
- **Audit** – Evaluate how this rule affects your organization if it's enabled (set to Block).
- **Disable** - Turn this rule off. Persistence is not blocked.

This rule doesn’t support the *Warn* option, and is also available as a Device configuration setting from the [Settings catalog](../configuration/settings-catalog.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Intune apps

#### Company Portal website improved load performance<!-- 8765415  -->

To improve page load performance, app icons will now load in batches. End users may see a placeholder icon for some of their applications when visiting the Company Portal website. The related icons will load shortly after. For more information about the Company Portal, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md) and [Manage apps from the Company Portal website](../user-help/manage-apps-cpweb.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Endpoint analytics in Microsoft Productivity Score<!-- IN8529842 -->

There's a new Endpoint Analytics page in [Microsoft Productivity Score](/microsoft-365/admin/productivity/productivity-score) that shares organizational level insights with the other roles outside of Microsoft Endpoint Manager. Understanding how your devices contribute to your end-users' experience is critical to enabling users to reach their goals. For more information, see [Endpoint analytics in Microsoft Productivity Score](../../analytics/productivity-score.md).

#### Endpoint analytics Application Reliability report<!-- IN5653073 -->

A new **Application Reliability** report will be available in Endpoint analytics. This report provides insight into potential issues for desktop applications on managed PCs. You can quickly identify the top applications that are impacting end user productivity, as well as see aggregate app usage and app failure metrics for these applications. You'll be able to troubleshoot by drilling into a specific device and viewing a timeline of app reliability events. This report is expected to be available in public preview during March 2021. For more information, see [Endpoint analytics application reliability](../../analytics/app-reliability.md).

#### Restart frequency (preview) in Endpoint analytics<!--6225459 -->

Endpoint analytics [startup performance](../../analytics/startup-performance.md) currently provides IT with insights to measure and optimize PC boot times. However, restart frequency can be just as impactful to the user experience since a device that reboots daily because of blue screens will have a poor user experience even if the boot times are fast. We have now included a preview report on restart frequencies within your organization to help you identify problematic devices. For more information, see [Restart frequency (preview) in endpoint analytics](../../analytics/restart-frequency.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Role-based access permissions update for Microsoft Tunnel Gateway<!-- 8554762   -->

To help control who has rights to manage the Microsoft Tunnel, we've added [**Microsoft Tunnel Gateway**](../protect/microsoft-tunnel-prerequisites.md#permissions) as a new permissions group to Intune role-based access control. This new group includes the following permissions:

- **Create** - Configure Microsoft Tunnel Gateway servers, server configurations, and sites.
- **Update** (modify) - Update Microsoft Tunnel Gateway servers, server configurations, and sites.
- **Delete** - Delete Microsoft Tunnel Gateway servers, server configurations, and sites.
- **Read** - View Microsoft Tunnel Gateway servers, server configurations, and sites.

By default, Intune Administrators and Azure Active Directory administrators have these permissions. You can also add these permissions to [custom roles you create](create-custom-role.md) for your Intune tenant.

#### Scope tag support for customization policies for Intune for Government and 21Vianet<!--9419267  -->

You can now assign scope tags to Customization policies for Intune for Government and Intune operated by 21Vianet. To do so, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Customization** where you will see **Scope tags** configuration options.

<!-- ########################## -->
## Week of February 22, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### New version of the PFX Certificate Connector<!-- 9333009 -->

We’ve released a new version of the PFX Certificate Connector, version **6.2101.13.0**. This new connector version adds [improvements for logging](../protect/certificate-connectors.md#logging) to the PFX Connector:

- New location for Event Logs, with logs broken down into Admin, Operational & Debug
- Admin & Operational logs default to 50 MB - with auto archiving enabled.
- EventIDs for PKCS Import, PKCS Create and Revocation.

For more information about certificate connectors, including a list of connector releases for both certificate connectors, see [Certificate connectors](../protect/certificate-connectors.md).

<!-- ########################## -->
## Week of February 8, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### End users can restart an app install from the Windows Company Portal<!-- 652935 -->

Using the Windows Company Portal, end users can restart an app installation if the progress seems to have stalled or is frozen. This functionality is allowed if the app installation progress has not changed in two hours. For related information, see [Add apps to Microsoft Intune](../apps/apps-add.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Google’s compliance screens are automatically shown on Android Enterprise 9.0+ dedicated devices running in kiosk mode<!-- 9323100  -->

In Intune, you can create a device configuration password policy and a device compliance password policy on Android Enterprise devices.

When you create the policies, Android Enterprise dedicated devices running in kiosk mode automatically use Google’s compliance screens. These screens guide and force users to set a password that meets your policy rules.

For more information on creating password and kiosk policies, see:

- [Android Enterprise settings to mark devices as compliant or not compliant](../protect/compliance-policy-create-android-for-work.md)
- [Android Enterprise device settings to allow or restrict features](../configuration/device-restrictions-android-for-work.md)

Applies to:

- Android Enterprise 9 and newer in kiosk mode

<!-- ########################## -->
## Week of February 1, 2021 (2101 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Configure whether a required iOS/iPadOS app is removable<!-- 8391462  -->

You can now configure whether a required iOS/iPadOS app is installed as a removable app by end users. This new setting applies to iOS store, LOB and built-in apps. You can find this setting in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** > **Add**. When setting the app assignments, you can select **Install as removable**. The default value is **Yes**, which means the app is removable. Existing required installs on iOS 14 have been updated to the default (removable) setting value. For more information about iOS/iPadOS apps, see [Microsoft Intune app management](..\apps\app-management.md).

#### Line-of-business apps supported on Shared iPad devices<!-- 8834566  -->

You can now deploy line-of-business (LOB) apps to Shared iPad devices. The line-of-business app must be assigned as **required** to a device group containing Shared iPad devices from the Microsoft Endpoint Manager admin center. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > **Add**. For related information, see [Add an iOS/iPadOS line-of-business app to Microsoft Intune](../apps/lob-apps-ios.md).

#### Microsoft Endpoint Configuration Manager connector<!-- 9229333, CM7138634 -->
The connector for Microsoft Endpoint Configuration Manager now displays in the admin center. To review the connector, go to **Tenant administration** > **Connectors and tokens** > **Microsoft Endpoint Configuration Manager**. Select a Configuration Manager hierarchy running version 2006, or later to display additional information about it.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### New version of the PFX Certificate Connector<!-- 9202990  -->

We’ve released a new version of the PFX Certificate Connector, version **6.2009.2.0**. This new connector version:

- Improves upgrade of the Connector to persist accounts that run Connector Services.

For more information about certificate connectors, including a list of connector releases for both certificate connectors, see [Certificate connectors](../protect/certificate-connectors.md).

#### Use device configuration to create folders and set the grid size on the Managed Home Screen<!-- 3041948 -->

On Android Enterprise dedicated devices, you can configure the Managed Home Screen settings (**Devices** > **Device configuration** > **Create profile** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile > Device restrictions** for profile > **Device experience**).

When using the Managed Home Screen in multi-app kiosk mode, there's a **Custom app layout** setting. With this setting, you can:

- Create folders, add apps to these folders, and put the folder on the Managed Home Screen. You don't have to order the folders.
- Choose whether or not to order apps and folders on the Managed Home Screen. If you order, you can also:

  - Set the grid size.
  - Add apps and folders to different places on the grid.

Previously, you had to use an [app configuration policy](../apps/app-configuration-managed-home-screen-app.md).

For more information, see [Android Enterprise dedicate devices device experience settings](../configuration/device-restrictions-android-for-work.md#device-experience).

Applies to:
- Android Enterprise dedicated devices

#### Use the settings catalog to configure Microsoft Edge browser on macOS devices<!-- 4552197   -->

Currently on macOS devices, you configure the Microsoft Edge browser using a `.plist` preference file (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Preference file** for profile).

There's an updated UI to configure the Microsoft Edge browser: **Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile. Select the Microsoft Edge settings you want, and then configure them. In your profile, you can also add settings, or remove existing settings.

To see a list of the settings you can configure, go to [Microsoft Edge - Policies](/DeployEdge/microsoft-edge-policies). Be sure macOS is listed as a supported platform. If some settings aren't available in the settings catalog, then it's recommended to continue using the preference file only.

For more information, see:
- [Settings catalog](../configuration/settings-catalog.md)
- [Add a property list file to macOS devices using Intune](../configuration/preference-file-settings-macos.md)

To see the policies you have configured, open Microsoft Edge, and go to `edge://policy`.

Applies to:
- Microsoft Edge browser version 77 and newer on macOS

#### Use NetMotion Mobility as a VPN connection type for Android Enterprise devices<!-- 7764263 7862120  -->

When you create a VPN profile, NetMotion Mobility is available as a VPN connection type for Android Enterprise:

- **Devices** > **Device configuration** > **Create profile** > **Android Enterprise** > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **VPN** for profile > **NetMotion Mobility**  for connection type
- **Devices** > **Device configuration** > **Create profile** > **Android Enterprise** > **Personally Owned Work Profile** > **VPN** for profile > **NetMotion Mobility** for connection type

For more information on VPN profiles in Intune, see [Create VPN profiles to connect to VPN servers](../configuration/vpn-settings-configure.md).

Applies to:
- Android Enterprise Personally Owned Work Profile
- Android Enterprise Fully Managed, Dedicated, and Corporate-Owned Work Profile

#### Settings catalog and Templates when creating device configuration profiles for macOS and Windows client devices<!-- 8673623 8254609  -->

There are UI updates when creating device configuration profiles for macOS and Windows 10/11 devices (**Devices** > **Configuration profiles** > **Create profile** > **macOS** or **Windows 10 and later** for platform).

The profile shows **Settings catalog** and **Templates**:

- **Settings catalog**: Use this option to start from scratch and select settings you want from the library of available settings. For macOS, the settings catalog includes settings to configure the Microsoft Edge version 77 and newer. Settings catalog for Windows client includes many existing settings, and new settings, all in one place.
- **Templates**: Use this option to configure all the existing profiles, such as device restrictions, device features, VPN, Wi-Fi, and more.

This is only a UI change, and doesn't impact existing profiles.

For more information, see [Settings catalog](../configuration/settings-catalog.md).

Applies to:
- macOS
- Windows 11
- Windows 10

#### Home screen layout updates on supervised iOS/iPadOS devices<!-- 8710594 7978976    -->

On iOS/iPadOS devices, you can configure the Home Screen layout (**Devices** > **Device Configuration** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **Home screen layout**). In Intune, the Home Screen Layout feature is updated:

-<!-- 8710594 --> The home screen layout has a new design. This feature allows admins to see in real time how the apps and app icons look on pages, the dock, and within folders. When adding apps in this new designer, you can't add separate pages. But, when you add nine or more apps to a folder, then those apps automatically go on the next page.
    Existing policies are not impacted, and don't need to be changed. The setting values are transferred to the new UI without any negative effects. The setting behavior on devices is the same.
-<!-- 7978976 --> Add a web link (web app) to a page, or to the dock. Be sure you add a specific URL of the web link only once. Existing policies are not impacted, and don't need to be changed.

For more information on the settings you can configure, including the home screen layout, see [iOS/iPadOS device settings to use common iOS/iPadOS features in Intune](../configuration/ios-device-features-settings.md).

Applies to:
- iOS/iPadOS supervised devices

#### Limit Apple's personalized advertising on iOS/iPadOS devices<!-- 8518601  -->

On iOS/iPadOS devices, you can configure Apple's personalized advertising. When enabled, personalized ads are limited in the App Store, Apple News, and Stocks apps (**Devices** > **Device Configuration** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile > **General** > **Limit Apple personalized advertising**).

This setting only impacts personalized ads. Configuring this setting sets **Settings** > **Privacy** > **Apple Advertising** to **off**. It doesn't impact non-personalized ads in the App Store, Apple News, and Stocks apps. For more information on Apple's advertising policy, see [Apple Advertising & Privacy](https://support.apple.com/HT205223) (opens Apple's web site).

To see the current settings you can configure in Intune, go to [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md).

Applies to:

- iOS/iPadOS 14.0 and newer, devices enrolled with device enrollment or automated device enrollment

#### Administrative templates includes new policies for Microsoft Edge version 88<!-- 9021341  -->

You can configure and deploy new ADMX settings that apply to Microsoft Edge version 88. To see the new policies, go to [Microsoft Edge release notes](/deployedge/microsoft-edge-relnote-stable-channel#policy-updates).

For more information on this feature in Intune, see [Configure Microsoft Edge policy settings](../configuration/administrative-templates-configure-edge.md).

Applies to:

- Windows 11
- Windows 10

#### Locale support in email notifications for non-compliance<!--7604191    -->

Compliance policies now support [Notification message templates](../protect/actions-for-noncompliance.md#create-a-notification-message-template) that include separate messages for different locales. Support for multiple languages no longer requires you to create separate templates and policies for each locale.

When you configure locale-specific messages in a template, non-compliant end-users receive the appropriate localized email notification message based on their O365 preferred language. You also designate one localized message in the template as the *default* message. The default message is sent to users that haven’t set a preferred language or when the template doesn’t include a specific message for their locale.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Hide more screens for the Apple Automated Device Enrollment Setup Assistant<!--7786092   -->

You can now set Automated Device Enrollment (ADE) profiles to hide these Setup Assistant Screens for iOS/iPadOS 14.0+ and macOS 11+ devices:

- Restore Completed, for iOS/iPadOS 14.0+.
- Software Update Completed, for iOS/iPadOS 14.0+.
- Accessibility, for macOS 11+ (the mac device must be connected to an Ethernet).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Migrate device security policies from Basic Mobility and Security to Intune<!--6306140   -->

The policy migration tool lets you permanently move Mobile Device Management (MDM) device security policies deployed by Basic Mobility and Security (formerly MDM for Office 365 or Office MDM) to standard Intune MDM configuration profiles and compliance policies. Using this tool will disable all future policy creation and edits in Basic Mobility and Security device security policies.

To use the tool, you must:

- Already have purchased (but not yet assigned) Intune licenses for all the users of devices managed by Basic Mobility and Security.
- Contact support to check eligibility if you have purchased an Intune for Education subscription.

For more information, see [Migrate your mobile device management from Basic Mobility and Security to Intune](migrate-to-intune.md).

#### Subnet ID and IP addresses on Properties page for corporate-owned Windows devices<!--5265589   -->

Subnet ID and IP addresses are now displayed on the **Properties** page for corporate-owned Windows devices. To see them, go to [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices** > choose a corporate-owned Windows device > **Properties**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Intune support for Microsoft Defender Application Guard now includes isolated Windows environments<!-- 8274282     -->

When you configure **Turn on Application Guard**  in an Intune [App and browser isolation profile](../protect/endpoint-security-asr-profile-settings.md#app-and-browser-isolation) in Endpoint security Attack surface reduction policy, you can choose from the following options when you enable Application Guard:

- **Microsoft Edge** - *Previously available*
- **Isolated Windows environments** - *New with this update*
- **Microsoft Edge** ***and*** **isolated Windows environments** - *New with this update*

Before this release, the setting was named *Turn on Application Guard for Edge (Options)*.

The new options for this setting expand Application Guard support beyond just URL’s for Edge. You can now enable Application Guard to help protect devices by opening potential threats in a hardware isolated Windows VM environment (container). For example, with support for isolated Windows environments, Application Guard can open untrusted Office documents in an isolated Windows VM.

With this change:

- Intune now supports the full range of values found in the Windows MDM CSP: [AllowWindowsDefenderApplicationGuard](/windows/client-management/mdm/windowsdefenderapplicationguard-csp).
- To help you understand the effect on device users when using isolated Windows environments, see [Application Guard testing scenarios](/windows/security/threat-protection/microsoft-defender-application-guard/test-scenarios-md-app-guard) in the Windows security documentation.
- Read more about Application Guard and support for Office apps in [Application Guard for Office](/microsoft-365/security/office-365-security/install-app-guard?view=o365-worldwide&preserve-view=true) in the Microsoft 365 documentation.

#### New Application Guard settings in Attack surface reduction policy<!-- 8274336   -->

We’ve added two new settings to the App and browser isolation profile of Intune’s [Endpoint security Attack surface reduction policy](../protect/endpoint-security-asr-policy.md):
- **Application Guard allow camera and microphone access** – Manage access by Application Guard apps to a devices camera and microphone.
- **Application Guard allow use of Root Certificate Authorities from the user's device** – When you specify one or more root certificate thumbprints, the matching certificates are transferred to the Microsoft Defender Application Guard container.

For more information, see the settings for [App and browser isolation](../protect/endpoint-security-asr-profile-settings.md#app-and-browser-isolation).

#### Updates for Security Baselines<!-- 8391335, 8377369   -->

We have new versions available for the following [security baselines](../protect/security-baselines.md):

- **[MDM Security baseline (Windows 10 Security)](../protect/security-baseline-settings-mdm-all.md?pivots=december-2020)**
- **[Microsoft Defender for Endpoint baseline](../protect/security-baseline-settings-defender-atp.md?pivots=december-2020)**

Updated baseline versions bring support for recent settings to help you maintain the best-practice configurations recommended by the respective product teams.

To understand what's changed between versions, see [Compare baseline versions](../protect/security-baselines.md#compare-baseline-versions) to learn how to export a .CSV file that shows the changes.

#### Endpoint Security Firewall reports<!-- 5653366    -->

We’ve added two new reports that are dedicated to Firewall policies in Endpoint Security:

- [Windows 10 MDM devices with firewall off](../protect/endpoint-security-policy.md) is found in the Endpoint security node and displays the list of Windows 10 devices with the Firewall turned off. This report identifies each device by device name, device ID, user information, and the Firewall status.
- [Windows 10 MDM Firewall status](../fundamentals/reports.md#windows-10-mdm-firewall-status-organizational) is an organizational report found in the *Reports* node, which lists the firewall status for your Windows 10 devices. This report displays status information that includes if the firewall is enabled, disabled, limited, or temporarily disabled.

#### Summary view for Defender Antivirus reports<!-- 8846877   -->

We’ve updated the view for the Microsoft Defender Antivirus reports found in the **Reports** node of the Microsoft Endpoint Manager admin center. Now, when you select Microsoft Defender Antivirus in the **Reports** node, you’ll see the default view of the **Summary** tab, and a second tab for **Reports**. The **Reports** tab is where you’ll find the previously available [Antivirus agent status](../fundamentals/reports.md#antivirus-agent-status-report-organizational) and [Detected malware](../fundamentals/reports.md#detected-malware-report-organizational) organizational reports.

The new **Summary** tab displays the following information:

- Displays aggregate details for the Antivirus reports.
- Includes a *Refresh* option that updates the counts of devices in each antivirus state.
- Reflects the same data as found in the [Antivirus agent status organizational](../fundamentals/reports.md#antivirus-agent-status-report-organizational) report, which is now accessed from the **Reports** tab.

#### App protection policy support on Android and iOS/iPadOS for additional Mobile Threat Defense partners<!-- 8846351  -->

In October of 2019, Intune app protection policy added the capability to use data from our Microsoft Threat Defense partners.

With this update, we're expanding this support to the following partner for using an app protection policy to block or selectively wipe a user’s corporate data based on the health of the device:

- **McAfee MVision Mobile** on Android, iOS and iPadOS

For more information, see [Create Mobile Threat Defense app protection policy with Intune](../protect/mtd-app-protection-policy.md).

#### Increased certificate validity period for SCEP and PKCS profiles<!-- 8629805   -->

Intune now supports a **Certificate validity period** of up to **24** months in certificate profiles for [Simple Certificate Enrollment Protocol](../protect/certificates-profile-scep.md#create-a-scep-certificate-profile) (SCEP) and [Public Key Cryptography Standards](../protect/certificates-pfx-configure.md#create-a-pkcs-certificate-profile) (PKCS). This is an increase from the previous support period of up to 12 months.

This support applies to Windows and Android. Certificate validity periods are ignored by iOS/iPadOS and macOS.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### New co-management eligibility organizational report<!-- 7854306  -->

The **Co-management eligibility** report provides an eligibility evaluation for devices that can be co-managed. Co-management enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune. You will be able to view a summary for this report in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Reports** > **Cloud attached devices** > **Reports** tab > **Co-management eligibility**. For related report information, see [Intune reports](../fundamentals/reports.md).

#### New co-managed workloads organizational report<!-- 7854306  -->

The **Co-Managed Workloads** report provides a report of devices that are currently co-managed. Co-management enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune. You can view this report in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Reports** > **Cloud attached devices** > **Reports** tab >  **Co-Managed Workloads**. For more information, see [Intune reports](../fundamentals/reports.md).

#### Log Analytics includes device details log<!--6014987  -->

Intune device detail logs are now available. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports** > **Log analytics**. You can correlate a set of device details to build custom queries and Azure workbooks. For more information, see [Azure Monitor integration reports (Specialist)](../fundamentals/reports.md#azure-monitor-integration-reports-specialist).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Scope tag support for the Enrollment Status Page<!--4172335 -->

You can now assign scope tags to the Enrollment Status Page so only the roles you define will be able to see it. For more information, see [Create Enrollment Status Page profile and assign to a group](../enrollment/windows-enrollment-status.md#create-new-profile).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Scripts

#### Additional Data Warehouse beta properties<!-- 8612282  -->

Additional properties are now available using the Intune Data Warehouse beta API. The following properties are exposed via the [devices](../developer/reports-ref-devices.md) entity in the beta API:

- `SubnetAddressV4Wifi` - The subnet address for IPV4 Wi-Fi connection.
- `IpAddressV4Wifi` - The IP address for IPV4 Wi-Fi connection.

For related information, see [Microsoft Intune Data Warehouse API](../developer/reports-nav-intune-data-warehouse.md).

<!-- ########################## -->
## Week of January 25, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Application icon update for iOS, macOS, and web Company Portal<!-- 7113985 -->

We've updated the app icon for the Company Portal for iOS, macOS, and web. This icon is also used by the Company Portal for Windows. End users will see the new icon in their device's application launcher and home screen, in Apple's App Store, and in experiences within the Company Portal apps.

#### Android Enterprise system app support in personally owned work profiles<!-- 5291507 -->

You can now deploy Android Enterprise system apps to Android Enterprise personally owned work profile devices. System apps are apps that do not appear in the Managed Google Play Store and often come pre-installed on the device. Once a system app is deployed, you will be unable to uninstall, hide, or otherwise remove the system app. For related information about system apps, see [Add Android Enterprise system apps to Microsoft Intune](../apps/apps-ae-system.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Update when exporting Intune reports using the Graph API<!-- 8764428 -->

When you use the `exportJobs` Graph API to export Intune reports without selecting any columns for the devices report, you will receive the default column set. To reduce confusion, we have removed columns from the default column set. The removed columns are `PhoneNumberE164Format`, `_ComputedComplianceState`, `_OS`, and `OSDescription`. These columns are still available for selection if you need them, but only explicitly, and not by default. If you have built automation around the default columns of the device export, and that automation uses any of these columns, you need to refactor your processes to explicitly select these and any other relevant columns. For related information, see [Export Intune reports using Graph APIs](../fundamentals/reports-export-graph-apis.md).

<!-- ########################## -->
## Week of January 18, 2021

### Device configuration

#### Microsoft Tunnel now supports Red Hat Enterprise Linux 8<!-- 8981769 -->

You can now use Red Hat Enterprise Linux (RHEL) 8 with the [Microsoft Tunnel](../protect/microsoft-tunnel-prerequisites.md#linux-server). To make use of for RHEL 8 you won't need to take any actions. Support has been added to the Docker containers which update automatically. In addition, this update also suppresses some extraneous logging.

<!-- ########################## -->
## Week of January 11, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Deleting Win32 apps in a dependency relationship<!-- 8997490 -->

Win32 apps added to Intune cannot be removed if they are in a dependency relationship. These apps can only be deleted after the dependency relationship is removed. This requirement is applied to both parent and child apps in a dependency relationship. Also, this requirement ensures that dependencies are enforced properly and that dependency behavior is more predictable. For more information, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

#### Scope tag support for customization policies<!--6182440  -->

You can now assign scope tags to Customization policies. To do so, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Customization** where you will see **Scope tags** configuration options. This feature is now available for Intune for Government or Intune operated by 21Vianet.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### New version of the PFX Certificate Connector<!-- 9139477 -->

We’ve released a new version of the PFX Certificate Connector, version **6.2009.1.9**. This new connector version:

- Improvements to the renewal of the connector certificate.

For more information about certificate connectors, including a list of connector releases for both certificate connectors, see [Certificate connectors](../protect/certificate-connectors.md).

<!-- ########################## -->
## Week of January 4, 2021

### App management

#### Browser access enabled automatically during Android work profile enrollment<!-- 5411101  -->

During new Android Enterprise personally owned work profile enrollments, browser access is now automatically enabled on the device. With this change, compliant devices can use the browser to access resources that are protected by conditional access without needing to take additional actions. Before this change, users had to launch the Company Portal and select **Settings** > **Enable Browser Access**, and then click **Enable**.

This change has no impact on devices that are already enrolled.

#### Win32 app download progress bar<!-- 5145837 -->

End users will now see a progress bar in the Windows Company Portal while a Win32 app is being downloaded. This feature will help customers better understand the app installation progress.

#### Update to Company Portal for Android app icon<!-- 7114401 -->

We've updated the Company Portal for Android app icon to create a more modern look and feel for device users. To see what the new icon looks like, go to the [Intune Company Portal listing on Google Play](https://go.microsoft.com/fwlink/?linkid=2151341).

<!-- ########################## -->
## Week of December 7, 2020

### Intune apps

#### Newly available protected apps for Intune<!-- 8766223 -->

The following protected apps are now available for Microsoft Intune:

- Dynamics 365 Remote Assist
- Box - Cloud Content Management
- STid Mobile ID
- FactSet 3.0
- Notate for Intune
- Field Service (Dynamics 365)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## What's New archive

For previous months, see the [What's New archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
