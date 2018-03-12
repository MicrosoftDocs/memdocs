---
title: Create a phased deployment for a task sequence
titleSuffix: "System Center Configuration Manager"
description: "Create phased deployments for task sequences"
ms.custom: na
ms.date: 03/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
caps.latest.revision: 1
author: mestew
ms.author: mstewart
manager: dougeby

---
# Create phased deployments for a task sequence with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Phased deployments automate a coordinated, sequenced rollout of a task sequence across multiple collections. You can create phased deployments with the default of two phases, or manually configure multiple phases. Phased deployment of task sequences does not support PXE or media installation. 

>[!NOTE]
> Phased deployments is a pre-release feature introduced in Configuration Manager 1802. <!--1356837-->

## Create a default two-phased deployment for a task sequence
Use the following instructions to create a phased deployment. 

1. In the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**.

2. Right-click on an existing task sequence and select **Create Phased Deployment**. 

3. On the **General** tab, give the phased deployment a name, description (optional), and select **Automatically create a default two phase deployment**. 

4. Populate the **First Collection** and **Second Collection** fields. Select **Next**.

5. On the **Settings** tab, choose one option for each of the scheduling settings and select **Next** when complete. 
    - **Criteria for success of the first phase.** 
        - **Deployment success percentage** -Specify percent of devices that successfully complete the deployment for phase success criteria. 
    - **Conditions for beginning second phase of deployment after success of the first phase** (choose one):
        - **Automatically begin this phase after a deferral period (in days)** - Choose the number of days to wait before beginning the second phase after the success of the first. 
        - **Manually begin the second phase of deployment** - Don't begin second phase automatically after success of the first. Require it to be started manually. 
    - **Once a device is targeted, install the software** (choose one):
        - **As soon as possible** - Sets the deadline for installation on the device as soon as the device is targeted.
        - **Deadline time (relative to the time device is targeted)** - Sets deadline for installation a certain number of days after device is targeted. 

6. On the **Phases** tab, click the first phase, then **Edit**.  Specify **User Experience** such as **User Notifications** and **Write filter handling for Windows Embedded devices**. Click **Apply**.

7. Specify **Distribution Points** settings for the phase on the **Distribution Points** tab. Click **Apply** and **OK**.        

8. On the **Phases** tab, edit the second phase for **User Experience** and **Distribution Points**. Click **Apply** and **OK**.

9. Confirm your selections on the **Summary** tab, and then click **Next** and proceed though the wizard.

>[!WARNING]
>Phased deployments will not notify you if a task sequence deployment is [high-risk](/sccm/protect/understand/settings-to-manage-high-risk-deployments.md). 


## Suspend and resume phases or move to the next phase
On occasion, you may need to manually suspend a phased deployment, resume a suspended phased deployment, or move onto the next phase. 

### Move to the next phase
When you select the setting **Manually begin the second phase of deployment**, you will need to start the second phase. Use the following instructions to move to the second phase: 

1. In the Configuration Manager console, select **Software Library**, expand **Operating Systems**, and click on **Task Sequences**.
2. Highlight the task sequence.
3. Click on the **Phased Deployment** tab near the bottom of the console. 
4. Right-click the phased deployment and select **Move to next phase**.
![Suspend, resume, or move to next phase](media/Suspend-phased-deployment.PNG)

### Suspend or resume a phased deployment
1. In the Configuration Manager console, select **Software Library**, expand **Operating Systems**, and click on **Task Sequences**.
2. Highlight the task sequence and click on the **Phased Deployment** tab near the bottom of the console. 
3. Select the phased deployment and click **Suspend** or **Resume** in the ribbon.

## Next steps
[Create a custom task sequence](create-a-custom-task-sequence.md) </br>
[Create a task sequence for non-operating system deployments](create-a-task-sequence-for-non-operating-system-deployments.md). 








