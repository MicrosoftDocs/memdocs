---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 05/31/2023
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

### Intune migrating from SafetyNet Attestation API to Google Play Integrity API<!-- 15571389   -->  
Google has deprecated the [SafetyNet Attestation API](https://developer.android.com/training/safetynet/attestation) and replaced it with the [Play Integrity API](https://developer.android.com/google/play/integrity). Intune will be migrating to the new API for app protection policies. The “SafetyNet device attestation” setting name will be updated to align with the new Google Play Integrity API for all policies in the Intune user interface (UI). For related information, see [Discontinuing the SafetyNet Attestation API](https://developer.android.com/training/safetynet/deprecation-timeline) and [Migrating from the SafetyNet Attestation API](https://developer.android.com/google/play/integrity/migrate).

### View app report for Android Enterprise corporate-owned devices<!-- 2055436  -->  
You'll be able to view a report containing all apps found on a device for Android Enterprise corporate-owned scenarios, including system apps. This report will be available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Monitor** > **Discovered apps**. You will see **Application Name** and **Version** for all apps detected as installed on the device.

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

### Intelligent recommendations within Intune Security Baselines<!-- 11127203 -->
We are adding tailored insights powered by Machine Learning models that help choose the right security settings from Security Baselines for your organization. These recommendations are based on best practices that similar organizations have adopted. Navigate to **Endpoint security** > **Security baselines** . While creating and editing the workflow these insights will be available for you in the form of a light bulb. 

### New settings available in the Apple settings catalog<!-- 19951554  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

**Authentication > Extensible Single Sign On (SSO)**:

- Denied Bundle Identifiers

Applies to:

- iOS/iPadOS
- macOS

**Login > Login Window Behavior**:

- Disable FDE Auto Login

Applies to:

- macOS

**Networking > Network Usage Rules**:

- SIM Rules

Applies to:

- iOS/iPadOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Android Enterprise 11+ devices can use Zebra's latest OEMConfig app version<!-- 8675347  -->  
On Android Enterprise devices, you can use OEMConfig to add, create, and customize OEM-specific settings in Microsoft Intune (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **OEMConfig**).

There's a new **Zebra OEMConfig Powered by MX** OEMConfig app that aligns more closely to Google’s standards. You'll be required to use this new app on Android Enterprise 11.0 and newer devices.

The older **Legacy Zebra OEMConfig** app continues to support devices with Android 11 and earlier. In your Managed Google Play, you'll see two versions of Zebra OEMConfig app. Be sure to select the correct app that applies to your Android device versions.

For more information on OEMConfig and Intune, go to [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Applies to:

- Android Enterprise 11.0 and newer

### Device Firmware Configuration Interface (DFCI) supports Asus devices <!-- 10249874  -->  
For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type.

Some Asus devices running Windows 10/11 are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

For more information about DFCI profiles, go to:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](/mem/autopilot/dfci-management)

Applies to:

- Windows 10
- Windows 11

<!-- *********************************************** -->

## Device enrollment

### Apple Account Driven User Enrollment available for iOS/iPadOS 15+ devices<!-- 14161683  -->  
Intune will support Apple Account Driven User Enrollment, a new and improved variation of Apple User Enrollment for iOS/iPadOS 15+ devices. The new option will utilize just-in-time-registration, which eliminates the need for the Company Portal app during enrollment. Device users can initiate enrollment directly in the Settings app, resulting in a shorter and more efficient onboarding experience. You can continue to target iOS/iPadOS devices using the existing profile-based User Enrollment method with Company Portal. Devices running iOS/iPadOS, version 14.8.1 and earlier will be unaffected by this update and can also continue to use the existing method.

<!-- *********************************************** -->

## Device management

### Update to Endpoint Privilege Management reports<!-- 17727222  -->  
Intune's Endpoint Privilege Management (EPM) reports will support exporting the full reporting payload to a CSV file. This will allow you to export all events from an elevation report in Intune.

### On-demand proactive remediation for a Windows device<!-- 14783338  -->  
A new device action that is in public preview allows you to run a proactive remediation on-demand to a single Windows device. The **Run** remediation device action will allow you to resolve issues without having to wait for a proactive remediation to run on its assigned schedule. You'll also be able to view the status of proactive remediations under **Remediations** in the **Monitor** section of a device.

<!-- *********************************************** -->

<!-- ## Device security  -->

<!-- *********************************************** -->

<!-- ## Intune apps -->
<!-- *********************************************** -->

## Monitor and troubleshoot

### Microsoft Intune troubleshooting pane is now generally available<!-- 18099474 -->
The Intune troubleshooting pane is now generally available.  It will provide details about user's devices, policies, applications, and status. The troubleshooting pane will include the following information:
- A summary of policy, compliance, and application deployment status.
- Support for exporting, filtering, and sorting all reports.
- Support to filter by excluding policies and applications.
- Support to filter to a user’s single device.
- Details about available device diagnostics and disabled devices.
- Details about offline devices that haven't checked-in to the service for three or more days.

You can find the troubleshooting pane in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Troubleshoot**. 

<!-- *********************************************** -->

<!-- ## Role-based access control -->
<!-- *********************************************** -->

<!-- ## Tenant administration -->
<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
