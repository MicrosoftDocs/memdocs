---
# required metadata

title: Protection and configuration levels overview in Microsoft Intune
titleSuffix: Microsoft Intune
description: Learn about the different levels of protection and configuration in Microsoft Intune, including minimum, enhanced, and high levels.
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/08/2023
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
- tier1
---

# Levels of protection and configuration in Microsoft Intune

Microsoft Intune gives admins the ability to [create policies that are applied to users, devices, and apps](what-is-intune.md). These policies can range from a minimum set to more secure or controlled policies. These policies depend on the organization needs, the devices that are used, and what the devices will do.

When you're ready to create policies, you can use the different levels of protection and configuration:

- [Level 1 - Minimum protection and configuration](#level-1---minimum-protection-and-configuration)
- [Level 2 - Enhanced protection and configuration](#level-2---enhanced-protection-and-configuration)
- [Level 3 - High protection and configuration](#level-3---high-protection-and-configuration)

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

This level enforces a reasonable amount of data protection and access requirements while minimizing the impact to users. This level ensures that apps are protected with a PIN and encrypted and performs selective wipe operations. For Android devices, this level validates Android device attestation. This level is an entry level configuration that provides similar data protection control in Exchange Online mailbox policies. It also introduces IT and the user population to app protection policies.

In this level, Microsoft recommends you configure the following protection and access for apps:
 
- Enable basic data protection requirements:
  - Allow app basic data transfer
  - Enforce basic app encryption
  - Allow basic access functionality
  
- Enable basic access requirements:
  - Require PIN, face ID, and biometric access
  - Enforce supporting basic access settings

- Enable basic conditional application launch:
  - Configure app basic access attempts
  - Block app access based on jailbroken/rooted devices
  - Restrict app access based on basic integrity of devices

For more information, see [Level 1 basic app protection](../apps/app-protection-framework.md#level-1-enterprise-basic-data-protection).

### Compliance (level 1)

In this level, device compliance includes configuring the tenant-wide settings that apply to all devices, and deploying minimal compliance policies to all devices to enforce a core set of compliance requirements. Microsoft recommends that these configurations be in place before you allow devices to access your organization’s resources. Level 1 device compliance includes:

*Compliance policy settings* are a few tenant-wide settings that affect how the Intune compliance service works with your devices.

*Platform-specific compliance policies* include settings for common themes across platforms. The actual setting name and implementation can be different between different platforms:

- Require antivirus, antispyware, and antimalware (Windows only)
- Operating system version:
  - Maximum OS
  - Minimum OS
  - Minor and Major build versions
  - OS patch levels
- Password configurations
  - Enforce lock screen after period of inactivity, requiring a password or pin to unlock
  - Require complex passwords with combinations of letters, numbers, and symbols
  - Require a password or PIN to unlock devices
  - Require minimum password length

*Actions for noncompliance* are automatically included with each platform specific policy. These actions are one or more time-ordered actions you configure that apply to devices that fail to meet the compliance requirements of the policy. By default, marking a device as non-compliant is an immediate action that’s included in each policy.

For more information, see [Level 1 - Minimal device compliance](../fundamentals/deployment-plan-compliance-policies.md#level-1---minimal-device-compliance).

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

This level recommends a standard level of application protection for devices where users access more sensitive information. This level introduces app protection policy data leakage prevention mechanisms and minimum OS requirements. This level is the configuration that is applicable to most mobile users accessing work or school data.

In addition to Level 1 settings, Microsoft recommends you configure the following protection and access for apps:

- Enable enhanced data protection requirements:
  - Transfer organization related data
  - Exempt selected apps data transfer requirements (iOS/iPadOS)
  - Transfer telecommunication data
  - Restrict cut, copy, and paste between apps
  - Block screen capture (Android)
  
- Enable enhanced conditional application launch:
  - Block disabling application accounts
  - Enforce minimum device OS requirements
  - Require minimum patch version (Android)
  - Require SafetyNet evaluation type (Android)
  - Require device lock (Android)
  - Allow app access based on increased integrity of device

For more information, see [Level 2 enhanced app protection](../apps/app-protection-framework.md#level-2-enterprise-enhanced-data-protection).

### Compliance (level 2)

At this level, Microsoft recommends adding more complex options to your compliance policies. Many of the settings at this level have platform-specific names that all deliver similar results. The following are the categories or types of settings that Microsoft recommends you use when they're available:

- Applications:
  - Manage where devices get apps, like Google Play for Android
  - Allow apps from specific locations
  - Block apps from unknown sources

- Firewall settings
  - Firewall settings (macOS, Windows)

- Encryption:
  - Require encryption of data storage
  - BitLocker (Windows)
  - FileVault (macOS)

- Passwords
  - Password expiration and reuse

- System level file and boot protection:
  - Block USB debugging (Android)
  - Block rooted or jailbroken devices (Android, iOS)
  - Require system integrity protection (macOS)
  - Require code integrity (Windows)
  - Require secure boot to be enabled (Windows)
  - Trusted Platform Module (Windows)

For more information, see [Level 2 - Enhanced device compliance settings](../fundamentals/deployment-plan-compliance-policies.md#level-2---enhanced-device-compliance-settings).

### Device configuration (level 2)

In this level, you're expanding on the settings and features you configured in level 1. Microsoft recommends you create policies that:

- Add another layer of security by enabling disk encryption, secure boot, and TPM on your devices.
- Configure your PINs & passwords to expire and manage if/when passwords can be reused.
- Configure more granular device features, settings, and behaviors.
- If you have on-premises GPOs, then you can determine if these GPOs are available in Intune.

For more specific information on device configuration policies at this level, go to [Level 2 - Enhanced protection and configuration](deployment-plan-configuration-profile.md#level-2---enhanced-protection-and-configuration).

## Level 3 - High protection and configuration

This level includes enterprise-level policies and may involve different admins in your organization. These policies continue moving to password-less authentication, have more security, and configure specialized devices.

Use the settings in this level to add what you've done in Levels 1 and 2.

### Apps (level 3)

This level recommends a standard level of application protection for devices where users access more sensitive information. This level introduces advanced data protection mechanisms, enhanced PIN configuration, and app protection policy Mobile Threat Defense. This configuration is desirable for users that are accessing high risk data.

In addition to level 1 and 2 settings, Microsoft recommends you configure the following protection and access for apps:

- Enable high data protection requirements:
  - High protection when transferring telecommunication data
  - Receive data from only policy managed apps
  - Block opening data into organization documents
  - Allow users to open data from selected services
  - Block third-party keyboards
  - Require/select approved keyboards (Android)
  - Block printing organization data
  
- Enable high access requirements:
  - Block simple PIN and require specific minimum PIN length
  - Require PIN reset after number of days
  - Require class 3 Biometrics (Android 9.0+)
  - Require override of Biometrics with PIN after biometric updates (Android)

- Enable high conditional application launch:
  - Require device lock (Android)
  - Require max allowed threat level
  - Require Max OS version

For more information, see [Level 3 high app protection](../apps/app-protection-framework.md#level-3-enterprise-high-data-protection).

### Compliance (level 3)

At this level, you can expand on Intune’s built-in compliance capabilities through the following capabilities:

- Integrate data from Mobile Threat Defense (MTD) partner
  - With an MTD partner, your compliance policies can require devices be at or under a *device threat level* or *machine risk score*, as determined by that partner

- Use a third-party compliance partner with Intune
- Use scripts to add custom compliance settings to your policies for settings that aren't available from within the Intune UI. (Windows, Linux)
- Use compliance policy data with Conditional Access policies to gate access to your organization’s resources

For more information, see [Level 3 - Advanced device compliance configurations](../fundamentals/deployment-plan-compliance-policies.md#level-3---advanced-device-compliance-configurations).

### Device configuration (level 3)

This level focuses on enterprise-level services and features, and can require an infrastructure investment. In this level, you can create policies that:

- Expand password-less authentication to other services in your organization, including certificate based authentication, single-sign on for apps, multi-factor authentication (MFA), and the Microsoft Tunnel VPN gateway.
- Configure device features that apply to the Windows firmware layer. Use Android common criteria mode.
- Configure specialized devices like kiosks and shared devices.
- Deploy scripts, if needed.

For more specific information on device configuration policies at this level, go to [Level 3 - High protection and configuration](deployment-plan-configuration-profile.md#level-3---high-protection-and-configuration).

## Next steps

For a complete list of all the device configuration profiles you can create, go to [Apply features and settings on your devices using device profiles in Microsoft Intune](../configuration/device-profiles.md).
