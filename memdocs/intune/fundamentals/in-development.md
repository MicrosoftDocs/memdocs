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

# In development for Microsoft Intune - May 2020

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

### Support for multiple accounts in Company Portal for Mac<!-- 5779449  -->
The Company Portal on macOS devices now caches user accounts, making sign-in easier. Users no longer need to sign into the Company Portal every time they launch the application. Additionally, the Company Portal will display an account picker if multiple user accounts are cached, so that users don't have to enter their user name. 

### Auto update VPP available apps<!-- 3640511  -->
Apps that are published as Volume Purchase Program (VPP) available apps will be automatically updated when **Automatic App Updates** is enabled for the VPP token. Currently, VPP available apps do not automatically update. Instead, end-users must go to Company Portal and reinstall the app if a newer version is available. However, required apps currently do support automatic updates.

### Customize self-service device actions in the Company Portal<!--4393379  -->
You'll be able to customize the available self-service device actions that are shown to end-users in the Company Portal app and website. To help prevent unintended device actions, you'll be able to configure these settings for the Company Portal app by selecting **Tenant Administration** > **Customization** > **Create** > **Hide features**. The following actions are available:
- Hide **Remove** button on corporate Windows device.
- Hide **Reset** button on corporate Windows devices.
- Hide **Reset** button on corporate iOS devices.
- Hide **Remove** button on corporate iOS devices.

