---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 09/26/2022
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

### Global quiet time app policy settings<!-- 15424417 -->
The global quiet time settings will allow you to create policies to schedule quiet time for your end users which will automatically mute Microsoft Outlook email and Teams notifications on iOS/iPadOS and Android platforms. These policies can be used to limit end user notifications received after work hours. When this feature is available, you will be able to find it in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Quiet Time** > **Policies**.

### Select default work apps in Intune Company Portal<!-- 14531482 -->
Android device users will be able to select and save their preferred work apps in Intune Company Portal. They'll be able to select the default apps they want to use for a specific intent or file type, and change or remove their preferences. Company Portal will securely store the device user's preferred defaults. This feature is an enhancement to the Android MAM custom app picker, which is a part of the Android MAM SDK. 

### Use filters with app configuration profiles for managed devices<!-- 7423842 -->
You will be able to use filters to refine the assignment scope when deploying app configuration profiles for managed devices.
You can first create a filter using any of the available properties for iOS and Android. Then, in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) you can assign your managed app configuration profile by selecting **Apps** > **App configuration policies** > **Add** > **Managed devices** and go to the assignment page. After selecting a group, you can refine the applicability of the policy by choosing a filter and deciding to use it in **Include** or **Exclude** mode. For related information about filters, see [Use filters when assigning your apps, policies, and profiles in Microsoft Endpoint Manager](../fundamentals/filters.md).

## Device management

### New hardware details available for individual devices running on iOS/iPadOS<!-- 15038076 -->
Select **Devices** > **All devices** > *select one of your listed devices* and open it's **Hardware** details. The following new details are available in the **Hardware** pane of individual devices:

 - **Battery level**: Shows the battery level of the device anywhere between 0 and 100, or defaults to null if the battery level cannot be determined. This is available for devices running iOS/iPadOS 5.0 and later.
- **Resident users**: Shows the number of users currently on the shared iPad device, or defaults to null if the number of users cannot be determined. This is available for devices running iOS/iPadOS 13.4 and later.

For more information, see [View device details with Microsoft Intune](../remote-actions/device-inventory.md).

Applies to:
- iOS/iPadOS

### Endpoint security firewall rules support for ICMP type<!-- 5653356 -->
We’re adding a new setting named **IcmpTypesAndCodes** to the endpoint security firewall rules template for Windows 10. To configure this in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Endpoint security** > **Firewall** > **Create Policy** > Platform: *Windows 10, Windows 11, and Windows Server*  > Profile: *Microsoft Defender Firewall Rules*).

With this new setting you’ll be able to configure inbound and outbound rules for [Internet Control Message Protocol](/windows/security/threat-protection/windows-firewall/create-an-inbound-icmp-rule) (ICMP) as part of a firewall rule.

Applies to:  
- Windows 10, Windows 11, and Windows Server

###  Support for Locate device on Android Enterprise corporate owned fully managed and Android Enterprise corporate owned work profile devices<!-- 12391424 -->
You'll be able to use "Locate device" on Android Enterprise corporate owned fully managed and Android Enterprise corporate owned work profile devices. Using this feature, admins will be able to locate lost or stolen corporate devices on-demand. To do this, in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices**, and then select **All devices**. From the list of devices you manage, select a supported device, and choose the **Locate device** remote action.

For information on locating lost or stolen devices with Intune, go to:
 - [Locate lost or stolen devices with Intune](../remote-actions/device-locate.md)

Applies to:
- Android Enterprise corporate owned fully managed
- Android Enterprise corporate owned dedicated devices
- Android Enterprise corporate owned work profile

<!-- ***********************************************-->

## Device enrollment

### iOS/iPadOS Setup Assistant with modern authentication supports Just in Time Registration (public preview)<!-- 15515188 -->  
Intune will support Just in Time Registration for iOS/iPadOS enrollment scenarios that use Setup Assistant with modern authentication. Just in Time Registration reduces the number of authentication prompts shown to users throughout the provisioning experience, giving them a more seamless onboarding experience. It eliminates the need to have the Company Portal app for Azure AD registration and compliance checks, while automatically establishing SSO across the device. Just In Time Registration will be available in public preview for devices enrolling through Apple Automated Device Enrollment and running iOS/iPadOS 13.0 or later.

