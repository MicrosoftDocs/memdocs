---
# required metadata

title: In development - Microsoft Intune
titleSuffix: 
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby 
ms.author: dougeby
manager: dougeby
ms.date: 05/03/2023
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

### View app report for Android Enterprise corporate-owned devices<!-- 2055436  -->  
You'll be able to view a report containing all apps found on a device for Android Enterprise corporate-owned scenarios, including system apps. This report will be available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Monitor** > **Discovered apps**. You will see **Application Name** and **Version** for all apps detected as installed on the device.

### Update to MAM reporting in Intune<!-- 10100428  -->  
MAM reporting will be simplified and overhauled to leverage Intune's newest reporting infrastructure. Benefits of these changes will include improved data accuracy and instantaneous updating. You will be able to find these streamlined MAM reports in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Monitor**. All MAM data available to you will be contained within the new **App protection status** report and **App configuration status** report.

### Assignment filters will support app protection policies and app configuration policies<!-- 7476247  -->  
Assignment filters will support MAM app protection policies and app configuration policies. When you create a new filter, you will be able to fine tune MAM policy targeting using the following properties:

- Device Management Type
- Device Manufacturer
- Device Model
- OS Version
- Application Version
- MAM Client Version

> [!IMPORTANT]
> All new and edited app protection policies that use **Device Type** targeting will be replaced with assignment filters.

For more information on filters, go to [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md).

### Install required apps during pre-provisioning<!-- 12716381   -->  
A new toggle will be available in the Enrollment Status Page (ESP) profile that allows you to select whether you want to attempt to install required applications during pre-provisioning (white glove) technician phase. We understand that installing as many applications as possible during pre-provisioning is desired to reduce the end user setup time. To help, we've implemented an option to attempt the installation of all the required apps assigned to a device during technician phase. If there's an app install failure, ESP will continue except for the apps specified in ESP profile. To enable this function, you'll need to edit your Enrollment Status Page profile by selecting **Yes** on the new setting entitled **Only fail selected apps in technician phase**. This setting will only appear if you have blocking apps selected. For information about ESP, go to [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).

### Company Portal automatically installed on Android Enterprise dedicated devices<!-- 6423852  -->  
Intune Company Portal will now be automatically installed on all Android Enterprise dedicated devices to ensure the appropriate handling of app protection policies. Users won't be able to see or launch the Company Portal, and there are no requirements for users to interact with it. Admins will notice that the Company Portal is automatically installed on their Android Enterprise dedicated devices, without the ability to uninstall.

### Uninstall Win32 apps in the Company Portal<!-- 5145748 -->  
*The time frame for the release of this update is still being determined.*

Users will be able to uninstall Win32 apps in the Company Portal. If a Win32 app can be uninstalled by the user, the user will be able to select **Uninstall** for the Win32 app in the Company Portal. For more information about Win32 apps, go to [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

### Global quiet time app policy settings<!-- 15424417 -->  
The global quiet time settings will allow you to create policies to schedule quiet time for your end users, which will automatically mute Microsoft Outlook email and Teams notifications on iOS/iPadOS and Android platforms. These policies can be used to limit end user notifications received after work hours. When this feature is available, you'll be able to find it in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Quiet Time** > **Policies**.

## Device configuration

### Visual Studio ADMX settings are in the Settings Catalog and Administrative Templates <!-- 10875730  -->  
Visual Studio settings are included in the Settings Catalog and Administrative Templates (ADMX). Previously, to configure Visual Studio settings on Windows devices, you imported them with ADMX import.

For more information on these policy types, go to:

- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)
- [Use Windows 10/11 templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md)
- [Visual Studio Administrative Templates (ADMX)](/visualstudio/install/administrative-templates)

Applies to:

- Windows 10/11

### Wipe device action and new obliteration behavior setting available for macOS<!-- 16647226  -->  
You'll soon be able to use the **Wipe** device action instead of Erase for macOS devices. Additionally, you'll be able to configure the **Obliteration Behavior** setting as part of the **Wipe** action.

This new key allows you to control the wipe fallback behavior on Macs that have Apple Silicon or the T2 Security Chip. To find this setting, navigate to **Devices** > **macOS** > [Select a device] > **Overview** > **Wipe** in the **Device action** area.

