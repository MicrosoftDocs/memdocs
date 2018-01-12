---
title: "Technical Preview 1801 | Microsoft Docs"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview version 1801 for System Center Configuration Manager."
ms.custom: na
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: angrobe
---
# Capabilities in Technical Preview 1801 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1801. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. 

Review [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview) before installing this version of the technical preview. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Known Issues in this Technical Preview:**
-   **Update to a new preview version fails when you have a site server in passive mode**. If you have a [primary site server in passive mode](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), then you must uninstall the passive mode site server before updating to this new preview version. You can reinstall the passive mode site server after your site completes the update.

  To uninstall the passive mode site server:
  1. In the Configuration Manager console, go to **Administration** > **Overview** > **Site Configuration** > **Servers and Site System Roles**, and then select the passive mode site server.
  2. In the **Site System Roles** pane, right-click on the **Site server** role, and then choose **Remove Role**.
  3. Right-click on the passive mode site server, and then choose **Delete**.
  4. After the site server uninstalls, on the active primary site server restart the service **CONFIGURATION_MANAGER_UPDATE**.
<!--sms 489412-->


**The following are new features you can try out with this version.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## Create phased deployments
Phased deployments allow you to automate a coordinated, sequenced rollout of applications, software updates, or task sequences. You no longer need to create multiple deployments when you want to deploy to pilot collections then to production collections. Phased deployments can be stopped manually or automatically based on configured criteria. 

<!--1357405-->
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
1. Create a phased deployment for a task sequence. </br>
    a. In the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**.</br>
    b. Right-click on an existing task sequence and select **Create Phased Deployment**. </br>
    c. On the **General** tab, give the phased deployment a name, description (optional), and select **Automatically create default pilot and production phases**. </br>
    d. Populate the **Pilot collection** and **Production Collection** fields. Select **Next**.</br>
    e. On the **Scheduling** tab, choose one option for each of the scheduling settings and select **Next** when complete.  
    - Criteria for success of the pilot phase:
        - Deployment success percentage
        - Number of devices successfully deployed
    - Conditions for beginning the production phase of deployment:
        - Automatically begin this many days after the success of the pilot phase
        - Manually begin this phase of deployment
    - Once a device is targeted, apply the upgrade:
        - As soon as possible
        - Deadline time (relative to the time the device is targeted)</br>

    f. On the **Phases** tab, edit any of the phases if needed then click **Next**.</br>
    g. On the **Stop Criteria** tab, select an option to automatically stop deployment. 
    - Criteria for automatic stop of the deployments in all phases
        - Percentage of deployments failed in all phases
        - Number of devices with failed deployments in all phases </br>

    h. Confirm your selections on the **Summary** tab then click **Next** to proceed.


2. Create a phased deployment for an application.
3. Create a phased deployment for a software update.

## Deployment templates for task sequences
<!--1357391_Create Deployment Template for TS-->
The deployment wizard for task sequences can now create a deployment template. The deployment template can be saved and applied to an existing or new task sequence to create a deployment. 

### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
1. Create a deployment template from a new task sequence deployment.
    a. 
2. Apply an existing deployment template to a task sequence deployment. 

## New settings for Windows Defender Application Guard
<!--1356256--WD Suite support for files and virtual gpu-->
On Windows 10 version 1709 and later devices, there are two new host interaction settings for Windows Defender Application Guard. 
1. Websites can be given access to the host’s virtual graphics processor. 
2. Files downloaded inside the container can be persisted on the host. </br>


## Improvements to Run Scripts
The [**Run Scripts** feature](/sccm/apps/deploy-use/create-deploy-scripts) now allows you to import and run signed PowerShell scripts. 
- To keep the script integrity, signed scripts must be imported rather than using copy/paste. 
- Imported signed scripts cannot be edited after import.
<!--1236459_import_signed_scripts--->




## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
