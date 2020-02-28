---
# required metadata
title: What's new in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Find out what's new in the Intune Azure portal
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# What's new in Microsoft Intune

Learn what’s new each week in Microsoft Intune. You can also find [important notices](#notices), [past releases](whats-new-archive.md), and information about [how Intune service updates are released](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728). 

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
> Check the [In development page](in-development.md) for a list of upcoming features in a release.

**RSS feed**: Get notified when this page is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
-->  


<!-- ########################## -->
## Week of February 17, 2020 (2002 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Microsoft Defender Advanced Threat Protection (ATP) app for macOS<!-- 5424618 -->
Intune provides an easy way to deploy the Microsoft Defender Advanced Threat Protection (ATP) app for macOS to managed Mac devices. For more information, see [Add Microsoft Defender ATP to macOS devices using Microsoft Intune](~/intune/apps/apps-advanced-threat-protection-macos.md) and [Microsoft Defender Advanced Threat Protection for Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).  


#### Microsoft's new Office app<!-- 5859926 -->
Microsoft's new Office app is now generally available for download and use. The Office app is a consolidated experience where your users can work across Word, Excel, and PowerPoint within a single app. You can target the app with an app protection policy to ensure the data being accessed is protected.

For more information, see [How to enable Intune app protection policies with the Office mobile preview app](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Enable network access control (NAC) with Cisco AnyConnect VPN on iOS devices<!-- 4860111  -->
On iOS devices, you can create a VPN profile, and use different connection types, including Cisco AnyConnect (**Device configuration** > **Profiles** > **Create profile** > **iOS** for platform > **VPN** for profile type > **Cisco AnyConnect** for connection type). 

You can enable network access control (NAC) with Cisco AnyConnect. To use this feature:

1. At [Cisco Identity Services Engine Administrator Guide](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html), use the steps in **Configuring Microsoft Intune as an MDM Server** to configure the Cisco Identity Services Engine (ISE) in Azure.
2. In the Intune device configuration profile, select the **Enable Network Access Control (NAC)** setting.

To see all the available VPN settings, go to [Configure VPN settings on iOS devices](../intune/configuration/vpn-settings-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Serial number on the Apple MDM Push certificate page<!--5947765  -->
The Apple MDM Push certificate page now shows the serial number. The serial number is needed to regain access to the Apple MDM Push certificate if access to the Apple ID that created the certificate is lost. To see the serial number, go to **Devices** > **iOS** > **iOS enrollment** > **Apple MDM Push certificate**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### New update schedule options for pushing OS updates to enrolled iOS/iPadOS devices<!--5879689  -->
You can choose from the following options when scheduling operating system updates for iOS/iPadOS devices. This applies to devices that that used the Apple Business Manager or Apple School Manager enrollment types.
- Update at next check-in
- Update during scheduled time
- Update outside of scheduled time

For the latter two options, you can create multiple time windows.

To see the new options, go to MEM > **Devices** > **iOS** > **Update policies for iOS/iPadOS** > **Create profile**.

#### Choose which iOS/iPadOS updates to push to enrolled devices<!--5879689  -->
You can choose a specific iOS/iPadOS update (except for the most recent update) to push to devices that have enrolled by using either Apple Business Manager or Apple School Manager. Such devices must have a device configuration policy set to delay software update visibility for some number of days. To see this feature, go to MEM > **Devices** > **iOS** > **Update policies for iOS/iPadOS** > **Create profile**.

### All devices list improved search, sort, and filter<!--6179023-->
The All devices list has been improved for better performance, searching, sorting, and filtering.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Improved Intune reporting experience<!-- 3791418   -->
Intune now provides an improved reporting experience, including new report types, better report organization, more focused views, improved report functionality, as well as more consistent and timely data. The reporting experience will move from public preview to GA (general availability). Additionally, the GA release will provide localization support, bug fixes, design improvements, and aggregate device compliance data on tiles in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). 

New report types focus on the following:
- **Operational** - Provides fresh records with a negative health focus. 
- **Organizational** - Provides an broader summary of the overall state.
- **Historical** - Provides patterns and trends over a period of time.
- **Specialist** - Allows you to use raw data to create your own custom reports.

The first set of new reports focuses on device compliance. For more information, see [Blog - Microsoft Intune reporting framework](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) and [Intune reports](~/intune/fundamentals/reports.md).

#### Consolidated the location of security baselines in the UI<!-- 6177074   -->
We've consolidated the paths to find [security baselines](../intune/protect/security-baselines.md) in the Microsoft Endpoint Manager admin center by removing *Security baselines* from several UI locations. To find Security baselines, you now use the following path:  **Endpoint security** > **Security baselines**.

#### Expanded support for imported PKCS certificates<!-- 6044197 WNReady -->
We’ve expanded support for using [imported PKCS certificates](../intune/protect/certificates-imported-pfx-configure.md#supported-platforms) to support *Android Enterprise fully managed devices*. Generally, importing PFX certificates is used for S/MIME encryption scenarios, where a user's encryption certificates are required on all of their devices so that email decryption can occur.

The following platforms support import of PFX certificates:
- Android - Device Administrator
- Android Enterprise - Fully Managed
- Android Enterprise - Work profile
- iOS
- Mac
- Windows 10

#### View the endpoint security configuration for devices<!-- 6206460  -->
We've updated the name of the option in the Microsoft Endpoint Manager admin center, for viewing [endpoint security configurations that apply to a specific device](../intune/protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device). This option is renamed to **Endpoint security configuration** because it shows applicable security baselines and additional policies created outside of security baselines. Previously, this option was named *Security baselines*. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Intune Roles user interface changes coming<!--5801612   -->
The user interface for [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Roles** has been improved to a more user-friendly and intuitive design. This experience provides the same settings and details that you use now, however the new experience employs a wizard-like process.

<!-- ########################## -->
## Week of February 17, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Microsoft's new Office app<!-- 5859926 -->
Microsoft's new Office app is now generally available for download and use. The Office app is a consolidated experience where your users can work across Word, Excel, and PowerPoint within a single app. You can target the app with an app protection policy to ensure the data being accessed is protected.

For more information, see [How to enable Intune app protection policies with the Office mobile preview app](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493).

<!-- ########################## -->
## Week of February 10, 2020

### Windows 7 ends extended support <!--3042987-->
Windows 7 reached end of extended support on January 14, 2020. Intune deprecated support for devices running Windows 7 at the same time. Technical assistance and automatic updates that help protect your PC are no longer available. You should upgrade to Windows 10. For more information, see the [Plan for Change blog post](https://aka.ms/Windows7_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Microsoft Edge version 77 and later on Windows 10 devices<!-- 5843584 -->
Intune now supports uninstalling Microsoft Edge version 77 and later on Windows 10 devices. For more information, see [Add Microsoft Edge for Windows 10 to Microsoft Intune](~/intune/apps/apps-windows-edge.md).

#### Screen removed from Company Portal, Android work profile enrollment<!--6103987 -->
The **What's next?** screen has been removed from the Android work profile enrollment flow in Company Portal to streamline the user experience. Go to [Enroll with Android work profile](/intune-user-help/enroll-device-android-work-profile) to see the updated Android work profile enrollment flow.  

#### Company Portal app improved performance<!-- 6178652 -->
The Company Portal app has been updated to support improved performance for devices that use ARM64 processors, such as the Surface Pro X. Previously, the Company Portal operated in an emulated ARM32 mode. Now, in version 10.4.7080.0 and above, the Company Portal app is natively compiled for ARM64. For more information about the Company Portal app, see [How to configure the Microsoft Intune Company Portal app](~/intune/apps/company-portal-app.md).

<!-- ########################## -->
## Week of January 27, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Intune support for additional Microsoft Edge version 77 deployment channel for macOS<!-- 5983950  -->
Microsoft Intune now support the additional **Stable** deployment channel for the Microsoft Edge app for macOS. The **Stable** channel is the recommended channel for deploying Microsoft Edge broadly in Enterprise environments. It updates every six weeks, each release incorporating improvements from the **Beta** channel. In addition to the **Stable** and **Beta** channels, Intune supports a **Dev** channel. The public preview offers stable and dev channels for Microsoft Edge version 77 and later for macOS. Automatic updates of the browser is On by default. For more information, see [Add Microsoft Edge for macOS devices using Microsoft Intune](~/intune/apps/apps-edge-macos.md).

#### Retirement of Intune Managed Browser<!--5728447 -->
The Intune Managed Browser will be retired. Use Microsoft Edge for your protected Intune browser experience. For more information, see the entry '[Take Action: Use Microsoft Edge for your Protected Intune Browser Experience](~/intune/fundamentals/whats-new.md#take-action-use-microsoft-edge-for-your-protected-intune-browser-experience)' in the [Notices](~/intune/fundamentals/whats-new.md#notices) section below.

<!-- ########################## -->
## Week of January 20, 2020 (2001 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### User experience change when adding apps to Intune<!-- 4705829   -->
You'll see a new user experience when adding apps to via Intune. This experience provides the same settings and details that you have used previously, however the new experience follows a wizard-like process before adding an app to Intune. This new experience also provides a review page before adding the app. From the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > **Add**. For more information, see [Add apps to Microsoft Intune](~/intune/apps/apps-add.md).

#### Require Win32 apps to restart <!-- 5622282   -->
You can require that a Win32 app must restart after a successful install. Also, you can choose the amount of time (the grace period) before the restart must occur.

#### User experience change when configuring apps in Intune<!-- 4207990   -->
You'll see a new user experience when creating app configuration policies in Intune. This experience provides the same settings and details that you have used previously, however the new experience follows a wizard-like process before adding a policy to Intune. From the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App configuration policies** > **Add**. For more information, see [App configuration policies for Microsoft Intune](~/intune/apps/app-configuration-policies-overview.md). 

#### Intune support for additional Microsoft Edge for Windows 10 deployment channel<!-- 5861774 -->
Microsoft Intune now support the additional **Stable** deployment channel for the Microsoft Edge (version 77 and later) for Windows 10 app. The **Stable** channel is the recommended channel for deploying Microsoft Edge for Windows 10 broadly in Enterprise environments. This channel updates every six weeks, each release incorporating improvements from the **Beta** channel. In addition to the **Stable** and **Beta** channels, Intune supports a **Dev** channel. For more information, see [Microsoft Edge for Windows 10 - Configure app settings](~/intune/apps/apps-windows-edge.md#configure-app-settings).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Improved user interface experience when configuring Exchange ActiveSync on-premises connector UI<!-- 5695492   -->
We've updated the experience for [configuring the Exchange ActiveSync on-premises connector](../intune/protect/exchange-connector-install.md). The updated experience uses a single pane to configure, edit, and summarize the details of your on-premises connectors. 

#### Add automatic proxy settings to Wi-Fi profiles for Android Enterprise work profiles<!-- 4490822   -->
On Android Enterprise Work Profile devices, you can create Wi-Fi profiles. When you choose the Wi-Fi Enterprise type, you can also enter the Extensible Authentication Protocol (EAP) type used on your Wi-Fi network.

Now when you choose the Enterprise type, you can also enter automatic proxy settings, including a proxy server URL, such as `proxy.contoso.com`.

To see the current Wi-Fi settings you can configure, go to [Add Wi-Fi settings for devices running Android Enterprise and Android kiosk in Microsoft Intune](../intune/configuration/wi-fi-settings-android-enterprise.md).

Applies to:
- Android Enterprise work profile

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Block Android enrollments by device manufacturer<!--5197392  -->
You can block devices from enrolling based on the manufacturer of the device. This applies to Android device administrator and Android Enterprise work profile devices. To see enrollment restrictions, go to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Enrollment restrictions**.

#### Improvements to the iOS/iPadOS Create enrollment type profile UI<!-- 6055005 -->
For iOS/iPadOS User Enrollment, the **Create enrollment type profile** **Settings** page has been streamlined to improve the **Enrollment type** choice process while keeping the same functionality. To see the new UI, go to [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **iOS** > **iOS enrollment** > **Enrollment types** > **Create profile** > **Settings** page. For more information, see [Create a User Enrollment profile in Intune](../intune/enrollment/ios-user-enrollment.md#create-a-user-enrollment-profile-in-intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### New information in device details<!-- 4471759 5604099  -->
The following information is now on the **Overview** page for devices:
- Memory Capacity (amount of physical memory on the device)
- Storage Capacity (amount of physical storage on the device) 
- CPU architecture

#### iOS Bypass Activation Lock remote action renamed to Disable Activation Lock <!--5904591  -->
The remote action **Bypass Activation Lock** has been renamed to **Disable Activation Lock**. For more information, see [Disable iOS Activation Lock with Intune](../intune/remote-actions/device-activation-lock-bypass.md).

#### Windows 10 feature update deployment support for Autopilot devices<!-- 5948137   -->
Intune now supports targeting Autopilot registered devices using [Windows 10 feature update deployments](../intune/protect/windows-update-for-business-configure.md#windows-10-feature-updates).

Windows 10 feature update policies cannot be applied during the Autopilot out of box experience (OOBE) and will only apply at the first Windows Update scan after a device has finished provisioning (which is typically a day).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Windows Autopilot deployment reports (preview) <!-- 3856172   -->
A new report details each device deployed through Windows Autopilot. For more information, see [Autopilot deployment report](../intune/enrollment/enrollment-autopilot.md#autopilot-deployments-report).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### New Intune built-in role Endpoint security manager<!--4253397   -->
A new Intune built-in role is available: the Endpoint security manager. This new role gives admins full access to the Endpoint Manager node in Intune and ready-only access to other areas. The role is an expansion of the “Security Administrator” role from Azure AD. If you currently just have Global Admins as roles, then there’s no changes needed. If you use roles, and you’d like the granularity that the Endpoint Security Manager provides, then assign that role when it is available. For more information about built-in roles, see [Role-based access control](role-based-access-control.md).

<!-- ########################## -->
## Week of January 6, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### S/MIME support for Microsoft Outlook for iOS<!-- 2669398 -->
Intune supports delivering S/MIME signing and encryption certificates that can be used with Outlook for iOS on iOS devices. For more information, see [Sensitivity labeling and protection in Outlook for iOS and Android](https://aka.ms/omsmime).

#### Cache Win32 app content using Microsoft Connected Cache server<!-- 6030314 -->
You can install a Microsoft Connected Cache server on your Configuration Manager distribution points to cache Intune Win32 app content. For more information, see [Microsoft Connected Cache in Configuration Manager - Support for Intune Win32 apps](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Windows 10 administrative templates (ADMX) profiles now support scope tags <!--5137390 -->
You can now assign scope tags to administrative template profiles (ADMX). To do so, go to **Intune** > **Devices** > **Configuration profiles** > choose an administrative templates profile in the list > **Properties** > **Scope tags**. For more information about scope tags, see [Assign scope tags to other objects](../intune/fundamentals/scope-tags.md#assign-scope-tags-to-other-objects).

<!-- ########################## -->
## Week of December 30, 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Retrieve personal recovery key from MEM encrypted macOS devices<!-- 4851745 -->
End users can retrieve their personal recovery key (FileVault key) using the iOS Company Portal app. The device that has the personal recovery key must be enrolled with Intune and encrypted with FileVault through Intune. Using the iOS Company Portal app, an end user can retrieve their personal recovery key on their encrypted macOS device by clicking **Get recovery key**. You can also retrieve the recovery key from Intune by selecting **Devices** > *the encrypted and enrolled macOS device* > **Get recovery key**. For more information about FileVault, see [FileVault encryption for macOS](~/intune/protect/encrypt-devices.md#filevault-encryption-for-macos).

#### iOS and iPadOS user-licensed VPP apps<!-- 5619268 -->
For user enrolled iOS and iPadOS devices, end users will no longer be presented with newly created device-licensed VPP applications deployed as available. However, end users will continue to see all user-licensed VPP apps within the Company Portal. For more information about VPP apps, see [How to manage iOS and macOS apps purchased through Apple Volume Purchase Program with Microsoft Intune](~/intune/apps/vpp-apps-ios.md).

<!-- ########################## -->
## Week of December 23, 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Notice - Windows 10 1703 (RS2) will be moving out of support <!-- 5026679 -->
Starting October 9, 2018, Windows 10 1703 (RS2) moved out of Microsoft platform support for Home, Pro, and Pro for Workstations editions. For Windows 10 Enterprise and Education editions, Windows 10 1703 (RS2) moved out of platform support on October 8, 2019. Starting December 26, 2019, we will be updating the minimum version of the Windows Company Portal application to Windows 10 1709 (RS3). Computers running versions prior to 1709 will no longer receive updated versions for the application from the Microsoft Store. We have previously communicated this change to customers who are managing older versions of Windows 10 via the message center. For more information, see [Windows lifecycle fact sheet](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

<!-- ########################## -->

## Week of December 16, 2019

### Device configuration

#### Updates to Administrative Templates for Windows 10 devices <!-- 5941568 -->

You can use ADMX templates in Microsoft Intune to control and manage settings for Microsoft Edge, Office, and Windows. Administrative Templates in Intune made the following policy setting updates:

- Added support for Microsoft Edge versions 78 and 79.
- Includes the November 11, 2019 ADMX files in [Administrative Template files (ADMX/ADML) and Office Customization Tool for Office 365 ProPlus, Office 2019, and Office 2016](https://www.microsoft.com/download/details.aspx?id=49030).

For more information on ADMX templates in Intune, see [Use Windows 10 templates to configure group policy settings in Microsoft Intune](../intune/configuration/administrative-templates-windows.md).

Applies to:

- Windows 10 and later

## Week of December 9, 2019 (1912 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Migrating to Microsoft Edge for managed browsing scenarios<!-- 5173762 -->
As we move closer to the retirement of the Intune Managed Browser, we made changes to app protection policies to simplify the steps needed to move your users over to Edge. We have updated the options for the app protection policy setting **Restrict web content transfer with other apps** to be one of the following:

- Any app
- Intune Managed Browser
- Microsoft Edge
- Unmanaged browser 

When you select **Microsoft Edge**, your end users will see conditional access messaging notifying them that Microsoft Edge is required for managed browsing scenarios. They will be prompted to download and sign-in to Microsoft Edge with their AAD accounts, if they have not already done so.  This will be the equivalent to having targeted your MAM-enabled apps with the app config setting `com.microsoft.intune.useEdge` set to **True**. Existing app protection policies that used the **Policy managed browsers** setting will now have **Intune Managed Browser** selected, and you will see no change in behavior. This means your users will see messaging to use Microsoft Edge if you've set the **useEdge** app configuration setting to **True**. We encourage all customers leveraging managed browsing scenarios to update their app protection policies with **Restrict web content transfer with other apps** to ensure users are seeing the proper guidance to transition to Microsoft Edge, no matter which app they are launching links from. 

#### Configure app notification content for organization accounts<!-- 2576686  -->
Intune app protection policies (APP) on Android and iOS devices allow you to control app notification content for Org accounts. You can select an option (Allow, Block org Data, or Blocked) to specify how notifications for org accounts are shown for the selected app.This feature requires support from applications and may not be available for all APP enabled applications. Outlook for iOS version 4.15.0 (or later) and Outlook for Android 4.83.0 (or later) will support this setting. The setting is available in the console, but the functionality will begin to take effect after December 16, 2019. For more about APP, see [What are app protection policies?](../intune/apps/app-protection-policy.md).

#### Microsoft app icons update<!--4677605  -->
The icons used for Microsoft apps in the app targeting pane for App protection policies and App configuration policies have been updated.

#### Require use of approved keyboards on Android<!--4761794  -->
As part of an app protection policy, you can specify the setting [**Approved keyboards**](../intune/apps/app-protection-policy-settings-android.md#data-protection) to manage which Android keyboards can be used with managed Android apps. When a user opens the managed app and doesn't already use an approved keyboard for that app, they are prompted to switch to one of the approved keyboards already installed on their device. If needed, they're presented with a link to download an approved keyboard from the Google Play Store, which they can install and set up. The user can only edit text fields in a managed app when their active keyboard isn't one of the approved keyboards.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Updated single sign-on experience for apps and websites on your iOS, iPadOS, and macOS devices<!-- 4999578  -->
Intune has added more single sign-on (SSO) settings for iOS, iPadOS, and macOS devices. You can now configure redirect SSO app extensions written by your organization or by your identity provider. Use these settings to configure a seamless single sign-on experience for apps and websites that use modern authentication methods, such as OAuth and SAML2. 

These new settings expand on the previous settings for SSO app extensions and Apple's built-in Kerberos extension (**Devices** > **Device configuration** > **Profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform type > **Device features** for profile type). 

To see the full range of SSO app extension settings you can configure, go to [SSO on iOS](../intune/configuration/ios-device-features-settings.md#single-sign-on-app-extension) and [SSO on macOS](../intune/configuration/macos-device-features-settings.md#single-sign-on-app-extension).

Applies to:

- iOS/iPadOS
- macOS

#### We have updated two device restriction settings for iOS and iPadOS devices to correct their behavior<!-- 5701352    -->
For iOS devices, you can create device restriction profiles that **Allow over-the-air PKI updates** and **Blocks USB Restricted mode** (**Devices** > **Device configuration** > **Profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile type). Prior to this release, the UI settings and descriptions for the following settings were incorrect, and they have now been corrected. Beginning with this release, the settings behavior is as follows:

**Block over-the-air PKI updates**: **Block** prevents your users from receiving software updates unless the device is connected to a computer. **Not configured** (default): allows a device to receive software updates without being connected to a computer.
- Previously, this setting let you configure it as: **Allow**, which let your users receive software updates without connecting their devices to a computer.
**Allow USB accessories while device is locked**: **Allow** lets USB accessories exchange data with a device that's been locked for over an hour. **Not configured** (default) doesn't update USB Restricted mode on the device, and USB accessories will be blocked from transferring data from the device if locked for over an hour.
- Previously, this setting let you configure it as: **Block** to disable USB Restricted mode on supervised devices.

For more information on the setting you can configure, see [iOS and iPadOS device settings to allow or restrict features using Intune](../intune/configuration/device-restrictions-ios.md).

This feature applies to:

- OS/iPadOS

#### Wired network device configuration profiles for macOS devices<!-- 3508686  -->
   > [!NOTE]
   > This feature has been delayed, but will be released soon.

#### Block users from configuring certificate credentials in the managed keystore on Android Enterprise device owner devices<!-- 3311998 -->
On Android Enterprise device owner devices, you can configure a new setting that blocks users from configuring their certificate credentials in the managed keystore (**Device configuration** > **Profiles** > **Create profile** > **Android Enterprise** for platform > **Device Owner Only > Device Restrictions** for profile type > **Users + Accounts**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Protected wipe action now available<!--51150000 -->
You now have the option to use the Wipe device action to perform a protected wipe of a device. Protected wipes are the same as standard wipes, except that they can't be circumvented by powering off the device. A protected wipe will keep trying to reset the device until successful. In some configurations this action may leave the device unable to reboot. For more information, see [Retire or wipe devices](../intune/remote-actions/devices-wipe.md).

#### Device Ethernet MAC address added to device's Overview page<!--5562275 -->
You can now see a device's Ethernet MAC address on the device details page (**Devices** > **All devices** > choose a device > **Overview**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Improved experience on a shared device when device based conditional access policies are enabled<!-- 1734096  -->
We improved the experience on a shared device with multiple users who are targeted with device based conditional access policy by checking the latest compliance evaluation for the user when enforcing policy. 
For more information, see  the following overview articles:
- [Azure overview for Conditional Access](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Intune device compliance overview](../intune/protect/device-compliance-get-started.md)

#### Use PKCS certificate profiles to provision devices with certificates<!-- 2317124, 2317130, 2317139, 2340517, 2340528, 2340529  -->
You can now use PKCS certificate profiles to issue certificates to *devices* that run Android for Work, iOS, and Windows, when associated with profiles like those for Wi-Fi and VPN. Previously those three platforms supported only user-based certificates, with device-based support being limited to macOS.

> [!NOTE]
> PKCS certificate profiles are not supported with Wi-Fi profiles. Instead, use SCEP certificate profiles when you use an [EAP type](../intune/configuration/wi-fi-settings-windows.md#enterprise-profile).

To use a device-based certificate, while [creating a PKCS certificate profile](../intune/protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile) for the supported platforms, select **Settings**. You’ll now see the setting for **Certificate type**, which supports the options for Device, or User.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Centralized audit logs<!--5603185, 5697164 -->
A new centralized audit log experience now collects audit logs for all categories into one page. You can filter the logs to get the data you're looking for. To see the audit logs, go to **Tenant administration** > **Audit logs**. 

#### Scope tag information included in audit log activity details<!--5763534 -->
Audit log activity details now include scope tag information (for Intune objects that support scope tags). For more information about audit logs, see [Use audit logs to track and monitor events](monitor-audit-logs.md).

<!-- ########################## -->
## Week of December 2, 2019

#### New Microsoft Endpoint Configuration Manager co-management licensing<!--5027281-->
Configuration Manager customers with Software Assurance can get Intune co-management for Windows 10 PCs without having to purchase an additional Intune license for co-management. Customers no longer need to assign individual Intune/EMS licenses to their end users for co-managing Windows 10.
- Devices managed by Configuration Manager and enrolled into co-management have almost the same rights as Intune Standalone MDM managed PCs. However, after resetting they can't be re-provisioned by using Autopilot.
- Windows 10 devices enrolled into Intune by using other means require full Intune licenses.
- Devices on other platforms still require full Intune licenses.

For more information, see [Licensing terms](https://www.microsoft.com/en-us/Licensing/product-licensing/products).

<!-- ########################## -->
## Week of November 18, 2019 (1911 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### UI update when selectively wiping app data<!-- 4102028 -->
The UI to selectively wipe app data in Intune has been updated. UI changes include:
- A simplified experience by using a wizard-style format condensed within one pane.
- An update to the create flow to include assignments.
- A summarized page of all things set when viewing properties, prior to creating a new policy or when editing a property. Also, when editing properties, the summary will only show a list of items from the category of properties being edited.

For more information, see [How to wipe only corporate data from Intune-managed apps](~/intune/apps/apps-selective-wipe.md).

#### iOS and iPadOS third party keyboard support<!-- 4922950 -->
In March  2019, we announced the removal of support for the iOS App protection policy setting "Third party keyboards". The feature is returning to Intune with both iOS and iPadOS support. To enable this setting, visit the **Data protection** tab of a new or existing iOS/iPadOS app protection policy and find the **Third party keyboards** setting under **Data Transfer**.

The behavior of this policy setting differs slightly from the previous implementation. In multi-identity apps using SDK version 12.0.16 and later, targeted by app protection policies with this setting configured to **Block**, end-users will be unable to opt for third party keyboards in both their organization and personal accounts. Apps using SDK versions 12.0.12 and earlier will continue to exhibit the behavior documented in our blog post title, [Known issue: Third party keyboards are not blocked in iOS for personal accounts](https://aka.ms/3rdparty_iOS_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Target macOS user groups to require Jamf management<!-- 4061739  --> 
You can target specific groups of users that will get their [macOS devices managed by Jamf](../intune/protect/conditional-access-integrate-jamf.md). This enables you apply the Jamf compliance integration to a subset of macOS devices while other devices are managed by Intune. If you are already using the Jamf integration, All Users will be targeted for the integration by default.

#### New Exchange ActiveSync settings when creating an Email device configuration profile on iOS devices<!-- 4892824   --> 
On iOS/iPadOS devices, you can configure email connectivity in a device configuration profile (**Device configuration** > **Profiles** > **Create profile** > **iOS/iPadOS** for platform > **Email** for profile type). 

There are new Exchange ActiveSync settings available, including:
- **Exchange data to sync**: Choose the Exchange services to sync (or block syncing) for Calendar, Contacts, Reminders, Notes, and Email.
- **Allow users to change sync settings**: Allow (or block) users to change the sync settings for these services on their devices.  

For more information on these setting, go to [Email profile settings for iOS devices in Intune](../intune/configuration/email-settings-ios.md). 

Applies to:

- iOS 13.0 and newer
- iPadOS 13.0 and newer

#### Prevent users from adding personal Google accounts to Android Enterprise fully managed and dedicated devices<!-- 5353228   -->
On Android Enterprise fully managed and dedicated devices, there's a new setting that prevent users from creating personal Google accounts (**Device configuration** > **Profiles** > **Create profile** > **Android Enterprise** for platform > **Device Owner Only > Device Restrictions** for profile type > **Users and Accounts settings** > **Personal Google Accounts**).

To see the settings you can configure, go to [Android Enterprise device settings to allow or restrict features using Intune](../intune/configuration/device-restrictions-android-for-work.md).

Applies to:

- Android Enterprise fully managed devices
- Android Enterprise dedicated devices

#### Server-side logging for Siri commands setting is removed in iOS/iPadOS device restrictions profile <!-- 5468501   -->
On iOS and iPadOS devices, the **Server-side logging for Siri commands** setting is removed from the Microsoft Endpoint Manager admin console (**Device configuration** > **Profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile type > **Built-in apps**). 

This setting has no effect on devices. To remove the setting from existing profiles, open the profile, make any change, and then save the profile. The profile is updated, and the setting is deleted from devices.

To see all the settings you can configure, see [iOS and iPadOS device settings to allow or restrict features using Intune](../intune/configuration/device-restrictions-ios.md).

Applies to:

- iOS/iPadOS

#### Windows 10 feature updates (public preview)<!-- 2384877 -->
You can now deploy [Windows 10 feature updates](../intune/protect/windows-update-for-business-configure.md#windows-10-feature-updates) to Windows 10 devices. Windows 10 feature updates are a new software update policy that sets the version of Windows 10 that you want devices to install and remain at. You can use this new policy type along with your existing Windows 10 update rings.

Devices that receive Windows 10 feature updates policy will install the specified version of Windows, and then remain at that version until the policy is edited or removed. Devices that run a later version of Windows remain at their current version. Devices that are held at a specific version of Windows can still install quality and security updates for that version from Windows 10 update rings.

This new type of policy begins rolling out to tenants this week. If this policy isn't available for your tenant yet, it will be soon.

#### Add and change key information in plist files for macOS applications<!-- 4736278 -->
On macOS devices, you can now create a device configuration profile that uploads a property list file (.plist) associated with an app or with the device (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Preference File** for profile type).

Only some apps support managed preferences, and these apps might not allow you to manage all settings. Be sure to upload a property list file that configures device channel settings, not user channel settings.

For more information on this feature, see [Add a property list file to macOS devices using Microsoft Intune](../intune/configuration/preference-file-settings-macos.md).

Applies to:

- macOS devices running 10.7 and newer

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Edit device name value for Autopilot devices<!-- 2640074 -->
You can edit the Device Name value for Azure AD Joined Autopilot devices.  For more information, see [Edit Autopilot device attributes](../intune/enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

#### Edit Group Tag value for Autopilot devices<!-- 4816775   -->
You can edit the Group Tag value for Autopilot devices. For more information, see [Edit Autopilot device attributes](../intune/enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Updated support experience<!-- 5012398 -->

Starting today, an updated and streamlined in-console experience for [getting help and support for Intune](get-support.md) is rolling out to tenants. If this new experience isn't available for you yet, it will be soon.

We've improved the in-console search and feedback for common issues, and the workflow you use to contact support. When opening a support issue, you'll see real-time estimates for when you can expect a callback or email reply, and Premier and Unified support customers can easily specify a severity for their issue, to help get support faster.

#### Improved Intune reporting experience (public preview) <!-- 3791418 -->
Intune now provides an improved reporting experience, including new report types, better report organization, more focused views, improved report functionality, as well as more consistent and timely data. New report types focus on the following:
- **Operational** - Provides fresh records with a negative health focus. 
- **Organizational** - Provides an broader summary of the overall state.
- **Historical** - Provides patterns and trends over a period of time.
- **Specialist** - Allows you to use raw data to create your own custom reports.

The first set of new reports focuses on device compliance. For more information, see [Blog - Microsoft Intune reporting framework](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) and [Intune reports](~/intune/fundamentals/reports.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Duplicate custom or built-in roles <!-- 1081938   -->
You can now copy built-in and custom roles. For more information, see [Copy a role](../intune/fundamentals/create-custom-role.md#copy-a-role).

#### New permissions for school administrator role <!-- 5621805  -->  
Two new permissions, **Assign profile** and **Sync device**, have been added to the school administrator role > **Permissions** > **Enrollment programs**. The sync profile permission lets group admins sync Windows Autopilot devices. The assign profile permission lets them delete user-initiated Apple enrollment profiles. It also gives them permission to manage Autopilot device assignments and Autopilot deployment profile assignments. For a list of all school administrator/group admin permissions, see [Assign group admins](https://docs.microsoft.com/intune-education/group-admin-delegate). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Security

#### BitLocker key rotation<!-- 2564951  -->
You can use an Intune device action to remotely [rotate BitLocker recovery keys](../intune/protect/encrypt-devices.md#rotate-bitlocker-recovery-keys)  for managed devices that run Windows version 1909 or later. To qualify to have recovery keys rotated, devices must be configured to support recovery key rotation.  

#### Updates to dedicated device enrollment to support SCEP device certificate deployment <!-- 5198878  -->
Intune now supports SCEP device certificate deployment to Android Enterprise dedicated devices for certificate-based access to Wi-Fi profiles. The Microsoft Intune app must be present on the device for deployment to work. As a result, we've updated the enrollment experience for Android Enterprise dedicated devices. New enrollments still start the same (with QR, NFC, Zero-touch, or device identifier) but now have a step that requires users to install the Intune app. Existing devices will start getting the app automatically installed on a rolling basis.

#### Intune audit logs for business-to-business collaboration<!--5670211 -->
Business-to-business (B2B) collaboration allows you to securely share you company's applications and services with guest users from any other organization, while maintaining control over your own corporate data. Intune now supports audit logs for B2B guest users. For example, when guest users make changes, Intune will be able to capture this data through audit logs. For more information, see [What is guest user access in Azure Active Directory B2B?](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b)

<!-- ########################## -->
## Week of November 11, 2019  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management  

#### Improved macOS enrollment experience in Company Portal <!-- 5074349  -->  
The Company Portal for macOS enrollment experience has a simpler enrollment process that aligns more closely with the Company Portal for iOS enrollment experience. Device users now see:  

* A sleeker user interface.  
* An improved enrollment checklist.  
* Clearer instructions about how to enroll their devices.  
* Improved troubleshooting options.  

#### Web apps launched from the Windows Company Portal app<!-- 5030972 -->
End-users can now launch web apps directly from the Windows Company Portal app. End-users can select the web app and then choose the option **Open in browser**. The published web URL is opened directly in a web browser. This functionality will be rolled out over the next week. For more information about Web apps, see [Add web apps to Microsoft Intune](~/intune/apps/web-app.md).  

#### New assignment type column in Company Portal for Windows 10 <!-- 5459950  -->
The Company Portal > **Installed Apps** > **Assignment type** column has been renamed to **Required by your organization**.  Under that column, users will see a **Yes** or **No** value to indicate that an app is either required or made optional by their organization. These changes were made because device users were confused about the concept of available apps. Your users can find more information about installing apps from Company Portal in [Install and share apps on your device](/intune-user-help/install-apps-cpapp-windows). For more  information about configuring the Company Portal app for your users, see [How to configure the Microsoft Intune Company Portal app](~/intune/apps/company-portal-app.md).  

<!-- ########################## -->
## Week of November 4, 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Security baselines are supported on Microsoft Azure Government<!-- 4062552 -->

Instances of  Intune that are hosted on *Microsoft Azure Government* can now use [security baselines](../intune/protect/security-baselines.md) to help you secure and protect your users and devices.

## What's New archive
For previous months, see the [What's New archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


