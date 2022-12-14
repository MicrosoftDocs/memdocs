---
# required metadata

title: Protection and configuration levels overview in Microsoft Intune
titleSuffix: Microsoft Intune
description: Learn about the different levels of protection and configuration in Microsoft Intune, including minimum, enhanced, and high levels.
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/13/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite:
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: 
  - M365-identity-device-management 
  - highpri
---

# Layers of protection and configuration in Microsoft Intune

Microsoft Intune gives admins the ability to [create policies that are applied to users, devices, and apps](what-is-intune.md). These policies can range from a minimum set to more secure or controlled policies. These policies depend on the organization needs, the devices that are used, and what the devices will do.

When you're ready to create policies, you can use the different levels of protection and configuration:

- Level 1 - Minimum protection and configuration
- Level 2 - Enhanced protection and configuration
- Level 3 - High protection and configuration

Your environment and business needs may have different levels defined. You can use these levels as a starting point and then customize them to fit your needs. For example, you can use the device configuration policies in level 1 and the app policies in level 3.

Choose the levels that are right for your organization. There isn't a wrong choice.

> [!TIP]
>
> On Android and iOS/iPadOS devices, the Enterprise security configuration framework includes a granular list of settings and their recommended values. If you use these platforms, then Microsoft recommends using the framework settings.
>
> For more information, go to:
>
> - [**Android** enterprise security configuration framework](../enrollment/android-configuration-framework.md)
> - [**iOS/iPadOS** enterprise security configuration framework](../enrollment/ios-ipados-configuration-framework.md)

## Level 1 - Minimum protection and configuration

This level includes policies that every organization should have, at a minimum. The policies in this level create a minimum baseline of security features and give users access to the resources they need to do their jobs.

### Apps (level 1)

### Device compliance (level 1)

### Device configuration (level 1)

In this level, the profiles include settings that focus on security and resource access. Specifically, in this level, Microsoft recommends you configure the following features:

- Enable basic security, including:

  - Antivirus and scanning
  - Threat detection and response
  - Firewall
  - Software updates
  - Strong PIN and password policy

- Give users access to the network:

  - Email
  - VPN for remote access
  - Wi-Fi for on-premises access

For more information on these policies in this level, go to [Step 4 - Create device configuration profiles to secure devices and create connections to organization resources](deployment-plan-configuration-profile.md).

## Level 2 - Enhanced protection and configuration

This level expands on the minimum set of policies to include more security and expand your mobile device management. The policies in this level secure more features, provide identity protection, and manage more device settings.

Use the settings in this level to add what you've done in Level 1.

### Apps (level 2)

### Device compliance (level 2)

### Device configuration (level 2)

In this level, Microsoft recommends you create policies that:

- Add another layer of security using disk encryption and move towards password-less sign-in.
- Configure more granular device features, settings, and behaviors.

Specifically, in this level, you can:

- Enable disk encryption on your devices:

  - [**Windows**: Manage BitLocker](../protect/encrypt-devices.md)
  - [**macOS**: Use FileVault](../protect/encrypt-devices-filevault.md)

- Configure password-less authentication:

  - [**Windows**: Manage Windows Hello for Business when devices enroll](../protect/windows-hello.md)
  - [**Windows**: Manage Windows Hello for Business after devices enroll](../protect/identity-protection-configure.md)
  - [Azure AD identity protection overview](/azure/active-directory/identity-protection/overview-identity-protection)
  - [Azure AD multi-factor authentication](/azure/active-directory/authentication/concept-mfa-howitworks)

- Configure more in-depth settings and use your on-premises GPOs:

  - [**Device restrictions**: Many built-in settings that can control different parts of the devices, including security, hardware, data sharing, and more](../configuration/device-restrictions-configure.md)
  - [**iOS/iPadOS, macOS, Windows**: Use the Settings catalog to see all the available settings](../configuration/settings-catalog.md)
  - **Windows 10/11**:
    - [Use built-in administrative templates](../configuration/administrative-templates-windows.md)
    - [Analyze your on-premises GPOs and import them in Intune](../configuration/group-policy-analytics.md)


## Level 3 - High protection and configuration

This level includes enterprise-level policies and may involve different admins in your organization. These policies continue moving to password-less authentication, additional security, and configuring specialized devices.

Use the settings in this level to add what you've done in Levels 1 and 2.

### Apps (level 3)

### Device compliance (level 3)


### Device configuration (level 3)

In this level, you can create policies that:

- Use certificate based authentication to access resources and use single-sign on for apps.
- Prevent malware from communicating with the Windows OS processes.
- Configure specialized devices like kiosks and shared devices.
- Deploy scripts.


Specifically, in this level, you can:

- Use certificates for authentication and authorization:

  - [Use PKCS or SCEP certificates for authentication](../protect/certificates-configure.md)
  - [Use derived credentials](../protect/derived-credentials.md)

- Enable single sign-on (SSO):
  - [**Android**: Enable cross-app SSO on Android using MSAL](/azure/active-directory/develop/msal-android-single-sign-on)
  - [**iOS/iPadOS, macOS**: Use the Enterprise SSO plug-in](../configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)
  - [**Windows**: Configure SSO with Azure AD](/azure/active-directory/manage-apps/what-is-single-sign-on)

- Create policies that apply to the Windows firmware layer

  - [Use Device Firmware Configuration Interface (DFCI) profiles on Windows devices](../configuration/device-firmware-configuration-interface-windows.md)

- Configure kiosks, shared devices, and other specialized devices:

  - **Android device administrator**
    - [Use and manage Zebra devices with Zebra Mobility Extensions](../configuration/android-zebra-mx-overview.md)
    - [Device settings to run as a kiosk](../configuration/device-restrictions-android.md#kiosk)

  - **Android Enterprise**:
    - [Use and manage Android Enterprise devices with OEMConfig](../configuration/android-oem-configuration-overview.md)
    - [Dedicated devices that run as a kiosk device settings](../configuration/device-restrictions-android-for-work.md#dedicated-devices)

  - **iOS/iPadOS**
    - [Device settings to run in autonomous single app mode (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam)
    - [Device settings to run as a kiosk](../configuration/device-restrictions-ios.md#kiosk)

  - **Windows**
    - [Device settings to run as a dedicated kiosk](../configuration/kiosk-settings.md)
    - [Device settings to run as a kiosk](../configuration/kiosk-settings-windows.md)
    - [Shared PC or multi-user devices](../configuration/shared-user-device-settings.md)
  - **Windows Holographic for Business**
    - [Device settings to run as a kiosk](../configuration/kiosk-settings-holographic.md)
    - [Device settings to run as a dedicated kiosk](../configuration/kiosk-settings.md)

- Deploy scripts:
  - [**macOS**: Use shell scripts](../apps/macos-shell-scripts.md)
  - [**Windows**: Use Windows PowerShell scripts](../apps/intune-management-extension.md)

## Next steps

For a complete list of all the device configuration profiles you can create, go to [Apply features and settings on your devices using device profiles in Microsoft Intune](../configuration/device-profiles.md).
