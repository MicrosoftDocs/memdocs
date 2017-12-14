---
title: "Technical Preview 1712 | Microsoft Docs"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview version 1712 for System Center Configuration Manager."
ms.custom: na
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: angrobe
---
# Capabilities in Technical Preview 1712 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1712. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. 

Review [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview) before installing this version of the technical preview. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.     


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
<!--sms489412-->


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

## Do not automatically upgrade superseded applications
<!-- 1351266 -->
Based upon your [user voice feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior), in this release you have the option to configure an application deployment to not automatically upgrade any superseded version. Now when creating the deployment, on the **Deployment Settings** page of the **Deploy Software Wizard**, for either **Available** or **Required** install purpose, you can enable or disable the option to **Automatically upgrade any superseded versions of this application**.


## Install multiple applications in Software Center
<!-- 1357126 -->
If an end user or desktop technician needs to install multiple applications on a device, Software Center now supports installing multiple selected applications. This allows the user to be more efficient while not waiting for one installation to finish before starting the next.

When using multi-select mode in the **Applications** tab, the following criteria determine which apps Software Center enables for multi-select:
 - The app is visible to the user
 - The app isn't already installed
 - Administrator approval isn't required or is already granted
 - The app status is available (for example, not already downloading content)

### Try it out!
**In the Configuration Manager console:**
 1. Deploy to a user or device multiple applications for installation, as either Available or Required (with the deadline in the future).
    - Do not require administrator approval
See [Deploy applications](/sccm/apps/deploy-use/deploy-applications) for more information.

**In Software Center:**
 1. The **Applications** tab should open by default. 
 2. To enter multi-select mode in the list view, click the new icon ![Software Center multi-select icon](media/software-center-multi-select-apps.png) in the upper right corner.
 3. Select two or more apps to install by clicking the checkbox to the left of the apps in the list.
 4. Click the **Install Selected** button.

The apps install as normal, only now in succession.


## Change in the Configuration Manager client install  
As a result of your user voice feedback, [Silverlight is no longer installed on clients automatically.](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## Change to the Surface device dashboard
The Surface dashboard now displays firmware versions for Surface devices rather than operating system version. In the console, go to **Monitoring** > **Surface Devices**. You can view the following items:
- Percent of Surfaces
- Percent of Surface models
- Top five firmware versions
 <!--1355788-->


## Improvements to Office 365 Client Management dashboard 
The Office 365 Client Management dashboard now displays a list of relevant devices when graph sections are selected. In the console, go to **Software Library** >**Overview** >**Office 365 Client Management**. The dashboard is displayed on the right. Selecting criteria from the chart shows a list of devices.  
<!--1357281-->


## Improvements to the Configuration Manager console 
We have made the following improvements to the Configuration Manager console, which were a result of your user voice feedback.

- [Device list displays primary user](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user): Device lists under Assets and Compliance, Devices, now display the primary user by default. The last logged on user can also be added as an optional column. <!-- 1357280 -->
- [Renamed collections display in existing collection membership rules](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections): If a collection is a member of another collection and it is renamed, then the new name is updated under membership rules.<!--1357282--> 


## Improvements to operating system deployment
We made the following improvements to operating system deployment, some of which were the result of your user voice feedback.
 - [Default log viewer in boot image](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a): In Windows PE, when launching cmtrace.exe, you are no longer prompted to choose whether to make this program the default viewer for log files. <!-- SMS 500897 -->
 - Download Package Content step: you can now add boot images to this task sequence step



<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
