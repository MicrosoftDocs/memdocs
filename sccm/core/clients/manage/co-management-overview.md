---
title: Co-management for Windows 10 devices
titleSuffix: Configuration Manager
description: Learn how to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
---

# Co-management for Windows 10 devices    

With previous Windows 10 updates, you can already join a Windows 10 device to on-premises Active Directory (AD) and cloud-based Azure AD at the same time (hybrid Azure AD). Starting with Configuration Manager version 1710, co-management takes advantage of this improvement. It enables you to concurrently manage Windows 10 version 1709 devices by using both Configuration Manager and Intune. <!-- 1350871 -->


## Why co-management?

Many customers want to manage Windows 10 devices in the same way they manage mobile devices using a simplified, lower cost, cloud-based solution. However, making the transition from traditional management to modern management can be challenging.  


## What is co-management?

Co-management enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Intune. It’s a solution that provides a bridge from traditional to modern management and gives you a path to make the transition using a phased approach.


## Benefits 

Immediate use of the following Intune features:  
 
- Remote actions
    - [Factory reset](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
    - [Selective wipe](https://docs.microsoft.com/intune/apps-selective-wipe)
    - [Delete devices](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
    - [Restart device](https://docs.microsoft.com/intune/device-restart)
    - [Fresh start](https://docs.microsoft.com/intune/device-fresh-start)  

- Orchestration with Intune for the following workloads:
    - [Compliance policies](https://docs.microsoft.com/intune/device-compliance-get-started)
    - [Resource access policies](https://docs.microsoft.com/intune/device-profiles)
    - [Windows Update policies](https://docs.microsoft.com/intune/windows-update-for-business-configure)
    - [Endpoint Protection](https://docs.microsoft.com/intune/endpoint-protection-windows-10), starting in Configuration Manager 1802. <!-- 1357365 -->
    - [Device configuration](https://docs.microsoft.com/intune/device-profile-create), starting in Configuration Manager 1806. <!-- 1357903 -->
    - [Office Click-to-Run apps](https://docs.microsoft.com/intune/apps-add-office365), starting in Configuration Manager 1806 <!--1357841-->
    - [Mobile apps](https://docs.microsoft.com/intune/app-management), starting in Configuration Manager 1806 as a pre-release feature. <!--1357892-->



## How to configure co-management

 There are two main paths to reach to co-management:  

   - Configuration Manager provisions co-management: You enroll into Intune your Azure AD-joined Windows 10 devices that are already Configuration Manager clients.  

   - Intune provisioned: For devices that are already Intune enrolled, you install the Configuration Manager client to reach a co-management state. 


### Configuration Manager

 -	Upgrade to Configuration Manager version 1710 or later.


### Azure Active Directory

 - Windows 10 devices must be joined or registered to Azure AD. This can be achieved through one of the following methods:  

     - [Hybrid Azure AD-joined](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup), where the device is joined to your on-premises Windows Server AD domain while also registered with your Azure AD environment.

     - Azure AD-joined only. (This type is sometimes referred to as "cloud domain-joined")<!--SCCMDocs issue 605-->

 - [Enable Windows 10 automatic enrollment](https://docs.microsoft.com/intune/windows-enroll).  


### Intune

 - [How to set up Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription) or [Set up Intune](/intune/setup-steps)  

 - [Start migrating from hybrid MDM to Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  

 > [!Note]  
 > If you have a hybrid MDM environment (Intune integrated with Configuration Manager), you can't enable co-management. However, you can start migrating users to Intune standalone and then enable their associated Windows 10 devices for co-management. For more information about migrating to Intune standalone, see [Start migrating from hybrid MDM to Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  


### Enable co-management 

 > [!Important]  
 > Starting in version 1802, to enable co-management, your administrative user account in Configuration Manager must be a **Full Administrator** with **All** security scopes. For more information, see [Fundamentals of role-based administration](/sccm/core/understand/fundamentals-of-role-based-administration).<!--SCCMDoc issue 626-->  

 In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Co-management** node. Click **Configure co-management** in the ribbon to open the **Co-management Onboarding Wizard**. 
   
1. On the **Subscription** page, click **Sign In**. Sign in to your Intune tenant, and then click **Next**.  

    > [!Tip]   
    > Make sure that the account used to sign in to your tenant has an Intune license assigned, otherwise it will fail with the error message "User not recognized".  

2. On the **Enablement** page, choose your **Automatic enrollment into Intune** setting. Copy the command line for devices already enrolled in Intune, if needed.  

    > [!Note]  
    > Starting in version 1806, automatic enrollment isn't immediate for all clients. This behavior helps enrollment scale better for large environments. Configuration Manager randomizes enrollment based on the number of clients. For example, if your environment has 100,000 clients, when you enable this setting, enrollment occurs over several days.<!--1358003-->  

3. On the **Workloads** page, for each workload, choose which device group to move over for management with Intune.  

4. On the **Staging** page, select a device collection to be the **Pilot collection**. Verify the **Summary** and complete the wizard.  


### Upgrade Windows 10 client

- Upgrade to [Windows 10, version 1709 (also known as the Fall Creators Update) and later](/sccm/osd/deploy-use/manage-windows-as-a-service)


### Configure workloads to switch to Intune 

The [Workloads able to be transitioned to Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) article shows you how to switch specific Configuration Manager workloads to Intune. The article also has instructions on changing the device groups for which workloads are transitioned.

#### Compliance policies 
Compliance policies define the rules and settings that a device must comply with to be considered compliant by conditional access policies. Also use compliance policies to monitor and remediate compliance issues with devices independently of conditional access. For details, see [Device compliance policies](https://docs.microsoft.com/intune/device-compliance-get-started).  

#### Windows Update policies
Windows Update for Business policies let you configure deferral policies for Windows 10 feature updates or quality updates for Windows 10 devices managed directly by Windows Update for Business. For details, see [Configure Windows Update for Business deferral policies](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

#### Resource access policies
Resource access policies configure VPN, Wi-Fi, email, and certificate settings on devices. For details, see [Deploy resource access profiles](https://docs.microsoft.com/intune/device-profiles).

#### Endpoint Protection
Starting in Configuration Manager 1802, the Endpoint Protection workload can be transitioned to Intune. For more information, see [Endpoint Protection for Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10)<!-- 1357365 --> and [Workloads able to be transitioned to Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).

#### Device configuration
Starting in Configuration Manager 1806, the device configuration workload can be transitioned to Intune. For more information, see [Create a device profile in Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create) and [Workloads able to be transitioned to Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).  <!--1357903-->

#### Office Click-to-Run apps
Starting in Configuration Manager 1806, the Office 365 workload can be transitioned to Intune. For more information, see [Workloads able to be transitioned to Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune). <!--1357841-->

#### Mobile apps
Starting in Configuration Manager version 1806, the mobile apps workload can be transitioned to Intune. This feature is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features). After you transition this workload, any available apps deployed from Intune are available in the Company Portal. Apps that you deploy from Configuration Manager are available in Software Center.<!--1357892-->


### Install Configuration Manager client to the devices enrolled in Intune

When Windows 10 devices are enrolled in Intune, install the Configuration Manager client on the devices [using a specific command-line](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client) to prepare the clients for co-management. Then, you enable co-management from the Configuration Manager console to start moving specific workloads to Intune for specific Windows 10 devices.
For Windows 10 devices that aren't yet enrolled in Intune, use automatic enrollment in Azure to enroll the devices. For new Windows 10 devices, use [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) to configure the Out of Box Experience (OOBE), which includes automatic enrollment that enrolls devices in Intune.

When you use Intune to install the Configuration Manager client, enable a [cloud management gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) in Configuration Manager.



## Monitor co-management

[The co-management dashboard](/sccm/core/clients/manage/co-management-dashboard) helps you review machines that are co-managed in your environment. The graphs can help identify devices that might need attention.



## Next steps

[Prepare Windows 10 devices for co-management](co-management-prepare.md)
