---
title: Enable co-management
titleSuffix: Configuration Manager
description: Quickly enable co-management in Configuration Manager to gain immediate value.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8fac7ac5-96a3-4ec1-85cb-623b26bf5b1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to enable co-management in Configuration Manager

When you enable co-management, you can gain immediate value. Then once you're ready, you can start transitioning workloads as needed in your environment.

Make sure the co-management prerequisites are set up before you start this process. For more information, see [Prerequisites](/sccm/comanage/overview#prerequisites).



## Process

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Co-management** node. Click **Configure co-management** in the ribbon to open the **Co-management Onboarding Wizard**.  

2. On the **Subscription** page of the wizard, select **Sign In**. Sign in to your Intune tenant, and then select **Next**.  

3. On the **Enablement** page, choose your **Automatic enrollment into Intune** setting, either **Pilot** or **All**.   

    This action enables automatic client enrollment in Intune for existing Configuration Manager clients. When you choose **Pilot**, only the Configuration Manager clients that are members of the pilot collection are automatically enrolled to Intune. This option allows you to enable co-management on a subset of clients to initially test co-management, and rollout co-management using a phased approach.  

    > [!Note]  
    > Starting in version 1806, automatic enrollment isn't immediate for all clients. This behavior helps enrollment scale better for large environments. Configuration Manager randomizes enrollment based on the number of clients. For example, if your environment has 100,000 clients, when you enable this setting, enrollment occurs over several days.<!--1358003-->  

    If you have internet-based devices that are already enrolled in Intune, copy the command line on this page. You can use this command line to install the Configuration Manager client as an app in Intune.

4. On the **Workloads** page, for each workload, choose which device group to move over for management with Intune. For more information, see [Workloads](/sccm/comanage/workloads).  

    If you only want to enable co-management, you don't need to switch workloads now. You can switch workloads later. For more information, see [How to switch workloads](/sccm/comanage/how-to-switch-workloads).  

    The **Pilot Intune** setting switches the associated workload only for the devices in the pilot collection. The **Intune** setting switches the associated workload for all co-managed Windows 10 devices.  

    > [!Important] 
    > Before you switch any workloads, make sure you properly configure and deploy the corresponding workload in Intune. Make sure that workloads are always managed by one of the management tools for your devices.  

5. On the **Staging** page, configure the following settings:  

    - **Pilot**: The pilot group contains one or more collections that you select. Use this group as part of your phased rollout of co-management. Start with a small test collection, and then add more collections to the pilot group as you roll out co-management to more users and devices. You can change the collections in the pilot group at any time.  

    - **Production**: Configure the **Exclusion group** with one or more collections. Devices that are members of any of the collections in this group are excluded from using co-management.  

6. To enable co-management, complete the wizard.  



## Next steps

Now that you've enabled co-management, look at the following articles for immediate value you can gain in your environment:

- [Conditional access](/sccm/comanage/quickstart-conditional-access)  

- [Remote actions from Intune](/sccm/comanage/quickstart-remote-actions)  

- [Client health](/sccm/comanage/quickstart-client-health)  
