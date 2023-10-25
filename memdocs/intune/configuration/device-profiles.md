---
# required metadata

title: Device features and settings in Microsoft Intune
description: Overview of the different Microsoft Intune device profiles. Get info on GPO, features, restrictions, email, wifi, VPN, education, certificates, upgrade Windows 10/11, BitLocker and Microsoft Defender, Windows Information Protection, administrative templates, and custom device configuration settings in the Microsoft Intune admin center. Use these profiles to manage and protect data and devices in your company.
keywords:
author: MandiOhlinger

ms.author: mandia
manager: dougeby
ms.date: 03/20/2023
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# Apply features and settings on your devices using device profiles in Microsoft Intune

Microsoft Intune includes settings and features you can enable or disable on different devices within your organization. These settings and features are added to "configuration profiles". You can create profiles for different devices and different platforms, including iOS/iPadOS, Android device administrator, Android Enterprise, and Windows. Then, use Intune to apply or "assign" the profile to the devices. Assigning device configuration profiles to user's devices at your organization help those users become productive quickly.


 [!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

As part of your mobile device management (MDM) solution, use these configuration profiles to complete different tasks. Intune has many templates that include groups of settings that are specific to a feature, such as certificates, VPN, email, and more.

Some profile examples include:

- Allow or prevent access to bluetooth on the device.
- Create a WiFi or VPN profile that gives different devices access to your corporate network.
- Manage software updates, including when they're installed.
- Run an Android device as dedicated kiosk device that can run one app, or run many apps.
- On iOS/iPadOS and macOS devices, allow users to use AirPrint printers in your organization.

You determine the specific capabilities and apply the unique settings for your organization. You also determine the groups of users and devices that require these capabilities and settings. It is common to have many device profiles for each supported platform, ranging from device anti-virus settings, to custom settings that aren't built into Intune as templates yet.

> [!NOTE]
> If you currently manage on-premises devices using Microsoft Configuration Manager, consider implementing co-management to cloud attach your on-premises devices. Co-management allows you to concurrently manage Windows 10 or Windows 11 devices with both Configuration Manager and Microsoft Intune. Once you implement co-management, you can create the device profiles and policies you need in Intune based on those you currently have in Configuration Manager. For more information about co-management, see [Understand co-management using Microsoft Configuration Manager](../../configmgr/comanage/overview.md). For related information, see [Prepare Intune for co-management](../../configmgr/core/get-started/capabilities-in-technical-preview-1709.md#prepare-intune-for-co-management).

### Fundamental device configuration profiles

Before you enroll your organization's devices into Microsoft Intune, you should create your fundamental device configuration profiles. These are the configuration profiles that are commonly set up at a company or organization. Consider creating and assigning these configuration profiles first.

Fundamental device configuration profiles to consider:
- [Device restrictions](#device-restrictions)
- [Email settings](#email)
- [VPN settings](#vpn)
- [Wi-Fi settings](#wi-fi)

### Protective device configuration profiles

In addition to the fundamental configuration profiles, you should consider adding more involved device configuration profiles. The following information describes these types of protective device configuration profiles. Unlike the fundamental configuration profiles that most organizations will add, these profiles should be added as needed.

Protective device configuration profiles to consider:
- [Derived credentials](#derived-credential)
- [Domain join](#domain-join)
- [Endpoint protection](#endpoint-protection)
- [Enable Microsoft Defender anti-virus settings](#microsoft-defender-for-endpoint)
- [Manage Android Enterprise devices with OEMConfig](#oemconfig)
- [Configure certificates](#certificates)
- [Configure Microsoft Edge settings](..\configuration\administrative-templates-configure-edge.md)

### Comprehensive device configuration profiles

Beyond fundamental and protective device configuration profiles, you should be aware of the following configuration control and concepts that Microsoft Intune provides. Intune provides a wide variety of device configuration control. These following areas can help you become familiar with the total configuration capabilities offered by Intune.

Comprehensive device configuration profiles to consider:
- [Group Policy analytics](#administrative-templates-and-group-policy)
- [Administrative templates](#administrative-templates-and-group-policy)
- [Custom profiles](#custom-profile)
- [Settings catalog](#settings-catalog)

This article gives an overview of the different types of profiles you can create. Use these profiles to allow or prevent some features on the devices.

## Platforms

When creating a new device configuration profile, you must first select the platform for the configuration profile. The available configuration settings are unique for each platform. The available platforms are included in the following list:
- Android device administrator
- Android (AOSP)
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10 and later
- Windows 8.1 and later
- Windows 10X

## Profile types

A profile type is a device configuration area, feature, or capability that contains specific device settings. As mentioned above, each platform has a unique set of available device configuration settings. To select a setting, you start by selecting a **Platform** and then a **Profile type**. For instance, if you choose **iOS/iPadOS** as the platform, you can select **Templates** for the profile type. Next, you can select a template name from the provided list. For instance, you can select the **Email** template to configure an email server, SSL communication, and other built-in email settings. Because capabilities are different for each platform, your available profile types and templates are also different.

## Administrative templates and Group policy

[Administrative templates](administrative-templates-windows.md) include hundreds of settings that you can configure for Internet Explorer, Microsoft Edge, OneDrive, remote desktop, Word, Excel, and other Office programs. These templates are a subset of the overall configuration profile templates. Also, these templates give administrators a simplified view of settings similar to group policy, and they're 100% cloud-based.

[Group Policy analytics](group-policy-analytics.md) analyzes your on-premises GPOs. It helps you determine how your GPOs translate in the cloud. The output shows which settings are supported in MDM providers, including Microsoft Intune. It also shows any deprecated settings, or settings not available to MDM providers. Group Policy is supported on Windows 10/11.

This feature supports:

- Windows 11
- Windows 10

## Certificates

You use [certificates in Intune](../protect/certificates-configure.md) to authenticate your users to reach applications and corporate resources through VPN, Wi-Fi, or email profiles. When you use certificates to authenticate these connections, your end users won't need to enter usernames and passwords, which can make their access seamless. Certificates are also used for signing and encryption of email using S/MIME. Common types of certificates used in Intune include trusted root certificates, Simple Certificate Enrollment Protocol (SCEP) certificates, and Public Key Cryptography Standards (PKCS) certificates.

This feature supports:

- Android device administrator
- Android (AOSP)
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 11
- Windows 10
- Windows 8.1

## Custom profile

[Custom settings](custom-settings-configure.md) let administrators assign device settings that aren't built in to Intune. On Android devices, you can enter OMA-URI values. For iOS/iPadOS devices, you can import a configuration file you created in the Apple Configurator.

This feature supports:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 11
- Windows 10

## Delivery optimization

[Delivery optimization](delivery-optimization-windows.md) provides a better experience to delivery software updates. These settings are replacing the **Software Updates** > **Windows 10 update ring** settings.

Use these settings to control how software updates are downloaded to devices in your organization. For example, you can let users get their own updates, or get updates using the delivery optimization cloud services in a device profile.

This feature supports:

- Windows 11
- Windows 10

## Derived credential

In an environment where smart cards are required for authentication or encryption and signing, you can use Intune to provision mobile devices with a certificate that's derived from a user's smart card. That certificate is called a [derived credential](../protect/derived-credentials.md). Intune [supports several derived credential issuers](../protect/derived-credentials.md##supported-issuers), though you can use only a single issuer per tenant at a time. Derived credentials are commonly used with device configuration profile types such as Wi-Fi, VPN, app authentication, Email, or S/MIME signing and encryption. However, each platform that supports derived credentials has a different set of supported device configuration settings.

This feature supports:

- Android Enterprise
- iOS/iPadOS

## Device features

[Device features](device-features-configure.md) controls features on iOS/iPadOS and macOS devices, such as AirPrint, notifications, and lock screen messages.

This feature supports:

- iOS/iPadOS
- macOS

## Device firmware configuration interface

[Device firmware configuration interface](device-firmware-configuration-interface-windows.md) (DFCI) allows administrators to enable or disable UEFI (BIOS) settings using Intune. Use these settings to enhance security at the firmware-level, which is typically more resilient to malicious attacks.

This feature supports:

- Windows 11 on supported firmware
- Windows 10 1809 and newer on supported firmware

## Device restrictions

[Device restrictions](device-restrictions-configure.md) controls security, hardware, data sharing, and more settings on the devices. For example, create a device restriction profile that prevents iOS/iPadOS device users from using the device camera. Additionally, you could create a device restriction profile that manages access to the App store or restricts certain apps from being installed on the device. Other examples include restricting device users from viewing corporate documents in unmanaged apps, requiring a password to access the device, or requiring devices to use only Wi-Fi networks set up via configuration profiles.

This feature supports:

- Android device administrator
- Android (AOSP)
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 11
- Windows 10
- Windows 10 Team

### Security baselines

Security baselines are groups of pre-configured Windows settings that help you apply and enforce granular security settings recommended by the relevant security teams at Microsoft. You can also customize each baseline you deploy to enforce only those settings and values that your organization requires. When you create a security baseline profile in Intune, you're creating a template that consists of multiple device configuration profiles.

Intune security baselines apply to Windows 10 and 11 and fall into the following areas:
- Security Baseline for Windows 10 and later
- Microsoft Defender for Endpoint Baseline
- Microsoft Edge Baseline
- Windows 365 Security Baseline

## Domain join

[Domain join](domain-join-configure.md) configures on-premises Active Directory domain information. This information is deployed to hybrid Azure AD joined devices when provisioned using Windows Autopilot and Intune. This profile tells devices which domain and OU to join.

This feature supports:

- Windows 11
- Windows 10

## Edition upgrade and mode switch

[Windows 10/11 edition upgrades](edition-upgrade-configure-windows-10.md) automatically upgrades devices that run some versions of Windows client to a newer edition.

This feature supports:

- Windows 11
- Windows 10

## Education

[Education settings - Windows 10](education-settings-configure.md) configure options for the [Windows Take a Test app](/education/windows/take-tests-in-windows-10). When you configure these options, no other apps can run on the device until the test is complete.

[Education settings - iOS/iPadOS](../fundamentals/education-settings-configure-ios-shared.md) uses the iOS/iPadOS Classroom app to guide learning, and control student devices in the classroom. You can configure iPad devices so many students can share a single device.

## Email

[Email settings](email-settings-configure.md) creates, assigns, and monitors Exchange ActiveSync email settings on the devices. Email profiles help with consistency, reduce support calls, and let end-users access company email on their personal devices, without any required setup on their part. 

This feature supports:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- Windows 11
- Windows 10

## Endpoint protection

[Endpoint protection](../protect/endpoint-protection-configure.md) configures BitLocker and Microsoft Defender settings for Windows client devices. On macOS devices, you can also configure the firewall, gateway, and other resources.

To onboard Microsoft Defender for Endpoint with Microsoft Intune, see [Configure endpoints using Mobile Device Management (MDM) tools](/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-mdm).

This feature supports:

- macOS
- Windows 11
- Windows 10

## eSIM cellular

[eSIM cellular profiles](esim-device-configuration.md) lets administrators configure cellular data plans on your managed devices for internet and data access. After getting activation codes from your mobile operator, use Intune to import these activation codes, and then assign to your eSIM capable devices.

This feature supports:

- Windows 11
- Windows 10 Fall Creators Update and newer

## Extensions

[macOS system extensions and kernel extensions](kernel-extensions-overview-macos.md) allows administrators to add features or programs that extend the native capabilities of the operating system. Configure these settings to trust all extensions from a specific developer or partner, or allow specific extensions.

This feature supports:

- macOS

## Identity protection

[Identity protection](../protect/identity-protection-configure.md) controls the Windows Hello for Business experience on Windows client devices. Configure these settings to make Windows Hello for Business available to users and devices, and to specify requirements for device PINs and gestures.  

This feature supports:  

- Windows 11
- Windows 10
- Windows Holographic for Business  

## Kiosk

[Kiosk settings](kiosk-settings.md) profile configures a device to run one app, or run many apps. You can also customize other features on your kiosk, including a start menu and a web browser.

This feature supports:

- Windows 11 (single app kiosk only)
- Windows 10

Kiosk settings also available as device restrictions for [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience), and [iOS/iPadOS](device-restrictions-ios.md#kiosk).

## MX profile (Zebra)

[Mobility extensions (MX)](android-zebra-mx-overview.md) expand on the built-in Intune settings to customize or add more settings specific to Zebra devices. Zebra devices are commonly used on factory floors, and retail environments. If you have hundreds or thousands of Zebra devices, you can use Intune to configure and manage these devices.

This feature supports:

- Android device administrator

## Microsoft Defender for Endpoint

[Microsoft Defender for Endpoint](../protect/advanced-threat-protection.md) integrates with Intune to monitor and help protect devices. You set risk levels, and determine what happens if devices exceed that level. When combined with conditional access, you can help prevent malicious activity in your organization.

This feature supports:

- Windows 11
- Windows 10

## Network boundary

[Network boundary](network-boundary-windows.md) creates a list of sites that are trusted by your organization. This feature is used with Microsoft Defender Application Guard and Microsoft Edge to help protect your devices.

This feature supports:

- Windows 11
- Windows 10

## OEMConfig

On Android Enterprise devices, [OEMConfig](android-oem-configuration-overview.md) is a standard. It allows OEMs (original equipment manufacturers) and EMMs (enterprise mobility management) to build and support OEM-specific features in a standardized way. With OEMConfig, an OEM creates a schema that defines OEM-specific management features, and embeds it in an app uploaded to Google Play. Intune reads the schema from the app, and allows Intune administrators to configure the settings in the schema.

This feature supports:

- Android Enterprise (OEMConfig)

## Preference file

[Preference files](preference-file-settings-macos.md) on macOS devices include information about apps. For example, you can use preference files to control web browser settings, customize apps, and more.

This feature supports:

- macOS

> [!TIP]
> macOS settings are continually being added to the [settings catalog](settings-catalog.md). Some of these settings can replace preference files. For more information, go to [Tasks you can complete using the Settings Catalog in Intune](settings-catalog-common-features.md).

## Templates

Templates include a logical grouping of settings that configure a feature or concept, such as VPN, email, kiosk devices, and more. Templates are available when you choose either iOS/iPadOS, macOS, Windows 10 and later, or Windows 10 as the platform.

## Settings catalog

The [settings catalog](settings-catalog.md) lists the settings you can configure. It's not template, or a logical grouping of settings. The setting catalog simplifies how you create a policy, and how you see all the available settings. More settings are continually being added as well.

On Windows, there are thousands of settings available, including many settings not found in the templates. When you want a complete list of all the settings, use the settings catalog to create your policy. If you want to use a logical grouping of settings, then continue to use the templates.

On macOS, you can configure Microsoft Edge version 77 and newer using the settings catalog. In your policy, you configure individual settings. It doesn't require a preference file.

This feature supports:

- iOS/iPadOS
- macOS
- Windows 11
- Windows 10

## Shared multi-user device

[Windows 10/11](shared-user-device-settings-windows.md) and [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) includes settings to manage devices with multiple users. These devices are known as shared devices, or shared PCs. When a user signs in to the device, you choose if the user can change the sleep options, or save files on the device. In another example, to save space, you can create a profile that deletes inactive credentials from Windows HoloLens devices.

These shared multi-user device settings allow administrators to control some of the device features, and manage these shared devices using Intune.

This feature supports:

- Windows 11
- Windows 10
- Windows Holographic for Business

## Shell scripts

On Linux devices, you can [add existing Bash scripts](../configuration/device-profiles.md) to customize settings and features on these devices. This concept is similar to creating a custom device configuration profile, and deploying the policy to your devices. With Linux, you're using existing Bash scripts to configure features and settings that aren't built into Intune.

On macOS devices, you can [add existing shell scripts](../apps/macos-shell-scripts.md), and then deploy these scripts to your macOS devices.

On Windows devices, you can use the Intune Management Extension to upload your [PowerShell scripts](../apps/intune-management-extension.md) in Intune, and then run these scripts on your devices. Also see what's required to use the extension, how to add them to Intune, and other important information.

This feature supports:

- Linux
- macOS
- Windows 11
- Windows 10

## Update policies

[iOS/iPadOS update policies](../protect/software-updates-ios.md) shows you how to create and assign iOS/iPadOS policies to install software updates on your iOS/iPadOS devices. You can also review the installation status.

For update policies on Windows devices, see [Delivery optimization](delivery-optimization-windows.md). 

This feature supports:

- iOS/iPadOS

## VPN

[VPN settings](vpn-settings-configure.md) assigns VPN profiles to users and devices in your organization, so they can easily and securely connect to the network. 

Virtual private networks (VPNs) give users secure remote access to your company network. Devices use a VPN connection profile to start a connection with your VPN server. 

This feature supports: 

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 11
- Windows 10
- Windows 8.1

## Wi-Fi

[Wi-Fi settings](wi-fi-settings-configure.md) assigns wireless network settings to users and devices. When you assign a WiFi profile, users get access to your corporate WiFi without having to configure it themselves. 

This feature supports:

- Android device administrator
- Android (AOSP)
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 11
- Windows 10
- Windows 8.1 (import only)

## Windows health monitoring

[Windows health monitoring](windows-health-monitoring.md) lets your data event be collected, and then analyzed by Endpoint Analytics. You can use this data to get insights on your Windows devices, including software updates and startup performance.

This feature supports:

- Windows 11
- Windows 10

## Wired networks

[Wired networks](wired-networks-configure.md) let you create and manage 802.1x wired connections for macOS and Windows desktop computers and devices. In your profile, you choose the network interface, select the accepted EAP types, and enter the server trust settings, including PKCS and SCEP certificates.

When you assign the profile, users get access to your corporate wired network without having to configure it themselves.

This feature supports:

- macOS
- Windows 11
- Windows 10

## Zebra Mobility Extensions (MX)

[Zebra Mobility Extensions (MX)](android-zebra-mx-overview.md) allows administrators to use and manage Zebra devices in Intune. You create StageNow profiles with your settings, and then use Intune to assign and deploy these profiles to your Zebra devices. The [StageNow logs and common issues](android-zebra-mx-logs-troubleshoot.md) is a great resource to troubleshoot profiles, and see some potential issues when using StageNow.

This feature supports:

- Android device administrator (Mobility Extensions)

## Refresh cycle times

Intune uses different refresh cycles to check for updates to configuration profiles. If the device recently enrolled, the check-in runs more frequently. Policy and profile refresh cycles lists the estimated refresh times. At any time, users can open the Company Portal app, and sync the device to immediately check for profile updates.

## Manage and troubleshoot

[Manage your profiles](device-profile-monitor.md) to check the status of devices, and the profiles assigned. Also help resolve conflicts by seeing the settings that cause a conflict, and the profiles that include these settings. [Common issues and resolutions](device-profile-troubleshoot.md) helps administrators work with profiles. It describes what happens when deleting a profile, what causes notifications to be sent to devices, and more.

## Next steps

Choose a profile, and get started.
