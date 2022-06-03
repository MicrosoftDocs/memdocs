---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 06/03/2022
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

### New app types for Microsoft Endpoint Manager<!-- 7210233 -->
As an admin, you will be able to create and assign two new types of Intune apps:
- **iOS/iPadOS web clip** 
- **Windows web link**

These new app types work in a similar way to the existing **web link** application type, however they apply only for their specific platform, whereas web link applications apply across all platforms. With these new app types, you can assign to groups and also use assignment filters to limit the scope of assignment. You will find this functionality in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), by selecting **Apps** > **All Apps** > **Add**.

Private preview will be after 2206 UX update (with flighting) and GA will be after that (OOB 2206 or 2207 depending on feedback and issues).

### Enterprise feedback policies for Web Company Portal<!-- 9846764 -->
Feedback settings will be provided to address M365 enterprise feedback policies for the currently logged in user via the Microsoft 365 Apps Admin Center. The settings are used to determine whether feedback can be enabled or must be disabled for a user in the Web Company Portal.

### Photo library outgoing data transfer support via app protection policies<!-- 14062176 -->
You will be able to select to include **Photo Library** as a supported application storage service for *outgoing* data. This support is in addition to *incoming* data transfer support for **Photo Library**. By selecting **Photo Library** in the **Allow users to open data from selected services** setting within Intune, you can allow managed accounts to send *outgoing* data to their device's photo library from their managed apps on iOS and Android platforms. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App protection policies** > **Create Policy**. Choose either **iOS/iPadOS** or **Android**. This setting will be available as part of the **Data protection** step and specifically for **Policy managed apps**. For related information, see [Data protection](../apps/app-protection-framework.md#data-protection-2).

