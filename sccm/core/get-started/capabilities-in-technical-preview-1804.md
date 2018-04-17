---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: Learn about new features available in the Configuration Manager Technical Preview version 1804.
ms.custom: na
ms.date: 04/20/2018 
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Capabilities in Technical Preview 1804 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1804. You can install this version to update and add new capabilities to your technical preview site. 

Review the [Technical Preview](/sccm/core/get-started/technical-preview) article before installing this update. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**The following are new features you can try out with this version.**  


## Configure a remote content library for the site server  
<!--1357525-->
To free up hard drive space on your primary site server, relocate its [content library](/sccm/core/plan-design/hierarchy/the-content-library) to another storage location. You can move the content library to another drive on the site server, a separate server, or fault-tolerant disks in a storage area network (SAN). We recommend a SAN as it provides elastic storage that grows or shrinks over time to meet your changing content requirements. 

This remote content library is a new prerequisite for [site server role high availability](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability). 

> [!Note]  
> This action only moves the content library on the site server. It doesn't impact the location of the content library on distribution points. 

### Prerequisites  
- The site server computer account needs **read** and **write** permissions to the network path to which you are moving the content library. No components are installed on the remote system. 

### Try it out!
 Try to complete the tasks. Then send [Feedback](#bkmk_feedback) letting us know how it worked.

1. In the Configuration Manager console, switch to the **Administration** workspace. Expand **Site Configuration** and select **Sites**. On the **Summary** tab at the bottom of the details pane, notice a new column for the **Content Library**.  

2. Click **Manage content library** on the ribbon.  

3. Select **On a network share** and enter a valid network path. This path is the location to which the site moves the content library. Click **OK**.  

4. Note the **Status** property in the Content Library column on the details pane. It updates to show the site's progress in moving the content library. When in progress it displays the percentage complete. If there is an error state, it displays the error. Common errors include `access denied` or `disk full`. When complete it displays `OK`. See the **distmgr.log** for details. For more information, see [Site server and site system server logs](/sccm/core/plan-design/hierarchy/log-files#BKMK_SiteSiteServerLog).  

If you need to move the content library back to the site server, repeat this process but select the option **Local to the site server**.  

> [!Tip]  
> To move the content to another drive on the site server, use the **Content Library Transfer** tool. For more information, see [Configuration Manager Toolkit](#configuration-manager-toolkit).  



## <a name="bkmk_feedback"></a> Submit feedback from the Configuration Manager console  
<!--1357542-->

Send a smile! You can now directly tell the Configuration Manager team about your experiences. Sending feedback is easy from the Configuration Manager console. We want to hear all of your feedback: praise, problems, and suggestions.  

### Try it out!
 Try to complete the tasks. Then send **Feedback** letting us know how it worked.  

1. In the Configuration Manager console, click the smile button in the upper right corner above the ribbon.  

2. From the drop-down list, select one of the available options:  

   - **Send a smile**: You really liked something! For this option, enter the details of your feedback. Then optionally include a screenshot and your email address.  

   - **Send a frown**: You encountered a problem in the console, or something didn't work as expected. For this option, enter the details of the potential product issue. Then optionally include a screenshot, your email address, and diagnostic data.  

   - **Send a suggestion**: You have an idea to change and improve Configuration Manager. This option opens our [UserVoice](https://configurationmanager.uservoice.com) site in your web browser.  

This feedback goes directly to the Microsoft product team for Configuration Manager. While using the Windows 10 Feedback Hub is still supported, you're encouraged to use the in-console feedback mechanism.  

The following anonymous information is always included with the feedback for context:  

 - Configuration Manager console version and language  

 - Configuration Manager site version  

 - Support ID, also known as the hierarchy ID  

 - OS version and language for the system on which the console is running  

 - The exact location in the console from which you clicked the smile  

This data is consistent with the collection of our diagnostics and usage data. For more information, see [Diagnostics and usage data](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).



## Support Center
<!--1357489-->

Use Support Center for client troubleshooting, real-time log viewing, or capturing the state of a Configuration Manager client computer for later analysis. Support Center is a single tool to consolidate many administrator troubleshooting tools. A preview of the latest version of Support Center with bug fixes, improvements, and a preview of our new log viewer is available in the technical preview. Find the Support Center installer on the site server in the **cd.latest\SMSSETUP\Tools\SupportCenter** folder.

 > [!Tip]  
 > Legacy documentation for the existing functionality in Support Center is available on [TechNet](https://technet.microsoft.com/library/dn688621.aspx). Relevant information is in process to migrate to the docs.microsoft.com library.  

### New Support Center features  

 - A new log viewer, OneTrace. It works similar to CMTrace, and includes improvements such as a tabbed view and dockable windows.  

 - A new data collector feature gathers diagnostic logs from the local or a remote Configuration Manager client. It provides real-time diagnostic of inventory (replaces Client Spy), policy (replaces Policy Spy), and client cache.  



## Configuration Manager Toolkit
<!--1357145-->

The Configuration Manager server and client tools are now included with the technical preview. Find them in the **cd.latest\SMSSETUP\Tools** folder on the site server. No further installation required.

#### Server tools  

 - **DP Job Manager**: Troubleshoots content distribution jobs to distribution points  

 - **Collection Evaluation Viewer**: View collection evaluation details  

 - **Content Library Explorer**: View contents of the content library single instance store  

 - **Content Library Transfer**: Transfers content library between drives  

 - **Content Ownership Tool**: Changes ownership of orphaned packages. These packages exist in the site without an owning site server.  

 - **Role-based Administration and Auditing Tool**: Helps administrators audit roles configuration  

#### Client tools

 - **CMTrace**: View logs  

 - **Deployment Monitoring Tool**: Troubleshoot applications, updates, and baseline deployments  

 - **Policy Spy**: View policy assignments  

 - **Power Viewer Tool**: View status of power management feature  

 - **Send Schedule Tool**: Trigger schedules and evaluations of DCM baselines  

> [!Important]  
> [Support Center](#support-center) is recommended for most use cases, as it includes the same or improved functionality for the following tools:  
>  - Client Spy
>  - CMTrace<sup>1</sup> 
>  - Deployment Monitoring Tool
>  - Policy Spy
>  - Send Schedule Tool
> 
> <sup>1</sup> CMTrace doesn't depend upon .NET or Windows Presentation Foundation (WPF), so is still used in Windows PE boot images.



## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
