---
# required metadata

title: Learn about Intune security baselines for Windows devices
description: Deploy security baselines that have preset and recommended configurations to the Windows devices you manage with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/27/2025
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: juidaewo
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom:
  - intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
- sub-secure-endpoints
---

# Use security baselines to help secure Windows devices you manage with Microsoft Intune

With Microsoft Intune’s security baselines, you can rapidly deploy a recommended security posture to your managed Windows devices for Windows security baselines to help you secure and protect your users and devices.

Even though Windows and Windows Server are designed to be secure out-of-the-box, many organizations still want more granular control over their security configurations. To navigate the large number of controls, organizations often seek guidance on configuring various security features. Microsoft provides this guidance in the form of security baselines.

This feature applies to:

- Windows 10 version 1809 and later
- Windows 11

## Intune security baseline overview

Each security baseline is a group of preconfigured Windows settings that help you apply and enforce granular security settings that the relevant security teams recommend. You can also customize each baseline you deploy to enforce only those settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple *device configuration* profiles.

The settings in each baseline are device configuration settings like those found in various Intune policies. Each setting in a baseline works with the configuration service provider for the relevant product that is present on a managed windows device.

To learn more about why and when you might want to deploy security baselines, see [Windows security baselines](/windows/security/threat-protection/windows-security-configuration-framework/windows-security-baselines) in the Windows security documentation.

You deploy security baselines to groups of users or devices in Intune, and the settings apply to devices that run Windows 10 or 11. For example, the default configuration of the *Security Baseline for Windows 10 and later* automatically enables BitLocker for removable drives, automatically requires a password to unlock a device, automatically disables basic authentication, and more. When a default value doesn't work for your environment, customize the baseline to apply the settings you need.

> [!NOTE]
>
> In May 2023, Intune began rollout of a new security baseline format for each new baseline release or version update. The new format updates the baseline settings to directly take their name and configuration options from the configuration service provider (CSP) that the baseline setting manages.
>
> Intune also introduced a new process to help you migrate an existing security baseline profile to the newer baseline version. This new behavior is a one-time process that replaces the normal update behavior when you move from the most recent version of an older profile to a newer version that became available in May 2023 or later.

**Benefits of using baselines**:  
Security baselines can help you to have an end-to-end secure workflow when working with Microsoft 365. Some of the benefits include:

- By default, each security baseline is configured to meet the best practices and recommendations for the settings that affect security. Intune partners with the same Windows security team that creates group policy security baselines. These recommendations are based on guidance and extensive experience.
- If you're new to Intune, and not sure where to start, security baselines give you an advantage. You can quickly create and deploy a secure profile, knowing that you're helping protect your organization's resources and data.
- If you currently use group policy, migrating to Intune for management is easier with these baselines. These baselines are natively built into Intune, and include a modern management experience.

**Default settings across multiple baselines**:  
Separate baseline types, like the MDM security baseline for Windows and the baseline for Microsoft Defender, might include the same settings and use different default values for those settings. Intune can’t determine which configuration is best for you, or even in which environment or scenario you might want to use one baselines default recommendation over another:

- It's important to understand the defaults in the baselines you use, and to then modify each baseline to fit your organizational needs.
- By default, each baseline is preconfigured using the recommendations that are specific to the product it applies to.
- In some cases, a configuration that Microsoft Defender recommends might not be the default configuration for similar settings when recommended by Windows. In such situations, it’s important to review each setting so you can understand its intent based on the configuration service provider details, and larger scope of the two products.

In almost all scenarios, the default settings in the security baselines are the most restrictive. You should confirm that these settings don't conflict with other policy settings or features in your environment.

For example, the default settings for firewall configuration might not merge connection security rules and local policy rules with MDM rules. So, if you're using delivery optimization, then you should validate these configurations before assigning the security baseline.

> [!NOTE]
>
> Microsoft doesn't recommend using preview versions of security baselines in a production environment. The settings in a preview baseline might change over the course of the preview.

## Available security baselines

The following security baseline instances are available for use with Intune. Use the links to view the settings for recent instances of each baseline.

- **Security Baseline for Windows 10 and later**:  
  - [Version 23H2](security-baseline-settings-mdm-all.md?pivots=mdm-23h2)
  - [November 2021](security-baseline-settings-mdm-all.md?pivots=november-2021)
  - [December 2020](security-baseline-settings-mdm-all.md?pivots=december-2020)
  - [August 2020](security-baseline-settings-mdm-all.md?pivots=mdm-sept-2020)

