---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 03/21/2020
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

# In development for Microsoft Intune - March 2020

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

### Company Portal for iOS to support landscape mode<!--6048329  -->
Users will be able to enroll their devices, find apps, and get IT support using the screen orientation of their choice. The app will automatically detect and adjust screens to fit portrait or landscape mode, unless users lock the screen in portrait mode.

### Improved sign-in experience in Company Portal for Android<!-- 6103997  -->
We're updating the layout of several sign-in screens in the Company Portal app for Android to make the experience more modern, simple, and clean for users.

<!-- ***********************************************-->
## Device configuration

### Wired network device configuration profiles for macOS devices<!-- 3508686  -->
A new macOS device configuration profile will be available that configures wired networks (**Device configuration** > **Profiles** > **Create profile** > **macOS** for platform > **Wired Network** for profile type). Use this feature to create 802.1x profiles to manage wired networks, and deploy these wired networks to your macOS devices.

Applies to:
- macOS

### Improved user interface experience when creating configuration profiles on iOS/iPadOS and macOS devices<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
When you create a profile for iOS/iPadOS or macOS devices, the experience in the Endpoint Management Admin Center will be updated. This change impacts the following device configuration profiles (**Devices** > **Configuration Profiles** > **Create profile** > **iOS** or **macOS** for platform):

- Custom: iOS/iPadOS, macOS
- Device features: iOS/iPadOS, macOS
- Device restrictions: iOS/iPadOS, macOS
- Endpoint protection: macOS
- Extensions: macOS
- Preference file: macOS

### Improved user interface experience when creating OEMConfig configuration profiles on Android Enterprise devices<!-- 5568645   -->
When you create or edit an OEMConfig profile for Android Enterprise devices, the experience in the Endpoint Management admin center is updated. The updated experience will provide a summary of settings you've configured at a glance. This change impacts the OEMConfig device configuration profile (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **OEMConfig** for profile type).

This feature applies to:
- Android Enterprise 

### Device configuration profile settings and values will be updated for Windows platforms<!-- 4091122 -->
When you create device configuration profiles for Windows platforms (**Devices** > **Configuration profiles** > **Create profile** > any **Windows** option for platform), some settings and their values are different from the CSP, and can be confusing. The setting names and their values will be updated to be more clear.

Applies to:

- Windows 10 and later device configuration profiles
- Windows Holographic for Business device configuration profiles
- Windows 8.1 device configuration profiles
- Windows Phone 8.1 device configuration profiles

### Improved user interface experience when creating device restrictions profiles on Android and Android Enterprise devices<!-- 5841361 -->
When you create a profile for Android or Android Enterprise devices, the experience in the Endpoint Management admin center will be updated. This change impacts the following device configuration profiles (**Devices** > **Configuration Profiles** > **Create profile** > **Android device administrator** or **Android Enterprise** for platform):

- Device restrictions: Android device administrator
- Device restrictions: Android Enterprise device owner
- Device restrictions: Android Enterprise work profile

For more information on the device restrictions you can configure, see [Android device administrator](../configuration/device-restrictions-android.md) and [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### Configure the Microsoft Defender ATP app for macOS  <!-- 5520115  -->
You'll soon be able to configure the [settings](../protect/endpoint-protection-macos.md) for the Microsoft Defender ATP app for devices that run macOS as part of an Endpoint protection device configuration profile (**Devices** > **Configuration profiles** > **Create profile**, select **macOS** for the *Platform*, and then **Endpoint protection** for the *Profile type*). There will be eight settings for macOS device configuration. 

Defender ATP is supported on macOS 10.13 (High Sierra) and later, and the [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) app must be deployed to the device *after* these settings apply. The settings should be sent down to the device before the app is deployed. Beta versions of macOS won't be supported.

### New FileVault setting for macOS Endpoint Protection device configuration policy<!-- 5459801   -->
We're adding a new setting to the FileVault category within the [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) template: Hide recovery key. (**Devices** > **Configuration profiles** > **Create profile**, select **macOS** for the *Platform* and then **Endpoint protection** for the *Profile type*). This setting hides the personal key from the end user during FileVault 2 encryption. A device user can view their personal recovery key at any time from the iOS company portal app or from the company portal website for the encrypted macOS device. To view the personal recovery key they can go to device details, and click on *get recovery key*.

This setting won't be available in previously created policy. You'll need to re-create FileVault policies to configure this setting to make use of it. 

### Configure Delivery Optimization agent when downloading Win32 app content<!-- 5410945  -->
You will be able to configure the Delivery Optimization agent to download Win32 app content either in background or foreground mode based on assignment. For existing Win32 apps, content will continue to download in background mode. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > *select the Win32 app* > **Properties**. Select **Edit** next to **Assignments**.  Edit the assignment by selecting **Include** under **Mode** in the **Required** section.  You will find the new setting in the **App settings** section when it becomes available. For more information about Delivery Optimization, see [Win32 app management - Delivery Optimization](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## Device management

### Change Primary User for Windows devices <!-- 3794742 -->
You'll be able to change the Primary User for Windows hybrid and Azure AD Joined devices. To do so, go to **Intune** > **Devices** > **All devices** > choose a device > **Properties** > **Primary User**.

### PowerShell scripts support for BYOD devices<!-- 1862833  -->
PowerShell scripts will support Azure AD registered devices in Intune. For more information about PowerShell, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md). This functionality does not support devices running Windows 10 Home edition.

### New information in device details<!-- 5604099 -->
The following information will be on the **Overview** page for devices:

- Storage capacity (amount of physical storage on device)
- Memory capacity (amount of physical memory on device)

### Script support for macOS devices<!-- 4280361  -->
You'll be able to add and deploy scripts to macOS devices. This support extends your ability to configure macOS devices beyond what is possible using native MDM capabilities on macOS devices.

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

### Derived credentials support on Android COBO devices<!--4839592-->
You'll be able to use derived credentials on Android Enterprise fully managed devices. Support will be included for retrieving a derived credential for Entrust Datacard, Intercede, and DISA Purebred. You'll be able to use a derived credential for app authentication, Wi-Fi, VPN, or S/MIME signing and/or encryption with apps that support it.

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
