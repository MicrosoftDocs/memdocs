---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: Microsoft Intune features in development
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 08/28/2020
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


<!-- ***********************************************-->
## Device configuration

### Create PKCS certificate profiles for Android Enterprise Fully Managed devices (COBO)<!-- 4839686 -->
You can create PKCS certificate profiles to deploy certificates to Android Enterprise Device owner and Work profile devices (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise > Device owner only**, or **Android Enterprise > Work profile only** for platform > **PKCS** for profile).

Soon you'll be able to create PKCS certificate profiles for Android Enterprise Fully Managed devices. The Intune PFX certificate connector is required. If you don't use SCEP, and only use PKCS, you can remove the NDES connector after you install the new PFX connector. The new PFX connector imports PFX files, and deploys PKCS certificates to all platforms.

For more information on PKCS certificates, see [Configure and use PKCS certificates with Intune](../protect/certificates-pfx-configure.md).

Applies to:
- Android Enterprise fully managed (COBO)

### Use NetMotion as a VPN connection type for Android Enterprise work profile devices<!-- 7764263 -->
When you create a VPN profile, NetMotion is available as a VPN connection type (**Devices** > **Device configuration** > **Create profile** > **Android Enterprise work profile** for platform > **VPN** for profile > **NetMotion** for connection type).

For more information on VPN profiles in Intune, see [Create VPN profiles to connect to VPN servers](../configuration/vpn-settings-configure.md).

Applies to:
- Android Enterprise work profile

### Changes for Password settings in Device restriction profiles for Android device administrator<!-- 7662279  --> 
We’re introducing a few changes for password settings for *Device restriction* and *compliance* policies for *Android device administrator*. (**Devices** > **Configuration profiles** > **Create profile** > **Device restrictions** and **Devices** > **Compliance policies** > **Create Policy**) These changes help Intune accommodate changes in Android version 10 and later, to ensure settings for passwords continue to apply to devices as expected.
 
Changes include:
- Removal of the top-level option for **Password**.  
- Settings will be reorganized into sections that are based on which devices they apply to.
- The **Minimum password length** will be disabled for use unless **Password type** is configured to a value where the password length applies.
- Additional updates to labels and example text.

These changes apply to the UI for settings, and won’t affect existing profiles. 

<!-- ***********************************************-->
## Device enrollment

### Ending support for iOS 11<!--7327321 -->
After iOS 14 releases, Intune enrollment and the Company Portal app will support iOS versions 12 and later. Older versions won't be supported but will continue to receive policies.

### Ending support for macOS 10.12<!--7327326 -->
After macOS 11 releases, Intune enrollment and the Company Portal will support macOS versions 10.13 and later. Older versions won't be supported.


<!-- ***********************************************-->
## Device management

### PowerShell scripts support for BYOD devices<!-- 1862833  -->
PowerShell scripts will support Azure AD registered devices in Intune. For more information about PowerShell, see [Use PowerShell scripts on Windows 10 devices in Intune](../apps/intune-management-extension.md). This functionality does not support devices running Windows 10 Home edition.

### Log Analytics will include device details log<!--6014987  -->
Intune device detail logs will be available in **Reports** > **Log analytics**. You can correlate device details to build custom queries and Azure workbooks.

### Tenant attach: Run Scripts from the admin center<!--7220536, CM6234688 -->
You'll be able to bring the power of the Configuration Manager on-premises [Run Scripts](../../configmgr/apps/deploy-use/create-deploy-scripts.md) feature to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to run PowerShell scripts from the cloud against an individual Configuration Manager managed device. This gives all the traditional benefits of PowerShell scripts that have already been defined and approved by the Configuration Manager admin to this new environment. For more information, see [Configuration Manager technical preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### Deploy Software Updates to macOS devices <!-- 3194876 -->
You'll be able to deploy Software Updates to groups of macOS devices. This feature includes critical, firmware, configuration file, and other updates. You'll be able to send updates on the next device check-in or select a weekly schedule to deploy updates in or out of time windows that you set. This helps when you want to update devices outside standard work hours or when your help desk is fully staffed. You'll also get a detailed report of all macOS devices with updates deployed. You can drill into the report on a per-device basis to see the statuses of particular updates.

<!-- ***********************************************-->
## Intune apps

### Unified delivery of Azure AD Enterprise and Office Online applications in the Windows Company Portal<!-- 1817861  -->
In the 2006 release, we announced [Unified delivery of Azure AD Enterprise and Office Online applications in the Company Portal](../fundamentals/whats-new.md). This feature will be supported in the Windows Company Portal. On the **Customization** pane of Intune, you will be able to select to **Hide** or **Show** both **Azure AD Enterprise applications** and **Office Online applications** in the Windows Company Portal. Each end-user will see their entire application catalog from the chosen Microsoft service. By default, each additional app source will be set to **Hide**. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you will select **Tenant administration** > **Customization** to find this configuration setting. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## Monitor and troubleshoot

### Power BI compliance report template V2.0<!-- 636958  -->
Admins will be able to update the Power BI compliance report template version from V1.0 to V2.0. V2.0 will include an improved design, as well as changes to the calculations and data that are being surfaced as part of the template. For related information, see [Connect to the Data Warehouse with Power BI](../developer/reports-proc-get-a-link-powerbi.md).



<!-- ***********************************************-->
<!--
## Role-based access control
-->

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



<!-- ***********************************************-->
## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
