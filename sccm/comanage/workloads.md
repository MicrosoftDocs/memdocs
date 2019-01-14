---
title: Co-management workloads
titleSuffix: Configuration Manager
description: Learn about the workloads that you can switch from Configuration Manager to Microsoft Intune. 
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
---

# Co-management workloads

You don't have to switch the workloads, or you can do them individually when you're ready. Configuration Manager continues to manage all other workloads, including those workloads that you don't switch to Intune, and all other features of Configuration Manager that co-management doesn't support.

Co-management supports the following workloads:

- [Compliance policies](#compliance-policies)  

- [Windows Update policies](#windows-update-policies)  

- [Resource access policies](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Device configuration](#device-configuration)  

- [Office Click-to-Run apps](#office-click-to-run-apps)  

- [Client apps](#client-apps)  



## Compliance policies 

Compliance policies define the rules and settings that a device must comply with to be considered compliant by conditional access policies. Also use compliance policies to monitor and remediate compliance issues with devices independently of conditional access. 

For more information on the Intune feature, see [Device compliance policies](https://docs.microsoft.com/intune/device-compliance-get-started).  



## Windows Update policies

Windows Update for Business policies let you configure deferral policies for Windows 10 feature updates or quality updates for Windows 10 devices managed directly by Windows Update for Business. 

For more information on the Intune feature, see [Configure Windows Update for Business deferral policies](https://docs.microsoft.com/intune/windows-update-for-business-configure).  



## Resource access policies

Resource access policies configure VPN, Wi-Fi, email, and certificate settings on devices. 

For more information on the Intune feature, see [Deploy resource access profiles](https://docs.microsoft.com/intune/device-profiles).



## Endpoint Protection
<!--1357365-->

Starting in Configuration Manager 1802, the Endpoint Protection workload includes the Windows Defender suite of antimalware protection features: 

- Windows Defender Application Guard  
- Windows Defender Firewall  
- Windows Defender SmartScreen  
- Windows Encryption  
- Windows Defender Exploit Guard  
- Windows Defender Application Control  
- Windows Defender Security Center  
- Windows Defender Advanced Threat Protection  
- Windows Information Protection  

For more information on the Intune feature, see [Endpoint Protection for Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).



## Device configuration
<!--1357903-->

Starting in Configuration Manager 1806, the device configuration workload includes settings that you manage for devices in your organization. Switching this workload also moves the **Resource Access** and **Endpoint Protection** workloads.

You can still deploy settings from Configuration Manager to co-managed devices even though Intune is the device configuration authority. This exception might be used to configure settings that your organization requires but aren't yet available in Intune. Specify this exception on a [Configuration Manager configuration baseline](/sccm/compliance/deploy-use/create-configuration-baselines). Enable the option to **Always apply this baseline even for co-managed clients** when creating the baseline. You can change it later on the **General** tab of the properties of an existing baseline.  

For more information on the Intune feature, see [Create a device profile in Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  



## Office Click-to-Run apps
<!--1357841-->

Starting in Configuration Manager 1806, this workload manages Office 365 apps on co-managed devices. 

- After moving the workload, the app shows up in the **Company Portal** on the device  

- Office updates may take around 24 hours to show up on client unless the devices are restarted  

- There's a new global condition, **Are Office 365 applications managed by Intune on the device**. This condition is added by default as a requirement to new Office 365 applications. When you transition this workload, co-managed clients don't meet the requirement on the application. Then they don't install Office 365 deployed via Configuration Manager.  

For more information on the Intune feature, see [Assign Office 365 apps to Windows 10 devices with Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365). 



## Client apps
<!--1357892-->

Starting in Configuration Manager version 1806, use Intune to manage client apps on co-managed Windows 10 devices. After you transition this workload, any available apps deployed from Intune are available in the Company Portal. Apps that you deploy from Configuration Manager are available in Software Center.

For more information on the Intune feature, see [What is Microsoft Intune app management?](https://docs.microsoft.com/intune/app-management). 

> [!Note]  
> The client apps workload is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  



## Next steps

[How to switch workloads](/sccm/comanage/how-to-switch-workloads)  


