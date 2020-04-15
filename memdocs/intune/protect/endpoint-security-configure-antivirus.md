---
# required metadata

title: Use Endpoint Security antivirus policy in Intune | Microsoft Docs
description: Configure the Endpoint Security policy for Antivirus for devices that run Windows 10 and macOS in Intune
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha

---

# Configure Antivirus policies in Intune

As part of Endpoint security in Intune, Antivirus policies make it easy for security admins to focus on managing the discrete group of antivirus settings for your managed devices. To use Antivirus policy, integrate Intune with Microsoft Defender Advanced Threat Protection (Defender ATP) as a Mobile Threat Defense solution.

Antivirus profiles contain only the settings that are relevant for Defender ATP antivirus for macOS and Windows 10, and for the user experience in the Windows Security app on Windows 10 devices.

While you can configure some of the same settings as part of *Endpoint Protection* profiles for [device configuration](../configuration/device-profile-create.md) or *device restriction* profiles for [device compliance](../protect/device-compliance-get-started.md), those other profiles include additional categories of settings that are unrelated to Antivirus, which can complicate the task of configuring Antivirus. Additionally, for macOS devices, the Antivirus settings are not available through other profiles. The macOS Antivirus profile replaces the need to configure the settings by using *.plist* files.

## Prerequisites

**Supported Platforms**

- macOS
- Windows 10 and later

**Defender ATP**

You must integrate Defender ATP with Intune and deploy Defender ATP to the devices you will manage with Antivirus policy.  

For more information, see the following articles as applicable for platforms you manage:

- [Microsoft Defender ATP for Windows](../protect/advanced-threat-protection.md) (In the Intune documentation)
- [Defender ATP for macOS](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (In the Defender ATP documentation)

## Antivirus profiles

The available profiles depend on the device platform.

### macOS

- **Antivirus** - Manage [Antivirus policy settings](../protect/antivirus-microsoft-defender-settings-macos.md) for macOS.

  When you use [Microsoft Defender ATP for Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac), you can configure and deploy Antivirus settings to your managed macOS devices through Intune instead of configuring those settings by use of *.plist* files.  

### Windows 10 and later

- **Microsoft Defender Antivirus** – Manage [Antivirus policy settings](../protect/antivirus-microsoft-defender-settings-windows.md) for Windows 10.

  Defender Antivirus is the next-generation protection component of Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP). Next-generation protection brings together machine learning, big-data analysis, in-depth threat resistance research, and cloud infrastructure to protect devices in your enterprise organization.

  Unlike other policy and profiles available under Endpoint security, the *Microsoft Defender Antivirus* profile settings for Windows are a special case. These settings are a new instance of settings that previously were managed as part of a *Device Restriction profile* for Device Compliance policy.

  The settings in the antivirus profile:
  - Are the same settings as found in device restrictions, but support a third option for configuration that's not available when configured as a device restriction profile.

  - Apply to devices that are co-managed with Configuration Manager, when the [co-management workload slider](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) for *Endpoint Protection* is set to Intune.

  Plan to use this new profile in place of configuring these settings with a device restriction profile.

- **Windows Security experience** - Manage the Windows Security app settings that end users can view in the Microsoft Defender Security center and the notifications they receive.

  The Windows Security app is used by a number of Windows security features to provide notifications about the health and security of the machine. These include notifications about firewalls, antivirus products, Windows Defender SmartScreen, and others.

## Configure profiles for Antivirus

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Antivirus** > **Create Policy**.

3. Select your **Platform**, select the **Profile** you want to configure for that platform, and then select **Create**.

4. On **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. A good policy name might include the *profile type* and *platform*.  
   - **Description**: Enter a description for the policy. This setting is optional, but recommended.

5. Select **Next**.

6. In **Configuration settings**, review and configure the settings you want to apply to devices. For additional information, use the links to view reference articles for the available settings.

   macOS:
   - **Antivirus** - macOS [Antivirus policy settings](../protect/antivirus-microsoft-defender-settings-macos.md)

   Windows 10:
   - **Microsoft Defender Antivirus** – Windows 10 [Antivirus policy settings](../protect/antivirus-microsoft-defender-settings-windows.md)
   - **Windows Security experience** - Windows 10 [Windows Security app policy settings](../protect/antivirus-security-experience-windows-settings.md)

7. Select **Next**.

8. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as US-NC IT Team or JohnGlenn_ITDepartment. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

   Select **Next**.

9. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   Select **Next**.

10. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Next step

Manage security task with [Endpoint security in Intune](../protect/endpoint-security.md)
