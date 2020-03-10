---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 03/03/2020
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

### Retarget web clips to Microsoft Edge on iOS/iPadOS devices<!-- 5455276 -->
Web clips, which act as pinned web apps on iOS/iPadOS devices, will need to be updated. Newly deployed web clips will open in Microsoft Edge instead of the Intune Managed Browser if required to open in a protected browser. You must retarget pre-existing web clips to ensure they open in Microsoft Edge instead of the Managed Browser.

### macOS and iOS Company Portal updates<!-- 5779439, 5780234  -->
The Profile pane of the macOS and iOS Company Portal will be updated to include the sign out button. Additionally, this update will include UI improvements to the Profile pane in the macOS Company Portal. For more information about the Company Portal, see [How to configure the Microsoft Intune Company Portal app](../apps/company-portal-app.md).

### Updates to Branding and customization pane<!-- 5236032 -->
We are updating the Intune pane that is currently named "Branding and customization" with improvements, including:

- Renaming the pane to **Customization**.
- Improving the organization and design of the settings.
- Improving the settings text and tooltips.

To find these setting in Intune, navigate to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and, select **Tenant administration** > **Customization**. For information about existing customization, see [How to configure the Microsoft Intune Company Portal app](../apps/company-portal-app.md).

### Configure the iOS Microsoft Azure AD SSO app extension<!-- 567534  -->
The Microsoft Azure AD team is developing a redirect single sign-on (SSO) app extension to allow iOS and iPadOS 13.0+ users to seamlessly gain access to Microsoft apps and websites with one sign-on. When the AAD SSO app extension releases, you will be able to configure the SSO extension with the **Device features** > **Single sign-on app extension** profile in the admin console with minimal clicks.

