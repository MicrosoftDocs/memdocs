---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 04/06/2020
ms.topic: conceptual
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

# In development for Microsoft Intune - April 2020

To help in your readiness and planning, this page lists Intune UI updates and features that are in development but not yet released. In addition to the information on this page: 

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in Office message center.
- When a feature enters production, whether it's a preview or generally available, the feature description will move from this page to [What's new](whats-new.md).
- This page and the [What's new](whats-new.md) page are updated periodically. Check back for additional updates.
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

> [!NOTE]
> This page reflects our current expectations about Intune capabilities in a future release. Dates and individual features might change. This page doesn't describe all features in development.

**RSS feed**: Find out when this page is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

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


<!-- ***********************************************-->
## Device configuration

### Wired network device configuration profiles for macOS devices<!-- 3508686  -->
A new macOS device configuration profile will be available that configures wired networks (**Device configuration** > **Profiles** > **Create profile** > **macOS** for platform > **Wired Network** for profile type). Use this feature to create 802.1x profiles to manage wired networks, and deploy these wired networks to your macOS devices.

Applies to:
- macOS

### Device configuration profile settings and values will be updated for Windows platforms<!-- 4091122 -->
When you create device configuration profiles for Windows platforms (**Devices** > **Configuration profiles** > **Create profile** > any **Windows** option for platform), some settings and their values are different from the CSP, and can be confusing. The setting names and their values will be updated to be clearer.

Applies to:

- Windows 10 and later device configuration profiles
- Windows Holographic for Business device configuration profiles
- Windows 8.1 device configuration profiles
- Windows Phone 8.1 device configuration profiles

### Configure the Microsoft Defender ATP app for macOS  <!-- 5520115  -->
You'll soon be able to configure the [settings](../protect/endpoint-protection-macos.md) for the Microsoft Defender ATP app for devices that run macOS as part of an Endpoint protection device configuration profile (**Devices** > **Configuration profiles** > **Create profile**, select **macOS** for the *Platform*, and then **Endpoint protection** for the *Profile type*). There will be eight settings for macOS device configuration. 

Defender ATP is supported on macOS 10.13 (High Sierra) and later, and the [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) app must be deployed to the device *after* these settings apply. The settings should be sent down to the device before the app is deployed. Beta versions of macOS won't be supported.

### New FileVault setting for macOS Endpoint Protection device configuration policy<!-- 5459801   -->
We're adding a new setting to the FileVault category within the [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) template: Hide recovery key. (**Devices** > **Configuration profiles** > **Create profile**, select **macOS** for the *Platform* and then **Endpoint protection** for the *Profile type*). This setting hides the personal key from the end user during FileVault 2 encryption. A device user can view their personal recovery key at any time from the iOS company portal app or from the company portal website for the encrypted macOS device. To view the personal recovery key they can go to device details, and click on *get recovery key*.

This setting won't be available in previously created policy. You'll need to re-create FileVault policies to configure this setting to make use of it. 

### Additional options in SSO and SSO app extension profiles on iOS/iPadOS devices<!-- 6504155  -->
On iOS/iPadOS devices, you can:

- In SSO profiles (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **Single sign-on**), set the Kerberos principal name to be the Security Account Manager (SAM) account name in SSO profiles. 
- In SSO app extension profiles (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **Single sign-on app extension**), configure the iOS/iPadOS Microsoft Azure AD extension with fewer clicks by using a new SSO app extension type. You can enable the Azure AD extension for shared devices and send extension-specific data to the extension.

Applies to:
- iOS/iPadOS 13.0+

For more information on using single sign-on on iOS/iPadOS devices, see [Single sign-on app extension overview](../configuration/device-features-configure.md#single-sign-on-app-extension) and [Single sign-on settings list](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- ***********************************************-->
## Device enrollment

### Bring-your-own-devices can use VPN to deploy<!--5015344 -->
The new  Autopilot profile **Skip Domain Connectivity Check** toggle lets you deploy Hybrid Azure AD Join devices without access to your corporate network using your own third party Win32 VPN client. To see the new toggle, go to [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices**  > **Windows** > **Windows enrollment** > **Deployment profiles** > **Create profile** > **Out-of-box experience (OOBE)**.

<!-- ***********************************************-->
## Device management

### PowerShell scripts support for BYOD devices<!-- 1862833  -->
PowerShell scripts will support Azure AD registered devices in Intune. For more information about PowerShell, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md). This functionality does not support devices running Windows 10 Home edition.

### Script support for macOS devices<!-- 4280361  -->
You'll be able to add and deploy scripts to macOS devices. This support extends your ability to configure macOS devices beyond what is possible using native MDM capabilities on macOS devices.

### Log Analytics will include device details log<!--6014987  -->
Intune device detail logs will be available in **Reports** > **Log analytics**. You can correlate device details to build custom queries and Azure workbooks.


<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--
## Monitor and troubleshoot
-->

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## Security

### Derived credentials support for DISA Purebred on Android devices<!--4839592 -->
You'll be able to use *DISA Purebred* as a [derived credentials](../protect/derived-credentials.md) provider on Android Enterprise fully managed devices (**Tenant administration** > **Connectors and tokens** > **Derived Credentials**). Support will be included retrieving a derived credential for DISA Purebred. You'll be able to use a derived credential for app authentication, Wi-Fi, VPN, or S/MIME signing and/or encryption with apps that support it. 

In April, Intune added support for *Entrust Datacard* and *Intercede* as providers for derived credential. 

### Privacy preferences settings for macOS devices<!-- 2934232 --> 
With the release of macOS Catalina 10.15, Apple added new security and privacy enhancements. By default, applications and processes are unable to access specific data without user consent. If users do not provide consent, the applications and processes may fail to function. Intune is adding support for settings that enable IT administrators to allow or disallow data access consent on behalf of end-users on devices running macOS 10.14 and later. These settings will ensure that applications and processes continue to function properly and reduce the number of prompts that end-users experience.

### Updated UI text and labels for Windows 10 Endpoint protection profile settings<!-- 5983747 -->
We're updating the text for various settings that you configure as Windows 10 device configuration profiles to make it easier to understand the settings intended use and results.

The settings we're updating include Windows 10 device configuration profiles for:

- [Device restrictions](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) > Microsoft Defender Antivirus  
- [Endpoint Protection](../protect/endpoint-protection-windows-10.md) > Microsoft Defender Antivirus

The settings that are supported with Intune aren't changing. This is only an update to the UI text in the Microsoft Endpoint Management Admin Center.

<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).



