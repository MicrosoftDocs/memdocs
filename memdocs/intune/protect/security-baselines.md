---
# required metadata

title: Learn about Windows security baselines you can deploy with Microsoft Intune
description: Deploy security baselines to devices to help protect users and data on devices you manage with Microsoft Intune. The default baseline configurations are the recommended windows security settings from the relevant security teams. You can also customize baselines to meet your business requirements. 
keywords:
author: brenduns 
ms.author: brenduns
manager: dougeby
ms.date: 08/11/2022
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
   - contperf-fy21q1
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo

---

# Use security baselines to configure Windows devices in Intune

Intune makes it easy to deploy Windows security baselines to help you secure and protect your users and devices.

Even though Windows and Windows Server are designed to be secure out-of-the-box, many organizations still want more granular control over their security configurations. To navigate the large number of controls, organizations often seek guidance on configuring various security features. Microsoft provides this guidance in the form of security baselines.

Security baselines are groups of pre-configured Windows settings that help you apply and enforce granular security settings that are recommended by the relevant security teams. You can also customize each baseline you deploy to enforce only those settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple *device configuration* profiles.

To learn more about why and when you might want to deploy security baselines, see [Windows security baselines](/windows/security/threat-protection/windows-security-configuration-framework/windows-security-baselines) in the Windows security documentation.

This feature applies to:

- Windows 10 version 1809 and later
- Windows 11

You deploy security baselines to groups of users or devices in Intune, and the settings apply to devices that run Windows 10/11. For example, the *MDM Security Baseline* automatically enables BitLocker for removable drives, automatically requires a password to unlock a device, automatically disables basic authentication, and more. When a default value doesn't work for your environment, customize the baseline to apply the settings you need.

Separate baseline types can include the same settings and use different default values for those settings. It's important to understand the defaults in the baselines you choose to use, and to then modify each baseline to fit your organizational needs.

In almost all scenarios, the default settings in the security baselines are the most restrictive. You should confirm that these settings don't conflict with other policy settings or features in your environment.

For example, the default settings for firewall configuration might not merge connection security rules and local policy rules with MDM rules. So, if you're using delivery optimization, then you should validate these configurations before assigning the security baseline.

> [!NOTE]
> Microsoft doesn't recommend using preview versions of security baselines in a production environment. The settings in a preview baseline might change over the course of the preview.

Security baselines can help you to have an end-to-end secure workflow when working with Microsoft 365. Some of the benefits include:

- A security baseline includes the best practices and recommendations on settings that impact security. Intune partners with the same Windows security team that creates group policy security baselines. These recommendations are based on guidance and extensive experience.
- If you're new to Intune, and not sure where to start, then security baselines gives you an advantage. You can quickly create and deploy a secure profile, knowing that you're helping protect your organization's resources and data.
- If you currently use group policy, migrating to Intune for management is much easier with these baselines. These baselines are natively built in to Intune, and include a modern management experience.

## Available security baselines

The following security baseline instances are available for use with Intune. Use the links to view the settings for recent instances of each baseline.

- **Security Baseline for Windows 10 and later**  
  - [November 2021](security-baseline-settings-mdm-all.md?pivots=november-2021)
  - [December 2020](security-baseline-settings-mdm-all.md?pivots=december-2020)
  - [August 2020](security-baseline-settings-mdm-all.md?pivots=mdm-sept-2020)
<!-- deprecating from content 
  - [May 2019](security-baseline-settings-mdm-all.md?pivots=mdm-may-2019)
  - [Preview: MDM Security Baseline for October 2018](security-baseline-settings-mdm-all.md?pivots=mdm-preview)
-->

