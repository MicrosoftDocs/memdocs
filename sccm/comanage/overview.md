---
title: Co-management for Windows 10 devices
titleSuffix: Configuration Manager
description: Learn how to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
#Customer intent: As an IT Pro, I want to enable co-management so that Configuration Manager is cloud-attached to Microsoft Intune.
---

# What is co-management?

<!-- 1350871 -->
Co-management enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune. It lets you cloud-attach your existing investment in Configuration Manager by adding new functionality. By using co-management, you have the flexibility to use the technology solution that works best for your organization. 

When a Windows 10 device has the Configuration Manager client and is enrolled to Intune, you get the benefits of both services. You control which workloads, if any, you switch the authority from Configuration Manager to Intune. Configuration Manager continues to manage all other workloads, including those workloads that you don't switch to Intune, and all other features of Configuration Manager that co-management doesn't support.

You're also able to pilot a workload with a separate collection of devices. Piloting allows you to test the Intune functionality with a subset of devices before switching a larger group. 

![Overview diagram of co-management](media/co-management-overview.png)



## Paths to co-management

There are two main paths to reach to co-management:  

- **Existing Configuration Manager clients**: You have Windows 10 devices that are already Configuration Manager clients. You set up hybrid Azure AD, and enroll them into Intune.  

- **New internet-based devices**: You have new Windows 10 devices that join Azure AD and automatically enroll to Intune. You install the Configuration Manager client to reach a co-management state.  



## Benefits 

When you enroll existing Configuration Manager clients in co-management, you gain the following immediate value:  

- Conditional access with device compliance  

- Intune-based remote actions:  
    - [Factory reset](https://docs.microsoft.com/intune/devices-wipe#factory-reset)  
    - [Selective wipe](https://docs.microsoft.com/intune/apps-selective-wipe)  
    - [Delete devices](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)  
    - [Restart device](https://docs.microsoft.com/intune/device-restart)  
    - [Fresh start](https://docs.microsoft.com/intune/device-fresh-start)   

- Centralized visibility of device health  

- Link users, devices, and apps with Azure Active Directory (Azure AD)  

- Modern provisioning with Windows Autopilot  

- Remote actions


Co-management also enables you to orchestrate with Intune for several workloads. For more information, see the [Workloads](#workloads) section. 



## Prerequisites


### Configuration Manager

Update to Configuration Manager version 1710 or later.

Starting in Configuration Manager version 1802, to enable co-management, your administrative user account in Configuration Manager must be a **Full Administrator** with **All** security scopes. For more information, see [Fundamentals of role-based administration](/sccm/core/understand/fundamentals-of-role-based-administration).<!--SCCMDoc issue 626-->  



### Azure AD

- Windows 10 devices must be joined to Azure AD. They can be either of the following types:  

    - [Hybrid Azure AD-joined](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), where the device is joined to your on-premises Active Directory and registered with your Azure Active Directory.  

    - [Azure AD-joined](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) only. (This type is sometimes referred to as "cloud domain-joined")<!--SCCMDocs issue 605-->  

- [Enable Windows 10 automatic enrollment](https://docs.microsoft.com/intune/windows-enroll)  


### Intune

For more information, see [Set up Intune](/intune/setup-steps).  

> [!Note]  
> If you have a hybrid MDM environment (Intune integrated with Configuration Manager), you can't enable co-management. However, you can start migrating users to Intune standalone and then enable their associated Windows 10 devices for co-management. For more information about migrating to Intune standalone, see [Start migrating from hybrid MDM to Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  

> [!Tip]  
> Make sure you assign an Intune license to the account that you use to sign in to your tenant. Otherwise, sign in fails with the error message "User not recognized".  


### Windows 10, version 1709 or later

Upgrade your devices to Windows 10, version 1709 or later. For more information, see [Adopting Windows as a service](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).



## Workloads 

You don't have to switch the workloads, or you can do them individually when you're ready. Configuration Manager continues to manage all other workloads, including those workloads that you don't switch to Intune, and all other features of Configuration Manager that co-management doesn't support.

Co-management supports the following workloads:

- [Compliance policies](#compliance-policies)  

- [Windows Update policies](#windows-update-policies)  

- [Resource access policies](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Device configuration](#device-configuration)  

- [Office Click-to-Run apps](#office-click-to-run-apps)  

- [Client apps](#client-apps)  


#### Compliance policies 
Compliance policies define the rules and settings that a device must comply with to be considered compliant by conditional access policies. Also use compliance policies to monitor and remediate compliance issues with devices independently of conditional access. 

For more information on the Intune feature, see [Device compliance policies](https://docs.microsoft.com/intune/device-compliance-get-started).  

#### Windows Update policies
Windows Update for Business policies let you configure deferral policies for Windows 10 feature updates or quality updates for Windows 10 devices managed directly by Windows Update for Business. 

For more information on the Intune feature, see [Configure Windows Update for Business deferral policies](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

#### Resource access policies
Resource access policies configure VPN, Wi-Fi, email, and certificate settings on devices. For details, see [Deploy resource access profiles](https://docs.microsoft.com/intune/device-profiles).

#### Endpoint Protection
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

#### Device configuration
<!--1357903-->
Starting in Configuration Manager 1806, the device configuration workload includes settings that you manage for devices in your organization. Switching this workload also moves the **Resource Access** and **Endpoint Protection** workloads.

You can still deploy settings from Configuration Manager to co-managed devices even though Intune is the device configuration authority. This exception might be used to configure settings that your organization requires but aren't yet available in Intune. Specify this exception on a [Configuration Manager configuration baseline](/sccm/compliance/deploy-use/create-configuration-baselines). Enable the option to **Always apply this baseline even for co-managed clients** when creating the baseline. You can change it later on the **General** tab of the properties of an existing baseline.  

For more information on the Intune feature, see [Create a device profile in Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  

#### Office Click-to-Run apps
<!--1357841-->
Starting in Configuration Manager 1806, this workload manages Office 365 apps on co-managed devices. 

- After moving the workload, the app shows up in the **Company Portal** on the device  

- Office updates may take around 24 hours to show up on client unless the devices are restarted  

- There's a new global condition, **Are Office 365 applications managed by Intune on the device**. This condition is added by default as a requirement to new Office 365 applications. When you transition this workload, co-managed clients don't meet the requirement on the application. Then they don't install Office 365 deployed via Configuration Manager.  

For more information on the Intune feature, see [Assign Office 365 apps to Windows 10 devices with Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365). 

#### Client apps
<!--1357892-->
Starting in Configuration Manager version 1806, use Intune to manage client apps on co-managed Windows 10 devices. After you transition this workload, any available apps deployed from Intune are available in the Company Portal. Apps that you deploy from Configuration Manager are available in Software Center.

For more information on the Intune feature, see [What is Microsoft Intune app management?](https://docs.microsoft.com/intune/app-management). 

> [!Note]  
> The client apps workload is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  



## Monitor co-management

The co-management dashboard helps you review machines that are co-managed in your environment. The graphs can help identify devices that might need attention.

![Screenshot of the co-management dashboard](media/co-management-dashboard.png)

For more information, see [How to monitor co-management](/sccm/comanage/how-to-monitor).



## Next steps

- [Learn more about immediate value and getting started with co-management](/sccm/comanage/quickstarts)  

- [Tutorial: Enable co-management for existing Configuration Manager clients](/sccm/comanage/tutorial-co-manage-clients)  

