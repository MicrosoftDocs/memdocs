---
# required metadata
title: What's new in Microsoft Intune
titleSuffix:
description: Find out what's new in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/27/2025
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- tier2
- M365-identity-device-management
- highseo
---

# What's new in Microsoft Intune

Learn what's new each week in Microsoft Intune.

You can also read:

- [**Important notices**](#notices)
- [Past releases](whats-new-archive.md) in the What's new archive
- Information about [how Intune service updates are released](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728)

> [!NOTE]
> Each [monthly update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) can take up to three days to roll out and will be in the following order:
>
> - Day 1: Asia Pacific (APAC)
> - Day 2: Europe, Middle East, Africa (EMEA)
> - Day 3: North America
> - Day 4+: Intune for Government
>
> Some features roll out over several weeks and might not be available to all customers in the first week.
>
> For a list of upcoming Intune feature releases, see [In development for Microsoft Intune](../fundamentals/in-development.md).
>
> For new information about Windows Autopilot solutions, see:
>
> - [Windows Autopilot device preparation: What's new](/autopilot/device-preparation/whats-new)
> - [Windows Autopilot: What's new](/autopilot/whats-new)

You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Get notified when this page is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us` -->

<!-- Common categories - in this order:

### Microsoft Intune Suite
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
### Scripts
### Tenant administration

-->

## Week of February 24, 2025  (Service release 2502)

### App management

#### VPP token name more easily available in Apps workload<!-- 5479088 -->

The **VPP token name** column, available in the Apps workload, allows you to quickly determine the token and app association. This column is now available in the **All apps** list (**Apps** > **All apps**) and the app selection pane for **App configuration policies** (**Apps** > **App configuration policies**). For more information about VPP apps, see [Manage volume-purchased apps and books with Microsoft Intune](../apps/vpp-apps.md).

Applies to:

- iOS/iPadOS
- macOS

### Device configuration

#### New Windows AI settings available in the Windows settings catalog<!-- 30339749 -->
 
The Settings Catalog lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog for Windows. To see these settings, in the Microsoft Intune admin center, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** > **Settings catalog** for profile type.

The new settings are:

- Disable AI Data Analysis
- Set Deny Uri List For Recall
- Set Deny App List For Recall
- Set Maximum Storage Space For Recall Snapshots
- Set Maximum Storage Duration For Recall Snapshots

Applies to:

- Windows

#### New Default Enforcement device control setting available in the Windows settings catalog<!-- 30253799 -->

The Settings Catalog lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog for Windows 24H2. To see these settings, in the Microsoft Intune admin center, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** > **Settings catalog** for profile type.

This setting is available in both the settings catalog and the ASR device control template. The Default Enforcement device control setting enables a default enforcement to be applied if:

- There are no policy rules present, or
- At the end of the policy rules evaluation none were matched.

Applies to:

- Windows

### Intune apps

#### Newly available protected app for Intune<!-- 30508606 -->

The following protected app is now available for Microsoft Intune:

- Applications Manager - Intune by ManageEngine

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of February 17, 2025

### Monitor and troubleshoot

#### Limited live chat support in Intune<!-- 30477421 -->

Intune is introducing limited live chat support within the Intune admin console. Live chat will not be available for all tenants or inquiries at this time.

## Week of February 10, 2025

### Device security

#### Updated security baseline for Windows version 24H2<!-- 29819143 -->

You can now deploy the Intune security baseline for **Windows version 24H2** to your Windows 10 and Windows 11 devices. The new baseline version uses the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline represents the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows

### Monitor and troubleshoot

#### Device Query for Multiple Devices<!--25234456 -->

We've added Device query for multiple devices. This feature allows you to gain comprehensive insights about your entire fleet of devices using Kusto Query Language (KQL) to query across collected inventory data for your devices.

Device query for multiple devices is now supported for devices running Windows 10 or later. This feature is now included as part of Advanced Analytics.

Applies to:

- Windows

## Week of February 5, 2025  (Service release 2501)

### Microsoft Intune Suite
 
#### Use Microsoft Security Copilot with Endpoint Privilege Manager to help identify potential elevation risks<!-- 27265509 -->

When your Azure Tenant is licensed for Microsoft Security Copilot, you can now use Security Copilot to help you investigate Endpoint Privilege Manager (EPM) file elevation requests from within the EPM [support approved](../protect/epm-support-approved.md#use-microsoft-security-copilot-to-analyze-file-elevation-requests) work flow.

With this capability, while reviewing the properties of a file elevation request, you'll now find option to **Analyze with Copilot**. Use of this option directs Security Copilot to use the files hash in a prompt Microsoft Defender Threat Intelligence to evaluate the file potential indicators of compromise so you can then make a more informed decision to either approve or deny that file elevation request. Some of the results that are returned to your current view in the admin center include:

- The files’ reputation
- Information about the trust of the publisher
- The risk score for the user requesting the file elevation
- The risk score of the device from which the elevation was submitted

EPM is available as an [Intune Suite add-on-capability](../fundamentals/intune-add-ons.md). To learn more about how you can currently use Copilot in Intune, see [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md).

To learn more about Microsoft Security Copilot, see, [Microsoft Security Copilot](/copilot/security/microsoft-security-copilot).

### App management

#### Update to Apps workload experience in Intune<!-- 15507048 -->

The Apps area in Intune, commonly known as the Apps workload, is updated to provide a more consistent UI and improved navigation structure so you can find the information you need faster. To find the **App** workload in Intune, navigate to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Apps**.

### Device configuration

#### New settings available in the Windows settings catalog to Configure multiple display mode<!-- 30305854 -->

The Settings Catalog lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog to *Configure Multiple Display Mode* for
Windows 24H2. To see available settings, in the Microsoft Intune admin center, go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later for platform** > **Settings catalog** for profile type.

The **Configure Multiple Display Mode** setting allows monitors to extend or clone the display by default, facilitating the need for manual setup. It streamlines the multi-monitor configuration process, ensuring a consistent and user-friendly experience.

Applies to:

- Windows

### Device security

#### Updated security baseline for Microsoft Edge v128<!-- 29463902 -->

You can now deploy the Intune security baseline for **Microsoft Edge version 128**. This update brings support for recent settings so you can continue to maintain best-practice configurations for Microsoft Edge.

[View the default configuration of settings in the updated baseline](../protect/security-baseline-v2-edge-settings.md?pivots=edge-v128).

For information about security baselines with Intune, see [Use security baselines to configure Windows devices in Intune](../protect/security-baselines.md).

Applies to:
 
- Windows

### Intune apps

#### Newly available protected app for Intune<!-- 30061339 -->

The following protected app is now available for Microsoft Intune:

- MoveInSync by MoveInSync Technologies

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of January 27, 2025

### Device security

#### Security baselines for HoloLens 2<!-- 24914095 -->

You can now deploy two distinct instances of the security baseline for HoloLens 2. These baselines represent Microsoft’s best practice guidelines and experience from deploying and supporting HoloLens 2 devices to customers across various industries. The two baselines instances:

- **Standard Security Baseline for HoloLens 2**:  
  The standard security baseline for HoloLens 2 represents the recommendations for configuring security settings that are applicable to all types of customers irrespective of HoloLens 2 use case scenarios. [View the default configuration of settings in the standard security baseline](../protect/security-baseline-hololens2-standard.md).

- **Advanced Security Baseline for HoloLens 2**:  
  The advanced security baseline for HoloLens 2 represents the recommendations for configuring security settings for the customers who have strict security controls of their environment and require stringent security policies to be applied to any device used in their environment. [View the default configuration of settings in the advanced security baseline](../protect/security-baseline-hololens2-advanced.md).

To learn more about security baselines with Intune, see [Use security baselines to configure Windows devices in Intune](../protect/security-baselines.md).

Applies to:

- Windows

## Week of January 20, 2025

### Monitor and troubleshoot

#### Use Support Assistant to resolve issues<!-- 29084113 -->

Support Assistant is now available in Intune. It leverages AI to enhance your help and support experience, ensuring more efficient issue resolution. Support Assistant is available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshoot + support** > **Help and Support**, or by selecting the question mark near your profile pic. Currently, the Support Assistant is in preview. You can enable and disable Support Assistant by choosing to opt in and opt out at any time. For related information, see [How to get support in the Microsoft Intune admin center](/mem/get-support).

## Week of December 30, 2024

### Device enrollment

#### Intune ends support for Android device administrator on devices with access to Google Mobile Services<!-- 24563742 -->
As of December 31, 2024, Microsoft Intune no longer supports Android device administrator management on devices with access to Google Mobile Services (GMS). This change comes after Google deprecated Android device administrator management and ceased support. Intune support and help documentation remains for devices without access to GMS running Android 15 or earlier, and Microsoft Teams devices migrating to Android Open Source Project (AOSP) management. For more information about how this change impacts your tenant, see [Intune ending support for Android device administrator on devices with GMS access in December 2024](https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-ending-support-for-android-device-administrator-on-devices-with-gms-in-de/3915443). 


## Week of December 16, 2024 (Service release 2412)

### App management

#### Increased scale for Customization policies<!-- 25308499 -->

You can now create up to 25 policies that customize the Company Portal and Intune app experience. The previous maximum number of Customization policies was 10. Navigate to the Intune admin center, and select **Tenant administration** > **Customization**.

For more information about customizing the Company Portal and Intune apps, see [Customizing the user experience](../apps/company-portal-app.md#customizing-the-user-experience).

### Device security

#### Support for tamper protection in policies for Security settings management for Microsoft Defender for Endpoint<!-- 13204113 -->
 
> [!NOTE]
>
> *Rollout of this feature is delayed and now expected to be available in May 2025.*

You can now manage the Microsoft Defender for Endpoint CSP setting for [tamper protection](/windows/client-management/mdm/defender-csp) on unenrolled devices you manage as part of the [Defender for Endpoint security settings management](../protect/mde-security-integration.md#which-solution-should-i-use) scenario.
 
With this support, tamper protection configurations from *Windows Security Experience* profiles for *Antivirus* policies now apply to all devices instead of only to those that are enrolled with Intune.

### Device configuration

#### Ending support for administrative templates when creating a new configuration profile<!-- 29989512 -->

Customers cannot create new Administrative Templates configuration profile through **Devices > Configuration > Create > New policy > Windows 10 and later > Administrative Templates**. A (retired) tag is seen next to **Administrative Templates** and the **Create** button is now greyed out. Other templates will continue to be supported.

However, customers can now use the Settings Catalog for creating new **Administrative Templates** configuration profile by navigating to **Devices > Configuration > Create > New policy > Windows 10 and later > Settings Catalog**.

There are no changes in the following UI experiences: 

- Editing an existing Administrative template.
- Deleting an existing Administrative template.
- Adding, modifying, or deleting settings in an existing Administrative template.
- **Imported Administrative templates (Preview)** template, which is used for Custom ADMX.

For more information, see [Use ADMX templates on Windows 10/11 devices in Microsoft Intune](..\configuration\administrative-templates-windows.md).

Applies to:

- Windows

### Device management

#### More Wi-Fi configurations are now available for personally-owned work profile devices<!-- 28331156 -->

Intune Wi-Fi configuration profiles for Android Enterprise personally-owned work profile devices now support configuration of pre-shared keys and proxy settings. 

You can find these settings in the admin console in **Devices** > **Manage devices** > **Configuration** > **Create** > **New Policy**. Set **Platform** to Android Enterprise and then in the **Personally-Owned Work Profile** section, select Wi-Fi and then select the **Create** button. 

In the **Configuration settings** tab, when you select Basic Wi-Fi type, several new options are available:

1. Security type, with options for Open (no authentication), WEP-Pre-shared key, and WPA-Pre-shared key.

2. Proxy settings, with the option to select Automatic and then specify the proxy server URL.

It was possible to configure these in the past with Custom Configuration policies, but going forward, we recommend setting these in the Wi-Fi Configuration profile, because [Intune is ending support for Custom policies in April 2024.](https://aka.ms/Intune/Android-customprofiles).

For more information, see [Wi-Fi settings for personally-owned work profile devices.](../configuration/wi-fi-settings-android-enterprise.md#personally-owned-work-profile).

Applies to:

- Android Enterprise

## Week of December 9, 2024

### Tenant administration

#### Intune now supports Ubuntu 24.04 LTS for Linux management.<!--28363586 -->

We're now supporting device management for Ubuntu 24.04 LTS. You can enroll and manage Linux devices running Ubuntu 24.04, and assign standard compliance policies, custom configuration scripts, and compliance scripts.

For more information, see the following in Intune documentation:

- [Deployment guide: Manage Linux devices in Microsoft Intune](../fundamentals/deployment-guide-platform-linux.md)
- [Enrollment guide: Enroll Linux desktop devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-linux.md). To enroll Linux devices, ensure that they're running Ubuntu 20.04 LTS or higher.

Applies to:

- Linux Ubuntu Desktops

## Week of December 2, 2024

### Device enrollment

#### Change to enrollment behavior for iOS enrollment profile type<!-- 29068674 -->

At Apple WWDC 2024, Apple ended support for profile-based Apple user enrollment. For more information, see [Support has ended for profile-based user enrollment with Company Portal](#support-has-ended-for-apple-profile-based-user-enrollment-with-company-portal). As a result of this change, we updated the behavior that occurs when you select **Determine based on user choice** as the enrollment profile type for bring-your-own-device (BYOD) enrollments.

Now when users select **I own this device** during a BYOD enrollment, Microsoft Intune enrolls them via account-driven user enrollment, rather than profile-based user enrollment, and then secures only work-related apps. Less than one percent of Apple devices across all Intune tenants are currently enrolled this way, so this change doesn't affect most enrolled devices. There is no change for iOS users who select **My company owns this device** during a BYOD enrollment. Intune enrolls them via device enrollment with Intune Company Portal, and then secures their entire device.

If you currently allow users in BYOD scenarios to determine their enrollment profile type, you must take action to ensure account-driven user enrollment works by completing all prerequisites. For more information, see [Set up account driven Apple user enrollment](../enrollment/apple-account-driven-user-enrollment.md). If you don't give users the option to choose their enrollment profile type, there are no action items.

### Device management

#### Device Inventory for Windows<!-- 24853010 -->

Device inventory lets you collect and view additional hardware properties from your managed devices to help you better understand the state of your devices and make business decisions.

You can now choose what you want to collect from your devices, using the catalog of properties and then view the collected properties in the Resource Explorer view.

For more information, see:

- [Properties catalog](../configuration/properties-catalog.md)
- [Data collection platform](../../analytics/data-platform-schema.md)

Applies to:

- Windows 10 and later (Corporate owned devices managed by Intune)

## Week of November 18, 2024 (Service release 2411)

### App management

#### Configuration values for specific managed applications on Intune enrolled iOS devices<!-- 30293382 -->

Starting with Intune's September (2409) service release, the **IntuneMAMUPN**, **IntuneMAMOID**, and **IntuneMAMDeviceID** app configuration values are automatically sent to managed applications on Intune enrolled iOS devices for the following apps:

- Microsoft Excel
- Microsoft Outlook
- Microsoft PowerPoint
- Microsoft Teams
- Microsoft Word

For more information, see [Plan for Change: Specific app configuration values will be automatically sent to specific apps](../fundamentals/whats-new.md#plan-for-change-specific-app-configuration-values-will-be-automatically-sent-to-specific-apps) and Intune [Support tip: Intune MAM users on iOS/iPadOS userless devices may be blocked in rare cases](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-intune-mam-users-on-iosipados-userless-devices-may-be-blocked-in-rar/4254335).

#### Additional installation error reporting for LOB apps on AOSP devices<!-- 27157460 -->

Additional details are now provided for app installation reporting of Line of Business (LOB) apps on Android Open Source Project (AOSP) devices. You can view installation error codes and detailed error messages for LOB apps in Intune.

For information about app installation error details, see [Monitor app information and assignments with Microsoft Intune](../apps/apps-monitor.md#app-installation-error-reporting).

Applies to:

- Android Open Source Project (AOSP) devices

#### Microsoft Teams app protection on VisionOS devices (preview)<!-- 29913431 -->

Microsoft Intune app protection policies (APP) are now supported on the Microsoft Teams app on VisionOS devices. 

To learn more about how to target policies to VisionOS devices, see [Managed app properties](../fundamentals/filters-device-properties.md#managed-app-properties) for more information about filters for managed app properties.

Applies to:

- Microsoft Teams for iOS on VisionOS devices

## Week of October 28, 2024

### Device security

#### Defender for Endpoint security settings support in government cloud environments (generally available)<!-- 30064299 -->

Now generally available, customer tenants in the Government Community Cloud (GCC), US Government Community High (GCC High), and Department of Defense (DoD) environments can use Intune to manage the Defender security settings on the devices you’ve onboarded to Defender without enrolling those devices with Intune. Previously, support for Defender security settings was in public preview.

This capability is known as [Defender for Endpoint security settings management](../protect/mde-security-integration.md).

## Week of October 14, 2024 (Service release 2410)

### App management

#### Updates to app configuration policies for Android Enterprise devices<!-- 26711672 -->

App configuration policies for Android Enterprise devices now support overriding the following permissions:

- Access background location
- Bluetooth (connect)

For more information about app configuration policies for Android Enterprise devices, see [Add app configuration policies for managed Android Enterprise devices](../apps/app-configuration-policies-use-android.md).

Applies to:

- Android Enterprise devices

### Device configuration

#### Windows Autopilot device preparation support in Intune operated by 21Vianet in China<!-- MAXADO-9313795 / INADO-28687730 -->

Intune now supports *Windows Autopilot device preparation* policy for [Intune operated by 21Vianet in China](../fundamentals/china.md) cloud. Customers with tenants located in China can now use *Windows Autopilot device preparation* with Intune to provision devices.

For information about this Autopilot support, see the following in the Autopilot documentation:

- Overview: [Overview of Windows Autopilot device preparation](/autopilot/device-preparation/overview)
- Tutorial: [Windows Autopilot device preparation scenarios](/autopilot/device-preparation/tutorial/scenarios)

### Device management

#### Minimum OS version for Android devices is Android 10 and later for user-based management methods<!-- 14755802 -->

Beginning in October 2024, Android 10 and later is the [minimum Android OS version that is supported for user-based management methods](../fundamentals/supported-devices-browsers.md#android), which includes:

- Android Enterprise personally-owned work profile
- Android Enterprise corporate owned work profile
- Android Enterprise fully managed
- Android Open Source Project (AOSP) user-based
- Android device administrator
- App protection policies (APP)
- App configuration policies (ACP) for managed apps

For enrolled devices on unsupported OS versions (Android 9 and lower)

- Intune technical support isn't provided.
- Intune won't make changes to address bugs or issues.
- New and existing features aren't guaranteed to work.

While Intune doesn't prevent enrollment or management of devices on unsupported Android OS versions, functionality isn't guaranteed, and use isn't recommended.

Userless methods of Android device management (Dedicated and AOSP userless) and Microsoft Teams certified Android devices aren't affected by this change.

#### Collection of additional device inventory details<!-- 29460196 -->

Intune now collects additional files and registry keys to assist in troubleshooting the [Device Hardware Inventory](../remote-actions/collect-diagnostics.md) feature.

Applies to:

- Windows

## Week of October 7, 2024

### App management

#### New UI for Intune Company Portal app for Windows<!-- 27219294 -->

The UI for the Intune Company Portal app for Windows is updated. Users now see an improved experience for their desktop app without changing the functionality they've used in the past. Specific UI improvements are focused on the **Home**, **Devices**, and **Downloads & updates** pages. The new design is more intuitive and highlights areas where users need to take action.

For more information, see [New look for Intune Company Portal app for Windows](https://techcommunity.microsoft.com/t5/intune-customer-success/new-look-for-intune-company-portal-app-for-windows/ba-p/4158755). For end user details, see [Install and share apps on your device](../user-help/install-apps-cpapp-windows.md).

### Device security

#### New strong mapping requirements for SCEP certificates authenticating with KDC<!-- 29005591 -->

The Key Distribution Center (KDC) requires user or device objects to be strongly mapped to Active Directory for certificate-based authentication. This means that a Simple Certificate Enrollment Protocol (SCEP) certificate's subject alternative name (SAN) must have a security identifier (SID) extension that maps to the user or device SID in Active Directory. The mapping requirement protects against certificate spoofing and ensures that certificate-based authentication against the KDC continues working.

To meet requirements, modify or create a SCEP certificate profile in Microsoft Intune. Then add a `URI` attribute and the `OnPremisesSecurityIdentifier` variable to the SAN. After you do that, Microsoft Intune appends a tag with the SID extension to the SAN and issues new certificates to targeted users and devices. If the user or device has a SID on premises that's synced to Microsoft Entra ID, the certificate shows the SID. If they don't have a SID, a new certificate is issued without the SID.

For more information and steps, see [Update certificate connector: Strong mapping requirements for KB5014754](../protect/certificates-profile-scep.md).

Applies to:

- Windows 10/11, iOS/iPadOS, and macOS user certificates
- Windows 10/11 device certificates

This requirement isn't applicable to device certificates used with Microsoft Entra joined users or devices, because the SID attribute is an on-premises identifier.

#### Defender for Endpoint security settings support in government cloud environments (public preview)<!-- 24191406 -->

In public preview, customer tenants in US Government Community (GCC) High, and Department of Defense (DoD) environments can now use Intune to manage the Defender security settings on the devices that onboarded to Defender without enrolling those devices with Intune. This capability is known as [Defender for Endpoint security settings management](../protect/mde-security-integration.md).

For more information about the Intune features supported in GCC High and DoD environments, see [Intune US Government service description](../fundamentals/intune-govt-service-description.md).

## Week of September 30, 2024

### Device security

#### Updates to PKCS certificate issuance process in Microsoft Intune Certificate Connector, version 6.2406.0.1001 <!-- 24186560 -->

We updated the process for Public Key Cryptography Standards (PKCS) certificate issuance in Microsoft Intune to support the security identifiers (SID) information requirements described in [KB5014754](https://support.microsoft.com/topic/kb5014754-certificate-based-authentication-changes-on-windows-domain-controllers-ad2c23b0-15d8-4340-a468-4d4f3b188f16). As part of this update, an OID attribute containing the user or device SID is added to the certificate. This change is available with the Certificate Connector for Microsoft Intune, version 6.2406.0.1001, and applies to users and devices synced from Active Directory on-premises to Microsoft Entra ID.

The SID update is available for user certificates across all platforms, and for device certificates specifically on Microsoft Entra hybrid joined Windows devices.

For more information, see:

- [What's new for the certificate connector](../protect/certificate-connector-overview.md#september-19-2024)

- [Apply PFX changes to certificate](../protect/certificates-pfx-configure.md)

## Week of September 23, 2024 (Service release 2409)

### App management

#### Working Time settings for app protection policies<!-- 14631539 -->

Working time settings allow you to enforce policies that limit access to apps and mute message notifications received from apps during non-working time. The limit access setting is now available for the Microsoft Teams and Microsoft Edge apps. You can limit access by using App Protection Policies (APP) to block or warn end users from using the iOS/iPadOS or Android Teams and Microsoft Edge apps during non-working time by setting the **Non-working time** conditional launch setting. Also, you can create a non-working time policy to mute notifications from the Teams app to end users during non-working time.

For more information, see:

- [Android app protection policy settings](../apps/app-protection-policy-settings-android.md#conditional-launch)
- [iOS app protection policy settings](../apps/app-protection-policy-settings-ios.md#conditional-launch)
- [Quiet time policies for iOS/iPadOS and Android apps](../apps/apps-quiet-time-policies.md#quiet-time-policy-types)

Applies to:

- Android
- iOS/iPadOS

#### Streamlined app creation experience for apps from Enterprise App Catalog<!-- 29411991 -->

We've streamlined the way apps from [Enterprise App Catalog](../apps/apps-add-enterprise-app.md) are added to Intune. We now provide a direct app link rather than duplicating the app binaries and metadata. App contents now download from a `*.manage.microsoft.com` subdomain. This update helps to improve the latency when adding an app to Intune. When you add an app from Enterprise App Catalog, it syncs immediately and is ready for additional action from within Intune.

#### Update Enterprise App Catalog apps<!-- 24875279 -->

Enterprise App Management is enhanced to allow you to update an **Enterprise App Catalog** app. This capability guides you through a wizard that allows you to add a new application and use supersedence to update the previous application.

For more information, see [Guided update supersedence for Enterprise App Management](../apps/apps-eam-supersedence.md).

### Device configuration

#### Samsung ended support for multiple Android device administrator (DA) settings <!-- 24990472 -->

On Android device administrator managed (DA) devices, Samsung has deprecated many [Samsung Knox APIs](https://docs.samsungknox.com/dev/knox-sdk/api-reference/deprecated-api-methods/) (opens Samsung's web site) configuration settings.

In Intune, this deprecation impacts the following device restrictions settings, compliance settings, and trusted certificate profiles:

- [Device restriction settings for Android in Microsoft Intune](../configuration/device-restrictions-android.md)
- [View the Android device administrator compliance settings for Microsoft Intune compliance policies](../protect/compliance-policy-create-android.md)
- [Create trusted certificate profiles in Microsoft Intune](../protect/certificates-trusted-root.md#trusted-certificate-profiles-for-android-device-administrator)

In the Intune admin center, when you create or update a profile with these settings, the impacted settings are noted.

Though the functionality might continue to work, there's no guarantee that it will continue working for any or all Android DA versions supported by Intune. For more information on Samsung support for deprecated APIs, see [What kind of support is offered after an API is deprecated?](https://docs.samsungknox.com/dev/knox-sdk/faqs/general/deprecated-api-support-change.htm) (opens Samsung's web site).

Instead, you can manage Android devices with Intune using one of the following Android Enterprise options:

- [Set up enrollment of Android Enterprise personally owned work profile devices](../enrollment/android-work-profile-enroll.md)
- [Set up Intune enrollment of Android Enterprise corporate-owned devices with work profile](../enrollment/android-corporate-owned-work-profile-enroll.md)
- [Set up enrollment for Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md)
- [Set up Intune enrollment of Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md)
- [App protection policies overview](../apps/app-protection-policy.md)

Applies to:

- Android device administrator (DA)

#### Device Firmware Configuration Interface (DFCI) supports VAIO devices <!-- 28186944 -->

For Windows 10/11 devices, you can create a DFCI profile to manage UEFI (BIOS) settings. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type.

Some VAIO devices running Windows 10/11 are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

For more information about DFCI profiles, see:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](../../autopilot/dfci-management.md)

Applies to:

- Windows 10
- Windows 11

#### New settings available in the Apple settings catalog <!-- 28672633 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Declarative Device Management (DDM) > Math Settings**:

- Calculator
  - Basic Mode
  - Math Notes Mode
  - Scientific Mode

- System Behavior
  - Keyboard Suggestions
  - Math Notes

**Web Content Filter**:

- Hide Deny List URLs

##### macOS

**Declarative Device Management (DDM) > Math Settings**:

- Calculator
  - Basic Mode
  - Math Notes Mode
  - Programmer Mode
  - Scientific Mode

- System Behavior
  - Keyboard Suggestions
  - Math Notes

**System Configuration > System Extensions**:

- Non Removable From UI System Extensions
- Non Removable System Extensions

#### Consent prompt update for remote log collection<!-- 28072852 -->

End users might see a different consent experience for remote log collection after the Android APP SDK 10.4.0 and iOS APP SDK 19.6.0 updates. End users no longer see a common prompt from Intune and only see a prompt from the application, if it has one.

Adoption of this change is per-application and is subject to each applications release schedule.

Applies to:

- Android
- iOS/iPadOS

### Device enrollment

#### New Setup Assistant screens available for configuration for ADE <!-- 26607203, 2532989 -->

New Setup Assistant screens are available to configure in the Microsoft Intune admin center. You can hide or show these screens during automated device enrollment (ADE).

For macOS:

- **Wallpaper**: Show or hide the macOS Sonoma wallpaper setup pane that appears after an upgrade on devices running macOS 14.1 and later.
- **Lockdown mode**: Show or hide the lockdown mode setup pane on devices running macOS 14.1 and later.
- **Intelligence**: Show or hide the Apple Intelligence setup pane on devices running macOS 15 and later.

For iOS/iPadOS:

- **Emergency SOS**: Show or hide the safety setup pane on devices running iOS/iPadOS 16 and later.
- **Action button**: Show or hide the setup pane for the action button on devices running iOS/iPadOS 17 and later.
- **Intelligence**: Show or hide the Apple Intelligence setup pane on devices running iOS/iPadOS 18 and later.

You can configure these screens in new and existing enrollment policies. For more information and additional resources, see:

- [Set up Apple automated device enrollment for iOS/iPadOS](../enrollment/device-enrollment-program-enroll-ios.md)
- [Set up Apple automated device enrollment for Macs](../enrollment/device-enrollment-program-enroll-macos.md)

#### Extended expiration date for corporate-owned, user-associated AOSP enrollment tokens<!-- 25782149 -->

Now when you create an enrollment token for Android Open Source Project (AOSP) corporate-owned, user-associated devices, you can select an expiration date that's up to 65 years into the future, an improvement over the previous 90 day expiration date. You can also modify the expiration date of existing enrollment tokens for Android Open Source Project (AOSP) corporate-owned, user-associated devices.

### Device security

#### New disk encryption template for Personal Data Encryption<!-- 28677934 -->

You can now use the new *Personal Data Encryption* (PDE) template that is available through endpoint security [*disk encryption* policy](../protect/encrypt-devices.md). This new template configures the Windows [PDE configuration service provider](/windows/client-management/mdm/personaldataencryption-csp) (CSP), which was introduced in Windows 11 22H2. The PDE CSP is also available through the settings catalog.

PDE differs from BitLocker in that it encrypts files instead of whole volumes and disks. PDE occurs in addition to other encryption methods such as BitLocker. Unlike BitLocker that releases data encryption keys at boot, PDE doesn't release data encryption keys until a user signs in using Windows Hello for Business.

Applies to:

- Windows 11 version 22h2 or later

For more information about PDE, including prerequisites, related requirements, and recommendations, see the following articles in the Windows security documentation:

- [PDE overview](/windows/security/operating-system-security/data-protection/personal-data-encryption/)
- [Configure PDE](/windows/security/operating-system-security/data-protection/personal-data-encryption/configure)
- [PDE frequently asked questions (FAQ)](/windows/security/operating-system-security/data-protection/personal-data-encryption/faq)

### Intune Apps

#### Newly available protected app for Intune<!-- 28730764 -->

The following protected app is now available for Microsoft Intune:

- Notate for Intune by Shafer Systems, LLC

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of September 9, 2024

### App management

#### Managed Home Screen user experience update<!-- 28232751 -->

All Android devices automatically migrate to the updated Managed Home Screen (MHS) user experience. For more information, see [Updates to the Managed Home Screen experience](https://techcommunity.microsoft.com/t5/intune-customer-success/updates-to-the-managed-home-screen-experience/bc-p/3997842).

### Device enrollment

#### Support has ended for Apple profile-based user enrollment with Company Portal<!-- 28361917 -->

Apple supports two types of manual enrollment methods for users and devices in bring-your-own-device (BYOD) scenarios: *profile-based enrollment* and *account-driven enrollment*. Apple ended support for profile-based user enrollment, known in Intune as *user enrollment with Company Portal*. This method was their privacy-focused BYOD enrollment flow that used managed Apple IDs. As a result of this change, Intune has ended support for [profile-based user enrollment with Company Portal](../enrollment/apple-user-enrollment-with-company-portal.md). Users can no longer enroll devices targeted with this enrollment profile type. This change doesn't affect devices that are already enrolled with this profile type, so you can continue to manage them in the admin center and receive Microsoft Intune technical support. Less than 1% of Apple devices across all Intune tenants are currently enrolled this way, so this change doesn't affect most enrolled devices.

There's no change to profile-based device enrollment with Company Portal, the default enrollment method for BYOD scenarios. Devices enrolled via Apple automated device enrollment also remain unaffected.

We recommend account-driven user enrollment as a replacement method for devices. For more information about your BYOD enrollment options in Intune, see:

- [Account-driven user enrollment](../enrollment/apple-account-driven-user-enrollment.md)
- [Web-based device enrollment](../enrollment/web-based-device-enrollment-ios.md)
- [Device enrollment with Company Portal](../enrollment/ios-device-enrollment.md#app-or-web-based-enrollment) (default enrollment method for BYOD scenarios)

For more information about the device enrollment types supported by Apple, see [Intro to Apple device enrollment types](https://support.apple.com/en-mide/guide/deployment/dep08f54fcf6/web) in the Apple Platform Deployment guide.

### Device management

#### Intune now supports iOS/iPadOS 16.x as the minimum version<!-- 28391935 -->

Later this year, we expect iOS 18 and iPadOS 18 to be released by Apple. Microsoft Intune, including the Intune Company Portal and Intune app protection policies (APP, also known as MAM), will require iOS/iPadOS 16 and higher shortly after the iOS/iPadOS 18 release.

For more information on this change, see [Plan for change: Intune is moving to support iOS/iPadOS 16 and later](whats-new.md#plan-for-change-intune-is-moving-to-support-iosipados-16-and-later).

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

Applies to:

- iOS/iPadOS

#### Intune now supports macOS 13.x as the minimum version<!-- 28391869 -->

With Apple's release of macOS 15 Sequoia, Microsoft Intune, the Company Portal app, and the Intune MDM agent will now require macOS 13 (Ventura) and later.

For more information on this change, see [Plan for change: Intune is moving to support macOS 13 and later](whats-new.md#plan-for-change-intune-is-moving-to-support-macos-13-and-higher-later-this-year)

> [!NOTE]
> macOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement](https://aka.ms/Intune/macOS/ADE-DE-support).

Applies to:

- macOS

## Week of August 19, 2024 (Service release 2408)

### Microsoft Intune Suite

#### Easy creation of Endpoint Privilege Management elevation rules from support approval requests and reports<!-- 28196775 -->

You can now create Endpoint Privilege Management (EPM) elevation rules directly from a support approved elevation request or from details found in the EPM Elevation report. With this new capability, you won’t need to manually identify specific file detection details for elevation rules. Instead, for files that appear in the Elevation report or a support approved elevation request, you can select that file to open its elevation detail pane, and then select the option to **Create a rule with these file details**.

When you use this option, you can then choose to add the new rule to one of your existing elevation policies, or create a new policy with only the new rule.

Applies to:

- Windows 10
- Windows 11

For information about this new capability, see [Windows elevation rules policy](../protect/epm-policies.md) in the *Configure policies for Endpoint Privilege management* article.

#### Introducing the Resource performance report for physical devices in Advanced Analytics<!-- 12659827 -->

We're introducing the Resource performance report for Windows physical devices in Intune Advanced Analytics. The report is included as an Intune-add on under Microsoft Intune Suite.

The resource performance scores and insights for physical devices are aimed to help IT admins make CPU/RAM asset management and purchase decisions that improve the user experience while balancing hardware costs.

For more information, see:

- [Resource Performance Report](../../analytics/resource-performance-report.md)
- [Microsoft Intune Suite](../fundamentals/intune-add-ons.md)

### App management

#### Managed Home Screen for Android Enterprise Fully Managed devices<!-- 15603355 -->

Managed Home Screen (MHS) is now supported on Android Enterprise Fully Managed devices. This capability offers organizations the ability to leverage MHS in scenarios where a device is associated with a single user.

For related information, see:

- [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md)
- [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md)
- [Configure permissions for the Managed Home Screen (MHS) on Android Enterprise devices using Microsoft Intune](../configuration/oemconfig-managed-home-screen-permissions-android.md)

#### Updates to the Discovered Apps report<!-- 28898418 -->

The **Discovered Apps** report, which provides a list of detected apps that are on Intune enrolled devices for your tenant, now provides publisher data for Win32 apps, in addition to Store apps. Rather than providing publisher information only in the exported report data, we're including it as a column in the **Discovered Apps** report.

For more information, see [Intune Discovered apps](../apps/app-discovered-apps.md#monitor-discovered-apps-with-intune).

#### Improvements to Intune Management Extension logs<!-- 26113668 -->

We have updated how log activities and events are made for Win32 apps and the Intune Management Extension (IME) logs. A new log file (*AppWorkload.log*) contains all logging information related to app deployment activities conducted by the IME. These improvements provide better troubleshooting and analysis of app management events on the client.

For more information, see [Intune management extension logs](../apps/intune-management-extension.md#intune-management-extension-logs).

### Device configuration

#### New settings available in the Apple settings catalog <!-- 28308531 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Apple Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Declarative Device Management (DDM) > Safari Extension Settings**:

- Managed Extensions
  - Allowed Domains
  - Denied Domains
  - Private Browsing
  - State

**Declarative Device Management (DDM) > Software Update Settings**:

- Automatic Actions
  - Download
  - Install OS Updates

- Deferrals
  - Combined Period In Days

- Notifications

- Rapid Security Response
  - Enable
  - Enable Rollback

- Recommended Cadence

**Restrictions**:

- Allow ESIM Outgoing Transfers
- Allow Genmoji
- Allow Image Playground
- Allow Image Wand
- Allow iPhone Mirroring
- Allow Personalized Handwriting Results
- Allow Video Conferencing Remote Control
- Allow Writing Tools

##### macOS

**Authentication > Extensible Single Sign On (SSO)**:

- Platform SSO
  - Authentication Grace Period
  - FileVault Policy
  - Non Platform SSO Accounts
  - Offline Grace Period
  - Unlock Policy

**Authentication > Extensible Single Sign On Kerberos**:

- Allow Password
- Allow SmartCard
- Identity Issuer Auto Select Filter
- Start In Smart Card Mode

**Declarative Device Management (DDM) > Disk Management**:

- External Storage
- Network Storage

**Declarative Device Management (DDM) > Safari Extension Settings**:

- Managed Extensions
  - Allowed Domains
  - Denied Domains
  - Private Browsing
  - State

**Declarative Device Management (DDM) > Software Update Settings**:

- Allow Standard User OS Updates

- Automatic Actions
  - Download
  - Install OS Updates
  - Install Security Update

- Deferrals
  - Major Period In Days
  - Minor Period In Days
  - System Period In Days

- Notifications

- Rapid Security Response
  - Enable
  - Enable Rollback

**Restrictions**:

- Allow Genmoji
- Allow Image Playground
- Allow iPhone Mirroring
- Allow Writing Tools

**System Policy > System Policy Control**:

- Enable XProtect Malware Upload

#### Enhancements to multi administrative approval<!-- 25174473 -->

Multi administrative approval adds the ability to limit application access policies to Windows applications or all non-Windows applications or both. We're adding a new access policy to the multiple administrative approval feature to allow approvals for changes to multiple administrative approval.

For more information, see [Multi admin approval](../fundamentals/multi-admin-approval.md).

### Device enrollment

#### Account-driven Apple User Enrollment now generally available for iOS/iPadOS 15+<!-- 10277062 -->

Intune now supports account-driven Apple User Enrollment, the new, and improved version of Apple User Enrollment, for devices running iOS/iPadOS 15 and later. This new enrollment method utilizes just-in-time registration, removing the Company Portal app for iOS as an enrollment requirement. Device users can initiate enrollment directly in the Settings app, resulting in a shorter and more efficient onboarding experience.

For more information, see [Set up account driven Apple User Enrollment](../enrollment/apple-account-driven-user-enrollment.md) on Microsoft Learn.

Apple announced they are ending support for profile-based Apple User Enrollment. As a result, Microsoft Intune will end support for Apple User Enrollment with Company Portal shortly after the release of iOS/iPadOS 18. We recommend enrolling devices with account-driven Apple User Enrollment for similar functionality and an improved user experience.

#### Use corporate Microsoft Entra account to enable Android Enterprise management options in Intune<!-- 25231452 -->

Managing Intune-enrolled devices with Android Enterprise management options previously required you to connect your Intune tenant to your managed Google Play account using an enterprise Gmail account. Now you can use a corporate Microsoft Entra account to establish the connection. This change is happening in new tenants, and doesn't affect tenants that have already established a connection.

For more information, see [Connect Intune account to Managed Google Play account - Microsoft Intune | Microsoft Learn](../enrollment/connect-intune-android-enterprise.md).

### Device management

#### 21Vianet support for Mobile Threat Defense connectors<!-- 10355489 -->

Intune operated by 21Vianet now supports Mobile Threat Defense (MTD) connectors for Android and iOS/iPadOS devices for MTD vendors that also have support in that environment. When an MTD partner is supported and you sign in to a 21Vianet tenant, the supported connectors are available.

Applies to:

- Android
- iOS/iPadOS

For more information, see:

- [Intune operated by 21Vianet in China](../fundamentals/china.md)
- [Mobile Threat Defense integration with Intune](../protect/mobile-threat-defense.md)

#### New `cpuArchitecture` filter device property for app and policy assignments<!-- 7423106 -->

When you assign an app, compliance policy, or configuration profile, you can filter the assignment using different device properties, such as device manufacturer, operating system SKU, and more.

A new `cpuArchitecture` device filter property is available for Windows and macOS devices. With this property, you can filter app and policy assignments depending on the processor architecture.

For more information on filters and the device properties you can use, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [Filter properties](filters-device-properties.md)
- [Supported workloads](filters-supported-workloads.md)

Applies to:

- Windows 10
- Windows 11
- macOS

### Device security

#### Windows platform name change for endpoint security policies<!-- 16104088 -->

When you create an endpoint security policy in Intune, you can select the Windows platform. For multiple templates in endpoint security, there are now only two options to choose for the Windows platform: **Windows** and **Windows (ConfigMgr)**.

Specifically, the platform name changes are:

| Original | New |
| --- | --- |
| Windows 10 and later​ | Windows |
| Windows 10 and later (ConfigMgr)​ | Windows (ConfigMgr)​ |
| Windows 10, Windows 11, and Windows Server | Windows |
| Windows 10, Windows 11, and Windows Server​ (ConfigMgr) | Windows (ConfigMgr)​ |

These changes apply to the following policies:

- Antivirus
- Disk encryption
- Firewall
- Endpoint Privilege Management
- Endpoint detection and response
- Attack surface reduction
- Account protection

##### What you need to know

- This change is only in the user experience (UX) that admins see when they create a new policy. There is no effect on devices.
- The functionally is the same as the previous platform names.
- There are no additional tasks or actions for existing policies.

For more information on endpoint security features in Intune, see [Manage endpoint security in Microsoft Intune](../protect/endpoint-security.md).

Applies to:

- Windows

#### Target Date Time setting for Apple software update enforcement schedules updates using the local time on devices <!-- 28865232 -->

You can specify the time that OS updates are enforced on devices in their local time zone. For example, configuring an OS update to be enforced at 5pm schedules the update for 5pm in the device's local time zone. Previously, this setting used the time zone of the browser where the policy was configured.

This change only applies to new policies that are created in the August 2408 release and later. The **Target Date Time** setting is in the [settings catalog](../configuration/settings-catalog.md) at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type > **Declarative Device Management** > Software Update.

In a future release, the **UTC** text will be removed from the **Target Date Time** setting.

For more information on using the settings catalog to configure software updates, see [Managed software updates with the settings catalog](../protect/managed-software-updates-ios-macos.md).

Applies to:

- iOS/iPadOS
- macOS

### Intune Apps

#### Newly available protected apps for Intune<!-- 28676100, 28442762, 28421791, 28441819, 28618264 -->

The following protected apps are now available for Microsoft Intune:

- Singletrack for Intune (iOS) by Singletrack
- 365Pay by 365 Retail Markets
- Island Browser for Intune (Android) by Island Technology, Inc.
- Recruitment.Exchange by Spire Innovations, Inc.
- Talent.Exchange by Spire Innovations, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Tenant administration

#### Organizational messages now in Microsoft 365 admin center<!-- 27711197 -->

The organizational message feature has moved out of the Microsoft Intune admin center and into its new home in the Microsoft 365 admin center. All organizational messages you created in Microsoft Intune are now in the Microsoft 365 admin center, where you can continue to view and manage them. The new experience includes highly requested features such as the ability to author custom messages, and deliver messages on Microsoft 365 apps.

For more information, see:

- [Introducing organizational messages (preview) in the Microsoft 365 admin center](https://techcommunity.microsoft.com/t5/microsoft-365-blog/introducing-organizational-messages-preview-in-the-microsoft-365/ba-p/4123890)
- [Organizational messages in the Microsoft 365 admin center](/microsoft-365/admin/misc/organizational-messages-microsoft-365)
- [Support tip: Organizational messages is moving to Microsoft 365 admin center - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-organizational-messages-is-moving-to-microsoft-365/ba-p/4148332)

## Week of July 29, 2024

### Microsoft Intune Suite

#### Endpoint Privilege Management, Advanced Analytics, and Intune Plan 2 are available for GCC High and DoD<!-- 25230811, 25300700, 27030977, 27234960 -->

We are excited to announce that the following capabilities from the Microsoft Intune Suite are now supported in U.S. Government Community Cloud (GCC) High and U.S. Department of Defense (DoD) environments.

Add-on capabilities:

- [Endpoint Privilege Management](../protect/epm-overview.md)
- [Advanced Analytics](../../analytics/advanced-endpoint-analytics.md) - With this release, GCC High and DoD support for Advanced Endpoint Analytics doesn't include the [*Device query*](../../analytics/device-query.md) functionality.

Plan 2 capabilities:

- [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-mam.md)
- [Firmware-over-the-air update](../protect/zebra-lifeguard-ota-integration.md)
- [Specialty devices management](../fundamentals/specialty-devices-with-intune.md)

For more information, see:

- [Use Microsoft Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md)
- [Microsoft Intune for US Government GCC service description](../fundamentals/intune-govt-service-description.md)

### Device enrollment

#### ACME protocol support for iOS/iPadOS and macOS enrollment<!-- 25140355 -->

As we prepare to support managed device attestation in Intune, we are starting a phased rollout of an infrastructure change for new enrollments that includes support for the *Automated Certificate Management Environment (ACME) protocol*. Now when new Apple devices enroll, the management profile from Intune receives an ACME certificate instead of a SCEP certificate. ACME provides better protection than SCEP against unauthorized certificate issuance through robust validation mechanisms and automated processes, which helps reduce errors in certificate management.

Existing OS and hardware eligible devices do not get the ACME certificate unless they re-enroll. There is no change to the end user's enrollment experience, and no changes to the Microsoft Intune admin center. This change only impacts enrollment certificates and has no impact on any device configuration policies.

ACME is supported for Apple Device Enrollment, Apple Configurator enrollment, and Automated device enrollment (ADE) methods. Eligible OS versions include:

- iOS 16.0 or later
- iPadOS 16.1 or later
- macOS 13.1 or later

This capability is also supported in [GCC High tenants](../fundamentals/intune-govt-service-description.md).



## What's new archive
<!-- Past announcements that are older than six months will be moved to the archive -->

For previous months, see the [What's new archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
