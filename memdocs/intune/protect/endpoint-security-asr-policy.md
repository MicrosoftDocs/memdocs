---
# required metadata

title: Manage attack surface reduction settings with endpoint security policies in Microsoft Intune | Microsoft Docs
description: Configure and deploy policies for devices you manage with endpoint security attack surface reduction policy settings in Microsoft Intune 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/05/2022
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
ms.collection: M365-identity-device-management
ms.reviewer: mattcall

---

# Attack surface reduction policy for endpoint security in Intune

When Defender antivirus is in use on your Windows 10/11 devices, you can use Intune endpoint security policies for Attack surface reduction to manage those settings for your devices.

Attack surface reduction policies help reduce your attack surfaces, by minimizing the places where your organization is vulnerable to cyberthreats and attacks. For more information, see [Overview of attack surface reduction]( /windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) in the Windows Threat protection documentation.

Find the endpoint security policies for attack surface reduction under *Manage* in the **Endpoint security** node of the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Each attack surface reduction *profile* manages settings for a specific area of a Windows 10/11 device.

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
> Beginning on April 5, 2022, the following profiles for Attack surface reduction policy have been updated to use the settings format as found in the Settings Catalog, while the other profiles are unchanged:  
> - Attack surface reduction rules
> - Exploit protection  
>
> The new versions of these two profiles include the same settings as the older profile templates they replace. With this change, all new instances of these profiles will use the new settings format. Your previously crated instances of these profiles remain available to use and edit.


### Devices managed by Intune

**Windows 10/11 profiles**:

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

- **Attack surface reduction rules** – Configure settings for attack surface reduction rules that target behaviors that malware and malicious apps typically use to infect computers, including:
  - Executable files and scripts used in Office apps or web mail that attempt to download or run files
  - Obfuscated or otherwise suspicious scripts
  - Behaviors that apps don't usually start during normal day-to-day work
Reducing your attack surface means offering attackers fewer ways to perform attacks.


  **Merge behavior for Attack surface reduction rules in Intune**:

  Attack surface reduction rules support a merger of settings from different policies, to create a superset of policy for each device. Only the settings that are not in conflict are merged, while those that are in conflict are not added to the superset of rules. Previously, if two policies included conflicts for a single setting, both policies were flagged as being in conflict, and no settings from either profile would be deployed.

  Attack surface reduction rule merge behavior is as follows:
  - Attack surface reduction rules from the following profiles are evaluated for each device the rules apply to:  
    - Devices > Configuration policy > Endpoint protection profile > Microsoft Defender Exploit Guard > **Attack Surface Reduction**
    - Endpoint security > Attack surface reduction policy > **Attack surface reduction rules**
    - Endpoint security > Security baselines > Microsoft Defender for Endpoint Baseline > **Attack Surface Reduction Rules**.
  - Settings that do not have conflicts are added to a superset of policy for the device.
  - When two or more policies have conflicting settings, the conflicting settings are not added to the combined policy, while settings that don’t conflict are added to the superset policy that applies to a device.
  - Only the configurations for conflicting settings are held back.

- **Device control** – With settings for device control, you can configure devices for a layered approach to secure removable media. Microsoft Defender for Endpoint provides multiple monitoring and control features to help prevent threats in unauthorized peripherals from compromising your devices.

  Device control profiles support [policy merge](#policy-merge-for-settings) for USB device IDs.

  To learn more, see [How to control USB devices and other removable media using Microsoft Defender for Endpoint](/windows/security/threat-protection/device-control/control-usb-devices-using-intune) in the Microsoft Defender for Endpoint documentation.

- **Exploit protection** - Exploit protection settings can help protect against malware that uses exploits to infect devices and spread. Exploit protection consists of a number of mitigations that can be applied to either the operating system or individual apps.

### Devices managed by Configuration Manager

[!INCLUDE [Attack surface reduction prerequisites](../includes/tenant-attach-asr-prerequisites.md)]

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

- Policy merge evaluates the lists of *setup classes* that were configured in each instance of *Allow hardware device installation by setup classes* that applies to a device. The into a single allowlist where any duplicate setup classes are removed.

  Removal of duplicates from the list is done to remove the common source of conflicts. The combined allowlist is then delivered to the device.

Policy merge doesn’t compare or merge the configurations from different settings. For example:

- Expanding on the first example, in which multiple lists from *Allow hardware device installation by setup classes* were merged into a single list, you have several instances of *Block hardware device installation by setup classes* that applies to the same device. All the related blocklists merge into a single blocklist for the device that then deploys to the device.

  - The allowlist for *setup classes* isn’t compared nor merged with the blocklist for *setup classes*.  
  - Instead, the device receives both lists, as they are from two distinct settings. The device then enforces the most restrictive setting for *installation by setup classes*.

  With this example, a setup class defined in the blocklist will override the same setup class if found on the allowlist. The result would be that the setup class is blocked on the device.

## Next steps

[Configure Endpoint security policies](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)

View details for the settings in profiles for [Attack surface reduction profiles](../protect/endpoint-security-asr-profile-settings.md).