- **Microsoft Defender for Endpoint baseline**  
  *(To use this baseline your environment must meet the prerequisites for using [Microsoft Defender for Endpoint](advanced-threat-protection.md#prerequisites))*.
  - [Version 6](security-baseline-settings-defender-atp.md?pivots=december-2020)
  - [Version 5](security-baseline-settings-defender-atp.md?pivots=atp-sept-2020)
  - [Version 4](security-baseline-settings-defender-atp.md?pivots=atp-april-2020)
  - [Version 3](security-baseline-settings-defender-atp.md?pivots=atp-march-2020)

  > [!NOTE]
  > The Microsoft Defender for Endpoint security baseline has been optimized for physical devices and is currently not recommended for use on virtual machines (VMs) or VDI endpoints. Certain baseline settings can impact remote interactive sessions on virtualized environments.  For more information, see [Increase compliance to the Microsoft Defender for Endpoint security baseline](/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) in the Windows documentation.

- **Microsoft Edge Baseline**
  - [September 2020 (Edge version 85 and later)](security-baseline-settings-edge.md?pivots-edge-sept-2020)
  - [April 2020 (Edge version 80 and later)](security-baseline-settings-edge.md?pivots-edge-april-2020)
  - [Preview: October 2019 (Edge version 77 and later)](security-baseline-settings-edge.md?pivots=edge-october-2019)

- **Windows 365 Security Baseline**
  - [October 2021](security-baseline-settings-windows-365.md)

After a new version for a profile releases, settings in profiles based on the older versions become read-only. You can continue using those older profiles, including editing their name, description, and assignments, but you won't be able to edit settings for them or create new profiles based on the older versions.

When you're ready to use the more recent version of a baseline, you can create new profiles or update your existing profiles to the new version. See [Change the baseline version for a profile](security-baselines-configure.md#change-the-baseline-version-for-a-profile) in the *Manage security baseline profiles* article.

## About baseline versions and instances

Each new version instance of a baseline can add or remove settings or introduce other changes. For example, as new Windows settings become available with new versions of Windows 10/11, the MDM Security Baseline might receive a new version instance that includes the newest settings.

In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), under **Endpoint security** > **Security baselines** you'll see a list of the available baselines. The list includes:
- The baseline template name.
- How many profiles you have that use that type of baseline.
- How many separate instances (versions) of the baseline type are available.
- A *Last Published* date that identifies when the latest version of the baseline template became available.

To view more information about the baseline versions you use, select a baseline type, like *MDM Security Baseline* to open its *Profiles* pane, and then select **Versions**. Intune displays details about the versions of that baseline that are in use by your profiles. The details include the most recent and current baseline version. You can select a single version to view deeper details about the profiles that use that version.

You can choose to [change of the version](security-baselines-configure.md#change-the-baseline-version-for-a-profile) of a baseline that's in use with a given profile. When you change the version, you don't have to create a new baseline profile to take advantage of updated versions. Instead you can select a baseline profile and use the built-in option to change the instance version for that profile to a new one.

## Avoid conflicts

You can use one or more of the available baselines in your Intune environment at the same time. You can also use multiple instances of the same security baselines that have different customizations.

When you use multiple security baselines, review the settings in each one to identify when your different baseline configurations introduce conflicting values for the same setting. Because you can deploy security baselines that are designed for different intents, and deploy multiple instances of the same baseline that includes customized settings, you might create configuration conflicts for devices that must be investigated and resolved.

In addition, security baselines often manage the same settings you might set with [device configuration profiles](../configuration/device-profiles.md) or other types of policy. Therefore, remain aware of and consider your additional policies and profiles for settings when seeking to avoid or resolve conflicts.

Use the information at the following links to help identify and resolve conflicts:

- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
- [Monitor your security baselines](security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## Q & A

### Why these settings?

The Microsoft security team has years of experience working directly with Windows developers and the security community to create these recommendations. The settings in this baseline are considered the most relevant security-related configuration options. In each new build of Windows, the team adjusts its recommendations based on newly released features.

### Is there a difference in the recommendations for Windows security baselines for group policy vs. Intune?

The same Microsoft security team chose and organized the settings for each baseline. Intune includes all the relevant settings in the Intune security baseline. There are some settings in the group policy baseline that are specific to an on-premises domain controller. These settings are excluded from Intune's recommendations. All the other settings are the same.

### Are the Intune security baselines CIS or NIST compliant?

Strictly speaking, no. The Microsoft security team consults organizations, such as CIS, to compile its recommendations. But, there isn't a one-to-one mapping between "CIS-compliant" and Microsoft baselines.

### What certifications does Microsoft's security baselines have?

- Microsoft continues to publish security baselines for group policies (GPOs) and the [Security Compliance Toolkit](/windows/security/threat-protection/security-compliance-toolkit-10), as it has for many years. These baselines are used by many organizations. The recommendations in these baselines are from the Microsoft security team's engagement with enterprise customers and external agencies, including the Department of Defense (DoD), National Institute of Standards and Technology (NIST), and more. We share our recommendations and baselines with these organizations. These organizations also have their own recommendations that closely mirror Microsoft's recommendations. As mobile device management (MDM) continues to grow into the cloud, Microsoft created equivalent MDM recommendations of these group policy baselines. These additional baselines are built in to Microsoft Intune, and include compliance reports on users, groups, and devices that follow (or don't follow) the baseline.

- Many customers are using the Intune baseline recommendations as a starting point, and then customizing it to meet their IT and security demands. Microsoft's Windows 10 RS5 **MDM Security Baseline** is the first baseline to release. This baseline is built as a generic infrastructure that allows customers to eventually import other security baselines based on CIS, NIST, and other standards. Currently, it's available for Windows and will eventually include iOS/iPadOS and Android.

- Migrating from on-premises Active Directory group policies to a pure cloud solution using Azure Active Directory (AD) with Microsoft Intune is a journey. To help, use the various tools from the [Security Compliance Toolkit](/windows/security/threat-protection/security-compliance-toolkit-10) that can help you identify cloud-based options from security baselines that can replace your on-premises GPO configurations.

## Next steps

- [Create security baseline profiles](security-baselines-configure.md)

- Check the status and monitor the [baseline and profile](security-baselines-monitor.md)

- View the settings in the latest versions of the available baselines:
  - [MDM security baseline](security-baseline-settings-mdm-all.md)
  - [Microsoft Defender for Endpoint baseline](security-baseline-settings-defender-atp.md)
