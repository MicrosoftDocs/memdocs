---
title: "Technical Preview 1708 | Microsoft Docs"
description: "Learn about features available in the Technical Preview version 1708 for System Center Configuration Manager."
ms.custom: na
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Capabilities in Technical Preview 1708 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1708. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->




**The following are new features you can try out with this version.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## Improvements for specifying script parameters when you deploy PowerShell scripts from Configuration Manager
<!-- 1236459 -->

From Configuration Manager 1706 onwards, you can [Create and run PowerShell scripts from the Configuration Manager console](/sccm/apps/deploy-use/create-deploy-scripts).

In [Technical Preview 1707](/sccm/core/get-started/capabilities-in-technical-preview-1707#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager), we expanded on this capability to let Configuration Manager read parameters from the script.

In this Technical Preview, we've expanded the script parameters capability to detect which parameters are mandatory, and which are optional, and prompt you to enter these.

### Try it out!

1. Follow the instructions to [Create and run PowerShell scripts from the Configuration Manager console](/sccm/apps/deploy-use/create-deploy-scripts).
2. On the new **Script Parameters** page of the **Create Script Wizard**, choose a parameter, and then edit its values.
The wizard displays which parameters are mandatory, and which are optional.
4. When you have finished editing parameters, complete the wizard.

When the script runs, it will use any parameter values you configured. If you did not configure a mandatory parameter, the end user will be asked to supply the parameter when the script runs.

## Management insights
<!-- 1353967 -->
You can now gain insights into the current state of your environment based on analysis of data in the site database. Insights help you to better understand your environment and take action based on the insight. Review management insights in the Configuration Manager console at **Administration** > **Management Insights** > **All Insights**. In this release, the following insights are now available:

- **Applications without deployments**: Lists the applications in your environment that do not have active deployments. This helps you to find and delete unused applications to simplify the list of applications displayed in the console.
- **Empty collections**: Lists the collections in your environment that have no members. You can delete these collections to simplify the list of collections displayed when deploying objects, for example.


## Restart computers from the Configuration Manager console   
<!-- 1356283 -->
Beginning with this release, you can use the Configuration Manager console to identify client devices that require a restart, and then use a client notification action to restart them.  

To identify devices that are pending a restart, go to **Assets and Compliance** > **Devices** and select a collection with devices that might need a restart. After you select a collection you can view the status for each device in the details pane in a new column named **Restart Pending**. Each device has a value of **Yes**, or **No**.

To create the client notification to restart a device:
1.	Locate the device you want to restart in the Devices node of the console.
2.	Right-click on the device, select **Client Notification**, and then select **Restart Client**.
3.	Click **OK** on the message pop-up to confirm the restart request.

### Try it out!
Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
1.	Deploy an app or update to a device that will require that device to restart to complete installation.
2.	Locate the device in the **Assets and Compliance** > **Devices** node of the console and confirm it displays **Yes** in the **Restart Pending** column. It can take up to 20 minutes for the restart required status to be reflected in the console.
3.	Use the **Restart Client** notification action to configure a restart of the device.  
4.	Monitor the device to confirm the device successfully restarts after receiving the notification.
