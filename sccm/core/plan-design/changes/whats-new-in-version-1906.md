---
title: What's new in version 1906
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 1906 of Configuration Manager current branch.
ms.date: 07/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 97e23075-549c-4e45-ab1e-0671027edacf
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# What's new in version 1906 of Configuration Manager current branch

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1906 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1806, 1810, or 1902. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> This article summarizes the changes and new features in Configuration Manager, version 1906.  

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 1906](/sccm/core/servers/manage/checklist-for-installing-update-1906). After you update a site, also review the [Post-update checklist](/sccm/core/servers/manage/checklist-for-installing-update-1906#post-update-checklist).

To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

> [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  

> [!Tip]  
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1906+-+Configuration+Manager%22&locale=en-us`


## <a name="bkmk_deprecated"></a> Deprecated features and operating systems

Learn about support changes before they're implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1906 drops support for the following features:  

- Classic service deployment to Azure for cloud management gateway and cloud distribution point. For more information, see [Plan for CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).



## <a name="bkmk_infra"></a> Site infrastructure

### Site server maintenance task improvements
<!--3555894-->
Site server maintenance tasks can now be viewed and edited from their own tab on the details view of a site server. The new **Maintenance Tasks** tab gives you information such as:

- If the task is enabled
- The task schedule
- Last start time
- Last completion time
- If the task completed successfully

![New tab for maintenance tasks in the detail view of a site server](./media/3555894-maintenance-tasks.png)

<!-- For more information, see [Maintenance tasks](sccm/core/servers/manage/maintenance-tasks). -->

### Configuration Manager update database upgrade monitoring
<!--4200581-->
When applying a Configuration Manager update, you can now see the state of the **Upgrade ConfigMgr database** task in the  installation status window.

- If the database upgrade is blocked, then you'll be given the warning **In progress, needs attention**.
   - The cmupdate.log will log the program name and sessionid from SQL that is blocking the database upgrade.
- When the database upgrade is no longer blocked, the status will be reset to **In progress** or **Complete**.
   - When the database upgrade is blocked, a check is done every 5 minutes to see if it's still blocked.

   ![Database upgrade monitoring during installation](./media/4200581-database-upgrade-monitoring.png)

<!-- For more information, see [Install in-console updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_install). -->

### Management insights rule for NTLM fallback
<!--4572953-->

[Management insights](/sccm/core/servers/manage/management-insights) includes a new rule that detects if you enabled the less secure NTLM authentication fallback method for the site: **NTLM fallback is enabled**.

When using the client push method of installing the Configuration Manager client, the site can require Kerberos mutual authentication. This enhancement helps to secure the communication between the server and the client. 

<!--For more information, see [How to install clients with client push](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).-->

### Add a SQL AlwaysOn node
<!--3127336-->
You can now add a new secondary replica node to an existing SQL AlwaysOn availability group. Instead of a [manual process](/sccm/core/servers/deploy/configure/configure-aoag#add-or-remove-synchronous-replica-members), use Configuration Manager setup to make this change.

<!--For more information on Configuration Manager support for SQL AlwaysOn, see the following articles:

- [Prepare to use SQL Server Always On availability groups](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)
- [Configure SQL Server Always On availability groups](/sccm/core/servers/deploy/configure/configure-aoag)-->



## <a name="bkmk_cloud"></a> Cloud-attached management

### Cloud services cost estimator
<!--3555774-->

Some customers are concerned about the potential cost for attaching cloud services in Configuration Manager. This release introduces a new cost estimator tool in the Configuration Manager console. The tool uses the following data from your site database to estimate the cost of deploying the cloud management gateway:  

- Aggregate, average client usage of management points and distribution points  

- Azure pricing  

In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Cloud Management** node.  

![Screenshot of cloud services usage estimation tool](./media/3555774-cmg-cost-estimator.png)

<!-- (New article) For more information, see [Planning for cloud usage](/sccm/core/clients/manage/cmg/plan-for-cloud-cost). -->

### Azure Active Directory user group discovery
<!--3611956-->

You can now discover user groups and members of those groups from Azure Active directory (Azure AD). Users found in Azure AD groups that haven't been previously discovered will be added as user resources in Configuration Manager. A user group resource record is created when the group is a security group.

<!-- For more information, see [Configure discovery methods](/sccm/core/servers/deploy/configure/configure-discovery-methods). -->


### Synchronize collection membership results to Azure Active Directory groups
<!--3607475-->

You can now enable the synchronization of collection memberships to an Azure Active Directory (Azure AD) group. This synchronization allows you to use your existing on premises grouping rules in the cloud. You can synchronize device collections. Only Azure AD-joined devices are synchronized to Azure AD.

The Azure AD synchronization is a one-way process, from Configuration Manager to Azure AD. Changes made in Azure AD aren't reflected in Configuration Manager collections, but aren't overwritten by Configuration Manager. For example, if the Configuration Manager collection has two devices, and the Azure AD group has three different devices, after synchronization the Azure AD group has five devices.

<!-- ? For more information, see [About discovery methods](/sccm/core/servers/deploy/configure/about-discovery-methods). -->

<!--COMMENTING OUT DA FOR RIGHT NOW SINCE IT IS NOT ON TAP Feature list

## <a name="bkmk_da"></a> Desktop Analytics

### DALogsCollector tool
<!--4622989--

The DALogsCollector tool is now included in the Configuration Manager media.

<!-- ? For more information, see [Configuration Manager Tools](/sccm/core/support/tools). 

### Changing the Desktop Analytics limiting collection on existing deployments
<!--3218073--

TBD

-->


## <a name="bkmk_real"></a> Real-time management

### CMPivot standalone
<!--3555890, 4619340, 4683130 -->
You can now use CMPivot as a standalone app. Run it outside of the Configuration Manager console to view the real-time state of devices in your environment. This change enables you to use CMPivot on a device without first installing the console.

You can now share the power of CMPivot with other personas, such as helpdesk or security admins, who don’t have the console installed on their computer. These other personas can use CMPivot to query Configuration Manager alongside the other tools that they traditionally use. By sharing this rich management data, you can work together to proactively solve business problems that cross roles.

<!-- For more information, see [CMPivot](/sccm/core/servers/manage/cmpivot#prerequisites). -->

#### Added CMPivot permissions to the Security Administrator role
<!--4683130-->

The following permissions have been added to Configuration Manager's built-in **Security Administrator** role:
 - Read on SMS Script
 - Run CMPivot on Collection
 - Read on Inventory Report

<!-- For more information, see [CMPivot](/sccm/core/servers/manage/cmpivot#prerequisites). -->

### Improvements to CMPivot
<!--4054074-->

#### Add joins, additional operators and aggregators in CMPivot
<!--4054074-->

 For CMPivot, you now have additional arithmetic operators, aggregators, and the ability to add query joins such as using Registry and File together. 

<!-- For more information, see [CMPivot](/sccm/core/servers/manage/cmpivot#prerequisites). -->


## <a name="bkmk_content"></a> Content management

### Delivery Optimization download data in client data sources dashboard
<!--3555759-->

The [Client data sources](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) dashboard now includes [Delivery Optimization](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization) data. This dashboard helps you understand from where clients are getting content in your environment.

For example, the Client Content Sources tile displays the source from which clients got content:

![Client Content Sources tile on the dashboard](./media/3555759-do-source.png)

<!--For more information, see [Manage Express installation files for Windows 10 updates](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).-->

### Use your distribution point as an in-network cache server for Delivery Optimization
<!--3555764-->

You can now install Delivery Optimization In-Network Cache server on your distribution points. By caching this content on-premises, your clients can benefit from the Delivery Optimization feature, but you can help to protect WAN links. 

This cache server acts as an on-demand transparent cache for content downloaded by Delivery Optimization. Use client settings to make sure this server is offered only to the members of the local Configuration Manager boundary group. 

This cache is separate from Configuration Manager's distribution point content. If you choose the same drive as the distribution point role, it stores content separately. 

> [!Note]  
> Delivery Optimization In-Network Cache server is a Windows Server feature that's still in development. It's tagged with a "beta" label in the Configuration Manager console.  

<!-- (new article and new section) For more information, see [Delivery Optimization In Network Cache (DOINC)](/sccm/core/plan-design/hierarchy/doinc) and [Content management delivery optimization](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization).-->

## <a name="bkmk_client"></a> Client management

### Support for Windows Virtual Desktop
<!--3556025-->
[Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) is a preview feature of Microsoft Azure and Microsoft 365. You can now use Configuration Manager technical preview to manage these virtual devices running Windows in Azure.

Similar to a terminal server, these virtual devices allow multiple concurrent active user sessions. To help with client performance, Configuration Manager now disables user policies on any device that allows these multiple user sessions. Even if you enable user policies, the client disables them by default on these devices, which include Windows Virtual Desktop and terminal servers.

The client only disables user policy when it detects this type of device during a new installation. For an existing client of this type that you update to this version, the previous behavior persists. On an existing device, it configures the user policy setting even if it detects that the device allows multiple user sessions.

If you require user policy in this scenario, and accept any potential performance impact, use the Configuration Manager SDK with the [SMS_PolicyAgentConfig server WMI class](/sccm/develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class). Set the new `PolicyEnableUserPolicyOnTS` property to `true`.

<!-- For more information, see [Supported OS versions for clients and devices](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices). -->

### OneTrace (Preview)
<!--3555962-->
OneTrace is a new log viewer with Support Center. It works similarly to CMTrace, with the following improvements:

- A tabbed view
- Dockable windows
- Improved search capabilities
- Ability to enable filters without leaving the log view
- Scrollbar hints to quickly identify clusters of errors
- Fast log opening for large files

![Screenshot of OneTrace log viewer](./media/3555962-onetrace.png)

OneTrace works with many types of log files, such as:

- Configuration Manager client logs
- Configuration Manager server logs
- Status messages
- Windows Update ETW log file on Windows 10
- Windows Update log file on Windows 7 & Windows 8.1

<!-- For more information, see [Configuration Manager tools](/sccm/core/support/tools). -->

<!-- Commenting out item for now since it isn't in the TAP feature list 

### 1906 client won't install on legacy OS (SHA-1)
<!--4222696-->

### Configure client cache minimum retention period
<!--4485509-->

You can now specify the minimum time for the Configuration Manager client to keep cached content. This client setting controls how long the client stores content in the cache before deleting it.

In the **Client Cache settings** group of client settings, configure the following setting: **Minimum duration before cached content can be removed (minutes)**. By default this value is 1,440 minutes (24 hours).

This setting gives you greater control over the client cache on different types of devices. You might reduce the value on clients that have small hard drives and don't need to keep existing content before another deployment runs.

> [!Note]  
> In the same client setting group, the existing setting to **Enable Configuration Manager client in full OS to share content** is now renamed to **Enable as peer cache source**. The behavior of the setting doesn't change.  

<!-- For more information, see [Client cache settings](/sccm/core/clients/deploy/about-client-settings#client-cache-settings). -->


## <a name="bkmk_comgmt"></a> Co-management

### Improvements to co-management auto-enrollment
<!--3555961-->

### Multiple pilot groups for co-management workloads
<!--3555750-->
You can now configure different pilot collections for each of the co-management workloads. Being able to use different pilot collections allows you to take a more  granular approach when shifting workloads. 

- In the **Enablement** tab, you can now specify an **Intune Auto Enrollment** collection. 
    - The **Intune Auto Enrollment** collection should contain all of the clients you want to onboard into co-management. It's essentially a superset of all the other staging collections.

  ![Co-management Enablement tab with Intune Auto Enrollment collection](./media/3555750-co-management-enablement-tab.png)

- The **Workloads** tab hasn't changed and you can still choose which workloads to transition.

  ![Co-management Workloads tab hasn't changed](./media/3555750-co-management-workloads-tab.png)

- In the **Staging** tab, instead of using one pilot collection for all workloads, you can now choose an individual collection for each workload.

    ![Co-management Staging tab allows you to choose a collection for each workload](./media/3555750-co-management-staging-tab.png)
  
These options are also available when you first [enable co-management](/sccm/comanage/how-to-enable.md).

<!-- For more information, see [Enable co-management](/sccm/comanage/how-to-enable.md). -->

### Co-management support for government cloud
<!--4075452-->



<!-- ## <a name="bkmk_compliance"></a> Compliance settings -->




## <a name="bkmk_app"></a> Application management

### Filter applications deployed to devices
<!--4451056-->
 User categories for device-targeted application deployments now show as filters in Software Center. Specify a **user category** for an application on the **Software Center** page of its properties. Then open the app in Software Center and look at the available filters.

<!--For more information, see [Manually specify application information](/sccm/apps/deploy-use/create-applications#bkmk_manual-app) and [Applications in Software Center](/sccm/core/understand/software-center#applications).-->


### Application groups
<!--3555907-->
Create a group of applications that you can send to a user or device collection as a single deployment. The metadata you specify about the app group is seen in Software Center as a single entity. You can order the apps in the group so that the client installs them in a specific order.

<!--For more information, see [Create application group](/sccm/apps/deploy-use/create-app-group)and [Create application group](/sccm/apps/deploy-use/deploy-applications).-->

### Retry the install of pre-approved applications
<!--4336307-->

You can now retry the installation of an app that you previously approved for a user or device. The approval option is only for available deployments. If the user uninstalls the app, or if the initial install process fails, Configuration Manager doesn't reevaluate its state and reinstall it. This feature allows a support technician to quickly retry the app install for a user that calls for help.
This is part of an [optional feature](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) called **Approve application requests for users per device**


<!--For more information, see [Approve applications](/sccm/apps/deploy-use/create-app-group).-->

### Install an application for a device
<!--4402180-->
From the Configuration Manager console, you can now install applications to a device in real time. This feature can help reduce the need for separate collections for every application. This is an [optional feature](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) called **Approve application requests for users per device**.  

<!--For more information, see [Install applications for a device](/sccm/apps/deploy-use/install-app-for-device).-->


### Improvements to app approvals
<!--4224910-->

This release includes the following improvements to app approvals:

> [!Note]  
> These improvements refer to the [optional feature](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Approve application requests for users per device**.  

- If you approve an app request in the console, and then deny it, you can now approve it again. The app is reinstalled on the client after you approve it.  

- There's a new WMI method, **DeleteInstance** to remove an app approval request. This action doesn't uninstall the app on the device. If it's not already installed, the user can't install the app from Software Center. The version 1810 blog post below includes a PowerShell script sample that you can adjust for use with this API.  

- Call the **CreateApprovedRequest** API to create a pre-approved request for an app on a device. To prevent automatically installing the app on the client, set the **AutoInstall** parameter to `FALSE`. The user sees the app in Software Center, but it's not automatically installed.

 <!--For more information, see [Approve applications](/sccm/apps/deploy-use/app-approval).-->




## <a name="bkmk_osd"></a> OS deployment

### Task sequence debugger
<!--3612274-->

### Improvements to driver management
<!--3555958-->

### Clear app content from client cache during task sequence
<!--4485675-->

### Reclaim SEDO lock for task sequences
<!--3699337-->

### Pre-cache driver packages and OS images
<!--4224642-->

### Improvement to task sequence media creation
<!--4090666-->

### Improvements to OS deployment 
<!--2839943,4447680-->
<!--4512937,4224642-->
<!--4668846, 2840337, 4512937-->



## <a name="bkmk_userxp"></a> Software Center

### Improvements to Software Center tab customizations
<!--4063773-->

### Software Center infrastructure improvements
<!--3555950-->

### Redesigned notification for newly available software
<!--3555904-->

### More frequent countdown notifications for restarts
<!--3976435-->

### Direct link to custom tabs in Software Center
<!--4655176-->



## <a name="bkmk_sum"></a> Software updates

### Additional options for WSUS maintenance
<!--4110109-->

### Configure the default maximum run time for software updates
<!--3734426-->

### Configure dynamic update during feature updates
<!--4062619-->

### New Windows 10, version 1903 and later product category
<!--4682946-->

### Drill through required updates
<!--4224414-->



## <a name="bkmk_o365"></a> Office management

### Office 365 ProPlus upgrade readiness dashboard
<!--4021125-->



## <a name="bkmk_inv"></a> Inventory

### Improvement to Asset Intelligence
<!--4586547-->



<!-- ## <a name="bkmk_pod"></a> Phased deployments -->




## <a name="bkmk_protect"></a> Protection

### Windows Defender Application Guard file trust criteria
<!--3555858-->




## <a name="bkmk_admin"></a> Configuration Manager console

### Add SMBIOS GUID column to device and device collection nodes
<!--4526580-->

### RBAC on folders
<!--3600867-->

### Administration service support for security nodes
<!--4223683-->



<!--
## Other updates

Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4498910).

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [PowerShell version 1906 release notes](https://docs.microsoft.com/powershell/sccm/1906-release-notes?view=sccm-ps).

The following update rollup (4486457) is available in the console starting on 25 January 2019: [Update rollup for Configuration Manager current branch, version 1902](https://support.microsoft.com/help/4486457).

### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](/sccm/core/servers/manage/updates#bkmk_supersede).
-->


## Next steps

When you're ready to install this version, see [Installing updates for Configuration Manager](/sccm/core/servers/manage/updates) and [Checklist for installing update 1906](/sccm/core/servers/manage/checklist-for-installing-update-1906).

> [!TIP]  
> To install a new site, use a baseline version of Configuration Manager.  
>
> Learn more about:
>
> - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites)  
> - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

For known, significant issues, see the [Release notes](/sccm/core/servers/deploy/install/release-notes).

After you update a site, also review the [Post-update checklist](/sccm/core/servers/manage/checklist-for-installing-update-1906#post-update-checklist).
