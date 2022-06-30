---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 07/01/2022
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

### Noncompliance details available for Android (AOSP) in Microsoft Intune app<!-- 12645770 -->
Android (AOSP) users will be able to view the reasons why devices are marked as noncompliant in the Microsoft Intune app. This information will be available in the Intune app for devices enrolled as user-associated Android (AOSP) devices.

### Android strong biometric change detection<!-- 9740832 -->
The Android **Fingerprint instead of PIN for access** setting in Intune, which allows the end-user to use [fingerprint authentication](https://developer.android.com/about/versions/marshmallow/android-6.0.html#fingerprint-authentication) instead of a PIN, is being modified. This change will allow you to require end-users to set strong biometrics, as well as require end-users to confirm their app protection policy (APP) PIN if a change in strong biometrics is detected. You can find Android app protection polices in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **App protection policies** > **Create policy** > **Android**.

### New app types for Microsoft Endpoint Manager<!-- 7210233 -->
As an admin, you will be able to create and assign two new types of Intune apps:
- **iOS/iPadOS web clip** 
- **Windows web link**

These new app types work in a similar way to the existing **web link** application type, however they apply only for their specific platform, whereas web link applications apply across all platforms. With these new app types, you can assign to groups and also use assignment filters to limit the scope of assignment. You will find this functionality in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), by selecting **Apps** > **All Apps** > **Add**.



<!-- ***********************************************-->

## Device management

Intune moving to support iOS/iPadOS 16 and higher later this year<!-- 14778947 -->
Later this year, Apple is expected to release iOS/iPadOS 16. Due to this expected release, Microsoft Intune and the Intune Company Portal will require iOS/iPadOS 14 and higher shortly after the release of iOS/iPad 16. For related information, see [Supported operating systems and browsers in Intune](../fundamentals/supported-devices-browsers.md).

Intune moving to support macOS 11.6 and higher later this year<!-- 14766663 -->
With Apple's expected release of macOS 13 Ventura later this year, Microsoft Intune, the Company Portal app, and the Intune MDM agent will be moving to support macOS 11.6 (Big Sur) and later. For related information, see [Supported operating systems and browsers in Intune](../fundamentals/supported-devices-browsers.md).

### Initiate compliance checks for your AOSP devices from the Microsoft Intune app<!--12645739 -->
You'll be able to initiate a compliance check for your AOSP devices from the Microsoft Intune app. Go to **Device details**. This feature will be available on devices that are enrolled in Microsoft Intune app as user-associated (Android) AOSP devices.

### New event viewers to assist in debugging WMI issues<!-- 14712854 -->
Intune’s remote action to [collect diagnostics](../remote-actions/collect-diagnostics.md#collect-diagnostics) will be expanded to collect details about Windows Management Instrumentation (WMI) app issues.

The new event viewers will include the following:
- Microsoft-Windows-WMI-Activity/Operational
- Microsoft-Windows-WinRM/Operational

For more information about Windows device diagnostics, see [Collect diagnostics from a Windows device](../remote-actions/collect-diagnostics.md).

### Monitor bootstrap escrow status on a Mac<!-- 12404441 -->  
A new macOS hardware property that you can monitor called **Bootstrap token escrowed** will be added to Microsoft Intune, and will report whether or not a bootstrap token has been escrowed on the device.

### Enable Common Criteria mode in Android Enterprise devices<!-- 13158881 -->
For Android Enterprise devices, you'll soon be able to create a device restrictions configuration profile that manages device settings (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** > **Fully managed, dedicated, and corporate-owned work profile** for platform > **Device restrictions** for profile type).

In the **System security**, there will be a new **Common Criteria mode** setting. These are an elevated set of security standards on a device which elevates security components on the device, including and not limited to:
- AES-GCM encryption of Bluetooth Long Term Keys
- Wi-Fi configuration stores
- Blocks bootloader download mode, the manual method for software updates
- Mandates additional key zeroization on key deletion
- Prevents non-authenticated Bluetooth connections
- Requires that FOTA updates have 2048-bit RSA-PSS signature

These configurations are typically required by only national security systems and other highly sensitive organizations.

For a list of the settings you can configure, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:
- Android 5.0 and newer
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)
- Android Enterprise corporate owned work profile (COPE)

