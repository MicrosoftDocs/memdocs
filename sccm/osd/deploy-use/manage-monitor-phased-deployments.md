---
title: Manage & monitor phased deployments
titleSuffix: Configuration Manager
description: Understand how to manage and monitor phased deployments for software in Configuration Manager.
ms.date: 11/16/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Manage and monitor phased deployments

This article describes how to manage and monitor phased deployments. Management tasks include manually beginning the next phase, and suspend or resume a phase. 

First, you need to create a phased deployment: 
- [Application](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  
- [Software update](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Task sequence](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)  



## <a name="bkmk_move"></a> Move to the next phase

When you select the setting, **Manually begin the second phase of deployment**, the site doesn't automatically start the next phase based on success criteria. You need to move the phased deployment to the next phase.  

1. How to start this action varies based on the type of deployed software:  

    - **Application** (only in version 1806 or later): Go to the **Software Library** workspace, expand **Application Management**, and select **Applications**.   

    - **Software update** (only in version 1810 or later): Go to the **Software Library** workspace, and then select one of the following nodes:    
        - Software Updates  
            - **All Software Updates**  
            - **Software Update Groups**   
        - Windows 10 Servicing, **All Windows 10 Updates**  
        - Office 365 Client Management, **Office 365 Updates**  

    - **Task sequence**: Go to the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**.   

2. Select the software with the phased deployment.  

3. In the details pane, switch to the **Phased Deployments** tab.  

4. Select the phased deployment, and click **Move to next phase** in the ribbon.  

    ![Right-click menu showing actions on a phased deployment](media/Suspend-phased-deployment.PNG)



## <a name="bkmk_suspend"></a> Suspend and resume phases 

You can manually suspend or resume a phased deployment. For example, you create a phased deployment for a task sequence. While monitoring the phase to your pilot group, you notice a large number of failures. You suspend the phased deployment to stop further devices from running the task sequence. After resolving the issue, you resume the phased deployment to continue the rollout. 

1. How to start this action varies based on the type of deployed software:  

    - **Application** (only in version 1806 or later): Go to the **Software Library** workspace, expand **Application Management**, and select **Applications**.   

    - **Software update** (only in version 1810 or later): Go to the **Software Library** workspace, and then select one of the following nodes:    
        - Software Updates  
            - **All Software Updates**  
            - **Software Update Groups**   
        - Windows 10 Servicing, **All Windows 10 Updates**  
        - Office 365 Client Management, **Office 365 Updates**  

    - **Task sequence**: Go to the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**. Select an existing task sequence, and then click **Create Phased Deployment** in the ribbon.  

2. Select the software with the phased deployment.  

3. In the details pane, switch to the **Phased Deployments** tab.  

4. Select the phased deployment, and click **Suspend** or **Resume** in the ribbon.  

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="bkmk_monitor"></a> Monitor
<!--1358577-->

Starting in version 1806, phased deployments have a native monitoring experience. From the **Deployments** node in the **Monitoring** workspace, select a phased deployment, and then click **Phased Deployment Status** in the ribbon.

![Phased deployment status dashboard showing status of two phases](media/1358577-phased-deployment-status.png)

This dashboard shows the following information for each phase in the deployment:  

- **Total devices**: How many devices are targeted by this phase.  

- **Status**: The current status of this phase. Each phase can be in one of the following states:  

    - **Deployment created**: The phased deployment created a deployment of the software to the collection for this phase. Clients are actively targeted with this software.  

    - **Waiting**: The previous phase hasn't yet reached the success criteria for the deployment to continue to this phase.  

    - **Suspended**: An administrator suspended the deployment.  

- **Progress**: The color-coded deployment states from clients. For example: Success, In Progress, Error, Requirements Not Met, and Unknown. 

#### Success criteria tile

Use the **Select Phase** drop-down list to change the display of the **Success Criteria** tile. This tile compares the **Phase Goal** against the current compliance of the deployment. With the default settings, the phase goal is 95%. This value means that the deployment needs a 95% compliance to move to the next phase. 

In this example, the phase goal is 65%, and the current compliance is 66.7%. The phased deployment automatically moved to the second phase, because the first phase met the success criteria.
![Example Success Criteria tile from Phased Deployment Status](media/pod-status-success-criteria-tile.png)

The phase goal is the same as the **Deployment success percentage** on the Phase Settings for the *next* phase. For the phased deployment to start the next phase, that second phase defines the criteria for success of the first phase. To view this setting: 

1. Go to the phased deployment object on the software, and open the Phased Deployment Properties.  

2. Switch to the **Phases** tab. Select **Phase 2** and click **View**.  

3. In the phase Properties window, switch to the **Phase Settings** tab.  

4. View the value for **Deployment success percentage** in the *Criteria for success of the previous phase* group.  

For example, the following properties are for the same phase as the success criteria tile shown above where the criteria is 65%:  
![Phase settings tab on phase properties](media/phase-properties-phase-settings.png)

