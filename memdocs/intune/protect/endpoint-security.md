---
# required metadata

title: Manage endpoint security in Microft Intune | Microsoft Docs
description: Learn how Security Administrators can use the Endpoint Security node to manage device security and remediate issues for devices in Microsoft Endpoint Manager. 
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

# Manage endpoint security in Microsoft Intune

As a Security Admin, use the *Endpoint security* node in Intune to configure device security and to manage security tasks for devices when those devices are at risk. The Endpoint security policies are designed to help you focus on the security of your devices and mitigate risk. The tasks that are available help you identify devices that are at risk, to remediate those devices, and restore them to a compliant or more secure state.

The Endpoint security node groups the tools that are available through Intune that you’ll use to keep devices secure:

- **Review the status of all your managed devices**. Use the [All devices](#view-all-devices-and-manage-device-actions) view where you can view device compliance from a high level and then drill into specific devices to understand which compliance policies weren't met so you can act to resolve them.

- **Deploy security baselines that establish best practice security configurations for devices**. Intune includes [security baselines](#manage-security-baselines) for Windows devices and a growing list of applications, like Defender ATP and Microsoft Edge.

- **Manage security configurations on devices through tightly focused policies**.  Each [Endpoint security policy](#use-policies-to-manage-device-security) focuses on specific aspects of device security like antivirus, disk encryption, firewalls, and several areas made available through integration with Defender ATP.

- **Establish device and user requirements through compliance policy**. With [compliance policies](../protect/device-compliance-get-started.md), you set the rules that devices and users must meet to be considered compliant. Rules can include OS versions, password requirements, device threat-levels, and more. When you integrate with Azure AD [conditional access policies](#configure-conditional-access) to enforce compliance policies, you can gate access to corporate resources for both managed devices, and devices that aren’t managed yet.

- **Integrate Intune with your Microsoft Defender Advanced Threat Protection (Defender ATP) team**. By [integrating with Defender ATP](#set-up-integration-with-defender-atp) you gain access to [security tasks](#review-security-tasks-from-defender-atp) that closely tie Defender ATP and Intune together to help identify and remediate devices that are at risk.

## View All devices and manage device actions

When you open the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Endpoint security** > **All devices**, you’ll see a list of all the devices from your Azure Active Directory (Azure AD) that are available in Microsoft Endpoint Manager. This list includes devices managed by Intune, Configuration Manager, and by [co-management](https://docs.microsoft.com/configmgr/comanage/overview) by both Intune and Configuration Manager. Devices can be in the cloud and from your on-premises infrastructure when integrated with your Azure AD.

The initial *All devices* view displays your devices and includes key information about each:

- How the device is managed
- Compliance status
- Operating system details
- When the device last checked in
- And more

When viewing devices in the Microsoft Endpoint Manager admin center, consider how the device is managed. The management source affects the information that’s presented in the admin center and which actions are available to manage the device from the admin center.

Consider the following fields:

- **Managed by** – This column identifies how the device is managed. Managed by options include:

  - **MDM**  - These devices are managed by Intune. Compliance data is collected and reported by Intune to the admin center.

  - **ConfigMgr** – These devices appear when you use *tenant attach* to add your devices that are managed by Configuration Manager to the Microsoft Endpoint Manager admin center. Devices that are added from Configuration Manager include the devices that are identified by Configuration Manager as **Client** = **Yes** and include:

    - Workgroup (AAD joined and otherwise)
    - Domain Joined
    - Hybrid AAD Joined (joined to the AD and AAD)

    Compliance status is managed in Configuration Manager and might not be visible in the Microsoft Endpoint Manager admin center.  Similarly, these devices won’t receive policy deployed by Intune.

    For more information, see [Enable tenant attach](https://docs.microsoft.com/configmgr/tenant-attach/device-sync-actions) in the Configuration Manager documentation.

  - **MDM/ConfigMgr Agent** – These devices are under co-management between Intune and Configuration Manager.

    With co-management, you [choose different co-management workloads](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) to determine which aspects are managed by Configuration Manager or by Intune. These choices will affect which policies the device applies, and how compliance data is reported to the admin center.

    For example, you can use Intune to configure policy for Antivirus, Firewall, and Encryption. These policy types are considered policy for *Endpoint Protection*. To have a co-managed device use the Intune policies and not the Configuration Manager policies, the co-management slider for Endpoint Protection must be set to either *Intune* or *Pilot Intune*. If the slider is set to Configuration Manager, the device uses the policies and settings from Configuration Manager instead.

  - **Compliance**: Compliance is evaluated against the compliance policies that are assigned to the device. The source of these policies and what information is in the console depends on how the device is managed; Intune, Configuration Manager, or co-management.

    After compliance is reported to the admin center for a device, you can drill into the details to view additional details. When a device isn’t compliant, drill into its details to information about which policies aren't compliant.  That information can help you investigate and help you bring the device into compliance.

  - **Last check-in**: If a device hasn’t checked in for some time, its details, including its Compliance status, can be out of date.

### Remote actions for devices

When you view details for a device, you can access remote actions that apply to the device.

Remote actions display across the top of the devices *Overview* page. Actions that can’t display because of limited space on your screen are available by selecting the ellipsis on the right side:

![View additional actions](./media/endpoint-security/view-additional-actions.png)

The remote actions that are available depend on how the device is managed:

- **Intune**: All [Intune remote actions](../remote-actions/device-management.md) that apply to the device platform are available.  
- **Configuration Manager**: You can use the following Configuration Manager actions:

  - Sync Machine Policy
  - Sync User Policy
  - App Evaluation Cycle

- **Co-management**: You can access both Intune remote actions and Configuration Manager actions.

Remote actions are actions you can start from the Microsoft Endpoint Manager admin center, which take effect the next time that device checks in with either Intune or Configuration Manager, depending on the action you use.

Some of the Intune remote actions can help secure devices or safeguard data that might be on the device. With remote actions you can lock a device, reset a device, remove company data, scan for malware outside of a scheduled run, and rotate BitLocker keys.

The following Intune remote actions are of interest to the security admin, and are a subset of the [full list](../remote-actions/device-inventory.md#view-the-device-details). Not all actions are available for all device platforms. The links go to content that provides in-depth details for each action.

- [Retire](../remote-actions/devices-wipe.md#retire) - Remove managed app data (where applicable), settings, and email profiles that were assigned by using Intune. The device is removed from Intune management.

- [Wipe](../remote-actions/devices-wipe.md#wipe) – Restores a device to its factory default settings. The user data is kept if you choose the **Retain enrollment state and user account** checkbox. Otherwise, all data, apps, and settings will be removed.

- [Delete](../remote-actions/devices-wipe.md#delete-devices-from-the-intune-portal) – Remove the device from the Intune portal. The next time the device checks in, any company data on the device is removed. You can also set up a clean-up rule that can delete a device when it hasn’t checked in from between 30 and 270 days.

- [Remote lock](../remote-actions/device-remote-lock.md) – Remotely lock a device. To unlock the device, the device owner enters their passcode.

- [Reset passcode](../remote-actions/device-passcode-reset.md) - Reset the passcode for an entire device, or for a device users work profile, depending on the Android platform in use.

- Update Windows Defender security intelligence – Have the device update its malware definitions for Microsoft Defender. This action doesn’t start a scan.

- [Full scan](../configuration/device-restrictions-windows-10.md) – Have Defender run a scan of the device for malware and then submit the results to Intune. In addition to Full, there is an option for a quick scan.

- [BitLocker key rotation](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key) – Remotely rotate the BitLocker recovery key of a device that runs Windows 10 version 1909 or later.

You can also use **Bulk Device Actions** to manage some actions like *Retire* and *Wipe* for multiple devices at the same time. [Bulk actions](../remote-actions/bulk-device-actions.md) are available from the *All devices* view. You’ll select the platform, action, and then specify up to 100 devices.

![Select bulk actions](./media/endpoint-security/select-bulk-actions.png)

Options you manage for devices don’t take effect until the device checks in with Intune.

## Manage Security baselines

Use Intune's security baselines to rapidly deploy a *best practice* configuration of device and application settings to protect your users and devices. Security baselines are supported for devices that run Windows 10 version 1809 and later.

The baselines are pre-configured groups of settings that are best practice recommendations from the relevant Microsoft security teams for the applicable product. Intune supports security baselines for Windows 10 device settings, Microsoft Edge, Microsoft Defender Advanced Threat Protection, and more.

When you deploy a security baseline, you can deploy the baseline in its default (recommended) configuration, or customize it to meet the needs of your unique environment.

For more information, see [Use security baselines to configure Windows 10 devices in Intune](../protect/security-baselines.md).

## Review Security tasks from Defender ATP

When you integrate Intune with Microsoft Defender Advanced Threat Protection (Defender ATP), you can review *Security tasks* in Intune that identify at-risk devices and provide steps to mitigate that risk. You can then use the tasks to report back to Defender ATP when those risks are successfully mitigated.

- Your Defender ATP team determine what devices are at risk and pass that information to your Intune team as a security task. With one click they create a security task for Intune that identifies the devices at risk, the vulnerability, and that provides guidance on how to mitigate that risk.

- The Intune Admins review security tasks and then act within Intune to remediate those tasks. Once mitigated, they set the task to complete, which communicates that status back to the Defender ATP team.

Through Security tasks both teams remain in synch as to which devices are at risk, and how and when those risks are remediated.

To learn more about using Security tasks, see [Use Intune to remediate vulnerabilities identified by Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md).

## Use policies to manage device security

As a security admin, use the policies found under *Manage* in the Endpoint security node to configure device security without the overhead of navigating the larger body and range of settings found in device configuration profiles and security baselines.  

![Manage policies](./media/endpoint-security/endpoint-security-policies.png)

Unless noted otherwise, the settings found in Endpoint security policies can also be managed through endpoint protection profiles in Device Configuration policy, and by security baselines. Therefore, it's important to understand how to identify and resolve policy conflicts should a device not adhere to the configurations you expect.

The information at the following links can help you identify and resolve conflicts:

- [Troubleshoot policies and profiles in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Monitor your security baselines](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

The following sections introduce the policy groups and the profiles available for each group.

### Antivirus

Use Antivirus profiles to manage Defender ATP antivirus settings on devices that run Windows 10 or macOS.

#### Prerequisites

- Windows 10 or later
- Any supported version of macOS
- For Intune to manage antivirus settings on a device, Defender ATP must be installed on that device.
- The Windows Security app is installed on all devices that run Window 10, and no additional prerequisites are required.

#### macOS profiles

- **Antivirus** - Manage Antivirus policy settings for macOS when you use Microsoft Defender ATP for Mac.

### Windows 10 profiles

- **Microsoft Defender Antivirus** - Manage Antivirus policy settings for cloud protection, Antivirus exclusions, remediation, scan options, and more.

  The *Microsoft Defender Antivirus* profile includes a new instance of settings that are otherwise found as part of a device restriction profile.

  Unlike settings that are part of a device restriction profile, these Antivirus settings support improved options. These settings can be used to manage Antivirus on co-managed devices when the [co-management workload slider](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) for Endpoint Protection is set to Intune. The Antivirus setting from device restriction profiles can’t be used with co-management.

- **Windows Security experience** – Manage [settings for the Windows Security app](../protect/antivirus-security-experience-windows-settings.md). The Windows security app is used by a number of Windows security features to provide notifications about the health and security of the machine. Security app notifications include firewalls, antivirus products, Windows Defender SmartScreen, and others.

### Disk encryption

[Disk encryption profiles](../protect/endpoint-security-configure-disk-encryption.md) focus on settings that manage a devices built-in encryption method, like BitLocker and FileVault.

#### Prerequisites

- Windows 10 or later
- macOS 10.13 or later

Because the encryption methods are part of the platforms, there are no additional general prerequisites. However, some settings for BitLocker can require a TPM.

#### macOS profiles

- **FileVault** – FileVault provides built-in Full Disk Encryption for macOS devices. Manage [settings for FileVault](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) on devices that run macOS.

#### Windows 10 profiles

- **BitLocker** – BitLocker Drive Encryption is a data protection feature that integrates with the operating system and addresses the threats of data theft or exposure from lost, stolen, or inappropriately decommissioned computers. Manage [settings for BitLocker](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker).

### Firewall

Use Firewall policy to configure a devices built-in firewall on devices that run macOS and Windows 10.

#### Prerequisites

- Windows 10 or later
- Any supported version of macOS

#### macOS profiles

- **macOS firewall** – Enable and configure settings for the built-in firewall on macOS.

#### Windows 10 profiles

- **Microsoft Defender Firewall** – Configure settings for Windows Defender Firewall with Advanced Security. Windows Defender Firewall provides host-based, two-way network traffic filtering for a device and can block unauthorized network traffic flowing into or out of the local device.

### Endpoint detection and response

When you integrate Defender ATP with Intune, you can use policy for endpoint detection and response.

The capabilities of Microsoft Defender ATP endpoint detection and response provide advanced attack detections that are near real-time and actionable. Security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats.

#### Prerequisites

- Windows 10 or later
- For Intune to manage endpoint detection and response settings on a device, Defender ATP must be installed on that device.

#### Windows 10 profiles

- **Endpoint detection and response** – Manage settings for Microsoft Defender ATP endpoint detection and response.

  The capabilities of Microsoft Defender ATP endpoint detection and response provide advanced attack detections that are near real-time and actionable. Security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats.

  To learn more, see [endpoint detection and response](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) in the Microsoft Defender ATP documentation.

### Attack surface reduction

Each attack surface reduction profile manages settings for a specific area of a Windows 10 device.

#### Prerequisites

- Windows 10 or later
- For Intune to manage attack surface reduction settings on a device, Defender ATP must be installed on that device.

#### Windows 10 profiles

- **App and browser isolation** – Manage settings for Windows Defender Application Guard (Application Guard), as part of Defender ATP. Application Guard helps to prevent old and newly emerging attacks and can isolate enterprise-defined sites as untrusted while defining what sites, cloud resources, and internal networks are trusted.

  To learn more, see [Application Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) in the Microsoft Defender ATP documentation.

- **Web protection** – Settings you can manage for Web protection in Microsoft Defender ATP configure network protection to secure your machines against web threats. By integrating with Microsoft Edge and popular third-party browsers like Chrome and Firefox, web protection stops web threats without a web proxy and can protect machines while they're away or on-premises. Web protection stops access to phishing sites, malware vectors, exploit sites, untrusted or low-reputation sites, and sites that you have blocked in your custom indicator list.

  To learn more, see [Web protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) in the Microsoft Defender ATP documentation.

- **Application control** - Application control settings can help mitigate security threats by restricting the applications that users can run and the code that runs in the System Core (kernel). Manage settings that can block unsigned scripts and MSIs, and restrict Windows PowerShell to run in Constrained Language Mode.

  To learn more, see [Application Control](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) in the Microsoft Defender ATP documentation.

- **Attack surface reduction rules** – Configure settings for attack surface reduction rules that target behaviors that malware and malicious apps typically use to infect computers, including:
  - Executable files and scripts used in Office apps or web mail that attempt to download or run files
  - Obfuscated or otherwise suspicious scripts
  - Behaviors that apps don't usually start during normal day-to-day work
Reducing your attack surface means offering attackers fewer ways to perform attacks.

  To learn more, see [Attack surface reduction rules](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction) in the Microsoft Defender ATP documentation.

- **Device control** – With settings for device control, you can configure devices for a layered approach to secure removable media. Microsoft Defender ATP provides multiple monitoring and control features to help prevent threats in unauthorized peripherals from compromising your devices.

  To learn more, see [How to control USB devices and other removable media using Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/device-control/control-usb-devices-using-intune) in the Microsoft Defender ATP documentation.

- Exploit protection - Exploit protection settings can help protect against malware that uses exploits to infect devices and spread. Exploit protection consists of a number of mitigations that can be applied to either the operating system or individual apps.

  To learn more, see [Enable exploit protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) in the Microsoft Defender ATP documentation.

### Account protection

Protect the identity and accounts of your users by configuring Windows Hello and credential guard.

#### Prerequisites

- Windows 10 or later

#### Windows 10 profiles

- **Account protection** – Settings for account protection policies help you protect user credentials.

  To learn more, see [Identity and access management](https://docs.microsoft.com/windows/security/identity-protection/) in the Windows identity and access management documentation.

## Use device compliance policy

Use device compliance policy to establish the conditions by which devices and users are allowed to access your network and company resources.

The [available compliance settings](../protect/device-compliance-get-started.md#next-steps) depend on the platform you use, but common policy rules include:

- Requiring devices run a minimum or specific OS version
- Setting password requirements
- Specifying a maximum allowed device threat-level, as determined by Defender ATP or another Mobile Threat Defense partner
- Use of network locations

In addition to setting conditions for compliance, you can configure automatic actions to take when a device is not compliant. Actions include sending email or notifications to alert device users about non-compliance, remotely locking devices, or even retiring non-compliant devices and removing any company data that might be on it.

When you integrate Intune with Azure AD [conditional access policies](#configure-conditional-access) to enforce compliance policies, Conditional access can use the compliance data to gate access to corporate resources for both managed devices, and devices that aren’t managed yet.

To learn more, see [Set rules on devices to allow access to resources in your organization using Intune](../protect/device-compliance-get-started.md).

## Configure conditional access

To protect your devices and corporate resources, you can use Azure Active Directory (Azure AD) Conditional Access policies with Intune.

Intune passes the results of your device compliance policies to Azure AD, which then uses conditional access policies enforce which devices and apps can access your corporate resources. Conditional access policies can also be configured to gate access for devices that aren’t managed by Intune. You can even use compliance details from [Mobile Threat Defense partners](../protect/mobile-threat-defense.md) you integrate with Intune.

The following are two common methods of using conditional access with Intune include:

- Device-based Conditional Access
- App-based conditional access

When you select *Conditional Access* from within the Microsoft Endpoint Manager admin center, the Conditional Access node that opens in the admin center is the node from Azure AD, and the policies you create are created in Azure.

To learn more about using conditional access with Intune, see [Learn about Conditional Access and Intune](../protect/conditional-access.md).

## Set up Integration with Defender ATP

When you integrate Microsoft Defender Advanced Threat Protection (Defender ATP) with Intune, you improve your ability to identify and respond to risks.

While Intune can integrate with several [Mobile Threat Defense partners](../protect/mobile-threat-defense.md), when you use Defender ATP you gain a tight integration between Defender ATP and Intune with access to deep device protection options, including:

- Security tasks – Seamless communication between ATP and Intune admins about devices at risk, how to remediate them, and confirmation when those risks are mitigated.
- Access to device protection settings *attack surface reduction* rules, and *endpoint detection and response* that help protect devices from a variety of risks
- Access to protection features like *Application Guard* and antivirus policy and settings that you can manage with Intune.

 To learn more about using Defender ATP with Intune, see [Enforce compliance for Microsoft Defender ATP with Conditional Access in Intune](../protect/advanced-threat-protection.md)

## Next steps

Configure:

- [Security baselines](../protect/security-baselines.md)
- [Compliance policies](../protect/device-compliance-get-started.md)
- [Conditional access policies](#configure-conditional-access)
- [Integration with Defender ATP](../protect/advanced-threat-protection.md)
