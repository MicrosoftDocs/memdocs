---
title: Manage antivirus settings with endpoint security policies in Microsoft Intune
description: Configure and deploy policies and use reports for devices you manage with endpoint security antivirus policy in Microsoft Intune.
ms.date: 05/13/2026
ms.topic: reference
ai-usage: ai-assisted
ms.collection:
- M365-identity-device-management
- sub-secure-endpoints
ms.reviewer: mattcall

---

# Antivirus policy for endpoint security in Microsoft Intune

Intune Endpoint security Antivirus policies help security admins focus on managing the discrete group of antivirus settings for managed devices.

Antivirus policy includes several profiles. Each profile contains only the settings that are relevant for Microsoft Defender for Endpoint antivirus for macOS and Windows devices, or for the user experience in the Windows Security app on Windows devices.

Find the antivirus policies under **Manage** in the Endpoint security node of the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

Antivirus policies include the same settings as found *endpoint protection* or *device restriction* templates for [device configuration](../create-device-profile.md) policy. However, those policy types include other categories of settings that are unrelated to Antivirus. The additional settings can complicate the task of configuring Antivirus workload. Also, the settings found in the Antivirus policy for macOS aren't available through the other policy types. The macOS Antivirus profile replaces the need to configure the settings by using `.plist` files.

Applies to:

- Linux
- macOS
- Windows
- Windows Server *(through the [Microsoft Defender for Endpoint Security settings management](../../device-security/microsoft-defender/security-settings-management.md) scenario)*

> [!IMPORTANT]
> [!INCLUDE [windows-10-support](../../includes/windows-10-support.md)]


## Prerequisites for antivirus policy

**Support for Intune (MDM) enrolled devices**:

- **macOS**
  - Any supported version of macOS
  - For Intune to manage antivirus settings on a device, Defender for Endpoint must be installed on that device. See [Microsoft Defender for Endpoint for macOS](/defender-endpoint/microsoft-defender-endpoint-mac) (In the Defender for Endpoint documentation).

- **Windows**
  - No additional prerequisites are required.

**Support for Microsoft Configuration Manager clients**:

*This scenario is in preview and requires use of Configuration Manager current branch version 2006 or later*.

- **Set up tenant attach for Configuration Manager devices** - To support deploying antivirus policy to devices managed by Configuration Manager, configure *tenant attach*. Set up of tenant attach includes configuring Configuration Manager device collections to support endpoint security policies from Intune.

  To set up tenant attach, see [Configure tenant attach to support endpoint protection policies](../../fundamentals/tenant-attach.md).

**Support for Defender for Endpoint clients:**

- **Defender for Endpoint security settings management** - To configure support for deploying antivirus policy to devices that are managed by Defender for Endpoint, but not enrolled with Intune, see [Manage Microsoft Defender for Endpoint on devices with Microsoft Intune](../../device-security/microsoft-defender/security-settings-management.md). This article also includes the information about platforms supported by this capability, and the policies and profiles that those platforms support.

### Role-based access controls (RBAC)