### Use App Protection Policies with Android Enterprise dedicated devices and Android (AOSP) devices<!-- 13819227 -->
Intune-managed Android Enterprise dedicated devices enrolled with Azure Active Directory (Azure AD) shared mode and Android (AOSP) devices will be able to receive app protection policies policies and can be targeted separately from other Android device types. For more information about Android Enterprise dedicated devices and Android (AOSP), see [Android Enterprise dedicated devices](../fundamentals/deployment-guide-enrollment-android.md#android-enterprise-dedicated-devices).

### Push notification will always be sent when device ownership changes from Personal to Corporate<!-- 12390037 -->
We’ll soon change push notification behavior to ensure a notification is always sent when an admin changes a device's ownership from Personal to Corporate. With this change, we’re removing the option to send a push notification to users when their device ownership type changes from personal to corporate (Android and iOS/iPadOS) in Microsoft Endpoint Manager admin center. Previously, admins were allowed to turn off this notification behavior. These notifications are pushed through the Company Portal app on Android and iOS/iPadOS devices.

### iOS Company Portal minimum required version<!-- 13016075 -->
With an upcoming release of the MS Authenticator app, users will be required to update to v5.2205 of the iOS Company Portal. If you have enabled the **[Block installing apps using App Store](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised)** device restriction setting, you will likely need to push an update to the related devices that use this setting. Otherwise, no action is needed. If you have a helpdesk, you may want to make them aware of the prompt to update the Company Portal app. In most cases, users have app updates set to automatic, so they receive the updated Company Portal app without taking any action. Users that have an earlier app version will be prompted to update to the latest Company Portal app.

<!-- ***********************************************-->

## Device management

### User configuration support for  Windows 11 multi-session VMs will be public preview.<!-- 7231329 --> 
You'll be able to:
- Configure user scope policies using **Settings catalog** and assign to groups of users
- Configure user certificates and assign to users
- Configure PowerShell scripts to install in the user context and assign to users

Applies to: 
- Windows 11

[!Note]: User support for Windows 10 multi-session builds will be available later this year.

For more information, see [Using Azure Virtual Desktop multi-session with Microsoft Intune](../fundamentals/azure-virtual-desktop-multi-session.md)

### Remotely restart and shut down macOS device <!-- 12472418 -->
You'll be able to remotely restart or shutdown a macOS device using device actions. These device actions are available for devices running macOS 10.13 and later. 
For more information, see [Restart devices with Microsoft Intune](../remote-actions/device-restart.md).

### Additional Remote actions for Android (AOSP) Corporate devices<!-- 8504019 -->
For Android Open Source Project (AOSP) Corporate devices, you can soon leverage additional remote actions from the Microsoft Endpoint Manager admin center - Reboot and Remote lock. 

For information about these features, see:

 - [Remotely restart devices with Intune](../remote-actions/device-restart.md)
 - [Remotely lock devices with Intune](../remote-actions/device-remote-lock.md).

Applies to:
- Android Open Source Project (AOSP)


### Cleaner view of certificate details when viewing certificate reports<!-- 13316515 -->
We’re changing what Intune displays when you view certificate details for devices and certificate profiles. [Microsoft Endpoint Manager admin center]( https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Monitor** > **Certificates**. 

Today, the certificate reports can show certificates that are no longer valid, or that are no longer on a device. With this change, you’ll won't see information for those invalid certificates. Instead, Intune displays only those that are valid, that were revoked within the last 30 days, or that expired within the last 30 days will be shown.

### Support for Retire on Android Enterprise corporate-owned work-profiles devices<!-- 10216870 -->
You'll be able to use the **Retire** admin action in the **Endpoint Manager admin center**  to remove the work profile including all corporate apps, data, and policies from an Android Enterprise corporate-owned work profile device.  Go to **Endpoint Manager admin center** >**Devices** pane >**All Devices** > then select the name of the device you want to retire and select **Retire**.  

When you select **Retire**, the device is unenrolled from Intune management. However, all the data and apps associated with your personal profile will remain untouched on the device.
For more information, see [Retire or wipe devices using Microsoft Intune](../remote-actions/devices-wipe.md).

### View a managed device's group membership<!-- 4100067 -->
In the monitor section of the **Devices** workload of Intune, you'll be able to view the group membership of all AAD groups for a managed device. When this is available, you will be able to select **Group Membership** by signing in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and selecting **Devices**.

<!-- ***********************************************-->

## Device enrollment

### Utilize bootstrap tokens on macOS devices <!-- 12693392 -->
Bootstrap token support, currently in public preview, will become available to all Microsoft Intune customers, including GCC High and Microsoft Azure Government Cloud tenants. Intune supports the use of bootstrap tokens on enrolled devices running macOS, version 10.15 or later. 

Bootstrap tokens allow for non-admin users to have increased MDM permissions, and perform specific software functions on behalf of the IT admin.  Bootstrap tokens will be supported on:  
- Supervised devices (in Intune, that's all user-approved enrollments)  
- Devices enrolled in Intune via Apple automated device enrollment   

For more information about how bootstrap tokens work with Intune, see [Set up enrollment for macOS devices](../enrollment/macos-enroll.md).  

### UI improvements when Android enrollment is available but not required<!-- 8764312  -->
We're updating the iconography users see in the Company Portal for Android when *Device enrollment* for *End user experiences* on your Intune tenants *Customization* page is set to **Available, no prompts**. The changes will make it easier for users to recognize when enrollment is available to them, but not required.   

### Enroll to co-management from Windows Autopilot<!-- 11300628 -->
You'll be able to configure device enrollment in Intune to enable co-management, which happens during the [Windows Autopilot](../../autopilot/windows-autopilot.md) process. This behavior directs the workload authority in an orchestrated manner between Configuration Manager and Intune.

If the device is targeted with an [Autopilot enrollment status page (ESP) policy](../enrollment/windows-enrollment-status.md), the device will wait for Configuration Manager. The Configuration Manager client installs, registers with the site, and applies the production co-management policy. Then the Autopilot ESP continues.

### Improvements for enrollment profiles for Apple Automated Device Enrollment<!-- 13165752 -->
Two Setup Assistant skip panes are becoming generally available for Apple Automated Device Enrollment (ADE). The screen configurations were previously released in Intune for public preview. The following screens will be generally available for both iOS/iPadOS and macOS under the **Setup Assistant** tab:  
  
- iOS/iPadOS 13 and later
   - Pane name: **Get Started ** 
  - Default: Show pane 
  - You can configure a setting in Intune that hides the Get Started pane in Setup Assistant during ADE enrollment.
  
- macOS 12 and later 
   - Pane name: **Auto Unlock with Apple Watch** 
  - Default: Show pane
  - You can configure a setting in Intune that hides the Unlock Your Mac with your Apple Watch pane in Setup Assistant during ADE enrollment.  

There is no change to functionality from the previous public preview release. 

<!-- ***********************************************-->

## Device configuration

### New macOS settings in Settings Catalog <!-- 14158964 -->
The Settings Catalog has new macOS settings you can configure (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform >**Settings catalog (preview)** for profile type):

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
- Autohide
- Autohide Immutable
- Contents Immutable
- Double Click Behavior
- Double Click Behavior Immutable
- Large Size
- Launch Animation
- Launch Animation Immutable
- Magnification
- Magnify Immutable
- Magsize Immutable
- MCX Dock Special Folders
- Minimize Effect
- Minimize Effect Immutable
- Minimize To Application
- Minimize To Application Immutable
- Orientation
- Persistent Apps
- Position Immutable
- Show Process Indicators
- Show Indicators Immutable
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

- Desktop Schedule
- Repeating Power Off
- Repeating Power On
- Desktop AC Power
- Portable Battery Power
- Portable AC Power
- Destroy FV Key On Standby
- Sleep Disabled

**System Configuration > System Logging**:

- Enable Private Data

**System Configuration > System Extensions**:

- Removable System Extensions

**System Configuration > Time Server**:

- Time Server
- Time Zone

The following settings are also in Settings Catalog. Previously, they were only available in Templates:

**Security > Passcode**:

- Allow Simple Passcode
- Change At Next Auth
- Expiration In Days
- Force Pin
- Lock After Inactivity Minutes
- Max Failed Attempts
- Max Grace Period
- Min Complex Chars
- Min Length
- Minutes Until Failed Login Reset
- Passcode History
- Require Alphanumeric Passcode

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

**System Configuration > System Extensions**:

- Allow User Overrides
- Allowed System Extension Types
- Allowed System Extensions
- Allowed Team Identifiers

There isn't any conflict resolution between policies created using the Settings catalog and policies created using Templates. When creating new policies in the Settings Catalog, be sure there are no conflicting settings with your current policies.

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog in Microsoft Intune](../configuration/settings-catalog.md).

Applies to:
- macOS

### Unlock the work profile on Android Enterprise corporate owned work profile (COPE) devices after a set time using password, PIN, or pattern<!-- 14133548 -->
On Android Enterprise devices, you can create a device restrictions configuration profile that manages device settings (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** > **Fully managed, dedicated, and corporate-owned work profile** for platform > **Device restrictions** for profile type).

On Android Enterprise devices, you can configure the **How often pin, password, or pattern is needed to unlock** setting. This setting will also be available for the work profile on Android Enterprise COPE devices.

For more information on this setting, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android 8.0 and newer
- Android Enterprise corporate owned work profile (COPE)

### Use TEAP authentication in wired networks device configuration profiles for Windows devices<!-- 14042602 -->
On Windows devices, you can create a **Wired Networks** device configuration profile that supports the Extensible Authentication Protocol (EAP) (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Wired networks** for profile type).

When you create the profile, you'll be able to use the Tunnel Extensible Authentication Protocol (TEAP).

For more information on wired networks, go to [Add and use wired networks settings on your macOS and Windows devices in Microsoft Intune](../configuration/wired-networks-configure.md).

Applies to:
- Windows 11
- Windows 10

### Filter on the user scope or device scope in the Settings Catalog for Windows devices<!-- 13949975 -->
When you create a Settings Catalog policy, you can use **Add settings** > **Add filter** to filter settings based on the Windows OS edition (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Settings Catalog (preview)** for profile type).

When you **Add filter**, you'll be able to filter on the settings by user scope or device scope.

For more information, go to [Use the settings catalog to configure settings: Device scope vs. user scope settings](../configuration/settings-catalog.md#device-scope-vs-user-scope-settings)

Applies to:
- Windows 10
- Windows 11

### iOS/iPadOS platform is in Settings Catalog <!-- 13934066 -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. The iOS/iPadOS platform and some settings are now available in the Settings Catalog (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Settings catalog (preview)** for profile type).

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

- **Managed Devices > Profile Removal Password**:

- Removal Password

**Networking > Cellular**:

- APNs
- Attach APN

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

**App Management > AppLock**:

- App Identifier
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
- Allow Assistive Touch Adjustment
- Allow Invert Colors Adjustment
- Allow Voice Control Adjustment
- Allow Voice Over Adjustment
- Allow Zoom Adjustment

**Networking > Domains**:

- Email Domains
- Safari Password Auto Fill Domains
- Web Domains

**Networking > DNS Settings**:

- DNS Protocol
- Server Addresses
- Server Name
- Server URL
- Supplemental Match Domains
- Action
- Action Parameters
- DNS Domain Match
- DNS Server Address Match
- Interface Type Match
- SSID Match
- URL String Probe

**Networking > Network Usage Rules**:

- Allow Cellular Data
- Allow Roaming Cellular Data
- App Identifier Matches

**Printing > Air Print**:

- Printers
- Force TLS
- IP Address
- Port
- Resource Path

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
- Allow Automatic Screen Saver
- Allow Bluetooth Modification
- Allow Bookstore
- Allow Bookstore Explicit Books
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
- Allow Wifi Power Modification
- Allow iTunes
- Autonomous Single App Mode Permitted App IDs
- Blocked App Bundle IDs
- Enforced Software Update Delay
- Enforced Software Update Major OS Deferred Install Delay
- Enforced Software Update Minor OS Deferred Install Delay
- Enforced Software Update Non OS Deferred Install Delay
- Force Air Drop Unmanaged
- Force Air Play Outgoing Requests Pairing Password
- Force Air Print Trusted TLS Requirement
- Force Assistant Profanity Filter
- Force Authentication Before Auto Fill
- Force Automatic Date And Time
- Force Classroom Automatically Join Classes
- Force Classroom Request Permission To Leave Classes
- Force Classroom Unprompted App And Device Lock
- Force Classroom Unprompted Screen Observation
- Force Delayed Major Software Updates
- Force Delayed Software Updates
- Force Encrypted Backup
- Force iTunes Store Password Entry
- Force Limit Ad Tracking
- Force On Device Only Dictation
- Force On Device Only Translation
- Force Unprompted Managed Classroom Screen Observation
- Force Watch Wrist Detection
- Force WiFi Power On
- Force WiFi To Allowed Networks Only
- Force WiFi Whitelisting
- Require Managed Pasteboard
- Safari Accept Cookies Double
- Safari Allow Autofill
- Safari Allow Java Script
- Safari Allow Popups
- Safari Force Fraud Warning

**Security > Passcode**:

- Allow Simple Passcode
- Expiration In Days
- Force Pin
- Lock After Inactivity Minutes
- Max Failed Attempts
- Max Grace Period
- Min Complex Chars
- Min Length
- Passcode History
- Require Alphanumeric Passcode

**System Configuration > Lock Screen Message**:

- Asset Tag Information
- Lock Screen Footnote

**User Experience > Notifications**:

- Alert Type
- Badges Enabled
- Bundle Identifier
- Critical Alert Enabled
- Grouping Type
- Notifications Enabled
- Preview Type
- Show In Car Play
- Show In Lock Screen
- Show In Notification Center
- Sounds Enabled

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:
- iOS/iPadOS

### Add custom support information to Android Enterprise devices<!-- 7913128 -->
On Android Enterprise devices, you can create a device restrictions configuration profile that manages device settings (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** > **Fully managed, dedicated, and corporate-owned work profile** for platform > **Device restrictions** for profile type).

There will be some new settings you can configure:

- **Short support message**: When users try to change a managed setting, you can add a short message that's shown to users in a system dialog window.
- **Long support message**: You can add a long message that's shown in **Settings** > **Security** > **Device admin apps** > **Device Policy**.

By default, the OEM default messages are shown. When you deploy a custom message, the Intune default message is also deployed. If you don't enter a custom message for the device's default language, then the Intune default message is shown. 

For example, you deploy a custom message for English and French. The user changes the device's default language to Spanish. Since you didn't deploy a custom message to the Spanish language, the Intune default message is shown.

The Intune default message is translated for all languages in the Endpoint Manger admin center (**Settings** > **Language + Region**). The **Language** setting value determines the default language used by Intune. By default, it's set to **English**.

In the policy, you can customize the messages for the following languages:

- Arabic
- Bulgarian
- Czech
- Danish
- German
- Greek
- English (United Kingdom)
- English (United States)
- Spanish (Spain)
- Spanish (Mexico)
- Estonian
- Finnish
- French (Canada)
- French (France)
- Hebrew
- Croatian
- Hungarian
- Italian
- Japanese
- Korean
- Lithuanian
- Latvian
- Norwegian, Bokmål
- Dutch
- Polish
- Portuguese (Brazil)
- Portuguese (Portugal)
- Romanian
- Slovak
- Slovenian
- Russian
- Serbian
- Swedish
- Thailand
- Turkish
- Ukrainian
- Chinese (Simplified)
- Chinese (Traditional)

For a list of settings you can currently configure, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android 7.0 and newer
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)
- Android Enterprise corporate owned work profile (COPE)

### New settings for DFCI profiles on Windows 10/11 devices<!-- 6039135 -->
On Windows 10/11 devices, you can create a Device Firmware Configuration Interface (DFCI) profile (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type).

DFCI profiles lets Intune pass management commands to UEFI (Unified Extensible Firmware Interface) using the DFCI firmware layer. This additional firmware layer makes configuration more resilient to malicious attacks. DFCI also limits end users' control over the BIOS by graying out managed settings.

There will be new settings you can configure:

- **Built-in hardware**:
  - Front cameras
  - Rear cameras
  - Infrared (IR) cameras

- **Built-in hardware**:
  - Microphones
  - Speakers

- **Built-in hardware**:
  - Bluetooth
  - WWAN
  - NFC
  - Wi-Fi

- **Ports**:
  - USB type A
  - USB type C
  - SD card

- **Wake on LAN**
- **Wake on power**

For more information on the DFCI profile, go to [Use Device Firmware Configuration Interface profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md).

Applies to:
- Windows 10/11

### Settings catalog for macOS and Windows is generally available (GA) <!-- 9558656 -->
The settings catalog will be generally available (GA). For more information on the settings catalog, go to [Use the settings catalog to configure settings on Windows and macOS devices](../configuration/settings-catalog.md)

Applies to:
- macOS
- Windows 10/11

### New Microsoft Office and Microsoft Outlook preference settings in the macOS Settings Catalog <!-- 14193331 -->
The Settings Catalog now supports preference settings for Microsoft Office and Microsoft Outlook (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform >**Settings catalog (preview)** for profile type). 

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

For more information about Microsoft Office settings, see [Use preferences to manage privacy controls for Office for Mac - Deploy Office](/deployoffice/privacy/mac-privacy-preferences#preference-setting-for-connected-experiences-that-download-online-content).

For more information about Microsoft Outlook settings, see [Set preferences for Outlook for Mac - Deploy Office](/deployoffice/mac/preferences-outlook).

For more information about configuring Settings catalog profiles in Intune, see [Create a policy using settings catalog in Microsoft Intune](../configuration/settings-catalog.md).

Applies to:

- macOS

### Certificate profiles support for Android (ASOP) devices<!-- 8506319, 8506363 -->
To expand our support for the Android Open Source Project (AOSP) platform, you’ll soon be able to deploy the following certificate profiles to corporate-owned and userless devices: 
- Trusted certificate profile
- PKCS certificate profile


### New macOS settings in the Settings Catalog<!-- 13923348 -->
The Settings Catalog has new macOS settings you can configure (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform >**Settings catalog (preview)** for profile type):

**Accounts > Accounts**:

- Disable Guest Account
- Enable Guest Account

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

### Create and deploy Wi-Fi profiles to Android AOSP devices<!-- 8506299 -->
You'll be able to configure and deploy a Wi-Fi profile to your Android AOSP devices.

Applies to:
- Android (AOSP)

### Unlock Android Enterprise devices after a set time using password, PIN, or pattern<!-- 7913163 -->
On Android Enterprise devices, you can create a device restrictions configuration profile that manages device settings (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** > **Fully managed, dedicated, and corporate-owned work profile** for platform > **Device restrictions** for profile type).

There will be a new **How often pin, password, or pattern is needed to unlock** setting. Select how long users must unlock the device using a strong authentication method (password, PIN, or pattern). Your options:
- **24 hours since last pin, password, or pattern unlock**: The screen locks 24 hours after users last used a strong authentication method to unlock the device or work profile.
- **Device default** (default): The screen locks using the device's default time.

For a list of settings you can currently configure, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

[2.3.4. Advanced passcode management](https://developers.google.com/android/work/requirements#2.3.-advanced-passcode-management_1) (opens Android's web site)

Applies to:
- Android 8.0 and newer
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)
- Android Enterprise corporate owned work profile (COPE)

### Import custom ADMX and ADML administrative templates to create a device configuration profile<!-- 4970862 -->
You can create a device configuration policy that uses built-in ADMX templates (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Administrative templates**).

You'll be able to import custom and 3rd party/partner ADMX and ADML templates into the Endpoint Manager admin center. Once imported, you can create a device configuration policy, assign the policy to your devices, and manage the settings in the policy.

For information on the built-in ADMX templates, see [Use Windows 10/11 templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md).

Applies to:
- Windows 11
- Windows 10

### Use the Settings Catalog to create a Universal Print policy on Windows 11 devices<!-- 5513123 -->
Many organizations are moving their printer infrastructure to the cloud. [Universal Print](/universal-print/fundamentals/universal-print-whatis) is a cloud-based printing solution for Microsoft 365 customers. It uses built-in cloud printers, built-in legacy printers, and runs entirely in Microsoft Azure. When Universal Print is deployed with Universal Print-compatible printers, it doesn't require any on-premises infrastructure. 

In the Endpoint Manager admin center, you'll be able to use the Settings Catalog to create a printer policy (**Device configuration** > **Create profile** > **Windows 10 and later** for platform > **Settings catalog** for profile type > **Printer provisioning**). When you deploy the policy, users select the printer from a list of registered Universal Print printers, and can also select a default printer.

Currently, you must use the [Universal Print printer provisioning tool](/universal-print/fundamentals/universal-print-intune-tool), which requires more manual steps, and has some limitations.

Applies to:
- Windows 11

<!-- ***********************************************-->

## Device security

### Users assigned the Endpoint Security Manager admin role can modify Mobile Threat Defense connector settings<!-- 14179885  -->
We’re expanding the scope of the Endpoint Security Manager built-in admin role to include the capability to modify the [Mobile Threat Defense connector](../protect/mtd-connector-enable.md) (MTD connector) settings for your Tenant.

Before these permissions change, we recommend you review the users that are assigned to the *Endpoint Security Manager* role for your tenant. If any should not have permissions to edit the MTD connector settings, then update their role permissions or [create a custom role](../fundamentals/create-custom-role.md) to only allow read permissions for MTD connectors settings.

[Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Roles** > **Endpoint Security Manager** > **Assignments**.

### Reusable groups of settings for Microsoft Defender Firewall Rules<!-- 5653346, 6009514 -->
 
You’ll soon be able to add reusable groups of settings to your profiles for Microsoft Defender Firewall Rules. The reusable groups are collections of remote IP addresses and FQDNs that you define one time and can then use with one or more firewall rule profiles. You’ll no longer need to reconfigure the same group of IP addresses in each individual profile that might require them.  

Features of the reusable settings groups will include:  
- Add one or more remote IP addresses.  
- Add one or more FQDNs that can auto resolve to the remote IP address, or for one or more simple keywords when auto resolve for the group is off.  
- Use each settings group with one or more firewall rule profiles and the different  profiles can support different access configurations for the group.  

  For example, you can create two firewall rule profiles that reference the same reusable settings group and assign each profile to a different group of devices. The first profile can block access to all the remote IP addresses in the reusable settings group, while the second profile can be configured to allow access.  

- Edits to a settings group that's in use are automatically applied to the Firewall Rules profiles that use that group.  
  
Reusable groups will be configured on a new Tab for *Reusable settings* that will be available when you view endpoint security Firewall policy.  In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Endpoint security** > **Firewall**.

### New settings to manage removable devices for Endpoint security Device control profiles<!-- 8844611 -->
We’re adding five new settings for Windows 10/11 to the [*device control* profile template](../protect/endpoint-security-asr-profile-settings.md#device-control) for Attack surface reduction policy in Endpoint Security. The new settings will help you manage the use of removable devices like a USB device, and to manage read and write access to removable disks like media players, cellular phones, displays, and CE devices.
 
 The new settings include: 
- [ADMX_DeviceInstallation/DeviceInstall_Removable_Deny](/windows/client-management/mdm/policy-csp-admx-deviceinstallation?WT.mc_id=Portal-fx#admx-deviceinstallation-deviceinstall-removable-deny)
-  [ADMX_RemovableStorage/WPDDevices_DenyRead_Access_2](/windows/client-management/mdm/policy-csp-admx-removablestorage?WT.mc_id=Portal-fx#admx-removablestorage-wpddevices-denyread-access-2)
-  [ADMX_RemovableStorage/WPDDevices_DenyRead_Access_1](/windows/client-management/mdm/policy-csp-admx-removablestorage?WT.mc_id=Portal-fx#admx-removablestorage-wpddevices-denyread-access-1)
-  [ADMX_RemovableStorage/WPDDevices_DenyWrite_Access_2](/windows/client-management/mdm/policy-csp-admx-removablestorage?WT.mc_id=Portal-fx#admx-removablestorage-wpddevices-denywrite-access-2)
-  [ADMX_RemovableStorage/WPDDevices_DenyWrite_Access_1](/windows/client-management/mdm/policy-csp-admx-removablestorage?WT.mc_id=Portal-fx#admx-removablestorage-wpddevices-denywrite-access-1)


### Microsoft Defender for Endpoint as the Tunnel client app for iOS will soon be out of Preview<!-- 9849514 --> 
The preview version of Microsoft Defender for Endpoint that supports [Microsoft Tunnel](../protect/microsoft-tunnel-overview.md) on iOS/iPadOS will soon be out of preview and become generally available.

When the Microsoft Defender for Endpoint app with support for Microsoft Tunnel becomes generally available for iOS, the standalone tunnel client app for iOS will be deprecated with support ending 60 days later.

If you are using the standalone tunnel app for iOS, prepare for this change by planning to [migrate to the Microsoft Defender for Endpoint app](../protect/microsoft-tunnel-migrate-app.md) before support for the standalone app ends.

## Monitor and troubleshoot

### Use Collect diagnostics to collect details about Windows expedited updates<!--  14337387 -->
Intune’s remote action to [*Collect diagnostics*](../remote-actions/collect-diagnostics.md) will soon collect additional details about [Windows expedited updates](../protect/windows-10-expedite-updates.md) that you deploy to devices.  (**Devices** > **Windows** > *select a device* > **Collect diagnostics**)  This information can be of use when troubleshooting problems with expedited updates.

The new details that will be collected include: 
- Files:  `C:\Program Files\Microsoft Update Health Tools\Logs\*.etl`
- Registry Keys:   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CloudManagedUpdate`

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
