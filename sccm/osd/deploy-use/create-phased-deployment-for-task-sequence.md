---
title: Create a phased deployment
titleSuffix: Configuration Manager
description: Use phased deployments to automate the rollout of software to several collections.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Create phased deployments with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Phased deployments automate a coordinated, sequenced rollout of software across multiple collections. For example, deploy software to a pilot collection, and then automatically continue the rollout based on success criteria. Create phased deployments with the default of two phases, or manually configure multiple phases. The phased deployment of task sequences doesn't support PXE or media installation. Starting in version 1806, create a phased deployment for an application.<!--1358147-->  

> [!NOTE]  
> Phased deployments is a pre-release feature introduced in Configuration Manager 1802. To enable the feature, see [pre-release feature](/sccm/core/servers/manage/pre-release-features).<!--1356837-->  

<!--
> [!Tip]
> The phased deployment feature was first introduced in version 1802 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version ---YYMM---, it's no longer a pre-release feature.<!--1356837
-->



## Prerequisites

#### Security scope
Deployments created by phased deployments aren't viewable to any administrative user that doesn't have the **All** security scope. For more information, see [Security scopes](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope).

#### Distribute application content
Before creating a phased deployment for an application, distribute the content to a distribution point.<!--518293-->



## <a name="bkmk_settings"></a> Phase settings

These settings are unique to phased deployments. Configure these settings when creating or editing the phases to control the scheduling and behavior of the phased deployment process. 


#### Criteria for success of the first phase  

- **Deployment success percentage**: Specify the percent of devices that need to successfully complete the deployment for the first phase to succeed. By default, this value is 95%. In other words, the site considers the first phase successful when the compliance state for 95% of the devices is **Success** for this deployment. The site then continues to the second phase, and creates a deployment of the software to the next collection.  


#### Conditions for beginning second phase of deployment after success of the first phase  

- **Automatically begin this phase after a deferral period (in days)**: Choose the number of days to wait before beginning the second phase after the success of the first. By default, this value is one day.  

- **Manually begin the second phase of deployment**: The site doesn't automatically begin the second phase after the first phase succeeds. This option requires that you manually start the second phase. For more information, see [Move to the next phase](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_move).  

    > [!Note]  
    > This option isn't available for phased deployments of applications.  


#### Gradually make this software available over this period of time (in days)
Starting in version 1806, configure this setting for the rollout in each phase to happen gradually. This behavior helps mitigate the risk of deployment issues, and decreases the load on the network that is caused by the distribution of content to clients. The site gradually makes the software available depending on the configuration for each phase. Every client in a phase has a deadline relative to the time the software is made available. The time window between the available time and deadline is the same for all clients in a phase. The default value of this setting is zero, so by default the deployment isn't throttled.<!--1358578-->  


#### Configure the deadline behavior relative to when the software is made available  

- **Installation is required as soon as possible**: Set the deadline for installation on the device as soon as the device is targeted.  

- **Installation is required after this period of time**: Set a deadline for installation a certain number of days after device is targeted. By default, this value is seven days.   


<!--### Examples
Include a timeline diagram
-->



## <a name="bkmk_auto"></a> Automatically create a default two-phase deployment

1. Start the Create Phased Deployment wizard in the Configuration Manager console. This action varies based on the type of software you're deploying:  

    - **Application** (only in version 1806 or later): Go to the **Software Library**, expand **Application Management**, and select **Applications**. Select an existing application, and then click **Create Phased Deployment** in the ribbon.  

    - **Task sequence**: Go to the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**. Select an existing task sequence, and then click **Create Phased Deployment** in the ribbon.  

2. On the **General** page, give the phased deployment a **Name**, **Description** (optional), and select **Automatically create a default two phase deployment**.  

3. Click **Browse** and select a target collection for both the **First Collection** and **Second Collection** fields. For a task sequence, select from device collections. For an application, select from user or device collections. Click **Next**.  

    > [!Important]  
    > The Create Phased Deployment wizard doesn't notify you if a deployment is potentially high-risk. For more information, see [Settings to manage high-risk deployments](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments) and the note when you [Deploy a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  

4. On the **Settings** page, choose one option for each of the scheduling settings. For more information, see [Phase settings](#bkmk_settings). Click **Next** when complete.  

5. On the **Phases** page, see the two phases that the wizard creates for the specified collections. Click **Next**.   

    > [!Note]  
    > This section covers the procedure to automatically create a default two phase deployment. The wizard lets you add, remove, reorder, edit, or view phases for a phased deployment. For more information on these additional actions, see [Create a phased deployment with manually configured phases](#bkmk_manual).  

6. Confirm your selections on the **Summary** tab, and then click **Next** to complete the wizard.  



## <a name="bkmk_manual"></a> Create a phased deployment with manually configured phases
<!--1358148--> 

Starting in version 1806, create a phased deployment with manually configured phases for a task sequence. Add up to 10 additional phases from the **Phases** tab of the Create Phased Deployment wizard. 

> [!Note]  
> You can't currently manually create phases for an application. The wizard automatically creates two phases for application deployments.


1. In the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**.  

2. Right-click on an existing task sequence and select **Create Phased Deployment**.  

3. On the **General** page of the Create Phased Deployment wizard, give the phased deployment a **Name**, **Description** (optional), and select **Manually configure all phases**.  

4. From the **Phases** page of the Create Phased Deployment wizard, the following actions are available:  

    - **Filter** the list of deployment phases. Enter a string of characters for a case-insensitive match of the Order, Name, or Collection columns. 

    - **Add** a new phase:  

        1. On the **General** page of the Add Phase Wizard, specify a **Name** for the phase, and then browse to the target **Phase Collection**. The additional settings on this page are the same as when normally deploying a task sequence.  

        2. On the **Phase Settings** page of the Add Phase Wizard, configure the scheduling settings, and select **Next** when complete. For more information, see [Settings](#bkmk_settings).   

            > [!Note]  
            > You can't edit the phase setting, **Deployment success percentage**, on the first phase. This setting only applies to phases that have a previous phase.  

        3. The settings on the **User Experience** and **Distribution Points** pages of the Add Phase Wizard are the same as when normally deploying a task sequence.  

        4. Review the settings on the **Summary** page, and then complete the Add Phase Wizard.  

    - **Edit**: After you've added a phase, select it, and click this button to edit the phase. This action opens the phase's Properties window, which has tabs the same as the pages of the Add Phase Wizard.  

    - **Remove**: Select an existing phase and click this button to delete the phase.  

       > [!Warning]  
       > There is no confirmation, and no way to undo this action.  

    - **Move Up** or **Move Down**: The wizard orders the phases by how you add them. The most recently added phase is last in the list. To change the order, select a phase, and then click one of these buttons to move the phase's location in the list.  

       > [!Important]  
       > Review the phase settings after changing the order. Make sure the following settings are still consistent with your requirements for this phased deployment:  
       > 
       > - Criteria for success of the previous phase  
       > - Conditions for beginning this phase of deployment after success of the previous phase   

5. Click **Next**. Review the settings on the **Summary** page, and then complete the Create Phased Deployment wizard.  


After you create a phased deployment, open its properties to make changes:  

- **Add** additional phases to an existing phased deployment.  

- If a phase isn't active, you can **Edit**, **Remove**, or **Move** it up or down. You can't move it before an active phase.  

- When a phase is active, it's read-only. You can't edit it, remove it, or move its location in the list. The only option is to **View** the properties of the phase.  

- An application phased deployment is always read-only.  



## Next steps
[Manage and monitor phased deployments](/sccm/osd/deploy-use/manage-monitor-phased-deployments)
