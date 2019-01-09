---
title: Switch co-management workloads
titleSuffix: Configuration Manager
description: Learn how to switch workloads currently managed by Configuration Manager to Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
---

# How to switch Configuration Manager workloads to Intune

One of the benefits of co-management is switching workloads from Configuration Manager to Microsoft Intune. When a Windows 10 device has the Configuration Manager client and is enrolled to Intune, you get the benefits of both services. You control which workloads, if any, you switch the authority from Configuration Manager to Intune. Configuration Manager continues to manage all other workloads, including those workloads that you don't switch to Intune, and all other features of Configuration Manager that co-management doesn't support.

For more information on the supported workloads, see [Workloads](/sccm/comanage/overview#workloads).

You can switch workloads when you enable co-management, or later when you're ready. If you haven't already enabled co-management, do that first. For more information, see [How to enable co-management](/sccm/comanage/how-to-enable).


After you enable co-management, modify the settings in the co-management properties. 

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Co-management** node.  

2. Select the co-management object, and then choose **Properties** in the ribbon.  

3. Switch to the **Workloads** tab. By default, all workloads are set to the **Configuration Manager** setting. To switch a workload, move the slider control for that workload to the desired setting.  

    ![Screenshot of Workloads tab on co-management properties page](media/properties-workloads.png)

    - **Configuration Manager**: Configuration Manager continues to manage this workload.  

    - **Pilot Intune**: Switch this workload only for the devices in the pilot collection. You can change the **Pilot collection** on the **Staging** tab of the co-management properties page.  

    - **Intune**: Switch this workload for all Windows 10 devices enrolled in co-management.  


> [!Important]  
> Before you switch any workloads, make sure you properly configure and deploy the corresponding workload in Intune. Make sure that workloads are always managed by one of the management tools for your devices.  

<!--1357377-->
Starting in Configuration Manager version 1806, when you switch a co-management workload, the co-managed devices automatically synchronize MDM policy from Microsoft Intune. This sync also happens when you initiate the **Download Computer Policy** action from client notifications in the Configuration Manager console. For more information, see [Initiate client policy retrieval using client notification](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).


