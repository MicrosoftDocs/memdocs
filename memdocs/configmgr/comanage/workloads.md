---
title: Co-management workloads
titleSuffix: Configuration Manager
description: Learn about the workloads that you can switch from Configuration Manager to Microsoft Intune.
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.date: 03/24/2023
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Co-management workloads

You don't have to switch any of the workloads. When you're ready, you can switch them individually, several at once, or all at the same time. However, until you switch the workloads over to Intune, Configuration Manager continues to manage the workloads that you don't switch to Intune, along with all other features of Configuration Manager that co-management doesn't support.

If you switch a workload to Intune, but later change your mind, you can switch it back to Configuration Manager, although there might be an impact. For example, Windows and Office versions will remain at a later version if installed by Intune.

Co-management supports the following workloads:

- [Compliance policies](#compliance-policies)

- [Windows Update policies](#windows-update-policies)

- [Resource access policies](#resource-access-policies)

- [Endpoint Protection](#endpoint-protection)

- [Device configuration](#device-configuration)

- [Office Click-to-Run apps](#office-click-to-run-apps)

- [Client apps](#client-apps)

## Compliance policies

Compliance policies define the rules and settings that a device must comply with to be considered compliant by conditional access policies. Also use compliance policies to monitor and remediate compliance issues with devices independently of conditional access. You can add evaluation of custom configuration baselines as a compliance policy assessment rule. For more information, see [Include custom configuration baselines as part of compliance policy assessment](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

For more information on the Intune feature, see [Use compliance policies to set rules for devices you manage with Intune](../../intune/protect/device-compliance-get-started.md).

## Windows Update policies

Windows Update for Business policies let you configure deferral policies for Windows 10 or later feature updates or quality updates for Windows 10 or later devices managed directly by Windows Update for Business.

> [!NOTE]
> To use Windows Autopatch with these devices, this workload needs to be managed by Intune. For more information, see [Prerequisites for Windows Autopatch](/windows/deployment/windows-autopatch/prepare/windows-autopatch-prerequisites).

For more information on the Intune feature, see [Manage Windows software updates in Intune](../../intune/protect/windows-update-for-business-configure.md).

## Resource access policies

> [!IMPORTANT]
> Starting in version 2203, these company resource access features of Configuration Manager and this co-management workload are no longer supported.<!-- 9315387 --> For more information, see [Frequently asked questions about resource access deprecation](../protect/plan-design/resource-access-deprecation-faq.yml).

Resource access policies configure VPN, Wi-Fi, email, and certificate settings on devices.

For more information on the Intune feature, see [Deploy resource access profiles](../../intune/configuration/device-profiles.md).

> [!NOTE]
> The resource access workload is also part of device configuration. These policies are managed by Intune when you switch the [Device Configuration](#device-configuration) workload.

## Endpoint Protection

<!--1357365-->

The Endpoint Protection workload includes the Defender suite of protection features:

- Microsoft Defender Antivirus
- Microsoft Defender Application Guard
- Microsoft Defender SmartScreen
- Microsoft Defender for Endpoint (formally known as Windows Defender Advanced Threat Protection)
- Windows Defender Firewall
- Windows Encryption (also known as BitLocker)
- Windows Defender Exploit Guard
- Windows Defender Application Control
- Windows Defender Security Center

For more information on the Intune feature, see [Windows 10 (and later) settings to protect devices using Intune](../../intune/protect/endpoint-protection-windows-10.md).

> [!NOTE]
> When you switch this workload, the Configuration Manager policies stay on the device until the Intune policies overwrite them. This behavior makes sure that the device still has protection policies during the transition.
>
> The Endpoint Protection workload is also part of device configuration. The same behavior applies when you switch the [Device Configuration](#device-configuration) workload.<!-- SCCMDocs.nl-nl issue #4 -->
>
>When the Endpoint Protection workload resides with Intune, Windows Information Protection settings will apply from both Configuration Manager and Intune. Configuration Manager will continue to apply Windows Information Protection policy until the Device Configuration workload is moved to Intune.<!-- 4184095 -->
>
> The Microsoft Defender Antivirus settings that are part of the Device restrictions profile type for Intune Device configuration are not included in scope of the Endpoint protection slider. To manage Microsoft Defender Antivirus for co-managed devices with the endpoint protection slider enabled, use the new Antivirus policies in **Microsoft Intune admin center** > **Endpoint security** > **Antivirus**. The new policy type has new and improved options available, and support all of the same settings available in the Device restrictions profile. <!--6609171-->
>
> The Windows Encryption feature includes BitLocker management. For more information on the behavior of this feature with co-management, see [Deploy BitLocker management](../protect/deploy-use/bitlocker/deploy-management-agent.md#co-management-and-intune).<!-- SCCMDocs#2321 -->

## Device configuration

<!--1357903-->

The device configuration workload includes settings that you manage for devices in your organization. Switching this workload also moves the **Resource Access** and **Endpoint Protection** workloads.

You can still deploy settings from Configuration Manager to co-managed devices even though Intune is the device configuration authority. This exception might be used to configure settings that your organization requires but aren't yet available in Intune. Specify this exception on a [Configuration Manager configuration baseline](../compliance/deploy-use/create-configuration-baselines.md). Enable the option to **Always apply this baseline even for co-managed clients** when creating the baseline. You can change it later on the **General** tab of the properties of an existing baseline.

To use Windows Autopatch with these devices, this workload needs to be managed by Intune. For more information, see [Prerequisites for Windows Autopatch](/windows/deployment/windows-autopatch/prepare/windows-autopatch-prerequisites).

For more information on the Intune feature, see [Create a device profile in Microsoft Intune](../../intune/configuration/device-profile-create.md).

> [!NOTE]
> A policy created from the settings catalog is controlled by the Device Configuration workload slider regardless of the contents of the policy. 
> 
> When you switch the device configuration workload, it also includes policies for the Windows Information Protection feature. Only policies from Intune will apply once the Device Configuration workload is moved to Intune.<!-- 4184095 -->

> [!NOTE]
> In order to tattoo remove Endpoint protection settings, Device Configuration workload also needs to be switched. 

## Office Click-to-Run apps

<!--1357841-->

This workload manages Microsoft 365 Apps on co-managed devices.

- After moving the workload, the app shows up in the **Company Portal** on the device

- Office updates may take around 24 hours to show up on client unless the devices are restarted

- There's a [global condition](../apps/deploy-use/create-global-conditions.md) that's added by default as a requirement to new Microsoft 365 applications. When you transition this workload, co-managed clients don't meet the requirement on the application. Then they don't install Microsoft 365 deployed via Configuration Manager. The global condition is named either:
   - **Microsoft 365 apps managed by Microsoft Intune** (version 2111 or later) <!--12425123, 10784457-->
   - **Are Office 365 applications managed by Intune on the device** (version 2107 and earlier)

Updates can be managed using either of the following features:

- [Use Update Channel and Target Version settings to update Microsoft 365 with Microsoft Intune Administrative Templates](../../intune/configuration/administrative-templates-update-office.md)
- [Manage Microsoft 365 Apps with Configuration Manager](../sum/deploy-use/manage-office-365-proplus-updates.md).

> [!NOTE]
> To use Windows Autopatch with these devices, this workload needs to be managed by Intune. For more information, see [Prerequisites for Windows Autopatch](/windows/deployment/windows-autopatch/prepare/windows-autopatch-prerequisites).

For more information on the Intune feature, see [Add Microsoft 365 apps to Windows devices with Microsoft Intune](../../intune/apps/apps-add-office365.md).

## Client apps

<!--1357892-->

> [!TIP]
> This feature may appear in the list of features as **Mobile apps for co-managed devices**.<!-- 5849669 -->

Use Intune to manage client apps and PowerShell scripts on co-managed Windows 10 or later devices. After you transition this workload, any available apps deployed from Intune are available in the Company Portal. Apps that you deploy from Configuration Manager are available in Software Center.

For more information on the Intune feature, see [What is Microsoft Intune app management?](../../intune/apps/app-management.md)

> [!NOTE]
> In Windows 10 version 1903 and later, PowerShell scripts still run on co-managed devices even if you haven't switched the **Client Apps** workload to Intune.

When you enable Microsoft Connected Cache on your Configuration Manager distribution points, they can serve Microsoft Intune Win32 apps to co-managed clients. For more information, see [Microsoft Connected Cache in Configuration Manager](../core/plan-design/hierarchy/microsoft-connected-cache.md#support-for-intune-win32-apps).

## Diagram for app workloads

:::image type="content" source="media/co-management-apps.svg" alt-text="Diagram of co-management app workloads." lightbox="media/co-management-apps.svg":::

> [!TIP]
> You can configure the Company Portal to also show Configuration Manager apps. If you change this app portal experience, it changes the behaviors described in the above diagram. For more information, see [Use the Company Portal app on co-managed devices](company-portal.md).<!--CMADO-3601237,INADO-4297660-->

## Next steps

[How to switch workloads](how-to-switch-workloads.md)
