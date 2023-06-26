---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 06/29/2023
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
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. Also:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description will move from this article to [What's new](whats-new.md).  
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](whats-new.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Tenant administration
## Notices
-->

<!-- ***********************************************-->

## App management

### Intune moving to support new Google Play Android Management API<!-- 10982449  -->  
You will see several changes to how Managed Google Play public apps in Intune are managed. These changes are being made so we can adopt [Google’s Android Management APIs](https://developers.google.com/android/management) (opens Google's web site).

To learn more about changes to the admin and user experience, go to [Support Tip: Intune moving to support new Google Play Android Management API](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-intune-moving-to-support-new-google-play-android/ba-p/3849875).

Applies to:

- Android Enterprise

## Deploy unmanaged PKG-type applications to managed macOS devices<!-- 17296091  -->  
You will be able to upload and deploy unmanaged PKG-type applications to managed macOS devices using the Intune MDM agent for macOS devices. This feature enables you to deploy custom PKG installers, such as unsigned apps and component packages.

You can add a PKG app in the Intune admin center: **Apps** > **macOS** > **Add** > **macOS app (PKG)** for app type.

To deploy managed PKG-type apps, you can continue to [add macOS line-of-business (LOB) apps to Microsoft Intune](../apps/lob-apps-macos.md).

For more information on the Intune MDM agent for macOS devices, go to [Microsoft Intune management agent for macOS](../apps/lob-apps-macos-agent.md).

Applies to:

- macOS

### Updates to app configuration policy reporting<!-- 18098046  -->  
As part of our continuing efforts to improve the Intune reporting infrastructure, there will be several user interface (UI) changes for app configuration policy reporting. The UI will be updated with the following changes:

- There will no longer be either a **User status** tile or a **Not applicable device** tile on the **Overview** section of the **App configuration policies** workload.
- There will no longer be a **User install status** report on the **Monitor** section of the **App configuration policies** workload. 
- The **Device install status** report under the **Monitor** section of the **App configuration policies** workload will no longer show the **Pending state** in the **Status** column.

You can find configure policy reporting in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **App configuration policies**.

### Default settings when adding Windows PowerShell scripts is changing<!-- 20986905  -->  
In Intune, you can use policies to deploy Windows PowerShell scripts to your Windows devices (**Devices** > **Scripts** > **Add** > **Windows 10 and later**).

When you add a Windows PowerShell script, there are settings you configure. To increase secure-by-default behavior of Intune, the default behavior of the following settings is changing:

- The **Run this script using the logged on credentials** setting defaults to **Yes**. Previously, the default was **No**.
- The **Enforce script signature check** setting defaults to **Yes**. Previously, the default was **No**.

This behavior applies to new scripts you add, not existing scripts.

For more information on using Windows PowerShell scripts in Intune, go to [Use PowerShell scripts on Windows 10/11 devices in Intune](../apps/intune-management-extension.md).

Applies to:

- Windows 10 and later (excluding Windows 10 Home)

### New settings available for the iOS/iPadOS web clip app type<!-- 21084128  -->  
In Intune, you can pin web apps to your iOS/iPadOS devices (**Apps** > **iOS/iPadOS** > **Add** > **iOS/iPadOS web clip**). When you add web clips, there are new settings available:

- **Full screen**: If true, launches the web clip as a full-screen web app without a browser. There’s no URL or search bar, and no bookmarks.
- **Ignore manifest scope**: If true, a full screen web clip can go to an external web site without showing Safari UI. Otherwise, Safari UI appears when going away from the web clip’s URL. This key has no effect when Full screen is set to false. Available in iOS 14 and later.
- **Precomposed**: If true, prevents SpringBoard from adding "shine" to the icon.
- **Target application bundle identifier**: Enter the application bundle identifier that specifies the application that opens the URL. Available in iOS 14 and later.

For more information on the settings you can currently configure, go to [Add web apps to Microsoft Intune](../apps/web-app.md).

Applies to:

- iOS/iPadOS





### Intune migrating from SafetyNet Attestation API to Google Play Integrity API<!-- 15571389   -->  
Google has deprecated the [SafetyNet Attestation API](https://developer.android.com/training/safetynet/attestation) and replaced it with the [Play Integrity API](https://developer.android.com/google/play/integrity). Intune will be migrating to the new API for app protection policies. The "SafetyNet device attestation" setting name will be updated to align with the new Google Play Integrity API for all policies in the Intune user interface (UI). For related information, see [Discontinuing the SafetyNet Attestation API](https://developer.android.com/training/safetynet/deprecation-timeline) and [Migrating from the SafetyNet Attestation API](https://developer.android.com/google/play/integrity/migrate).

### View app report for Android Enterprise corporate-owned devices<!-- 2055436  -->  
You'll be able to view a report containing all apps found on a device for Android Enterprise corporate-owned scenarios, including system apps. This report will be available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Monitor** > **Discovered apps**. You'll see **Application Name** and **Version** for all apps detected as installed on the device.

### Advanced application management<!-- 10986080  -->  
Advanced application management provides you with an enterprise catalog of applications that are easily accessible. It also provides application update capabilities. The enterprise catalog is planned to be available in public preview in late Q2 2023. The application update capabilities are planned to be available in early Q3 2023.

### Company Portal automatically installed on Android Enterprise dedicated devices<!-- 6423852  -->  
Intune Company Portal will now be automatically installed on all Android Enterprise dedicated devices to ensure the appropriate handling of app protection policies. Users won't be able to see or launch the Company Portal, and there are no requirements for users to interact with it. Admins will notice that the Company Portal is automatically installed on their Android Enterprise dedicated devices, without the ability to uninstall.

### Uninstall Win32 apps in the Company Portal<!-- 5145748 -->  
*The time frame for the release of this update is still being determined.*

Users will be able to uninstall Win32 apps in the Company Portal. If a Win32 app can be uninstalled by the user, the user will be able to select **Uninstall** for the Win32 app in the Company Portal. For more information about Win32 apps, go to [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

### Support for multi-SIM iOS/iPadOS device inventory<!--17016690 (replaced 16360290 for tracking -->

You'll be able to view the service subscription fields on devices that have multiple SIM cards installed under the per-device Hardware section. The inventory fields that are capable of reporting multiple values to Intune are:

- **ICCID**
- **IMEI**
- **MEID**
- **Phone number**

These fields will default to using labels returned by the device, such as:  *Primary*, *Secondary*, *CTSubscriptionSlotOne*, and *CTSubscriptionSlotTwo*. These returned labels may be displayed in the language of the local device that is reporting its inventory to Intune.

Applies to:  
- **iOS/iPadOS**

<!-- *********************************************** -->

## Device configuration

### New settings available in the macOS settings catalog <!-- 24167142  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. 

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **macOS** > **Settings catalog** for profile type.

**Microsoft AutoUpdate (MAU)**:

- Current Channel (Monthly)

**Microsoft Defender > User interface preferences**:

- Control sign-in to consumer version

**Microsoft Office > Microsoft Outlook**:

- Disable 'Do not send response'

**User Experience > Dock**:

- MCX Dock Special Folders

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Added Support for Scope tags<!-- 16485280 iddraft  -->  
You will be able to add scope tags when creating deployments using Zebra LifeGuard Over-the-Air integration (in public preview). 

### Intelligent recommendations within Intune Security Baselines<!-- 11127203 -->
We're adding tailored insights powered by Machine Learning models that help choose the right security settings from Security Baselines for your organization. These recommendations are based on best practices that similar organizations have adopted. Navigate to **Endpoint security** > **Security baselines**. Creating and editing the workflow these insights will be available for you in the form of a light bulb.

<!-- *********************************************** -->

## Device enrollment

### Apple Account Driven User Enrollment available for iOS/iPadOS 15+ devices<!-- 14161683  -->  
Intune will support Apple Account Driven User Enrollment, a new and improved variation of Apple User Enrollment for iOS/iPadOS 15+ devices. The new option will utilize just-in-time-registration, which eliminates the need for the Company Portal app during enrollment. Device users can initiate enrollment directly in the Settings app, resulting in a shorter and more efficient onboarding experience. You can continue to target iOS/iPadOS devices using the existing profile-based User Enrollment method with Company Portal. Devices running iOS/iPadOS, version 14.8.1 and earlier will be unaffected by this update and can also continue to use the existing method.

<!-- *********************************************** -->

## Device management

### Intune will support iOS/iPadOS 15.x as the minimum version<!-- 24161619  -->  
Later this year, Apple is expected to release iOS/iPadOS version 17. After the release of iOS/iPadOS 17, the minimum version supported by Intune will be iOS/iPadOS 15.x.

For more information on this change, go to [Plan for change: Intune is moving to support iOS/iPadOS 15 and later](whats-new.md#plan-for-change-intune-is-moving-to-support-iosipados-15-and-later).

Applies to:

- iOS/iPadOS

### On-demand proactive remediation for a Windows device<!-- 14783338  -->  
A new device action that is in public preview allows you to run a proactive remediation on-demand to a single Windows device. The **Run** remediation device action will allow you to resolve issues without having to wait for a proactive remediation to run on its assigned schedule. You'll also be able to view the status of proactive remediations under **Remediations** in the **Monitor** section of a device.

<!-- *********************************************** -->

## Device security

### Endpoint Privilege Management support to manage elevation rules for child processes<!-- 15931887  -->
With [Endpoint Privilege Management](../protect/epm-overview.md) (EPM) you can manage which files and processes are allowed to *Run as Administrator*. When a process is elevated to run in the administrative context, any child processes it creates inherit that administrative context.
 
Soon, EPM will support options that let you control the run context of those child processes. You’ll be able to allow a child process to always run elevated, run elevated only if a rule exists for the child process, or never run elevated (always run as a standard user). 

### Tamper protection support for Windows on Azure Virtual Desktop<!--15135590  -->
Intune will soon support use of Tamper protection for Windows on Azure Virtual Desktop multi- session.  Support for Tamper protection requires onbarding to Microsoft Defender for Endpoint before the policy that enables Tamper protection is applied. 


### Microsoft Defender for Endpoint Settings Management enhancements<!-- 14743017, 15319901, 18713045, 18713050 -->  
Microsoft Defender for Endpoint Settings Management will expand platform support for Linux Servers and macOS channel. This applies to the Linux and macOS Antivirus policy templates found in **Endpoint Security** > **Antivirus**. In addition, onboarding devices to Microsoft Defender for Endpoint settings management will be simplified to no longer have Azure AD Hybrid Join be a management prerequisite for existing and new policies. You'll also be able to create, edit, and find all Intune Endpoint Security policies through the Microsoft Defender for Endpoint portal.

<!-- *********************************************** -->

<!-- ## Intune apps -->
<!-- *********************************************** -->

<!-- ## Monitor and troubleshoot -->
<!-- *********************************************** -->

<!-- ## Role-based access control -->
<!-- *********************************************** -->

<!-- ## Tenant administration -->
<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
