---
# required metadata

title: Use Intune to manage Microsoft Defender for Endpoint Security on devices not enrolled with Microsoft Intune 
description: Use Intune profiles to manage security settings for Microsoft Defender for Endpoint on devices that register in your Azure Active Directory. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/01/2023
ms.topic: how-to
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

# Manage Microsoft Defender for Endpoint on devices with Microsoft Intune

With Microsoft Defender for Endpoint (MDE), you can now deploy security configurations from Microsoft Intune directly to your onboarded devices without requiring a full Microsoft Intune device enrollment. This capability is known as *Security Management for Microsoft Defender for Endpoint*. With this capability, devices that aren’t managed by a Microsoft Intune service can receive security configurations for Microsoft Defender for Endpoint directly from Endpoint Manager.

When devices are managed through this capability:

- You use the Microsoft Intune admin center to configure endpoint security policies for MDE and assign those policies to Azure AD groups
- Devices get the policies based on their Azure Active Directory device object. A device that isn’t already present in Azure Active Directory is joined as part of this solution
- When a device receives a policy, the Defender for Endpoint components on the device enforce the policy and report on the device's status. The device's status is available in the Microsoft Intune admin center

This scenario extends the Microsoft Intune Endpoint Security surface to devices that aren't capable of enrolling in Intune. When a device is managed by Intune (enrolled to Intune) the device won't process policies for Security Management for Microsoft Defender for Endpoint. Instead, use Intune to deploy policy for Defender for Endpoint to your devices.

:::image type="content" source="./media/mde-security-integration/endpoint-security-overview.png" alt-text="Conceptual diagram of the MDE-Attach solution." lightbox="./media/mde-security-integration/endpoint-security-overview.png":::

[!INCLUDE [Prerequisites](includes/security-config-mgt-prerequisites.md)]

## Monitor status

Status and reports for policies that target devices in this channel are available from the policy node under Endpoint security in the Microsoft Intune admin center.

Drill in to the policy type and then select the policy to view its status. The following policy types support MDE security configuration:

- Antivirus > *Microsoft Defender Antivirus*
- Firewall > *Microsoft Defender Firewall* or *Microsoft Defender Firewall Rules*
- Endpoint detection and response > *Endpoint detection and response*

When you select a policy, you'll see information about the device check-in status, and can select:

- **View report** - View a list of devices that received the policy. You can select a device to drill in and see its per-setting status. You can then select a setting to view more information about it, including other policies that manage that same setting, which could be a source of conflict.

- **Per setting status** - View the settings that are managed by the policy, and a count of success, errors, or conflicts for each setting.

## Frequently asked questions and considerations

### Device check-in frequency

Devices managed by this capability check-in with Microsoft Intune every 90 minutes to update policy.

You can manually sync a device on-demand from the [Microsoft 365 Defender portal](https://security.microsoft.com/). Sign-in to the portal and go to **Devices**. Select a device that is managed by MDE, and then select the **Policy sync** button:  

:::image type="content" source="./media/mde-security-integration/policy-sync-from-mde.png" alt-text="Manually sync devices managed by MDE." lightbox="./media/mde-security-integration/policy-sync-from-mde.png":::

The Policy sync button only appears for devices that are successfully managed by MDE. 

### Devices protected by Tamper Protection

If a device has Tamper Protection turned on, it will not be possible to edit its settings without turning off Tamper Protection. 

### Assignment Filters and Security Management for Microsoft Defender for Endpoint

Assignment filters aren't supported for devices communicating through the Microsoft Defender for Endpoint channel. While assignment filters can be added to a policy that could be targeted at these devices, the device will ignore assignment filters. For assignment filter support, the device must be enrolled in to Microsoft Intune.

### Deleting and removing devices

You can delete devices that use this flow using one of two methods:

- From within the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Devices** > **All devices**, select a device that displays either *MDEJoined* or *MDEManaged* in the *Managed by* column, and then select **Delete**.
- You can also remove devices from the scope of Configuration Management in the Security Center.

Once a device is removed from either location, that change will propagate to the other service.

### Unable to enable the Security Management for Microsoft Defender for Endpoint workload in Endpoint Security

Most initial provisioning flows are typically completed by an Administrator of both services (such as a Global Administrator). There are some scenarios where Role-based Administration is used to customize the permissions of administrators. Today, individuals who are delegated the *Endpoint Security Manager* role might not have the necessary permissions to enable this feature.

### Active Directory joined devices

Devices that are joined to Active Directory will use their **existing infrastructure** to complete the Hybrid Azure Active Directory join process. While the Defender for Endpoint component will start this process, the join action uses your Federation provider or Azure Active Directory Connect (Azure AD Connect) to complete the join. Review [Plan your hybrid Azure Active Directory join implementation](/azure/active-directory/devices/hybrid-azuread-join-plan) to learn more about configuring your environment.

To troubleshoot Azure Active Directory onboarding issues, see  [Troubleshoot Security Configuration Management Azure Active Directory onboarding issues](/microsoft-365/security/defender-endpoint/troubleshoot-security-config-mgt).

### Unsupported security settings

The following security settings are pending deprecation. The Security Management for Microsoft Defender for Endpoint flow doesn't support these settings:

- Expedite telemetry reporting frequency (under **Endpoint Detection and Response**)
- AllowIntrusionPreventionSystem (under **Antivirus**)

### Managing security configurations on domain controllers

Currently, devices aren't supported to complete a Hybrid Join to Azure Active Directory. Since an Azure Active Directory trust is required, domain controllers aren't currently supported. We're looking at ways to add this support.

### Server Core installation

Due to the platform limitations of Server core installations, these aren't supported by Security Management for Microsoft Defender for Endpoint.

### PowerShell restrict mode

Security Management for Microsoft Defender for Endpoint won't work for a device that has PowerShell *LanguageMode* configured with *ConstrainedLanguage* mode ‘enabled’. For more information, see [about_Language_Modes](/powershell/module/microsoft.powershell.core/about/about_language_modes) in the PowerShell documentation.

## Next steps

[Monitor Defender for Endpoint](../protect/advanced-threat-protection-monitor.md)
