---
title: Technical Preview 1712 | Microsoft Docs
titleSuffix: Configuration Manager
description: Learn about features available in the Technical Preview version 1712 for Configuration Manager.
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Capabilities in Technical Preview 1712 for Configuration Manager

*Applies to: Configuration Manager (technical preview branch)*

This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1712. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. 

Review [Technical Preview for Configuration Manager](technical-preview.md) before installing this version of the technical preview. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Known Issues in this Technical Preview:**
- **Update to a new preview version fails when you have a site server in passive mode**. If you have a [primary site server in passive mode](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), then you must uninstall the passive mode site server before updating to this new preview version. You can reinstall the passive mode site server after your site completes the update.

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
Based upon your feedback, in this release you have the option to configure an application deployment to not automatically upgrade any superseded version. Now when creating the deployment, on the **Deployment Settings** page of the **Deploy Software Wizard**, for either **Available** or **Required** install purpose, you can enable or disable the option to **Automatically upgrade any superseded versions of this application**.


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
Deploy to a user or device multiple applications for installation, as either available or required (with the deadline in the future). Do not require administrator approval. For more information, see [Deploy applications](../../apps/deploy-use/deploy-applications.md).

**In Software Center:**
 1. The **Applications** tab should open by default. 
 2. To enter multi-select mode in the list view, click the new icon ![Software Center multi-select icon](media/software-center-multi-select-apps.png) in the upper right corner.
 3. Select two or more apps to install by clicking the checkbox to the left of the apps in the list.
 4. Click the **Install Selected** button.

The apps install as normal, only now in succession.


## Client-based PXE responder service
<!-- 1357148 -->
A common challenge for customers is providing PXE services at remote/branch offices with little or no server infrastructure. The distribution point role supports client operating systems, but can't be PXE-enabled due to the dependency on Windows Deployment Services.

New client settings are now available to enable a PXE responder service on Configuration Manager clients. A PXE-enabled boot image must reside in the PXE responder's client cache.

### Try it out!
Ensure there are no existing PXE-enabled distribution points or other PXE servers in the test environment that may conflict with this client PXE responder.

In the Configuration Manager console:
1. In the **Software Library** workspace under **Operating Systems**, **Task Sequences**: create a task sequence using the custom template.
   1. Click **Add**, select **General**, and then the **Set Task Sequence Variable** step. Enter **SMSTSPersistContent** as the task sequence variable, and enter the value **TRUE**.
   1. Click **Add**, select **Software**, and then the **Download Package Content** step. Click the gold asterisk and then select a PXE-enabled boot image. Include both x86 and x64 boot images. Configure the step to place it into the **Configuration Manager client cache**.
   1. Click **Add**, select **General**, and then the **Set Task Sequence Variable** step. Enter **SMSTSPreserveContent** as the task sequence variable, and enter the value **TRUE**.
2. In the **Administration** workspace under **Client Settings**: create a custom client device settings policy.
   1. Select the **Client Cache Settings** group.
   1. Set the **Enable Configuration Manager client in full OS to share content** setting to **Yes**.
   1. Set the **Enable PXE responder service** setting to **Yes**.
   1. For the **Create a self-signed certificate or import a PKI client certificate** setting, click **Provide a certificate**. Select **Import certificate** if your test environment has PKI, otherwise click **OK** to create a self-signed certificate. 
   1. Configure the remaining settings as necessary for your test environment. (The default settings should work unless there are specific network or security requirements.)
3. Deploy the task sequence and custom client settings to a collection of target clients to be PXE responders. Wait for the policies to apply and the task sequence to run.
4. Start another client on the same subnet to PXE/network boot as normal.

### Known issues
- The task sequence editor displays a red error icon for the **Download Package Content** step when you add a boot image, but the task sequence successfully saves. Opening this task sequence again in the editor also shows a harmless warning that referenced objects cannot be found. <!-- sms427542 -->
- The boot image from the Download Package Content step does not show in the custom task sequence's list of references. Also the **Distribute Content** action is not available. <!-- sms504017 -->


## Change in the Configuration Manager client install  
As a result of your feedback, Silverlight is no longer installed on clients automatically.<!--1356195-->
  

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
We have made the following improvements to the Configuration Manager console, which were a result of your feedback.

- Device list displays primary user: Device lists under Assets and Compliance, Devices, now display the primary user by default. The last logged on user can also be added as an optional column. <!-- 1357280 -->
- Renamed collections display in existing collection membership rules: If a collection is a member of another collection and it is renamed, then the new name is updated under membership rules.<!--1357282--> 


## Improvements to operating system deployment
We made the following improvements to operating system deployment, some of which were the result of your feedback.
- Default log viewer in boot image: In Windows PE, when launching cmtrace.exe, you are no longer prompted to choose whether to make this program the default viewer for log files. <!-- SMS 500897 -->
- Download Package Content step: You can now add boot images to this task sequence step.


## Windows 10 Feedback Hub app integration

We love feedback so much that we're now enabling feedback through the [Feedback Hub app](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) built-in to Windows 10. When you **Add new feedback**, be sure to select the **Enterprise Management** category, and then choose from one of the following subcategories:
- Configuration Manager Client
- Configuration Manager Console
- Configuration Manager OS Deployment
- Configuration Manager Server

Continue to use our product feedback site to vote on new feature ideas in Configuration Manager.


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for Configuration Manager](technical-preview.md).    
