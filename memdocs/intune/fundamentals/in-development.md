---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 02/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1

# optional metadata

#audience:
#ms.devlang:
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# In development for Microsoft Intune - February 2020

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

### Display notifications for the Company Portal app on Windows<!-- 1808082  -->
We'll update the Company Portal app on Windows devices to display toast notifications to users, even when the application is closed. The update will show notifications for available apps only when the installation status is completed or failed. The Company Portal app won't show notifications for required applications. 

### Display installation status messages for the Company Portal app<!-- 2514416  -->
The Company Portal app will show additional app installation status messages to end users. The following conditions will apply to new Win32 dependency features:
- App failed to install. Dependencies defined by the admin were not met.

### Retarget web clips to Microsoft Edge on iOS/iPadOS devices<!-- 5455276 -->
Web clips, which act as pinned web apps on iOS/iPadOS devices, will need to be updated. Newly deployed web clips will open in Microsoft Edge instead of the Intune Managed Browser if required to open in a protected browser. You must retarget pre-existing web clips to ensure they open in Microsoft Edge instead of the Managed Browser.

### macOS Company Portal user experience improvements<!-- 5568987 -->
We are making improvements to the macOS device enrollment experience and the Company Portal app for Mac. You can expect the following:
- A better Microsoft **AutoUpdate** experience during enrollment that will ensure your users have the latest version of the Company Portal.
- An enhanced compliance check step during enrollment.
- Support for copied Incident IDs, so your users can send errors from their devices to your company support team faster.

For more information about enrollment and the Company Portal app for Mac, see Enroll your macOS device using the Company Portal app (https://docs.microsoft.com/intune-user-help/enroll-your-device-in-intune-macos-cp). 


### Screen removed from Company Portal, Android work profile enrollment<!--6103987 -->
The **What's next?** screen will be removed from the Android work profile enrollment flow in Company Portal, to streamline the user experience. Go to [Enroll with Android work profile]( https://docs.microsoft.com/intune-user-help/enroll-device-android-work-profile) to see the current Android work profile enrollment flow.

<!-- ***********************************************-->
## Device configuration

### Wired network device configuration profiles for macOS devices<!-- 3508686  -->
A new macOS device configuration profile will be available that configures wired networks (**Device configuration** > **Profiles** > **Create profile** > **macOS** for platform > **Wired Network** for profile type). Use this feature to create 802.1x profiles to manage wired networks, and deploy these wired networks to your macOS devices.

Applies to:
- macOS

### VPN profiles with IKEv2 VPN connections can use always on with iOS/iPadOS devices <!-- 1947932 idready -->
On iOS/iPadOS devices, you can create a VPN profile that uses an IKEv2 connection (**Device configuration** > **Profiles** > **Create profile** > **iOS/iPadOS** for platform > **VPN** for profile type). In a future update, you can configure always-on with IKEv2. When configured, IKEv2 VPN profiles connect automatically, and stay connected (or quickly reconnect) to the VPN. It stays connected even when moving between networks or restarting devices.

On iOS/iPadOS, always-on VPN is limited to IKEv2 profiles.

To see the current IKEv2 settings you can configure, go to [Add VPN settings on iOS/iPadOS devices in Microsoft Intune](../configuration/vpn-settings-ios.md#ikev2-settings).

Applies to:
- iOS

### Improved user interface experience when creating configuration profiles on iOS/iPadOS and macOS devices<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984 idready -->
When you create a profile for iOS/iPadOS or macOS devices, the experience in the Endpoint Management Admin Center will be updated. This change impacts the following device configuration profiles (**Devices** > **Configuration Profiles** > **Create profile** > **iOS** or **macOS** for platform):

- Custom: iOS/iPadOS, macOS
- Device features: iOS/iPadOS, macOS
- Device restrictions: iOS/iPadOS, macOS
- Endpoint protection: macOS
- Extensions: macOS
- Preference file: macOS

### Improved user interface experience when creating OEMConfig configuration profiles on Android Enterprise devices<!-- 5568645 idready  -->
When you create or edit an OEMConfig profile for Android Enterprise devices, the experience in the Endpoint Management admin center is updated. The updated experience will provide a summary of settings you've configured at a glance. This change impacts the OEMConfig device configuration profile (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **OEMConfig** for profile type).

This feature applies to:
- Android Enterprise 


<!-- ***********************************************-->
<!--## Device enrollment-->


<!-- ***********************************************-->
## Device management

### Change Primary User for Windows devices <!-- 3794742 -->
You'll be able to change the Primary User for Windows hybrid and Azure AD Joined devices. To do so, go to **Intune** > **Devices** > **All devices** > choose a device > **Properties** > **Primary User**. 

### New update schedule options for pushing OS updates to enrolled iOS/iPadOS devices<!--5879689-->
You'll be able to from the following options when scheduling operating system updates for iOS/iPadOS devices. This applies to devices that that used the Apple Business Manager or Apple School Manager enrollment types.
- Update at next check-in
- Update during scheduled time
- Update outside of scheduled time

For the latter two options, you can create multiple time windows.

To see the new options, go to MEM > **Devices** > **iOS** > **Update policies for iOS/iPadOS** > **Create profile**.


<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- ***********************************************-->
<!--
## Monitoring and troubleshooting
-->

<!-- ***********************************************-->
<!--
## Role-based access control
-->


<!-- ***********************************************-->
## Security

### Derived credentials support on Android COBO devices<!--4839592-->
You'll be able to use derived credentials on Android Enterprise fully managed devices. Support will be included for retrieving a derived credential for Entrust Datacard, Intercede, and DISA Purebred. You'll be able to use a derived credential for app authentication, Wi-Fi, VPN, or S/MIME signing and/or encryption with apps that support it.

### Use Antivirus policy to manage settings for Microsoft Defender Antivirus and the Windows Security experience<!--6131401 -->
From the *Endpoint security* node, you’ll be able to configure settings for **Antivirus**. When you configure policy for Antivirus, you’ll define settings for your Windows 10 devices through two profile types:

- Microsoft Defender Antivirus: Manage settings for cloud protection, Antivirus exclusions, remediation, scan options, and more.
- Windows Security experience: Manage how users experience Windows Security settings on their devices. You’ll be able configure what end users can view in the Microsoft Defender Security center and the notifications they receive. 

<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also
For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).