For more information about iOS SSO app extensions or how to configure device features, see [Single sign-on app extension](../configuration/device-features-configure.md#single-sign-on-app-extension).

### Company Portal for iOS to support landscape mode<!--6048329  -->
Users will be able to enroll their devices, find apps, and get IT support using the screen orientation of their choice. The app will automatically detect and adjust screens to fit portrait or landscape mode, unless users lock the screen in portrait mode.

### Configure if enrollment is available in Company Portal for Android and iOS<!-- 4260128 idready idstaged -->
A new setting will be available that allows you to configure whether device enrollment in the Company Portal on Android and iOS devices is available with prompts, available without prompts, or unavailable to users. To find these setting in Intune, navigate to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and, select **Tenant administration** > **Customization** > **Edit** > **Device enrollment**. For more information about existing Company Portal customization, see [How to configure the Microsoft Intune Company Portal app](../apps/company-portal-app.md).

### Improved sign-in experience in Company Portal for Android<!-- 6103997  -->
We're updating the layout of several sign-in screens in the Company Portal app for Android to make the experience more modern, simple, and clean for users.

<!-- ***********************************************-->
## Device configuration

### Wired network device configuration profiles for macOS devices<!-- 3508686  -->
A new macOS device configuration profile will be available that configures wired networks (**Device configuration** > **Profiles** > **Create profile** > **macOS** for platform > **Wired Network** for profile type). Use this feature to create 802.1x profiles to manage wired networks, and deploy these wired networks to your macOS devices.

Applies to:
- macOS

### VPN profiles with IKEv2 VPN connections can use always on with iOS/iPadOS devices <!-- 1947932  -->
On iOS/iPadOS devices, you can create a VPN profile that uses an IKEv2 connection (**Device configuration** > **Profiles** > **Create profile** > **iOS/iPadOS** for platform > **VPN** for profile type). In a future update, you can configure always-on with IKEv2. When configured, IKEv2 VPN profiles connect automatically, and stay connected (or quickly reconnect) to the VPN. It stays connected even when moving between networks or restarting devices.

On iOS/iPadOS, always-on VPN is limited to IKEv2 profiles.

To see the current IKEv2 settings you can configure, go to [Add VPN settings on iOS/iPadOS devices in Microsoft Intune](../configuration/vpn-settings-ios.md#ikev2-settings).

Applies to:
- iOS

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

### Enterprise app trust settings modification setting will be removed from iOS/iPadOS device restriction profiles<!-- 6225131  -->
On iOS/iPadOS devices, you create a device restrictions profile (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile type). The **Enterprise app trust settings modification** setting will be removed by Apple, and will be removed from Intune. If you currently use this setting in a profile, it has no impact, and will stay in your profile until you create a new profile. This setting will also removed from any reporting in Intune.

Applies to:
- iOS/iPadOS

To see the settings you can restrict, go to [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md).

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

### Delete bundles and bundle arrays in OEMConfig device configuration profiles on Android Enterprise devices<!-- 5550355  -->
On Android Enterprise devices, you create and update OEMConfig profiles. Users will be able to delete bundles and bundle arrays using the **Configuration designer** in Intune.

For more information on OEMConfig profiles, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

This feature applies to:
- Android Enterprise

### Support for WPA and WPA2 in iOS Enterprise Wi-Fi profiles<!--6215273   -->
We're adding the *Security type* field to the [Enterprise Wi-Fi profile for iOS](../configuration/wi-fi-settings-ios.md) (**Devices** > **Configuration profiles** > **Create profile** and select **iOS/iPadOS** for *Platform* and then **Wi-Fi** for *Profile* ). This is similar to the options available for a Basic Wi-Fi profile for iOS. With this change you'll be able to create new profiles that specify a security type of **WPA-Enterprise** or **WPA/WPA2-Enterprise**, and then specify a selection for the *EAP type*.

### New user experience for certificate, email, VPN, and Wi-Fi profiles<!-- 5615208   -->
Were updating the [user experience](../configuration/device-profile-create.md) in the Endpoint Management Admin Center (**Devices** > **Configuration profiles** > **Create profile**) for creating and modifying the following profile types. The new experience will present the same settings as before, but uses a wizard-like experience that doesn't require as much horizontal scrolling. You won't need to modify existing configurations with the new experience.
- Derived credential
- Email
- PKCS certificate
- PKCS imported certificate
- SCEP certificate
- Trusted certificate
- VPN
- Wi-Fi

(**Devices** > **Configuration profiles** > **Create profile**, and then for *Profile type* select any of the preceding profiles.)

### Configure the Microsoft Defender ATP app for macOS  <!-- 5520115  -->
You'll soon be able to configure the [settings](../protect/endpoint-protection-macos.md) for the Microsoft Defender ATP app for devices that run macOS as part of an Endpoint protection device configuration profile (**Devices** > **Configuration profiles** > **Create profile**, select **macOS** for the *Platform*, and then **Endpoint protection** for the *Profile type*). There will be eight settings for macOS device configuration. 

Defender ATP is supported on macOS 10.13 (High Sierra) and later, and the [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md) app must be deployed to the device *after* these setting apply. The settings should be sent down to the device before the app is deployed. Beta versions of macOS won't be supported.

### New FileVault setting for macOS Endpoint Protection device configuration policy<!-- 5459801   -->
We're adding a new setting to the FileVault category within the [macOS Endpoint Protection](../protect/endpoint-protection-macos.md) template: Hide recovery key. (**Devices** > **Configuration profiles** > **Create profile**, select **macOS** for the *Platform* and then **Endpoint protection** for the *Profile type*). This setting hides the personal key from the end user during FileVault 2 encryption. A device user can view their personal recovery key at any time from the iOS company portal app or from the company portal website for the encrypted macOS device. To view the personal recovery key they can go to device details, and click on *get recovery key*.

This setting won't be available in previously created policy. You'll need to re-create FileVault policies to configure this setting to make use of it. 

###  UI update when configuring compliance policy <!-- 3961639  -->
We're updating the UI for configuring compliance policies in Microsoft Endpoint manager (**Devices** > **Compliance policies** > **Policies** > **Create Policy**). You will see a new user experience that provides the same settings and details that you have used previously. The new experience will follow a wizard-like process to create a compliance policy and will include the page where you can add *Assignments* for the policy, and then a *Summary* page where you can review your configuration before creating the policy. 

### Configure Delivery Optimization agent when downloading Win32 app content<!-- 5410945  -->
You will be able to configure the Delivery Optimization agent to download Win32 app content either in background or foreground mode based on assignment. For existing Win32 apps, content will continue to download in background mode. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > *select the Win32 app* > **Properties**. Select **Edit** next to **Assignments**.  Edit the assignment by selecting **Include** under **Mode** in the **Required** section.  You will find the new setting in the **App settings** section when it becomes available. For more information about Delivery Optimization, see [Win32 app management - Delivery Optimization](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## Device management

### Change Primary User for Windows devices <!-- 3794742 -->
You'll be able to change the Primary User for Windows hybrid and Azure AD Joined devices. To do so, go to **Intune** > **Devices** > **All devices** > choose a device > **Properties** > **Primary User**.

### New Android report on Android Devices overview page<!-- 5435435 -->
We'll be adding a report to the Microsoft Endpoint Manager admin console in the Android Devices overview page that displays how many Android devices have been enrolled in each device management solution. This chart (like the same chart already in the Azure console) shows work profile, fully managed, dedicated, and device administrator enrolled device counts. To see the report, choose **Devices** > **Android** > **Overview**.

### PowerShell scripts support for BYOD devices<!-- 1862833  -->
PowerShell scripts will support Azure AD registered devices in Intune. For more information about PowerShell, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md). This functionality does not support devices running Windows 10 Home edition.

### Additional Data Warehouse device inventory properties<!-- 6125732  -->
Additional device inventory properties will be available using the Intune Data Warehouse. The following properties will be exposed via the [devices](../developer/intune-data-warehouse-collections.md#devices) collection:

- Storage capacity
- Memory capacity
- Office 365 version
- Device model

For more information about the Data Warehouse, see [Microsoft Intune Data Warehouse API](../developer/reports-nav-intune-data-warehouse.md).

### Guide users from Android device administrator management to work profile management<!--5857738-->
We're releasing a new compliance setting for the Android device administrator platform. This setting lets you make a device non-compliant if it's managed with device administrator.

On these non-compliant devices, on the **Update device settings** page users will see the **Move to new device management setup** message. If they tap the **Resolve** button they'll be guided through:

1. Unenrolling from device administrator management
2. Enrolling in work profile management
3. Resolving compliance issues

Google is decreasing device administrator support in new Android releases in an effort to move to modern, richer, and more secure device management with Android Enterprise.  Intune can only provide full support for device administrator-managed Android devices running Android 10 and later through Q2 CY2020. Device administrator-managed devices (except Samsung) that are running Android 10 or later after this time won't be able to be entirely managed. In particular, impacted devices won't receive new password requirements. For more information, see this [Notice](#decreasing-support-for-android-device-administrator).

### Retire noncompliant devices<!-- 1827291 -->
We're adding a new optional compliance action to retire a noncompliant device (**Devices** > **Compliance policies** > **Policies** > **Create policy** and then view available *Actions* on the *Actions for noncompliance* page).  Retiring a noncompliant device removes all company data from it, and also removes the device from being managed by Intune. This action runs when the configured value in days is reached. The minimum value is 30 days.  Explicit IT admin approval will be required to retire the devices by using  the *Retire Non-compliant devices* section, where admins can retire all eligible devices.

### New information in device details<!-- 5604099 -->
The following information will be on the **Overview** page for devices:

- Storage capacity (amount of physical storage on device)
- Memory capacity (amount of physical memory on device)

### Script support for macOS devices<!-- 4280361  -->
You'll be able to add and deploy scripts to macOS devices. This support extends your ability to configure macOS devices beyond what is possible using native MDM capabilities on macOS devices.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Help and support workflow update to support additional services<!-- 5654170 -->
We're updating the Help and support page in the Microsoft Endpoint Manager admin center so you'll be able to choose the management type you use, to better provide specific support (**Troubleshooting + support** >  **Help and support**). With this change you'll be able to select from the following management types:
- Configuration Manager (includes Desktop Analytics)
- Intune
- Co-management

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## Security

### Derived credentials support on Android COBO devices<!--4839592-->
You'll be able to use derived credentials on Android Enterprise fully managed devices. Support will be included for retrieving a derived credential for Entrust Datacard, Intercede, and DISA Purebred. You'll be able to use a derived credential for app authentication, Wi-Fi, VPN, or S/MIME signing and/or encryption with apps that support it.

### Use Antivirus policy to manage settings for Microsoft Defender Antivirus and the Windows Security experience<!--6131401 -->
From the *Endpoint security* node, you'll be able to configure settings for **Antivirus**. When you configure policy for Antivirus, you'll define settings for your Windows 10 devices through two profile types:

- Microsoft Defender Antivirus: Manage settings for cloud protection, Antivirus exclusions, remediation, scan options, and more.
- Windows Security experience: Manage how users experience Windows Security settings on their devices. You'll be able configure what end users can view in the Microsoft Defender Security center and the notifications they receive.

### User's personal encrypted recovery key<!-- 6273943 -->
A new Intune feature will be available that enables users to retrieve their personal encrypted **FileVault** recovery key for Mac devices through the Android Company Portal application or through the Android Intune application. There will be a link in both the Company Portal application and Intune application that will open a Chrome browser to the Web Company Portal where the user can see the **FileVault** recovery key needed to access their Mac devices. For more information about encryption, see [Use device Encryption with Intune](../protect/encrypt-devices.md).

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
