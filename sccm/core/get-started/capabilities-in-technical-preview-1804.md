---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: Learn about new features available in the Configuration Manager Technical Preview version 1804.
ms.date: 04/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Capabilities in Technical Preview 1804 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1804. You can install this version to update and add new capabilities to your technical preview site. 

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

### Known issues

If you attempt to send feedback from a device that isn't able to access the internet, the application may unexpectedly close. To send a smile or frown, make sure the device is able to access petrol.office.microsoft.com.



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

### Known issues
Some client and server tools may unexpectedly quit when launching. This issue is due to a missing file on the media. As a workaround, copy the **Microsoft.Diagnostics.Tracing.EventSource.dll** file from the AdminConsole\bin directory into both SMSSETUP\Tools\ClientTools and ServerTools directories. This file must be the same version as used by the Configuration Manager console. Other versions may not work. <!--513977-->



## Uninstall application on approval revocation
<!--1357891-->

The behavior has changed when you revoke approval for an application. Now when you deny the request for the application, the client uninstalls the application from the user's device. 

### Prerequisites
- Enable the feature **Approve application requests for users per device**.

### Try it out!
 Try to complete the tasks. Then send [Feedback](#bkmk_feedback) letting us know how it worked.

1. In the Configuration Manager console, deploy to a user an application that requires approval. On the **Deployment Settings** tab of the deployment, enable the option **An administrator must approve a request for this application on the device**.  

2. On the Configuration Manager client in Software Center, the user requests approval to install the application.  

3. In the Configuration Manager console, approve the request for this user to install the application on the device. Application approval requests are displayed in the **Software Library** workspace, under **Application Management**, in the **Approval Requests** node.  

4. On the client in Software Center, the user installs the application.  

5. In the Configuration Manager console, deny the user's request for the application on the device.  

### Known issues
- After the user installs the application on the client, update user policy. In Software Center, switch to the **Options** tab, expand **Computer maintenance** and click **Sync Policy**.<!--480609-->  

- The application catalog web service point must be HTTP. For more information, see [Known issues in this technical preview](#bkmk_appcathttps).<!--512637-->  



## Exclude Active Directory containers from discovery
<!--1358143-->
To reduce the number of discovered objects, you can now exclude specific containers from Active Directory system discovery. This feature is a result of your [UserVoice feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery).

### Try it out!
 Try to complete the tasks. Then send [Feedback](#bkmk_feedback) letting us know how it worked.

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Hierarchy Configuration** and select **Discovery Methods**. Select **Active Directory System Discovery** and click **Properties** in the ribbon.  

2. Click the New icon to specify a new Active Directory container.   

3. In the Active Directory Container dialog box, browse to or enter the **Path** in the Location section to start the discovery.  

4. In the Search Options section, enable the option to **Recursively search Active Directory child containers**. Then click **Add** to select subcontainers to be excluded from this discovery.  

5. In the Select New Container dialog box, select a child container to exclude. Click **OK** to close the Select New Container dialog box.  

6. Click **OK** to close the Active Directory Container dialog box.  

7. In the Active Directory System Discovery Properties window, see the path of the Active Directory container at which discovery starts. The **Recursive** column shows **Yes**, and the new **Has Exclusions** column also shows **Yes**. Click **OK** to close the Active Directory System Discovery Properties window.  



## Specify the visibility of the Application Catalog website link in Software Center
<!--1358214-->

You can now control whether the link to **Open the Application Catalog web site** appears in the **Installation status** node of Software Center.  

> [!Note]  
> Support for the Application Catalog website user experience ends with the first update released after June 1, 2018. For more information, see [Removed and deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

### Try it out!
 Try to complete the tasks. Then send [Feedback](#bkmk_feedback) letting us know how it worked.

1. In the Configuration Manager console, **Administration** workspace, **Client Settings** node, create a custom client device settings policy.  

2. Select the **Software Center** group.  

3. For **Software Center settings**, click **Customize**.  

4. Enable the option to **Hide the Application Catalog web site link in Software Center**.   

For more information on client settings, see [Configure client settings](/sccm/core/clients/deploy/configure-client-settings).




## Filter automatic deployment rules by software update architecture
 <!--1322266-->
You can now filter automatic deployment rules to exclude architectures like Itanium and ARM64.

### Try it out!
Try to complete the tasks. Then send [Feedback](#bkmk_feedback) letting us know how it worked.

1. In the Configuration Manager console, switch to the **Software Library** workspace. Expand **Software Updates** and select **Automatic Deployment Rules**. On the ribbon, select **Create Automatic Deployment Rule**.  

2. Fill in the appropriate settings for the **General** tab and the **Deployment Settings** tab.  

3. In the **Software Updates** tab, select **Architecture** then click on **items to find** in the **Search criteria**.  

4. Select the architectures you want to include in the automatic deployment rule.  

5. Click **Next** and proceed with the creation of the automatic deployment rule.  

> [!IMPORTANT]  
> Remember that there are 32-bit (x86) applications and components running on 64-bit (x64) systems. Unless you're certain that you don't need x86, enable it as well when you choose x64.  

### Known issues
After adding the architecture criteria, the automatic deployment rule properties page shows **Title** in the search criteria. The automatic deployment rule still functions as expected, and selects the correct software updates. However, you can’t include both **Architecture** and **Title** criteria at this time. <!--512634,512632-->



## Improvements to OS deployment
We made the following improvements to OS deployment, some of which were the result of your user voice feedback.  

 - [Mask sensitive data stored in task sequence variables](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): In the [Set Task Sequence Variable](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) step, select the new option to **Do not display this value**. For example, when specifying a password.<!--1358330--> The following behaviors apply when you enable this option:
   - The value of the variable isn't displayed in smsts.log.
   - The Configuration Manager console and SMS Provider handle this value the same as other secrets such as passwords.
   - The value isn't included when you export the task sequence.
   - The task sequence editor doesn't read this value when you edit the step. Retype the entire value to make changes.

   > [!Important]  
   > Variables and their values are saved with the task sequence as XML, and obfuscated in the database. When the client requests a task sequence policy from the management point, it is encrypted in transit and when stored on the client. However, all variable values are plain text in the task sequence environment in memory during runtime on the client. If the task sequence includes a step to output the value of the variable, this output is in plain text. This behavior requires an explicit action by the administrator to include such a step in the task sequence. 


 - [Mask program name during Run Command Step of a task sequence](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): To prevent potentially sensitive data from being displayed or logged, set the task sequence variable **OSDDoNotLogCommand** to `TRUE`. This variable masks the program name in the smsts.log during a [Run Command Line](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) task sequence step. <!--1358493-->  



## Improvements to the Configuration Manager console
- Primary user information is now visible when viewing the members of a collection under **Assets and Compliance**, **Device Collections**.<!--510252-->  



## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
