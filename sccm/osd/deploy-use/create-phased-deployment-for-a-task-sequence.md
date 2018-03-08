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
> Phased deployments are a pre-release feature introduced in Configuration Manager 1802. <!--1356837-->

## Create a default two phased deployment for a task sequence
Use the following instructions to create a phased deployment. 

1. In the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**.

2. Right-click on an existing task sequence and select **Create Phased Deployment**. 

3. On the **General** tab, give the phased deployment a name, description (optional), and select **Automatically create a default two phase deployment**. 

4. Populate the **First Collection** and **Second Collection** fields. Select **Next**.

5. On the **Settings** tab, choose one option for each of the scheduling settings and select **Next** when complete. 
    - **Criteria for success of the first phase.** (choose one)
        - **Deployment success percentage** -Specify percent of devices that successfully complete the deployment for phase success criteria. 
        - **Number of devices successfully deployed** -Specify number of devices that successfully complete the deployment for phase success criteria. 
    - **Conditions for beginning second phase of deployment after success of the first phase.** (choose one)
        - **Automatically begin this phase after a deferral period (in days)** - Choose the number of days to wait before beginning the second phase after the success of the first. 
        - **Manually begin the second phase of deployment** -Don't begin second phase automatically after success of the first. 
    - **Interval for targeting devices in the second phase (in days)** -The number of days to span targeting of device deployments across for the second phase. 
    - **Once a device is targeted, install the software** (choose one)
        - **As soon as possible** -Sets the deadline for installation on the device as soon as the device is targeted.
        - **Deadline time (relative to the time device is targeted)** -Sets deadline for installation a certain number of days after device is targeted. 
6. Specify **User Experience** such as **User Notifications** and **Write filter handling for Windows Embedded devices**.

7. Specify **Distribution Point** settings for the phase. Verify the summary for the phase.        

8. On the **Phases** tab, edit any of the phases if needed then click **Next**.

9. The **Stop Criteria** tab allows you to specify when to automatically stop deploying for all phases.
    - **Criteria for automatic stop of deployments in all phases** (choose one)
        - **Percentage of deployments failed across all phases** - Select the percentage of deployment failures to stop deployments in all phases. 
        - **Number of devices with failed deployments across all phases** - Choose the number of devices that failed the deployment to stop deployments in all phases.  

10. Confirm your selections on the **Summary** tab then click **Next** and proceed though the wizard.


## Create a phased deployment with manually configured phases for a task sequence
Follow the instructions to create a phased deployment where you manually configure all phases. You can configure up to 10 phases. 

1. In the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**.

2. Right-click on an existing task sequence and select **Create Phased Deployment**. 

3. On the **General** tab, give the phased deployment a name, description (optional), and select **Manually configure all phases**. 

4. On the **Phases** tab, click on **Add**.

5. Populate the **Phase Collection** for your first phase and choose if you want to **pre-download content for this task sequence**.  

6. On the **Phase Settings** tab, choose one option for each of the scheduling settings and select **Next** when complete. 
    - **Criteria for success of the previous phase.** (choose one)
        - **Deployment success percentage** -Specify percent of devices that successfully complete the deployment for the previous phase success criteria. 
        - **Number of devices successfully deployed** -Specify number of devices that successfully complete the deployment for previous phase success criteria. 
    - **Conditions for beginning this phase of deployment after success of the previous phase.** (choose one)
        - **Automatically begin this phase after a deferral period (in days)** - Choose the number of days to wait before beginning the next phase after the success of the previous phase. 
        - **Manually begin this phase of deployment** -Don't begin this phase automatically after success of the previous phase. 
    - **Interval for targeting devices in this phase (in days)** -The number of days to span targeting of device deployments across for this phase. 
    - **Once a device is targeted, install the software** (choose one)
        - **As soon as possible** -Sets the deadline for installation on the device as soon as the device is targeted.
        - **Deadline time (relative to the time device is targeted)** -Sets deadline for installation a certain number of days after device is targeted. 
     
7. Specify **User Experience** such as **User Notifications** and **Write filter handling for Windows Embedded devices**.

8. Specify **Distribution Point** settings for the phase. Verify the summary for the phase. 

9. On the **Phases** tab, add, edit, remove, or reorder any  phases as needed then click **Next**.

10. The **Stop Criteria** tab allows you to specify when to automatically stop deploying for all phases.
    - **Criteria for automatic stop of deployments in all phases** (choose one)
        - **Percentage of deployments failed across all phases** - Select the percentage of deployment failures to stop deployments in all phases. 
        - **Number of devices with failed deployments across all phases** - Choose the number of devices that failed the deployment to stop deployments in all phases.  

11. Confirm your selections on the **Summary** tab then click **Next** and proceed though the wizard.

