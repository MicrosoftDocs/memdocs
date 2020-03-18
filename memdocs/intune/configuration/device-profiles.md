---
# required metadata

title: Device features and settings in Microsoft Intune - Azure | Microsoft Docs
description: Overview of the different Microsoft Intune device profiles. Get info on features, restrictions, email, wifi, VPN, education, certificates, upgrade Windows 10, BitLocker and Microsoft Defender, Windows Information Protection, administrative templates, and custom device configuration settings in the Microsoft Endpoint Manager admin center. Use these profiles to manage and protect data and devices in your company.
keywords:
author: MandiOhlinger

ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
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
ms.collection: M365-identity-device-management
---

# Apply features and settings on your devices using device profiles in Microsoft Intune

Microsoft Intune includes settings and features you can enable or disable on different devices within your organization. These settings and features are added to "configuration profiles". You can create profiles for different devices and different platforms, including iOS/iPadOS, Android device administrator, Android Enterprise, and Windows. Then, use Intune to apply or "assign" the profile to the devices.

As part of your mobile device management (MDM) solution, use these configuration profiles to complete different tasks. Some profile examples include:

- On Windows 10 devices, use a profile template that blocks ActiveX controls in Internet Explorer.
- On iOS/iPadOS and macOS devices, allow users to use AirPrint printers in your organization.
- Allow or prevent access to bluetooth on the device.
- Create a WiFi or VPN profile that gives different devices access to your corporate network.
- Manage software updates, including when they're installed.
- Run an Android device as dedicated kiosk device that can run one app, or run many apps.

This article gives an overview of the different types of profiles you can create. Use these profiles to allow or prevent some features on the devices.

## Administrative templates

[Administrative templates](administrative-templates-windows.md) include hundreds of settings that you can configure for Internet Explorer, OneDrive, remote desktop, Word, Excel, and other Office programs.

These templates give administrators a simplified view of settings similar to group-policy, but they're 100% cloud-based.

This feature supports:

- Windows 10 and later

## Certificates

[Certificates](../protect/certificates-configure.md) configure trusted, SCEP, and PKCS certificates that are assigned to devices. These certificates authenticate WiFi, VPN, and email profiles.

This feature supports: 

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1
- Windows 8.1
- Windows 10 and later

## Custom profile

[Custom settings](custom-settings-configure.md) let administrators assign device settings that aren't built in to Intune. On Android devices, you can enter OMA-URI values. For iOS/iPadOS devices, you can import a configuration file you created in the Apple Configurator.

This feature supports:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1

## Delivery optimization

[Delivery optimization](delivery-optimization-windows.md) provides a better experience to delivery software updates. These settings are replacing the **Software Updates** > **Windows 10 update ring** settings.

Use these settings to control how software updates are downloaded to devices in your organization. For example, you can let users get their own updates, or get updates using the delivery optimization cloud services in a device profile.

This feature supports:

- Windows 10 and later

## Device features

[Device features](device-features-configure.md) controls features on iOS/iPadOS and macOS devices, such as AirPrint, notifications, and lock screen messages.

This feature supports:

- iOS/iPadOS
- macOS

## Device firmware configuration interface

[Device firmware configuration interface](device-firmware-configuration-interface-windows.md) (DFCI) allows administrators to enable or disable UEFI (BIOS) settings using Intune. Use these settings to enhance security at the firmware-level, which is typically more resilient to malicious attacks.

This feature supports:

- Windows 10 1809 and later on supported firmware

## Device restrictions

[Device restrictions](device-restrictions-configure.md) controls security, hardware, data sharing, and more settings on the devices. For example, create a device restriction profile that prevents iOS/iPadOS device users from using the device camera. 

This feature supports:

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10 and later
- Windows 10 Team

## Domain join

[Domain join](domain-join-configure.md) configures on-premises Active Directory domain information. This information is deployed to hybrid Azure AD joined devices when provisioned using Windows Autopilot and Intune. This profile tells devices which domain and OU to join.

This feature supports:

- Windows 10 and later

## Edition upgrade

[Windows 10 edition upgrades](edition-upgrade-configure-windows-10.md) automatically upgrades devices that run some versions of Windows 10 to a newer edition.

This feature supports:

- Windows 10 and later

## Education

