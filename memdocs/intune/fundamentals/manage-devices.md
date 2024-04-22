---
# required metadata

title: Manage and secure devices in Intune
titleSuffix: Microsoft Intune
description: Learn more about the concepts and features you should know when managing devices that access organization resources in Microsoft Intune. You can manage new and existing devices, including BYOD personal devices, check health compliance and view reports, configure device features, and secure devices using mobile threat solutions.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 11/21/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice:
ms.localizationpriority: high
ms.assetid: 
# optional metadata
 
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
search.appverid:
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Manage your devices and control device features in Microsoft Intune

Managing devices is a significant part of any endpoint management strategy and solution. Organizations have to manage laptops, tablets, mobile phones, wearables, and more. It can be a large task, especially if you're not sure where to start.

Enter Microsoft Intune. Intune is a cloud-based service that can control devices through policy, including security policies. For more information on Intune and its benefits, go to [What is Microsoft Intune?](what-is-intune.md).

:::image type="content" source="./media/manage-devices/manage-devices-with-intune.png" alt-text="Diagram that shows organization owned and personal devices in the Microsoft Intune admin center and using compliance policies and Conditional Access for resource access." lightbox="./media/manage-devices/manage-devices-with-intune.png":::

The goal of any organization that's managing devices is to secure devices and the data they access. This task includes organization owned devices and personally owned devices that access your organization resources.

From a service perspective, Intune uses Microsoft Entra ID for device storage and permissions. Using the [Microsoft Intune admin center](tutorial-walkthrough-endpoint-manager.md), you can manage device tasks and policies in a central location designed for endpoint management.

This article discusses concepts and features you should consider when managing your devices.

## Manage organization owned and personal devices

Many organizations allow personally owned devices to access organization resources, including email, meetings, and so on. There are different options available and these options depend on how strict your organization is.

You can require personal devices be enrolled in your organization's device management services. On these personal devices, your admins can deploy policies, set rules, configure device features, and more. Or, you can use app protection policies that focus on protecting app data, such as Outlook, Teams, and Sharepoint. You can also use a combination of device enrollment and app protection policies.

For organization owned devices, they should be fully managed by your organization, and receive policies that enforce rules and protect data.

For more information and guidance, go to:

- [Microsoft Intune planning guide](intune-planning-guide.md)
- [Deployment guide: Setup or move to Microsoft Intune](deployment-guide-intune-setup.md)

## Use your existing devices and use new devices

You can manage new devices and existing devices. Intune supports Android, iOS/iPadOS, Linux, macOS, and Windows devices.

There are some things you should know. For example, if existing devices are managed by another MDM provider, then they might need to be factory reset. If the devices are using an older OS version, they might not be supported.

If your organization is investing in new devices, then it's recommended to start with a cloud approach using Intune.

For more information and guidance, go to:

- [Microsoft Intune planning guide](intune-planning-guide.md)
- [Deployment guide: Setup or move to Microsoft Intune](deployment-guide-intune-setup.md)

For more specific information by platform, go to:

- [Android platform deployment guide](deployment-guide-platform-android.md)
- [iOS/iPadOS platform deployment guide](deployment-guide-platform-ios-ipados.md)
- [Linux enrollment deployment guide](deployment-guide-enrollment-linux.md)
- [macOS platform deployment guide](deployment-guide-platform-macos.md)
- [Windows enrollment deployment guide](deployment-guide-enrollment-windows.md)

## Check the compliance health of your devices

Device compliance is a significant part of managing devices. Your organization will want to set password/PIN rules and check for security features on these devices. You'll want to know which devices don't meet your rules. This task is where compliance comes in.

You can create compliance policies that block simple passwords, require a firewall, set the minimum OS version, and more. You can use these policies and built-in reporting to see noncompliant devices and see the noncompliant settings on these devices. This information gives you an idea of the overall health of the devices accessing your organization resources.

Conditional Access is a feature of Microsoft Entra ID. With Conditional Access, you can enforce compliance. For example, if a device doesn't meet your compliance rules, then you can block access to organization resources, including Outlook, SharePoint, Teams, and more. Conditional Access helps your organization secure your data and protect your devices.

For more information, go to:

- [Use compliance policies to set rules for devices you manage](../protect/device-compliance-get-started.md)
- [Monitor results of your device compliance policies](../protect/compliance-policy-monitor.md)
- [Learn about Conditional Access and Intune](../protect/conditional-access.md)

## Control device features and assign policies to device groups

All devices have features that you can control and manage using policies. For example, you can block the built-in camera, allow Bluetooth pairing, manage the power button, and more.

For many organizations, it's common to create device groups. Device groups are Microsoft Entra groups that only include devices. They don't include user identities.

When you have device groups, you create policies that focus on the device experience or task, like running a single app or scanning bar codes. You can also create policies that include settings that you want to always be on the device, regardless of who's using the device.

You can group devices by OS platform, by function, by location, and other features you prefer.

Device groups can also include devices that are shared with many users or aren't associated with a specific user. These dedicated or kiosk devices are typically used by frontline workers (FLW) and can also be managed by Intune.

When the groups are ready, you can assign your policies to these device groups.

For more information, go to:

- [FLW device management in Intune](../../solutions/frontline-worker/frontline-worker-overview.md)
- [Get started with Microsoft 365 for frontline workers](/microsoft-365/frontline/flw-overview)
- [Windows device settings to run as a dedicated kiosk using Intune](../configuration/kiosk-settings.md)
- [Control access, accounts, and power features on shared PC or multi-user devices using Intune](../configuration/shared-user-device-settings.md)

## Secure your devices

To help secure your devices, you can install antivirus, scan & react to malicious activity, and enable security features.

In Intune, some common security tasks include:

- **Integrate with Mobile Threat Defense** (MTD) partners to help protect organization owned devices and personally owned devices. These MTD services scan the devices and can help remediate vulnerabilities.

  The MTD partners support different platforms, including Android, iOS/iPadOS, macOS, and Windows.

  For more specific information, go to [Mobile Threat Defense integration with Intune](../protect/mobile-threat-defense.md)

- **Use security baselines** on your Windows devices. Security baselines are preconfigured settings that you can deploy to your devices. These baseline settings focus on security at a granular level and can also be changed to meet any organization specific requirements.

  If you're not sure where to start, then look at security baseline and the built-in guided scenarios.

  For more specific information, go to:

  - [Use security baselines to configure Windows devices in Intune](../protect/security-baselines.md)
  - [Guided scenarios overview](guided-scenarios-overview.md)

- **Manage software updates, encrypt hard disks, configure built-in firewalls**, and more using built-in policy settings. You can also use Windows Autopatch for automatic patching of Windows, including Windows quality updates and Windows feature updates.

  For more information, go to:

  - [Manage endpoint security in Microsoft Intune](../protect/endpoint-security.md)
  - [Manage device security with endpoint security policies in Microsoft Intune](../protect/endpoint-security-policy.md)
  - [Windows Autopatch overview](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview)

- **Manage devices remotely** using the Intune admin center. You can remotely lock, restart, locate a lost device, restore a device to its factory settings, and more. These tasks are helpful if a device is lost or stolen, or if you're remotely troubleshooting a device.

  For more information, go to [Remote actions in Intune](../remote-actions/device-management.md).

## Next steps

- [Manage identities in Intune](manage-identities.md)
- [Manage apps](manage-apps.md)
