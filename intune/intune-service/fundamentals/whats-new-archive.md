---
title: What's new in previous months in the Microsoft Intune
description: Review older announcements from the Intune what's new page
author: brenduns
ms.author: brenduns
ms.date: 10/02/2025
ms.topic: whats-new

ROBOTS: NOINDEX,NOFOLLOW
ms.reviewer: lebacon
ms.collection:
- M365-identity-device-management
---

# What's new in the Microsoft Intune - previous months

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

<!-- Maintenance plan:

     Maintain ~2 years of archived content -->


## Week of February 24, 2025 (Service release 2502)

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

#### Low privileged account for Intune Connector for Active Directory for Hybrid join Windows Autopilot flows<!-- 28662823 -->

The Intune Connector for Active Directory now uses a low privileged account, which helps increase the security of your environment. The old connector continues to work until deprecation in late May 2025.

For more information, see [Deploy Microsoft Entra hybrid joined devices by using Intune and Windows Autopilot](../../autopilot/windows-autopilot-hybrid.md).

#### Managed Home Screen QR Code Authentication in public preview<!-- 25348926 -->

Managed Home Screen for Android devices natively supports QR Code Authentication in Microsoft Entra ID. Authentication involves both a QR code and PIN. This capability eliminates the need for users to enter and re-enter long UPNs and alphanumeric passwords. For more information, see [Sign in to Microsoft Teams or Managed Home Screen (MHS) with QR code](/entra/identity/authentication/how-to-authentication-qr-code#sign-in-to-microsoft-teams-or-managed-home-screen-mhs-with-qr-code).

Applies to:

- Android devices

#### More device details for Managed Home Screen<!-- 27006536 -->

Android **OS version**, **Security patch**, and **Last device reboot time** details are now available from the **Device Information** page of the Managed Home Screen app. For related information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

Applies to:

- Android Enterprise devices

#### Display ringtone selector for Managed Home Screen<!-- 26826233 -->

In Intune, you can choose to expose a setting in the Managed Home Screen app to allow users to select a ringtone. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

Applies to:

- Android devices

### Device security

#### Manage the DeviceControlEnabled configuration for Microsoft Defender Device Control on Windows devices<!-- 31171641 -->

You can now use Intune to manage the configuration of the Microsoft Defender CSP for [DeviceControlEnabled](/windows/client-management/mdm/defender-csp#configurationdevicecontrolenabled) for Device Control. DeviceControlEnabled is used to enable or disable support for the Microsoft Defender Device Control feature on Windows devices.

You can use the following two Microsoft Intune options to configure DeviceControlEnabled. With both options, the setting appears as **Device Control Enabled**, and is found in the *Defender* category:

- Configure a [**Device Control** template](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy), which is a profile for [Attack Surface Reduction](../protect/endpoint-security-asr-policy.md) policy.
- Configure a [**Settings Catalog** profile](../configuration/settings-catalog.md#create-the-policy) for Windows.

Both the Device Control template and Settings Catalog support the following options for *Device Control Enabled*:

- Device Control is enabled
- Device Control is disabled (Default)

Applies to:

- Windows

#### Manage the DefaultEnforcement configuration for Microsoft Defender Device Control on Windows devices<!-- 30253799 -->

You can now use Intune to manage the configuration of the Microsoft Defender CSP for [DefaultEnforcement](/windows/client-management/mdm/defender-csp#configurationdefaultenforcement) for Device Control.

DefaultEnforcement manages the configuration of Device Control:

- On devices that don't receive Device Control policies
- For devices that receive and evaluate a policy for Device Control when no rules in the policy are matched

You can use the following two Microsoft Intune options to configure DefaultEnforcement. With both options, the setting appears as **Default Enforcement**, and is found in the *Defender* category:

- Configure a [**Device Control** template](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy), which is a profile for [Attack Surface Reduction](../protect/endpoint-security-asr-policy.md) policy.
- Configure a [**Settings Catalog** profile](../configuration/settings-catalog.md#create-the-policy) for Windows.

Both the Device Control template and Settings Catalog support the following options for *Default Enforcement*:

- Default Allow Enforcement (Default)
- Default Deny Enforcement

Applies to:

- Windows

### Intune apps

#### Newly available protected app for Intune<!-- 30508606 -->

The following protected app is now available for Microsoft Intune:

- Applications Manager - Intune by ManageEngine

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Device configuration

#### New settings available in the Apple settings catalog<!-- 30457000 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings For Apple devices in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

#### iOS/iPadOS

**Managed Settings**:
- Default Applications
- Wallpaper

**Networking > Domains**:
- Cross Site Tracking Prevention Relaxed Apps

**Restrictions**:
- Allowed External Intelligence Workspace IDs
- Allow Notes Transcription Summary
- Allow Satellite Connection
- Allow Visual Intelligence Summary

#### macOS

**Networking > Domains**:

- Cross Site Tracking Prevention Relaxed Apps

**Restrictions**:

- Allow Bookstore
- Allow Bookstore Erotica
- Allow Explicit Content
- Rating Apps
- Rating Movies
- Rating Region
- Rating TV Shows

**System Configuration > File Provider**:

- Management Allows Known Folder Syncing
- Management Known Folder Syncing Allow List


## Week of February 17, 2025

### Monitor and troubleshoot

#### Limited live chat support in Intune<!-- 30477421 -->

Intune is introducing limited live chat support within the Intune admin console. Live chat isn't available for all tenants or inquiries at this time.

## Week of February 10, 2025

### Device security

#### Updated security baseline for Windows version 24H2<!-- 29819143 -->

You can now deploy the Intune security baseline for **Windows version 24H2** to your Windows 10 and Windows 11 devices. The new baseline version uses the unified settings platform seen in the Settings Catalog. This change features an improved user interface and reporting experience, more consist and accurate improvements with setting tattooing, and supports profile assignment filters.

Use of [Intune security baselines](../protect/security-baselines.md) can help you maintain best-practice configurations for your Windows devices. It can also help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline represents the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows

### Monitor and troubleshoot

#### Device Query for Multiple Devices<!--25234456 -->

Device query for multiple devices is available. This feature allows you to gain comprehensive insights about your entire fleet of devices using Kusto Query Language (KQL) to query across collected inventory data for your devices.

Device query for multiple devices is now supported for devices running Windows 10 or later. This feature is now included as part of Advanced Analytics.

Applies to:

- Windows

## Week of February 5, 2025 (Service release 2501)

### Microsoft Intune Suite

#### Use Microsoft Security Copilot with Endpoint Privilege Management to help identify potential elevation risks<!-- 27265509 -->

When your Azure Tenant is licensed for Microsoft Security Copilot, you can now use Security Copilot to help you investigate Endpoint Privilege Management (EPM) file elevation requests from within the EPM [support approved](../protect/epm-support-approved.md#use-microsoft-security-copilot-to-analyze-file-elevation-requests) work flow.

With this capability, while reviewing the properties of a file elevation request, you see the **Analyze with Copilot** option. This option directs Security Copilot to use the files hash in a prompt Microsoft Defender Threat Intelligence to evaluate the file for potential indicators of compromise. You can then make a more informed decision to either approve or deny that file elevation request. Some of the results that are returned to your current view in the admin center include:

- The files' reputation
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

Applies to:

- Windows 10 and later (Corporate owned devices managed by Intune)

## Week of January 27, 2025

### Device security

#### Security baselines for HoloLens 2<!-- 24914095 -->

You can now deploy two distinct instances of the security baseline for HoloLens 2. These baselines represent Microsoft's best practice guidelines and experience from deploying and supporting HoloLens 2 devices to customers across various industries. The two baselines instances:

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

You can now manage the Microsoft Defender for Endpoint CSP setting for [tamper protection](/windows/client-management/mdm/defender-csp) on unenrolled devices you manage as part of the [Defender for Endpoint security settings management](../protect/mde-security-integration.md#which-solution-should-i-use) scenario.

With this support, tamper protection configurations from *Windows Security Experience* profiles for *Antivirus* policies now apply to all devices instead of only to those that are enrolled with Intune.

### Device configuration

#### Ending support for administrative templates when creating a new configuration profile<!-- 29989512 -->

Customers cannot create new Administrative Templates configuration profile through **Devices > Configuration > Create > New policy > Windows 10 and later > Administrative Templates**. A (retired) tag is seen next to **Administrative Templates** and the **Create** button is now greyed out. Other templates continue to be supported.

However, customers can now use the Settings Catalog for creating new **Administrative Templates** configuration profile by navigating to **Devices > Configuration > Create > New policy > Windows 10 and later > Settings Catalog**.

There are no changes in the following UI experiences:

- Editing an existing Administrative template.
- Deleting an existing Administrative template.
- Adding, modifying, or deleting settings in an existing Administrative template.
- **Imported Administrative templates (Preview)** template, which is used for Custom ADMX.

For more information, see [Use ADMX templates on Windows devices in Microsoft Intune](../configuration/administrative-templates-windows.md).

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

For more information, see [Wi-Fi settings for personally-owned work profile devices.](../configuration/wi-fi-settings-android-enterprise.md).

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

At Apple WWDC 2024, Apple ended support for profile-based Apple user enrollment. For more information, see [Support has ended for profile-based user enrollment with Company Portal](../fundamentals/whats-new-archive.md#support-has-ended-for-apple-profile-based-user-enrollment-with-company-portal). As a result of this change, we updated the behavior that occurs when you select **Determine based on user choice** as the enrollment profile type for bring-your-own-device (BYOD) enrollments.

Now when users select **I own this device** during a BYOD enrollment, Microsoft Intune enrolls them via account-driven user enrollment, rather than profile-based user enrollment, and then secures only work-related apps. Less than one percent of Apple devices across all Intune tenants are currently enrolled this way, so this change doesn't affect most enrolled devices. There is no change for iOS users who select **My company owns this device** during a BYOD enrollment. Intune enrolls them via device enrollment with Intune Company Portal, and then secures their entire device.

If you currently allow users in BYOD scenarios to determine their enrollment profile type, you must take action to ensure account-driven user enrollment works by completing all prerequisites. For more information, see [Set up account driven Apple user enrollment](../enrollment/apple-account-driven-user-enrollment.md). If you don't give users the option to choose their enrollment profile type, there are no action items.

### Device management

#### Device Inventory for Windows<!-- 24853010 -->

Device inventory lets you collect and view additional hardware properties from your managed devices to help you better understand the state of your devices and make business decisions.

You can now choose what you want to collect from your devices, using the catalog of properties and then view the collected properties in the Resource Explorer view.

For more information, see:

- [Properties catalog](../configuration/properties-catalog.md)
- [Data collection platform](../../analytics/data-platform-schema.md)

## Week of November 18, 2024 (Service release 2411)

### App management

#### Configuration values for specific managed applications on Intune enrolled iOS devices<!-- 30293382 -->

Starting with Intune's September (2409) service release, the **IntuneMAMUPN**, **IntuneMAMOID**, and **IntuneMAMDeviceID** app configuration values are automatically sent to managed applications on Intune enrolled iOS devices for the following apps:

- Microsoft Excel
- Microsoft Outlook
- Microsoft PowerPoint
- Microsoft Teams
- Microsoft Word

For more information, see Intune [Support tip: Intune MAM users on iOS/iPadOS userless devices may be blocked in rare cases](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-intune-mam-users-on-iosipados-userless-devices-may-be-blocked-in-rar/4254335).

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

Now generally available, customer tenants in the Government Community Cloud (GCC), US Government Community High (GCC High), and Department of Defense (DoD) environments can use Intune to manage the Defender security settings on the devices you've onboarded to Defender without enrolling those devices with Intune. Previously, support for Defender security settings was in public preview.

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

For information about this Windows Autopilot device preparation support, see the following in the Windows Autopilot device preparation documentation:

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

- Windows, iOS/iPadOS, and macOS user certificates
- Windows device certificates

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

For Windows devices, you can create a DFCI profile to manage UEFI (BIOS) settings. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type.

Some VAIO devices running Windows are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

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

With the release of iOS 18 and iPadOS 18, Microsoft Intune, including the Intune Company Portal and Intune app protection policies (APP, also known as MAM), will now require iOS/iPadOS 16 and higher.

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

Applies to:

- iOS/iPadOS

#### Intune now supports macOS 13.x as the minimum version<!-- 28391869 -->

With Apple's release of macOS 15 Sequoia, Microsoft Intune, the Company Portal app, and the Intune MDM agent will now require macOS 13 (Ventura) and later.

> [!NOTE]
> macOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement](https://aka.ms/Intune/macOS/ADE-DE-support).

Applies to:

- macOS

## Week of August 19, 2024 (Service release 2408)

### Microsoft Intune Suite

#### Easy creation of Endpoint Privilege Management elevation rules from support approval requests and reports<!-- 28196775 -->

You can now create Endpoint Privilege Management (EPM) elevation rules directly from a support approved elevation request or from details found in the EPM Elevation report. With this new capability, you won't need to manually identify specific file detection details for elevation rules. Instead, for files that appear in the Elevation report or a support approved elevation request, you can select that file to open its elevation detail pane, and then select the option to **Create a rule with these file details**.

When you use this option, you can then choose to add the new rule to one of your existing elevation policies, or create a new policy with only the new rule.

Applies to:

- Windows 10
- Windows 11

For information about this new capability, see [Windows elevation rules policy](../protect/epm-elevation-rules.md) in the *Configure policies for Endpoint Privilege management* article.

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

For more information on using the settings catalog to configure software updates, see [Managed software updates with the settings catalog](../protect/updates/apple.md).

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

## Week of July 22, 2024 (Service release 2407)

### Microsoft Intune Suite

#### New actions for Microsoft Cloud PKI<!-- 24231040 -->

The following actions have been added for Microsoft Cloud PKI issuing and root certification authorities (CA):

- Delete: Delete a CA.
- Pause: Temporarily suspend use of a CA.
- Revoke: Revoke a CA certificate.

You can access all new actions in the Microsoft Intune admin center and Graph API. For more information, see [Delete Microsoft Cloud PKI certification authority](../protect/microsoft-cloud-pki-delete.md).

### App management

#### Intune support for additional macOS app types from the Company Portal<!-- 26133163 -->

Intune supports the capability to deploy DMG and PKG apps as **Available** in the Intune macOS Company Portal. This capability enables end users to browse and install agent-deployed applications using Company Portal for macOS. This capability requires a minimum version of the Intune agent for macOS v2407.005 and Intune Company Portal for macOS v5.2406.2.

#### Newly available Enterprise App Catalog apps for Intune<!-- 28691663 -->

The Enterprise App Catalog has updated to include additional apps. For a complete list of supported apps, see [Apps available in the Enterprise App Catalog](../apps/apps-enterprise-app-management.md#apps-available-in-the-enterprise-app-catalog).

#### The Intune App SDK and Intune App Wrapping Tool are now in a different GitHub repo<!-- 27264674, 27264632 -->

The Intune App SDK and Intune App Wrapping Tool have moved to a different GitHub repository and a new account. There are redirects in place for all existing repositories. In addition, the Intune sample applications are also included in this move. This change relates to both Android and iOS platforms.

### Device configuration

#### New clipboard transfer direction settings available in the Windows settings catalog <!-- 28748086 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type.

**Administrative Templates > Windows Components > Remote Desktop Services > Remote Desktop Session Host > Device and Resource Redirection**:

- Restrict clipboard transfer from server to client
- Restrict clipboard transfer from server to client (User)
- Restrict clipboard transfer from client to server
- Restrict clipboard transfer from client to server (User)

For more information on configuring the clipboard transfer direction in Azure Virtual Desktop, see [Configure the clipboard transfer direction and types of data that can be copied in Azure Virtual Desktop](/azure/virtual-desktop/clipboard-transfer-direction-data-types).

Applies to:

- Windows 11
- Windows 10

#### New settings available in the Apple settings catalog <!-- 28052449 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Restrictions**:

- Allow Auto Dim

##### macOS

**Privacy > Privacy Preferences Policy Control**:

- Bluetooth Always

#### Android Enterprise has new values for the Allow access to all apps in Google Play store setting<!-- 28367525 -->

In an Intune device restrictions configuration policy, you can configure the **Allow access to all apps in Google Play store** setting using the **Allow** and **Not configured** options (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully managed, dedicated and corporate-owned work profile > Device restrictions** for profile type > **Applications**).

The available options are updated to **Allow**, **Block**, and **Not configured**.

There's no impact to existing profiles using this setting.

For more information on this setting and the values you can currently configure, see [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:

- Android Enterprise Fully managed, dedicated and corporate-owned work profile

### Device enrollment

#### New support for Red Hat Enterprise Linux<!-- 25160548 -->

Microsoft Intune now supports device management for Red Hat Enterprise Linux. You can enroll and manage Red Hat Enterprise Linux devices, and assign standard compliance policies, custom configuration scripts, and compliance scripts. For more information, see [Deployment guide: Manage Linux devices in Microsoft Intune](deployment-guide-platform-linux.md) and [Enrollment guide: Enroll Linux desktop devices in Microsoft Intune](deployment-guide-enrollment-linux.md).

Applies to:

- Red Hat Enterprise Linux 9
- Red Hat Enterprise Linux 8

#### New Intune report and device action for Windows enrollment attestation (public preview)<!-- 12581956 -->

Use the new device attestation status report in Microsoft Intune to find out if a device has attested and enrolled securely while being hardware-backed. From the report, you can attempt remote attestation via a new device action.

For more information, see:

- [Windows enrollment attestation](../enrollment/windows-enrollment-attestation.md)
- [Intune Reports](../fundamentals/reports.md#device-attestation-status-report)

#### Just-in-time registration and compliance remediation available for all iOS/iPadOS enrollments<!-- 27759589 -->

You can now configure just-in-time (JIT) registration and JIT compliance remediation for all Apple iOS and iPadOS enrollments. These Intune-supported features improve the enrollment experience because they can take the place of the Intune Company Portal app for device registration and compliance checks. We recommend setting up JIT registration and compliance remediation for new enrollments, and to improve the experience for existing enrolled devices. For more information, see [Set up just in time registration in Microsoft Intune](../enrollment/set-up-just-in-time-registration.md).

### Device management

#### Consolidation of Intune profiles for identity protection and account protection <!-- 24810271 -->

We have consolidated the Intune profiles that were related to identity and account protection, into a single new profile named *Account protection*. This new profile is found in the [account protection policy node of endpoint security](../protect/endpoint-security-account-protection-policy.md), and is now the only profile template that remains available when creating new policy instances for identity and account protection. The new profile includes Windows Hello for Business settings for both users and devices, and settings for Windows Credential Guard.

Because this new profile uses Intune's unified settings format for device management, the profiles settings are also available through the [settings catalog](../configuration/settings-catalog.md), and help to improve the reporting experience in the Intune admin center.

You can continue to use any instances of the following profile templates that you already have in place, but Intune no longer supports creating new instances of these profiles:

- **Identity protection** – previously available from *Devices* > *Configuration* > *Create* > *New Policy* > *Windows 10 and later* > *Templates* > *Identity Protection*
- **Account protection (Preview)** – previously available from *Endpoint Security* > *Account protection* > *Windows 10 and later* > *Account protection (Preview)*

Applies to:

- Windows 10
- Windows 11

#### New `operatingSystemVersion` filter property with new comparison operators (preview) <!-- 10033345 -->

There's a new `operatingSystemVersion` filter property. This property:

- Is in [public preview](public-preview.md) and still being developed. So, some features, like **Preview devices**, don't work yet.

- Should be used instead of the existing `OSVersion` property. The `OSVersion` property is being deprecated.

  When `operatingSystemVersion` is generally available (GA), the `OSVersion` property will retire, and you won't be able to create new filters using this property. Existing filters that use `OSVersion` continue to work.

- Has new comparison operators:

  - `GreaterThan`: Use for version value types.

    - Allowed values: `-gt` | `gt`
    - Example: `(device.operatingSystemVersion -gt 10.0.22000.1000)`

  - `GreaterThanOrEquals`: Use for version value types.

    - Allowed values: `-ge` | `ge`
    - Example: `(device.operatingSystemVersion -ge 10.0.22000.1000)`

  - `LessThan`: Use for version value types.

    - Allowed values: `-lt | lt`
    - Example: `(device.operatingSystemVersion -lt 10.0.22000.1000)`

  - `LessThanOrEquals`: Use for version value types.

    - Allowed values: `-le` | `le`
    - Example: `(device.operatingSystemVersion -le 10.0.22000.1000)`

For managed devices, `operatingSystemVersion` applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

For managed apps, `operatingSystemVersion` applies to:

- Android
- iOS/iPadOS
- Windows

For more information on filters and the device properties you can use, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [Filter properties](filters-device-properties.md)

#### Government community cloud (GCC) support for Remote Help for macOS devices<!-- 25568551 -->

GCC customers can now use Remote Help for macOS devices on both web app and native application.

Applies to:

- macOS 12, 13 and 14

For more information, see:

- [Remote Help on macOS](../fundamentals/remote-help-macos.md)
- [Microsoft Intune for US Government GCC service description](../fundamentals/intune-govt-service-description.md)

### Device security

#### Updated security baseline for Windows 365 Cloud PC<!-- 26504698 -->

You can now deploy the Intune security baseline for **Windows 365 Cloud PC**. This new baseline is based on Windows **version 24H1**. This new baseline version uses the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline represents the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

To view the new baselines included settings with their default configurations, see, [Windows 365 baseline settings version 24H1](../protect/security-baseline-settings-windows-365.md?pivots=win365-24h1).

### Intune apps

#### Newly available protected apps for Intune<!-- 28334000, 28157519, 28311088, 28156655, 28246919, 28246936, 28100886 -->

The following protected apps are now available for Microsoft Intune:

- Asana: Work in one place (Android) by Asana, Inc.
- Goodnotes 6 (iOS) by Time Base Technology Limited
- Riskonnect Resilience by Riskonnect, Inc.
- Beakon Mobile App by Beakon Mobile Team
- HCSS Plans: Revision control (iOS) by Heavy Construction Systems Specialists, Inc.
- HCSS Field: Time, cost, safety (iOS) by Heavy Construction Systems Specialists, Inc.
- Synchrotab for Intune (iOS) by Synchrotab, LLC

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of July 15, 2024

### Device management

#### New setting in the Device Control profile for Attack surface reduction policy<!-- 28761508 -->

We've added a new category and setting to the Device Control profile for the *Windows 10, Windows 11, and Windows Server* platform of Intune [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

The new setting is **Allow Storage Card**, and found in the new **System** category of the profile. This setting is also available from the Intune [settings catalog](../configuration/settings-catalog.md) for the Windows devices.

This setting controls whether the user is allowed to use the storage card for device storage, and can prevent programmatic access to the storage card. For more information on this new setting, see [AllowStorageCard](/windows/client-management/mdm/policy-csp-system?branch=main&branchFallbackFrom=pr-en-us-15655&WT.mc_id=Portal-fx#allowstoragecard) in the Windows documentation.

## Week of July 8, 2024

### Device management

#### Copilot in Intune now has the device query feature using Kusto Query Language (KQL) (public preview)<!-- 24874816 -->

When you use Copilot in Intune, there's a new device query feature that uses KQL.
Use this feature to ask questions about your devices using a natural language. If device query can answer your question, Copilot generates the KQL query you can run to get the data you want.

To learn more about how you can currently use Copilot in Intune, see [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md).

### Monitor and Troubleshoot

#### New actions for policies, profiles, and apps<!-- 15283153 -->

You can now remove, reinstall, and reapply individual policies, profiles, and apps for iOS/iPadOS devices and Android corporate owned devices. You can apply these actions without changing assignments or group membership. These actions are intended to help resolve customer challenges that are external to Intune. Also, these actions can help to quickly restore end user productivity.

For more information, see [Remove apps and configuration](../remote-actions/remove-apps-config.md)

### App management

#### MAC address available from the Managed Home Screen app<!-- 25994454 -->

MAC address details are now available from the **Device Information** page of the Managed Home Screen (MHS) app. For information about MHS, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### New configuration capabilities for Managed Home Screen<!-- 25013268 -->

You can now configure Managed Home Screen (MHS) to enable a virtual app-switcher button that allows end users to easily navigate between apps on their kiosk devices from MHS. You can select between a floating or swipe-up app-switcher button. The configuration key is `virtual_app_switcher_type` and the possible values are `none`, `float`, and `swipe_up`. For information related to configuring the Managed Home Screen app, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

### Device enrollment

#### Update for Apple user and device enrollments with Company Portal <!-- 27557088 -->

We've made changes to the device registration process for Apple devices enrolling with Intune Company Portal. Previously, Microsoft Entra device registration occurred during enrollment. With this change, registration occurs after enrollment.

Existing enrolled devices aren't affected by this change. For new user or device enrollments that utilize Company Portal, users must return to Company Portal to complete registration:

- For iOS users: Users with notifications enabled are prompted to return to the Company Portal app for iOS. If they disable notifications, they aren't alerted, but still need to return to Company Portal to complete registration.

- For macOS devices: The Company Portal app for macOS detects the installation of the management profile and automatically register the device, unless the user closes the app. If they close the app, they must reopen it to complete registration.

If you're using dynamic groups, which rely on device registration to work, it's important for users to complete device registration. Update your user guidance and admin documentation as needed. If you're using Conditional Access (CA) policies, no action is required. When users attempt to sign in to a CA-protected app, they are prompted to return to Company Portal to complete registration.

These changes are currently rolling out and will be made available to all Microsoft Intune tenants by the end of July. There's no change to the Company Portal user interface. For more information about device enrollment for Apple devices, see:

- [Enrollment guide: Enroll macOS devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-macos.md#device-enrollment-end-user-tasks)
- [Enrollment guide: Enroll iOS and iPadOS devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-ios-ipados.md)

## Week of June 24, 2024

### Device enrollment

#### Add corporate device identifiers for Windows<!-- 25873757 -->

Microsoft Intune now supports corporate device identifiers for devices running Windows 11, version 22H2 and later so that you can identify corporate machines ahead of enrollment. When a device that matches the model, manufacturer, and serial number criteria enrolls, Microsoft Intune marks it as a corporate device and enable the appropriate management capabilities. For more information, see [Add corporate identifiers](../enrollment/corporate-identifiers-add.md).

### Microsoft Intune Suite

#### Remote Help

Version 5.1.1419.0

- Resolve issue where the screen may be blank on first launch.

## Week of June 17, 2024 (Service release 2406)

### Microsoft Intune Suite

#### Endpoint Privilege Management support for MSI and PowerShell file types<!-- 25230336 -->

Endpoint Privilege Management (EPM) *elevation rules* now support the elevation of Windows Installer and PowerShell files in addition to executable files that were previously supported. The new file extensions that EPM supports include:

- .msi
- .ps1

For information about using EPM, see [Endpoint Privilege Management](../protect/epm-overview.md).

#### View the certification authority key type in Microsoft Cloud PKI properties<!-- 27032276 -->

A new Microsoft Cloud PKI property called *CA keys* is available in the admin center and shows the type of certification authority keys used for signing and encryption. The property displays one of the following values:

- HSM: Indicates the use of a hardware security module-backed key.
- SW: Indicates the use of a software-backed key.

Certification authorities created with a licensed Intune Suite or Cloud PKI standalone add-on use HSM signing and encryption keys. Certification authorities created during a trial period use software-backed signing and encryption keys. For more information about Microsoft Cloud PKI, see [Overview of Microsoft Cloud PKI for Microsoft Intune](../protect/microsoft-cloud-pki-overview.md).

### App management

#### US GCC and GCC High support for Managed Home Screen<!-- 25827679 -->

Managed Home Screen (MHS) now supports sign-in for the US Government Community (GCC), US Government Community (GCC) High, and U.S. Department of Defense (DoD) environments. For more information, see [Configure the Managed Home Screen](../apps/app-configuration-managed-home-screen-app.md) and [Microsoft Intune for US Government GCC service description](../fundamentals/intune-govt-service-description.md).

Applies to:

- Android Enterprise

#### Updates to the Managed Apps report<!-- 26711898 -->

The Managed Apps report now provides details about Enterprise App Catalog apps for a specific device. For more information about this report, see [Managed Apps report](../fundamentals/reports.md#managed-apps-report-operational).

### Device configuration

#### New settings available in the Apple settings catalog <!--27175914 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Restrictions**:

- Allow Web Distribution App Installation

**System Configuration > Font**:

- Font
- Name

##### macOS

**Privacy > Privacy Preferences Policy Control**:

- Bluetooth Always

Applies to:

- iOS/iPadOS
- macOS

#### OS Version picker available for configuring managed iOS/iPadOS DDM software updates using the settings catalog<!-- 27565292 -->

Using the [Intune settings catalog](../configuration/settings-catalog.md), you can configure Apple's declarative device management (DDM) feature to manage software updates on iOS/iPadOS devices.

When you configure a managed software update policy using the settings catalog, you can:

- Select a target OS version from a list of updates made available by Apple.
- Manually enter the target OS version, if needed.

For more information about configuring managed software update profiles in Intune, see [Use the settings catalog to configure managed software updates](../protect/updates/apple.md).

Applies to:

- iOS/iPadOS

#### Intune admin center UI updates at Devices > By platform<!-- 25104008 -->

In the Intune admin center, you can select **Devices** > **By platform**, and view the policy options for the platform you select. These platform-specific pages are updated and include tabs for navigation.

For a walkthrough of the Intune admin center, see [Tutorial: Walkthrough Microsoft Intune admin center](tutorial-walkthrough-endpoint-manager.md).

### Device enrollment

### RBAC changes to enrollment platform restrictions for Windows<!-- 25036419 -->

We've updated role-based access controls (RBAC) for all enrollment platform restrictions in the Microsoft Intune admin center. The Intune Service Administrator roles can create, edit, delete, and reprioritize enrollment platform restrictions. For all other built-in Intune roles, restrictions are read-only.

**Applies to:**

- Android
- Apple
- Windows

It's important to know that with these changes:

- Scope tag behavior doesn't change. You can apply and use scope tags as usual.
- If an assigned role or permission is currently preventing a user from viewing enrollment platform restrictions, nothing changes. The user will still be unable to view enrollment platform restrictions in the admin center.

For more information, see [Create device platform restrictions](../enrollment/create-device-platform-restrictions.md).

### Device management

### Updates to replace Wandera with Jamf is complete in the Intune admin center<!-- 26525211 -->

We've completed a rebrand in the Microsoft Intune admin center to support replacing Wandera with Jamf. This includes updates to the name of the Mobile Threat Defense connector, which is now *Jamf*, and changes to the minimum required platforms to use the Jamf connector:

- Android 11 and later
- iOS / iPadOS 15.6 and later

For information about Jamf and other Mobile Threat Defense (MTD) vendors that Intune supports, see [Mobile Threat Defense partners](../protect/mobile-threat-defense.md).

### Intune apps

#### Newly available protected apps for Intune<!-- 28033401, 28035558, 27795962, 27795905, 27831146, 27795905 -->

The following protected apps are now available for Microsoft Intune:

- Atom Edge (iOS) by Arlanto GmbH
- HP Advance for Intune by HP Inc.
- IntraActive by Fellowmind
- Microsoft Azure (Android) by Microsoft Corporation
- Mobile Helix Link for Intune by Mobile Helix
- VPSX Print for Intune by Levi, Ray & Shoup, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md)

### Monitor and troubleshoot

#### View BitLocker recovery key in Company Portal apps for iOS and macOS<!-- 26615990 -->

End users can view the BitLocker recovery key for an enrolled Windows device and the FileVault recovery key for an enrolled Mac in the Company Portal app for iOS and Company Portal app for macOS. This capability will reduce helpdesk calls in the event the end user gets locked out of their corporate machines. End users can access the recovery key for an enrolled device by signing into the Company Portal app and selecting **Get recovery key**. This experience is similar to the recovery process on the Company Portal website, which also allows end users to see recovery keys.

You can prevent end users within your organization from accessing BitLocker recovery keys by configuring the **Restrict non-admin users from recovering the BitLocker keys for their owned device** setting in Microsoft Entra ID.

Applies to:

- macOS
- Windows

For more information, see:

- [Manage BitLocker policy for Windows devices with Intune](../protect/encrypt-devices.md)
- [Get recovery key for Windows](../user-help/get-recovery-key-windows.md)
- [Use FileVault disk encryption for macOS with Intune](../protect/encrypt-devices-filevault.md)
- [Get recovery key for Mac](../user-help/get-recovery-key-cpweb.md)
- [Manage device identities using the Microsoft Entra admin center](/entra/identity/devices/manage-device-identities#configure-device-settings)

### Role-based access control

#### New granular RBAC controls for Intune endpoint security<!-- 5475572 -->

We've begun to replace the role-based access control (RBAC) rights to endpoint security policies that are granted by the *Security baselines* permission with a series of more granular permissions for specific endpoint security tasks. This change can help you assign the specific rights your Intune admins require to do specific jobs instead of relying on either the [built-in](../fundamentals/role-based-access-control.md#built-in-roles) *Endpoint Security Manager* role or a [custom role](../fundamentals/create-custom-role.md) that includes the *Security baseline* permission. Prior to this change, the *Security baseline* permission grants rights across all endpoint security policies.

The following new RBAC permissions are available for endpoint security workloads:

- App Control for Business
- Attack surface reduction
- Endpoint detection and response

Each new permission supports the following rights for the related policy:

- Assign
- Create
- Delete
- Read
- Update
- View Reports

Each time we add a new granular permission for an endpoint security policy to Intune, those same rights are removed from the *Security baselines* permission. If you use custom roles with the *Security baselines* permission, the new RBAC permission is assigned automatically to your custom roles with the same rights that were granted through the *Security baseline* permission. This autoassignment ensures your admins continue to have the same permissions they have today.

For more information about current RBAC permissions and built-in roles, see:

- [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md)
- [Built-in role permissions for Microsoft Intune](../fundamentals/role-based-access-control-reference.md)
- [Assign role-based access controls for endpoint security policy](../protect/endpoint-security-policy.md#assign-role-based-access-controls-for-endpoint-security-policy) in *Manage device security with endpoint security policies in Microsoft Intune*.

> [!IMPORTANT]
>
> With this release, the granular permission of **Antivirus** for endpoint security policies might be temporarily visible in some Tenants. This permission is not released and isn't supported for use. Configurations of the *Antivirus* permission are ignored by Intune. When *Antivirus* becomes available to use as a granular permission, it's availability will be announced in this [What's new in Microsoft Intune](../fundamentals/whats-new.md) article.

## Week of June 3, 2024

### Device enrollment

#### New enrollment time grouping feature for devices <!-- 16902437 -->

Enrollment time grouping is a new, faster way to group devices during enrollment. When configured, Intune adds devices to the appropriate group without requiring inventory discovery and dynamic membership evaluations. To set up enrollment time grouping, you must configure a static Microsoft Entra security group in each enrollment profile. After a device enrolls, Intune adds it to the static security group and delivers assigned apps and policies.

This feature is available for Windows 11 devices enrolling via Windows Autopilot device preparation. For more information, see [Enrollment time grouping in Microsoft Intune](../enrollment/enrollment-time-grouping.md).

## Week of May 27, 2024

### Microsoft Intune Suite

#### New primary endpoint for Remote Help

To improve the experience for [Remote Help](../fundamentals/remote-help.md) on Windows, Web, and macOS devices, we have updated the primary endpoint for Remote Help:

- Old primary endpoint: `https://remoteassistance.support.services.microsoft.com`
- New primary endpoint: `https://remotehelp.microsoft.com`

If you use Remote Help and have firewall rules that block the new primary endpoint, admins and users might experience connectivity issues or disruptions when using Remove Help.

To support the new primary endpoint on Windows devices, upgrade Remote Help to version 5.1.124.0. Web and macOS devices don't require an updated version of Remote Help to make use of the new primary endpoint.

Applies to:

- macOS 11, 12, 13 and 14
- Windows
- Windows 11 on ARM64 devices
- Windows 10 on ARM64 devices
- Windows 365

For information on the newest version of Remote Help, see [Week of March 13, 2024](#week-of-march-13-2024). For information about Intune endpoints for Remote Help, see [Remote Help](../fundamentals/intune-endpoints.md#remote-help) in *Network endpoints for Microsoft Intune*.

### Device management

### Evaluate compliance of Windows Subsystem for Linux (public preview)<!-- 24557103 -->

Now in a public preview, Microsoft Intune supports compliance checks for instances of Windows Subsystem for Linux (WSL) running on a Windows host device.

With this preview you can create a custom compliance script that evaluates the required distribution and version of WSL. WSL compliance results are included in the overall compliance state of the host device.

Applies to:

- Windows 10
- Windows 11

For information about this capability, see [Evaluate compliance of Windows Subsystem for Linux (public preview)](../protect/compliance-wsl.md).

## Week of May 20, 2024 (Service release 2405)

### Device configuration

#### New settings available in the macOS settings catalog<!-- 26970197 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the macOS Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

**Microsoft AutoUpdate (MAU)**:

- Microsoft Teams (work or school)
- Microsoft Teams classic

**Microsoft Defender > Features**:

- Use Data Loss Prevention
- Use System Extensions

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:

- macOS

### Device enrollment

#### Stage Android device enrollment to reduce end-user steps<!-- 15503468 -->

To reduce the enrollment time for end users, Microsoft Intune supports device staging for Android Enterprise devices. With *device staging*, you can stage an enrollment profile and complete all related enrollment steps for workers receiving these devices:

- Corporate-owned fully managed devices
- Corporate-owned devices with a work profile

When frontline workers receive the devices, all they have to do is connect to Wi-Fi and sign in to their work account. A new *device staging token* is required to enable this feature. For more information, see [Device staging overview](../enrollment/device-staging-overview.md).

### Device management

#### End user access to BitLocker Recovery Keys for enrolled Windows devices<!-- 8077173 -->

End users can now view the BitLocker Recovery Key for enrolled Windows devices from the Company Portal website. This capability can reduce helpdesk calls in the event the end user gets locked out of their corporate machines. End users can access the recovery key for an enrolled device by signing into the Company Portal website and selecting **Show recovery key**. This experience is similar to the MyAccount website, which also allows end users to see recovery keys.

You can prevent end users within your organization from accessing BitLocker recovery keys by configuring the Microsoft Entra toggle **Restrict non-admin users from recovering the BitLocker key(s) for their owned device**.

For more information, see:

- [Manage device identities using the Microsoft Entra admin center](/entra/identity/devices/manage-device-identities#configure-device-settings)
- [Get recovery key for Windows](../user-help/get-recovery-key-windows.md)
- [Manage BitLocker policy for Windows devices with Intune](../protect/encrypt-devices.md)

#### New version of Windows hardware attestation report<!-- 15425680 -->

We've released a new version of the Windows hardware attestation report that shows the value of settings attested by Device Health Attestation and Microsoft Azure Attestation for Windows. The Windows hardware attestation report is built on a new reporting infrastructure, and reports on new settings added to Microsoft Azure Attestation. The report is available in the admin center under **Reports** > **Device Compliance** > **Reports**.

For more information, see [Intune reports](reports.md#windows-hardware-attestation-report-organizational).

The Windows health attestation report previously available under **Devices** > **Monitor** has been retired.

Applies to:

- Windows 10
- Windows 11

#### Optional Feature updates<!--12769586 -->

Feature updates can now be made available to end users as **Optional** updates, with the introduction of **Optional** Feature updates. End users see the update in the **Windows Update** settings page in the same way that it's shown for consumer devices.

End users can easily opt in to try out the next Feature update and provide feedback. When it's time to roll out the feature as a **Required** update, admins can change the setting on the policy and update the rollout settings so that the update is deployed as a **Required** update to devices that don't yet have it installed.

For more information on Optional Feature updates, see [Feature updates for Windows 10 and later policy in Intune](..//protect/windows-10-feature-updates.md#create-and-assign-feature-updates-for-windows-10-and-later-policy).

Applies to:

- Windows 10
- Windows 11

### Device security

#### Updated security baseline for Microsoft Defender for Endpoint<!-- 26504935 -->

You can now deploy the Intune security baseline for **Microsoft Defender for Endpoint**. The new baseline, **version 24H1**, uses the unified settings platform seen in the Settings Catalog, which features an improved user interface and reporting experience, consistency and accuracy improvements with setting tattooing, and the new ability to support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you maintain best-practice configurations for your Windows devices and can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft.

As with all baselines, the default baseline represents the recommended configurations for each setting, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

### Intune apps

#### Newly available protected apps for Intune<!-- 27575008, 27575336 -->

The following protected apps are now available for Microsoft Intune:

- Fellow.app by Fellow Insights Inc
- Unique Moments by Unique AG

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of May 6, 2024

### Device management

#### Intune and the macOS Company Portal app support Platform SSO (public preview)<!-- 24325427 -->

On Apple devices, you can use Microsoft Intune and the Microsoft Enterprise SSO plug-in to configure single sign-on (SSO) for apps and websites that support Microsoft Entra authentication, including Microsoft 365.

On macOS devices, Platform SSO is available in public preview. Platform SSO expands the SSO app extension by allowing you to configure different authentication methods, simplify the sign-in process for users, and reduce the number of passwords they need to remember.

Platform SSO is included in the Company Portal app version 5.2404.0 and newer.

For more information on Platform SSO and to get started, see:

- [Configure Platform SSO for macOS devices in Microsoft Intune](../configuration/platform-sso-macos.md)
- [Single sign-on (SSO) overview and options for Apple devices in Microsoft Intune](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)

Applies to:

- macOS 13 and later

### Tenant administration

#### Customize your Intune admin center experience<!-- 24155584 -->

You can now customize your Intune admin center experience by using collapsible navigation and favorites. The left navigation menus in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) are updated to support expanding and collapsing each subsection of the menu. In addition, you can set admin center pages as favorites. This portal capability will gradually roll out over the next week.

By default, menu sections are expanded. You can choose your portal menu behavior by selecting the **Settings** gear icon at the top right to display the **Portal settings**. Then, select **Appearance + startup views** and set the **Service menu behavior** to **Collapsed** or **Expanded** as the default portal option. Each menu section retains the expanded or collapsed state that you choose. Additionally, selecting the star icon next to a page on the left navigation adds the page to a **Favorites** section near the top of the menu.

For related information, see [Change the Portal settings](../fundamentals/tutorial-walkthrough-endpoint-manager.md#change-the-portal-settings).

## Week of April 29, 2024

### App management

#### Updates to the Managed Home Screen experience<!-- 24990268 -->

We recently released and improved the Managed Home Screen experience, which is now Generally Available. The app is redesigned to improve the core workflows throughout the application. The updated design offers a more usable and supportable experience.

With the release, we stop investing in previous Managed Home Screen workflows. New features and fixes for Managed Home Screen are only added to the new experience. During August 2024, the new experience is automatically enabled for all devices.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md) and [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

#### Require end users to enter PIN to resume activity on Managed Home Screen<!-- 9322838 -->

In Intune, you can require end users to enter their session PIN to resume activity on Managed Home Screen after the device is inactive for a specified period of time. Set the **Minimum inactive time before session PIN is required** setting to the number of seconds the device is inactive before the end user must input their session PIN.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Device IPv4 and IPv6 details available from Managed Home Screen<!-- 25994445 -->

IPv4 and IPv6 connectivity details are now both available from the **Device Information** page of the Managed Home Screen app. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](..\remote-actions\collect-diagnostics.md).

#### Updates to Managed Home Screen sign-in support<!-- 25597636 -->

Managed Home Screen now supports domainless sign-in. Admins can configure a domain name, which will be automatically appended to usernames upon sign-in. Also, Managed Home Screen supports a custom login hint text to be displayed to users during the sign-in process.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md) and [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

#### Allow end users to control Android Enterprise device auto-rotation<!-- 9322838 -->

In Intune, you can now expose a setting in the Managed Home Screen app that allows the end user to turn on and off the device's auto-rotation. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Allow end users to adjust Android Enterprise device screen brightness<!-- 9322834 -->

In Intune, you can expose settings in the Managed Home Screen app to adjust screen brightness for Android Enterprise devices. You can choose to expose a setting in the app to allow end users to access a brightness slider to adjust the device screen brightness. Also, you can expose a setting to allow end users to toggle adaptive brightness.

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Migrated to .NET MAUI from Xamarin<!-- 27143739 -->

Xamarin.Forms has evolved into .NET Multi-platform App UI (MAUI). Existing Xamarin projects should be migrated to .NET MAUI. For more information about upgrading Xamarin projects to .NET, see the [Upgrade from Xamarin to .NET & .NET MAUI](/dotnet/maui/migration/?WT.mc_id=dotnet-35129-website) documentation.

Xamarin support ended as of May 1, 2024 for all Xamarin SDKs including Xamarin.Forms and Intune App SDK Xamarin Bindings. For Intune support on Android and iOS platforms, see [Intune App SDK for .NET MAUI - Android](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android)and [Microsoft Intune App SDK for MAUI.iOS](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS).

## Week of April 22, 2024 (Service release 2404)

### App management

#### Auto update available with Win32 app supersedence<!-- 17644510 -->

Win32 app supersedence provides the capability to supersede apps deployed as available with **auto-update** intent. For example, if you deploy a Win32 app (app A) as available and installed by users on their device, you can create a new Win32 app (app B) to supersede app A using **auto-update**. All targeted devices and users with app A installed as available from the Company Portal are superseded with app B. Also, only app B shows in the Company Portal. You can find the **auto-update** feature for available app supersedence as a toggle under the **Available assignment** in the **Assignments** tab.

For more information about app supersedence, see [Add Win32 app supersedence](../apps/apps-win32-supersedence.md).

### Device configuration

#### Error message is shown when OEMConfig policy exceeds 500 KB on Android Enterprise devices<!-- 15326924 -->

On Android Enterprise devices, you can use an OEMConfig device configuration profile to add, create and/or customize OEM specific settings.

When you create an OEMConfig policy that exceeds 500 KB, then the following error is shown in the Intune admin center:

`Profile is larger than 500KB. Adjust profile settings to decrease the size.`

Previously, OEMConfig policies that exceeded 500 KB were shown as pending.

For more information on OEMConfig profiles, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Applies to:

- Android Enterprise

### Device security

#### Windows Firewall CSP changes for processing Firewall Rules<!-- 10734904 -->

Windows changed how the Firewall configuration service provider (CSP) enforces rules from Atomic blocks of firewall rules. The Windows Firewall CSP on a device implements the firewall rule settings from your [Intune endpoint security Firewall policies](../protect/endpoint-security-firewall-policy.md). The change of CSP behavior now enforces an all-or-nothing application of firewall rules from each Atomic block of rules.

- Previously, the CSP on a device would go through the firewall rules in an Atomic block of rules - one rule (or setting) at a time with the goal of applying all the rules in that Atomic block, or none of them. If the CSP encountered any issue with applying any rule from the block to the device, the CSP wouldn't only stop that rule, but also cease to process subsequent rules without trying to apply them. However, rules that applied successfully before a rule failed, would remain applied to the device. This behavior can lead to a partial deployment of firewall rules on a device, since the rules that were applied before a rule failed to apply aren't reversed.

- With the change to the Firewall CSP, when any rule in the block is unsuccessful in applying to the device, all the rules from that same Atomic block that were applied successfully are rolled back. This behavior ensures the desired all-or-nothing behavior is implemented and prevents a partial deployment of firewall rules from that block. For example, if a device receives an Atomic block of firewall rules that has a misconfigured rule that can't apply, or has a rule that isn't compatible with the devices operating system, then the CSP fails all the rules from that block, And, it rolls back any rules that applied to that device.

This change of Firewall CSP behavior is available on devices that run the following Windows versions or later:

- Windows 11 21H2
- Windows 11 22H2
- Windows 10 21H2

For more information on the subject of how the Windows Firewall CSP uses Atomic blocks to contain firewall rules, see the note near the top of [Firewall CSP](/windows/client-management/mdm/firewall-csp) in the Windows documentation.

For troubleshooting guidance, see the Intune support blog [How to trace and troubleshoot the Intune Endpoint Security Firewall rule creation process](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-trace-and-troubleshoot-the-intune-endpoint-security/ba-p/3261452).

#### CrowdStrike – New mobile threat defense partner<!-- 16882021 -->

We added [CrowdStrike Falcon](../protect/crowdstrike-falcon-defense-connector.md) as an integrated Mobile Threat Defense (MTD) partner with Intune. By configuring the CrowdStrike connector in Intune, you can control mobile device access to corporate resources using Conditional Access that's based on risk assessment in your compliance policies.

With the Intune 2404 service release, the CrowdStrike connector is now available in the admin center. However, it isn't useable until CrowdStrike publishes the required App Configuration profile details necessary to support iOS and Android devices. The profile details are expected sometime after second week of May.

### Intune apps

#### Newly available protected apps for Intune<!-- 26825160, 26954999, 26891466, 27184602 -->

The following protected apps are now available for Microsoft Intune:

- Asana: Work in one place by Asana, Inc.
- Freshservice for Intune by Freshworks, Inc.
- Kofax Power PDF Mobile by Tungsten Automation Corporation
- Remote Desktop by Microsoft Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Windows update distribution report<!--16579592 -->

The Windows update distribution report in Intune provides a summarized report. This report shows:

- The number of devices that are on each quality update level.
- The percentage of coverage for each update across Intune managed devices, including co-managed devices.

You can drill down further in the report for each quality update that aggregates devices based on the Windows feature version and the update statuses.

Finally, the admins can get the list of devices that aggregate to the numbers shown in the previous two reports, which can also be exported and used for troubleshooting and analysis along with the Windows Update for business reports.

For more information on Windows update distribution reports, see [Windows Update reports on Intune](../protect/windows-update-reports.md#windows-update-distribution-report).

Applies to:

- Windows 10
- Windows 11

#### Intune support of Microsoft 365 remote application diagnostics<!-- 17409991 -->

The Microsoft 365 remote application diagnostics allows Intune admins to request Intune app protection logs and Microsoft 365 application logs (where applicable) directly from the Intune console. You can find this report in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Troubleshoot** > *select a user* > **Summary** > *App protection**. This feature is exclusive to applications that are under Intune app protection management. If supported, the application specific logs are gathered and stored within dedicated storage solutions for each application.

For more information, see [Collect diagnostics from an Intune managed device](../remote-actions/collect-diagnostics.md).

#### Remote Help supports full control of a macOS device<!--22985205 -->

Remote Help now supports helpdesk connecting to a user's device and requesting full control of the macOS device.

For more information, see:

- [Remote Help on macOS](../fundamentals/remote-help-macos.md)
- [Remote Help Web App](../fundamentals/remote-help-webapp.md)

Applies to:

- macOS 12, 13 and 14

## Week of April 15, 2024

### Intune apps

#### Newly available protected app for Intune<!-- 26740168 -->

The following protected app is now available for Microsoft Intune:

- Atom Edge by Arlanto Apps

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of April 1, 2024

### Device management

#### Copilot in Intune is available in the Intune admin center (public preview)<!-- 24105429 26122887 24205474 24205510 24205460 26113632-->

Copilot in Intune is integrated in the Intune admin center, and can help you get information quickly. You can use Copilot in Intune for the following tasks:

✅ **Copilot can help you manage your settings and policies**

- **Copilot tooltip on settings**: When you add settings to a policy or review settings in an existing policy, there's a new Copilot tooltip. When you select the tooltip, you get AI generated guidance based on Microsoft content and recommendations. You can see what each setting does, how the setting works, any recommended values, if the setting is configured in another policy, and more.

- **Policy summarizer**: On existing policies, you get a Copilot summary of the policy. The summary describes what the policy does, the users and groups assigned to the policy, and the settings in the policy. This feature can help you understand the impact of a policy and its settings on your users and devices.

✅ **Copilot shows device details and can help troubleshoot**

- **All about a device**: On a device, you can use Copilot to get key information about the device, including its properties, configuration, and status information.

- **Device compare**: Use Copilot to compare the hardware properties and device configurations of two devices. This feature helps you determine what's different between two devices with similar configurations, especially when troubleshooting.

- **Error code analyzer**: Use Copilot in the device view to analyze an error code. This feature helps you understand what the error means and provides a potential resolution.

✅ **Intune capabilities in Copilot for Security**

Intune has capabilities available in the Copilot for Security portal. SOC Analysts and IT admins can use these capabilities to get more information on policies, devices, group membership, and more. On a single device, you can get more specific information that's unique to Intune, like compliance status, device type, and more.

You can also ask Copilot to tell you about a user's devices and get a quick summary of critical information. For example, the output shows links to the user's devices in Intune, device ID, enrollment date, last check-in date, and compliance status. If you're an IT admin and reviewing a user, then this data provides a quick summary.

As a SOC analyst that's investigating a suspicious or potentially compromised user or device, information like enrollment date and last check-in can help you make informed decisions.

For more information on these features, see:

- [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md)
- [Access your Microsoft Intune data in Copilot for Security](../copilot/security-copilot.md)

Applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

#### GCC customers can use Remote Help for Windows and Android devices<!-- 10613615 25825071-->

The [Microsoft Intune Suite](intune-add-ons.md) includes advanced endpoint management and security features, including Remote Help.

On Windows and enrolled Android Enterprise dedicated devices, you can use remote help on US Government GCC environments.

For more information on these features, see:

- [Microsoft Intune for US Government GCC service description](intune-govt-service-description.md)
- [Use Remote Help with Microsoft Intune](remote-help.md)

Applies to:

- Windows
- Windows on ARM64 devices
- Windows 365
- Samsung and Zebra devices enrolled as Android Enterprise dedicated devices

### Device configuration

#### New BIOS device configuration profile for OEMs<!-- 9278502 -->

There's a new **BIOS configuration and other settings** device configuration policy for OEMs. Admins can use this new policy to enable or disable different BIOS features that secure device. In the Intune device configuration policy, you add the BIOS configuration file, deploy a Win32 app, and then assign the policy to your devices.

For example, admins can use the [Dell Command tool](https://www.dell.com/support/kbdoc/000108963/how-to-use-and-troubleshoot-dell-command-update-to-update-all-drivers-bios-and-firmware-for-your-system) (opens Dell's website) to create the BIOS configuration file. Then, they add this file to the new Intune policy.

For more information on this feature, see [Use BIOS configuration profiles on Windows devices in Microsoft Intune](../configuration/bios-configuration.md).

Applies to

- Windows 10 and later

## Week of March 25, 2024 (Service release 2403)

### Microsoft Intune Suite

#### New elevation type for Endpoint Privilege Management<!-- 25230692 -->

Endpoint Privilege Management has a new file elevation type, **support approved**. Endpoint Privilege Management is a feature component of the Microsoft Intune Suite and is also available as a standalone [Intune add-on](../fundamentals/intune-add-ons.md).

A support-approved elevation gives you a third option for both the default elevation response and the elevation type for each rule. Unlike automatic or user confirmed, a support-approved elevation request requires Intune administrators to manage which files can run as elevated on a case-by-case basis.

With support approved elevations, users can request approval to elevate an application that isn't explicitly allowed for elevation by automatic or user approved rules. This takes the form of an elevation request that must be reviewed by an Intune administrator who can approve or deny the elevation request.

When the request is approved, users are notified that the application can now be run as elevated, and they have 24 hours from the time of approval to do so before the elevation approval expires.

Applies to:

- Windows 10
- Windows 11

For more information on this new capability, see [Support approved elevation requests](../protect/epm-support-approved.md).

### App management

#### Extended capabilities for Managed Google Play apps on personally owned Android devices with a work profile<!-- 26554642 -->

There are new capabilities extended to work profile devices. The following capabilities were previously available only on corporate-owned devices:

- **Available apps for device groups**: You can use Intune to make apps available for device groups through the Managed Google Play store. Previously, apps could only be made available to user groups.

- **Update priority setting**: You can use Intune to configure the app update priority on devices with a work profile. To learn more about this setting, see [Update a Managed Google Play app](../apps/apps-add-android-for-work.md#update-a-managed-google-play-app).

- **Required apps display as available in Managed Google Play**: You can use Intune to make required apps available for users through the Managed Google Play store. Apps that are part of existing policies now display as available.

These new capabilities will follow a phased rollout over multiple months.

Applies to:

- Android Enterprise personally owned devices with a work profile

### Device configuration

#### New settings available in the Apple settings catalog<!-- 26551582 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Declarative Device Management (DDM) > Passcode**:

- Maximum Passcode Age In Days
- Minimum Complex Characters
- Require Alphanumeric Passcode

**Restrictions**:

- Allow Marketplace App Installation

##### macOS

**Declarative Device Management (DDM) > Passcode**:

- Change At Next Auth
- Custom Regex
- Failed Attempts Reset In Minutes
- Maximum Passcode Age In Days
- Minimum Complex Characters
- Require Alphanumeric Passcode

**Full Disk Encryption > FileVault**:

- Recovery Key Rotation In Months

#### New settings available in the Windows settings catalog<!-- 26763724, 26170998, + 26801723 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type.

- **Delivery optimization**:

  - **DO Disallow Cache Server Downloads On VPN** - This setting blocks downloads from Microsoft Connected Cache servers when the device connects using VPN. By default, the device is allowed to download from Microsoft Connected Cache when connected using VPN.

  - **DO Set Hours To Limit Background Download Bandwidth** - This setting specifies the maximum background download bandwidth. Delivery Optimization uses this bandwidth during and outside business hours across all concurrent download activities as a percentage of available download bandwidth.

  - **DO Set Hours To Limit Foreground Download Bandwidth** - This setting specifies the maximum foreground download bandwidth. Delivery Optimization uses this bandwidth during and outside business hours across all concurrent download activities as a percentage of available download bandwidth.

  - **DO Vpn Keywords** - This policy allows you to set one or more keywords used to recognize VPN connections.

- **Messaging**:

  - **Allow Message Sync** - This policy setting allows the backup and restore of cellular text messages to Microsoft's cloud services.

- **Microsoft Defender Antivirus**:

  - **Specify the maximum depth to scan archive files**
  - **Specify the maximum size of archive files to be scanned**

For more information on these settings, see:

- [Policy CSP - DeliveryOptimization](/windows/client-management/mdm/policy-csp-deliveryoptimization)
- [Policy CSP - Messaging](/windows/client-management/mdm/policy-csp-messaging#allowmessagesync)
- [Policy CSP - ADMX_MicrosoftDefenderAntivirus](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus)

Applies to:

- Windows 10 and later

#### New archive file scan settings added to Antivirus policy for Windows devices<!-- 26801723 -->

We added the following two settings to the *Microsoft Defender Antivirus* profile for [endpoint security Antivirus policy](../protect/endpoint-security-antivirus-policy.md#antivirus-profiles) that apply to Windows 10 and Windows 11 devices:

- [Specify the maximum depth to scan archive files](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#scan_archivemaxdepth) - This setting allows you to configure the maximum directory depth level into which archive files such as .ZIP or .CAB are unpacked during scanning.
- [Specify the maximum size of archive files to be scanned](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#scan_archivemaxsize) - This setting allows you to configure the maximum size of archive files such as .ZIP or .CAB that are scanned. The value represents file size in kilobytes (KB).

With Antivirus policy, you can manage these settings on devices enrolled by Intune and on devices managed through the [Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario.

Both settings are also available in the [settings catalog](../configuration/settings-catalog.md) at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type > **Defender**.

Applies to:

- Windows 10
- Windows 11

#### Updates to assignment filters<!-- 12798031, 24801139 -->

You can use [Intune assignment filters](filters.md) to assign a policy based on rules you create.

Now, you can:

- Use managed app assignment filters for Window MAM app protection policies and app configuration policies.
- Filter your existing assignment filters by **Platform**, and by the **Managed apps** or **Managed devices** filter type. When you have many filters, this feature makes it easier to find specific filters you created.

For more information on these features, see:

- [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md)
- [Data protection for Windows MAM](../apps/protect-mam-windows.md)

This feature applies to:

- **Managed devices** on the following platforms:

  - Android device administrator
  - Android Enterprise
  - Android (AOSP)
  - iOS/iPadOS
  - macOS
  - Windows

- **Managed apps** on the following platforms:

  - Android
  - iOS/iPadOS
  - Windows

### Device management

#### New compliance setting lets you verify device integrity using hardware-backed security features<!-- 12391862 -->

A new compliance setting called **Check strong integrity using hardware-backed security features** lets you verify device integrity using hardware-backed key attestation. If you configure this setting, strong integrity attestation is added to Google Play's integrity verdict evaluation. Devices must meet device integrity to remain compliant. Microsoft Intune marks devices that don't support this type of integrity check as noncompliant.

This setting is available in profiles for Android Enterprise fully managed, dedicated, and corporate-owned work profile, under **Device Health** > **Google Play Protect**. It only becomes available when the Play integrity verdict policy in your profile is set to **Check basic integrity** or **Check basic integrity & device integrity**.

Applies to:

- Android Enterprise

For more information, see [Device compliance - Google Play Protect](../protect/compliance-policy-create-android-for-work.md#google-play-protect).

#### New compliance settings for Android work profile, personal devices<!-- 24743927 -->

Now you can add compliance requirements for work profile passwords without impacting device passwords. All new Microsoft Intune settings are available in compliance profiles for Android Enterprise personally owned work profiles under **System Security** > **Work Profile Security**, and include:

- Require a password to unlock work profile
- Number of days until password expires
- Number of previous passwords to prevent reuse
- Maximum minutes of inactivity before password is required
- Password complexity
- Required password type
- Minimum password length

If a work profile password fails to meet requirements, Company Portal marks the device as noncompliant. Intune compliance settings take precedence over the respective settings in an Intune device configuration profile. For example, the password complexity in your compliance profile is set to *medium*. The password complexity in a device configuration profile is set to *high*. Intune prioritizes and enforces the compliance policy.

Applies to:

- Android Enterprise personally owned devices with a work profile

For more information, see [Compliance settings - Android Enterprise](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile).

#### Windows quality updates support for expediting non-security updates<!-- 17614146 -->

Windows quality updates now support expediting non-security updates for those times when a quality fix needs to be deployed faster than the normal quality update settings.

Applies to:

- Windows 11 devices

For more information about installing an expedited update, see [Expedite Windows quality updates in Microsoft Intune](../protect/windows-10-expedite-updates.md#create-and-assign-an-expedited-quality-update).

#### Introducing a remote action to pause the config refresh enforcement interval<!--24249019 -->

In the Windows Settings Catalog, you can configure **Configuration Refresh**. This feature lets you set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check in to Intune. The device will replay and re-enforce settings based on previously received policy to minimize the chance for configuration drift.

To support this feature, a remote action is added to allow a pause in action. If an admin needs to make changes or run remediation on a device for troubleshooting or maintenance, they can issue a pause from Intune for a specified period. When the period expires, settings are enforced again.

The remote action **Pause configuration refresh** can be accessed from the device summary page.

For more information, see:

- [Remote actions](../remote-actions/index.md)
- [Pause Config Refresh Remote action](../remote-actions/pause-config-refresh.md)

### Device security

#### Updated security baseline for Windows version 23H2<!-- 25021947 -->

You can now deploy the Intune security baseline for Windows version 23H2. This new baseline is based on the **version 23H2** of the Group Policy security baseline found in the [Security Compliance Toolkit and Baselines](https://www.microsoft.com/en-us/download/details.aspx?id=55319) from the Microsoft Download Center, and includes only the settings that are applicable to devices managed through Intune. Use of this updated baseline can help you maintain best-practice configurations for your Windows devices.

This baseline uses the unified settings platform seen in the Settings Catalog. It features an improved user interface and reporting experience, consistency and accuracy improvements related to setting tattooing, and can support assignment filters for profiles.

Use of [Intune security baselines](../protect/security-baselines.md) can help you rapidly deploy configurations to your Windows devices that meet the security recommendations of the applicable security teams at Microsoft. As with all baselines, the default baseline represents the recommended configurations, which you can modify to meet the requirements of your organization.

Applies to:

- Windows 10
- Windows 11

To view the new baselines included settings with their default configurations, see, [Windows MDM security baseline version 23H2](../protect/security-baseline-settings-mdm-all.md?pivots=mdm-23h2).

#### Use a rootless implementation of Podman to host Microsoft Tunnel<!-- 24836716 -->

When prerequisites are met, you can use a rootless Podman container to host a Microsoft Tunnel server. This capability is available when you use [Podman for Red Hat Enterprise Linux (RHEL)](../protect/microsoft-tunnel-prerequisites.md#linux-server) version 8.8 or later, to host Microsoft Tunnel.

When using a rootless Podman container, the mstunnel services run under a non-privileged service user. This implementation can help limit impact from a container escape. To use a rootless Podman container, you must start the tunnel installation script using a modified command line.

For more information about this Microsoft Tunnel install option, see [Use a rootless Podman container](../protect/microsoft-tunnel-configure.md#use-a-rootless-podman-container).

#### Improvements for Intune deployments of Microsoft Defender for Endpoint<!-- 26314441 -->

We improved and simplified the experience, workflow, and report details for onboarding devices to Microsoft Defender when using Intune's endpoint detection and response (EDR) policy. These changes apply for Windows devices managed by Intune and by the tenant-attach scenario. These improvements include:

- Changes to the EDR node, dashboards, and reports to improve the visibility of your Defender EDR deployment numbers. See [About the endpoint detection and response node](../protect/endpoint-security-edr-policy.md#about-the-endpoint-detection-and-response-node).

- A new tenant-wide option to deploy a preconfigured EDR policy that streamlines the deployment of Defender for Endpoint to applicable Windows devices. See [Use a preconfigured EDR policy](../protect/endpoint-security-edr-policy.md#use-a-preconfigured-edr-policy).

- Changes to Intune's the Overview page of the endpoint security node. These changes provide a consolidated view of reports for the device signals from Defender for Endpoint on your managed devices. See [Use a preconfigured EDR policy](../protect/endpoint-security-edr-policy.md#use-a-preconfigured-edr-policy).

These changes apply to the Endpoint security and endpoint detection and response nodes of the admin center, and the following device platforms:

- Windows 10
- Windows 11

#### Windows quality updates support expediting non-security updates<!-- 17614146 -->

Windows quality updates now support expediting non-security updates for those times when a quality fix needs to be deployed faster than the normal quality update settings.

Applies to:

- Windows 11 devices

For more information about installing an expedited update, see [Expedite Windows quality updates in Microsoft Intune](../protect/windows-10-expedite-updates.md#create-and-assign-an-expedited-quality-update).

### Intune apps

#### Newly available protected apps for Intune<!-- 26677733, 26711918, 26763096, 26763121 -->

The following protected apps are now available for Microsoft Intune:

- Cerby by Cerby, Inc.
- OfficeMail Go by 9Folders, Inc.
- DealCloud by Intapp, Inc.
- Intapp 2.0 by Intapp, Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of March 13, 2024

### Microsoft Intune Suite

#### Remote Help

Version: 5.1.1214.0

- Changed the primary endpoint for Remote Help from https://remoteassistance.support.services.microsoft.com to https://remotehelp.microsoft.com.

  > [!NOTE]
  > This could cause a breaking change for some organizations that have not yet allowed remotehelp.microsoft.com through their firewall after 5/30/2024.

- Resolved various bugs including an issue with Conditional Access. If a tenant had a **Terms of Use** policy enabled for Office 365, Remote Help wouldn't know how to respond and would instead present an authentication error message to the user.
- Enabled a shortcut to open context menus with the keyboard shortcut 'Alt + Space'

## Week of March 3, 2024

### Device enrollment

#### Role-based access control changes to enrollment settings for Windows Hello for Business<!-- 25661866 -->

We updated Role-based access control (RBAC) in the enrollment area for Windows Hello for Business. Enrollment settings related to Windows Hello for Business are read-only for all roles except the Intune Service Administrator. The Intune Service Administrator can create and edit Windows Hello for Business enrollment settings.

For more information, see [Role-based access control](../protect/windows-hello.md#role-based-access-control) in the *Windows Hello at device enrollment* article.

### Device security

#### New enrollment configuration for Windows Hello for Business<!-- 9601416 -->

A new Windows Hello for Business enrollment setting, **Enable enhanced sign in security** is available in the Intune admin center. Enhanced sign-in security is a Windows Hello feature that prevents malicious users from gaining access to a user's biometrics through external peripherals.

For more information about this setting, see [Create a Windows Hello for Business policy](../protect/windows-hello.md).

#### HTML formatting supported in noncompliance email notifications<!-- 24197255 -->

Intune now supports HTML formatting in noncompliance email notifications for all platforms. You can use supported HTML tags to add formatting such as italics, URL links, and bulleted lists to your organization's messages.

For more information, see [Create a notification message template](../protect/actions-for-noncompliance.md#create-a-notification-message-template).

## Week of February 26, 2024

### Microsoft Intune Suite

#### New Microsoft Cloud PKI service<!-- 17272901 -->

Use the Microsoft Cloud PKI service to simplify and automate certificate lifecycle management for Intune-managed devices. ​Microsoft Cloud PKI is a feature component of the Microsoft Intune Suite and is also available as a standalone [Intune add-on](../fundamentals/intune-add-ons.md). The cloud-based service provides a dedicated PKI infrastructure for your organization, and doesn't require on-premises servers, connectors, or hardware. Microsoft Cloud PKI automatically issues, renews, and revokes certificates for all OS platforms supporting the SCEP certificate device configuration profile. Issued certificates can be used for certificate-based authentication for Wi-Fi, VPN, and other services supporting certificate-based authentication. For more information, see [Overview of Microsoft Cloud PKI](../protect/microsoft-cloud-pki-overview.md).

Applies to:

- Windows
- Android
- iOS/iPadOS
- macOS

### Intune apps

#### Newly available protected app for Intune<!-- 26607121 -->

The following protected app is now available for Microsoft Intune:

- Cinebody by Super 6 LLC

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of February 19, 2024 (Service release 2402)

### App management

#### More app configuration permissions for Android apps<!-- 25115278 -->

There are six new permissions that can be configured for an Android app using an app configuration policy. They are:

- Allow background body sensor data
- Media Video (read)
- Media Images (read)
- Media Audio (read)
- Nearby Wifi Devices
- Nearby Devices

For more information about how to use app config policies for Android apps, see [Add app configuration policies for managed Android Enterprise devices](../apps/app-configuration-policies-use-android.md).

#### Newly available protected apps for Intune<!-- 26607067, 26607087, 26632132 -->

The following protected apps are now available for Microsoft Intune:

- Bob HR by Hi Bob Ltd
- ePRINTit SaaS by ePRINTit USA LLC
- Microsoft Copilot by Microsoft Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

#### Update to Intune Management Extension on Windows<!-- 26472055 -->

To support expanded functionality and bug fixes, use .NET Framework 4.7.2 or higher with the Intune Management Extension on Windows clients. If a Windows client continues to use an earlier version of the .NET Framework, the Intune Management Extension continues to function. The .NET Framework 4.7.2 is available from Windows Update as of July 10, 2018, which is included in Windows 10 1809 (RS5) and newer. Multiple versions of the .NET Framework can coexist on a device.

Applies to:

- Windows 10
- Windows 11

### Device configuration

#### Use assignment filters on Endpoint Privilege Management (EPM) policies<!-- 25230705 -->

You can use assignment filters to assign a policy based on rules you create. A filter allows you to narrow the assignment scope of a policy, like targeting devices with a specific OS version or a specific manufacturer.

You can use filters on Endpoint Privilege Management (EPM) policies.

For more information, see:

- [Use filters when assigning your apps, policies, and profiles in Intune](filters.md)
- [List of platforms, policies, and app types supported by filters in Intune](filters-supported-workloads.md)

Applies to:

- Windows 10
- Windows 11

#### New settings available in the Apple settings catalog<!-- 25280353 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

- **Restrictions**

  - Allow Live Voicemail
  - Force Classroom Unprompted Screen Observation
  - Force Preserve ESIM On Erase

##### macOS

- **Full Disk Encryption > FileVault** > Force Enable In Setup Assistant
- **Restrictions** > Force Classroom Unprompted Screen Observation

For more information, see:

- [Use FileVault disk encryption for macOS with Intune](../protect/encrypt-devices-filevault.md)
- [Create a policy using settings catalog](../configuration/settings-catalog.md)

#### Import up to 20 custom ADMX and ADML administrative templates<!-- 25780608 -->

You can import custom ADMX and ADML administrative templates in Microsoft Intune. Previously, you could import up to 10 files. Now, you can upload up to 20 files.

Applies to:

- Windows 10
- Windows 11

For more information on this feature, see [Import custom ADMX and ADML administrative templates into Microsoft Intune (public preview)](../configuration/administrative-templates-import-custom.md).

#### New setting for updating MAC address randomization on Android Enterprise devices<!-- 24259789 -->

There's a new **MAC address randomization** setting on Android Enterprise devices (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Wi-Fi** for profile type).

Starting with Android 10, when connecting to a network, devices present a randomized MAC address instead of the physical MAC address. Using randomized MAC addresses is recommended for privacy, as it's harder to track a device by its MAC address. However, randomized MAC addresses break functionality that relies on a static MAC address, including network access control (NAC).

Your options:

- **Use device default**: Intune doesn't change or update this setting. By default, when connecting to a network, devices present a randomized MAC address instead of the physical MAC address. Any updates made by the user to the setting persist.

- **Use randomized MAC**: Enables MAC address randomization on devices. When devices connect to a new network, devices present a randomized MAC address, instead of the physical MAC address. If the user changes this value on their device, it resets to **Use randomized MAC** on the next Intune sync.

- **Use device MAC**: Forces devices to present their actual Wi-Fi MAC address instead of a random MAC address. This setting allows devices to be tracked by their MAC address. Only use this value when necessary, such as for network access control (NAC) support. If the user changes this value on their device, it resets to **Use device MAC** on the next Intune sync.

Applies to:

- Android 13 and newer

For more information on the Wi-Fi settings you can configure, see [Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices in Microsoft Intune](../configuration/wi-fi-settings-android-enterprise.md).

#### Turn Off Copilot in Windows setting in the Windows settings catalog<!-- 26725574 -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There's a new setting in the Settings Catalog. To see this setting, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows** for platform > **Settings catalog** for profile type.

- **Windows AI > Turn Off Copilot in Windows (User)**

  - If you enable this policy setting, users can't use Copilot. The Copilot icon won't appear on the taskbar.
  - If you disable or don't configure this policy setting, users can use Copilot when it's available to them.

This setting uses the [Policy CSP - WindowsAI](/windows/client-management/mdm/policy-csp-windowsai).

For more information about configuring Settings Catalog policies in Intune, including user scope vs. device scope, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

Applies to:

- Windows 10 and later

#### Windows Autopilot self-deploying mode is now generally available<!-- 26780755 -->

Windows Autopilot self-deploying mode is now generally available and out of preview. Windows Autopilot self-deploying mode enables you to deploy Windows devices with little to no user interaction. Once the device connects to network, the device provisioning process starts automatically: the device joins Microsoft Entra ID, enrolls in Intune, and syncs all device-based configurations targeted to the device. Self-deploying mode ensures that the user can't access desktop until all device-based configuration is applied. The Enrollment Status Page (ESP) is displayed during OOBE so users can track the status of the deployment. For more information, see:

- [Windows Autopilot self-deploying mode](/autopilot/self-deploying)
- [Step by step tutorial for Windows Autopilot self-deploying mode in Intune](/autopilot/tutorial/self-deploying/self-deploying-workflow)

This information is also published in [Windows Autopilot: What's new](/autopilot/whats-new).

#### Windows Autopilot for pre-provisioned deployment is now generally available<!-- 26780755 -->

Windows Autopilot for pre-provisioned deployment is now generally available and out of preview. Windows Autopilot for pre-provisioned deployment is used by organizations that want to ensure devices are business-ready before the user accesses them. With pre-provisioning, admins, partners, or OEMs can access a technician flow from the Out-of-box experience (OOBE) and kick off device setup. Next, the device is sent to the user who completes provisioning in the user phase. Pre-provisioning delivers most the configuration in advance so the end user can get to the desktop faster. For more information, see:

- [Windows Autopilot for pre-provisioned deployment](/autopilot/pre-provision).
- [Step by step tutorial for Windows Autopilot for pre-provisioned deployment Microsoft Entra join in Intune](/autopilot/tutorial/pre-provisioning/azure-ad-join-workflow)
- [Step by step tutorial for Windows Autopilot for pre-provisioned deployment Microsoft Entra hybrid join in Intune](/autopilot/tutorial/pre-provisioning/hybrid-azure-ad-join-workflow).

This information is also published in [Windows Autopilot: What's new](/autopilot/whats-new).

### Device enrollment

#### ESP setting to install required apps during Windows Autopilot pre-provisioning<!-- 26583413 -->

The setting **Only fail selected blocking apps in technician phase** is now generally available to configure in Enrollment Status Page (ESP) profiles. This setting only appears in ESP profiles that have *blocking apps* selected.

For more information, see [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md#create-new-profile).

#### New local primary account configuration for macOS automated device enrollment<!-- 5877061 -->

Configure local primary account settings for Macs enrolling in Intune via Apple automated device enrollment. These settings, supported on devices running macOS 10.11 and later, are available in new and existing enrollment profiles under the new **Account Settings** tab. For this feature to work, the enrollment profile must be configured with user-device affinity and one of the following authentication methods:

- Setup Assistant with modern authentication
- Setup Assistant (legacy)

Applies to:

- macOS 10.11 and later

For more information about macOS account settings, see [Create an Apple enrollment profile in Intune](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile).

#### Await final configuration for macOS automated device enrollment now generally available<!-- 24973562 -->

Now generally available, *await final configuration* enables a locked experience at the end of Setup Assistant to ensure that critical device configuration policies are installed on devices. The locked experience works on devices targeted with new and existing enrollment profiles, enrolling via one of these authentication methods:

- Setup Assistant with modern authentication
- Setup Assistant (legacy)
- Without user device affinity

Applies to:

- macOS 10.11 and later

For information about how to enable await final configuration, see [Create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile).

### Device management

#### AOSP devices check for new tasks and notifications approximately every 15 minutes<!-- 8506468 -->

On devices enrolled with Android (AOSP) management, Intune attempts to check for new tasks and notifications approximately every 15 minutes. To use this feature, devices must be using the Intune app version 24.02.4 or newer.

Applies to:

- Android (AOSP)

For more information, see:

- [How to use Intune in environments without Google Mobile Services](../apps/manage-without-gms.md#some-tasks-can-be-delayed)
- [Policy refresh intervals in Intune](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals)

#### New device management experience for Government clouds in Microsoft Intune<!-- 17585897 23692982 -->

In government clouds, there's a new device management experience in the Intune admin center. The **Devices** area now has a more consistent UI, with more capable controls and an improved navigation structure so you can find what you need faster.

If you want to try the new experience before your tenant is updated, go to **Devices** > **Overview**, select the **Preview upcoming changes to Devices and provide feedback** notification banner, and select **Try it now**.

#### Bulk approval of drivers<!-- 14723288 -->

Bulk actions are now available for Windows Driver update policies. With bulk actions, multiple driver updates can be approved, paused, or declined at the same time, saving time and effort.

When you bulk approve drivers, the date for when the drivers become available to applicable devices can also be set, enabling drivers to be installed together.

Applies to:

- Windows 10
- Windows 11

For more information, see [Bulk driver updates](../protect/windows-driver-updates-policy.md#bulk-driver-updates).

#### App Control for Business policy limitation is resolved<!-- 19548950 -->

A previously documented limitation for App Control for Business policy (WDAC), that limited the number of active policies per device to 32, is resolved by Windows. The issue involves a potential [Boot stop failure when more than 32 policies are active](/windows/security/application-security/application-control/windows-defender-application-control/operations/known-issues#boot-stop-failure-blue-screen-occurs-if-more-than-32-policies-are-active) on a device.

This issue is resolved for devices that run Windows 10 1903 or later with a Windows security update released on or after March 12, 2024. Older versions of Windows can expect to receive this fix in future Windows security updates.

Applies to:

- Windows 10 version 1903 and later

To learn more about App Control for Business policy for Intune, see [Manage approved apps for Windows devices with App Control for Business policy and Managed Installers for Microsoft Intune](../protect/endpoint-security-app-control-policy.md).

### Tenant administration

#### Customization pane support for excluding groups<!-- 17654599 -->

The Customization pane now supports selecting groups to exclude when assigning policies. You can find this setting in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Tenant administration** > **Customization**.

For more information, see [Assign policies in Microsoft Intune](../configuration/device-profile-assign.md).

## Week of January 29, 2024

### Microsoft Intune Suite

#### Microsoft Intune Enterprise Application Management<!-- 10986080 -->

Enterprise Application Management provides an Enterprise App Catalog of Win32 applications that are easily accessible in Intune. You can add these applications to your tenant by selecting them from the Enterprise App Catalog. When you add an Enterprise App Catalog app to your Intune tenant, default installation, requirements, and detection settings are automatically provided. You can modify these settings as well. Intune hosts Enterprise App Catalog apps in Microsoft storage.

For more information, see:

- [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md)
- [Microsoft Intune Enterprise Application Management](../apps/apps-enterprise-app-management.md)
- [Add an Enterprise App Catalog app to Microsoft Intune](../apps/apps-add-enterprise-app.md)

#### Microsoft Intune Advanced Analytics<!--25194145 -->

Intune Advanced Analytics provides comprehensive visibility of the end-user experience in your organization and optimizes it with data driven insights. It includes near real-time data about your devices with Device query, increased visibility with custom device scopes, a battery health report and a detailed device timeline for troubleshooting device issues, and anomaly detection to help identify potential vulnerabilities or risks across your device estate.

- **Battery health report**<!-- 9747162 -->

  The battery health report provides visibility into the health of batteries in your organization's devices and its influence on user experience. The scores and insights in this report are aimed to help IT admins with asset management and purchase decisions that improve user experience while balancing hardware costs.

- **Run on-demand device queries on single devices**<!-- 16719466 -->

  Intune allows you to quickly gain on-demand information about the state of your device. When you enter a query on a selected device, Intune runs a query in real time.

  The data returned can then be used to respond to security threats, troubleshoot the device, or make business decisions.

  Applies to:

  - Windows devices

Intune Advanced Analytics is part of the Microsoft Intune Suite. For added flexibility, this new set of capabilities, together with the existing Advanced Analytics features, is also now available as an individual add-on to Microsoft subscriptions that include Intune.

To use Device query and battery health report in your tenant, or any of the existing Advanced Analytics capabilities, you must have a license for either:

- The Intune Advanced Analytics add-on
- The Microsoft Intune Suite add-on

For more information, see:

- [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md)
- [Microsoft Intune Advanced Analytics](../../analytics/advanced-endpoint-analytics.md)
- [Battery health](../../analytics/battery-health.md)
- [Device query](../../analytics/device-query.md)

## Week of January 22, 2024 (Service release 2401)

### App management

#### Install DMG and PKG apps up to 8 GB in size on managed Macs<!-- 25766031 -->

The size-limit of DMG and PKG apps that can be installed using Intune on managed Macs has been increased. The new limit is 8 GB and is applicable to apps (DMG and unmanaged PKG) that are installed using the Microsoft Intune management agent for macOS.

For more information about DMG and PKG apps, see [Add a macOS DMG app to Microsoft Intune](../apps/lob-apps-macos-dmg.md) and [Add an unmanaged macOS PKG app to Microsoft Intune](../apps/macos-unmanaged-pkg.md).

#### Intune support of store-signed LOB apps for Surface Hub devices<!-- 25865620 -->

Intune now supports the deployment of store-signed LOB apps (single file `.appx`, `.msix`, `.appxbundle`, and `.msixbundle`) to Surface Hub devices. The support for store-signed LOB apps enables offline store apps to be deployed to Surface Hub devices following the retirement of the Microsoft Store for Business.

#### Route SMS/MMS messages to specific app<!-- 24594466 -->

You can configure an app protection policy to determine which SMS/MMS app must be used when the end user intends to send a SMS/MMS message after getting redirected from a policy managed app. When the end user selects on a number with the intent of sending an SMS/MMS message, the app protection settings are used to redirect to the configured SMS/MMS app. This capability relates to the **Transfer messaging data to** setting and applies to both iOS/iPadOS and Android platforms.

For more information, see [iOS app protection policy settings](../apps/app-protection-policy-settings-ios.md) and [Android app protection policy settings](../apps/app-protection-policy-settings-android.md).

#### End user app PIN reset<!-- 24605159 -->

For managed apps that require a PIN to access, allowed end users can now reset the app PIN at any time. You can require an app PIN in Intune by selecting the **PIN for access** setting in iOS/iPadOS and Android app protection policies.

For more information about app protection policies, see [App protection policies overview](../apps/app-protection-policy.md).

#### Maximum app package size<!-- 17546826 -->

The maximum package size for uploading apps to Intune is changed from 8 GB to 30 GB for paid customers. Trial tenants are still restricted to 8 GB.

For more information, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md#prerequisites).

### Device configuration

#### New setting that disables location on Android Enterprise devices<!-- 21060837 -->

On Android Enterprise devices, there's a new setting that allows admins to control the location (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile > Device Restrictions** for profile type > **General**):

- **Location**: **Block** disables the **Location** setting on the device and prevents users from turning it on. When this setting is disabled, then any other setting that depends on the device location is affected, including the **Locate device** remote action. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow using location on the device.

Applies to:

- Android Enterprise

For more information on the settings you can configure, see [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune](../configuration/device-restrictions-android-for-work.md).

#### Date and time picker for managed software updates in the settings catalog on iOS/iPadOS and macOS devices<!-- 26015175 -->

Using the settings catalog, you can enforce managed updates on iOS/iPadOS and macOS devices by entering a date and time (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type > **Declarative Device Management > Software Update**).

Previously, you had to manually type the date and time. Now, there's a date and time picker for the **Target Local Date Time** setting:

**Declarative Device Management (DDM) > Software Update**:

- Target Local Date Time

> [!IMPORTANT]
> If you create a policy using this setting before the January 2024 release, then this setting shows `Invalid Date` for the value. The updates are still scheduled correctly and use the values you originally configured, even though it shows `Invalid Date`.
>
> To configure a new date and time, you can delete the `Invalid Date` values, and select a new date and time using the date time picker. Or, you can create a new policy.

Applies to:

- iOS/iPadOS
- macOS

For more information about configuring Managed software updates in Intune, see [Use the settings catalog to configure managed software updates](../protect/updates/apple.md).

### Device management

#### New device management experience in Microsoft Intune<!-- 17585897 23692982 -->

We're rolling out an update to the device management experience in the Intune admin center. The **Devices** area now has a more consistent UI, with more capable controls and an improved navigation structure so you can find what you need faster. The new experience, previously in public preview, will gradually roll out for general availability over the coming weeks. The public preview experience continues to be available until your tenant receives the update.

The availability of this new admin center experience varies tenant by tenant. While a few will see this update immediately, many might not see the new experience for several weeks. For Government clouds, the availability of this experience is estimated around late February 2024.

Due to the rollout timelines, we're updating our documentation to the new experience as soon as possible to help ease the transition to the new admin center layout. We're unable to provide a side-by-side content experience during this transition and believe providing documentation that aligns to the newer experience brings more value to more customers. If you want to try the new experience and align with doc procedures before your tenant is updated, go to **Devices** > **Overview**, select the notification banner that reads **Preview upcoming changes to Devices and provide feedback**, and select **Try it now**.

#### BlackBerry Protect Mobile now supports app protection policies<!-- 13357196  -->

You can now use Intune app protection policies with *BlackBerry Protect Mobile* (powered by Cylance AI). With this change, Intune supports BlackBerry Protect Mobile for mobile application management (MAM) scenarios for [unenrolled devices](../protect/mtd-add-apps-unenrolled-devices.md). This support includes the use of risk assessment with Conditional Access and configuration of Conditional Launch settings for unenrolled devices.

While configuring the CylancePROTECT Mobile connector (formerly BlackBerry Mobile), you now can select options to turn on *App protection policy evaluation* for both Android and iOS/iPadOS devices.

For more information, see [Set up BlackBerry Protect Mobile](../protect/blackberry-mobile-threat-defense-connector.md), and [Create Mobile Threat Defense app protection policy with Intune](../protect/mtd-app-protection-policy.md).

### Device security

#### Support for Intune Defender Update control policies for devices managed by Microsoft Defender for Endpoint<!--25470154 -->

You can now use the endpoint security policy for *Defender Update control* (Antivirus policy) from the Microsoft Intune admin center with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.

- **Defender Update control** policies are part of endpoint security [Antivirus policy](../protect/endpoint-security-antivirus-policy.md).

Applies to the following when you use the *Windows 10, Windows 11, and Windows Server* platform:

- Windows 10
- Windows 11

With this support available, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive the policy will get it.

### Intune apps

#### Newly available protected apps for Intune<!-- 25765585, 26137219 -->

The following protected apps are now available for Microsoft Intune:

- PrinterOn Print by PrinterOn, Inc. (iOS/iPadOS)
- Align for Intune by MFB Technologies, Inc. (iOS/iPadOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Monitoring reports for devices<!-- 17744651 -->

In Intune, you can view a new list of all device monitoring reports. You can find these reports in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Monitor**. The **Monitor** pane provides reports related to configuration, compliance, enrollment, and software updates. Additionally, there are other reports that you can view, such as **Device actions**.

For more information, see [Intune reports](reports.md).

#### Exported report data maintains search results<!-- 17723620 -->

Intune can now maintain your report search and filter results when exporting report data. For example, when you use the [Noncompliant devices and settings](reports.md#noncompliant-devices-report-organizational) report, set the OS filter to "Windows", and search for "PC", the exported data will only contain Windows devices with "PC" in their name. This capability is also available when calling the `ExportJobs` API directly.

#### Easy upload of diagnostic logs for Microsoft Tunnel servers<!-- 15728481 -->

You can now use a single click within the Intune admin center to have Intune enable, collect, and submit eight hours of verbose logs for a Tunnel Gateway Server to Microsoft. The verbose logs can then be referenced while working with Microsoft to identify or resolve issues with a Tunnel server.

In contrast, the collection of verbose logs previously required you to sign on to the server, run manual tasks and scripts to enable and collect verbose logs, and then copy them to a location from which you can transfer them to Microsoft.

To find this new capability, in the admin center go to **Tenant administration** > **Microsoft Tunnel Gateway** > select a server > select the **Logs** tab. On this tab, is a new section named **Send verbose server logs** with button labeled **Send logs**, and a list view that displays the various log sets that have been collected and submitted to Microsoft.

When you select the **Send logs** button:

- Intune captures and submits the current server logs as a baseline, prior to collecting verbose logs.
- Verbose logging is automatically enabled at level 4, and runs for eight hours to provide time to reproduce an issue for capture in those logs.
- After eight hours, Intune submits the verbose logs and then restores the server to its default verbosity level of zero (0), for normal operations. If you previously set logs to run at a higher verbosity level, you can restore your custom verbosity level after log collection and upload is complete.
- Each time Intune collects and submits logs, it updates the list view below the button.
- Below the button is a list of past log submissions, displaying their verbosity level and an Incident ID that you can use when working with Microsoft to reference a specific set of logs.

For more information about this capability, see [Easy upload of diagnostic logs for Tunnel servers](../protect/microsoft-tunnel-monitor.md#easy-upload-of-diagnostic-logs-for-tunnel-servers).

## Week of December 11, 2023 (Service release 2312)

### App management

#### Support to add unmanaged PKG-type applications to managed macOS devices is now generally available<!-- 17296091   -->

You can now upload and deploy unmanaged PKG-type applications to managed macOS devices using the Intune MDM agent for macOS devices. This feature enables you to deploy custom PKG installers, such as unsigned apps and component packages. You can add a PKG app in the Intune admin center by selecting **Apps** > **macOS** > **Add** > **macOS app (PKG)** for app type.

Applies to:

- macOS

For more information, see [Add an unmanaged macOS PKG app to Microsoft Intune](../apps/macos-unmanaged-pkg.md). To deploy managed PKG-type app, you can continue to [add macOS line-of-business (LOB) apps to Microsoft Intune](../apps/lob-apps-macos.md). For more information about the Intune MDM agent for macOS devices, see [Microsoft Intune management agent for macOS](../apps/lob-apps-macos-agent.md).

#### Windows MAM supported in government cloud environments and in 21 Vianet in China<!-- 25273622  -->

Customer tenants in US Government Community (GCC), US Government Community (GCC) High, and Department of Defense (DoD) environments are now able to use Windows MAM. For related information, see [Deploying apps using Intune on the GCC High and DoD Environments](../apps/apps-deploy-gcc-dod.md) and [Data protection for Windows MAM](../apps/protect-mam-windows.md).

In addition, Windows MAM is available for Intune operated by 21Vianet in China. For more information, see [Intune operated by 21Vianet in China](china.md).

### Device configuration

#### Updated security baseline for Microsoft Edge v117<!-- 25021903 -->

We released a new version of the Intune security baseline for **Microsoft Edge**, version [**v117**](../protect/security-baselines.md#available-security-baselines). This update brings support for recent settings so you can continue to maintain best-practice configurations for Microsoft Edge.

We also updated our [reference article](../protect/security-baseline-v2-edge-settings.md?pivots=edge-v117) for this baseline where you can view the default configuration of the settings this baseline version includes.

### Device management

#### Support for variables in noncompliant email notifications<!-- 6111965  -->

Use variables to personalize email notifications that are sent when a user's device becomes noncompliant. The variables included in the template, such as `{{username}}` and `{{devicename}}`, are replaced by the actual username or device name in the email that users receive. Variables are supported with all platforms.

For more information and a list of supported variables, see [Create a notification message template](../protect/actions-for-noncompliance.md#create-a-notification-message-template).

#### Updated report visualization for Microsoft Defender for Endpoint connector<!--  24762035  -->

We updated the reporting visualization for the Microsoft Defender for Endpoint connector. This [report visualization](../protect/advanced-threat-protection-configure.md#view-the-count-of-devices-that-are-onboarded-to-microsoft-defender-for-endpoint) displays the count of devices that are onboarded to Defender for Endpoint based on status from the Defender CSP, and visually aligns to other recent report views that use a bar to represent the percentage of devices with different status values.

### Device security

#### New settings for scheduling Antivirus scans added to Antivirus policy for Windows devices<!-- 26013546  -->

We added two settings to the *Microsoft Defender Antivirus* profile for [endpoint security Antivirus policy](../protect/endpoint-security-antivirus-policy.md#antivirus-profiles) that applies to Windows 10 and Windows 11 devices. These two settings work together to first enable support for a random start time of a device's antivirus scan, and to then define a range of time during which the randomized scan start can begin. These settings are supported with devices managed by Intune and devices managed through the [Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario.

- [**RandomizeScheduleTaskTimes**](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#admx-microsoftdefenderantivirus-randomizescheduletasktimes) – This setting enables randomization of the scan start time on devices.
- [**SchedulerRandomizationTime**](/windows/client-management/mdm/defender-csp?WT.mc_id=Portal-fx#configurationschedulerrandomizationtime) – With this setting, you can set boundaries for the random start time.

In addition to being added to the Microsoft Defender Antivirus profile, both settings are now available from the [settings catalog](../configuration/settings-catalog.md).

Applies to:

- Windows 10
- Windows 11

#### Microsoft Tunnel support for direct proxy exclusion list in VPN profiles for Android Enterprise<!-- 24139621 -->

Intune now supports configuration of a *Proxy exclusion list* when you [configure a VPN profile for Microsoft Tunnel](../protect/microsoft-tunnel-configure.md#create-a-vpn-profile) for Android devices. With an exclusion list, you can exclude specific domains from your proxy setup without requiring the use of a Proxy Auto-Configuration (PAC) file. The proxy exclusion list is available with both Microsoft Tunnel and Microsoft Tunnel for MAM.

The proxy exclusion list is supported in environments that use a single proxy. The exclusion list isn't suitable or supported when you use multiple proxy servers, for which you should continue to use a `.PAC` file.

Applies to:

- Android Enterprise

#### Microsoft Tunnel server health metric to report on TLS certificate revocation<!-- 25853648  -->

We added a new health metric for Microsoft Tunnel named **TLS certificate revocation**. This new health metric report on the status of the Tunnel Servers TLS certificate by accessing the Online Certificate Status Protocol (OCSP) or CRL address as defined in the TLS certificate. You can view the status of this new check with all the health checks in the Microsoft Intune admin center by navigating to **Tenant administration** > **Microsoft Tunnel Gateway** > **Health status**, selecting a server, and then selecting that servers **Health check** tab.

This metric runs as part of the existing Tunnel Health checks, and supports the following status:

- *Healthy*: The TLs certificate isn't revoked
- *Warning*: Unable to check if the TLS certificate is revoked
- *Unhealthy*: The TLS certificate is revoked, and should be updated

For more information about the TLS certificate revocation check, see [Monitor Microsoft Tunnel](../protect/microsoft-tunnel-monitor.md).

### Intune apps

#### Newly available protected app for Intune<!-- 25636619  -->

The following protected app is now available for Microsoft Intune:

- Akumina EXP by Akumina Inc.

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of November 27, 2023

### App management

#### Configure offline caching in Microsoft 365 (Office) for Android devices<!-- 25008682 -->

When the **Save As to Local Storage** setting is set to **blocked** in an [app protection policy](../apps/app-protection-policies.md), you can use a configuration key in an app configuration policy to enable or disable offline caching. This setting is only applicable to the Microsoft 365 (Office) app on Android.

For more information, see [Data protection settings in Microsoft 365 (Office)](../apps/manage-microsoft-office.md#data-protection-settings-in-microsoft-365-office).

#### Win32 app grace period settings on a device<!-- 17644728 -->

On a device where a Win32 app with grace period settings is deployed, low-rights users without administrative privileges can now interact with the grace period UX. Admins on the device continue to be able to interact with the grace period UX on the device.

For more information about grace period behavior, see [Set Win32 app availability and notifications](../apps/apps-win32-app-management.md#set-win32-app-availability-and-notifications).

#### Managed Home Screen app configuration additions<!-- 25374056 -->

Now in public preview, Microsoft Managed Home Screen (MHS) is updated to improve the core workflows and user experience. In addition to some user interface changes, there's a new top bar navigation where admins can configure device identifying attributes to be displayed. Additionally, users can access settings, sign in/out, and view notifications when permissions are requested on the top bar.

You can add more settings to configure the Managed Home Screen app for Android Enterprise. Intune now supports the following settings in your Android Enterprise app configuration policy:

- Enable updated user experience
- Top Bar Primary Element
- Top Bar Secondary Element
- Top Bar User Name Style

For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### Intune APP SDK for .NET MAUI<!-- 17696301 -->

Using the Intune APP SDK for .NET MAUI, you can develop Android or iOS apps for Intune that incorporate the [.NET Multi-platform App UI](https://dotnet.microsoft.com/apps/maui). Apps developed using this framework allow you to enforce [Intune mobile application management](../apps/app-management.md). For .NET MAUI support on Android, see [Intune App SDK for .NET MAUI - Android](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android). For .NET MAUI support on iOS, see [Intune App SDK for .NET MAUI - iOS](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS).

## Week of November 13, 2023 (Service release 2311)

### App management

#### New grace period status added in apps for Android, Android AOSP<!-- 13498172 13498291  -->

The Intune Company Portal app for Android and Microsoft Intune app for Android AOSP now show a grace period status for devices that don't meet compliance requirements but are still within their given grace period. Users can see the date by which devices must be compliant, and the instructions for how to become compliant. If users don't update their device by the given date, the device is marked as noncompliant.

For more information, see the following articles:

- [Configure compliance policies with actions for noncompliance](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance)
- [Check compliance in Intune app for AOSP](../user-help/check-compliance-aosp.md)
- [Check compliance in Company Portal for Android](../user-help/check-compliance-on-your-device-android.md)

### Device configuration

#### New settings available in the Apple settings catalog<!-- 25189345  -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Managed Settings**:

- Data roaming
- Personal hotspot
- Voice roaming (deprecated): This setting is deprecated in iOS 16.0. Data roaming is the replacement setting.

##### Shared iPad

**Managed Settings**:

- Diagnostic submission

##### macOS

**Microsoft Defender > Antivirus engine**:

- Enable passive mode (deprecated): This setting is deprecated. Enforcement level is the replacement setting.
- Enable real-time protection (deprecated): This setting is deprecated. Enforcement level is the replacement setting.
- Enforcement level

#### Settings to manage Windows Subsystem for Linux are now available in the Windows settings catalog<!-- 17757930  -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings to the Windows settings catalog for *Windows Subsystem for Linux* (WSL). These settings enable Intune integration with WSL so admins can manage deployments of WSL and controls into Linux instances themselves.

To find these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Devices** > **Configuration** > **Create** > **New Policy** > **Windows 10 and later** for platform > **Settings catalog** for profile type.

**Windows Subsystem for Linux**:

- Allow kernel debugging
- Allow custom networking configuration
- Allow custom system distribution configuration
- Allow kernel command line configuration
- Allow custom kernel configuration
- Allow WSL1
- Allow the Windows Subsystem for Linux
- Allow the Inbox version of the Windows Subsystem For Linux
- Allow user setting firewall configuration
- Allow nested virtualization
- Allow passthrough disk mount
- Allow the debug shell

Applies to:

- Windows 10
- Windows 11

### Device enrollment

#### Enrollment for iOS/iPadOS devices in shared device mode now generally available<!-- 25199565   -->

Now generally available to configure in the Microsoft Intune admin center, set up automated device enrollment for iOS/iPadOS devices that are in shared device mode. Shared device mode is a feature of Microsoft Entra that enables your frontline workers to share a single device throughout the day, signing in and out as needed.

For more information, see [Set up enrollment for devices in shared device mode](../enrollment/automated-device-enrollment-shared-device-mode.md).

### Device management

#### Improvements to new device experience in admin center (public preview)<!-- 24155098, 25103808, 17705028   -->

We made the following changes to the new Devices experience in the Microsoft Intune admin center:

- More entry points to platform-specific options: Access the platform pages from the **Devices** navigation menu.
- Quick entry to monitoring reports: Select the titles of the metrics cards to go to the corresponding monitoring report.
- Improved navigation menu: We added icons back in to provide more color and context as you navigate.

Flip the toggle in the Microsoft Intune admin center to try out the new experience while it's in public preview and share your feedback.

For more information, see:

- [New Microsoft Intune Devices experience - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/intune-customer-success/new-microsoft-intune-devices-experience/ba-p/3777342)
- [Try new Devices experience - Microsoft Learn](public-preview.md)

### Device security

#### Additional settings for the Linux Antivirus policy template<!-- 24191424 -->

We expanded support for Linux by adding the following settings to the *Microsoft Defender Antivirus* template for Linux devices:

- cloudblocklevel
- scanarhives
- scanafterdefinitionupdate
- maximumondemandscanthreads
- behaviormonitoring
- enablefilehashcomputation
- networkprotection
- enforcementlevel
- nonexecmountpolicy
- unmonitoredfilesystems

The Microsoft Defender Antivirus template for Linux is supported for devices [managed by Intune](../protect/endpoint-security-antivirus-policy.md), and devices managed only by Defender through the [Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario.

#### Updated security baseline for Microsoft 365 Apps for Enterprise<!-- 25021846   -->

We released a new version of the Intune security baseline for **Microsoft 365 Apps for Enterprise**, version [**2306**](../protect/security-baselines.md#available-security-baselines).

The Microsoft 365 Office Apps baseline can help you rapidly deploy configurations to your Office Apps that meet the security recommendations of the Office and security teams at Microsoft. As with all baselines, the default baseline represents the recommended configurations. You can modify the default baseline to meet the requirements of your organization.

We also updated our [reference article](../protect/security-baseline-v2-office-settings.md?pivots=v2306) for this baseline where you can view the default configuration of the settings this baseline version includes.

#### Deprecation and replacement of two settings found in the Linux and macOS endpoint security Antivirus policies<!-- 25234740  -->

There are two deprecated settings that in the *Antivirus engine* category of [Microsoft Defender Antivirus](../protect/endpoint-security-antivirus-policy.md) profiles of both macOS and Linux. These profiles are available as part of Intune's endpoint security Antivirus policies.

For each platform, a single setting replaces the two deprecated settings. This new setting aligns with how Microsoft Defender for Endpoint manages the device configurations.

The following are the two deprecated settings:

- *Enable real-time protection* now appears as *Enable real-time protection (deprecated)*
- *Enable passive mode* now appears as *Enable passive mode (deprecated)*

The new setting that replaces the two deprecated settings:

- *Enforcement level* - By default, Enforcement level is set to *Passive* and supports options of *Real time* and *On demand*.

These settings are also available from the Intune [settings catalog](../configuration/settings-catalog.md) for each platform, where the old settings are also marked as deprecated and replaced by the new setting.

With this change, a device that has either of the *deprecated* settings configured will continue to apply that configuration until the device is targeted by the new setting *Enforcement level*. Once targeted by Enforcement Level, the deprecated settings no longer are applied to the device.

The *deprecated* settings will be removed from the Antivirus profiles and the settings catalog in a future update to Intune.

> [!NOTE]
> The changes for Linux are now available. The macOS settings are marked as deprecated, but the *Enforcement level* setting will not be available until December.

Applies to:

- Linux
- macOS

#### Microsoft Defender Firewall profiles are renamed to Windows Firewall<!-- 25171457 -->

To align to Firewall branding changes in Windows, we are updating the names of Intune profiles for endpoint security Firewall policies. In profiles that have *Microsoft Defender Firewall* in the name we're replacing that with *Windows Firewall*.

The following platforms have profiles that are affected, with only the profile names being affected by this change:

- Windows 10 and later (ConfigMgr)
- Windows 10, Windows 11, and Windows Server

#### Endpoint security Firewall policy for Windows Firewall to manage firewall settings for Windows Hyper-V<!--  25767542  -->

We added new settings to the *Windows Firewall* profile (formerly *Microsoft Defender Firewall*) for endpoint security [Firewall policy](../protect/endpoint-security-firewall-policy.md). The new settings can be used to manage Windows Hyper-V settings. To configure the new settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Endpoint security** > **Firewall** > Platform: **Windows 10, Windows 11, and Windows Server** > Profile: **Windows Firewall**.

The following settings are added to the *Firewall* category:

- **Target** - When *Target* is set to **Windows Subsystem for Linux**, the following child settings are applicable:
  - Enable Public Network Firewall
  - Enable Private Network Firewall
  - Allow Host Policy Merge
  - Enable Domain Network Firewall
  - Enable Loopback

Applies to:

- Windows 10
- Windows 11

For more information about these settings, see [Windows Firewall with Advanced Security](/windows/security/operating-system-security/network-security/windows-firewall/windows-firewall-with-advanced-security).

#### New Endpoint Security Firewall policy profile for Windows Hyper-V Firewall Rules<!-- 10946486  -->

We released a new profile named *Windows Hyper-V Firewall Rules* that you can find through the *Windows 10, Windows 11, and Windows Server* platform path for endpoint security [Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune). Use this profile to manage the firewall settings and rules that apply to specific Hyper-V containers on Windows, including applications like the Windows Subsystem for Linux (WSL) and the Windows Subsystem for Android (WSA).

Applies to:

- Windows 10
- Windows 11

### Intune apps

#### Newly available protected apps for Intune<!-- 25417889, 25161990, 25174019  -->

The following protected apps are now available for Microsoft Intune:

- Hey DAN for Intune by Civicom, Inc.
- Microsoft Azure by Microsoft Corporation (iOS)
- KeePassium for Intune by KeePassium Labs (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of November 6, 2023

### App management

#### Minimum version update for iOS Company Portal<!-- 17964541 -->

Users are required to update to v5.2311.1 of the iOS Company Portal. If you enabled the **[Block installing apps using App Store](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised)** device restriction setting, you'll likely need to push an update to the related devices that use this setting. Otherwise, no action is needed.

If you have a helpdesk, you might want to make them aware of the prompt to update the Company Portal app. In most cases, users have app updates set to automatic, so they receive the updated Company Portal app without taking any action. Users that have an earlier app version are prompted to update to the latest Company Portal app.

### Device security

#### Defender for Endpoint security settings management enhancements and support for Linux and macOS are generally available<!-- 24190967 -->

The improvements that were introduced in the Defender for Endpoint security settings management [opt-in public preview](#defender-for-endpoint-security-settings-management-enhancements-and-support-for-linux-and-macos-in-public-preview) are now generally available.

With this change, the default behavior for security settings management includes all the behavior added for the opt-in preview – without having to enable support for preview features in Microsoft Defender for Endpoint. This includes the general availability and support for the following endpoint security profiles for Linux and macOS:

**Linux**:

- Microsoft Defender Antivirus
- Microsoft Defender Antivirus exclusions
- Endpoint detection and response

**MacOS**:

- Microsoft Defender Antivirus
- Microsoft Defender Antivirus exclusions
- Endpoint detection and response

For more information, see [Microsoft Defender for Endpoint Security settings management](../protect/mde-security-integration.md) in the Intune documentation.

### Device management

### Feature updates and reports support Windows 11 policies<!--17614166 -->

The new setting on Feature update policies enables an organization to deploy Windows 11 to those devices that are eligible for the upgrade, while ensuring devices not eligible for the upgrade are on the latest Windows 10 feature update with a single policy. As a result, admins don't need to create or manage groups of eligible and non-eligible devices.

For more information on feature updates, see [Feature updates for Windows 10 and later](../protect/windows-10-feature-updates.md).

## Week of October 30, 2023

### Device security

#### Strict Tunnel Mode in Microsoft Edge available for Microsoft Tunnel for MAM on Android and iOS/iPadOS devices<!--24045412-->

In Intune, you can use the Microsoft Tunnel for mobile application management (MAM) on Android and iOS/iPadOS devices. With the MAM tunnel, unmanaged devices (devices not enrolled in Intune) can access on-premises apps and resources.

There's a new **Strict Tunnel Mode** feature you can configure for Microsoft Edge. When users sign into Microsoft Edge with an organization account, if the VPN isn't connected, then **Strict Tunnel Mode** blocks internet traffic. When the VPN reconnects, internet browsing is available again.

To configure this feature, create a Microsoft Edge app configuration policy, and add the following setting:

- **Key**: `com.microsoft.intune.mam.managedbrowser.StrictTunnelMode`
- **Value**: `True`

Applies to:

- Android Enterprise version 10 and later
- iOS/iPadOS version 14 and later

For more information, see:

- [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-mam.md)
- [Microsoft Tunnel for MAM - Android](../protect/microsoft-tunnel-mam-android.md)
- [Microsoft Tunnel for MAM - iOS/iPadOS](../protect/microsoft-tunnel-mam-ios.md)

## Week of October 23, 2023 (Service release 2310)

### App management

#### Update for users of Android Company Portal app<!-- 25109006   -->

If users launch a version of the Android Company Portal app below version 5.0.5333.0 (released November 2021), they'll see a prompt encouraging them to update their Android Company Portal app. If a user with an older Android Company Portal version attempts a new device registration using a recent version of the Authenticator app, the process will likely fail. To resolve this behavior, update the Android Company Portal app.

#### Minimum SDK version warning for iOS devices<!-- 9410239  -->

The **Min SDK version** for the iOS Conditional Launch setting on iOS devices now includes a **warn** action. This action warns end users if the min SDK version requirement isn't met.

For more information, see [iOS app protection policy settings](../apps/app-protection-policy-settings-ios.md).

#### Minimum OS for Apple LOB and store apps<!-- 24623225  -->

You can configure the minimum operating system to be the latest Apple OS releases for both Apple line-of-business apps and iOS/iPadOS store apps. You can set the minimum operating system for Apple apps as follows:

- iOS/iPadOS 17.0 for iOS/iPadOS line-of-business apps
- macOS 14.0 for macOS line-of-business apps
- iOS/iPadOS 17.0 for iOS/iPadOS store apps

Applies to:

- iOS/iPadOS
- macOS

#### Android (AOSP) supports line-of-business (LOB) apps<!-- 24823138   -->

You can install and uninstall mandatory LOB apps on AOSP devices by using the **Required** and **Uninstall** group assignments.

Applies to:

- Android

To learn more about managing LOB apps, see [Add an Android line-of-business app to Microsoft Intune](../apps/lob-apps-android.md).

#### Configuration scripts for unmanaged macOS PKG apps<!-- 17745891  -->

You can now configure pre-install and post-install scripts in unmanaged macOS PKG apps. This feature gives you greater flexibility over custom PKG installers. Configuring these scripts is optional and requires the Intune agent for macOS devices v2309.007 or higher.

For more information about adding scripts to unmanaged macOS PKG apps, see [Add an unmanaged macOS PKG app](../apps/macos-unmanaged-pkg.md).

### Device configuration

#### FSLogix settings are available in the Settings Catalog and Administrative Templates<!-- 10946920  -->

The [FSLogix settings](/fslogix/reference-configuration-settings) are available in the Settings Catalog and in Administrative Templates (ADMX) for you to configure.

Previously, to configure FSLogix settings on Windows devices, you imported them using the ADMX import feature in Intune.

Applies to:

- Windows 10
- Windows 11

For more information on these features, see:

- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)
- [Use Windows templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md)
- [What is FSLogix?](/fslogix/overview-what-is-fslogix)

#### Use delegated scopes in your Managed Google Play apps that configure enhanced permissions on Android Enterprise devices<!-- 14029609  -->

In your Managed Google Play apps, you can give apps enhanced permissions using delegated scopes.

When your apps include delegated scopes, you can configure the following settings in a device configuration profile (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Device Restrictions** for profile type > **Applications**):

- **Allow other apps to install and manage certificates**: Admins can select multiple apps for this permission. The selected apps are granted access to certificate installation and management.
- **Allow this app to access Android security logs**: Admins can select one app for this permission. The selected app is granted access to security logs.
- **Allow this app to access Android network activity logs**: Admins can select one app for this permission. The selected app is granted access to network activity logs.

To use these settings, your Managed Google Play app must use delegated scopes.

Applies to:

- Android Enterprise fully managed devices
- Android Enterprise dedicated devices
- Android Enterprise corporate-owned devices with a work profile

For more information on this feature, see:

- [Android's built-in app configurations](../developer/app-sdk-android-phase6.md#androids-built-in-app-configurations)
- [Android Enterprise device settings list to allow or restrict features on corporate-owned devices using Intune > Applications](../configuration/device-restrictions-android-for-work.md)

#### Samsung ended support for kiosk mode on Android device administrator (DA) devices<!-- 24810356  -->

Samsung marked the Samsung Knox kiosk APIs used on Android device administrator as deprecated in Knox 3.7 (Android 11).

Though the functionality might continue to work, there's no guarantee that it will continue working. Samsung won't fix bugs that might arise. For more information on Samsung support for deprecated APIs, see [What kind of support is offered after an API is deprecated?](https://docs.samsungknox.com/dev/knox-sdk/faqs/general/deprecated-api-support-change.htm) (opens Samsung's web site).

Instead, you can manage kiosk devices with Intune using [dedicated device management](../enrollment/android-kiosk-enroll.md).

Applies to:

- Android device administrator (DA)

#### Import and export settings catalog policies<!-- 3470151  -->

The Intune [settings catalog](../configuration/settings-catalog.md) lists all the settings you can configure, and all in one place (**Devices** > **Manage devices** > **Configuration** > **Create** > **New Policy** > Select your **platform** > For **Profile type**, select **Settings catalog**).

The settings catalog policies can be imported and exported:

- To export an existing policy, select the profile > select the ellipsis > **Export JSON**.
- To import a previously exported settings catalog policy, select **Create** > **Import policy** > select the previously exported JSON file.

For more information about the settings catalog, see [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md).

> [!NOTE]
>
> This feature is continuing to roll out. It may be a couple of weeks before it's available in your tenant.

#### New setting to block users from using the same password to unlock the device and access the work profile on Android Enterprise personally owned devices with a work profile<!-- 6167371  -->

On Android Enterprise personally owned devices with a work profile, users can use the same password to unlock the device and access the work profile.

There's a new setting that can enforce different passwords to unlock the device and access the work profile (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** > **Personally Owned Work Profile** for platform > **Device Restrictions** for profile type):

- **One lock for device and work profile**: **Block** prevents users from using the same password for the lock screen on the device and work profile. End users are required to enter the device password to unlock the device and enter their work profile password to access their work profile. When set to **Not Configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to access their work profile using a single password.

This setting is optional and doesn't impact existing configuration profiles.

Currently, if the work profile password doesn't meet the policy requirements, then device users see a notification. The device isn't marked as non-compliant. A separate compliance policy for the work profile is being created and will be available in a future release.

Applies to:

- Android Enterprise personally owned devices with a work profile (BYOD)

For a list of settings you can configure on personally owned devices with a work profile, see [Android template device settings list to restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

#### New settings available in the macOS settings catalog<!-- 24950434  -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** > **Settings catalog** for profile type.

**Privacy > Privacy Preferences Policy Control**:

- System Policy App Data

**Restrictions**:

- Force On Device Only Dictation

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

### Device enrollment

#### Web based device enrollment with JIT registration for personal iOS/iPadOS devices<!-- 15412485  -->

Intune supports web-based device enrollment with just in time (JIT) registration for personal devices set up via Apple device enrollment. JIT registration reduces the number of authentication prompts shown to users throughout the enrollment experience and establishes SSO across the device. Enrollment takes place on the web version of Intune Company Portal, eliminating need for the Company Portal app. Also, this enrollment method enables employees and students without managed Apple IDs to enroll devices and access volume-purchased apps.

For more information, see [Set up web based device enrollment for iOS](../enrollment/web-based-device-enrollment-ios.md).

### Device management

#### Updates to the Intune add-ons page<!--17395941 -->

The Intune add-ons page under **Tenant administration** includes **Your add-ons**, **All add-ons**, and **Capabilities**. It provides an enhanced view into your trial or purchased licenses, the add-on capabilities you're licensed to use in your tenant, and support for new billing experiences in Microsoft admin center.

For more information, see [Use Intune Suite add-ons capabilities](intune-add-ons.md).

#### Remote Help for Android is now Generally available<!--17675897 -->

Remote Help is generally available for Android Enterprise Dedicated devices from Zebra and Samsung.

With Remote Help, IT Pros can remotely view the device screen and take full control in both attended and unattended scenarios, to diagnose and resolve issues quickly and efficiently.

Applies to:

- Android Enterprise Dedicated devices, manufactured by Zebra or Samsung

For more information, see [Remote Help on Android](remote-help-android.md).

### Device security

#### Configure declarative software updates and passcode policies for Apple devices in the Settings Catalog<!-- 24989083  -->

You can manage software updates and passcode using Apple's declarative device management (DDM) configuration using the settings catalog (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type > **Declarative device management**).

For more information about DDM, see [Apple's declarative device management (DDM)](https://developer.apple.com/documentation/devicemanagement/leveraging_the_declarative_management_data_model_to_scale_devices) (opens Apple's website).

DDM allows you to install a specific update by an enforced deadline. The autonomous nature of DDM provides an improved user experience as the device handles the entire software update lifecycle. It prompts users that an update is available and also downloads, prepares the device for the installation, & installs the update.

In the settings catalog, the following declarative software update settings are available at **Declarative device management > Software Update**:

- **Details URL**: The web page URL that shows the update details. Typically, this URL is a web page hosted by your organization that users can select if they need organization-specific help with the update.
- **Target Build Version**: The target build version to update the device to, like `20A242`. The build version can include a supplemental version identifier, like `20A242a`. If the build version you enter isn't consistent with the **Target OS Version** value you enter, then the **Target OS Version** value takes precedence.
- **Target Local Date Time**: The local date time value that specifies when to force install the software update. If the user doesn't trigger the software update before this time, then the device force installs it.
- **Target OS Version**: The target OS version to update the device to. This value is the OS version number, like `16.1`. You can also include a supplemental version identifier, like `16.1.1`.

For more information on this feature, see [Manage software updates with the settings catalog](../protect/updates/apple.md).

In the settings catalog, the following declarative passcode settings are available at **Declarative device management > Passcode**:

- **Automatic Device Lock**: Enter the maximum time period that a user can be idle before the system automatically locks the device.
- **Maximum Grace Period**: Enter the maximum time period that a user can unlock the device without a passcode.
- **Maximum Number of Failed Attempts**: Enter the maximum number of wrong passcode attempts before:
  - iOS/iPadOS wipes the device
  - macOS locks the device
- **Minimum Passcode Length**: Enter the minimum number of characters a passcode must have.
- **Passcode Reuse Limit**: Enter the number of previously used passcodes that can't be used.
- **Require Complex Passcode**: When set to **True**, a complex passcode is required. A complex passcode doesn't have repeated characters, and doesn't have increasing or decreasing characters, like `123` or `CBA`.
- **Require Passcode on Device**: When set to **True**, the user must set a passcode to access the device. If you don't set other passcode restrictions, then there aren't any requirements about the length or quality of the passcode.

Applies to:

- iOS/iPadOS 17.0 and later
- macOS 14.0 and later

For information about the settings catalog, see [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md).

#### Mvision Mobile is now Trellix Mobile Security<!-- 16208061 -->

The Intune [Mobile Threat Defense partner](../protect/mobile-threat-defense.md) **Mvision Mobile** has transitioned to **Trellix Mobile Security**. With this change, we've updated our documentation and the Intune admin center UI. For example, the *Mvision Mobile connector* is now *Trellix Mobile Security*. Existing installs of the Mvision Mobile connector also update to Trellix Mobile Security.

If you have questions about this change, reach out to your Trellix Mobile Security representative.

### Intune apps

#### Newly available protected app for Intune<!-- 24920511, 24950232  -->

The following protected app is now available for Microsoft Intune:

- BuddyBoard by Brother Industries, LTD
- Microsoft Loop by Microsoft Corporation

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Updated reports for Policy compliance and Setting compliance are now generally available<!-- 24299948, 24299945  -->

The following device compliance reports are out of public preview and are now generally available:

- [Policy compliance](reports.md#policy-compliance-report-organizational)
- [Setting compliance](reports.md#settings-compliance--organizational)

With this move to general availability, the older versions of both reports have been retired from the Intune admin center and are no longer available.

For more information about these changes, see the Intune Support Team blog at [https://aka.ms/Intune/device_compl_report](https://aka.ms/Intune/device_compl_report).

### Tenant administration

#### Intune admin center home page update<!-- 16950040  -->

The Intune admin center home page has been redesigned with a fresh new look and more dynamic content. The **Status** section has been simplified. You can explore Intune related capabilities in the **Spotlight** section. The **Get more out of Intune** section provides links to the Intune community and blog, and Intune customer success. Also, the **Documentation and training** section provides links to **What's New in Intune**, **Feature in development**, and more training. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Home**.

### Microsoft Intune Suite

#### Remote Help

Version: 5.0.1311.0

- Disabled the relaying of system audio from the Sharer device to the Helper device, which caused an echo when both users were using another app to communicate (such as Teams).
- Added the capability for Helpers that have elevation permissions to also be able to elevate apps on devices where the Sharer is an Administrator.

## Week of October 16, 2023

### Tenant administration

#### `endpoint.microsoft.com` URL redirects to `intune.microsoft.com`<!-- 25169925 -->

Previously, it was announced that the Microsoft Intune admin center has a new URL (`https://intune.microsoft.com`).

The `https://endpoint.microsoft.com` URL now redirects to `https://intune.microsoft.com`.

## Week of September 18, 2023 (Service release 2309)

### App management

#### MAM for Windows general availability<!-- 12394345, 12394352 -->

You can now enable protected MAM access to org data via Microsoft Edge on personal Windows devices. This capability uses the following functionality:
- Intune Application Configuration Policies (ACP) to customize the org user experience in Microsoft Edge
- Intune Application Protection Policies (APP) to secure org data and ensure the client device is healthy when using Microsoft Edge
- Windows Security Center threat defense integrated with Intune APP to detect local health threats on personal Windows devices
- Application Protection Conditional Access to ensure the device is protected and healthy before granting protected service access via Microsoft Entra ID.

Intune Mobile Application Management (MAM) for Windows is available for Windows 11, build 10.0.22621 (22H2) or later. This feature includes the supporting changes for Microsoft Intune (2309 release), Microsoft Edge (v117 stable branch and later) and Windows Security Center (v 1.0.2309.xxxxx and later). App Protection Conditional Access is in Public Preview.

Sovereign cloud support is expected in the future. For more information, see [App protection policy settings for Windows](../apps/app-protection-policy-settings-windows.md).

### Device configuration

#### OEMConfig profiles that don't deploy successfully aren't shown as "pending"<!-- 24284049 -->

For Android Enterprise devices, you can create a configuration policy that configures the OEMConfig app (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **OEMConfig** for profile type).

Previously, OEMConfig profiles that exceed 350 KB show a "pending" state. This behavior changed. An OEMConfig profile that exceeds 350 KB isn't deployed to the device. Profiles in a pending state or profiles larger that 350 KB aren't shown. Only profiles that successfully deploy are shown.

This change is a UI change only. No changes are made to the corresponding Microsoft Graph APIs.

To monitor the profile pending status in the Intune admin center, go to **Devices** > **Manage devices** > **Configuration** > Select the profile > **Device status**.

Applies to:

- Android Enterprise

For more information on OEM Configuration, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

#### Config Refresh settings are in the settings catalog for Windows Insiders<!-- 15060174  -->

In the Windows Settings Catalog, you can configure **Config Refresh**. This feature lets you set a cadence for Windows devices to reapply previously received policy settings, without requiring devices to check in to Intune.

Config Refresh:

- Enable config refresh
- Refresh cadence (minutes)

Applies to:

- Windows 11

For more information on the Settings Catalog, see [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md).

#### Managed Settings now available in the Apple settings catalog<!-- 21083384  -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

The settings within the Managed Settings command are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** > **Settings catalog** for profile type.

**Managed Settings > App Analytics**:

- Enabled: If true, enable sharing app analytics with app developers. If false, disable sharing app analytics.

Applies to:

- Shared iPad

**Managed Settings > Accessibility Settings**:

- Bold Text Enabled
- Grayscale Enabled
- Increase Contrast Enabled
- Reduce Motion Enabled
- Reduce Transparency Enabled
- Text Size
- Touch Accommodations Enabled
- Voice Over Enabled
- Zoom Enabled

**Managed Settings > Software Update Settings**:

- Recommendation Cadence: This value defines how the system presents software updates to the user.

**Managed Settings > Time Zone**:

- Time Zone: The Internet Assigned Numbers Authority (IANA) time zone database name.

Applies to:

- iOS/iPadOS

**Managed Settings > Bluetooth**:

- Enabled: If true, enable the Bluetooth setting. If false, disable the Bluetooth setting.

**Managed Settings > MDM Options**:

- Activation Lock Allowed While Supervised: If true, a supervised device registers itself with Activation Lock when the user enables Find My.

Applies to:

- iOS/iPadOS
- macOS

For more information on these settings, see [Apple's developer website](https://developer.apple.com/documentation/devicemanagement/settingscommand/command/settings). For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### New settings available in the macOS settings catalog<!-- 24809885  -->

The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

There's a new setting in the Settings Catalog. To see this setting, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** > **Settings catalog** for profile type.

**Microsoft Defender > Cloud delivered protection preferences**:

- Cloud Block Level

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### Intune integration with the Zebra Lifeguard Over-the-Air service is generally available<!-- 16238201  -->

Microsoft Intune supports integration with Zebra Lifeguard Over-the-Air service, which allows you to deliver OS updates and security patches over-the-air to eligible Zebra devices that are enrolled with Intune. You can select the firmware version you want to deploy, set a schedule, and stagger update downloads and installs. You can also set minimum battery, charging status, and network conditions requirements for when the update can happen.

This integration is now generally available for Android Enterprise Dedicated and Fully Managed Zebra devices that are running Android 8 or later. It also requires a Zebra account and Intune Plan 2 or Microsoft Intune Suite.

Previously, this feature was in public preview and free for use. With this release as generally available, this solution now requires an add-on license for its use.

For licensing details, see [Intune add-ons](intune-add-ons.md).

### Device enrollment

#### SSO support during enrollment for Android Enterprise fully managed and corporate-owned devices with a work profile<!-- 8080357 -->

Intune supports single sign-on (SSO) on Android Enterprise devices that are fully managed or corporate-owned with a work profile.  With the addition of SSO during enrollment, end users enrolling their devices only need to sign in once with their work or school account.


Applies to:

- Android Enterprise corporate owned devices with a work profile
- Android Enterprise fully managed

For more information on these enrollment methods, see:

- [Set up Intune enrollment of Android Enterprise corporate-owned devices with work profile](../enrollment/android-corporate-owned-work-profile-enroll.md)
- [Set up enrollment for Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md)

### Device management

#### Introducing Remote Help on macOS<!--12454029 -->

The Remote Help web app allows users to connect to macOS devices and join a view-only remote assistance session.

Applies to:

- 11 Big Sur
- 12 Monterey
- 13 Ventura

For more information on Remote Help on macOS, see [Remote Help](remote-help-macos.md).

#### Management certificate expiration date<!-- 17648747  -->

Management certificate expiration date is available as a column in the **Devices** workload. You can filter on a range of expiration dates for the management certificate and also export a list of devices with an expiration date matching the filter.

This information is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **All devices**.

#### Windows Defender Application Control (WDAC) references are updated to App Control for Business<!-- 24863807  -->

Windows renamed *Windows Defender Application Control* (WDAC) as *App Control for Business*. With this change, the references in Intune docs and the Intune admin center are updated to reflect this new name.

#### Intune supports iOS/iPadOS 15.x as the minimum version<!-- 24161619 -->

Apple released iOS/iPadOS version 17. Now, the minimum version supported by Intune is iOS/iPadOS 15.x.

Applies to:

- iOS/iPadOS

> [!NOTE]
>
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. For more information, see [Support statement for supported versus allowed iOS/iPadOS versions for user-less devices](https://aka.ms/ADE_userless_support).

#### Government tenant support for endpoint security Application Control policy and managed installer<!-- 24850055   -->

We've added support to use endpoint security [Application Control policies](../protect/endpoint-security-app-control-policy.md), and to configure a managed installer, to the following sovereign cloud environments:

- US Government clouds
- 21Vianet in China

Support for Application Control policy and managed installers was originally [released in preview in June 2023](#new-endpoint-security-application-control-policy-in-preview). Application Control policies in Intune are an implementation of Defender Application Control (WDAC).

### Device security

#### Endpoint Privilege Management support for Windows 365 devices<!-- 17016794  -->

You can now use [Endpoint Privilege Management](../protect/epm-overview.md) to manage application elevations on Windows 365 devices (also known as Cloud PCs).

This support doesn't include Azure Virtual Desktop.

#### Elevation report by Publisher for Endpoint Privilege Management<!--  24593400  -->

We've released a new report named **Elevation report by Publisher** for Endpoint Privilege Management (EPM). With [this new report](../protect/epm-reports.md#elevation-report-by-publisher) you can view all managed and unmanaged elevations, which are aggregated by the publisher of the app that is elevated.

You'll find the report in the Report node for EPM in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Navigate to **Endpoint security** > **Endpoint Privilege Management** and then select the **Reports** tab.

#### macOS support with Intune Endpoint security policies for Endpoint detection and response<!--  17757981 -->

Intune Endpoint security policies for *Endpoint detection and response* (EDR) now support macOS. To enable this support, we've added a new [EDR template profile for macOS](../protect/endpoint-security-edr-policy.md#devices-managed-by-microsoft-intune). Use this profile with macOS devices enrolled with Intune and macOS devices managed through the opt-in public preview of the [Defender for Endpoint security settings management](../protect/mde-security-integration.md?pivots=mdssc-preview) scenario.

The EDR template for macOS includes the following settings for the *Device tags* category from Defender for Endpoint:

- **Type of  tag** – The GROUP tag, tags the device with the specified value. The tag is reflected in the admin center on the device page and can be used for filtering and grouping devices.
- **Value of tag** - Only one value per tag can be set. The Type of a tag is unique and shouldn't be repeated in the same profile.

To learn more about Defender for Endpoint settings that are available for macOS, see [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences#device-tags) in the Defender documentation.

#### Linux support with Intune Endpoint security policies for Endpoint detection and response<!--  17757972  -->

Intune Endpoint security policies for *Endpoint detection and response* (EDR) now support Linux. To enable this support, we've added a new [EDR template profile for Linux](../protect/endpoint-security-edr-policy.md#devices-managed-by-microsoft-intune). Use this profile with Linux devices enrolled with Intune and Linux devices managed through the opt-in public preview of the [Defender for Endpoint security settings management](../protect/mde-security-integration.md?pivots=mdssc-preview) scenario.

The EDR template for Linux includes the following settings for the *Device tags* category from Defender for Endpoint:

- **Value of tag** - Only one value per tag can be set. The Type of a tag is unique and shouldn't be repeated in the same profile.
- **Type of tag** – The GROUP tag, tags the device with the specified value. The tag is reflected in the admin center on the device page and can be used for filtering and grouping devices.

You can learn more about Defender for Endpoint settings that are available for Linux in [Set preferences for Microsoft Defender for Endpoint on Linux](/microsoft-365/security/defender-endpoint/linux-preferences#device-tags) in the Defender documentation.

### Monitor and troubleshoot

#### Updated reports for Update rings for Windows 10 and later<!-- 10159960 -->

Reporting for [Update rings for Windows 10 and later](../protect/windows-10-update-rings.md) has been updated to use Intune's improved reporting infrastructure. These changes align to similar improvements introduced for other Intune features.

With this change for reports for Update rings for Windows 10 and later, when you select an update rings policy in the Intune admin center, there isn't a left-pane navigation for *Overview*, *Manage*, or *Monitor* options. Instead, the policy view opens to a single pane that includes the following policy details:

- **Essentials** – including the policy name, created and modified dates, and more details.
- **Device and user check-in status** – This view is the default report view and includes:
  - A high-level overview of device status for this policy, and a *View report* button to open a more comprehensive report view.
  - A streamlined representation and count of the different device status values returned by devices assigned to the policy. The simplified bar and chart replace former doughnut charts seen in the prior reporting representation.
- Two other report tiles to open more reports. These tiles include:
  - **Device assignment status** – This report combines the same information as the previous Device status and User status reports, which are no longer available. However, with this change, pivots and drill-in through based on the user name is no longer available.
  - **Per setting status** – This new report provides success metrics for each setting configured differently than the defaults, allowing for new insight to which settings might not be successfully deploying to your organization.
- **Properties** – View details for each configuration page of the policy, including an option to **Edit** each areas profile details.

For more information about reports for update rings for Windows 10 and later, see [Reports for Update rings for Windows 10 and later policy](../protect/windows-update-reports.md#reports-for-update-rings-for-windows-10-and-later-policy) in the Windows Update reports for Microsoft Intune article.

### Role-based access

#### Updating the scope of UpdateEnrollment<!--25077072 -->

With the introduction of a new role **UpdateEnrollment**, the scope of **UpdateOnboarding** is getting updated.

The **UpdateOnboarding** setting for custom and built-in roles is modified to only manage or change the Android Enterprise binding to Managed Google Play and other account-wide configurations. Any built-in roles that used **UpdateOnboarding** will now have **UpdateEnrollmentProfiles** included.

The resource name is being updated from **Android for work** to **Android Enterprise**.

For more information, see [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md).

## Week of September 11, 2023

### Device configuration

#### Introducing Remote Launch on Remote Help<!--9843475 -->

With Remote Launch, the helper can launch Remote Help seamlessly on the helper and user's device from Intune by sending a notification to the user's device. This feature allows both helpdesk and the sharer to be connected to a session quickly without exchanging session codes.

Applies to:

- Windows

For more information, see [Remote Help](remote-help-windows.md).

## Week of September 4, 2023

### Microsoft Intune Suite

#### Remote Help

Version: 5.0.1045.0

With Remote Launch, the helper can launch Remote Help seamlessly on the helper and sharer's device from Intune by sending a notification to the sharer's device.

### Device management

#### Microsoft Intune ending support for Android device administrator on devices with GMS access in August 2024<!--13891824 -->

Microsoft Intune is ending support for [Android device administrator management](../enrollment/android-enroll-device-administrator.md) on devices with access to Google Mobile Services (GMS) on August 30, 2024. After that date, device enrollment, technical support, bug fixes, and security fixes will be unavailable.

If you currently use device administrator management, we recommend switching to another Android management option in Intune before support ends.

For more information, see [Ending support for Android device administrator on GMS devices](https://aka.ms/Intune-Android-DA-blog).

## Week of August 28, 2023

### Device configuration

#### Windows and Android support for 4096-bit key size for SCEP and PFX certificate profiles<!--16314561  -->

Intune [SCEP certificate profiles](../protect/certificates-profile-scep.md) and [PKCS certificate profiles](../protect/certificates-pfx-configure.md) for Windows and Android devices now support a **Key size (bits)** of **4096**. This key size is available for new profiles and existing profiles you choose to edit.

- SCEP profiles have always included the *Key size (bits)* setting and now support 4096 as an available configuration option.
- PKCS profiles don't include the *Key size (bits)* setting directly. Instead, an admin must [modify the certificate template on the Certification Authority](../protect/certificates-pfx-configure.md#configure-certificate-templates-on-the-ca) to set the *Minimum key size* to 4096.

If you use a third-party Certificate Authority (CA), you might need to contact your vendor for assistance with implementing the 4096-bit key size.

When updating or deploying new certificate profiles to take advantage of this new key size, we recommend using a staggered deployment approach. This approach can help avoid creating excessive demand for new certificates across a large number of devices at the same time.

With this update, be aware of the following limitations on Windows devices:

- 4096-bit key storage is supported only in the *Software Key Storage Provider* (KSP). The following don't support storing keys of this size:
  - The hardware TPM (Trusted Platform Module). As a workaround you can use the Software KSP for key storage.
  - Windows Hello for Business. There isn't a workaround at this time.

### Tenant administration

#### Access policies for multiple Administrator Approval are now generally available<!-- 24936423   -->

Access policies for multiple Administrator Approval are out of public preview and are now generally available. With these policies, you can protect a resource, like App deployments, by requiring any change to the deployment to be approved by one of a group of users who are *approvers* for the resource, before that change is applied.

For more information, see [Use Access policies to require multiple administrative approval](multi-admin-approval.md).

## Week of August 21, 2023 (Service release 2308)

### App management

#### Managed Home Screen end-users prompted to grant exact alarm permission<!-- 19804494 -->
Managed Home Screen uses the exact alarm permission to do the following actions:

- Automatically sign out users after a set time of inactivity on the device
- Launch a screen saver after a set period of inactivity
- Automatically relaunch MHS after a certain period of time when a user exits kiosk mode

For devices running Android 14 and higher, by default, the exact alarm permission will be denied. To make sure critical user functionality isn't impacted, end-users are prompted to grant exact alarm permission upon first launch of Managed Home Screen. For more information, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](..\apps\app-configuration-managed-home-screen-app.md) and [Android's developer documentation]( https://developer.android.com/about/versions/14/changes/schedule-exact-alarms).

#### Managed Home Screen notifications<!-- 19805777  -->
For Android devices running Android 13 or higher that target API level 33, by default, applications don't have permission to send notifications. In previous versions of Managed Home Screen, when an admin had enabled automatic relaunch of Managed Home Screen, a notification was displayed to alert users of the relaunch. To accommodate change to notification permission, in the scenario when an admin has enabled auto-relaunch of Managed Home Screen, the application will now display a toast message alerting users of the relaunch. Managed Home Screen is able to auto-grant permission for this notification, so no change is required for admins configuring Managed Home Screen to accommodate the change in notification permission with API level 33. For more information about Android 13 (API level 33) notification messages, see the [Android developer documentation](https://developer.android.com/develop/ui/views/notifications/notification-permission). For more information about Managed Home Screen, see [Configure the Microsoft Managed Home Screen app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

#### New macOS web clip app type<!-- 24128407  -->
In Intune, end users can pin web apps to the dock on your macOS devices (**Apps** > **macOS** > **Add** > **macOS web clip**).

Applies to:

- macOS

For related information about the settings you can configure, see [Add web apps to Microsoft Intune](../apps/web-app.md).

#### Win32 app configurable installation time<!-- 17644704  -->
In Intune, you can set a configurable installation time to deploy Win32 apps. This time is expressed in minutes. If the app takes longer to install than the set installation time, the system will fail the app install. Max timeout value is 1440 minutes (1 day). For more information about Win32 apps, see [Win32 app management in Microsoft Intune](../apps/apps-win32-add.md#step-2-program).

#### Samsung Knox conditional launch check<!-- 8610063   -->
You can add more detection of device health compromises on Samsung Knox devices. Using a conditional launch check within a new Intune App Protection Policy, you can require that hardware-level device tamper detection and device attestation be performed on compatible Samsung devices. For more information, see the **Samsung Knox device attestation** setting in the **Conditional launch** section of [Android app protection policy settings in Microsoft Intune](../apps/app-protection-policy-settings-android.md#device-conditions).

### Device configuration

#### Remote Help for Android in public preview<!-- 16238217 -->
Remote Help is available in public preview for Android Enterprise Dedicated devices from Zebra and Samsung. With Remote Help, IT Pros can remotely view the device screen and take full control in both attended and unattended scenarios, to diagnose and resolve issues quickly and efficiently.

Applies to:

- Android Enterprise Dedicated devices, manufactured by Zebra or Samsung

For more information, see [Remote Help on Android](remote-help-android.md).

#### Group Policy analytics is generally available<!-- 24249203  -->
Group Policy analytics is generally available (GA). Use Group Policy analytics to analyze your on-premises group policy objects (GPOs) for their migration to Intune policy settings.

Applies to:

- Windows 11
- Windows 10

For more information about Group Policy analytics, see [Analyze your on-premises GPOs using Group Policy analytics in Microsoft Intune](../configuration/group-policy-analytics.md).

#### New SSO, login, restrictions, passcode, and tamper protection settings available in the Apple settings catalog<!-- 24335541  -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

There are new settings in the Settings Catalog. To see these settings, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** > **Settings catalog** for profile type.

##### iOS/iPadOS 17.0 and later

**Restrictions**:

- Allow iPhone Widgets On Mac

##### macOS

**Microsoft Defender > Tamper protection**:

- Process's arguments
- Process path
- Process's Signing Identifier
- Process's Team Identifier
- Process exclusions

##### macOS 13.0 and later

**Authentication > Extensible Single Sign On (SSO)**:

- Account Display Name
- Additional Groups
- Administrator Groups
- Authentication Method
- Authorization Right
- Group
- Authorization Group
- Enable Authorization
- Enable Create User At Login
- Login Frequency
- New User Authorization Mode
- Account Name
- Full Name
- Token To User Mapping
- User Authorization Mode
- Use Shared Device Keys

##### macOS 14.0 and later

**Login > Login Window Behavior**:

- Autologin Password
- Autologin Username

**Restrictions**:

- Allow ARD Remote Management Modification
- Allow Bluetooth Sharing Modification
- Allow Cloud Freeform
- Allow File Sharing Modification
- Allow Internet Sharing Modification
- Allow Local User Creation
- Allow Printer Sharing Modification
- Allow Remote Apple Events Modification
- Allow Startup Disk Modification
- Allow Time Machine Backup

**Security > Passcode**:

- Password Content Description
- Password Content Regex

### Device enrollment

#### Just-in-time registration and compliance remediation for iOS/iPadOS Setup Assistant with modern authentication now generally available<!-- 16276610 -->

Just in time (JIT) registration and compliance remediation for Setup Assistant with modern authentication are now out of preview and generally available. With just in time registration, the device user doesn't need to use the Company Portal app for Microsoft Entra registration and compliance checking. JIT registration and compliance remediation are embedded into the user's provisioning experience, so they can view their compliance status and take action within the work app they're trying to access. Also, this establishes single-sign on across the device. For more information about how to set up JIT registration, see [Set up Just in Time Registration](../enrollment/automated-device-enrollment-authentication.md).

#### Awaiting final configuration for iOS/iPadOS automated device enrollment now generally available<!-- 17473384  -->
Now generally available, *awaiting final configuration* enables a locked experience at the end of Setup Assistant to ensure that critical device configuration policies install on devices. The locked experience works on devices targeted with new and existing enrollment profiles. Supported devices include:

- iOS/iPadOS 13+ devices enrolling with Setup Assistant with modern authentication
- iOS/iPadOS 13+ devices enrolling without user affinity
- iOS/iPadOS 13+ devices enrolling with Microsoft Entra ID shared mode

This setting is applied once during the out-of-box automated device enrollment experience in Setup Assistant. The device user doesn't experience it again unless they re-enroll their device.  Awaiting final configuration is enabled by default for new enrollment profiles. For information about how to enable awaiting final configuration, see [Create an Apple enrollment profile](..//enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

### Device management

#### Changes to Android notification permission prompt behavior<!-- 19783177  -->
We've updated how our Android apps handle notification permissions to align with recent changes made by Google to the Android platform.  As a result of Google changes, notification permissions are granted to apps as follows:

- **On devices running Android 12 and earlier**: Apps are permitted to send notifications to users by default.
- **On devices running Android 13 and later**: Notification permissions vary depending on the API the app targets.
  - *Apps targeting API 32 and lower*: Google has added a notification permission prompt that appears when the user opens the app. Management apps can still configure apps so that they're automatically granted notification permissions.
  - *Apps targeting API 33 and higher*: App developers define when the notification permission prompts appear. Management apps can still configure apps so that they're automatically granted notification permissions.

You and your device users can expect to see the following changes now that our apps target API 33:

- **Company Portal used for work profile management**: Users see a notification permission prompt in the personal instance of the Company Portal when they first open it. Users don't see a notification permission prompt in the work profile instance of Company Portal because notification permissions are automatically permitted for Company Portal in the work profile. Users can silence app notifications in the Settings app.
- **Company Portal used for device administrator management**: Users see a notification permission prompt when they first open the Company Portal app.  Users can adjust app notification settings in the Settings app.
- **Microsoft Intune app**: No changes to existing behavior. Users don't see a prompt because notifications are automatically permitted for the Microsoft Intune app.  Users can adjust some app notification settings in the Settings app.
- **Microsoft Intune app for AOSP**: No changes to existing behavior. Users don't see a prompt because notifications are automatically permitted for the Microsoft Intune app.  Users can't adjust app notification settings in the Settings app.

### Device security

#### Defender Update controls to deploy updates for Defender is now generally available<!-- 24666660 -->
The profile **Defender Update controls** for Intune Endpoint security Antivirus policy, which manages update settings for Microsoft Defender, is now generally available. This profile is available for the *Windows 10, Windows 11, and Windows Server* platform. While in public preview, this profile was available for the *Windows 10 and later* platform.

The profile includes settings for the rollout release channel by which devices and users receive Defender Updates that are related to daily security intelligence updates, monthly platform updates, and monthly engine updates.

This profile includes the following settings, which are all directly taken from [Defender CSP - Windows Client Management](/windows/client-management/mdm/policy-csp-Defender).

- Engine Updates Channel
- Platform Updates Channel
- Security Intelligence Updates Channel

These settings are also available from the [settings catalog](../configuration/settings-catalog.md) for the *Windows 10 and later* profile.

#### Elevation report by applications for Endpoint Privilege Management<!-- 24593324 -->
We've released a new report named **Elevation report by applications** for Endpoint Privilege Management (EPM). With [this new report](../protect/epm-reports.md#elevation-report-by-applications) you can view all managed and unmanaged elevations, which are aggregated by the application that elevated. This report can aid you in identifying applications that might require elevation rules to function properly, including rules for child processes.

You'll find the report in the Report node for EPM in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Navigate to **Endpoint security** > **Endpoint Privilege Management** and then select the **Reports** tab.

#### New settings available for macOS Antivirus policy<!-- 24191427 -->
The [Microsoft Defender Antivirus](../protect/endpoint-security-antivirus-policy.md) profile for macOS devices has been updated with nine more settings, and three new settings categories:

**Antivirus engine** – The following settings are new in this category:

- **Degree of parallelism for on-demand scans** – Specifies the degree of parallelism for on-demand scans. This setting corresponds to the number of threads used to perform the scan and impacts the CPU usage, and the duration of the on-demand scan.
- **Enable file hash computation** – Enables or disables file hash computation feature. When this feature is enabled, Windows Defender computes hashes for files it scans. This setting helps improve the accuracy of Custom Indicator matches. However, enabling Enable file hash computation can impact device performance.
- **Run a scan after definitions are updated** – Specifies whether to start a process scan after new security intelligence updates are downloaded on the device. Enabling this setting triggers an antivirus scan on the running processes of the device.
- **Scanning inside archive files** – If true, Defender unpacks archives and scan files inside them. Otherwise archive content is skipped, which improves scanning performance.

**Network protection** – A new category that includes the following setting:

- **Enforcement level** – Configure this setting to specify if network protection is *disabled*, *in audit mode*, or *enforced*.

**Tamper  protection** - A new category that includes the following setting:

- **Enforcement level** - Specify whether tamper protection is *disabled*, in *audit mode*, or *enforced*.

**User interface preferences** – A new category that includes the following settings:

- **Control sign-in to consumer version** - Specify whether users can sign into the consumer version of Microsoft Defender.
- **Show / hide status menu icon** – Specify whether the status menu icon (shown in the top-right corner of the screen) is hidden or not.
- **User initiated feedback** – Specify whether users can submit feedback to Microsoft by going to *Help* > *Send Feedback*.

New profiles that you create include the original settings and the new settings. Your existing profiles automatically update to include the new settings, with each new setting set to *Not configured* until you choose to edit that profile to change it.

For more information about how to set preferences for Microsoft Defender for Endpoint on macOS in enterprise organizations, see [Set preferences for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-preferences?view=o365-worldwide&preserve-view=true).

### Intune apps

#### Newly available protected app for Intune<!-- 24400497  -->
The following protected app is now available for Microsoft Intune:

- VerityRMS by Mackey LLC (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### CloudDesktop log now collected with Windows diagnostics data<!-- 24541366 -->
The Intune remote action to [collect diagnostics](../remote-actions/collect-diagnostics.md) from a Windows device now includes data in a log file.

Log file:
- %temp%\CloudDesktop\*.log

#### Anomaly detection device cohorts in Intune Endpoint analytics is generally available<!-- 24577118  -->
Anomaly detection device cohorts in Intune Endpoint analytics is now generally available.

Device cohorts are identified in devices associated with a high or medium severity anomaly. Devices are correlated into groups based on one or more factors they have in common like an app version, driver update, OS version, device model. A correlation group will contain a detailed view with key information about the common factors between all affected devices in that group. You can also view a breakdown of devices currently affected by the anomaly and 'at risk' devices. "At risk" devices haven't yet shown symptoms of the anomaly.

For more information, see [Anomaly detection in Endpoint analytics](../../analytics/anomaly-detection.md#anomalies-tab).

#### Improved user experience for device timeline in Endpoint Analytics<!-- 24604944 -->
The user interface (UI) for device timeline in Endpoint analytics is improved and includes more advanced capabilities (support for sorting, searching, filtering, and exports). When viewing a specific device timeline in Endpoint analytics, you can search by event name or details. You can also filter the events and choose the source and level of events that appear on the device timeline and select a time range of interest.

For more information, see [Enhanced device timeline](../../analytics/enhanced-device-timeline.md).

#### Updates for compliance policies and reports<!--15425771  -->
We've made several improvements to the Intune compliance policies and reports. With these changes, the reports more closely align to the experience in use for device configuration profiles and reports. We've updated our [compliance report documentation](../protect/compliance-policy-monitor.md) to reflect the available compliance report improvements.

Compliance report improvements include:

- Compliance details for Linux devices.
- Redesigned reports that are up-to-date and simplified, with newer report versions beginning to replace older report versions, which will remain available for some time.
- When viewing a policy for compliance, there isn't a left-pane navigation. Instead, the policy view opens to a single pane that defaults to the Monitor tab and its Device status view.
  - This view provides a high-level overview of device status for this policy, supports drilling in to review the full report, and a per-setting status view of the same policy.
  - The doughnut chart is replaced by a streamlined representation and count of the different device status values returned by devices assigned the policy.
  - You can select the Properties tab to view the policy details, and review and edit its configuration and assignments.
  - The *Essentials* section is removed with those details appearing in the policy's *Properties* tab.
- The updated status reports support sorting by columns, the use of filters, and search. Combined, these enhancements enable you to pivot the report to display specific subsets of details you want to view at that time. With these enhancements, we have removed the *User status* report as it has become redundant. Now, while viewing the default *Device status* report you can focus the report to display the same information that was available from *User status* by sorting on the *User Principal Name* column, or searching for a specific username in the search box.
- When viewing status reports, the count of devices that Intune displays now remains consistent between different report views as you drill in for deeper insights or details.

For more information about these changes, see the Intune Support Team blog at [https://aka.ms/Intune/device_compl_report](https://aka.ms/Intune/device_compl_report).

## Week of August 14, 2023

### App management

#### Use the Turn off the Store application setting to disable end user access to Store apps, and allow managed Intune Store apps<!-- 16544362 -->
In Intune, you can use the new **Store app** type to deploy Store apps to your devices.

Now, you can use the **Turn off the Store application** policy to disable end users' direct access to Store apps. When it's disabled, end users can still access and install Store apps from the Windows Company Portal app and through Intune app management. If you want to allow random store app installs outside of Intune, then don't configure this policy.

The previous **Only display the private store within the Microsoft Store app** policy doesn't prevent end users from directly accessing the store using the Windows Package Manager `winget` APIs. So, if your goal is to block random unmanaged Store application installs on client devices, then it's recommended to use the **Turn off the Store application** policy. Don't use the **Only display the private store within the Microsoft Store app** policy.
Applies to:

- Windows 10 and later

For more information, see [Add Microsoft Store Apps to Microsoft Intune](../apps/store-apps-microsoft.md).

## Week of August 7, 2023

### Role-based access control

#### Introducing a new role-based access control (RBAC) permission under the resource Android for work<!--11298214 -->
Introducing a new RBAC **Permission** for creating a custom role in Intune, under the resource **Android for work**. The permission **Update Enrollment Profile** allows the admin to manage or change both AOSP and Android Enterprise Device Owner enrollment profiles that are used to enroll devices.

For more information, see [Create custom role](create-custom-role.md).

## Week of July 31, 2023

### Device security

### New BitLocker profile for Intune's endpoint security Disk encryption policy<!-- 24631986   -->
We have released a new experience creating new *BitLocker* profiles for endpoint security Disk Encryption policy. The experience for editing your previously created BitLocker policy remains the same, and you can continue to use them. This update applies only for the new [BitLocker](../protect/endpoint-security-disk-encryption-policy.md) policies you create for the *Windows 10 and later* platform.

This update is part of the continuing rollout of new profiles for endpoint security policies, which began in April 2022.

### App management

#### Uninstall Win32 and Microsoft store apps using the Windows Company Portal<!-- 4664389 -->
End-users can uninstall Win32 apps and Microsoft store apps using the Windows Company Portal if the apps were assigned as available and were installed on-demand by the end-users. For Win32 apps, you have the option to enable or disable this feature (off by default). For Microsoft store apps, this feature is always on and available for your end-users. If an app can be uninstalled by the end-user, the end-user will be able to select **Uninstall** for the app in the Windows Company Portal. For related information, see [Add apps to Microsoft Intune](../apps/apps-add.md).

## Week of July 24, 2023 (Service release 2307)

### App management

#### Intune supports new Google Play Android Management API<!-- 10982449 -->
Changes have been made to how Managed Google Play public apps are managed in Intune. These changes are to support [Google's Android Management APIs](https://developers.google.com/android/management) (opens Google's web site).

Applies to:

- Android Enterprise

To learn more about changes to the admin and user experience, see [Support Tip: Intune moving to support new Google Play Android Management API](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-intune-moving-to-support-new-google-play-android/ba-p/3849875).



#### App report for Android Enterprise corporate-owned devices<!-- 2055436  -->
You can now view a report containing all apps found on a device for Android Enterprise corporate-owned scenarios, including system apps. This report is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Monitor** > **Discovered apps**. You'll see **Application Name** and **Version** for all apps detected as installed on the device. It can take up to 24 hours for app information to populate the report.

For related information, see [Intune discovered apps](../apps/app-discovered-apps.md).

#### Add unmanaged PKG-type applications to managed macOS devices [Public Preview]<!-- 17296091  -->
You can now upload and deploy unmanaged PKG-type applications to managed macOS devices using the Intune MDM agent for macOS devices. This feature enables you to deploy custom PKG installers, such as unsigned apps and component packages. You can add a PKG app in the Intune admin center by selecting **Apps** > **macOS** > **Add** > **macOS app (PKG)** for app type.

Applies to:

- macOS

For more information, see [Add an unmanaged macOS PKG app to Microsoft Intune](../apps/macos-unmanaged-pkg.md). To deploy managed PKG-type app, you can continue to [add macOS line-of-business (LOB) apps to Microsoft Intune](../apps/lob-apps-macos.md). For more information about the Intune MDM agent for macOS devices, see [Microsoft Intune management agent for macOS](../apps/lob-apps-macos-agent.md).

#### New settings available for the iOS/iPadOS web clip app type<!-- 21084128   -->
In Intune, you can pin web apps to your iOS/iPadOS devices (**Apps** > **iOS/iPadOS** > **Add** > **iOS/iPadOS web clip**). When you add web clips, there are new settings available:

- **Full screen**: If configured to **Yes**, launches the web clip as a full-screen web app without a browser. There isn't a URL nor search bar, and no bookmarks.
- **Ignore manifest scope**: If configured to **Yes**, a full screen web clip can navigate to an external web site without showing Safari UI. Otherwise, Safari UI appears when navigating away from the web clip's URL. This setting has no effect when **Full screen** is set to **No**. Available in iOS 14 and later.
- **Precomposed**: If configured to **Yes**, prevents Apple's application launcher (SpringBoard) from adding "shine" to the icon.
- **Target application bundle identifier**: Enter the application bundle identifier that specifies the application that opens the URL. Available in iOS 14 and later.

Applies to:

- iOS/iPadOS

For more information, see [Add web apps to Microsoft Intune](../apps/web-app.md).

#### Change to default settings when adding Windows PowerShell scripts<!-- 20986905  -->
In Intune, you can use policies to deploy Windows PowerShell scripts to your Windows devices (**Devices** > **Scripts** > **Add** > **Windows 10 and later**). When you add a Windows PowerShell script, there are settings you configure. To increase secure-by-default behavior of Intune, the default behavior of the following settings has changed:

- The **Run this script using the logged on credentials** setting defaults to **Yes**. Previously, the default was **No**.
- The **Enforce script signature check** setting defaults to **Yes**. Previously, the default was **No**.

This behavior applies to new scripts you add, not existing scripts.

Applies to:

- Windows 10 and later (excluding Windows 10 Home)

For more information about using Windows PowerShell scripts in Intune, see [Use PowerShell scripts on Windows devices in Intune](../apps/powershell-scripts.md).

### Device configuration

#### Added Support for Scope tags<!-- 16485280  -->
You can now add scope tags when creating deployments using Zebra LifeGuard Over-the-Air integration (in public preview).

#### New settings available in the macOS settings catalog<!-- 24167142  -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

**Microsoft AutoUpdate (MAU)**:

- Current Channel (Monthly)

**Microsoft Defender > User interface preferences**:

- Control sign-in to consumer version

**Microsoft Office > Microsoft Outlook**:

- Disable `Do not send response`

**User Experience > Dock**:

- MCX Dock Special Folders

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### Compliance Retrieval service support for MAC address endpoints<!--  24332824  -->
We've now added MAC address support to the Compliance Retrieval service.

The initial release of the CR service included support for using only the Intune device ID with the intent to eliminate the need to manage internal identifiers like serial numbers and MAC addresses. With this update, organizations that prefer to use MAC addresses over certificate authentication can continue to do so while implementing the CR service.

While this update adds MAC address support to the CR service, our recommendation is to use certificate-based authentication with the Intune device ID included in the certificate.

For information about the CR service as a replacement for the Intune Network Access Control (NAC) service, see the Intune blog at [https://techcommunity.microsoft.com/t5/intune-customer-success/new-microsoft-intune-service-for-network-access-control/ba-p/2544696](https://techcommunity.microsoft.com/t5/intune-customer-success/new-microsoft-intune-service-for-network-access-control/ba-p/2544696).

#### Settings insight within Intune security baselines is generally available<!-- 24507891   -->
Announcing the general availability of Settings insight in Microsoft Intune.

The [Settings insight](settings-insight.md) feature adds insight to settings giving you confidence in configurations that have been successfully adopted by similar organizations. Settings insight is currently available for security baselines.

Navigate to **Endpoint security** > **Security baselines**. While creating and editing a workflow, these insights are available for all settings with light bulbs.

### Device security

#### Tamper protection support for Windows on Azure Virtual Desktop<!--15135590  -->
Intune now supports use of endpoint security [Antivirus policy](../protect/endpoint-security-antivirus-policy.md#prerequisites-for-tamper-protection) to manage *Tamper protection* for Windows on Azure Virtual Desktop multi-session devices. Support for Tamper protection requires devices to onboard to Microsoft Defender for Endpoint before the policy that enables Tamper protection is applied.

#### EpmTools PowerShell module for Endpoint Privilege Management<!-- 22800379  -->
The EpmTools PowerShell module is now available for use with Intune Endpoint Privilege Management (EPM). EpmTools includes the cmdlets like **Get-FileAttributes** that you can use to retrieve file details to help build accurate elevation rules, and other cmdlets you can use to troubleshoot or diagnose EPM policy deployments.

For more information, see [EpmTools PowerShell module](../protect/epm-plan.md#epmtools-powershell-module).

#### Endpoint Privilege Management support to manage elevation rules for child processes<!-- 15931887 -->
With Intune Endpoint Privilege Management (EPM) you can manage which files and processes are allowed to *Run as Administrator* on your Windows devices.  Now, EPM [elevation rules](../protect/epm-elevation-rules.md#controlling-child-process-behavior) support a new setting, **Child process behavior**.

With *Child process behavior*, your rules can manage the elevation context for any child processes created by the managed process. Options include:

- Allowing all child processes created by the managed process to always run as elevated.
- Allow a child process to run as elevated only when it matches the rule that manages its parent process.
- Deny all child processes from running in an elevated context, in which case they run as standard users.

Endpoint Privilege Management is available as an Intune add-on. For more information, see [Use Intune Suite add-on capabilities](intune-add-ons.md).

### Intune apps

#### Newly available protected app for Intune<!-- 24323519  -->
The following protected app is now available for Microsoft Intune:

- Dooray! for Intune

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Updated reports for Setting compliance and Policy compliance are in public preview<!-- 15425624, 15425656  -->
We've released two new reports as a public preview for Intune device compliance. You can find these new preview reports in the Intune admin center at **Reports** > **Device compliance** > *Reports* tab:

- [Setting compliance (preview)](reports.md)
- [Policy compliance (preview)](reports.md)

Both reports are new instances of existing reports, and deliver improvements over the older versions, including:

- Details for Linux settings and devices
- Support for sorting, searching, filtering, exports, and paging views
- Drill-down reports for deeper details, which are filtered based on the column you select.
- Devices are represented a single time. This behavior is in contrast to the original reports, which could count a device more than once if multiple users used that device.

Eventually, the [older report versions](../protect/compliance-policy-monitor.md#other-compliance-reports) that are still available in the admin center at *Devices > Monitor* will be retired.

## Week of July 10, 2023

### Microsoft Intune Suite

#### Remote Help

Version: 5.0.1045.0

This version of Remote Help provides support for ARM64 devices including the Microsoft Surface Pro X and Parallels Desktop on macOS.

### App management

#### Updates to app configuration policy reporting<!-- 18098046  -->
As part of our continuing efforts to improve the Intune reporting infrastructure, there have been several user interface (UI) changes for app configuration policy reporting. The UI has been updated with the following changes:

- There isn't a **User status** tile or a **Not applicable device** tile on the **Overview** section of the **App configuration policies** workload.
- There isn't a **User install status** report on the **Monitor** section of the **App configuration policies** workload.
- The **Device install status** report under the **Monitor** section of the **App configuration policies** workload no longer shows the **Pending state** in the **Status** column.

You can configure policy reporting in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Configuration**.

## Week of July 3, 2023

### Device management

#### Intune support for Zebra devices on Android 13<!-- 17192763 -->
Zebra will be releasing support for Android 13 on their devices. You can read more at [Migrating to Android 13](https://techdocs.zebra.com/lifeguard/a13/) (opens Zebra's web site).

- **Temporary issues on Android 13**

  The Intune team thoroughly tested Android 13 on Zebra devices. Everything continues working as normal, except for the following two temporary issues for device administrator (DA) devices.

  For Zebra devices running Android 13 and enrolled with DA management:

  1. App installations don't happen silently. Instead, users get a notification from the Company Portal app (if they allow notifications) that asks for permission to allow the app installation. If a user doesn't accept the app installation when prompted, then the app doesn't install. Users will have a persistent notification in the notification drawer until they allow the installation.

  2. New MX profiles don't apply to Android 13 devices. Newly enrolled Android 13 devices don't receive configuration from MX profiles. MX profiles that previously applied to enrolled devices continue to apply.

  In an update coming later in July, these issues will be resolved and the behavior will return to how it was before.

- **Update devices to Android 13**

  You'll soon be able to use Intune's Zebra LifeGuard Over-the-Air integration to update Android Enterprise dedicated and fully managed devices to Android 13. For more information, see [Zebra LifeGuard Over-the-Air Integration with Microsoft Intune](../protect/zebra-lifeguard-ota-integration.md).

  Before you migrate to Android 13, review [Migrating to Android 13](https://techdocs.zebra.com/lifeguard/a13/) (opens Zebra's web site).

- **OEMConfig for Zebra devices on Android 13**

  OEMConfig for Zebra devices on Android 13 requires using Zebra's new [Zebra OEMConfig Powered by MX OEMConfig app](https://play.google.com/store/apps/details?id=com.zebra.oemconfig.release) (opens the Google Play store). This new app can also be used on Zebra devices running Android 11, but not earlier versions.

  For more information on this app, go to the [New Zebra OEMConfig app for Android 11 and later](https://techcommunity.microsoft.com/t5/intune-customer-success/new-zebra-oemconfig-app-for-android-11-and-later/ba-p/3846730) blog post.

  The [Legacy Zebra OEMConfig app](https://play.google.com/store/apps/details?id=com.zebra.oemconfig.common) (opens the Google Play store) can only be used on Zebra devices running Android 11 and earlier.

For more general information about Intune Android 13 support, go to the [Day Zero support for Android 13 with Microsoft Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/day-zero-support-for-android-13-with-microsoft-intune/ba-p/3601760) blog post.

### Device security

#### Defender for Endpoint security settings management enhancements and support for Linux and macOS in public preview<!-- 14743017, 15319901, 18713045, 18713050, 17757959 17757967, 17758270  -->
With [Defender for Endpoint security settings management](../protect/mde-security-integration.md), you can use Intune's endpoint security policies to manage Defender security settings on devices that onboard to Defender for Endpoint but aren't enrolled with Intune.

Now, you can opt in to a public preview from within the Microsoft Defender portal to gain access to several enhancements for this scenario:

- Intune's endpoint security policies become visible in and can be managed from within the Microsoft Defender portal. This enables security admins to remain in the Defender portal to manage Defender and the Intune endpoint security policies for Defender security settings management.

- Security settings management supports deploying Intune endpoint security Antivirus policies to devices that run Linux and macOS.

- For Windows devices, the Windows Security Experience profile is now supported with security settings management.

- A new onboarding workflow removes the Microsoft Entra hybrid join prerequisite. Microsoft Entra hybrid join requirements prevented many Windows devices from successfully onboarding to Defender for Endpoint security settings management. With this change, those devices can now complete enrollment and start processing policies for security settings management.

- Intune creates a synthetic registration in Microsoft Entra ID for devices that can't fully register with Microsoft Entra ID. Synthetic registrations are device objects created in Microsoft Entra ID that enable devices to receive and report back on Intune policies for security settings management. In addition, should a device with a synthetic registration become fully registered, the synthetic registration is removed from Microsoft Entra ID in deference to the full registration.

If you don't opt in to the Defender for Endpoint Public Preview, the previous behaviors remain in place. In this case, while you can view the Antivirus profiles for Linux, you can't deploy it as its supported only for devices managed by Defender. Similarly, the macOS profile that's currently available for devices enrolled with Intune can't be deployed to devices managed by Defender.

Applies to:

- Linux
- macOS
- Windows

## Week of June 26, 2023

### Device configuration

#### Android (AOSP) supports assignment filters<!-- 7591220 -->
Android (AOSP) supports assignment filters. When you create a filter for Android (AOSP), you can use the following properties:

- DeviceName
- Manufacturer
- Model
- DeviceCategory
- oSVersion
- IsRooted
- DeviceOwnership
- EnrollmentProfileName

For more information on filters, see [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md).

Applies to:

- Android

#### On-demand remediation for a Windows device<!-- 14783338 -->
A new device action that is in public preview allows you to run a remediation on-demand on a single Windows device. The **Run remediation** device action allows you to resolve issues without having to wait for a remediation to run on its assigned schedule. You'll also be able to view the status of remediations under **Remediations** in the **Monitor** section of a device.

The **Run remediation** device action is rolling-out and can take a few weeks to reach all customers.

For more information, see [Remediations](remediations.md).

### Device management

#### Windows Driver update management in Intune is generally available<!-- 5584639  -->
Announcing the general availability of **Windows Driver update management** in Microsoft Intune. With driver update policies, you can view a list of driver updates that are recommended and applicable to your Windows 10 and Windows 11 device that are assigned to the policy. Applicable driver updates are those that can update a device's driver version. Driver update policies update automatically to add new updates as they're published by the driver manufacturer and remove older drivers that no longer apply to any device with the policy.

Update policies can be configured for one of two approval methods:

- With *Automatic approval*, each new *recommended* driver that's published by the driver manufacturer and added to the policy is automatically approved for deployment to applicable devices. Policies set for automatic approvals can be configured with a deferral period before the automatically approved updates are installed on devices. This deferral gives you time to review the driver and to pause its deployment if necessary.

- With *manual approval*, all new driver updates are automatically added to the policy, but an admin must explicitly approve each update before Windows Update deploys it to a device. When you manually approve an update, you choose the date when Windows Update will begin to deploy it to your devices.

To help you manage driver updates, you review a policy and decline an update you don't want to install. You can also indefinitely pause any approved update, and reapprove a paused update to restart its deployment.

This release also includes [driver update reports](../protect/windows-update-reports.md#reports-for-windows-driver-updates-policy) that provide a success summary, per-device update status for each approved driver, and error and troubleshooting information. You can also select an individual driver update and view details about it across all the policies that include that driver version.

To learn about using Windows Driver update policies, see [Manage policy for Windows Driver updates with Microsoft Intune](../protect/windows-driver-updates-overview.md).

Applies to:

- Windows 10
- Windows 11

## Week of June 19, 2023 (Service release 2306)

### Microsoft Intune Suite

#### Remote Help

Version: 4.2.1424.0

With Remote Help 4.2.1424.0, a new in-session connection mode feature provides users with a way to seamlessly switch between full control and view-only modes during a remote assistance session.

### App management

#### MAM for Microsoft Edge for Business [Preview]<!-- 12394345 -->
You can now enable protected MAM access to org data via Microsoft Edge on personal Windows devices. This capability uses the following functionality:

- Intune Application Configuration Policies (ACP) to customize the org user experience in Microsoft Edge
- Intune Application Protection Policies (APP) to secure org data and ensure the client device is healthy when using Microsoft Edge
- Windows Defender client threat defense integrated with Intune APP to detect local health threats on personal Windows devices
- Application Protection Conditional Access to ensure the device is protected and healthy before granting protected service access via Microsoft Entra ID

For more information, see [Preview: App protection policy settings for Windows](../apps/app-protection-policy-settings-windows.md).

To participate in the public preview, [complete the opt-in form](https://aka.ms/MAMforWindowsPublic).

### Device configuration

#### New settings available in the Apple settings catalog<!-- 19951554  -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place. For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **iOS/iPadOS** or **macOS** for platform > **Settings catalog** for profile type.

##### iOS/iPadOS

**Networking > Network Usage Rules**:

- SIM Rules

##### macOS

**Authentication > Extensible Single Sign On (SSO)**:

- Authentication Method
- Denied Bundle Identifiers
- Registration Token

**Full Disk Encryption > FileVault**:

- Output path
- Username
- Password
- UseKeyChain

#### Device Firmware Configuration Interface (DFCI) supports Asus devices <!-- 10249874 -->
For Windows devices, you can create a DFCI profile to manage UEFI (BIOS) settings. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type.

Some Asus devices running Windows are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

For more information about DFCI profiles, see:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](/autopilot/dfci-management)

Applies to:

- Windows 10
- Windows 11

#### Saaswedo Datalert telecom expense management is removed in Intune <!-- 23616707  -->
In Intune, you could manage telecom expenses using Saaswedo's Datalert telecom expense management. This feature is removed from Intune. This removal includes:

- The **Telecom Expense Management** connector

- **Telecom expenses** RBAC category
  - **Read** permission
  - **Update** permission

For more information from Saaswedo, see [The datalert service is unavailable](https://www.saaswedo.com/datalert-service-unavailable) (opens Saaswedo's web site).

Applies to:

- Android
- iOS/iPadOS

#### Settings insight within Intune security baseline<!-- 11127203  -->
The [Settings insight](settings-insight.md) feature adds insights to security baselines giving you confidence in configurations that are successfully adopted by similar organizations.

Navigate to **Endpoint security** > **Security baselines**. When you create and edit the workflow, these insights are available for you in the form of a light bulb.

### Device management

#### New endpoint security Application Control policy in preview<!-- 15711976 -->
As a public preview, you can use a new endpoint security policy category, Application Control. Endpoint security Application Control policy includes:

- Policy to set the Intune Management Extension as a tenant-wide managed installer. When enabled as a managed installer, apps you deploy through Intune (after enablement of Managed Installer) to Windows devices are tagged as installed by Intune. This tag becomes useful when you use Application Control policies to manage which apps you want to allow or block from running on your managed devices.

- Application Control policies that are an implementation of Defender Application Control (WDAC). With Endpoint security Application Control policies, it's easy to configure policy that allows trusted apps to run on your managed devices. Trusted apps are installed by a managed installer or from the App store. In addition to built-in trust settings, these policies also support custom XML for application control so you can allow other apps from other sources to run to meet your organizations requirements.

To get started with using this new policy type, see [Manage approved apps for Windows devices with Application Control policy and Managed Installers for Microsoft Intune](../protect/endpoint-security-app-control-policy.md)

Applies to:

- Windows 10
- Windows 11

#### Endpoint analytics is available to tenants in Government cloud<!-- 8527244  -->
With this release, Endpoint analytics is available to tenants in Government cloud.

Learn more about [endpoint analytics](../../analytics/index.md).

#### Introducing in-session connection mode switch in Remote Help<!-- 10602971  -->
In Remote Help, you can now take advantage of the in-session connection mode switch feature. This feature can help effortlessly transition between full control and view-only modes, granting flexibility and convenience.

For more information on Remote Help, see [Remote Help](remote-help.md).

Applies to:

- Windows

### Device security

#### Update to Endpoint Privilege Management reports<!-- 17727222 -->
Intune's Endpoint Privilege Management (EPM) reports now support exporting the full reporting payload to a CSV file. With this change, you can now export all events from an elevation report in Intune.

#### Endpoint Privilege Managements run with elevated access option now available on the top-level menu for Windows 11<!-- 17749664  -->
The Endpoint Privilege Management option to *Run with elevated access* is now available as a top-level right-click option on Windows 11 devices. Previous to this change, standard users were required to select *Show more options* to view the *Run with elevated access* prompt on Windows 11 devices.

[Endpoint Privilege Management](../protect/epm-overview.md) is available as an Intune add-on. For more information, see [Use Intune Suite add-on capabilities](intune-add-ons.md).

Applies to:

- Windows 11

### Intune apps

#### Newly available protected apps for Intune<!-- 23027634, 21159364, 21234187, 21237641, 20771088  -->
The following protected apps are now available for Microsoft Intune:

- Idenprotect Go by Apply Mobile Ltd (Android)
- LiquidText by LiquidText, Inc. (iOS)
- MyQ Roger: OCR scanner PDF by MyQ spol. s r.o.
- CiiMS GO by Online Intelligence (Pty) Ltd
- Vbrick Mobile by Vbrick Systems

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Microsoft Intune troubleshooting pane is now generally available<!-- 18099474 -->
The Intune troubleshooting pane is now generally available.  It provides details about user's devices, policies, applications, and status. The troubleshooting pane includes the following information:

- A summary of policy, compliance, and application deployment status.
- Support for exporting, filtering, and sorting all reports.
- Support to filter by excluding policies and applications.
- Support to filter to a user's single device.
- Details about available device diagnostics and disabled devices.
- Details about offline devices that haven't checked-in to the service for three or more days.

You can find the troubleshooting pane in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Troubleshoot**.

#### Updated troubleshoot + support pane in Intune<!-- 16240430  -->
The **Troubleshooting + support** pane in the Intune admin center has been updated by consolidating the **Roles and Scopes** report into a single report. This report now includes all relevant role and scope data from both Intune and Microsoft Entra ID, providing a more streamlined and efficient experience. For related information, see [Use the troubleshooting dashboard to help users at your company](help-desk-operators.md).

#### Download mobile app diagnostics<!-- 22139638  -->
Now generally available, access user-submitted mobile app diagnostics in the Intune admin center, including app logs sent through Company Portal apps, which include Windows, iOS, Android, Android AOSP, and macOS. In addition, you can retrieve app protection logs via Microsoft Edge. For more information, see [Company Portal app logs](../apps/company-portal-app.md#app-logs) and [Use Microsoft Edge for iOS and Android to access managed app logs](../apps/manage-microsoft-edge.md#use-microsoft-edge-for-ios-and-android-to-access-managed-app-logs).

## Week of June 12, 2023

### Device management

#### New Devices from HTC and Pico supported on Microsoft Intune for Android Open Source Devices<!-- 24271568 -->
Microsoft Intune for Android open source project devices (AOSP) now supports the following devices:

- HTC Vive XR Elite
- Pico Neo 3 Pro
- Pico 4

For more information, see:

- [Operating systems and browsers supported by Microsoft Intune](supported-devices-browsers.md)

- [Android Open Source Project Supported Devices](android-os-project-supported-devices.md)

Applies to:

- Android (AOSP)

### App management

#### Microsoft Store for Business or Microsoft Store for Education<!-- 24250535 -->
Apps added from the Microsoft Store for Business or Microsoft Store for Education won't deploy to devices and users. Apps show as "not applicable" in reporting. Apps already deployed are unaffected. Use the [new Microsoft Store app](../apps/store-apps-microsoft.md) to deploy Microsoft Store apps to devices or users. For related information, see [Adding your Microsoft Store for Business and Education apps to the Microsoft Store in Intune](https://aka.ms/Intune/MSfB-support) for upcoming dates when Microsoft Store for Business apps will no longer deploy and Microsoft Store for Business apps will be removed.

For more information, see the following resources:

- [Update to Intune integration with the Microsoft Store on Windows](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/update-to-intune-integration-with-the-microsoft-store-on-windows/ba-p/3585077)
- [Embracing the Future of Microsoft Store with Intune: A Step-by-Step Guide](https://www.youtube.com/watch?v=c534X9yMvDo)
- [Embracing the Future of Microsoft Store with Intune for Education: A Step-by-Step Guide](https://www.youtube.com/watch?v=Heoi0RuClQM)

## Week of June 5, 2023

### Device configuration

### Android Enterprise 11+ devices can use Zebra's latest OEMConfig app version<!-- 8675347 -->

On Android Enterprise devices, you can use OEMConfig to add, create, and customize OEM-specific settings in Microsoft Intune (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **OEMConfig**).

There's a new **Zebra OEMConfig Powered by MX** OEMConfig app that aligns more closely to Google's standards. This app supports Android Enterprise 11.0 and newer devices.

The older **Legacy Zebra OEMConfig** app continues to support devices with Android 11 and earlier.

In your Managed Google Play, there are two versions of Zebra OEMConfig app. Be sure to select the correct app that applies to your Android device versions.

For more information on OEMConfig and Intune, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Applies to:

- Android Enterprise 11.0 and newer

## Week of May 29, 2023

### Device management

#### Intune UI displays Windows Server devices as distinct from Windows clients for the Security Management for Microsoft Defender for Endpoint scenario<!-- 16882836 -->
To support the [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md) (MDE security configuration) scenario, Intune now differentiates Windows devices in Microsoft Entra ID as either *Windows Server* for devices that run Windows Server, or as *Windows* for devices that run Windows 10 or Windows 11.

With this change, you can improve policy targeting for MDE security configuration. For example, you can use dynamic groups that consist of only Windows Server devices, or only Windows client devices (Windows).

For more information about this change, see the Intune Customer Success blog [Windows Server devices now recognized as a new OS in Microsoft Intune, Microsoft Entra ID, and Defender for Endpoint
](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-windows-server-devices-will-now-be-identified-as-a/ba-p/3767773).

### Tenant administration

#### Organizational messages for Windows 11 now generally available<!-- 15272978 -->
Use organizational messages to deliver branded, personalized call-to-actions to employees. Select from more than 25 messages that support employees through device onboarding and lifecycle management, in 15 different languages. Messages can be assigned to Microsoft Entra user groups. They're shown just above the taskbar, in the notifications area, or in the Get started app on devices running Windows 11. Messages continue to appear or reappear based on the frequency you configure in Intune, and until the user has visited the customized URL.

Other features and functionality added in this release include:

- Confirm licensing requirements prior to first message.
- Choose from eight new themes for taskbar messages.
- Give messages a custom name.
- Add scope groups and scope tags.
- Edit the details of a scheduled message.

Scope tags were previously unavailable for organizational messages. With the addition of scope tag support, Intune adds the default scope tag to every message created before June 2023. Admins that want access to those messages must be associated with a role that has the same tag. For more information about available features and how to set up organizational messages, see
[Overview of organizational messages](/microsoft-365/admin/misc/organizational-messages-microsoft-365).

## Week of May 22, 2023 (Service release 2305)

### App management

#### Update to macOS shell scripts maximum running time limit<!-- 23187517 -->
Based on customer feedback, we're updating the Intune agent for macOS (version 2305.019) to extend the maximum script run time to 60 minutes. Previously, the Intune agent for macOS only allowed shell scripts to run for up to 15 minutes before reporting the script as a failure. The Intune agent for macOS 2206.014 and higher supports the 60-minute timeout.

#### Assignment filters support app protection policies and app configuration policies<!-- 7476247 -->
Assignment filters support MAM app protection policies and app configuration policies. When you create a new filter, you can fine tune MAM policy targeting using the following properties:

- Device Management Type
- Device Manufacturer
- Device Model
- OS Version
- Application Version
- MAM Client Version

> [!IMPORTANT]
> All new and edited app protection policies that use **Device Type** targeting are replaced with assignment filters.

For more information on filters, see [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md).

#### Update to MAM reporting in Intune<!-- 10100428  -->
MAM reporting has been simplified and overhauled, and now uses Intune's newest reporting infrastructure. Benefits of this include improved data accuracy and instantaneous updating. You can find these streamlined MAM reports in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **Monitor**. All MAM data available to you is contained within the new **App protection status** report and **App configuration status** report.

#### Global quiet time app policy settings<!-- 15424417   -->
The global quiet time settings allow you to create policies to schedule quiet time for your end users. These settings automatically mute Microsoft Outlook email and Teams notifications on iOS/iPadOS and Android platforms. These policies can be used to limit end user notifications received after work hours. For more information, see [Quiet time notification policies](../apps/app-office-policies.md#quiet-time-notification-policies).

### Device configuration

#### Introducing enhanced chat in Remote Help<!-- 10602997 -->
Introducing enhanced chat with Remote Help. With the new and enhanced chat you can maintain a continuous thread of all messages. This chat provides support for special characters and other languages including Chinese and Arabic.

For more information on Remote Help, see [Remote Help](remote-help.md).

Applies to:

- Windows

#### Remote Help administrators can reference audit log sessions<!-- 9052185  -->
For Remote Help, in addition to existing session reports, administrators can now reference audit logs sessions created in Intune. This feature enables administrators to reference past events for troubleshooting and analyzing log activities.

For more information on Remote Help, see [Remote Help](remote-help.md).

Applies to:

- Windows 10
- Windows 11

#### Turn on/off Personal data encryption on Windows 11 devices using the settings catalog<!-- 10346018  -->
The settings catalog includes hundreds of settings that you can configure and deploy to your devices.

In the settings catalog, you can turn on/off **Personal data encryption** (PDE). PDE is a security feature introduced in Windows 11 version 22H2 that provides more encryption features for Windows.

PDE is different than BitLocker. PDE encrypts individual files and content, instead of whole volumes and disks. You can use PDE with other encryption methods, such as BitLocker.

For more information on the settings catalog, see:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS and macOS devices](../configuration/settings-catalog.md)
- [Common Tasks you can complete using the Settings Catalog in Intune](../configuration/settings-catalog-common-features.md)

This feature applies to:

- Windows 11

#### Visual Studio ADMX settings are in the Settings Catalog and Administrative Templates <!-- 10875730 -->
Visual Studio settings are included in the Settings Catalog and Administrative Templates (ADMX). Previously, to configure Visual Studio settings on Windows devices, you imported them with ADMX import.

For more information on these policy types, see:

- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)
- [Use Windows templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md)
- [Visual Studio Administrative Templates (ADMX)](/visualstudio/install/administrative-templates)

Applies to:

- Windows 10
- Windows 11

#### Group policy analytics supports scope tags<!-- 12714882  -->
In Group Policy analytics, you import your on-premises GPO. The tool analyzes your GPOs and shows the settings that can (and can't) be used in Intune.

When you import your GPO XML file in Intune, you can select an existing scope tag. If you don't select a scope tag, then the **Default** scope tag is automatically selected. Previously, when you imported a GPO, the scope tags assigned to you were automatically applied to the GPO.

Only admins within that scope tag can see the imported policies. Admins not in that scope tag can't see the imported policies.

Also, admins within their scope tag can migrate the imported policies that they have permissions to see. To migrate an imported GPO into a Settings Catalog policy, a scope tag must be associated with the imported GPO. If a scope tag isn't associated, then it can't migrate to a Settings Catalog policy. If no scope tag is selected, then a default scope tag is automatically applied.

For more information on scope tags and Group Policy analytics, see:

- [Analyze your on-premises GPOs using Group Policy analytics in Microsoft Intune](../configuration/group-policy-analytics.md)
- [Create a Settings Catalog policy using your imported GPOs](../configuration/group-policy-analytics-migrate.md)
- [Use role-based access control (RBAC) and scope tags for distributed IT](scope-tags.md)

#### Introducing Intune integration with the Zebra Lifeguard Over-the-Air service (public preview)<!-- 14340034  -->
Now available in public preview, Microsoft Intune supports integration with Zebra Lifeguard Over-the-Air service, which allows you to deliver OS updates and security patches over-the-air to eligible Zebra devices that are enrolled with Intune. You can select the firmware version you want to deploy, set a schedule, and stagger update downloads and installs. You can also set minimum battery, charging status, and network conditions requirements for when the update can happen.

Available for Android Enterprise Dedicated and Fully Managed Zebra devices that are running Android 8 or later, and requires an account with Zebra.

#### New Google domain allowlist settings for Android Enterprise personally owned devices with a work profile<!-- 14711684 -->
On Android Enterprise personally owned devices with a work profile, you can configure settings that restrict device features and settings.

Currently, there's an **Add and remove accounts** setting that can allow Google accounts be added to the work profile. For this setting, when you select **Allow all accounts types**, you can also configure:

- **Google domain allow-list**:  Restricts users to add only certain Google account domains in the work profile. You can import a list of allowed domains or add them in the admin center using the `contoso.com` format. When left blank, by default, the OS might allow adding all Google domains in the work profile.

For more information on the settings you can configure, see [Android template device settings list to restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:

- Android Enterprise personally owned devices with a work profile

#### Renaming Proactive remediation to Remediations and moving to a new location<!-- 16526263  -->
Proactive remediations are now Remediations and are available from **Devices** > **Remediations**. You can still find Remediations in both the new location and the existing **Reports** > **Endpoint Analytics** location until the next Intune service update.

Remediations are currently not available in the new [Devices experience preview](public-preview.md).

Applies to:

- Windows 10
- Windows 11

#### Remediations are now available in Intune for US Government GCC High and DoD<!-- 16526300 -->
Remediations (previously known as proactive remediations) are now available in [Microsoft Intune for US Government GCC High and DoD](intune-govt-service-description.md).

Applies to:

- Windows 10
- Windows 11

#### Create inbound and outbound network traffic rules for VPN profiles on Windows devices<!-- 17943658 -->
> [!NOTE]
> This setting is coming in a future release, possibly the 2308 Intune release.

You can create a device configuration profile that deploys a VPN connection to devices (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **VPN** for profile type).

In this VPN connection, you can use the **Apps and Traffic rules** settings to create network traffic rules.

There's a new **Direction** setting you can configure. Use this setting to allow Inbound and Outbound traffic from the VPN connection:

- **Outbound** (default): Allows only traffic to external networks/destinations to flow using the VPN. Inbound traffic is blocked from entering the VPN.
- **Inbound**: Allows only traffic coming from external networks/ sources to flow using the VPN. Outbound traffic is blocked from entering the VPN.

For more information on the VPN settings you can configure, including the network traffic rule settings, see [Windows device settings to add VPN connections using Intune](../configuration/vpn-settings-windows-10.md).

Applies to:

- Windows 10 and later

#### New settings available in the macOS settings catalog <!-- 18430228  -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

**Microsoft Defender > Antivirus engine**:

- Scanning inside archive files
- Enable file hash computation

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, see [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### Wipe device action and new obliteration behavior setting available for macOS<!-- 16647226 -->
You can now use the **Wipe** device action instead of Erase for macOS devices. You can also configure the **Obliteration Behavior** setting as part of the **Wipe** action.

This new key allows you to control the wipe fallback behavior on Macs that have Apple Silicon or the T2 Security Chip. To find this setting, navigate to **Devices** > **By platform** > **macOS** > [Select a device] > **Overview** > **Wipe** in the **Device action** area.

For more information on the Obliteration Behavior setting, go to Apple's Platform Deployment site [Erase Apple devices - Apple Support](https://support.apple.com/guide/deployment/erase-devices-dep0a819891e/web).

Applies to:

- macOS

### Device enrollment

#### Account driven Apple User Enrollment available for iOS/iPadOS 15+ devices (public preview)<!-- 14161683  -->
Intune supports account driven user enrollment, a new and improved variation of Apple User Enrollment for iOS/iPadOS 15+ devices. Now available for public preview, the new option utilizes just-in-time registration, which eliminates the need for the Company Portal app during enrollment. Device users can initiate enrollment directly in the Settings app, resulting in a shorter and more efficient onboarding experience. You can continue to target iOS/iPadOS devices using the existing profile-based user enrollment method that uses Company Portal. Devices running iOS/iPadOS, version 14.8.1 and earlier remain unaffected by this update and can continue to use the existing method. For more information, see [Set up account driven Apple User Enrollment](../enrollment/apple-account-driven-user-enrollment.md).

### Device security

#### New security baseline for Microsoft 365 Office Apps<!-- 9587103  -->
We've released a new security baseline to help you manage security configurations for **M365 Office Apps**. This new baseline uses an updated template and experience that uses the unified settings platform seen in the Intune settings catalog. You can view the list of settings in the new baseline at [Microsoft 365 Apps for Enterprise baseline settings (Office)](../protect/security-baseline-v2-office-settings.md).

The new Intune security baseline format aligns the presentation of settings that are available to the settings found in the Intune settings catalog. This alignment helps resolve past issues for setting names and implementations for settings that could create conflicts. The new format also improves the reporting experience for baselines in the Intune admin center.

The Microsoft 365 Office Apps baseline can help you rapidly deploy configurations to your Office Apps that meet the security recommendations of the Office and security teams at Microsoft. As with all baselines, the default baseline represents the recommended configurations. You can modify the default baseline to meet the requirements of your organization.

To learn more, see [Security baselines overview](../protect/security-baselines.md).

Applies to:

- Windows 10
- Windows 11

#### Security baseline update for Microsoft Edge version 112<!-- 3408610  -->
We've released a new version of the Intune security baseline for Microsoft Edge, version 112. In addition to releasing this new version for Microsoft Edge, the new baseline uses an updated template experience that uses the unified settings platform seen in the Intune settings catalog. You can view the list of settings in the new baseline at [Microsoft Edge baseline settings (version 112 and higher)](../protect/security-baseline-v2-edge-settings.md).

The new Intune security baseline format aligns the presentation of settings that are available to the settings found in the Intune settings catalog. This alignment helps resolve past issues for setting names and implementations for settings that could create conflicts. The new format also improves the reporting experience for baselines in the Intune admin center.

Now that the new baseline version is available, all new profiles you create for Microsoft Edge use the new baseline format and version. While the new version becomes the default baseline version, you can continue to use the profiles you've previously created for older versions of Microsoft Edge. But, you can't create new profiles for those older versions of Microsoft Edge.

To learn more, see [Security baselines overview](../protect/security-baselines.md).

Applies to:

- Windows 10
- Windows 11

### Intune apps

#### Newly available protected apps for Intune<!-- 17782795, 17782816, 17851777, 17644967, 17948005, 17971727 -->
The following protected apps are now available for Microsoft Intune:

- Achievers by Achievers Inc.
- Board.Vision for iPad by Trusted Services PTE. LTD.
- Global Relay by Global Relay Communications Inc.
- Incorta (BestBuy) by Incorta, Inc. (iOS)
- Island Enterprise Browser by Island (iOS)
- Klaxoon for Intune by Klaxoon (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

## Week of May 8, 2023

### Device configuration

#### Device Firmware Configuration Interface (DFCI) supports Dynabook devices<!-- 10249859 -->
For Windows devices, you can create a DFCI profile to manage UEFI (BIOS) settings. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Windows 10 and later** for platform > **Templates** > **Device Firmware Configuration Interface** for profile type.

Some Dynabook devices running Windows are enabled for DFCI. Contact your device vendor or device manufacturer for eligible devices.

For more information about DFCI profiles, see:

- [Configure Device Firmware Configuration Interface (DFCI) profiles on Windows devices in Microsoft Intune](../configuration/device-firmware-configuration-interface-windows.md)
- [Device Firmware Configuration Interface (DFCI) management with Windows Autopilot](/autopilot/dfci-management)

Applies to:

- Windows 10
- Windows 11

#### eSIM bulk activation for Windows PCs via download server is now available on the Settings Catalog<!-- 19809114 -->
You can now perform at-scale configuration of Windows eSIM PCs using the Settings Catalog. A download server (SM-DP+) is configured using a configuration profile.

Once the devices receive the configuration, they automatically download the eSIM profile. For more information, see [eSIM configuration of a download server](../configuration/esim-device-configuration-download-server.md).

Applies to:

- Windows 11
- eSIM capable devices

## Week of May 1, 2023

### App management

#### macOS shell scripts maximum running time limit<!-- 19396575 -->
We have fixed an issue that caused Intune tenants with long-running shell scripts to not report back on the script run status. The macOS Intune agent stops any macOS shell scripts that run longer than 15 minutes. These scripts report as failed. The new behavior is enforced from macOS Intune agent version 2305.019.

#### DMG app installation for macOS<!-- 13911806 -->
The DMG app installation feature for macOS is now generally available. Intune supports **required** and **uninstall** assignment types for DMG apps. The Intune agent for macOS is used to deploy DMG apps.

#### Deprecation of Microsoft Store for Business and Education<!-- 19677954 -->
The Microsoft Store for Business connector is no longer available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Apps added from the Microsoft Store for Business or Microsoft Store for Education won't sync with Intune. Apps that have previously synced continue to be available and deploy to devices and users.

It's now also possible to delete Microsoft Store for Business apps from the **Apps** pane in the Microsoft Intune admin center so that you can clean up your environment as you move to the new Microsoft Store app type.

For related information, see [Adding your Microsoft Store for Business and Education apps to the Microsoft Store in Intune](https://aka.ms/Intune/MSfB-support) for upcoming dates when Microsoft Store for Business apps won't deploy and Microsoft Store for Business apps are removed.

### Device configuration

#### Remote Help now supports Conditional Access capability<!--16108299 -->
Administrators can now utilize Conditional Access capability when setting up policies and conditions for Remote Help. For example, multifactor authentication, installing security updates, and locking access to Remote Help for a specific region or IP addresses.

For more information, see:

- [Conditional Access](../protect/conditional-access.md)
- [Remote Help](remote-help-windows.md#set-up-conditional-access-for-remote-help)

### Device security

#### Updated settings for Microsoft Defender in endpoint security Antivirus policy<!-- 19991301  -->
We've updated the available settings in the *Microsoft Defender Antivirus* profile for endpoint security Antivirus policy.  You can find this profile in the Intune admin center at **Endpoint security** > **Antivirus** > *Platform:* **Windows 10, Windows 11, and Windows Server**  > *Profile:* **Microsoft Defender Antivirus**.

- **The following settings have been added**:

  - Metered Connection Updates
  - Disable Tls Parsing
  - Disable Http Parsing
  - Disable Dns Parsing
  - Disable Dns Over Tcp Parsing
  - Disable Ssh Parsing
  - Platform Updates Channel
  - Engine Updates Channel
  - Security Intelligence Updates Channel
  - Allow Network Protection Down Level
  - Allow Datagram Processing On Win Server
  - Enable Dns Sinkhole

  For more information about these settings, see the [Defender CSP]( /windows/client-management/mdm/Defender-csp?WT.mc_id=Portal-fx).
The new settings are also available through the Intune [Settings Catalog](../configuration/settings-catalog.md).

- **The following setting has been deprecated**:

  - Allow Intrusion Prevention System

  This setting now appears with the *Deprecated* tag. If this deprecated setting was previously applied on a device, the setting value is updated to *NotApplicable* and has no effect on the device. If this setting is configured on a device, there's no effect on the device.

Applies to:

- Windows 10
- Windows 11

### Microsoft Intune Suite

#### Remote Help

Version: 4.2.1270.0

This version includes a minor update that enables future functionality.

- Added support for slashes within the Remote Help URI (to enable future functionality)

## Week of April 17, 2023 (Service release 2304)

### App management

#### Changes to iCloud app backup and restore behavior on iOS/iPadOS and macOS devices<!-- 16261392  -->
As an app setting, you can select to **Prevent iCloud app backup** for iOS/iPadOS and macOS devices. You can *not* backup managed App Store apps and line-of-business (LOB) apps on iOS/iPadOS, as well as managed App Store apps on macOS devices (macOS LOB apps don't support this feature), for both user and device licensed VPP/non-VPP apps. This update includes both new and existing App Store/LOB apps sent with and without VPP that are being added to Intune and targeted to users and devices.

Preventing the backup of the specified managed apps ensures that these apps can be properly deployed via Intune when the device is enrolled and restored from backup. If the admin configures this new setting for new or existing apps in their tenant, then managed apps can and will be reinstalled for devices. But, Intune doesn't allow them to be backed up.

This new setting appears in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by modifying the properties of an app. For an existing app, you can select **Apps** > **iOS/iPadOS** or **macOS** > *select the app* > **Properties** > Assignment **Edit**. If no group assignment has been set, select **Add group** to add a group. Modify either the setting under **VPN**, **Uninstall on device removal**, or **Install as removable**. Then, select **Prevent iCloud app backup**. The **Prevent iCloud app backup** setting is used to prevent backup of app data for the application. Set to **No** to allow the app to be backed up by iCloud.

For more information, see [Changes to applications' backup and restore behavior on iOS/iPadOS and macOS devices](https://techcommunity.microsoft.com/t5/intune-customer-success/changes-to-applications-backup-and-restore-behavior-on-ios/ba-p/3692064) and [Assign apps to groups with Microsoft Intune](../apps/apps-deploy.md).

#### Prevent automatic updates for Apple VPP apps<!-- 16876430   -->
You can control the automatic update behavior for Apple VPP at the per-app assignment level using the **Prevent automatic updates** setting. This setting is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Apps** > **iOS/iPadOS** or **macOS** > *Select a volume purchase program app* > **Properties** > **Assignments** > *Select a Microsoft Entra group* > **App settings**.

Applies to:

- iOS/iPadOS
- macOS

### Device configuration

#### Updates to the macOS Settings Catalog <!-- 17673709  -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

A new setting is available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

The new setting is located under:

**Microsoft AutoUpdate (MAU) > [targeted app]**:

- Update channel override

The following settings have been deprecated:

**Microsoft AutoUpdate (MAU) > [targeted app]**:

- Channel Name (Deprecated)

**Privacy > Privacy Preferences Policy Control > Services > Listen Event or Screen Capture**:

- Allowed

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### The Microsoft Enterprise SSO plug-in for Apple devices is now generally available<!-- 17826329  -->
In Microsoft Intune, there's a Microsoft Enterprise SSO plug-in. This plug-in provides single sign-on (SSO) to iOS/iPadOS and macOS apps and websites that use Microsoft Entra ID for authentication.

This plug-in is now generally available (GA).

For more information about configuring the Microsoft Enterprise SSO plug-in for Apple devices in Intune, go to [Microsoft Enterprise SSO plug-in in Microsoft Intune](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md).

Applies to:

- iOS/iPadOS
- macOS

#### Disable Activation Lock device action for supervised macOS devices<!-- 16813146  -->
You can now use the **Disable Activation Lock** device action in Intune to bypass Activation Lock on Mac devices without requiring the current username or password. This new action is available in **Devices** > **By platform** > **macOS** > select one of your listed devices > **Disable Activation Lock**.

More information on managing Activation Lock is available at [Bypass iOS/iPadOS Activation Lock with Intune](../remote-actions/device-activation-lock-disable.md) or on Apple's website at [Activation Lock for iPhone, iPad, and iPod touch - Apple Support](https://support.apple.com/en-us/HT201365).

Applies to:

- macOS 10.15 or later

#### ServiceNow Integration is now Generally Available (GA)<!-- 18163832  -->
Now generally available, you can view a list of ServiceNow incidents associated with the user you've selected in the Intune Troubleshooting workspace. This new feature is available under **Troubleshooting + Support** > select a user > **ServiceNow Incidents**. The incidents shown have a direct link back to the source incident and show key information from the incident. All incidents listed link the "Caller" identified in the incident with the user selected for Troubleshooting.

For more information, go to [Use the troubleshooting portal to help users at your company](service-now-integration.md).

#### More permissions to support administrators in controlling delivery of organization messages<!-- 16982298  -->
With more permissions administrators can control delivery of content created and deployed from Organizational messages and the delivery of content from Microsoft to users.

The **Update organizational message control** RBAC permission for organizational messages determines who can change the Organizational Messages toggle to allow or block Microsoft direct messages. This permission is also added to the **Organizational Messages Manager** built-in role.

Existing custom roles for managing Organizational Messages must be modified to add this permission for users to modify this setting.

- For more information, about role-based access control (RBAC), see [RBAC with Microsoft Intune](role-based-access-control.md).
- For more information, about prerequisites for organization messages, see [Organizational messages prerequisites](/microsoft-365/admin/misc/organizational-messages-microsoft-365#role-based-access-control-requirements).

### Device management

#### Endpoint security firewall rules support for ICMP type<!-- 5653356  -->
You can now use the **IcmpTypesAndCodes** setting to configure inbound and outbound rules for [Internet Control Message Protocol](/windows/security/threat-protection/windows-firewall/create-an-inbound-icmp-rule) (ICMP) as part of a firewall rule. This setting is available in the [*Microsoft Defender Firewall rules*](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune) profile for the *Windows 10, Windows 11, and Windows Server* platform.

Applies to:

- Windows 11 and later

#### Manage Windows LAPS with Intune policies (public preview)<!-- 11890571  -->
Now available in a public preview, manage Windows Local Administrator Password Solution (Windows LAPS) with Microsoft Intune [Account protection policies](../protect/endpoint-security-account-protection-policy.md). To get started, see [Intune support for Windows LAPS](../protect/windows-laps-overview.md).

[Windows LAPS](/windows-server/identity/laps/laps-overview) is a Windows feature that allows you to manage and backs up the password of a local administrator account on your Microsoft Entra joined or Windows Server Active Directory-joined devices.

To manage LAPS, Intune configures the Windows [LAPS configuration service provider](/windows/client-management/mdm/LAPS-csp) (CSP) that is built in to Windows devices. It takes precedence over other sources of Windows LAPS configurations, like GPOs or the Microsoft Legacy LAPS tool. Some of the capabilities you can use when Intune manages Windows LAPS include:

- Define password requirements like complexity and length that apply to the local administrator accounts on a device.
- Configure devices to rotate their local admin account passwords on a schedule. And, back up the account and password in your Microsoft Entra ID or on-premises Active Directory.
- Use an Intune device action from the admin center to manually rotate the password for an account on your own schedule.
- View account details from within the Intune admin center, like the account name and password. This information can help you recover devices that are otherwise inaccessible.
- Use Intune reports to monitor your LAPS policies, and when devices last rotated passwords manually or by schedule.

Applies to:

- Windows 10
- Windows 11

#### New settings available for macOS software update policies<!-- 16646756  -->
macOS software update policies now include the following settings to help manage when updates install on a device. These settings are available when the *All other updates* update type is configured to *Install later*:

- **Max User Deferrals**:  When the *All other updates* update type is configured to *Install later*, this setting allows you to specify the maximum number of times a user can postpone a minor OS update before it's installed. The system prompts the user once a day. Available for devices running macOS 12 and later.

- **Priority**: When the *All other updates* update type is configured to *Install later*, this setting allows you to specify values of *Low* or *High* for the scheduling priority for downloading and preparing minor OS updates. Available for devices running macOS 12.3 and later.

For more information, see [Use Microsoft Intune policies to manage macOS software updates](../protect/updates/software-updates-macos.md).

Applies to:

- macOS

#### Introducing the new partner portals page<!-- 17829024  -->
You can now manage hardware specific information on your HP or Surface devices from our partner portals page.

The HP link takes you to HP Connect where you can update, configure, and secure the BIOS on your HP devices.
The Microsoft Surface link takes you to the Surface Management Portal where you can get insights into device compliance, support activity, and warranty coverage.

To access the Partner portals page, you must enable the Devices pane preview and then navigate to **Devices** > **Partner Portals**.

#### Windows Update compatibility reports for Apps and Drivers are now generally available<!-- 17917026  -->
The following Microsoft Intune reports for [Windows Update compatibility](../protect/windows-update-compatibility-reports.md) are out of preview and now generally available:

- **Windows feature update device readiness report** - This report provides per-device information about compatibility risks that are associated with an upgrade or update to a chosen version of Windows.

- **Windows feature update compatibility risks report** - This report provides a summary view of the top compatibility risks across your organization for a chosen version of Windows. You can use this report to understand which compatibility risks impact the greatest number of devices in your organization.

These reports can help you plan an upgrade from Windows 10 to 11, or for installing the latest Windows feature update.

### Device security

#### Microsoft Intune Endpoint Privilege Management is generally available<!--1564177  -->
Microsoft Endpoint Privilege Management (EPM) is now generally available and no longer in preview.

With [Endpoint Privilege Management](../protect/epm-overview.md), admins can set policies that allow standard users to perform tasks normally reserved for an administrator. To do so, you configure policies for *automatic* and *user-confirmed* workflows that elevate the run-time permissions for apps or processes you select. You then assign these policies to users or devices that have end users running without Administrator privileges. After the device receives a policy, EPM brokers the elevation on behalf of the user, allowing them to elevate approved applications without needing full administrator privileges. EPM also includes built-in insights and reporting.

Now that EPM is out of preview, it requires another license to use. You can choose between a stand-alone license that adds only EPM, or license EPM as part of the Microsoft Intune Suite. For more information, see [Use Intune Suite add-on capabilities](intune-add-ons.md).

While Endpoint Privilege Management is now generally available, the [reports for EPM](../protect/epm-reports.md) will transition to a feature in *preview*, and will receive some more enhancements before being removed from preview.

#### Support for WDAC Application ID tagging with Intune Firewall Rules policy<!-- 17224780  -->
Intune's *Microsoft Defender Firewall Rules* profiles, which are available as part of [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md), now include the Policy App ID setting. This setting is described in the [*MdmStore/FirewallRules/{FirewallRuleName}/PolicyAppId*](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx#mdmstorefirewallrulesfirewallrulenamepolicyappid) CSP and supports specifying a Windows Defender Application Control (WDAC) Application ID tag.

With this capability, you can scope your firewall rules to an application or a group of applications and rely on your WDAC policies to define those applications. By using tags to link to and rely on WDAC policies, your Firewall Rules policy won't need to rely on the firewall rules option of an absolute file path, or use of a variable file path that can reduce security of the rule.

Use of this capability requires you to have WDAC policies in place that include *AppId* tags that you can then specify in your Intune Microsoft Defender Firewall Rules.

For more information, see the following articles in the Windows Defender Application Control documentation:

- [About application control for Windows](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)
- [WDAC Application ID (AppId) Tagging guide](/windows/security/threat-protection/windows-defender-application-control/appidtagging/windows-defender-application-control-appid-tagging-guide)

Applies to:

- Windows

#### New App and browser isolation profile for Intune's endpoint security Attack Surface Reduction policy<!-- 17392386  -->
We have released a new experience creating new *App and Browser Isolation* profiles for endpoint security Attack Surface Reduction policy. The experience for editing your previously created App and Browser isolation policies remains the same, and you can continue to use them. This update applies only for the new [App and Browser Isolation](../protect/endpoint-security-asr-policy.md#attack-surface-reduction-profiles) policies you create for the *Windows 10 and later* platform.

This update is part of the continuing rollout of new profiles for endpoint security policies, which began in April 2022.

Additionally, the new profile includes the following changes for the settings it includes:

- **Block external content from non-enterprise approved sites** - This setting is removed from the updated profile as it was supported only by Microsoft Edge Legacy. Microsoft Edge Legacy support ended in March 2021. [Microsoft 365 apps say farewell to Internet Explorer 11 and Windows 10 sunsets Microsoft Edge Legacy - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/microsoft-365-blog/microsoft-365-apps-say-farewell-to-internet-explorer-11-and/ba-p/1591666).

- **Clipboard file type** – This setting is added to the updated profile and determines the type of content that can be copied from the host to Application Guard environment and vice versa. You can view the CSP for this new setting at [Settings/ClipboardFileType](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#settingsclipboardfiletype) in the WindowsDefenderApplicationGuard CSP documentation.

### Intune apps

#### Newly available protected apps for Intune<!-- 17318943, 17319737, 17457189, 17624650  -->
The following protected apps are now available for Microsoft Intune:

- ixArma by INAX-APPS (iOS)
- myBLDNG by Bldng.ai (iOS)
- RICOH Spaces V2 by Ricoh Digital Services
- Firstup - Intune by Firstup, Inc. (iOS)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Role-based access control

#### New Assign (RBAC) permissions for organizational messages<!-- 16872833  -->
The **Assign** RBAC permissions for organizational messages determines who can assign target Microsoft Entra groups to an organizational message. To access RBAC permissions, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Roles**.

This permission is also added to the **Organizational Messages Manager** built-in role.  Existing custom roles for managing Organizational Messages must be modified to add this permission for users to modify this setting.

- For more information, about role-based access control (RBAC), see [RBAC with Microsoft Intune](role-based-access-control.md).
- For more information, about prerequisites for organization messages, see [Organizational messages prerequisites](/microsoft-365/admin/misc/organizational-messages-microsoft-365#role-based-access-control-requirements).

### Tenant administration

#### Delete organizational messages<!-- 15273028  -->
You can now delete organizational messages from Microsoft Intune.  After you delete a message, it's removed from Intune, and no longer appears in the admin center. You can delete a message anytime, regardless of its status. Intune automatically cancels active messages after you delete them. For more information, see [Delete organizational messages](/microsoft-365/admin/misc/organizational-messages-microsoft-365#delete-message).

#### Review audit logs for organizational messages<!-- 16576073 -->
Use audit logs to track and monitor organizational message events in Microsoft Intune. To access the logs, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Audit logs**. For more information, see [Audit logs for Intune activities](monitor-audit-logs.md#view-the-audit-logs).

## Week of April 10, 2023

### Device configuration

#### User configuration support for Windows 10 multi-session VMs is now GA<!-- 17060455 -->
You can now:

- Configure user scope policies using **Settings catalog** and assign to groups of users.
- Configure user certificates and assign to users.
- Configure PowerShell scripts to install in the user context and assign to users.

Applies to:

- **Windows 10**
- Virtual machines created in [Azure Public and Azure Government clouds](intune-govt-service-description.md)

## Week of April 3, 2023

### Device configuration

#### Add Google accounts to Android Enterprise personally owned devices with a work profile<!-- 9113561 -->
On Android Enterprise personally owned devices with a work profile, you can configure settings that restrict device features and settings. Currently, there's an **Add and remove accounts** setting. This setting prevents accounts from being added in the work profile, including preventing Google accounts.

This setting changed. You can now add Google accounts. The **Add and remove accounts** setting options are:

- **Block all accounts types**: Prevents users from manually adding or removing accounts in the work profile. For example, when you deploy the Gmail app into the work profile, you can prevent users from adding or removing accounts in this work profile.
- **Allow all accounts types**: Allows all accounts, including Google accounts. These Google accounts are blocked from installing apps from the **Managed Google Play Store**.

  This setting requires:

  - Google Play app version 80970100 or higher

- **Allow all accounts types, except Google accounts** (default): Intune doesn't change or update this setting. By default, the OS might allow adding accounts in the work profile.

For more information on the settings you can configure, go to [Android template device settings list to restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:

- Android Enterprise personally owned devices with a work profile

## Week of March 27, 2023

### App management

#### Update macOS DMG apps<!-- 13155074 -->
You can now update apps of type **macOS apps (DMG)** deployed using Intune. To edit a DMG app that's already created in Intune, upload the app update with the same bundle identifier as the original DMG app. For related information, see [Add a macOS DMG app to Microsoft Intune](../apps/lob-apps-macos-dmg.md).

#### Install required apps during pre-provisioning<!-- 12716381 -->
A new toggle is available in the Enrollment Status Page (ESP) profile that allows you to select whether you want to attempt to install required applications during the Windows Autopilot pre-provisioning technician phase. We understand that installing as many applications as possible during pre-provisioning is desired to reduce the end user setup time. If there's an app install failure, ESP continues except for the apps specified in the ESP profile. To enable this function, you need to edit your Enrollment Status Page profile by selecting **Yes** on the new setting entitled **Only fail selected apps in technician phase**. This setting only appears if you have blocking apps selected. For information about ESP, go to [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).

### Microsoft Intune Suite

#### Remote Help

Version: 4.2.1167.0 - Changes in this release:

This release addresses a bug in the Laser Pointer and includes some updates to prepare for future releases.

- Updated product name from **Remote help** to **Remote Help**
- Updated application description to better localize it for non-US locales
- Resolved a bug where the app would flash a white screen when launched in dark mode
- Fixed a bug with the Laser pointer color change

## Week of March 20, 2023 (Service release 2303)

### App management

### More minimum OS versions for Win32 apps<!-- 16842404  -->
Intune supports more minimum operating system versions for Windows 10 and 11 when installing Win32 apps. In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **Windows** > **Add** > **Windows app (Win32)**. In the **Requirements** tab next to **Minimum operating system**, select one of the available operating systems. Other OS options include:

- Windows 10 21H2
- Windows 10 22H2
- Windows 11 21H2
- Windows 11 22H2

#### Managed apps permission is no longer required to manage VPP apps<!-- 17205644  -->
You can view and manage VPP apps with only the **Mobile apps** permission assigned. Previously, the **Managed apps** permission was required to view and manage VPP apps. This change doesn't apply to Intune for Education tenants who still need to assign the **Managed apps** permission. More information about permissions in Intune is available at [Custom role permissions](create-custom-role.md#custom-role-permissions).

### Device configuration

#### New settings and setting options available in the macOS Settings Catalog <!-- 16813395  -->
The [Settings Catalog](../configuration/settings-catalog.md) lists all the settings you can configure in a device policy, and all in one place.

New settings are available in the Settings Catalog. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can see these settings at **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **macOS** for platform > **Settings catalog** for profile type.

New settings include:

**Microsoft Defender > Tamper protection**:

- Enforcement level

**Microsoft Office > Microsoft OneDrive**:

- Automatic upload bandwidth percentage
- Automatically and silently enable the Folder Backup feature (aka Known Folder Move)
- Block apps from downloading online-only files
- Block external sync
- Disable automatic sign in
- Disable download toasts
- Disable personal accounts
- Disable tutorial
- Display a notification to users once their folders have been redirected
- Enable Files On-Demand
- Enable simultaneous edits for Office apps
- Force users to use the Folder Backup feature (aka Known Folder Move)
- Hide dock icon
- Ignore named files
- Include ~/Desktop in Folder Backup (aka Known Folder Move)
- Include ~/Documents in Folder Backup (aka Known Folder Move)
- Open at login
- Prevent users from using the Folder Backup feature (aka Known Folder Move)
- Prompt users to enable the Folder Backup feature (aka Known Folder Move)
- Set maximum download throughput
- Set maximum upload throughput
- SharePoint Prioritization
- SharePoint Server Front Door URL
- SharePoint Server Tenant Name

Applies to:

- macOS

For more information about configuring Settings Catalog profiles in Intune, go to [Create a policy using settings catalog](../configuration/settings-catalog.md).

#### Add custom Bash scripts to configure Linux devices<!-- 12508999  -->
In Intune, you can add existing Bash scripts to configure Linux devices (**Devices** > **By platform** > **Linux** > **Scripts**).

When you create this script policy, you can set the context that the script runs in (user or root), how frequently the script runs, and how many times execution should retry.

For more information on this feature, go to [Use custom Bash scripts to configure Linux devices in Microsoft Intune](../configuration/custom-settings-linux.md).

Applies to:

- Linux Ubuntu Desktops

### Device enrollment

#### Support for the await final configuration setting for iOS/iPadOS Automated device enrollment (public preview)<!-- 13156553  -->
Now in public preview, Intune supports a new setting called **Await final configuration** in eligible new and existing iOS/iPadOS automated device enrollment profiles. This setting enables an out-of-the-box locked experience in Setup Assistant. It prevents device users from accessing restricted content or changing settings on the device until most Intune device configuration policies are installed. You can configure the setting in an existing automated device enrollment profile, or in a new profile (**Devices** > **By platform** > **iOS/iPadOS** > **Device onboarding** > **Enrollment** > **Enrollment program tokens** > **Create profile**). For more information, see [Create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

#### New setting gives Intune admins control over device-to-category mapping<!-- 15029839 -->
Control visibility of the device category prompt in Intune Company Portal. You can now hide the prompt from end users and leave the device-to-category mapping up to Intune admins. The new setting is available in the admin center under **Tenant Administration** > **Customization** > **Device Categories**. For more information, see [Device categories](../apps/company-portal-app.md#device-categories).

#### Support for multiple enrollment profiles and tokens for fully managed devices <!-- 14205233  -->
Create and manage multiple enrollment profiles and tokens for Android Enterprise fully managed devices. With this new functionality, you can now use the *EnrollmentProfileName* dynamic device property to automatically assign enrollment profiles to fully managed devices. The enrollment token that came with your tenant remains in a default profile. For more information, see [Set up Intune enrollment of Android Enterprise fully managed devices](../enrollment/android-fully-managed-enroll.md).

<a name='new-azure-ad-frontline-worker-experience-for-ipad-public-preview---6367427----'></a>

#### New Microsoft Entra frontline worker experience for iPad (public preview)<!-- 6367427  -->
*This capability begins to roll out to tenants in mid-April.*

Intune now supports a frontline worker experience for iPhones and iPads using Apple automated device enrollment. You can now enroll devices that are enabled in Microsoft Entra ID shared mode via zero-touch. For more information about how to configure automated device enrollment for shared device mode, see [Set up enrollment for devices in Microsoft Entra shared device mode](../enrollment/automated-device-enrollment-shared-device-mode.md).

Applies to:

- iOS/iPadOS

### Device management

#### Endpoint security firewall policy support for log configurations<!-- 16730565   -->
You can now configure settings in [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune) that configure firewall logging options. These settings can be found in the *Microsoft Defender Firewall* profile template for the *Windows 10 and later* platform, and are available for the *Domain*, *Private*, and *Public* profiles in that template.

Following are the new settings, all found in the [Firewall configuration service provider (CSP)](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx):

- Enable Log Success Connections
- Log File Path
- Enable Log Dropped Packets
- Enable Log Ignored Rules

Applies to:

- Windows 11

#### Endpoint security firewall rules support for Mobile Broadband (MBB)<!-- 16730577  -->
The **Interface Types** setting in [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune) now include the option for **Mobile Broadband**. Interface Types is available in the **Microsoft Defender Firewall Rules** profile for all platforms that support Windows. For information about the use of this setting and option, see [Firewall configuration service provider (CSP)](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx).

Applies to:

- Windows 10
- Windows 11

#### Endpoint security firewall policy support for network list manager settings<!-- 9803477  -->
We've added a pair of network list manager settings to [endpoint security Firewall policy](../protect/endpoint-security-firewall-policy.md#devices-managed-by-intune). To help determine when a Microsoft Entra device is or isn't on your on-premises domain subnets, you can use the network list manager settings. This information can help firewall rules apply correctly.

The following settings are found in a new category named *Network List Manager*, that's available in the *Microsoft Defender Firewall* profile template for the *Windows 10, Windows 11, and Windows Server* platform:

- Allowed Tls Authentication Endpoints
- Configured Tls Authentication Network Name

For information about Network Categorization settings, see [NetworkListManager CSP](/windows/client-management/mdm/policy-csp-networklistmanager).

Applies to:

- Windows 10
- Windows 11

#### Improvements to Devices area in admin center (public preview) <!-- 12775837 -->
The Devices area in the admin center now has a more consistent UI, with more capable controls and an improved navigation structure so you can find the information you need faster. To opt in to the public preview and try out the new experience, go to **Devices** and flip the toggle at the top of the page. Improvements include:

* A new scenario-focused navigation structure.
* New location for platform pivots to create a more consistent navigation model.
* A reduction in journey, helping you get to your destination faster.
* Monitoring and reports are within the management workflows, giving you easy access to key metrics and reports without having to leave the workflow.
* A consistent way across list views to search, sort, and filter data.

For more information about the updated UI, see [Try new Devices experience in Microsoft Intune](public-preview.md).

### Device security

#### Microsoft Intune Endpoint Privilege Management (public preview)<!-- 15654169   -->
As a public preview, you can now use Microsoft Intune Endpoint Privilege Management. With Endpoint Privilege Management, admins can set policies that allow standard users to perform tasks normally reserved for an administrator. Endpoint Privilege Management can be configured in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) at **Endpoint security** > **Endpoint Privilege Management**.

With the public preview, you can configure policies for *automatic* and *user-confirmed* workflows that elevate the run-time permissions for apps or processes you select. You then assign these policies to users or devices that have end users running without Administrator privileges. Once policy is received, Endpoint Privilege Management will broker the elevation on behalf of the user, allowing them to elevate approved applications without needing full administrator privileges. The preview also includes built-in insights and reporting for Endpoint Privilege Management.

To learn how to activate the public preview and use Endpoint Privilege Management policies, start with [Use Endpoint Privilege Management with Microsoft Intune](../protect/epm-overview.md). Endpoint Privilege Management is part of the [Intune Suite](intune-add-ons.md) offering, and free to try while it remains in public preview.

### Intune apps

#### Newly available protected apps for Intune<!-- 16927438, 17030201, 17074872 17103353 -->
The following protected apps are now available for Microsoft Intune:

- EVALARM by GroupKom GmbH (iOS)
- ixArma by INAX-APPS (Android)
- Seismic | Intune by Seismic Software, Inc.
- Microsoft Viva Engage by Microsoft (formally Microsoft Yammer)

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

### Monitor and troubleshoot

#### Diagnostic data collection for Endpoint Privilege Management<!-- 17392824   -->
To support the release of Endpoint Privilege Management, we've updated [Collect diagnostics from a Windows device](../remote-actions/collect-diagnostics.md) to include the following data, which is collected from devices enabled for Endpoint Privilege Management:

- Registry keys:

  - HKLM\SOFTWARE\Microsoft\EPMAgent

- Commands:

  - %windir%\system32\pnputil.exe /enum-drivers

- Log files:

  - %ProgramFiles%\Microsoft EPM Agent\Logs\\\*.*
  - %windir%\system32\config\systemprofile\AppData\Local\mdm\\\*.log

#### View status for pending and failed organizational messages<!-- 17017707  -->
We've added two more states to organizational message reporting details to make it easier to track pending and failed messages in the admin center.

- **Pending**: The message hasn't been scheduled yet and is currently in progress.
- **Failed**: The message failed to schedule due to a service error.

For information about reporting details, see [View reporting details for organizational messages](/microsoft-365/admin/misc/organizational-messages-microsoft-365).


#### More reporting information related to tenant attach devices<!-- 9220597  -->
You can now view information for tenant attach devices in the existing antivirus reports under the Endpoint Security workload. A new column differentiates between devices managed by Intune and devices managed by Configuration Manager. This reporting information is available in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Endpoint security** > **Antivirus**.

## Week of March 13, 2023

### Device management

#### Meta Quest 2 and Quest Pro are now in Open Beta (US only) on Microsoft Intune for Android Open Source Devices
Microsoft Intune for Android open source project devices (AOSP) has welcomed Meta Quest 2 and Quest Pro into Open Beta for the US market.

For more information, go to [Operating systems and browsers supported by Microsoft Intune](supported-devices-browsers.md)

Applies to:

- Android (AOSP)

### App management

#### Trusted Root Certificates Management for Intune App SDK for Android<!-- 15135752 -->
If your Android application requires SSL/TLS certificates issued by an on-premises or private certificate authority to provide secure access to internal websites and applications, the Intune App SDK for Android now has support for certificate trust management. For more information and examples, see [Trusted Root Certificates Management](../developer/app-sdk-android-phase7.md#trusted-root-certificates-management).

#### System context support for UWP apps<!-- 16544103 -->
In addition to user context, you can deploy Universal Windows Platform (UWP) apps from the **Microsoft Store app (new)** in system context. If a provisioned *.appx* app is deployed in system context, the app auto-installs for each user that logs in. If an individual end user uninstalls the user context app, the app still shows as installed because it's still provisioned. In addition, the app must not already be installed for any users on the device. Our general recommendation is to not mix install contexts when deploying apps. Win32 apps from the **Microsoft Store app (new)** already support system context.

## Week of March 6, 2023

### App management

#### Deploy Win32 apps to device groups<!-- 7359954 -->
You can now deploy Win32 apps with **Available** intent to device groups. For more information, see [Win32 app management in Microsoft Intune](../apps/apps-win32-app-management.md).

### Device management

#### New URL for Microsoft Intune admin center<!-- 17441426 -->
The Microsoft Intune admin center has a new URL: [https://intune.microsoft.com](https://intune.microsoft.com). The previously used URL, [https://endpoint.microsoft.com](https://endpoint.microsoft.com), continues to work but will redirect to the new URL in late 2023. We recommend taking the following actions to avoid issues with Intune access and automated scripts:

* Update login or automation to point to `https://intune.microsoft.com`.
* Update your firewalls, as needed, to allow access to the new URL.
* Add the new URL to your favorites and bookmarks.
* Notify your helpdesk and update IT administrator documentation.

### Tenant administration

#### Add CMPivot queries to Favorites folder<!-- 16702226 -->
You can add your frequently used queries to a **Favorites** folder in CMPivot. CMPivot allows you to quickly assess the state of a device managed by Configuration Manager via Tenant Attach and take action. The functionality is similar to one already present in the Configuration Manager console. This addition helps you keep all your most used queries in one place. You can also add tags to your queries to help search and find queries. The queries saved in the Configuration Manager console aren't automatically added to your **Favorites** folder. You need to create new queries and add them to this folder. For more information about CMPivot, see [Tenant attach: CMPivot usage overview](../../configmgr/tenant-attach/cmpivot-start.md).

### Device enrollment

#### New Microsoft Store apps now supported with the Enrollment Status Page<!-- 16280325 -->
The Enrollment Status Page (ESP) now supports the new Microsoft store applications during Windows Autopilot. This update enables better support for the new Microsoft Store experience and should be rolling out to all tenants starting with Intune 2303. For related information, see [Set up the Enrollment Status Page](../enrollment/windows-enrollment-status.md).

## Week of February 27, 2023

### Device configuration

#### Support for Locate device on Android Enterprise corporate owned fully managed and Android Enterprise corporate owned work profile devices<!--12391424 -->

You can now use "Locate device" on Android Enterprise corporate owned fully managed and Android Enterprise corporate owned work profile devices. With this feature, admins are able to locate lost or stolen corporate devices on-demand.

In [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you need to turn the feature on using a device configuration profiles (**Devices** > **Manage devices** > **Configuration** > **Create** > **New policy** > **Android Enterprise** for platform > **Device Restrictions** for profile type).

Select **Allow** on the **Locate device** toggle for fully managed and corporate owned work profile devices and select applicable groups. **Locate device** is available when you select **Devices**, and then select **All devices**. From the list of devices you manage, select a supported device, and choose the **Locate device** remote action.

For information on locating lost or stolen devices with Intune, go to:

- [Locate lost or stolen devices with Intune](../remote-actions/device-locate.md)

Applies to:

- Android Enterprise corporate owned fully managed
- Android Enterprise corporate owned dedicated devices
- Android Enterprise corporate owned work profile

#### Intune add-ons <!-- 13817801 -->

Microsoft Intune Suite provides mission-critical advanced endpoint management and security capabilities into Microsoft Intune.

You can find add-ons to Intune in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) under **Tenant administration** > **Intune add-ons**.

For detailed information, see [Use Intune Suite add-on capabilities](intune-add-ons.md).

#### View ServiceNow Incidents in the Intune Troubleshooting workspace (Preview)<!-- 12508062 -->

In public preview, you can view a list of ServiceNow incidents associated with the user you've selected in the Intune Troubleshooting workspace. This new feature is available under **Troubleshooting + Support** > select a user > **ServiceNow Incidents**. The list of incidents shown have a direct link back to the source incident and show key information from the incident. All incidents listed link the "Caller" identified in the incident with the user selected for Troubleshooting.

For more information, go to [Use the troubleshooting portal to help users at your company](service-now-integration.md).

### Device security

#### Microsoft Tunnel for MAM is now generally available<!-- 16883728  -->

Now out of preview and generally available, you can add [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-overview.md) to your tenant. Tunnel for MAM supports connections from unenrolled [Android](../protect/microsoft-tunnel-mam-android.md) and [iOS](../protect/microsoft-tunnel-mam-ios.md) devices. This solution provides your tenant with a lightweight VPN solution that allows mobile devices access to corporate resources while adhering to your security policies.

In addition, MAM Tunnel for iOS now supports Microsoft Edge.

Previously, Tunnel for MAM for Android and iOS was in public preview and free for use. With this release as generally available, this solution now requires an add-on license for its use.

For licensing details, see [Intune add-ons](intune-add-ons.md).

Applies to:

- Android
- iOS

### Tenant administration

#### Organizational messages now support custom destination URLs <!-- 16576068  -->

You can now add any custom destination URL to organizational messages in the taskbar, notifications area, and Get Started app. This feature applies to Windows 11. Messages created with Microsoft Entra registered domains that are in a scheduled or active state are still supported. For more information, see [Create organizational messages](/microsoft-365/admin/misc/organizational-messages-microsoft-365?tabs=taskbar#step-1-create-a-message).
