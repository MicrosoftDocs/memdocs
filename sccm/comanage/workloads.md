---
title: Co-management workloads
titleSuffix: Configuration Manager
description: Learn about the workloads that you can switch from Configuration Manager to Microsoft Intune. 
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
---

# Co-management workloads

You don't have to switch the workloads, or you can do them individually when you're ready. Configuration Manager continues to manage all other workloads, including those workloads that you don't switch to Intune, and all other features of Configuration Manager that co-management doesn't support.

If you switch a workload to Intune, but later change your mind, you can switch it back to Configuration Manager.

Co-management supports the following workloads:

- [Compliance policies](#compliance-policies)  

- [Windows Update policies](#windows-update-policies)  

- [Resource access policies](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Device configuration](#device-configuration)  

- [Office Click-to-Run apps](#office-click-to-run-apps)  

- [Client apps](#client-apps)  

## Compliance policies

Compliance policies define the rules and settings that a device must comply with to be considered compliant by conditional access policies. Also use compliance policies to monitor and remediate compliance issues with devices independently of conditional access. Beginning in Configuration Manager version 1910, you can add evaluation of custom configuration baselines as a compliance policy assessment rule. For more information, see [Include custom configuration baselines as part of compliance policy assessment](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

For more information on the Intune feature, see [Device compliance policies](https://docs.microsoft.com/intune/device-compliance-get-started).  

## Windows Update policies

Windows Update for Business policies let you configure deferral policies for Windows 10 feature updates or quality updates for Windows 10 devices managed directly by Windows Update for Business.

For more information on the Intune feature, see [Configure Windows Update for Business deferral policies](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

## Resource access policies

Resource access policies configure VPN, Wi-Fi, email, and certificate settings on devices.

For more information on the Intune feature, see [Deploy resource access profiles](https://docs.microsoft.com/intune/device-profiles).

> [!Note]  
> The resource access workload is also part of device configuration. These policies are managed by Intune when you switch the [Device Configuration](#device-configuration) workload.

## Endpoint Protection

<!--1357365-->

The Endpoint Protection workload includes the Windows Defender suite of antimalware protection features:

- Windows Defender Antimalware
- Windows Defender Application Guard  
- Windows Defender Firewall  
- Windows Defender SmartScreen  
- Windows Encryption  
- Windows Defender Exploit Guard  
- Windows Defender Application Control  
- Windows Defender Security Center  
- Windows Defender Advanced Threat Protection (now known as Microsoft Defender Threat Protection)
- Windows Information Protection  

For more information on the Intune feature, see [Endpoint Protection for Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

> [!Note]  
> When you switch this workload, the Configuration Manager policies stay on the device until the Intune policies overwrite them. This behavior makes sure that the device still has protection policies during the transition.
>
> The Endpoint Protection workload is also part of device configuration. The same behavior applies when you switch the [Device Configuration](#device-configuration) workload.<!-- SCCMDocs.nl-nl issue #4 -->
>
> The Microsoft Defender Antivirus settings that are part of the Device restrictions profile type for Intune Device configuration are not included in scope of the Endpoint protection slider. To manage Microsoft Defender Antivirus for co-managed devices with the endpoint protection slider enabled, use the new Antivirus policies in **Microsoft Endpoint manager admin center** > **Endpoint security** > **Antivirus**. The new policy type has new and improved options available, and support all of the same settings available in the Device restrictions profile. <!--6609171-->

## Device configuration

<!--1357903-->

The device configuration workload includes settings that you manage for devices in your organization. Switching this workload also moves the **Resource Access** and **Endpoint Protection** workloads.

You can still deploy settings from Configuration Manager to co-managed devices even though Intune is the device configuration authority. This exception might be used to configure settings that your organization requires but aren't yet available in Intune. Specify this exception on a [Configuration Manager configuration baseline](../compliance/deploy-use/create-configuration-baselines.md). Enable the option to **Always apply this baseline even for co-managed clients** when creating the baseline. You can change it later on the **General** tab of the properties of an existing baseline.  

For more information on the Intune feature, see [Create a device profile in Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  

## Office Click-to-Run apps

<!--1357841-->

This workload manages Office 365 apps on co-managed devices.

- After moving the workload, the app shows up in the **Company Portal** on the device  

- Office updates may take around 24 hours to show up on client unless the devices are restarted  

- There's a new global condition, **Are Office 365 applications managed by Intune on the device**. This condition is added by default as a requirement to new Office 365 applications. When you transition this workload, co-managed clients don't meet the requirement on the application. Then they don't install Office 365 deployed via Configuration Manager.  

For more information on the Intune feature, see [Assign Office 365 apps to Windows 10 devices with Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365).

## Client apps

<!--1357892-->

Use Intune to manage client apps and PowerShell scripts on co-managed Windows 10 devices. After you transition this workload, any available apps deployed from Intune are available in the Company Portal. Apps that you deploy from Configuration Manager are available in Software Center.

For more information on the Intune feature, see [What is Microsoft Intune app management?](https://docs.microsoft.com/intune/app-management).

> [!Tip]  
> This feature was first introduced in version 1806 as a [pre-release feature](../core/servers/manage/pre-release-features.md). Beginning with version 2002, it's no longer a pre-release feature.  
>
> This feature may appear in the list of features as **Mobile apps for co-managed devices**.<!-- 5849669 -->

Starting in version 1910, when you enable Microsoft Connected Cache on your Configuration Manager distribution points, they can now serve Microsoft Intune Win32 apps to co-managed clients. For more information, see [Microsoft Connected Cache in Configuration Manager](../core/plan-design/hierarchy/microsoft-connected-cache.md#bkmk_intune).

## Diagram for app workloads

![Diagram of co-management app workloads](media/co-management-apps.svg)

[View the diagram at full size](media/co-management-apps.svg)

## Known issues

When the Endpoint Protection workload is moved over to Intune, the client may still honor policies set by Configuration Manager and Microsoft Defender. <!--5024559-->

To work around this issue, apply the CleanUpPolicy.xml using ConfigSecurityPolicy.exe after the Intune policies have been received by the client using the steps below:

1. Copy and save the below text as `CleanUpPolicy.xml`.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SecurityPolicy xmlns="http://forefront.microsoft.com/FEP/2010/01/PolicyData" Name="FEP clean-up policy"><PolicySection Name="FEP.AmPolicy"><LocalGroupPolicySettings><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Microsoft Antimalware"/><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Windows Defender"/></LocalGroupPolicySettings></PolicySection></SecurityPolicy>
   ```
1. Open an elevated command prompt to `ConfigSecurityPolicy.exe`. Typically this executable is in one of the following directories:
   - C:\Program Files\Windows Defender
   - C:\Program Files\Microsoft Security Client
1. From the command prompt, pass in the xml file to clean up the policy. For example, `ConfigSecurityPolicy.exe C:\temp\CleanUpPolicy.xml`.  

## Next steps

[How to switch workloads](how-to-switch-workloads.md)  
