---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 07/22/2020
ms.topic: reference
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

# In development for Microsoft Intune

To help in your readiness and planning, this page lists Intune UI updates and features that are in development but not yet released. In addition to the information on this page: 

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in Office message center.
- When a feature enters production, whether it's a preview or generally available, the feature description will move from this page to [What's new](whats-new.md).
- This page and the [What's new](whats-new.md) page are updated periodically. Check back for additional updates.
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

> [!NOTE]
> This page reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This page doesn't describe all features in development.

**RSS feed**: Find out when this page is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**This article was last updated on the date listed under the title above.**

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

### Update to device icons in Company Portal and Intune apps on Android<!-- 6057023  -->
We're updating the device icons in the Company Portal and Intune apps on Android devices to create a more modern look and feel and to align with the Microsoft Fluent Design System. For related information, see [Update to icons in Company Portal app for iOS/iPadOS and macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

### iOS Company Portal will support Apple's Automated Device Enrollment without user affinity<!-- 7282707  --> 
iOS Company Portal will be supported on devices enrolled using Apple's Automated Device Enrollment without requiring an assigned user. An end user can sign in to the iOS Company Portal to establish themselves as the primary user on an iOS/iPadOS device enrolled without device affinity. For more information about Automated Device Enrollment, see [Automatically enroll iOS/iPadOS devices with Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md).

### The Company Portal adds Configuration Manager application support<!-- 4297660 -->
The Company Portal now supports Configuration Manager applications. This feature allows end users to see both Configuration Manager and Intune deployed applications in the Company Portal for co-managed customers. This support will help administrators consolidate their different end-user portal experiences. For more information, see [Use the Company Portal app on co-managed devices](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

### Unified delivery of Azure AD Enterprise and Office Online applications in the Windows Company Portal<!-- 1817861  -->
In the 2006 release, we announced [Unified delivery of Azure AD Enterprise and Office Online applications in the Company Portal](../fundamentals/whats-new.md#unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal). This feature is now supported in the Windows Company Portal. On the **Customization** pane of Intune, you can select to **Hide** or **Show** both **Azure AD Enterprise applications** and **Office Online applications** in the Windows Company Portal. Each end-user will see their entire application catalog from the chosen Microsoft service. By default, each additional app source will be set to **Hide**. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Customization** to find this configuration setting. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

<!-- ***********************************************-->
## Device configuration

### Set device compliance state from third-party MDM partners<!-- 6361689   -->
Microsoft 365 customers who own third-party MDM solutions will be able to enforce Conditional Access policies for Microsoft 365 apps on iOS and Android via integration with Microsoft Intune Device Compliance service. Third-party MDM vendor will leverage the Intune Device Compliance service to send device compliance data to Intune. Intune will then evaluate to determine if the device is trusted and set the conditional access attributes in Azure AD.  Customers will be required to set Azure AD Conditional Access policies from within the Microsoft Endpoint Manager admin center or the Azure AD portal.

### Create PKCS certificate profiles for Android Enterprise Fully Managed devices (COBO)<!-- 4839686 -->
You can create PKCS certificate profiles to deploy certificates to Android Enterprise Device owner and Work profile devices (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise > Device owner only**, or **Android Enterprise > Work profile only** for platform > **PKCS** for profile).

Soon you'll be able to create PKCS certificate profiles for Android Enterprise Fully Managed devices. The Intune PFX certificate connector is required. If you don't use SCEP, and only use PKCS, you can remove the NDES connector after you install the new PFX connector. The new PFX connector imports PFX files, and deploys PKCS certificates to all platforms.

For more information on PKCS certificates, see [Configure and use PKCS certificates with Intune](../protect/certficates-pfx-configure.md).

Applies to:
- Android Enterprise fully managed (COBO)

### Use NetMotion as a VPN connection type for iOS/iPadOS, and macOS devices<!-- 1333631 -->
When you create a VPN profile, NetMotion is available as a VPN connection type (**Devices** > **Device configuration** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **VPN** for profile > **NetMotion** for connection type).

For more information on VPN profiles in Intune, see [Create VPN profiles to connect to VPN servers](../configuration/vpn-settings-configure.md).

Applies to:
- iOS/iPadOS
- macOS

### More Protected Extensible Authentication Protocol (PEAP) options for Windows 10 Wi-Fi profiles<!-- 3805024 -->
On Windows 10 devices, you can create Wi-Fi profiles using the Extensible Authentication Protocol (EAP) to authenticate Wi-Fi connections (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Wi-Fi** for profile > **Enterprise**). When you select Protected EAP (PEAP), there are new settings available:

- **Perform server validation in PEAP phase 1**: In PEAP negotiation phase 1, devices validate the certificate, and verify the server.
  - **Disable user prompts for server validation in PEAP phase 1**: In PEAP negotiation phase 1, user prompts asking to authorize new PEAP servers for trusted certification authorities aren't shown.
- **Require cryptographic binding**: Prevents connections to PEAP servers that don't use cryptobinding during the PEAP negotiation.

To see the settings you can currently configure, go to [Add Wi-Fi settings for Windows 10 and later devices](../configuration/wi-fi-settings-windows.md).

Applies to: 
- Windows 10 and newer

### Configure the macOS Microsoft Enterprise SSO plug-in<!-- 5627576 -->
The Microsoft Azure AD team created a redirect single sign-on (SSO) app extension to allow macOS 10.15+ users to gain access to Microsoft apps, organization apps, and websites that support Apple's SSO feature and authenticate using Azure AD, with one sign-on. With the Microsoft Enterprise SSO plug-in release, you can configure the SSO extension with the new Microsoft Azure AD app extension type (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device features** for profile >  **Single sign-on app extension** > SSO app extension type > **Microsoft Azure AD**).

To achieve SSO with the Microsoft Azure AD SSO app extension type, users need to install and sign in to the Company Portal app on their macOS devices. 

For more information about macOS SSO app extensions, see [Single sign-on app extension](../configuration/device-features-configure.md#single-sign-on-app-extension).

Applies to:
- macOS 10.15 and newer

### Use SSO app extensions on more iOS/iPadOS apps with the Microsoft Enterprise SSO plug-in<!-- 7369991 -->
The [Microsoft Enterprise SSO plug-in for Apple devices](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin) can be used with all apps that support SSO app extensions. In Intune, this feature means the plug-in works with mobile iOS/iPadOS apps that don't use the Microsoft Authentication Library (MSAL) for Apple devices. The apps don't need to use MSAL, but they do need to authenticate with Azure AD endpoints.

To configure your iOS/iPadOS apps to use SSO with the plug-in, add the app bundle identifiers in an iOS/iPadOS configuration profile (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **Single sign-on app extension** > **Microsoft Azure AD** for SSO app extension type > **App bundle IDs**).

To see the current SSO app extension settings you can configure, go to [Single sign-on app extension](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

Applies to:
- iOS/iPadOS

### Improvement to **Update device settings** page in Company Portal app for Android to shows descriptions<!-- 7414768 -->
In the Company Portal app on Android devices, the **Update device settings** page lists the settings a user needs to update to be compliant. We have improved the user experience so that listed settings are expanded by default to show the description and the RESOLVE button (when applicable). Previously, they defaulted to collapsed. This new default behavior reduces the number of clicks, so users can resolve issues more quickly.

<!-- ***********************************************-->
<!-- ## Device enrollment-->




<!-- ***********************************************-->
## Device management

### PowerShell scripts support for BYOD devices<!-- 1862833  -->
PowerShell scripts will support Azure AD registered devices in Intune. For more information about PowerShell, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md). This functionality does not support devices running Windows 10 Home edition.

### Log Analytics will include device details log<!--6014987  -->
Intune device detail logs will be available in **Reports** > **Log analytics**. You can correlate device details to build custom queries and Azure workbooks.

### Tenant attach: Device timeline in the admin center<!--7220536, CM7141381 -->
When Configuration Manager synchronizes a device to Microsoft Endpoint Manager through tenant attach, you'll be able to see a timeline of events. This timeline shows past activity on the device that can help you troubleshoot problems. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### Tenant attach: Install an application from the admin center<!-- 7220536, CM6024389 -->
You'll be able to initiate an application install in real time for a tenant attached device from the Microsoft Endpoint Management admin center. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### Tenant attach: CMPivot from the admin center<!--7220536, CM6024392 -->
You'll be able to bring the power of [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to be able to initiate real-time queries from the cloud against an individual ConfigMgr managed device and return the results back to the admin center. This gives all the traditional benefits of CMPivot, which allows IT Admins and other designated personas the ability to quickly assess the state of devices in their environment and take action. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### Tenant attach: Run Scripts from the admin center<!--7220536, CM6234688 -->
You'll be able to bring the power of the Configuration Manager on-premises [Run Scripts](../../configmgr/apps/deploy-use/create-deploy-scripts.md) feature to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to run PowerShell scripts from the cloud against an individual Configuration Manager managed device. This gives all the traditional benefits of PowerShell scripts that have already been defined and approved by the Configuration Manager admin to this new environment. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### New merge logic for Windows 10 devices<!--179048-->
Today, if a customer reimages a device and then re-enrolls it, multiple records for the device will appear in the Microsoft Endpoint Manager admin console. New merge logic is in development to merge such duplicate records for Windows 10 devices.

### Deploy Software Updates to macOS devices <!-- 3194876 -->
You'll be able to deploy Software Updates to groups of macOS devices. This feature includes critical, firmware, configuration file, and other updates. You'll be able to send updates on the next device check-in or select a weekly schedule to deploy updates in or out of time windows that you set. This helps when you want to update devices outside standard work hours or when your help desk is fully staffed. You'll also get a detailed report of all macOS devices with updates deployed. You can drill into the report on a per-device basis to see the statuses of particular updates.

### Collect logs remote actions<!--2167272 -->
A new remote action, *Collect logs*, will let you collect the logs from corporate devices without interrupting or waiting for the end user. Collected logs will include MDM, Autopilot, event viewers, key, Configuration Manager client, networking, and other critical troubleshooting logs.

The new remote action will be located at [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **All devices** > choose a device > **Collect logs**.

### Associated licenses revoked before deletion of Apple VPP token<!--6195322 -->
In a future update, when you delete an Apple VPP token in Microsoft Endpoint Manager, all Intune-assigned licenses associated with that token will be automatically revoked before the deletion.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Power BI compliance report template V2.0<!-- 636958  -->
Admins will be able to update the Power BI compliance report template version from V1.0 to V2.0. V2.0 will include an improved design, as well as changes to the calculations and data that are being surfaced as part of the template. For related information, see [Connect to the Data Warehouse with Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
## Role-based access control

### Scope tag support for customization policies<!--6182440 -->
You'll be able to assign scope tags to Customization policies. To do so, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration**> **Customization** where you will see **Scope tags** configuration options.

<!-- ***********************************************-->
## Security

### App protection policy support for Symantec Endpoint Security and Check Point Sandblast<!--  4452423, 4731168 -->

In October of 2019, Intune app protection policy added the capability to use data from some of our Microsoft Threat Defense partners (MTD partners). We are adding support for the following partners, to use an app protection policy to block, or selectively wipe the user's corporate data based on the health of a device:

- **Check Point Sandblast** on Android, iOS and iPadOS
- **Symantec Endpoint Security** on Android, iOS and iPadOS

For information about using app protection policy with MTD partners, see [Create Mobile Threat Defense app protection policy with Intune](../protect/mtd-app-protection-policy.md).

### Microsoft Defender ATP creates Endpoint Manager Security task with vulnerability details<!-- 5568193  -->
Threat and Vulnerability Management (TVM) in Microsoft Defender ATP discovers misconfigured security settings on devices. Administrators use this information to update vulnerable devices.

Soon, Microsoft Defender ATP can raise an Endpoint Manager Security task (**Endpoint Manager** > **Endpoint Security** > **Security tasks**) with the vulnerability details, and show the affected devices. IT administrators can accept the security task, and deploy the required configuration. 

For more information on security tasks, see [Use Intune to remediate vulnerabilities identified by Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md).

### Changes for Endpoint security Antivirus policy exclusions<!--5583940, 6018119  -->
We’re introducing two changes for managing the Microsoft Defender Antivirus exclusion lists you configure as part of an Endpoint Security Antivirus policy. (**Endpoint security** > **Antivirus** > **Create Policy** > **Windows 10 and later** for platform). These two changes help prevent conflicts between policies, and existing policies that were in conflict will no longer be in conflict for the list of exclusions:

- First, we are adding a new profile type for Windows 10 and later; **Microsoft Defender Antivirus exclusions**.  This new profile type includes only the settings for specifying a list of Defender *processes*, *file extensions*, and *files* and *folders* that you don’t want Microsoft Defender to scan. This can help you simplify management of your exclusion lists by separating them from other policy configurations.
- The second change is that the list of exclusions you define in different profiles will merge into a single list of exclusions for each device or user, based on the individual policies that apply to a specific user or device. For example, when you target a user with three separate policies, the exclusion lists from those three policies are merged into a single superset of Microsoft Defender Antivirus exclusions, which are then applied to the user. This merge includes the exclusions lists from the new profile type were adding, as well as from any existing policies you have that were configured in a *Microsoft Defender Antivirus* profile.

### Add tri-state support to additional settings in the Microsoft Defender Firewall profile<!-- 7122957  -->
We're updating settings in the Microsoft Defender Firewall profile, which is part of the endpoint security Firewall policy for windows 10. (**Endpoint security** > **Firewall** > **Create Policy** > **Windows 10 and later** > **Microsoft Defender Firewall**)  This update will add support for a third option of *No* to the settings that currently support only *Yes* and *Not configured*.


<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
