---
# required metadata

title: Manage attack surface reduction settings with endpoint security policies in Microsoft Intune | Microsoft Docs
description: Configure and deploy policies for devices you manage with endpoint security attack surface reduction policy settings in Microsoft Intune 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/16/2023
ms.topic: conceptual
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
ms.collection:
- tier1
- M365-identity-device-management
- highpri
ms.reviewer: mattcall

---

# Attack surface reduction policy for endpoint security in Intune

When Defender antivirus is in use on your Windows 10/11 devices, you can use Intune endpoint security policies for Attack surface reduction to manage those settings for your devices.

Attack surface reduction policies help reduce your attack surfaces, by minimizing the places where your organization is vulnerable to cyberthreats and attacks. For more information, see [Overview of attack surface reduction]( /windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) in the Windows Threat protection documentation.

Find the endpoint security policies for attack surface reduction under *Manage* in the **Endpoint security** node of the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Each attack surface reduction *profile* manages settings for a specific area of a Windows 10/11 device.

## Prerequisites for Attack surface reduction profiles

**General**:

- Windows 10 or Windows 11
- Defender antivirus must be the primary antivirus on the device

**Support for Configuration Manager clients**:

*This scenario is in preview and requires use of Configuration Manager current branch version 2006 or later*.

- **Set up tenant attach for Configuration Manager devices** - To support deploying attack surface reduction policy to devices managed by Configuration Manager, configure tenant attach. Set up of tenant attach includes configuring Configuration Manager device collections to support endpoint security policies from Intune.

  To set up tenant attach, see [Configure tenant attach to support endpoint protection policies](../protect/tenant-attach-intune.md).

## Attack surface reduction profiles

> [!NOTE]  
> Beginning in April 2022, new profiles for Attack surface reduction policy have begun to release. When a new profile becomes available, it uses the same name of the profile it replaces and includes the same settings as the older profile but in the newer settings format as seen in the Settings Catalog. Your previously created instances of these profiles remain available to use and edit, but all new instances you create will be in the new format. The following profiles have been updated:
>
> - Attack surface reduction rules (April 5, 2022)
> - Exploit protection (April 5, 2022)
> - Device control (May 23, 2022)
 

### Devices managed by Intune

**Platform: Windows 10 and later**: Profiles for this platform are supported on Windows 10 and Windows 11 devices enrolled with Intune. Profiles include:

- **App and browser isolation** – Manage settings for Windows Defender Application Guard (Application Guard), as part of Defender for Endpoint. Application Guard helps to prevent old and newly emerging attacks and can isolate enterprise-defined sites as untrusted while defining what sites, cloud resources, and internal networks are trusted.

  To learn more, see [Application Guard](/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) in the Microsoft Defender for Endpoint documentation.

- **Web protection (Microsoft Edge Legacy)** – Settings you can manage for Web protection in Microsoft Defender for Endpoint configure network protection to secure your machines against web threats. By integrating with Microsoft Edge and popular third-party browsers like Chrome and Firefox, web protection stops web threats without a web proxy and can protect machines while they're away or on-premises. Web protection stops access to:
  - Phishing sites
  - Malware vectors
  - Exploit sites
  - Untrusted or low-reputation sites
  - Sites that you've blocked in your custom indicator list.

  To learn more, see [Web protection](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) in the Microsoft Defender for Endpoint documentation.

- **Application control** - Application control settings can help mitigate security threats by restricting the applications that users can run and the code that runs in the System Core (kernel). Manage settings that can block unsigned scripts and MSIs, and restrict Windows PowerShell to run in Constrained Language Mode.

  To learn more, see [Application Control](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) in the Microsoft Defender for Endpoint documentation.
  
    > [!NOTE]
    > If you use this setting, AppLocker CSP behavior currently prompts end user to reboot their machine when a policy is deployed.

- **Attack Surface Reduction Rules** – Configure settings for attack surface reduction rules that target behaviors that malware and malicious apps typically use to infect computers, including:
  - Executable files and scripts used in Office apps or web mail that attempt to download or run files
  - Obfuscated or otherwise suspicious scripts
  - Behaviors that apps don't usually start during normal day-to-day work
