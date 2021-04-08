---
# required metadata

title: Manage antivirus settings with endpoint security policies in Microsoft Intune | Microsoft Docs
description: Configure and deploy policies and use reports for devices you manage with endpoint security antivirus policy in Microsoft Endpoint Manager. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/29/2021
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

# Antivirus policy for endpoint security in Intune

Intune Endpoint security Antivirus policies can help security admins focus on managing the discrete group of antivirus settings for managed devices. To use Antivirus policy, integrate Intune with Microsoft Defender for Endpoint as a Mobile Threat Defense solution.

Antivirus policy includes several profiles. Each profile contains only the settings that are relevant for Microsoft Defender for Endpoint antivirus for macOS, Windows 10, or for the user experience in the Windows Security app on Windows 10 devices.

You'll find the antivirus policies under **Manage** in the Endpoint security node of the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

Antivirus policies include the same settings as *endpoint protection* or *device restriction* profiles for [device configuration](../configuration/device-profile-create.md) policy and are similar to settings from [device compliance](../protect/device-compliance-get-started.md) policy. However, those policy types include additional categories of settings that are unrelated to Antivirus. The additional settings can complicate the task of configuring Antivirus. Additionally, the settings found in the Antivirus policy for macOS aren't available through the other policy types. The macOS Antivirus profile replaces the need to configure the settings by using `.plist` files.

## Prerequisites for antivirus policy

**General**:

- **macOS**
  - Any supported version of macOS
  - For Intune to manage antivirus settings on a device, Microsoft Defender for Endpoint must be installed on that device. See. [Microsoft Defender for Endpoint for macOS](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (In the Microsoft Defender for Endpoint documentation)

- **Windows 10 and later**
  - No additional prerequisites are required.

**Support for Configuration Manager clients**:

*This scenario is in preview and requires use of Configuration Manager current branch version 2006 or later*.

- **Set up tenant attach for Configuration Manager devices** - To support deploying antivirus policy to devices managed by Configuration Manager, configure *tenant attach*. Set up of tenant attach includes configuring Configuration Manager device collections to support endpoint security policies from Intune.

  To set up tenant attach, see [Configure tenant attach to support endpoint protection policies](../protect/tenant-attach-intune.md).

### Prerequisites for tamper protection

You can use Intune to manage tamper protection on Windows devices as part of Antivirus policy. This includes both devices you manage with Intune, and devices you manage with Configuration Manager through the tenant attach scenario.

#### Intune managed devices

Prerequisites to support tamper protection for devices managed by Intune:

- Your environment must meet the [prerequisites for managing  tamper protection with Intune](/windows/security/threat-protection/microsoft-defender-antivirus/prevent-changes-to-security-settings-with-tamper-protection#turn-tamper-protection-on-or-off-for-your-organization-using-intune) as detailed in the Windows documentation.

Profiles for *Antivirus* policy that support tamper protection for [devices managed by Intune](#devices-managed-by-intune):

- Platform: **Windows 10 later**
  - Profile: **Windows Security experience**  

You can also use the [Endpoint protection](../protect/endpoint-protection-configure.md) profile for *Device configuration* policy to configure tamper protection for devices managed by Intune.

#### Configuration Manager clients managed through the tenant attach scenario

Prerequisites to support managing tamper protection with these profiles:

- Your environment must meet the [prerequisites for managing  tamper protection with Intune](/windows/security/threat-protection/microsoft-defender-antivirus/prevent-changes-to-security-settings-with-tamper-protection#turn-tamper-protection-on-or-off-for-your-organization-using-intune) as detailed in the Windows documentation.
- You must use Configuration Manager current branch 2006 or later.
- You must configure tenant attach to support endpoint protection policies. This includes configuring Configuration Manager device collections for synchronization with Intune.

 Profiles for *Antivirus* policy that support tamper protection for [devices managed by Configuration Manager](#devices-managed-by-configuration-manager):

- Platform: **Windows 10 and Windows Server (ConfigMgr)**
  - Profile: **Windows Security experience (preview)**

## Antivirus profiles

### Devices managed by Intune

The following profiles are supported for devices you manage with Intune:

**macOS**:

- Platform: **macOS**

  - Profile: **Antivirus** - Manage [Antivirus policy settings](../protect/antivirus-microsoft-defender-settings-macos.md) for macOS.

    When you use [Microsoft Defender for Endpoint for Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac), you can configure and deploy Antivirus settings to your managed macOS devices through Intune instead of configuring those settings by use of `.plist` files.

**Windows 10**:

- Platform: **Windows 10 profiles**

  - Profile: **Microsoft Defender Antivirus** - Manage [Antivirus policy settings](../protect/antivirus-microsoft-defender-settings-windows.md) for Windows 10.

    Defender Antivirus is the next-generation protection component of Microsoft Defender for Endpoint. Next-generation protection brings together technologies like machine learning and cloud infrastructure to protect devices in your enterprise organization.

    The *Microsoft Defender Antivirus* profile is a separate instance of the antivirus settings that are found in the *Device Restriction profile* for Device Configuration policy.
  
    Unlike the antivirus settings in a *Device Restriction profile*, you can use these settings to with devices that are co-managed. To use these settings, the [co-management workload slider](/configmgr/comanage/how-to-switch-workloads) for Endpoint Protection must be set to Intune.

  - Profile: **Microsoft Defender Antivirus exclusions** - Manage policy settings for only [Antivirus exclusions](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions).
  
    With this policy, you can manage settings for the following Microsoft Defender Antivirus configuration service providers (CSPs) that define Antivirus exclusions:

    - Defender/ExcludedPaths
    - Defender/ExcludedExtensions
    - Defender/ExcludedProcesses

    These CSPs for antivirus exclusion are also managed by *Microsoft Defender Antivirus* policy, which includes identical settings for exclusions. Settings from both policy types  (*Antivirus* and *Antivirus exclusions*) are subject to [policy merge](#policy-merge-for-settings), and create a super set of exclusions for applicable devices and users.

  - Profile: **Windows Security experience**-  Manage the [Windows Security app settings](../protect/antivirus-security-experience-windows-settings.md) that end users can view in the Microsoft Defender Security center and the notifications they receive.

    The Windows security app is used by a number of Windows security features to provide notifications about the health and security of the machine. Security app notifications include firewalls, antivirus products, Windows Defender SmartScreen, and others.

### Devices managed by Configuration Manager

[!INCLUDE [antivirus policy prerequisites](../includes/tenant-attach-antivirus-prerequisites.md)]

## Policy merge for settings

Some Antivirus policy settings support *policy merge*. Policy merge helps avoid conflicts when multiple policies apply to the same devices and configure the same setting. Intune evaluates the settings that policy merge supports, for each user or device as taken from all applicable policies. Those settings are then merged into a single superset of policy.

For example, you create three separate antivirus policies that define different antivirus file path exclusions. Eventually, all three policies are assigned to the same user. Because the Microsoft Defender file path exclusion CSP supports policy merge, Intune evaluates and combines the file exclusions from all applicable policies for the user. The exclusions are added to a superset and the single list of exclusions is delivered to the users’ device.

When policy merge isn’t supported for a setting, a conflict can occur. Conflicts can result in the user or device not receiving any policy for the setting. For example, policy merge doesn't support the CSP for preventing installation of matching device IDs (*PreventInstallationOfMatchingDeviceIDs*). Configurations for this CSP don’t merge, and are processed separately.

When processed separately, policy conflicts are resolved as follows:

1. The most secure policy applies.
2. If two policies are equally secure, the last modified policy applies.
3. If the last modified policy can’t resolve the conflict, no policy is delivered to the device.

### Settings and CSPs that support policy merge

The following settings support policy merge:

[Microsoft Defender Antivirus policies](../protect/antivirus-microsoft-defender-settings-windows.md)

- **Defender Processes To Exclude** - CSP: [Defender/ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)
- **File extensions to exclude from scans and real-time protection** - CSP: [Defender/ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)
- **Defender Files And Folders To Exclude** - CSP: [Defender/ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

## Antivirus policy reports

Antivirus policy reports display status details about your endpoint security Antivirus policies and device status. These reports are available in the Endpoint security node of the Microsoft Endpoint Manager admin center.

To view the reports, in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to  Endpoint security and select **Antivirus**. Selecting Antivirus opens the Summary page. Additional report and status views are available as additional pages.

In addition to reports detailed in the following sections, additional reports for Microsoft Defender Antivirus are found in the Reports node of the Microsoft Endpoint Manager admin center, as documented in the Intune Reports article:

- [Antivirus agent status report (Organizational)](../fundamentals/reports.md#antivirus-agent-status-report-organizational)
- [Detected malware report (Organizational)](../fundamentals/reports.md#detected-malware-report-organizational)

### Summary

On the **Summary** page, you can [create new policies](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) and view a list of the policies that were previously created. The list includes high-level details about the profile that policy includes (Policy Type), and if the policy is assigned.

![Summary page of antivirus policy](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

When you select a policy from the list, the *Overview* page for that policy instance opens and displays more information. After selecting a tile from this view, Intune displays additional details for that profile if they’re available.

![Overview page of antivirus policy](./media/endpoint-security-antivirus-policy/policy-overview.png)

### Windows 10 unhealthy endpoints

On the **Windows 10 unhealthy endpoints** page, you can view information about the antivirus status of your MDM-managed Windows 10 devices. This information is returned from Windows Defender Antivirus that runs on the device, as *Threat agent status*.

Only devices with detected issues appear in this view. This view doesn't display details for devices that are identified as clean.

![Unhealthy endpoints page of antivirus policy](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## Next steps

[Configure Endpoint security policies](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)