<!-- ***********************************************-->

## Device enrollment

### Detect and manage hardware changes on Windows Autopilot devices <!-- 12795465 --> 
Microsoft Intune will alert you when it detects a hardware change on an Autopilot-registered device. You'll be able to view and manage all affected devices in the admin center. Additionally, you'll have the option to remove the affected device from Windows Autopilot and register it again so that the hardware change is accounted for.

### New authentication option for iOS/iPadOS automated device enrollment <!-- 12377183 -->
A new authentication option in Microsoft Intune will allow users going through automated device enrollment (ADE) to authenticate by signing in from another device.  This option will be available for iOS/iPadOS devices enrolling via Setup Assistant with modern authentication. The screen that prompts device users to authenticate will be embedded into Setup Assistant and shown to them during enrollment.

<!-- ***********************************************-->

## Device configuration

### Filter on the user scope or device scope in the Settings Catalog for Windows devices<!-- 13949975 -->
When you create a Settings Catalog policy, you can use **Add settings** > **Add filter** to filter settings based on the Windows OS edition (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Settings Catalog (preview)** for profile type).

When you **Add filter**, you'll be able to filter on the settings by user scope or device scope.

For more information, go to [Use the settings catalog to configure settings: Device scope vs. user scope settings](../configuration/settings-catalog.md#device-scope-vs-user-scope-settings)

Applies to:
- Windows 10
- Windows 11

### Certificate profiles support for Android (ASOP) devices<!-- 8506319, 8506363 -->
To expand our support for the Android Open Source Project (AOSP) platform, you’ll soon be able to deploy the following certificate profiles to corporate-owned and userless devices: 
- Trusted certificate profile
- PKCS certificate profile

### Import custom ADMX and ADML administrative templates to create a device configuration profile<!-- 4970862 -->
You can create a device configuration policy that uses built-in ADMX templates (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Administrative templates**).

You'll be able to import custom and 3rd party/partner ADMX and ADML templates into the Endpoint Manager admin center. Once imported, you can create a device configuration policy, assign the policy to your devices, and manage the settings in the policy.

For information on the built-in ADMX templates, see [Use Windows 10/11 templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md).

Applies to:
- Windows 11
- Windows 10

<!-- ***********************************************-->

## Device security

### Disable use of UDP connections on your Microsoft Tunnel Gateway servers<!-- 9295335 -->
You’ll soon be able to configure your Microsoft Tunnel Servers to disable use of UDP. When you disable use of UDP, the VPN server supports only TCP connections from tunnel clients. To support use of only TCP connections, your devices must use the generally available version of [Microsoft Defender for Endpoint as the Microsoft Tunnel client app](../protect/microsoft-tunnel-migrate-app.md) as the tunnel client app.

You’ll be able to disable UDP when creating or editing a *Server configuration* for Microsoft Tunnel Gateway. The Server configuration will support a new option named **Disable UDP Connections** that will be available for the *Server port* field.  [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant Administration** > **Microsoft Tunnel Gateway** > **Server configurations**.

### Reusable groups of settings for Microsoft Defender Firewall Rules<!-- 5653346, 6009514 -->
 
You’ll soon be able to add reusable groups of settings to your profiles for Microsoft Defender Firewall Rules. The reusable groups are collections of remote IP addresses and FQDNs that you define one time and can then use with one or more firewall rule profiles. You’ll no longer need to reconfigure the same group of IP addresses in each individual profile that might require them.  

Features of the reusable settings groups will include:  
- Add one or more remote IP addresses.  
- Add one or more FQDNs that can auto resolve to the remote IP address, or for one or more simple keywords when auto resolve for the group is off.  
- Use each settings group with one or more firewall rule profiles and the different  profiles can support different access configurations for the group.  

  For example, you can create two firewall rule profiles that reference the same reusable settings group and assign each profile to a different group of devices. The first profile can block access to all the remote IP addresses in the reusable settings group, while the second profile can be configured to allow access.  

- Edits to a settings group that's in use are automatically applied to the Firewall Rules profiles that use that group.  
  
Reusable groups will be configured on a new Tab for *Reusable settings* that will be available when you view endpoint security Firewall policy.  In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Endpoint security** > **Firewall**.

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
