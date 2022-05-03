---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 05/02/2022
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

### Improved report data experience on the Managed Apps pane<!-- 10147133 -->
The **Managed Apps** pane will be updated to better display app data. You will be able to switch between displaying app data for the primary user and other users on a device, or display data for the device without any user. The generated app data will be displayed using the primary user of the device when the report is initially loaded, or displayed with no primary user if none exists. This capability will be available in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Managed Apps**.

### Photo library outgoing data transfer support via app protection policies<!-- 14062176 -->
You will be able to select to include **Photo Library** as a supported application storage service for *outgoing* data. This support is in addition to *incoming* data transfer support for **Photo Library**. By selecting **Photo Library** in the **Allow users to open data from selected services** setting within Intune, you can allow managed accounts to send *outgoing* data to their device's photo library from their managed apps on iOS and Android platforms. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App protection policies** > **Create Policy**. Choose either **iOS/iPadOS** or **Android**. This setting will be available as part of the **Data protection** step and specifically for **Policy managed apps**. For related information, see [Data protection](../apps/app-protection-framework.md#data-protection-2).

### Deploy macOS LOB apps by uploading PKG-type installer files<!-- 10671861 -->
The capability to deploy macOS LOB apps by uploading PKG-type installer files to Intune will be generally available. You can upload and deploy PKG-type installer files as macOS line-of-business apps. To add a macOS LOB app from [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **macOS** > **Add** > **Line-of-business app**. Additionally, the App Wrapping Tool for macOS will no longer be required to deploy macOS LOB apps.

### Use MAM policies with COSU devices<!-- 13819227 -->
Intune-managed Android Enterprise corporate owned dedicated devices (COSU) in Azure Active Directory (AAD) shared mode will be able to receive MAM policies and be targeted separately from other Android enterprise devices. For more information about COSU, see [Android Enterprise dedicated devices](../fundamentals/deployment-guide-enrollment-android.md#android-enterprise-dedicated-devices).

### Push notification will always be sent when device ownership changes from Personal to Corporate<!-- 12390037 -->
We’ll soon change push notification behavior to ensure a notification is always sent when an admin changes a devices ownership from Personal to Corporate. With this change, we’re removing the following setting from the [*Customization* node](../apps/company-portal-app.md#device-ownership-notification) of the Microsoft Endpoint Manager admin center, which currently allows admins to turn off this notification behavior:
- Send a push notification to users when their device ownership type changes from personal to corporate (Android and iOS/iPadOS only)​

These notifications are pushed through the Company Portal app on Android and iOS/iPadOS devices.

### iOS Company Portal minimum required version<!-- 13016075 -->
With an upcoming release of the MS Authenticator app, users will be required to update to v5.2205 of the iOS Company Portal. If you have enabled the **[Block installing apps using App Store](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised)** device restriction setting, you will likely need to push an update to the related devices that use this setting. Otherwise, no action is needed. If you have a helpdesk, you may want to make them aware of the prompt to update the Company Portal app. In most cases, users have app updates set to automatic, so they receive the updated Company Portal app without taking any action. Users that have an earlier app version will be prompted to update to the latest Company Portal app.

### iOS/iPadOS notifications will require March Company Portal or newer<!-- 14131757 -->
We plan to make service side updates to iOS/iPadOS notifications in Intune's May (2205) service release that will require users to have the March Company Portal (version 5.2203.1) or newer. If you are using functionality that could generate iOS/iPadOS Company Portal push notifications, you will want to ensure your users update the iOS/iPadOS Company Portal to continue receiving push notifications. There is no additional change in functionality. For related information, see [Update the Company Portal app](../user-help/install-a-new-version-of-the-company-portal-app.md).

<!-- ***********************************************-->

## Device management

### Support for Retire on Android Enterprise corporate-owned work-profiles devices<!-- 10216870 -->
You'll be able to use the **Retire** admin action in the **Endpoint Manager admin center**  to remove the work profile including all corporate apps, data, and policies from an Android Enterprise corporate-owned work profile device.  Go to **Endpoint Manager admin center** >**Devices** pane >**All Devices** > then select the name of the device you want to retire and select **Retire**.  

When you select **Retire**, the device is unenrolled from Intune management. However, all the data and apps associated with your personal profile will remain untouched on the device.
For more information, see [Retire or wipe devices using Microsoft Intune](../remote-actions/devices-wipe.md).

### Initiate compliance checks for your AOSP devices from the Microsoft Intune app<!-- 12645739 -->
You'll be able to initiate a compliance check for your AOSP devices from the Microsoft Intune app. Go to **Device details**. This feature will be available on devices that are enrolled in Microsoft Intune app as user-associated (Android) AOSP devices.

For more information, see [Enroll Android (AOSP) corporate-owned user associated devices](../enrollment/android-aosp-corporate-owned-user-associated-enroll.md)

### View a managed device's group membership<!-- 4100067 -->
In the monitor section of the **Devices** workload of Intune, you'll be able to view the group membership of all AAD groups for a managed device. When this is available, you will be able to select **Group Membership** by signing in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and selecting **Devices**.

<!-- ***********************************************-->

## Device enrollment

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

**System Updates > Software Update**:

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

[DevicePolicyManager - getRequiredStrongAuthTimeout method](https://developer.android.com/reference/android/app/admin/DevicePolicyManager#getRequiredStrongAuthTimeout(android.content.ComponentName)) (opens Android's web site)

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

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
