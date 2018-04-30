---
title: Technical Preview 1805
titleSuffix: Configuration Manager
description: Learn about new features available in the Configuration Manager Technical Preview version 1805.
ms.date: 05/11/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Capabilities in Technical Preview 1805 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1805. You can install this version to update and add new capabilities to your technical preview site. 

Review the [Technical Preview](/sccm/core/get-started/technical-preview) article before installing this update. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.     


<!--  Known Issues Template   -->
## Known Issues in this Technical Preview

### <a name="bkmk_appcathttps"></a> The application catalog web service point can't be HTTPS-enabled
<!--512637-->
If the application catalog web service point is HTTPS-enabled:

- Applications deployed as available to users don't show in Software Center  

- The following error shows in the awebsctl.log:  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### Workaround
Reconfigure the application catalog web service point to communicate using HTTP connections.  




</br>

**The following are new features you can try out with this version.**  



## Create a phased deployment with manually configured phases for a task sequence
<!--1358148--> 
You can now create a phased deployments with manually configured phases for a task sequence. You can also add up to 10 additional phases from the **Phases** tab on **Create Phased Deployment** wizard. 

### Try it out!
Follow the instructions to create a phased deployment where you manually configure all phases. Add additional phases from the **Phases** tab on **Create Phased Deployment** wizard using steps 4 though 9. You can configure up to 10 phases. Send [Feedback](#bkmk_feedback) letting us know how it worked. 

1. In the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**.  

2. Right-click on an existing task sequence and select **Create Phased Deployment**.  

3. On the **General** tab, give the phased deployment a name, description (optional), and select **Manually configure all phases**.  

4. On the **Phases** tab, click on **Add**.  

5. Populate the **Phase Collection** for your first phase and choose if you want to **pre-download content for this task sequence**.  

6. On the **Phase Settings** tab, choose one option for each of the scheduling settings and select **Next** when complete.  
    - **Criteria for success of the previous phase.** (Choose one. This is disabled for the first phase)
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

11. Confirm your selections on the **Summary** tab. Then click **Next** and proceed though the wizard.  

### Known issues
- When you edit a phase, it causes a console exception that a key is not found. As a temporary workaround in this technical preview, delete the phase, and then add a new phase with the desired changes.<!--512691-->  






## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
