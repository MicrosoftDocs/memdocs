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
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->

## Create phased deployments
Phased deployments automate a coordinated, sequenced rollout of software without creating multiple deployments. In this Technical Preview version, the phased deployment wizard can be completed for task sequences in the admin console. However, deployments are not created. 

<!--1357405- Phased Deployments-->
### Try it out!  
  Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 
**Create a phased deployment for a task sequence** </br></br>
   1. In the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**.
   2. Right-click on an existing task sequence and select **Create Phased Deployment**. 
   3. On the **General** tab, give the phased deployment a name, description (optional), and select **Automatically create default pilot and production phases**. 
   4. Populate the **Pilot collection** and **Production Collection** fields. Select **Next**.
    5. On the **Scheduling** tab, choose one option for each of the scheduling settings and select **Next** when complete.  
    6. On the **Phases** tab, edit any of the phases if needed then click **Next**.
    7. Confirm your selections on the **Summary** tab then click **Next** to proceed.
  
 <!-- 
change to 1357405- not adding stop criteria as this TP is wizard walk through  only.
 On the **Stop Criteria** tab, select an option to automatically stop deployment. 
    - Criteria for automatic stop of the deployments in all phases
        - Percentage of deployments failed in all phases
        - Number of devices with failed deployments in all phases 
 -->
 
## Deployment templates for task sequences
The deployment wizard for task sequences can now create a deployment template. The deployment template can be saved and applied to an existing or new task sequence to create a deployment. 

### Try it out!  
Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked. 

 **Create a deployment template for a new task sequence deployment** <br/> <br/>
1. In the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**.
  2. Right-click on a task sequence and select **Deploy**. 
  3. On the **General** tab, note there is now an option to **Select Deployment Template**. 
  4. Continue through the **Deploy Software Wizard** selecting the deployment settings for the task sequence. 
  5. When you reach the **Summary** tab of the **Deploy Software Wizard**, click on **Save As Template**.
  6. Give the template a name and select the settings to save in the template. 
  7. Click **Save**. The template is now available for use from the **Select Deployment Template** option.
<!--1357391_Create Deployment Template for TS-->

## Improvements to automatic deployment rule evaluation schedule
Based upon your [user voice feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling), you can now schedule automatic deployment rule (ADR) evaluation to be offset from a base day. For example, an offset of two days after the second Tuesday of the month evaluates the rule on Thursday. <!--1357133- ADR eval schedule relative to Patch Tuesday-->

### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked. <br/>

**Create a custom schedule that evaluates and ADR offset from a base day** </br>
1.  In the **Software Library** workspace, expand **Software Updates**, and select **Automatic Deployment Rules**.
2. Right-click on **Automatic Deployment Rules** and choose **Create Automatic Deployment Rule**. 
3. Follow the prompts to complete the **General**, **Deployment Settings**, and **Software Updates** tabs. 
4. On the **Evaluation Schedule** tab, select **Run the rule on a schedule** and **Customize**.
5. For the custom schedule, select **Monthly** and put in a base day such as the second Tuesday. 
6. Check **Offset (days)** and the number of days for the offset then **OK** when finished.  
7. Complete the rest of the **Create Automatic Deployment Rule Wizard**. 

## Improvements to hardware inventory
For newly added classes, string lengths greater than 255 characters can be specified for hardware inventory properties that are not keys.
<!--1357389 - HINV string length-->

### Try it out!  
Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.<br/>

1. In the **Administration** workspace, click on **Client Settings** highlight a client device setting to edit, right-click then select **Properties**. 
2. Select **Hardware Inventory**, then **Set Classes**, and **Add**.
3. Click the **Connect** button.
4. Fill in **Computer Name**, **WMI namespace**, select **recursive** if needed. Provide credentials if necessary to connect. Click **Connect** to view the namespace classes.
5. Select a new class then click **Edit**.
6. Change the **Length** of at least one property, other than the key, to be greater than 255. Click **OK**. 
7. Ensure that the edited property is selected for **Add Hardware Inventory Class** and click **OK**. 
8. Collect hardware inventory with the newly added class containing a property greater than 255 characters in length. 

## Improvements to client settings for Software Center
In this version of the Technical Preview, improvements have been made for Software Center customization under the client settings. 

1. The client settings for Software Center now have a **Customize** button.
2. A preview has been added to show what the Software Center banner looks like.<!--1351224-->
    - If a logo is not selected, the preview shows the company name text and color.
    - If a logo is selected, the preview shows the logo and company name text.  
3.  **Hide unapproved applications in Software Center** is a new  setting for Software Center. When this option is enabled, user available applications that require approval are hidden in Software Center.<!--1355146-->

### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.

1. In the **Administration** workspace, click on **Client Settings** highlight a client device setting to edit. Right-click then select **Properties** then **Software Center**.
2.  Click on the **Customize** button. Try out the different customization settings including the preview.
3. Enable the setting **Hide unapproved applications in Software Center** and observe the changes in Software Center. 

## New settings for Windows Defender Application Guard
For Windows 10 version 1709 and later devices, there are two new host interaction settings for [Windows Defender Application Guard](/sccm/protect/deploy-use/create-deploy-application-guard-policy). 
1. Websites can be given access to the host’s virtual graphics processor. 
2. Files downloaded inside the container can be persisted on the host. </br>
 <!--1356256--WD Suite support for files and virtual gpu-->

## Improvements to Run Scripts
The [**Run Scripts** feature](/sccm/apps/deploy-use/create-deploy-scripts) now allows you to import and run signed PowerShell scripts. 
- To keep the script integrity, signed scripts must be imported rather than using copy/paste. 
- Imported signed scripts cannot be edited after import.
<!--1236459_import_signed_scripts--->
<!--1236459_import_signed_scripts POSSIBLE ISSUE, waiting on confirmation
[!IMPORTANT] In this Technical Preview, there is a temporary limitation where scripts can only be imported in the Run Scripts feature and can't be edited directly from the console. 
--->




## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