For more information, see [User self-service device actions from the Company Portal](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

### Control the display of Azure AD Enterprise or Office Online applications in the Company Portal<!--4404429 -->
You'll be able to toggle (**Hide** or **Show**) the display of Azure AD Enterprise or Office Online applications in the Company Portal. Each user will see their entire application catalog from the chosen Microsoft service. By default, each additional app source will be set to **Hide**. This feature will first take effect in the Company Portal website in the 2005 release with support in the Windows, iOS/iPadOS, and macOS Company Portals expected to follow. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Customization** to find this future setting. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

### Search the Intune docs from the Company Portal<!-- 1736480 -->
You can now search the Intune documentation directly from the Company Portal for macOS app. In the menu bar, select **Help** > **Search** and enter the key words of your search to quickly find answers to your questions.

### Company Portal for Android will guide users to get apps after work profile enrollment <!-- 6103999  -->
We're improving the in-app guidance in Company Portal to make it easier for users to find and install apps.  After they enroll in work profile management, users will see a message telling them they can find suggested apps in the badged version of Google Play. Users will also see a new **Get apps** link in the Company Portal drawer on the left. To make way for these new and improved experiences, the **APPS** tab will be removed. 

### Android Company Portal user experience<!-- 5736084 -->
In the 2005 release of Android Company Portal, end-users of Android devices that are issued a warn, block, or wipe by an app protection policy will see a new user experience. Instead of the current dialog experience, end-users will see a full page message describing the reason for the warn, block, or wipe and the steps to remediate the issue. For more information, see [App protection experience for Android devices](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) and [Android app protection policy settings in Microsoft Intune](../apps/app-protection-policy-settings-android.md).


<!-- ***********************************************-->
## Device configuration

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

### Configure system extensions on macOS devices<!-- 6255624  -->
On macOS devices, you can create a kernel extensions profile to configure settings at the kernel-level (**Devices** > **Configuration profiles** > **macOS** for platform > **Kernel extensions** for profile). Apple is eventually deprecating kernel extensions and replacing them with system extensions in a future release. System extensions run in the user space, and don’t give access to the kernel. The goal is to increase security and provide more end user control, while limiting attacks at the kernel level. Both kernel extensions and system extensions allow users to install app extensions that extend the native capabilities of the operating system.

In Intune, you can configure both kernel extensions and system extensions (**Devices** > **Configuration profiles** > **macOS** for platform > **System extensions** for profile). Kernel extensions apply to 10.13.2 and newer. System extensions apply to 10.15 and newer. From macOS 10.15 to macOS 10.15.4, kernel extensions and system extensions can run side-by-side. 

To learn about kernel extensions on macOS devices, see [Add macOS kernel extensions](../configuration/kernel-extensions-overview-macos.md).

Applies to:
- macOS 10.15 and newer

<!-- ***********************************************-->
## Device enrollment

### Bring-your-own-devices can use VPN to deploy<!--5015344 -->
The new  Autopilot profile **Skip Domain Connectivity Check** toggle lets you deploy Hybrid Azure AD Join devices without access to your corporate network using your own third party Win32 VPN client. To see the new toggle, go to [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices**  > **Windows** > **Windows enrollment** > **Deployment profiles** > **Create profile** > **Out-of-box experience (OOBE)**.

### Automated device sync interval down to 12 hours<!--3077535 -->
For Apple's Automated Device Enrollment, the automated device sync interval between Intune and Apple Business Manager will be reduced from 24 hours to 12 hours. For more information on sync, see [Sync managed devices](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).

### Autopilot support for Hololens 2 devices<!--6305220-->
Windows Autopilot will support Hololens 2 devices. For more information on using Autopilot in Intune, see [Enroll Windows devices in Intune by using the Windows Autopilot](../enrollment/enrollment-autopilot.md).

### Enrollment restrictions will support scope tags<!--4209550 -->
You'll be able to assign scope tags to enrollment restrictions. To do so, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Enrollment restrictions** > **Create restriction**. Create either type of restriction and you'll see the **Scope tags** page.

### Shared iPads for Business<!--6367326 -->
You'll be able to use Intune and Apple Business Manager to easily and securely set up Shared iPad so that multiple employees can share devices. Apple's [Shared iPad](https://developer.apple.com/education/shared-ipad/) provides a personalized experience for multiple users while preserving user data. Using a Managed Apple ID, users can access their apps, data, and settings after signing into any Shared iPad in their organization. Shared iPad works with federated identities.

To see this feature, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **iOS** > **iOS enrollment** > **Enrollment program tokens** > choose a token** > **Profiles** > **Create profile** > **iOS**. On the **Management Settings** page, select **Enroll without User Affinity** and you'll see the **Shared iPad** option.

**Applies to:** iPadOS 13.4 and later. This release added support for temporary sessions with Shared iPad so that users can access a device without a Managed Apple ID. Upon logout, the device erases all user data so that the device is immediately ready for use, eliminating the need for a device wipe. 

<!-- ***********************************************-->
## Device management

### PowerShell scripts support for BYOD devices<!-- 1862833  -->
PowerShell scripts will support Azure AD registered devices in Intune. For more information about PowerShell, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md). This functionality does not support devices running Windows 10 Home edition.

### Log Analytics will include device details log<!--6014987  -->
Intune device detail logs will be available in **Reports** > **Log analytics**. You can correlate device details to build custom queries and Azure workbooks.

### New details for the Autopilot report<!--5405786 -->
To see the new details about App and Policy install status, go to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Monitor** > **Autopilot deployments**.

### macOS script support<!-- 6376978  -->
Script support for macOS is now generally available. In addition, we will be adding support for both user assigned scripts and macOS devices that have been enrolled with Apple's Automated Device Enrollment (formerly Device Enrollment Program). For more information, see [Use shell scripts on macOS devices in Intune](../apps/macos-shell-scripts.md).

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Power BI compliance report template V2.0<!-- 636958  -->
Admins will be able to update the Power BI compliance report template version from V1.0 to V2.0. V2.0 will include an improved design, as well as changes to the calculations and data that is being surfaced as part of the template. For related information, see [Connect to the Data Warehouse with Power BI](../developer/reports-proc-get-a-link-powerbi.md).

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

### Set device compliance state from third-party MDM partners<!-- 6361689      -->
You’ll soon be able to allow the compliance state of iOS or Android devices managed by third-party Mobile Device Management (MDM) partners to be set in Azure Active Directory (Azure AD).

When Intune is configured for partner compliance, compliance data for devices managed by the third-party MDM partner is sent to Intune for compliance evaluation. The results are then passed to Azure AD where the compliance data is used to enforce your conditional access policies for those devices.

Support will soon include the following partners:
- VMware WorkspaceONE (previously known as AirWatch)

To enable a device compliance partner you’ll use a new node in the Microsoft Endpoint Manager admin center: **Tenant Administration** > **Connectors and Tokens** > **Partner Compliance management** where you’ll select **Add Compliance Partner**.

### Duplicate your policies in Endpoint Security<!-- 5892558   -->
You’ll be able to select a policy you’ve created in the Endpoint security node of the Microsoft Endpoint Manager admin center, and then duplicate it to create a copy.  The policies you’ll be able to duplicate include those you create for:

- Antivirus
- Disk encryption
- Firewall
- Endpoint detection and response
- Attack surface reduction
- Account protection

Duplication will make a copy of the original policy, which you can then rename and edit. The copy will not include assignments from the original.

### Send push notifications as an action for non-compliance <!-- 1733150   -->
For iOS and Android platforms, we are adding a new action for non-compliance that will send an app push notification through the Company Portal app. Users can click on the notifications which will launch the Company Portal app that then displays the reason they are non-compliant. Admins will be able to configure this new action for non-compliance in the Microsoft Endpoint Manager admin center by going to **Devices** > **Compliance policies** > **Create policy**, and then selecting the *Action* to send an app push notification. 

### New profile for Endpoint Security Firewall policy<!-- 5653324   -->
As a preview, we're adding an additional profile for Windows 10 and later to the Firewall policy in Intune's Endpoint security (**Endpoint security** > **Firewall** > **Create Policy** > select **Windows 10 and later**). 

Each instance of this new profile supports up to 150 custom *Microsoft Defender Firewall rules*. The Microsoft Defender Firewall rules profile allows you define granular Windows Firewall rules to allow or block ports and applications in Windows 10.

<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).



