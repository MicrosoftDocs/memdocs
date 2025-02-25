---
# required metadata

title: Device features and settings in Microsoft Intune
description: Overview of the different Microsoft Intune device profiles. Get info on GPO, features, restrictions, email, wifi, VPN, education, certificates, upgrade Windows 10/11, BitLocker and Microsoft Defender, Windows Information Protection, administrative templates, and custom device configuration settings in the Microsoft Intune admin center. Use these profiles to manage and protect data and devices in your company.
keywords:
author: MandiOhlinger

ms.author: mandia
manager: dougeby
ms.date: 09/23/2024
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
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

Microsoft Intune includes settings and features you can enable or disable on different devices within your organization. These settings and features are added to **configuration profiles**.

When you configure device features using configuration profile, you can help your end users be productive on their devices faster.

You can create profiles for different devices and different platforms, including Android, iOS/iPadOS, macOS, and Windows. There are some configuration settings that are unique to each platform. It's also common to have many device profiles for each platform, ranging from antivirus settings to custom settings.

When the profiles are ready, you use Intune to apply or "assign" the profile to user groups or device groups. 

 [!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

As part of your mobile device management (MDM) solution, use these configuration profiles to complete different tasks. Some profile examples include:

- Allow or prevent access to bluetooth on the device.
- Create a WiFi or VPN profile that gives different devices access to your corporate network.
- Manage software updates, including when they're installed.
- Run an Android device as dedicated kiosk device that can run one app, or run many apps.
- On iOS/iPadOS and macOS devices, allow users to use AirPrint printers in your organization.

> [!TIP]
> If you manage on-premises devices using Microsoft Configuration Manager, then you can use co-management to cloud attach your on-premises devices. With co-management, you manage Windows client devices with Configuration Manager and Microsoft Intune.
>
> You can create the device profiles and policies you need in Intune based on policies you currently have in Configuration Manager. For more information about co-management, go [Understand co-management using Microsoft Configuration Manager](../../configmgr/comanage/overview.md). For related information, see [Prepare Intune for co-management](../../configmgr/core/get-started/capabilities-in-technical-preview-1709.md#prepare-intune-for-co-management).

## Use templates or the settings catalog

In Intune, for most platforms, when you create a device configuration profile, you have two policy types: **Templates** or the **[Settings Catalog](settings-catalog.md)**.

The settings catalog lists all the settings you can configure, and all in one place. Templates include a logical grouping of settings that configure a feature or concept, like email, kiosk devices, and device firmware.

Intune has many templates that include groups of settings that focus on different parts of device management, including accessing resources (VPN, Wi-Fi), security (antivirus, firewall, certificates), and Group Policy Objects (ADMX administrative templates).

You can create a baseline of profiles that all devices must have, or you can configure specific features based on your organization needs and levels of security. For more information, go to [Levels of protection and configuration in Microsoft Intune](../fundamentals/protection-configuration-levels.md).

This article gives an overview of the different types of profiles you can create. Use these profiles to allow or prevent some features on the devices.

## Administrative templates and Group policy

[Administrative templates](administrative-templates-windows.md) include hundreds of settings that you can configure for Internet Explorer, Microsoft Edge, OneDrive, remote desktop, Word, Excel, and other Office apps. These templates give administrators a simplified view of settings similar to group policy, and they're 100% cloud-based.

[Group Policy analytics](group-policy-analytics.md) analyzes your on-premises GPOs. It's a tool that helps you determine how your GPOs translate in the cloud. The output shows any deprecated settings and the settings that are available (or not available) to MDM providers, including Microsoft Intune.

This feature supports:

- Windows 11
- Windows 10

## Certificates

You use [certificates in Intune](../protect/certificates-configure.md) to authenticate your users so they can access applications and corporate resources through VPN, Wi-Fi, or email profiles. When you use certificates to authenticate these connections, your end users don't need to enter usernames and passwords.

Certificates are also used for signing and encrypting email using S/MIME. Common types of certificates used in Intune include trusted root certificates, Simple Certificate Enrollment Protocol (SCEP) certificates, and Public Key Cryptography Standards (PKCS) certificates.

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

If your organization uses smart cards for authentication, signing, or encryption, then you can use [derived credentials](../protect/derived-credentials.md). In Intune, you can configure and deploy a certificate that's derived from a user's smart card. Derived credentials are commonly used for Wi-Fi & VPN connections, app & email authentication, or S/MIME signing & encryption.

Intune [supports several derived credential issuers](../protect/derived-credentials.md#supported-issuers). Each platform also has their own set of settings.

This feature supports:

- Android Enterprise
- iOS/iPadOS

## Device features

[Device features](device-features-configure.md) controls features on iOS/iPadOS and macOS devices, such as AirPrint, notifications, and lock screen messages.

This feature supports:

- iOS/iPadOS
- macOS

## BIOS configuration and DFCI

With [BIOS configuration](bios-configuration.md), administrators can password-protect access to the BIOS and create a configuration file using an OEM tool with the BIOS settings they want. Then, they add this configuration file to the Intune policy.

[Device firmware configuration interface](device-firmware-configuration-interface-windows.md) (DFCI) allows administrators to enable or disable UEFI (BIOS) settings using Intune. Use these settings to enhance security at the firmware-level, which is typically more resilient to malicious attacks.

This feature supports:

- Windows 11
- Windows 10

## Device restrictions

[Device restrictions](device-restrictions-configure.md) controls security, hardware, data sharing, and more settings on the devices. For example, create a device restriction profile that prevents iOS/iPadOS device users from using the device camera.

There are also settings that manage access to app stores, restrict users from viewing corporate documents in unmanaged apps, require a password to unlock the device, or require devices to use only specific Wi-Fi networks.

This feature supports:

- Android device administrator
- Android (AOSP)
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 11
- Windows 10
- Windows 10 Team

## Domain join

[Domain join](domain-join-configure.md) configures on-premises Active Directory domain information. This information is deployed to Microsoft Entra hybrid joined devices when provisioned using Windows Autopilot and Intune. This profile tells devices which domain and OU to join.

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

> [!IMPORTANT]
> This template is deprecated in the August 2024 service release (2408). Existing policies continue to work. But, you can't create new policies using this template.
>
> Instead, use the settings catalog to create new policies that configure the FileVault, Firewall, and System Policy Control (Gatekeeper) payloads. To learn more, go to [macOS settings catalog](settings-catalog.md).

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

> [!IMPORTANT]
> This template is deprecated in the August 2024 service release (2408). Existing policies continue to work. But, you can't create new policies using this template.
>
> Instead, use the settings catalog to create new policies that configure the System Extensions payload. To learn more, go to [macOS settings catalog](settings-catalog.md).

[macOS system extensions and kernel extensions](kernel-extensions-overview-macos.md) allows administrators to add features or programs that extend the native capabilities of the operating system. Configure these settings to trust all extensions from a specific developer or partner, or allow specific extensions.

This feature supports:

- macOS

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

[Microsoft Defender for Endpoint](../protect/advanced-threat-protection.md) integrates with Intune to monitor and help protect devices. You set risk levels, and determine what happens if devices exceed that level. When combined with Conditional Access, you can help prevent malicious activity in your organization.

This feature supports:

- Windows 11
- Windows 10

## Network boundary

[Network boundary](network-boundary-windows.md) creates a list of sites that your organization trusts. This feature is used with Microsoft Defender Application Guard and Microsoft Edge to help protect your devices.

This feature supports:

- Windows 11
- Windows 10

## OEMConfig

On Android Enterprise devices, [OEMConfig](android-oem-configuration-overview.md) is a standard. It allows OEMs (original equipment manufacturers) and EMMs (enterprise mobility management) to build and support OEM-specific features in a standardized way.

With OEMConfig, an OEM creates a schema that defines OEM-specific management features, and embeds it in an app uploaded to Google Play. Intune reads the schema from the app, and allows Intune administrators to configure the settings in the schema.

This feature supports:

- Android Enterprise (OEMConfig)

## Preference file

[Preference files](preference-file-settings-macos.md) on macOS devices include information about apps. For example, you can use preference files to control web browser settings, customize apps, and more.

This feature supports:

- macOS

> [!TIP]
> macOS settings are continually being added to the [settings catalog](settings-catalog.md). Some of these settings can replace preference files. For more information, go to [Tasks you can complete using the Settings Catalog in Intune](settings-catalog-common-features.md).

## Settings catalog

The [settings catalog](settings-catalog.md) lists all the available settings you can configure, and all in one place. It's not template, or a logical grouping of settings. The settings catalog is similar to configuring on-premises Group Policy Objects (GPOs), but is cloud native.

On Windows, there are thousands of settings available, including many settings not found in the templates. When you want a complete list of all the settings, use the settings catalog to create your policy. If you want to use a logical grouping of settings, then continue to use the templates.

[Tasks you can complete using the Intune settings catalog](settings-catalog-common-features.md) is a good resource.

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

[Windows health monitoring](windows-health-monitoring.md) lets Endpoint Analytics collect and analyze your event data. You can use this data to get insights on your Windows devices, including software updates and startup performance.

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

## Manage and troubleshoot

[Manage your profiles](device-profile-monitor.md) to check the status of devices, and the profiles assigned. Also help resolve conflicts by seeing the settings that cause a conflict, and the profiles that include these settings.

[Common questions and behaviors with policies and profiles](device-profile-troubleshoot.md) helps administrators work with profiles. It describes what happens when deleting a profile, what causes notifications to be sent to devices, and more.

## Next steps

Choose a profile, and get started.
