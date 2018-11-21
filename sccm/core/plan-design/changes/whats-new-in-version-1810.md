---
title: What's new in version 1810
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 1810 of Configuration Manager current branch.
ms.date: 11/16/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# What's new in version 1810 of Configuration Manager current branch

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1810 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1710, 1802, or 1806. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810). After you update a site, also review the [Post-update checklist](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist).

> [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 1810](https://support.microsoft.com/help/4459701).

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [PowerShell 1810 Release Notes](https://docs.microsoft.com/powershell/sccm/1810_release_notes?view=sccm-ps).

The following additional updates to this release are also now available:
- [Update rollup for Configuration Manager current branch, version 1810](https://support.microsoft.com/help/4462978)
-->

> [!Important]  
> To take advantage of new Configuration Manager features, first update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

This article summarizes the changes and new features in Configuration Manager, version 1810.  



## <a name="bkmk_deprecated"></a> Deprecated features and operating systems

Learn about support changes before they're implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Starting on August 14, 2018, the hybrid mobile device management feature is deprecated. For more information, see [What is hybrid MDM](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  

Support for System Center Endpoint Protection (SCEP) for Mac and Linux (all versions) ends on December 31, 2018. Availability of new virus definitions for SCEP for Mac and SCEP for Linux will be discontinued after the end of support. For more information, see [End of support blog post](https://go.microsoft.com/fwlink/?linkid=870182).
<!--
Version 1810 drops support for the following products:
-->



## <a name="bkmk_infra"></a> Site infrastructure

### Support for Windows Server 2019
<!--1359195-->
Configuration Manager now supports Windows Server 2019 and Windows Server, version 1809, as site systems. 

For more information, see [Supported operating systems for site system servers](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).


### Hierarchy support for site server high availability
<!--1358224-->
Central administration sites and child primary sites can now have an additional site server in passive mode. 

<!--For more information, see [Site server high availability](/sccm/core/servers/deploy/configure/site-server-high-availability).-->


### Improvements to setup prerequisites

When you install or update to version 1810, Configuration Manager setup now includes or improves the following prerequisite checks:

- **Pending system restart**: This prerequisite check is now more resilient. It checks additional registry keys for Windows features. For more information, see [Pending system restart](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#pending-system-restart). <!--SCCMDocs-pr issue 3010-->  

- **SQL change tracking cleanup**: A new check if the site database has a backlog of SQL change tracking data. For more information, including a procedure to verify and clear this backlog, see [SQL change tracking cleanup](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#bkmk_changetracking). <!--SCCMDocs-pr issue 3023-->  

<!-- - **SQL Native Client version**: This prerequisite check is updated for versions of SQL Native Client that support TLS 1.2. The minimum version is 11.4.7001.0. For more information, see [SQL Native Client version](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-native-client). <!--SCCMDocs-pr issue 3094->  
 -->
- **Site system on Windows cluster node**: The Configuration Manager setup process no longer blocks installation of the site server role on a computer with the Windows role for Failover Clustering. SQL Always On requires this role, so previously you couldn't colocate the site database on the site server. With this change, you can create a highly available site with fewer servers by using SQL Always On and a site server in passive mode. For more information, see [Windows Failover Cluster](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#windows-failover-cluster). <!--1359132-->  




### New permission for client notification actions
<!--SCCMDocs-pr issue #2972-->
Client notification actions now require the **Notify Resource** permission on the SMS_Collection class. The following built-in roles have this permission by default:
- Full Administrator  
- Infrastructure Administrator  

Add this permission to any custom roles that need to use client notification actions. 

For more information, see [Client notifications](/sccm/core/clients/manage/client-notification).



## <a name="bkmk_content"></a> Content management

### New boundary group options
<!--1358749-->
Boundary groups now include the following additional settings to give you more control over content distribution in your environment:

- **Prefer distribution points over peers with the same subnet**: By default, the management point prioritizes peer cache sources at the top of the list of content locations. This setting reverses that priority for clients that are in the same subnet as the peer cache source.  

- **Prefer cloud distribution points over distribution points**: If you have a branch office with a faster internet link, you can now prioritize cloud content.  

For more information, see [Boundary group options for peer downloads](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).


### Management insights rule for peer cache source client version
<!-- 1358008 -->
The **Management Insights** node has a new rule to identify clients that serve as a peer cache source but haven't upgraded from a pre-1806 client version. The new rule is **Upgrade peer cache sources to the latest version of the Configuration Manager client**, and is part of the new **Proactive Maintenance** rule group. Pre-1806 clients can't be used as a peer cache source for clients that run version 1806 or later. Select **Take action** to open a device view that displays the list of clients. 

For more information, see [Management insights](/sccm/core/servers/manage/management-insights).



## <a name="bkmk_client"></a> Client management

### New client notification action to wake up device
<!--1317364-->
You can now wake up clients from the Configuration Manager console, even if the client isn't on the same subnet as the site server. If you need to do maintenance or query devices, you're not limited by remote clients that are asleep. The site server uses the client notification channel to identify another client that's awake on the same remote subnet. The awake client then sends a wake on LAN request (magic packet).

<!--For more information, see [Plan how to wake up clients](/sccm/core/clients/deploy/plan/plan-wake-up-clients).-->


### Improvements to collection evaluation
<!--1358981-->
The following changes in collection evaluation behavior can improve site performance:  
 
- Previously, when you configured a schedule on a query-based collection, the site would continue to evaluate the query whether or not you enabled the collection setting to **Schedule a full update on this collection**. To fully disable the schedule, you had to change the schedule to **None**. Now the site clears the schedule when you disable this setting. To specify a schedule for collection evaluation, enable the option to **Schedule a full update on this collection**.  

- You can't disable the evaluation of built-in collections like **All Systems**, but now you can configure the schedule. This behavior allows you to customize this action at a time that meets your business requirements. 

<!--For more information, see [How to create collections](/sccm/core/clients/manage/collections/create-collections).-->


### Improvement to client installation
<!--1358840-->
When installing the Configuration Manager client, the ccmsetup process contacts the management point to locate the necessary content. Previously in this process the management point only returns distribution points in the client's current boundary group. If no content is available, the setup process falls back to download content from the management point. There's no option to fall back to distribution points in other boundary groups that might have the necessary content. Now the management point returns distribution points based on boundary group configuration. 

For more information, see [Configure boundary groups](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_ccmsetup).


### Improvements to internet-based client setup
<!--1359181-->
<!--move this under co-management?-->
This release further simplifies the Configuration Manager client setup process for clients on the internet. The site publishes additional Azure Active Directory (Azure AD) information to the cloud management gateway (CMG). An Azure AD-joined client gets this information from the CMG during the ccmsetup process, using the same tenant to which it's joined. This behavior further simplifies enrolling devices to co-management in an environment with more than one Azure AD tenant. Now the only two required ccmsetup properties are **CCMHOSTNAME** and **SMSSiteCode**.

<!--For more information, see [Prepare Windows 10 devices for co-management](https://docs.microsoft.com/en-us/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).-->



## <a name="bkmk_comgmt"></a> Co-management

### Required app compliance policy for co-managed devices
<!--1358196-->
Define compliance policy rules in Configuration Manager for required applications. This app assessment is part of the overall compliance state sent to Microsoft Intune for co-managed devices.

<!--For more information, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview).-->


### Improvement to co-management dashboard
<!--1358980-->
The co-management dashboard is enhanced with the following more detailed information:  

- The **Co-management enrollment status** tile includes additional states

- A new **Co-management status** tile with a funnel chart shows states of the enrollment process

- A new tile with counts of **Enrollment errors**

![Co-management dashboard screenshot showing the top four tiles](media/1358980-comgmt-dashboard.png)

For more information, see [Co-management dashboard](/sccm/core/clients/manage/co-management-dashboard).



<!-- ## <a name="bkmk_compliance"></a> Compliance settings -->



## <a name="bkmk_app"></a> Application management

### Convert applications to MSIX
<!--1359029-->
Starting in version 1806, Configuration Manager supports deployment of the new Windows 10 app package (.msix) format. Now you can convert your existing Windows Installer (.msi) applications to the MSIX format.

<!--For more information, see [Create Windows applications](/sccm/apps/get-started/creating-windows-applications#bkmk_general).  this might move to a new section for msix-->


### Repair applications
<!--1357866-->
Specify a repair command line for Windows Installer and Script Installer deployment types. Then if you enable the option on the deployment, a new button is available in Software Center to **Repair** the application. When you configure an application with a repair program, users can start the command from Software Center. 

For more information, see [Create applications](/sccm/apps/deploy-use/create-applications#bkmk_dt-content) and [Deploy applications](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy-settings).


### Approve application requests via email
<!--1321550-->
Configure email notifications for application approval requests. When a user requests an application, you receive an email. Click links in the email to approve or deny the request, without requiring the Configuration Manager console.

For more information, see [Approve applications](/sccm/apps/deploy-use/app-approval).


### Detection methods don't load Windows PowerShell profiles
<!--1359239-->
You can use Windows PowerShell scripts for detection methods on applications and in compliance settings. When these scripts run on clients, the Configuration Manager client now calls PowerShell with the `-NoProfile` parameter. This option starts PowerShell without profiles. 

A PowerShell profile is a script that runs when PowerShell starts. You can create a PowerShell profile to customize your environment and to add session-specific elements to every PowerShell session that you start. 

> [!Note]  
> This change in behavior doesn't apply to [Scripts](/sccm/apps/deploy-use/create-deploy-scripts).  

<!--For more information, see []().-->


## <a name="bkmk_osd"></a> OS deployment

### Task sequence support of Windows Autopilot for existing devices
<!--1358333-->

[Windows Autopilot for existing devices](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430), is now available with Windows 10 Insider Preview. This new feature allows you to reimage and provision a Windows 7 device for [Windows Autopilot user-driven mode](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) using a single, native Configuration Manager task sequence. 

<!--For more information, see []().--> 


### Specify the drive for offline OS image servicing  
<!--1358924-->
Now specify the drive that Configuration Manager uses when adding software updates to OS images and OS upgrade packages. This process can consume a large amount of disk space with temporary files, so this option gives you flexibility to select the drive to use. 

For more information, see [Manage OS images](/sccm/osd/get-started/manage-operating-system-images#bkmk_servicing-drive) or [Manage OS upgrade packages](/sccm/osd/get-started/manage-operating-system-upgrade-packages#bkmk_servicing-drive).


### Task sequence support for boundary groups
<!--1359025-->
When a device runs a task sequence and needs to acquire content, it now uses boundary group behaviors similar to the Configuration Manager client.   

For more information, see [Boundary groups](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd).


### Improvements to driver maintenance
<!--1358270-->
Driver packages now have additional metadata fields for **Manufacturer** and **Model**. Use these fields to tag driver packages with information to assist in general housekeeping, or to identify old and duplicate drivers that you can delete.


### New task sequence variable for last action name
<!--SCCMDocs-pr issue #2964-->
Along with the task sequence variable _SMSTSLastActionRetCode, the task sequence also sets a new variable **_SMSTSLastActionName**. It also logs this value to the smsts.log file. This new variable is beneficial when troubleshooting a task sequence. When a step fails, a custom script can include the step name along with the return code.

For more information, see [Task sequence variables](/sccm/osd/understand/task-sequence-variables#SMSTSLastActionName).



<!-- ## <a name="bkmk_userxp"></a> Software Center -->



## <a name="bkmk_sum"></a> Software updates

### Phased deployment of software updates
<!--1358146-->
Create phased deployments for software updates. Phased deployments allow you to orchestrate a coordinated, sequenced rollout of software based on customizable criteria and groups.

For more information, see [Create phased deployments](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).


### Improvement to maintenance windows for software updates
<!--vso2839307-->
The following client setting is in the **Software Updates** group to control the installation behavior of software updates in maintenance windows: 

**Enable installation of updates in "All deployments" maintenance window when "Software update" maintenance window is available**

By default, this option is **No** to keep consistent with the existing behavior. Change it to **Yes** to allow clients to use other available maintenance windows to install software updates.

<!--For more information, see []().-->



## <a name="bkmk_report"></a> Reporting

### Improvement to lifecycle dashboard
<!--1358702-->
The product lifecycle dashboard now includes information for **System Center 2012 Configuration Manager and later**. 

There's also a new report, **Lifecycle 05A - Product lifecycle dashboard**. It includes similar information as the in-console dashboard.

For more information on this dashboard, see [Use the Product Lifecycle dashboard](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard).


### Improvement to data warehouse
<!--1358870--> 
You can now synchronize more tables from the site database to the data warehouse. This change allows you to create more reports based on your business requirements.

For more information, see [Data warehouse](/sccm/core/servers/manage/data-warehouse).



<!-- ## <a name="bkmk_inv"></a> Inventory -->




<!-- ## <a name="bkmk_protect"></a> Protect devices-->




## <a name="bkmk_admin"></a> Configuration Manager console

### Configuration Manager administrator authentication
<!--1357013-->
You can now specify the minimum authentication level for administrators to access Configuration Manager sites. This feature enforces administrators to sign in to Windows with the required level. To configure this setting, find the **Authentication** tab in **Hierarchy Settings**. 

For more information, see [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth).


### Support Center
<!--1357489-->
Use Support Center for client troubleshooting, real-time log viewing, or capturing the state of a Configuration Manager client computer for later analysis. Support Center is a single tool to combine many administrator troubleshooting tools. Find the Support Center installer on the site server in the **cd.latest\SMSSETUP\Tools\SupportCenter** folder.

For more information, see [Support Center](/sccm/core/support/support-center).


### Management insights dashboard
<!--1357979-->

The **Management Insights** node now includes a graphical dashboard. This dashboard displays an overview of the rule states, which makes it easier for you to show your progress. The dashboard includes the following tiles:

- **Management insights index**: Tracks overall progress on management insights rules. The index is a weighted average. Critical rules are worth the most. This index gives the least weight to optional rules.  

- **Management insights groups**: Shows percent of rules in each group.  

- **Management insights priority**: Shows percent of rules by priority.  

- **All insights**: A table of insights including priority and state.  

![Screenshot of management insights dashboard](media/1357979-management-insights-dashboard.png)

For more information, see [Management insights](/sccm/core/servers/manage/management-insights).


### Improvements to CMPivot
<!--1359068-->
CMPivot includes the following improvements:

- Save **Favorite** queries  

- On the Query Summary tab, select the count of Failed or Offline devices, and then select the option to **Create Collection**. 

For more information on additional performance and troubleshooting improvements to CMPivot, see [Improvements to scripts](#bkmk_scripts).

<!--For more information on CMPivot, see [CMPivot](/sccm/core/servers/manage/cmpivot).-->


### <a name="bkmk_scripts"></a> Improvements to scripts
<!--1358239-->
You can now view detailed script output in raw or structured JSON format. This formatting makes the output easier to read and analyze. 

The following performance and troubleshooting improvements apply to both CMPivot and scripts:

- Updated clients return output less than 80 KB to the site over a fast communication channel. This change increases the performance of viewing script or query output.  

- Additional logs for troubleshooting  

<!--For more information, see the following articles:  

- [Create and run PowerShell scripts from the Configuration Manager console](/sccm/apps/deploy-use/create-deploy-scripts)  

- [CMPivot](/sccm/core/servers/manage/cmpivot)  -->


### SMS Provider API
<!--1321523-->
The SMS Provider now provides read-only API interoperability access to WMI over HTTPS. The **SMS Provider** appears as a role with an option to allow communication over the cloud management gateway. The current use for this setting is to enable application approvals via email from a remote device. For more information, see [Approve application requests via email](#approve-application-requests-via-email).



## <a name="bkmk_opmdm"></a> On-premises MDM

### An Intune connection is no longer required for on-premises MDM
<!--1359124-->
The on-premises MDM prerequisite to configure a Microsoft Intune subscription is no longer required. Your organization still requires Intune licenses to use this feature. 



## Next steps

When you're ready to install this version, see [Installing updates for Configuration Manager](/sccm/core/servers/manage/updates) and [Checklist for installing update 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810).

> [!TIP]  
> To install a new site, use a baseline version of Configuration Manager.  
>
>  Learn more about:    
>   - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

For known, significant issues, see the [Release notes](/sccm/core/servers/deploy/install/release-notes).

After you update a site, also review the [Post-update checklist](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist).