For more information on the Obliteration Behavior setting, go to Apple's Platform Deployment site [Erase Apple devices - Apple Support](https://support.apple.com/guide/deployment/erase-devices-dep0a819891e/web).

Applies to:

- macOS

#### Turn on/off Personal data encryption on Windows 11 devices using the settings catalog<!-- 10346018  -->  
The setting catalog includes hundreds of settings that you can configure and deploy to your devices.

In the settings catalog, you can turn on/off **Personal data encryption** (PDE). PDE is a security feature introduced in Windows 11 version 22H2 that provides more encryption features for Windows.

It's different than BitLocker. PDE encrypts individual files and content, instead of whole volumes and disks. You can use PDE with other encryption methods, such as BitLocker.

For more information on the settings catalog, go to:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md)
- [Common Tasks you can complete using the Settings Catalog in Intune](../configuration/settings-catalog-common-features.md)

This feature applies to:

- Windows 11

#### Group policy analytics supports scope tags<!-- 12714882  -->  
In Group Policy analytics, you import your on-premises GPO. The tool analyzes your GPOs and shows the settings that can (and can't) be used in Intune. 

When you import your GPO XML file in Intune, you can also select an existing scope tag. Only admins within that scope tag can see the imported policies. Admins not in that scope tag can't see the imported policies.

Also, admins within their scope tag can migrate the imported policies that they have permissions to see. To migrate an imported GPO into a Settings Catalog policy, a scope tag must be associated with the imported GPO. If a scope tag isn't associated, then it can't migrate to a Settings Catalog policy. If no scope tag is selected, then a default scope tag is automatically applied.

For more information on scope tags and Group Policy analytics, go to:

- [Use role-based access control (RBAC) and scope tags for distributed IT](scope-tags.md)
- [Analyze your on-premises GPOs using Group Policy analytics in Microsoft Intune](../configuration/group-policy-analytics.md)

#### New settings available in the macOS settings catalog <!-- 18430228  -->  
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Settings catalog** for profile type.

**Microsoft Defender > Antivirus engine**:

- Scanning inside archive files
- Enable file hash computation

Applies to:  

- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Remote Help administrators will be able to reference audit log sessions<!-- 9052185   -->  
For Remote Help, in addition to existing session reports, administrators can now reference audit logs sessions created in Intune. This enables administrators to reference past events for troubleshooting and analyzing log activities.

For more information on Remote Help, go to [Remote Help](../fundamentals/remote-help.md).

Applies to:

- Windows 10/11

### Introducing Intune integration with the Zebra Lifeguard Over-the-Air service (public preview)<!-- 14340034  -->
Intune will be adding integration with Zebra Lifeguard Over-the-Air service, which allows you to deliver OS updates and security patches over-the-air to eligible Zebra devices that are enrolled with Intune. You can select the firmware version you want to deploy, set a schedule, and stagger update downloads and installs. You can also set minimum battery, charging status, and network conditions requirements for when the update can happen.

Available for Android Enterprise Zebra devices that are running Android 8 or later, and requires an account with Zebra.

### Renaming Proactive remediation to Remediations and moving to a new location<!-- 16526263  -->  
Going forward Proactive remediations will be known as Remediations and will be available from Devices > Remediations. You will still be able to find Remediations in both the new location and the existing Reports > Endpoint Analytics location until the next Intune service update. Remediations are not currently available in the new [Devices experience preview](../fundamentals/microsoft-intune-admin-center-devices.md).

Remediations will now use the [Windows license verification](../protect/data-enable-windows-data.md#windows-license-verification) category in Tenant administration > Connectors and tokens > Windows data to verify that you own the Windows E3 or equivalent licenses required to use the feature. Customers who previously verified licensing for Remediations prior to this change will automatically be migrated to this category.

#### Create inbound and outbound network traffic rules for VPN profiles on Windows devices<!-- 17943658  -->  
You can create a device configuration profile that deploys a VPN connection to devices (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Templates** > **VPN** for profile type).

In this VPN connection, you can use the **Apps and Traffic rules** settings to create network traffic rules.

There's a new **Direction** setting you can configure. Use this setting to allow Inbound and Outbound traffic from the VPN connection:

- **Outbound** (default): Allows only traffic to external networks/destinations to flow using the VPN. Inbound traffic is blocked from entering the VPN.
- **Inbound**: Allows only traffic coming from external networks/ sources to flow using the VPN. Outbound traffic is blocked from entering the VPN.

For more information on the VPN settings you can configure, including the network traffic rule settings, go to [Windows device settings to add VPN connections using Intune](../configuration/vpn-settings-windows-10.md).

Applies to:

- Windows 10 and later

### New Google domain allow-list settings for Android Enterprise personally owned devices with a work profile<!-- 14711684 -->

On Android Enterprise personally owned devices with a work profile, you can configure settings that restrict device features and settings.

Currently, there's an **Add and remove accounts** setting that can allow Google accounts be added to the work profile. For this setting, when you select **Allow all accounts types**, you can also configure:

- **Google domain allow-list**:  Restricts users to add only certain Google account domains in the work profile. You can import a list of allowed domains or add them in the admin center using the `contoso.com` format. When left blank, by default, the OS might allow adding all Google domains in the work profile.

For more information on the settings you can configure, go to [Android Enterprise device settings list to allow or restrict features on personally owned devices using Intune](../configuration/device-restrictions-android-enterprise-personal.md).

Applies to:


- Android Enterprise personally owned devices with a work profile

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

## Device enrollment

### Apple Account Driven User Enrollment available for iOS/iPadOS 15+ devices<!-- 14161683  -->  
Intune will support Apple Account Driven User Enrollment, a new and improved variation of Apple User Enrollment for iOS/iPadOS 15+ devices. The new option will utilize just-in-time-registration, which eliminates the need for the Company Portal app during enrollment. Device users can initiate enrollment directly in the Settings app, resulting in a shorter and more efficient onboarding experience. You can continue to target iOS/iPadOS devices using the existing profile-based User Enrollment method with Company Portal. Devices running iOS/iPadOS, version 14.8.1 and earlier will be unaffected by this update and can also continue to use the existing method.

<!-- *********************************************** -->

## Device management

### On-demand proactive remediation for a Windows device<!-- 14783338  -->  
A new device action that is in public preview allows you to run a proactive remediation on-demand to a single Windows device. The **Run** remediation device action will allow you to resolve issues without having to wait for a proactive remediation to run on its assigned schedule. You'll also be able to view the status of proactive remediations under **Remediations** in the **Monitor** section of a device.

<!-- *********************************************** -->

## Device security

### Security baseline update for Microsoft Edge version 107<!-- 3408610  -->  
We’re working on an update for the Intune security baseline for Microsoft Edge version 107. In addition to releasing this new version for Microsoft Edge, the new baseline uses an updated template experience that leverages the unified settings platform seen in the Intune settings catalog.

The new Intune security baseline format aligns the presentation of settings that are available to those found in the Intune settings catalog. This alignment helps resolve past issues for setting names and implementations for settings that could create conflicts. The new format also improves the reporting experience for baselines in the Intune admin center.

Once the new baseline version is available, all new profiles you create for Microsoft Edge will use the new baseline format and version. While the new version becomes the default baseline version, you’ll still be able to use the profiles you’ve previously created for older versions of Microsoft Edge, but not create new profiles for those older versions of Microsoft Edge.

To learn more, see [Security baselines overview](../protect/security-baselines.md).

### New security baseline for Microsoft 356 Office Apps<!-- 9587103 -->  
We’re working to add a new security baseline to help you manage security configurations for **M365 Office Apps**. This new baseline will be released in a new format for security baselines that uses an updated template and experience that leverages the unified settings platform seen in the Intune settings catalog.

The new Intune security baseline format aligns the presentation of settings that are available to those found in the Intune settings catalog. This alignment helps resolve past issues for setting names and implementations for settings that could create conflicts. The new format also improves the reporting experience for baselines in the Intune admin center.

The M365 Office Apps baseline can help you rapidly deploy configurations to your Office Apps that meet the security recommendations of the Office and security teams at Microsoft. As with all baselines, the default baseline represents the recommended configurations and you’ll be free to modify the default baseline to meet the requirements of your organization.

To learn more, see [Security baselines overview](../protect/security-baselines.md).


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