### Windows Autopilot diagnostics will capture ESP failures<!-- 1895390 -->
Windows Autopilot diagnostics will automatically capture diagnostics about Windows Autopilot failures that occur on the Enrollment Status Page (ESP). Diagnostics will be available to download in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  

<!-- ***********************************************-->

## Device configuration

### New settings for Device Firmware Configuration Interface (DFCI) profiles on Windows devices<!-- 15511597 -->
You can create a DFCI profile that enables the Windows OS to pass management commands from Intune to UEFI (Unified Extensible Firmware Interface) (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates > Device Firmware Configuration Interface**). 

You can use this feature to control BIOS settings. There will be new settings you can configure in the DFCI policy:

- Cameras:
  - Front camera
  - Infrared camera
  - Rear camera

- Radios:
  - WWAN
  - NFC

- Ports
  - SD Card

For more information on DFCI profiles, go to [Use Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md) and [DFCI profile settings list](../configuration/device-firmware-configuration-interface-windows-settings.md).

Applies to:
- Windows 11 on supported UEFI
- Windows 10 RS5 (1809) and later on supported UEFI

### New settings available in the iOS/iPadOS and macOS Settings Catalog<!-- 15514929 -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. 

New settings are available in the Settings Catalog. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

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

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Filter app and group policy assignments using Windows 11 SE operating system SKUs<!-- 10588651 -->
When you assign an app or policy, you can filter the assignment using different device properties, such as device manufacturer, operating system SKU, and more.

Two new Windows 11 SE operating system SKU's will added. You'll be able to use these SKUs in your assignment filters to include or exclude Windows 11 SE devices from applying group-targeted policies and applications.

For more information on filters and the device properties you can currently use, go to:
- [Use filters when assigning your apps, policies, and profiles in Microsoft Endpoint Manager](filters.md)
- [Device properties, operators, and rule editing when creating filters in Microsoft Endpoint Manager](filters-device-properties.md)

Applies to:
- Windows 11 SE

### New password complexity requirements for Android Enterprise 12+ personally owned devices with a work profile<!-- 12436068 -->
On Android Enterprise 11 and older personally owned devices with a work profile, you can set the **Required password type** and a **Minimum password length** in device configuration profiles and compliance policies.

