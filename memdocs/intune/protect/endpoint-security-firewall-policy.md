---
# required metadata

title: Manage firewall settings with endpoint security policies in Microsoft Intune | Microsoft Docs
description: Configure and deploy policies for devices you manage with endpoint security firewall policy in Microsoft Endpoint Manager. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
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

# Firewall policy for endpoint security in Intune

Use the endpoint security Firewall policy in Intune to configure a devices built-in firewall for devices that run macOS and Windows 10. Built-in firewalls include BitLocker for Windows devices and FileVault for macOS.

While you can configure the same firewall settings by using Endpoint Protection profiles for device configuration, the device configuration profiles include additional categories of settings. These additional settings are unrelated to firewalls and can complicate the task of configuring only firewall settings for your environment.

Find the endpoint security policies for firewalls under *Manage* in the **Endpoint security** node of the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

View [settings for Firewall profiles](../protect/endpoint-security-Firewall-profile-settings.md).

## Prerequisites for Firewall profiles

- Windows 10 or later
- Any supported version of macOS

## Firewall profiles

**macOS profiles**:

- **macOS firewall** – Enable and configure settings for the built-in firewall on macOS.

**Windows 10 profiles**:

- **Microsoft Defender Firewall** – Configure settings for Windows Defender Firewall with Advanced Security. Windows Defender Firewall provides host-based, two-way network traffic filtering for a device and can block unauthorized network traffic flowing into or out of the local device.

- **Microsoft Defender Firewall rules** *(Public preview)* - Define granular Firewall rules, including specific ports, protocols, applications and networks, and to allow or block network traffic. Each instance of this profile supports up to 150 custom rules.

## Firewall rule mergers and policy conflicts

Plan for Firewall policies to be applied to a device using only one policy. Use of a single policy instance and policy type helps avoid having two separate policies apply different configurations to the same setting, which creates conflicts. When a conflict exists between two policy instances or types of policy that manage the same setting with different values, the setting isn't sent to the device.

- That form of policy conflict applies to the **Microsoft Defender Firewall** profile, which can conflict with other Microsoft Defender Firewall profiles, or a firewall configuration that’s delivered by a different policy type, like device configuration.

  Microsoft *Defender Firewall profiles* don't conflict with *Microsoft Defender Firewall rules* profiles.

When you use **Microsoft Defender Firewall rules** profiles, you can apply multiple rules profiles to the same device. However, when different rules exist for the same thing with different configurations, both are sent to the device and create a conflict, on that device.

- For example, if one rule blocks *Teams.exe* through the firewall and a second rule allows *Teams.exe*, both rules are delivered to the client. This result is different from conflicts created through other policies for  Firewall settings.

When rules from multiple rules profiles don't conflict with each other, devices merge the rules from each profile to create combined firewall rule configuration on the device. This behavior enables you to deploy more than the 150 rules that each individual profile supports to a device.

- For example, you have two Microsoft Defender Firewall rules profiles. The first profile allows *Teams.exe* through the firewall. The second profile allows *Outlook.exe* through the firewall. When a device receives both profiles, the device is configured to allow both apps through the firewall.

## Next steps

[Configure Endpoint security policies](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
