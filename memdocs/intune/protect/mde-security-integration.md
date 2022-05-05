---
# required metadata

title: Use Intune to manage Microsoft Defender for Endpoint Security on devices not enrolled with Microsoft Intune 
description: Use Intune profiles to manage security settings for Microsoft Defender for Endpoint on devices that register in your Azure Active Directory. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/12/2022
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
ms.collection: M365-identity-device-management
ms.reviewer: mattcall

---

# Manage Microsoft Defender for Endpoint on devices with Microsoft Endpoint Manager

With Microsoft Defender for Endpoint (MDE), you can now deploy security configurations from Microsoft Endpoint Manager directly to your onboarded devices without requiring a full Microsoft Endpoint Manager device enrollment. This capability is known as *Security Management for Microsoft Defender for Endpoint*. With this capability, devices that aren’t managed by a Microsoft Endpoint Manager service can receive security configurations for Microsoft Defender for Endpoint directly from Endpoint Manager.

When devices are managed through this capability:

- You use the Microsoft Endpoint Manager admin center to configure endpoint security policies for MDE and assign those policies to Azure AD groups
- Devices get the policies based on their Azure Active Directory device object. A device that isn’t already present in Azure Active Directory is joined as part of this solution
- When a device receives a policy, the Defender for Endpoint components on the device enforce the policy and report on the devices status. The device's status is available in the Microsoft Endpoint Manager admin center

This scenario extends the Microsoft Endpoint Manager Endpoint Security surface to devices that aren't capable of enrolling in Endpoint Manager. When a device is managed by Endpoint Manager (enrolled to Intune) the device won't process policies for Security Management for Microsoft Defender for Endpoint. Instead, use Intune to deploy policy for Defender for Endpoint to your devices.

:::image type="content" source="./media/mde-security-integration/endpoint-security-overview.png" alt-text="Conceptual diagram of the MDE-Attach solution." lightbox="./media/mde-security-integration/endpoint-security-overview.png":::

[!INCLUDE [Prerequisites](includes/security-config-mgt-prerequisites.md)]

## Monitor status

Status and reports for policies that target devices in this channel are available from the policy node under Endpoint security in the Microsoft Endpoint Manager admin center.

Drill in to the policy type and then select the policy to view its status. The following policy types support MDE security configuration:

- Antivirus > *Microsoft Defender Antivirus*
- Firewall > *Microsoft Defender Firewall* or *Microsoft Defender Firewall Rules*
- Endpoint detection and response > *Endpoint detection and response*

When you select a policy, you'll see information about the device check-in status, and can select:

- **View report** - View a list of devices that received the policy. You can select a device to drill in and see its per-setting status. You can then select a setting to view more information about it, including other policies that manage that same setting, which could be a source of conflict.

- **Per setting status** - View the settings that are managed by the policy, and a count of success, errors, or conflicts for each setting.

## Frequently asked questions and considerations

### Assignment Filters and Security Management for Microsoft Defender for Endpoint

Assignment filters aren't supported for devices communicating through the Microsoft Defender for Endpoint channel. While assignment filters can be added to a policy that could be targeted at these devices, the device will ignore assignment filters. For assignment filter support, the device must be enrolled in to Microsoft Endpoint Manager.

### Deleting and removing devices

Devices that are using this flow will be unable to be deleted from the Microsoft Endpoint Manager admin center. The enrollment state is driven from Microsoft Defender for Endpoint, and deleting them from the admin center would only cause them to be removed temporarily. If devices need to be removed from management, they should be removed from the scope of Configuration Management in the Security Center. Once removed, that change will be propagated across services.

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

Currently, devices are not supported to complete a Hybrid Join to Azure Active Directory. Since an Azure Active Directory trust is required, domain controllers aren't currently supported. We're looking at ways to add this support.

### Non-persistent VDI environments

Due to the potential effect on Azure Active Directory environments with respect to device lifecycle and service quota, we advise against testing the current installation files and builds shared in this public preview in a non-persistent VDI environment.

### Server Core installation

Due to the platform limitations of Server core installations, these are not supported by Security Management for Microsoft Defender for Endpoint.

## Next steps

[Monitor Defender for Endpoint](../protect/advanced-threat-protection-monitor.md)
