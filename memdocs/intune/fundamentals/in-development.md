---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 10/31/2022
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
  - M365-identity-device-management
  - highpri
  - highseo
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. In addition to the information in this article:

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

### Uninstall Win32 apps in the Company Portal<!-- 5145748 -->  
Users will be able to uninstall Win32 apps in the Company Portal. If a Win32 app can be uninstalled by the user, the user will be able to select **Uninstall** for the Win32 app in the Company Portal. For more information about Win32 apps, go to [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

### Configure whether to show apps from Configuration Manager in Windows Company Portal<!-- 9135109 -->  
In the Intune console, you'll be able to choose whether to show or hide Configuration Manager apps from appearing in the Windows Company Portal. This option will be available in [Intune](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Customization**. Next to **Settings**, select **Edit**. The option to **Show** or **Hide** the **Configuration Manager applications will be located in the **App Sources** section of the pane. For related information about configuring the Company Portal app, see [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).


### Global quiet time app policy settings<!-- 15424417 -->
The global quiet time settings will allow you to create policies to schedule quiet time for your end users which will automatically mute Microsoft Outlook email and Teams notifications on iOS/iPadOS and Android platforms. These policies can be used to limit end user notifications received after work hours. When this feature is available, you will be able to find it in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Quiet Time** > **Policies**.

### Control the display of Managed Google Play apps<!-- 621615  -->
You will be able to group Managed Google Play apps into collections and control the order that collections are displayed when selecting apps in Intune. You will also be able to make apps visible via search only. This capability will be available in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **All apps** > **Add** > **Managed Google Play app**.

<!-- ***********************************************-->

## Device configuration

### Device Firmware Configuration Interface (DFCI) will support Panasonic devices<!-- 15729353 -->  
For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type).

New Panasonic devices running Windows 10/11 will be enabled for DFCI starting Fall 2022. So, admins can create DFCI profiles to manage the BIOS and then deploy the profiles to these Panasonic devices.

Contact your device vendor or device manufacturer to ensure you get eligible devices.

For more information about DFCI profiles in Intune, go to [Use Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md).

Applies to:

- Windows 10
- Windows 11

### Login and background item management support on macOS devices using the settings catalog<!-- 15751007 -->  
On macOS devices, you can open items automatically when users sign in to their macOS devices. For example, you can open apps, documents, and folders.

In Intune, the settings catalog will include new Service Management settings that can prevent users from disabling the managed login and background items on their devices in System Settings > General > Login Items.

For more information on the settings catalog, go to:

- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)
- [Common tasks you can complete using the Settings Catalog](../configuration/settings-catalog-common-features.md)

Applies to:

- macOS 13 and newer

### New password complexity requirements for Android Enterprise 12+ personally owned devices with a work profile<!-- 12436068 -->
On Android Enterprise 11 and older personally owned devices with a work profile, you can set the **Required password type** and a **Minimum password length** in device configuration profiles and compliance policies.