For guidance on assigning the right level of permissions and rights to manage Intune antivirus policy, see [Role-based access control for endpoint security](./manage-policies.md#role-based-access-control-for-endpoint-security).

### Prerequisites for tamper protection

Intune supports managing tamper protection on devices that run one of the following operating systems:

- macOS (any supported version)
- Windows 10 and 11 (including Enterprise multi-session)
- Windows Server 2016 and later
- Windows Server, version 1803 or later
- Windows Server 2012 R2 ([using the modern, unified solution](/defender-endpoint/onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2))

Defender for Endpoint supports tamper protection on additional platforms beyond those manageable through Intune policy. For the full list, see [Tamper protection prerequisites](/defender-endpoint/prevent-changes-to-security-settings-with-tamper-protection#supported-operating-systems).

> [!NOTE]
> Devices are required to be onboarded to Microsoft Defender for Endpoint (P1 or P2). Devices might see a delay enabling tamper protection if previously not onboarded to Microsoft Defender for Endpoint. Tamper protection will enable on the first device check-in after onboarding to Microsoft Defender for Endpoint.

For more information about tamper protection behavior, including which settings are protected and troubleshooting options, see [What is tamper protection?](/defender-endpoint/prevent-changes-to-security-settings-with-tamper-protection) in the Defender for Endpoint documentation.

You can use Intune to manage tamper protection on Windows devices as part of Windows Security Experience profile (an Antivirus policy). This includes both devices you manage with Intune, and devices you manage with Configuration Manager through the tenant attach scenario. Tamper protection is also now available for Azure Virtual Desktop.

#### Intune managed devices

Prerequisites to support tamper protection for devices managed by Intune:

- Your environment must meet the [requirements for managing tamper protection in Intune](/defender-endpoint/manage-tamper-protection-intune#requirements-for-managing-tamper-protection-in-intune)
- Devices are onboarded to Microsoft Defender for Endpoint (P1 or P2)

Profiles for *Antivirus* policy that support tamper protection for [devices managed by Microsoft Intune](./deploy-edr.md#supported-platforms-and-profiles):

- Platform: **Windows**
  - Profile: **Windows Security experience**

  > [!NOTE]
  > On April 5, 2022, the *Windows 10 and later* platform was replaced by the *Windows* platform.
  >
  > The *Windows* platform supports devices communicating with Intune through Microsoft Intune or Microsoft Defender for Endpoint. These profiles also add support for the Windows Server platform which isn't supported through Microsoft Intune natively.
  >
  > Profiles for this new platform use the settings format as found in the Settings Catalog. Each new profile template for this new platform includes the same settings as the older profile template it replaces. With this change you can no longer create new versions of the old profiles. Your existing instances of the old profile remain available to use and edit.

You can also use the [Endpoint protection](./configure-endpoint-protection.md) profile for *Device configuration* policy to configure tamper protection for devices managed by Intune.

#### Configuration Manager clients managed through the tenant attach scenario

Prerequisites to support managing tamper protection with these profiles:

- Your environment must meet the [requirements for managing tamper protection in Intune](/defender-endpoint/manage-tamper-protection-intune#requirements-for-managing-tamper-protection-in-intune) as detailed in the Defender for Endpoint documentation.
- You must use Configuration Manager current branch 2006 or later.
- You must configure tenant attach to support endpoint protection policies. This includes configuring Configuration Manager device collections for synchronization with Intune.
- Devices are onboarded to Microsoft Defender for Endpoint (P1 or P2)

 Profiles for *Antivirus* policy that support tamper protection for [devices managed by Configuration Manager](#devices-managed-by-configuration-manager):

- Platform: **Windows (ConfigMgr)**
  - Profile: **Windows Security experience (preview)**

## Antivirus profiles

Find guidance for creating endpoint security profiles at [Create an endpoint security policy](./manage-policies.md).

### Devices managed by Microsoft Intune

The following profiles are supported for devices you manage with Intune:

#### Linux

- Platform: **Linux**

  - Profile: **Microsoft Defender Antivirus** - Manage Antivirus settings on Linux devices.
  - Profile: **Microsoft Defender Antivirus Exclusions** - Manage settings for Microsoft Defender Antivirus that define Antivirus exclusions for paths, extensions, and processes.

  Antivirus exclusions are also managed by Microsoft Defender Antivirus policy, which includes identical settings for exclusions, and from other policies like Intune's Endpoint detection and response profile for [Microsoft Defender Global Exclusions (AV+EDR)](./deploy-edr.md#create-a-linux-global-exclusions-policy) for Linux, which includes both EDR and Antivirus exclusions. Settings from multiple sources are subject to policy merge, and create a super set of exclusions for applicable devices and users.

  > [!IMPORTANT]
  > The *Microsoft Defender Global Exclusions (AV+EDR)* profile is supported only for Linux devices managed by Defender through the [Microsoft Defender for Endpoint security settings management](../../device-security/microsoft-defender/security-settings-management.md) scenario.

  For more information about Linux exclusions, see [Configure and validate exclusions for Microsoft Defender for Endpoint on Linux](/defender-endpoint/linux-exclusions) in the Microsoft Defender documentation.

#### macOS

- Platform: **macOS**

  - Profile: **Antivirus** - Manage [Antivirus policy settings](./ref-antivirus-defender-settings-macos.md) for macOS.

    When you use [Microsoft Defender for Endpoint for Mac](/defender-endpoint/microsoft-defender-endpoint-mac), you can configure and deploy Antivirus settings to your managed macOS devices through Intune instead of configuring those settings by use of `.plist` files.

#### Windows

- Platform: **Windows**  
  Profiles for this platform can be used with devices enrolled with Intune, and devices managed through [Security Management for Microsoft Defender for Endpoint](../../device-security/microsoft-defender/security-settings-management.md).

  > [!NOTE]
  > On April 5, 2022, the *Windows 10 and later* platform was replaced by the *Windows* platform.
  >
  > The *Windows* platform supports devices communicating with Intune through Microsoft Intune or Microsoft Defender for Endpoint. These profiles also add support for the Windows Server platform which isn't supported through Microsoft Intune natively.
  >
  > Profiles for this new platform use the settings format as found in the Settings Catalog. Each new profile template for this new platform includes the same settings as the older profile template it replaces. With this change you can no longer create new versions of the old profiles. Your existing instances of the old profile remain available to use and edit.

  - Profile: **Microsoft Defender Antivirus** - [Manage Antivirus policy settings for Windows devices](/defender-endpoint/use-intune-config-manager-microsoft-defender-antivirus).

    Defender Antivirus is the next-generation protection component of Microsoft Defender for Endpoint. Next-generation protection brings together technologies like machine learning and cloud infrastructure to protect devices in your enterprise organization.

    The *Microsoft Defender Antivirus* profile is a separate instance of the antivirus settings that are found in the *Device Restriction profile* for Device Configuration policy.

    Unlike the antivirus settings in a *Device Restriction profile*, you can use these settings with devices that are co-managed. To use these settings, the [co-management workload slider](/configmgr/comanage/how-to-switch-workloads) for Endpoint Protection must be set to Intune.

  - Profile: **Microsoft Defender Antivirus exclusions** - [Manage policy settings for only Antivirus exclusion](/defender-endpoint/configure-exclusions-microsoft-defender-antivirus#create-a-new-antivirus-policy-with-exclusions-in-intune).

    With this policy, you can manage settings for the following Microsoft Defender Antivirus configuration service providers (CSPs) that define Antivirus exclusions:

    - Defender/ExcludedPaths
    - Defender/ExcludedExtensions
    - Defender/ExcludedProcesses

    These CSPs for antivirus exclusion are also managed by *Microsoft Defender Antivirus* policy, which includes identical settings for exclusions. Settings from both policy types  (*Antivirus* and *Antivirus exclusions*) are subject to [policy merge](#policy-merge-for-settings), and create a super set of exclusions for applicable devices and users.

    > [!WARNING]
    > **Defining exclusions lowers the protection offered by Microsoft Defender Antivirus**. Always evaluate the risks that are associated with implementing exclusions. Only exclude files you know aren't malicious.
    >
    > For more information, see [Exclusions overview](/defender-endpoint/navigate-defender-endpoint-antivirus-exclusions) in the Microsoft Defender documentation.

  - Profile: **Windows Security experience** - Manage the Windows Security app settings that end users can view in the Microsoft Defender Security center and the notifications they receive.

    The Windows security app is used by many Windows security features to provide notifications about the health and security of the machine. Security app notifications include firewalls, antivirus products, Windows Defender SmartScreen, and others.

  - Profile: **Defender Update controls** - Manage update settings for Microsoft Defender, including the following settings that are taken directly from the [Defender CSP](/windows/client-management/mdm/defender-csp):

    - [Engine Updates Channel](/windows/client-management/mdm/defender-csp?WT.mc_id=Portal-fx#configurationengineupdateschannel)
    - [Platform Updates Channel](/windows/client-management/mdm/defender-csp?WT.mc_id=Portal-fx#configurationplatformupdateschannel)
    - [Security Intelligence Updates Channel](/windows/client-management/mdm/defender-csp?WT.mc_id=Portal-fx#configurationsecurityintelligenceupdateschannel)

### Devices managed by Configuration Manager

[!INCLUDE [antivirus policy prerequisites](../../includes/tenant-attach-antivirus-prerequisites.md)]

## Policy merge for settings

Some Antivirus policy settings support *policy merge*. Policy merge helps avoid conflicts when multiple policies apply to the same devices and configure the same setting. Intune evaluates the settings that policy merge supports, for each user or device as taken from all applicable policies. Those settings are then merged into a single superset of policy.

For example, you create three separate antivirus policies that define different antivirus file path exclusions. Eventually, all three policies are assigned to the same user. Because the Microsoft Defender file path exclusion CSP supports policy merge, Intune evaluates and combines the file exclusions from all applicable policies for the user. The exclusions are added to a superset and the single list of exclusions is delivered to the users' device.

When policy merge isn't supported for a setting, a conflict can occur. Conflicts can result in the user or device not receiving any policy for the setting. For example, policy merge doesn't support the CSP for preventing installation of matching device IDs (*PreventInstallationOfMatchingDeviceIDs*). Configurations for this CSP don't merge, and are processed separately.

When processed separately, policy conflicts are resolved as follows:

1. The most secure policy applies.
2. If two policies are equally secure, the last modified policy applies.
3. If the last modified policy can't resolve the conflict, no policy is delivered to the device.

### Settings and CSPs that support policy merge

The following settings support policy merge:

- **Excluded Processes** - CSP: [Defender/ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)
- **Excluded Extensions** - CSP: [Defender/ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)
- **Excluded Paths** - CSP: [Defender/ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

## Antivirus policy reports

Antivirus policy reports display status details about your endpoint security Antivirus policies and device status. These reports are available in the Endpoint security node of the Microsoft Intune admin center.

To view the reports, in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to  Endpoint security and select **Antivirus**. Selecting Antivirus opens the Summary page. Additional report and status views are available as additional pages.

In addition to reports detailed in the following sections, additional reports for Microsoft Defender Antivirus are found in the Reports node of the Microsoft Intune admin center, as documented in the Intune Reports article:

- [Antivirus agent status report (Organizational)](../../device-management/reports/overview.md#antivirus-agent-status-report-organizational)
- [Detected malware report (Organizational)](../../device-management/reports/overview.md#detected-malware-report-organizational)

### Summary

On the **Summary** page, you can [create new policies](./manage-policies.md#create-endpoint-security-policies) and view a list of the policies that were previously created. The list includes high-level details about the profile that policy includes (Policy Type), and if the policy is assigned.

![Summary page of antivirus policy](./media/antivirus/antivirus-summary.png)

When you select a policy from the list, the *Overview* page for that policy instance opens and displays more information. After selecting a tile from this view, Intune displays additional details for that profile if they're available.

![Overview page of antivirus policy](./media/antivirus/policy-overview.png)

### Unhealthy endpoints

On the **Unhealthy endpoints** page, you can view information about the antivirus status of your MDM-managed Windows devices. This information is returned from Windows Defender Antivirus that runs on the device, as *Threat agent status*. On this page, select **Columns** to view the full list of details that are available in the report.

Only devices with detected issues appear in this view. This view doesn't display details for devices that are identified as clean.

The information for this report is based on details available from the following CSPs, which are documented in the Windows client-management documentation:

- [Defender CSP](/windows/client-management/mdm/defender-csp)
- [WindowsAdvancedThreatProtection CSP](/windows/client-management/mdm/windowsadvancedthreatprotection-csp).

:::image type="content" source="./media/antivirus/antivirus-unhealthy-endpoints.png" alt-text="Screenshot of the Unhealthy endpoints report.":::

## Next steps

[Configure Endpoint security policies](./manage-policies.md#create-endpoint-security-policies)

View details for the Windows settings in the deprecated profiles for the deprecated *Windows 10 and later* platform:

- [Antivirus policy settings](./ref-antivirus-defender-settings-windows.md)
- [Antivirus exclusions](./ref-antivirus-defender-settings-windows.md#microsoft-defender-antivirus-exclusions)
- [Windows Security app settings](./ref-security-experience-settings-windows.md)