Google is deprecating these features for Android 12+ personally owned devices with a work profile and replacing them with new password complexity requirements. For more information about this change, go to [Day zero support for Android 13](https://aka.ms/Intune/Android13).

The new **Password complexity** setting will have the following options:

- **Not configured**: Intune doesn't change or update this setting. By default, the OS may not require a password.
- **Low**: Pattern or PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked.
- **Medium**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length, alphabetic length, or alphanumeric length must be at least 4 characters.
- **High**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length must be at least 8 characters. The alphabetic or alphanumeric length must be at least 6 characters.

If you currently use the **Required password type** and **Minimum password length** settings in your device configuration and compliance policies on Android 12+, then we recommend using the new **Password complexity** setting instead.

If you continue to use the **Required password type** and **Minimum password length** settings, and don't configure the **Password complexity** setting, then new devices running Android 12+ will default to the **High** password complexity.

There is no impact for existing devices with the **Required password type** and **Minimum password length** settings configured.

For more information on the existing settings you can configure, go to:

- [Android Enterprise personally owned devices with a work profile - configuration profile settings list](../configuration/device-restrictions-android-for-work.md#personally-owned-devices-with-a-work-profile)
- [Android Enterprise personally owned devices with a work profile - compliance policy settings list](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile)

Applies to:
- Android 12.0 and newer
- Android Enterprise personally owned devices with a work profile

<!-- ***********************************************-->

## Device security

### Grant apps permission on Android Enterprise devices<!-- 12441244 -->
For Android Enterprise devices, you’ll soon be able to configure certificate profiles to silently grant specific apps access to use the certificate. This expands on the current behavior where a device user must approve the use of a certificate by an application.

You’ll be able to choose to grant certificate access silently to specific apps or to require user approval. When configured for specific apps, you’ll then select which apps have this access as part of the profile, while all other apps will continue to require user approval before being able to use the certificate.

This support will be added to profiles for SCEP, PKCS, PKCS imported, and Derived Credential certificate profiles.

Applies to:  
- Android Enterprise devices that enroll as Fully Managed, Dedicated, and Corporate-Owned work Profile.

### Attack surface reduction rule exclusions on a per-rule basis<!-- 13385644 -->
Attack surface reduction rules provide valuable controls for protecting your devices. Currently, exclusions are only supported for all of the rules that are enabled on the device.

With Intune, you’ll soon be able to configure exclusions for your [attack surface reduction rules](../protect/endpoint-security-asr-policy.md) on a per-rule basis. This will allow you to define exclusions for individual rules versus an exclusion that applies to all of the attack surface reduction rules on a device.

Applies to:  
- Windows 10/11

### Manage macOS software updates with Intune<!-- 9801186 -->
You’ll soon be able to use Intune policies to manage macOS software updates for devices that enrolled using Automated Device Enrollment (ADE). The policy will be available in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) at **Devices** > **macOS** > **Update policies for macOS**.
 
Supported update types will include:
- Critical updates
- Firmware updates
- Configuration file updates
- All other updates (OS, built-in apps)

In addition to scheduling when a device updates, you’ll be able to manage behaviors like the following:
- Download and install: Download or install the update, depending on the current state.
- Download only: Download the software update without installing it.
- Install immediately: Download the software update and trigger the restart countdown notification.
- Notify only:  Download the software update and notify the user through the App Store.
- Install later: Download the software update and install it at a later time.
- Not configured: No action taken on the software update. 

For information from Apple about managing macOS software updates, see [Manage software updates for Apple devices - Apple Support](https://support.apple.com/guide/deployment/manage-software-updates-depc4c80847a/web) in the Apple's Platform Deployment documentation.
Apple maintains a list of security updates at [Apple security updates - Apple Support](https://support.apple.com/en-us/HT201222). 

### Reusable groups of settings for removable storage in Device Control profiles<!-- 7351534 -->
You’ll soon be able to add reusable groups of settings to your profiles for device control profiles in your attack surface reduction policies. To configure device control profiles, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Endpoint security** >**Attack surface reduction** > **Create Policy** > Platform: *Windows 10 and later* > Profile: *Device Control*.
 
The reusable groups for device control profiles will include a collection of settings that support managing *read*, *write*, and *execute* access for removable storage. Examples of common scenarios include:
- Prevent write and execute access to all but allow specific approved USBs
- Audit write and execute access to all but block specific unapproved USBs
- Only allow specific user groups to access specific removable storage on a shared PC

Applies to:  
- Windows 10 or later

### Reusable groups of settings for Microsoft Defender Firewall Rules<!-- 5653346, 6009541 -->
 You’ll soon be able to add reusable groups of settings to your profiles for Microsoft Defender Firewall Rules. The reusable groups are collections of remote IP addresses and FQDNs that you define one time and can then use with one or more firewall rule profiles. You’ll no longer need to reconfigure the same group of IP addresses in each individual profile that might require them.  

Features of the reusable settings groups will include:  
- Add one or more remote IP addresses.  
- Add one or more FQDNs that can auto resolve to the remote IP address, or for one or more simple keywords when auto resolve for the group is off.  
- Use each settings group with one or more firewall rule profiles and the different  profiles can support different access configurations for the group.  

  For example, you can create two firewall rule profiles that reference the same reusable settings group and assign each profile to a different group of devices. The first profile can block access to all the remote IP addresses in the reusable settings group, while the second profile can be configured to allow access.  

- Edits to a settings group that's in use are automatically applied to the Firewall Rules profiles that use that group.  
  
Reusable groups will be configured on a new Tab for *Reusable settings* that will be available when you view endpoint security Firewall policy.  In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Endpoint security** > **Firewall**.

<!-- ***********************************************-->

## Monitor and troubleshoot

### Open Help and Support without losing your context in the Microsoft Endpoint Manager admin center<!-- 12469338 -->
You’ll soon be able to use the **?** icon in the Microsoft Endpoint Manager admin center to  open a help and support session without losing your current node of focus in the admin center. The **?** icon is always available in the upper right of the admin center title bar. This change will add an additional method for accessing *Help and support*.

When you select  **?**, the admin center will open a new and separate side-by-side pane you use to navigate the support experience. By opening this separate pane, you’ll be free to navigate the support experience without affecting your original location and focus on the admin center. You will however be free to navigate through the admin center in that original pane if you choose.

<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