Google is deprecating these features for Android 12+ personally owned devices with a work profile and replacing them with new password complexity requirements. For more information about this change, go to [Day zero support for Android 13](https://aka.ms/Intune/Android13).

The new **Password complexity** setting will have the following options:

- **Not configured**: Intune doesn't change or update this setting. By default, the OS may not require a password.
- **Low**: Pattern or PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked.
- **Medium**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length, alphabetic length, or alphanumeric length must be at least 4 characters.
- **High**: PIN with repeating (4444) or ordered (1234, 4321, 2468) sequences are blocked. The length must be at least 8 characters. The alphabetic or alphanumeric length must be at least 6 characters.

If you currently use the **Required password type** and **Minimum password length** settings in your device configuration and compliance policies on Android 12+, then we recommend using the new **Password complexity** setting instead.

If you continue to use the **Required password type** and **Minimum password length** settings, and don't configure the **Password complexity** setting, then new devices running Android 12+ will default to the **High** password complexity.

There is no impact for existing devices with the **Required password type** and **Minimum password length** settings configured.

For more information on the existing settings you can configure, go to:

- [Android Enterprise personally owned devices with a work profile - configuration profile settings list](../configuration/device-restrictions-android-for-work.md#personally-owned-devices-with-a-work-profile)
- [Android Enterprise personally owned devices with a work profile - compliance policy settings list](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile)

Applies to:
- Android 12.0 and newer
- Android Enterprise personally owned devices with a work profile

<!-- ***********************************************-->

## Device management

### Endpoint security firewall rules support for ICMP type<!-- 5653356 -->
We’re adding a new setting named **IcmpTypesAndCodes** to the endpoint security firewall rules template for Windows 10. To configure this in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Endpoint security** > **Firewall** > **Create Policy** > Platform: *Windows 10, Windows 11, and Windows Server*  > Profile: *Microsoft Defender Firewall Rules*).

With this new setting you’ll be able to configure inbound and outbound rules for [Internet Control Message Protocol](/windows/security/threat-protection/windows-firewall/create-an-inbound-icmp-rule) (ICMP) as part of a firewall rule.

Applies to:  
- Windows 10, Windows 11, and Windows Server

<!-- ***********************************************-->

## Device security

### Microsoft Tunnel for Mobile Application Management for Android (public preview)<!-- 15769204  -->  
As a public preview, we’re adding support for Mobile Application Management (MAM) to the Microsoft Tunnel VPN gateway.  With this preview for Android devices that have not enrolled with Intune, supported apps will be able to use Microsoft Tunnel to connect to your organization when working with corporate data and resources. This includes VPN gateway support for:  

- Secure access to on-prem apps and resources using modern authentication
- Single Sign On and conditional access.

To use Tunnel for MAM on an unenrolled device will require the following three profiles:  

- An App configuration profile for managed apps, to configure Microsoft Defender on devices for use as the Tunnel client app 
- A second App configuration profile for managed apps, to configure Microsoft Edge to connect to Tunnel.
- An App protection profile to enable automatic start of the Microsoft Tunnel connection

For information about using Tunnel on enrolled devices, see [Microsoft Tunnel overview](../protect/microsoft-tunnel-overview.md)

Applies to:

- Android Enterprise


<!-- ***********************************************-->
## Monitor and troubleshoot

#### Review Cloud PC connectivity health checks and errors in Microsoft Endpoint Manager admin center<!-- 13811774  -->  
You’ll be able to review connectivity health checks and errors in the Microsoft Endpoint Manager admin center to help you understand if your users are experiencing connectivity issues. You’ll also get a troubleshooting tool to help resolve connectivity issues.

<!-- ***********************************************-->

## Tenant administration

### Deliver organizational messages for Windows 11 (public preview)<!-- 15314747 -->  

Deliver branded personalized messages to employees just above their taskbar, in their Notifications, or when they run the Get Started app on Windows 11 devices. Organizational messages are intended to improve employee communication in remote and hybrid-work scenarios, and to help employees adapt to their new roles more quickly, learn more about their organization, and stay informed of new updates and trainings.  

### Access policies for multiple administrative approvals (public preview)<!--9348867   -->
As a public preview, Intune *access policies* to require that a second administrative account be used to approve a change before the change is applied will soon be available to use. This capability is known as multiple administrative approval (MAA). Access policies will be available in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) at **Tenant administration** > **Multi Admin Administration** > **Access policies**.

Access policies can protect a type of resource, like App deployments. Each access policy will include a group of users who are *approvers* for the changes protected by the policy. When a resource like an app deployment configuration is protected by an access policy, any changes that are made to the deployment, including creating, deleting, or modifying an existing deployment won't apply until a member of the approvers group for that access policy reviews and approves that change.

Approvers will also be able to reject requests, and both the individual requesting a change and the approver can provide notes about the change, or why it was approved or rejected.

Access policies will be supported for the following resources:

- **Apps** – Applies to [app deployments](../apps/apps-add.md), but doesn't apply to app protection policies.
- **Scripts** – Applies to deploying scripts to devices that run [macOS](../apps/macos-shell-scripts.md) or [Windows](../apps/intune-management-extension.md).
<!-- ***********************************************-->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
