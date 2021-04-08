---
# required metadata

title: Manage firewall settings with endpoint security policies in Microsoft Intune | Microsoft Docs
description: Configure and deploy policies for devices you manage with endpoint security firewall policy in Microsoft Endpoint Manager. 
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

# Firewall policy for endpoint security in Intune

Use the endpoint security Firewall policy in Intune to configure a devices built-in firewall for devices that run macOS and Windows 10.

While you can configure the same firewall settings by using Endpoint Protection profiles for device configuration, the device configuration profiles include additional categories of settings. These additional settings are unrelated to firewalls and can complicate the task of configuring only firewall settings for your environment.

Find the endpoint security policies for firewalls under *Manage* in the **Endpoint security** node of the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

View [settings for Firewall profiles](../protect/endpoint-security-Firewall-profile-settings.md).

## Prerequisites for Firewall profiles

- Windows 10 or later
- Any supported version of macOS

## Firewall profiles

### Devices managed by Intune

**macOS profiles**:

- **macOS firewall** – Enable and configure settings for the built-in firewall on macOS.

**Windows 10 profiles**:

- **Microsoft Defender Firewall** – Configure settings for Windows Defender Firewall with Advanced Security. Windows Defender Firewall provides host-based, two-way network traffic filtering for a device and can block unauthorized network traffic flowing into or out of the local device.

- **Microsoft Defender Firewall rules** *(Preview)* - Define granular Firewall rules, including specific ports, protocols, applications and networks, and to allow or block network traffic. Each instance of this profile supports up to 150 custom rules.

### Devices managed by Configuration Manager

[!INCLUDE [Firewall policy prerequisites](../includes/tenant-attach-firewall-prerequisites.md)]

## Firewall rule mergers and policy conflicts

Plan for Firewall policies to be applied to a device using only one policy. Use of a single policy instance and policy type helps avoid having two separate policies apply different configurations to the same setting, which creates conflicts. When a conflict exists between two policy instances or types of policy that manage the same setting with different values, the setting isn't sent to the device.

- That form of policy conflict applies to the **Microsoft Defender Firewall** profile, which can conflict with other Microsoft Defender Firewall profiles, or a firewall configuration that’s delivered by a different policy type, like device configuration.

  *Microsoft Defender Firewall profiles* don't conflict with *Microsoft Defender Firewall rules* profiles.

When you use **Microsoft Defender Firewall rules** profiles, you can apply multiple rules profiles to the same device. However, when different rules exist for the same thing with different configurations, both are sent to the device and create a conflict, on that device.

- For example, if one rule blocks *Teams.exe* through the firewall and a second rule allows *Teams.exe*, both rules are delivered to the client. This result is different from conflicts created through other policies for  Firewall settings.

When rules from multiple rules profiles don't conflict with each other, devices merge the rules from each profile to create a combined firewall rule configuration on the device. This behavior enables you to deploy more than the 150 rules that each individual profile supports to a device.

- For example, you have two Microsoft Defender Firewall rules profiles. The first profile allows *Teams.exe* through the firewall. The second profile allows *Outlook.exe* through the firewall. When a device receives both profiles, the device is configured to allow both apps through the firewall.

## Firewall policy reports

*Reports for Firewall policy are in public preview.*

The reports for Firewall policy display status details about the firewall status for your managed devices.  Firewall reports support managed devices that run the following operating systems.

- Windows 10 or later

### Summary

Summary is the default view when you open the Firewall node. Open the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and then go to **Endpoint security** > **Firewall** > **Summary**.

This view provides:

- An aggregate count of devices that have the firewall turned off.
- A list of your Firewall policies, including the name, type, if it's assigned, and when it was last modified.

### Windows 10 MDM devices with firewall off

This report is located in the Endpoint security node.  Open the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and then go to **Endpoint security** > **Firewall** >  **Windows 10 MDM devices with firewall off**.

Data is reported through the Windows [DeviceStatus CSP](/windows/client-management/mdm/devicestatus-csp), and identifies each device where the Firewall is off. By default, visible details include:

- Device name
- Firewall status
- User principle name
- Target (The method of device management)
- Last check in time

> [!div class="mx-imgBorder"]
> ![View the Firewall Off](media/endpoint-security-firewall-policy/firewall-off-report.png)

### Windows 10 MDM Firewall status

*This organizational report is also described in [Intune Reports](../fundamentals/reports.md#windows-10-mdm-firewall-status-organizational)*.

As an organizational report, this report is available from the **Reports** node.  Open the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and then go to **Reports** > **Firewall** >  **Windows 10 MDM Firewall status**.

> [!div class="mx-imgBorder"]
> ![Select firewall reports](media/endpoint-security-firewall-policy/select-firewall-reports.png)

Data is reported through the Windows [DeviceStatus CSP](/windows/client-management/mdm/devicestatus-csp), and reports on the status of the firewall on your managed devices. You can filter returns for this report by using one or more of the status detail categories.

Status details include:

- **Enabled** – The firewall on, and successfully reporting.
- **Disabled** - The firewall is turned off.
- **Limited** – The firewall isn’t monitoring all networks, or some rules are turned off.
- **Temporarily Disabled (default)** – The firewall is temporarily not monitoring all networks
- **Not applicable** – The device doesn’t support firewall reporting.

You can filter returns for this report by using one or more of the status detail categories.

> [!div class="mx-imgBorder"]
> ![View the Firewall Status report](media/endpoint-security-firewall-policy/firewall-status.png)

## Next steps

[Configure Endpoint security policies](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