<!-- Deprecating outdated baselines from content:
  - [May 2019](security-baseline-settings-mdm-all.md?pivots=mdm-may-2019)
  - [Preview: MDM Security Baseline for October 2018](security-baseline-settings-mdm-all.md?pivots=mdm-preview)
-->

- **Microsoft Defender for Endpoint baseline**:  
  *(To use this baseline your environment must meet the prerequisites for using [Microsoft Defender for Endpoint](advanced-threat-protection.md#prerequisites))*.
  - [Version 24H1](security-baseline-settings-defender.md?pivots=mde-v24h1)
  - [Version 6](security-baseline-settings-defender.md?pivots=atp-december-2020)
  - [Version 5](security-baseline-settings-defender.md?pivots=atp-sept-2020)
  - [Version 4](security-baseline-settings-defender.md?pivots=atp-april-2020)
  - [Version 3](security-baseline-settings-defender.md?pivots=atp-march-2020)

  > [!NOTE]
  > The Microsoft Defender for Endpoint security baseline has been optimized for physical devices and is currently not recommended for use on virtual machines (VMs) or VDI endpoints. Certain baseline settings can impact remote interactive sessions on virtualized environments. For more information, see [Increase compliance to the Microsoft Defender for Endpoint security baseline](/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) in the Windows documentation.

- **Microsoft 365 Apps for Enterprise**:  
  - [Version 2306 (Office baseline)](../protect/security-baseline-v2-office-settings.md?pivots=v2023) *Released in November 2023*
  - [May 2023 (Office baseline)](../protect/security-baseline-v2-office-settings.md?pivots=office-may-2023)

- **Microsoft Edge Baseline**:
  - [Microsoft Edge version 128](../protect/security-baseline-v2-edge-settings.md?pivots=edge-v128) - January 2025
  - [Microsoft Edge version 117](../protect/security-baseline-v2-edge-settings.md?pivots=edge-v117) - November 2023
  - [Microsoft Edge version 112 and later](../protect/security-baseline-v2-edge-settings.md?pivots=edge-v112) - May 2023
  - [Microsoft Edge version 85 and later](../protect/security-baseline-settings-edge.md?pivots-edge-sept-2020) - September 2020
  - [Microsoft Edge version 80 and later](../protect/security-baseline-settings-edge.md?pivots-edge-april-2020) - April 2020
  - [Preview: Microsoft Edge version 77 and later](../protect/security-baseline-settings-edge.md?pivots=edge-october-2019) - October 2019

- **Windows 365 Security Baseline**:
  - [Version 24H1](security-baseline-settings-windows-365.md?pivots=win365-24h1)
  - [November 2021](security-baseline-settings-windows-365.md?pivots=win365-nov21)

When a new version for a profile becomes available, settings in profiles based on the older versions become read-only. You can continue to use those older profiles. You can also edit the profile names, description, and assignments, but they don't support a change to their settings configuration and you can't create new profiles based on the older versions.

When you're ready to use the more recent baseline version, you can create new profiles or update your existing profiles to the new version. See [Change the baseline version for a profile](../protect/security-baselines-configure.md#update-a-profile-to-the-latest-version) in the *Manage security baseline profiles* article.

## About baseline versions and instances

Each new version instance of a baseline can add or remove settings or introduce other changes. For example, as new Windows settings become available with new versions of Windows 10/11, *Security Baseline for Windows 10 and later* might receive a new version instance that includes the newest settings.

You can view the list of available baselines in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), under **Endpoint security** > **Security baselines**. The list includes:

- The name of each security baseline template.
- How many profiles you have that use that type of baseline.
- How many separate instances (versions) of the baseline type are available.
- A *Last Published* date that identifies when the latest version of the baseline template became available.

To view more information about the baseline versions you use, select a baseline type, like *Security Baseline for Windows 10 and later* to open its *Profiles* pane, and then select **Versions**. Intune displays details about the versions of that baseline that are in use by your profiles. The details include the most recent and current baseline version. You can select a single version to view deeper details about the profiles that use that version.

You can choose to [change the version](../protect/security-baselines-configure.md#update-a-profile-to-the-latest-version) of a baseline that's in use with a given profile. When you change the version, you don't have to create a new baseline profile to take advantage of updated versions. Instead you can select a baseline profile and use the built-in option to change the instance version for that profile to a new one.

## Avoid conflicts

You can use one or more of the available baselines in your Intune environment at the same time. You can also use multiple instances of the same security baselines that have different customizations.

When you use multiple security baselines, review the settings in each one to identify when your different baseline configurations introduce conflicting values for the same setting. Because you can deploy security baselines that are designed for different intents, and deploy multiple instances of the same baseline that includes customized settings, you might create configuration conflicts for devices that must be investigated and resolved.

In addition, security baselines often manage the same settings you might set with [device configuration profiles](../configuration/device-profiles.md) or other types of policy. Therefore, remain aware of and consider your other policies and profiles for settings when seeking to avoid or resolve conflicts.

For information that can help you identify and resolve conflicts, see:

- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
- [Monitor your security baselines](security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## Q & A

### Why these settings?

The Microsoft security team has years of experience working directly with Windows developers and the security community to create these recommendations. The settings in this baseline are considered the most relevant security-related configuration options. In each new build of Windows, the team adjusts its recommendations based on newly released features.

### Is there a difference in the recommendations for Windows security baselines for group policy vs. Intune?

The same Microsoft security team chose and organized the settings for each baseline. Intune includes all the relevant settings in the Intune security baseline. There are some settings in the group policy baseline that are specific to an on-premises domain controller. These settings are excluded from Intune's recommendations. All the other settings are the same.

### Are the Intune security baselines CIS or NIST compliant?

Strictly speaking, no. The Microsoft security team consults organizations, such as CIS, to compile its recommendations. However, there isn't a one-to-one mapping between "CIS-compliant" and Microsoft baselines.

### What certifications do Microsoft's security baselines have?

Microsoft continues to publish security baselines for group policies (GPOs) and the [Security Compliance Toolkit](/windows/security/threat-protection/security-compliance-toolkit-10), as it has for many years. These baselines are used by many organizations. The recommendations in these baselines are from the Microsoft security team's engagement with enterprise customers and external agencies, including the Department of Defense (DoD), National Institute of Standards and Technology (NIST), and more. We share our recommendations and baselines with these organizations. These organizations also have their own recommendations that closely mirror Microsoft's recommendations. As mobile device management (MDM) continues to grow into the cloud, Microsoft created equivalent MDM recommendations of these group policy baselines. Many of these baselines are built into Microsoft Intune, and include compliance reports on users, groups, and devices that follow (or don't follow) the baseline.

Many customers use the Intune baseline recommendations as a starting point, and then customize them to meet their IT and security demands. Microsoft's Windows 10 and later baseline template was the first baseline to release. This baseline is built as a generic infrastructure that allows customers to eventually import other security baselines based on CIS, NIST, and other standards.

Migrating from on-premises Active Directory group policies to a pure cloud solution using Microsoft Entra ID with Microsoft Intune is a journey. To help, use the various tools from the [Security Compliance Toolkit](/windows/security/threat-protection/security-compliance-toolkit-10) that can help you identify cloud-based options from security baselines that can replace your on-premises GPO configurations.

### Where can I find details about using or configuring the settings that are available in a security baseline?

Each security baseline manages device configurations by applying the options found in a configuration service provider on a device. For example, settings that apply to Microsoft Defender are taken from the Microsoft Defender CSP. Because Intune is a configuration vehicle for those options and doesn’t determine their functionality or scope, the CSP documentation owns the content for how to configure each option.

Within the Intune security baseline policy UI, Intune provides information text that is taken from the source CSP and provides a link to that CSP. In some cases, the CSP might be part of a larger content set that includes proactive guidance that remains beyond the scope of Intune to include or duplicate in our content. However, Intune does document the list of settings in each security baseline version and its default configuration.

## Next steps

- [Create security baseline profiles](security-baselines-configure.md)

- Check the status and monitor the [baseline and profile](security-baselines-monitor.md)

- View the settings in the latest versions of the available baselines:
  - [Windows 10 and later - MDM security baseline](security-baseline-settings-mdm-all.md)
  - [Microsoft Defender for Endpoint baseline](security-baseline-settings-defender.md)
  - [Microsoft 365 Apps for Enterprise security baseline (Office)](security-baseline-v2-office-settings.md)
  - [Microsoft Edge security baseline](security-baseline-settings-edge.md)
  - [Windows 365 Security Baseline](security-baseline-settings-windows-365.md)
