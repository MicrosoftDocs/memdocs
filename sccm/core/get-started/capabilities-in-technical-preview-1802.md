---
title: "Technical Preview 1802 | Microsoft Docs"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview version 1802 for System Center Configuration Manager."
ms.custom: na
ms.date: 02/09/2018 
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Capabilities in Technical Preview 1802 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1802. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. 

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



## Microsoft Edge browser policies
<!-- 1357310 -->
For customers who use the [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) web browser on Windows 10 clients, you can now create a Configuration Manager compliance settings policy to configure several Microsoft Edge settings. This policy currently includes the following settings:
- **Set Microsoft Edge browser as default**: configures the Windows 10 default app setting for web browser to Microsoft Edge
- **Allow address bar drop-down**: Requires Windows 10, version 1703 or later. For more information, see [AllowAddressBarDropdown browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Sync favorites between Microsoft browsers**: Requires Windows 10, version 1703 or later. For more information, see [SyncFavoritesBetweenIEAndMicrosoftEdge browser policy](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Clear browsing data on exit**: Requires Windows 10, version 1703 or later. For more information, see [ClearBrowsingDataOnExit browser policy](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Allow Do Not Track headers**: For more information, see [AllowDoNotTrack browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
<!-- more settings added for 1802 TP -->

### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.

**Create the policy**
1. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Expand **Compliance Settings** and select the new **Microsoft Edge Browser Profiles** node. Click the ribbon option to **Create Microsoft Edge Browser Policy**.
2. Specify a **Name** for the policy, optionally enter a **Description**, and click **Next**.
3. On the **Settings** page, change the value to **Configured** for the settings to include in this policy, and click **Next**.
4. On the **Supported Platforms** page, select the operating system versions and architectures to which this policy applies, and click **Next**. 
5. Complete the wizard.

**Deploy the policy**
1. Select your policy and click the ribbon option to **Deploy**.
2. Click **Browse** to select the user or device collection to which to deploy the policy. 
3. Select additional options as necessary. Generate alerts when the policy is not compliant. Set the schedule by which the client evaluates the device's compliance with this policy.
4. Click **OK** to create the deployment.

Like any compliance settings policy, the client remediates the settings on the schedule you specify. [Monitor and report on device compliance](/sccm/compliance/deploy-use/monitor-compliance-settings) in the Configuration Manager console.

## Deployment templates for task sequences
<!-- 1357391 -->
The deployment wizard for task sequences can now create a deployment template. The deployment template can be saved and applied to an existing or new task sequence to create a deployment. 

### Try it out!  
Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked. 

 **Create a deployment template for a new task sequence deployment** <br/> 
1. In the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**.
2. Right-click on a task sequence and select **Deploy**. 
3. On the **General** tab, note there is now an option to **Select Deployment Template**. 
4. Continue through the **Deploy Software Wizard** selecting the deployment settings for the task sequence. 
5. When you reach the **Summary** tab of the **Deploy Software Wizard**, click on **Save As Template**.
6. Give the template a name and select the settings to save in the template. 
7. Click **Save**. The template is now available for use from the **Select Deployment Template** option.

## Product Lifecycle dashboard
<!--1319632-->
The new Product Lifecycle dashboard shows the state of the Microsoft Product Lifecycle policy for Microsoft products installed on devices managed with Configuration Manager. The dashboard provides you with information about Microsoft products in your environment, supportability state, and support end dates. You can use the dashboard to understand the availability of support for each product. 

To access the Lifecycle Dashboard, in the Configuration Manager console, go to **Assets and Compliance** >**Asset Intelligence** >**Product Lifecycle**

## Improvements to reporting
<!--1357653-->
As a result of [your feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and) we added a new report, **Windows 10 Servicing details for a specific collection**. This report shows Resource ID, NetBIOS name, OS name, OS release name, build, OS branch, and servicing state for Windows 10 devices. To access the report, go to **Monitoring** >**Reporting** >**Reports** >**Operating Systems** >**Windows 10 Servicing details for a specific collection**.

## Improvements to Software Center
<!--1357592-->
As a result of [your feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid) installed applications can now be hidden in Software Center. Applications that are already installed will no longer show in the Applications tab when this option is enabled. 

### Try it out!
Enable the **Hide Installed Applications in Software Center** setting in the Software Center client settings. Observe the behavior on Software Center when the end user installs an application.

## Improvements to Run Scripts
<!--1236459-->
The [Run Scripts](/sccm/apps/deploy-use/create-deploy-scripts) feature now returns script output using JSON formatting. This format consistently returns a readable script output. Scripts that fail to run may not get output returned. 

## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
