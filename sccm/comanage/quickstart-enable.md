---
title: Enable co-management
titleSuffix: Configuration Manager
description: Quickly enable co-management in Configuration Manager to gain immediate value.
ms.date: 01/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8fac7ac5-96a3-4ec1-85cb-623b26bf5b1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Enable co-management

When you enable co-management, you can gain immediate value. Then once you're ready, you can start transitioning workloads as needed in your environment.



## Prerequisites

- Clients running Windows 10, version 1709 and later  

- An [Intune subscription](/intune/setup-steps)  

    > [!Tip]  
    > Make sure you assign an Intune license to the account that you use to sign in to your tenant. Otherwise, sign in fails with the error message "User not recognized".  

- Starting in Configuration Manager version 1802, to enable co-management, your administrative user account in Configuration Manager must be a **Full Administrator** with **All** security scopes. For more information, see [Fundamentals of role-based administration](/sccm/core/understand/fundamentals-of-role-based-administration).<!--SCCMDoc issue 626-->  



## Process

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Co-management** node. Click **Configure co-management** in the ribbon to open the **Co-management Onboarding Wizard**.  

2. On the **Subscription** page of the wizard, select **Sign In**. Sign in to your Intune tenant, and then select **Next**.  

3. On the **Enablement** page, choose your **Automatic enrollment into Intune** setting. Copy the command line for devices already enrolled in Intune, if needed.  

    > [!Note]  
    > Starting in version 1806, automatic enrollment isn't immediate for all clients. This behavior helps enrollment scale better for large environments. Configuration Manager randomizes enrollment based on the number of clients. For example, if your environment has 100,000 clients, when you enable this setting, enrollment occurs over several days.<!--1358003-->  

4. On the **Workloads** page, for each workload, choose which device group to move over for management with Intune. For more information, see [How to switch workloads](/sccm/comanage/how-to-switch-workloads). If you just want to enable co-management, you don't need to switch workloads at this time.  

5. On the **Staging** page, select a device collection to be the **Pilot collection**.  

6. Verify the **Summary** and complete the wizard.  



## Next steps

Now that you've enabled co-management, look at the following articles for immediate value you can gain in your environment:

- [Conditional access](/sccm/comanage/quickstart-conditional-access)  

- [Real-time actions from Intune](/sccm/comanage/quickstart-real-time-actions)  

- [Client health](/sccm/comanage/quickstart-client-health)  