[Education settings - Windows 10](education-settings-configure.md) configure options for the [Windows Take a Test app](https://education.microsoft.com/gettrained/win10takeatest). When you configure these options, no other apps can run on the device until the test is complete.

[Education settings - iOS/iPadOS](../fundamentals/education-settings-configure-ios-shared.md) uses the iOS/iPadOS Classroom app to guide learning, and control student devices in the classroom. You can configure iPad devices so many students can share a single device.

## Email

[Email settings](email-settings-configure.md) creates, assigns, and monitors Exchange ActiveSync email settings on the devices. Email profiles help with consistency, reduce support calls, and let end-users access company email on their personal devices, without any required setup on their part. 

This feature supports: 

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- Windows Phone 8.1
- Windows 10 and later

## Endpoint protection

[Endpoint protection settings for Windows 10](../protect/endpoint-protection-windows-10.md) configures BitLocker and Microsoft Defender settings for Windows 10 devices.

To onboard Microsoft Defender Advanced Threat Protection (WDATP) with Microsoft Intune, see [Configure endpoints using Mobile Device Management (MDM) tools](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-mdm).

This feature supports:

- Windows 10 and later

## eSIM cellular - Public preview

[eSIM cellular profiles](esim-device-configuration.md) lets administrators configure cellular data plans on your managed devices for internet and data access. After getting activation codes from your mobile operator, use Intune to import these activation codes, and then assign to your eSIM capable devices.

This feature supports:

- Windows 10 Fall Creators Update and later

## Extensions

[Kernel extensions](kernel-extensions-overview-macos.md) allows administrators to add features or programs at the kernel-level on macOS devices. Configure these settings to trust all extensions from a specific developer or partner, or allow specific kernel extensions.

This feature supports:

- macOS

## Identity protection

[Identity protection](../protect/identity-protection-configure.md) controls the Windows Hello for Business experience on Windows 10 and Windows 10 Mobile devices. Configure these settings to make Windows Hello for Business available to users and devices, and to specify requirements for device PINs and gestures.  

This feature supports:  

- Windows 10 and later
- Windows Holographic for Business  

## Kiosk

[Kiosk settings](kiosk-settings.md) profile configures a device to run one app, or run many apps. You can also customize other features on your kiosk, including a start menu and a web browser.

This feature supports:

- Windows 10 and later

Kiosk settings also available as device restrictions for [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-device-settings), and [ios/iPadOS](device-restrictions-ios.md#kiosk).

## OEMConfig

[OEMConfig](android-oem-configuration-overview.md) is a standard that allows OEMs (original equipment manufacturers) and EMMs (enterprise mobility management) to build and support OEM-specific features in a standardized way on Android Enterprise devices. With OEMConfig, an OEM creates a schema that defines OEM-specific management features, and embeds it in an app uploaded to Google Play. Intune reads the schema from the app, allows Intune administrators to configure the settings in the schema.

This feature supports:

- Android Enterprise (OEMConfig)

## PowerShell scripts

[PowerShell scripts on Windows 10 devices](../apps/intune-management-extension.md) uses the Intune Management Extension to upload your PowerShell scripts in Intune, and then run these scripts on your devices. Also see what's required to use the extension, how to add them to Intune, and other important information.


This feature supports:

- Windows 10 and later
- Windows Holographic for Business

## Shared multi-user device

[Windows 10](shared-user-device-settings-windows.md) and [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) includes settings to manage devices with multiple users, also known as shared devices or shared PCs. When a user signs in to the device, you choose if the user can change the sleep options, or save files on the device. In another example, to save space, you can create a profile that deletes inactive credentials from Windows HoloLens devices.

These shared multi-user device settings allow an administrator to control some of the device features, and manage these shared devices using Intune.

This feature supports:

- Windows 10 and later
- Windows Holographic for Business

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
- Windows Phone 8.1
- Windows 8.1
- Windows 10 and later

## Wi-Fi

[Wi-Fi settings](wi-fi-settings-configure.md) assigns wireless network settings to users and devices. When you assign a WiFi profile, users get access to your corporate WiFi without having to configure it themselves. 

This feature supports: 

- Android device administrator
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 8.1 (import only)
- Windows 10 and later

## Windows Information Protection profile

[Windows Information Protection](../protect/windows-information-protection-configure.md) helps protect against data leakage without interfering with the employee experience. It also helps protect enterprise apps and data against accidental data leaks on enterprise-owned devices and personal devices that employees use at work. Using Windows Information Protection doesn't require changes to your environment or other apps.

This feature supports:

- Windows 10 and later

## Zebra Mobility Extensions (MX)

[Zebra Mobility Extensions (MX)](android-zebra-mx-overview.md) allows administrators to use and manage Zebra devices in Intune. You create StageNow profiles with your settings, and then use Intune to assign and deploy these profiles to your Zebra devices. The [StageNow logs and common issues](android-zebra-mx-logs-troubleshoot.md) is a great resource to troubleshoot profiles, and see some potential issues when using StageNow.

This feature supports:

- Android device administrator (Mobility Extensions)

## Manage and troubleshoot

[Manage your profiles](device-profile-monitor.md) to check the status of devices, and the profiles assigned. Also help resolve conflicts by seeing the settings that cause a conflict, and the profiles that include these settings. [Common issues and resolutions](device-profile-troubleshoot.md) helps administrators work with profiles. It describes what happens when deleting a profile, what causes notifications to be sent to devices, and more.

## Next steps

Choose your platform, and get started.