Reducing your attack surface means offering attackers fewer ways to perform attacks.

  **Merge behavior for Attack surface reduction rules in Intune**:

  Attack surface reduction rules support a merger of settings from different policies, to create a superset of policy for each device. Settings that aren't in conflict are merged, while settings that are in conflict aren't added to the superset of rules. Previously, if two policies included conflicts for a single setting, both policies were flagged as being in conflict, and no settings from either profile would be deployed.

  Attack surface reduction rule merge behavior is as follows:
  - Attack surface reduction rules from the following profiles are evaluated for each device the rules apply to:  
    - Devices > Configuration policy > Endpoint protection profile > Microsoft Defender Exploit Guard > **Attack Surface Reduction**
    - Endpoint security > Attack surface reduction policy > **Attack surface reduction rules**
    - Endpoint security > Security baselines > Microsoft Defender for Endpoint Baseline > **Attack Surface Reduction Rules**.
  - Settings that don't have conflicts are added to a superset of policy for the device.
  - When two or more policies have conflicting settings, the conflicting settings aren't added to the combined policy, while settings that don’t conflict are added to the superset policy that applies to a device.
  - Only the configurations for conflicting settings are held back.

- **Device Control** – With settings for device control, you can configure devices for a layered approach to secure removable media. Microsoft Defender for Endpoint provides multiple monitoring and control features to help prevent threats in unauthorized peripherals from compromising your devices.

  Device control profiles support [policy merge](#policy-merge-for-settings) for USB device IDs.

  To learn more, see [How to control USB devices and other removable media using Microsoft Defender for Endpoint](/windows/security/threat-protection/device-control/control-usb-devices-using-intune) in the Microsoft Defender for Endpoint documentation.

- **Exploit Protection** - Exploit protection settings can help protect against malware that uses exploits to infect devices and spread. Exploit protection consists of many mitigations that can apply to either the operating system or individual apps.

#### Add reusable settings groups to profiles for Device control

In public preview, Device control profiles support use of [reusable settings groups](../protect/reusable-settings-groups.md) to help manage settings for the following settings groups on devices for the *Windows 10 and later* platform:

- Printer device
- Removable storage

The following device control profile settings are available for *printer device*:

- PrimaryId
- PrinterConnectionID
- VID_PID

The following device control profile settings are available in for *removable storage*:

- Device class
- Device ID
- Hardware ID
- Instance ID
- Primary ID
- Product ID
- Serial number
- Vendor ID
- Vendor ID and Product ID

For information about these options, see the following articles in the Microsoft Defender for Endpoint documentation:

- [Printer Protection Overview](/microsoft-365/security/defender-endpoint/printer-protection-overview)
- [Microsoft Defender for Endpoint Device Control Removable Storage Access Control](/microsoft-365/security/defender-endpoint/device-control-removable-storage-access-control)

When you configure a Device control profile and one or more reusable settings groups, you also configure *Actions* to define how the settings in those groups are used.

Each rule you add to the profile can include both reusable settings groups and individual settings that are added directly to the rule.  However, consider using each rule for either reusable settings groups or to manage settings you add directly to the rule. This separation can help simplify future configurations or changes you might make.  

For guidance on configuring reusable groups, and then adding them to this profile, see [Use reusable groups of settings with Intune policies](../protect/reusable-settings-groups.md).

#### Exclusions for Attack Surface Reduction Rules

Intune supports the following two settings to exclude specific file and folder paths from evaluation by Attack Surface Reduction rules:

- **Global**: Use **Attack Surface Reduction Only Exclusions**.

  :::image type="content" source="./media/endpoint-security-asr-policy/global-asr-rule-exclusion.png" alt-text="Screen capture of the Attack Surface Reduction Only Exclusions setting.":::

  When a device is assigned at least one policy that configures **Attack Surface Reduction Only Exclusions**, the configured exclusions apply to all attack surface reduction rules that target that device. This occurs because devices receive a superset of attack surface reduction rule settings from all applicable policies, and the settings exclusions can't be managed for individual settings. To avoid having exclusions applied to all settings on a device, don't use this setting and instead configure **ASR Only Per Rule Exclusions** for individual settings.

  For more information, see the documentation for the Defender CSP: [Defender/AttackSurfaceReductionOnlyExclusions](/windows/client-management/mdm/policy-csp-Defender#defender-attacksurfacereductiononlyexclusions).

- **Individual settings**: Use **ASR Only Per Rule Exclusions**

  :::image type="content" source="./media/endpoint-security-asr-policy/individual-rule-exclusion.png" alt-text="Screen capture of the ASR Only \Per Rule Exclusions setting.":::

  When you set an applicable setting in an attack surface reduction rule profile to anything other than *Not configured*, Intune presents the option to use **ASR Only Per Rule Exclusions** for that individual setting. With this option, you can configure a file and folder exclusion that are isolated to individual settings, which is in contrast to use of the global setting **Attack Surface Reduction Only Exclusions** which applies its exclusions to all settings on the device.

  By default, **ASR Only Per Rule Exclusions** is set to **Not configured**.
  
  > [!IMPORTANT]
  > ASR polices do not support merge functionality for *ASR Only Per Rule Exclusions* and a policy conflict can result when multiple polices that configure *ASR Only Per Rule Exclusions* for the same device conflict. To avoid conflicts, combine the configurations for *ASR Only Per Rule Exclusions* into a single ASR policy. We are investigating adding policy merge for *ASR Only Per Rule Exclusions* in a future update.

  <!-- 
  For more information, see the documentation for the Defender CSP  [Defender/ASROnlyPerRuleExclusions](/windows/client-management/mdm/policy-csp-Defender#defender-asronlyperruleexclusions). 
  -->

<!--
**When both settings are configured and apply to a device**:
Behavior details pending. 
-->

### Devices managed by Configuration Manager

[!INCLUDE [Attack surface reduction prerequisites](../includes/tenant-attach-asr-prerequisites.md)]

### Devices managed by Security Management for Defender for Endpoint

Profiles for this platform can be used with Windows 10 and Windows 11 devices enrolled with Intune, and with devices managed through [Security Management for Microsoft Defender for Endpoint](../protect/mde-security-integration.md).  
Profiles include:  

- **Attack Surface Reduction Rules** - Configure settings for attack surface reduction rules that target behaviors that malware and malicious apps typically use to infect computers, including:
  - Executable files and scripts used in Office apps or web mail that attempt to download or run files.
  - Obfuscated or otherwise suspicious scripts.
  - Behaviors that apps don't usually start during normal day-to-day work Reducing your attack surface means offering attackers fewer ways to perform attacks.

## Policy merge for settings

Policy merge helps avoid conflicts when multiple profiles that apply to the same device configure the same setting with different values, creating a conflict. To avoid conflicts, Intune evaluates the applicable settings from each profile that applies to the device. Those settings then merge into a single superset of settings.

For Attack surface reduction policy, the following profiles support policy merge:

- Device control

### Policy merge for device control profiles

Device control profiles support policy merge for USB Device IDs. The profile settings that manage Device IDs and that support policy merge include:

- Allow hardware device installation by device identifiers
- Block hardware device installation by device identifiers
- Allow hardware device installation by setup classes
- Block hardware device installation by setup classes
- Allow hardware device installation by device instance identifiers
- Block hardware device installation by device instance identifiers

Policy merge applies to the configuration of each setting across the different profiles that apply that specific setting to a device. The result is a single list for each of the supported settings being applied to a device. For example:

- Policy merge evaluates the lists of *setup classes* that were configured in each instance of *Allow hardware device installation by setup classes* that applies to a device. The lists are merged into a single allowlist where any duplicate setup classes are removed.

  Removal of duplicates from the list is done to remove the common source of conflicts. The combined allowlist is then delivered to the device.

Policy merge doesn’t compare or merge the configurations from different settings. For example:

- Expanding on the first example, in which multiple lists from *Allow hardware device installation by setup classes* were merged into a single list, you have several instances of *Block hardware device installation by setup classes* that applies to the same device. All the related blocklists merge into a single blocklist for the device that then deploys to the device.

  - The allowlist for *setup classes* isn’t compared nor merged with the blocklist for *setup classes*.  
  - Instead, the device receives both lists, as they are from two distinct settings. The device then enforces the most restrictive setting for *installation by setup classes*.

  With this example, a setup class defined in the blocklist will override the same setup class if found on the allowlist. The result would be that the setup class is blocked on the device.

## Next steps

[Configure Endpoint security policies](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)

View details for the settings in profiles for [Attack surface reduction profiles](../protect/endpoint-security-asr-profile-settings.md).
