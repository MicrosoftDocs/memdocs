---
title: What's new in version 1806
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 1806 of Configuration Manager current branch.
ms.date: 10/26/2018
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

# What's new in version 1806 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 1806 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1706, 1710, or 1802. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 1806](../../servers/manage/checklist-for-installing-update-1806.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).

<!--
> [!Important]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
-->

The following sections provide details about the changes and new features in version 1806 of Configuration Manager current branch.  



## Deprecated features and operating systems

Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

As of August 14, 2018, the hybrid mobile device management feature is deprecated. For more information, see [What happened to hybrid MDM](../../../mdm/understand/what-happened-to-hybrid.md).<!--Intune feature 2683117-->  

<!--
Version 1806 drops support for the following products:
-->



## Site infrastructure

### CMPivot
<!--1358456-->
Configuration Manager has always provided a large centralized store of device data, which customers use for reporting purposes. The site typically collects this data on a weekly basis. CMPivot is a new in-console utility that now provides access to real-time state of devices in your environment. It immediately runs a query on all currently connected devices in the target collection and returns the results. You can then filter and group this data in the tool. By providing real-time data from online clients, you can more quickly answer business questions, troubleshoot issues, and respond to security incidents. 

For more information, see [CMPivot](../../servers/manage/cmpivot.md).  


### Site server high availability
<!--1128774-->
High availability for a standalone primary site server role is a Configuration Manager-based solution to install an additional site server in passive mode. The site server in passive mode is in addition to your existing site server that is in active mode. A site server in passive mode is available for immediate use, when needed. 

For more information, see the following articles: 
- [Site server high availability](../../servers/deploy/configure/site-server-high-availability.md) 
- [Flowchart - Set up a site server in passive mode](../../servers/deploy/configure/passive-site-server-flowchart.md)
- [Flowchart - Promote site server (planned)](../../servers/deploy/configure/promote-site-server-flowchart.md)
- [Flowchart - Promote site server (unplanned)](../../servers/deploy/configure/promote-site-server-unplanned-flowchart.md)


### Improvements to management insights
This release includes the following improvements to management insights:  

- Some management insights now have the option to take an action. This action is either navigating to the associated node in the console, or showing a filtered, query-based view.<!--1357930-->  

- A new group for Proactive Maintenance is available with six new rules, which help highlight potential configuration issues to avoid through regular upkeep.<!--1352184-->  

For more information, see [Management insights](../../servers/manage/management-insights.md).


### Configuration Manager tools
<!--1357145-->
The Configuration Manager server and client tools are now included on the server. Find them in the `CD.Latest\SMSSETUP\Tools` folder on the site server. No further installation required. 

For more information, see [Configuration Manager tools](../../support/tools.md).


### Exclude Active Directory containers from discovery
<!--1358143-->
To reduce the number of discovered objects, exclude specific containers from Active Directory system discovery. 

For more information, see [Configure Active Directory System Discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_config-adsd).



## Content management

### Configure a remote content library for the site server
<!--1357525-->
To configure site server high availability or to free up hard drive space on your central administration or primary site servers, relocate the content library to another storage location. Move the content library to another drive on the site server, a separate server, or fault-tolerant disks in a storage area network (SAN). 

For more information, see the following articles: 
- [The content library](../hierarchy/the-content-library.md)
- [Flowchart - Manage content library](../hierarchy/manage-content-library-flowchart.md)


### Cloud distribution point support for Azure Resource Manager
<!--1322209-->
When creating a cloud distribution point, the wizard now provides the option to create an **Azure Resource Manager deployment**. Azure Resource Manager is a modern platform for managing all solution resources as a single entity, called a resource group. When deploying a cloud distribution point with Azure Resource Manager, the site uses Azure Active Directory to authenticate and create the necessary cloud resources. This modernized deployment doesn't require the classic Azure management certificate. 

The feature documentation for the cloud distribution point is also revised and enhanced. For more information, see the following articles:
- [Use a cloud distribution point](../hierarchy/use-a-cloud-based-distribution-point.md)   
- [Install a cloud distribution point](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  


### Pull-distribution points support cloud distribution points as source  
<!--1321554-->
Many customers use pull-distribution points in remote or branch offices, which download content from a source distribution point across the WAN. If your remote offices have a better connection to the internet, or to reduce load on your WAN links, you can now use a cloud distribution point in Microsoft Azure as the source. When you add a source on the **Pull Distribution Point** tab of the distribution point properties, any cloud distribution point in the site is now listed as an available distribution point. The behavior of both site system roles remains the same otherwise. 

For more information, see [Use a pull-distribution points](../hierarchy/use-a-pull-distribution-point.md).


### Enable distribution points to use network congestion control
<!--1358112-->
Windows Low Extra Delay Background Transport (LEDBAT) is a feature of Windows Server to help manage background network transfers. For distribution points running on supported versions of Windows Server, enable an option to help adjust network traffic. Clients only use network bandwidth when it's available. 

For more information, see [Windows LEDBAT](../hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat).


### Partial download support in client peer cache to reduce WAN utilization
<!--1357346-->
Client peer cache sources can now divide content into parts. These parts minimize the network transfer to reduce WAN utilization. The management point provides more detailed tracking of the content parts. It tries to eliminate more than one download of the same content per boundary group. 

For more information, see [Partial download support](../hierarchy/client-peer-cache.md#partial-download-support). 


### Boundary group options for peer downloads
<!--1356193-->
Boundary groups now include additional settings to give you more control over content distribution in your environment. This release adds the following options:  

- **Allow peer downloads in this boundary group**: The management point provides clients a list of content locations that includes peer sources. This setting also affects applying Group IDs for Delivery Optimization.  

- **During peer downloads, only use peers within the same subnet**: The management point only includes in the content location list peer sources that are in the same subnet as the client.  

For more information, see [Boundary group options for peer downloads](../../servers/deploy/configure/boundary-group-options.md).


### Improvement to peer cache source location status
<!--SCCMDocs issue 850-->
Configuration Manager is more efficient at determining if a peer cache source has roamed to another location. This behavior makes sure the management point offers it as a content source to clients in the new location and not the old location. If you're using the peer cache feature with roaming peer cache sources, after updating the site to version 1806, also update all peer cache sources to the latest client version. The management point doesn't include these peer cache sources in the list of content locations until they are updated to at least version 1806.

For more information, see [Requirements for peer cache](../hierarchy/client-peer-cache.md#requirements).



<!-- ## Migration  -->



## Client management

### Improvement to client push security
<!--1358204-->
When using the client push method of installing the Configuration Manager client, the site can now require Kerberos mutual authentication. This enhancement helps to secure the communication between the server and the client. 

For more information, see [How to install clients with client push](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).


### <a name="bkmk_ehttp"></a> Enhanced HTTP site system
<!--1356889,1358228-->
Using HTTPS communication is recommended for all Configuration Manager communication paths, but can be challenging for some customers due to the overhead of managing PKI certificates.

This release includes improvements to how clients communicate with site systems. On the site properties, **Client Computer Communication** tab, select the option for **HTTPS or HTTP**, and then enable the new option to **Use Configuration Manager-generated certificates for HTTP site systems**. This feature is a [pre-release feature](../../servers/manage/pre-release-features.md).

For more information, see [Enhanced HTTP](../hierarchy/enhanced-http.md).


### Azure AD device identity 
<!--1358460-->
An [Azure AD-joined](/azure/active-directory/devices/concept-azure-ad-join) or [hybrid Azure AD device](/azure/active-directory/devices/concept-azure-ad-join-hybrid) without an Azure AD user signed in can securely communicate with its assigned site. The cloud-based device identity is now sufficient to authenticate with the CMG and management point.  

For more information, see [Enhanced HTTP](../hierarchy/enhanced-http.md).


### CMTrace installed with client
<!--1357971-->
The CMTrace log viewing tool is now automatically installed along with the Configuration Manager client. It's added to the client installation directory, which by default is `%WinDir%\ccm\cmtrace.exe`. 

For more information, see [CMTrace](../../support/cmtrace.md).


### Cloud management dashboard
<!--1358461-->
The new cloud management dashboard provides a centralized view for cloud management gateway (CMG) usage. When the site is onboarded with Azure AD, it also displays data about cloud users and devices.   

This feature also includes the **CMG connection analyzer** for real-time verification to aid troubleshooting. The in-console utility checks the current status of the service, and the communication channel through the CMG connection point to any management points that allow CMG traffic. 

For more information, see the following sections of the [Monitor CMG](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md) article:  
- [Cloud management dashboard](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#cloud-management-dashboard)  
- [Connection analyzer](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#connection-analyzer)  


### Improvements to cloud management gateway

Version 1806 includes the following improvements to the cloud management gateway (CMG):

#### Simplified client bootstrap command line
<!--1358215-->
When installing the Configuration Manager client on the internet via a CMG, the command-line now requires fewer properties. This improvement reduces the size of the command line used in Microsoft Intune when preparing for co-management. 

For more information, see [How to prepare internet-based devices for co-management](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).

#### Download content from a CMG
<!--1358651-->
Previously, you had to deploy a cloud distribution point and CMG as separate roles. A CMG can now also serve content to clients. This functionality reduces the required certificates and cost of Azure VMs. 

For more information, see [Modify a CMG](../../clients/manage/cmg/modify-cloud-management-gateway.md).

#### Trusted root certificate isn't required with Azure AD
<!--503899-->
When you create a CMG, you're no longer required to provide a [trusted root certificate](../../clients/manage/cmg/server-auth-cert.md) on the Settings page. This certificate isn't required when using Azure Active Directory (Azure AD) for client authentication, but used to be required in the wizard. If you're using PKI client authentication certificates, then you still must add a trusted root certificate to the CMG.



## Co-management

### Sync MDM policy from Microsoft Intune for a co-managed device
<!--1357377-->
When you switch a co-management workload, the co-managed devices automatically synchronize MDM policy from Microsoft Intune. This sync also happens when you initiate the **Download Computer Policy** action from Client Notifications in the Configuration Manager console. 

For more information, see [How to switch Configuration Manager workloads to Intune](../../../comanage/how-to-switch-workloads.md).


### Transition new workloads to Intune using co-management
The following workloads are now able to transition from Configuration Manager to Intune after enabling co-management:  

- **Device configuration**<!--1357903-->: This workload lets you use Intune to deploy MDM policies, while continuing to use Configuration Manager for deploying applications.  

- **Office 365**<!--1357841-->: Devices don't install Microsoft 365 deployments from Configuration Manager.  

- **Mobile apps**<!--1357892-->: Any available apps deployed from Intune are available in the Company Portal. Apps that you deploy from Configuration Manager are available in Software Center. This feature is a [pre-release feature](../../servers/manage/pre-release-features.md).  

To transition these workloads, go to the co-management properties page and move the workload slider bar from Configuration Manager to **Pilot** or **All**. 

For more information, see [Co-management for Windows 10 devices](../../../comanage/overview.md).


### Support for multiple hierarchies to one Intune tenant
<!--1357944-->
Some customers have several Configuration Manager hierarchies and want to consolidate in the future to a single tenant for Azure Active Directory and Microsoft Intune. Co-management now supports connecting more than one Configuration Manager environment to the same Intune tenant.

For more information, see [Co-management prerequisites](../../../comanage/overview.md#prerequisites).
 


## Compliance settings

### Configure Windows Defender SmartScreen settings for Microsoft Edge
<!--1353701-->
The Microsoft Edge browser compliance settings policy adds the following three settings for Windows Defender SmartScreen: 
- Allow SmartScreen
- Users can override SmartScreen prompt for sites
- Users can override SmartScreen prompt for files

For more information, see [Configure Microsoft Edge settings](../../../compliance/deploy-use/browser-profiles.md).


### SCAP extensions
<!--1357552-->
Convert Security Content Automation Protocol (SCAP) content to compliance settings baselines and generate SCAP reports using a console extension. This feature also includes a new dashboard to visualize the client compliance as well as XCCDF rule compliance. 





## Application management

### Phased deployment of applications
<!--1358147-->
Create a phased deployment for an application. Phased deployments allow you to orchestrate a coordinated, sequenced rollout of software based on customizable criteria and groups. For example, deploy the application to a pilot collection, and then automatically continue the rollout based on success criteria. 

For more information, see the following articles:  

- [Create a phased deployment](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  

- [Manage and monitor phased deployments](../../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  


### Provision Windows app packages for all users on a device
<!--1358310-->
Provision an application with a Windows app package for all users on the device. One common example of this scenario is provisioning an app from the Microsoft Store for Business and Education, like Minecraft: Education Edition, to all devices used by students in a school. Previously, Configuration Manager only supported installing these applications per user. After signing in to a new device, a student would have to wait to access an app. Now when the app is provisioned to the device for all users, they can be productive more quickly. 

For more information, see [Create Windows applications](../../../apps/get-started/creating-windows-applications.md#bkmk_provision).


### Office Customization Tool integration with the Office 365 Installer
<!--1358149-->
The Office Customization Tool is now integrated with the Office 365 Installer in the Configuration Manager console. When creating a deployment for Microsoft 365, dynamically configure the latest Office manageability settings. Microsoft updates the Office Customization Tool when they release new builds of Microsoft 365. This integration allows you to take advantage of new manageability settings in Microsoft 365 as soon as they're available. 

For more information, see [Deploy Microsoft 365 apps](../../../sum/deploy-use/manage-office-365-proplus-updates.md).


### Support for new Windows app package formats
<!--1357427-->
Configuration Manager now supports the deployment of new Windows 10 app package (.msix) and app bundle (.msixbundle) formats. 

For more information, see [Create Windows applications](../../../apps/get-started/creating-windows-applications.md#bkmk_msix).


### Uninstall application on approval revocation
<!--1357891-->
The behavior has changed when you revoke approval for an application. Now when you deny the request for the application, the client uninstalls the application from the user's device. This behavior requires that you enable the [optional feature](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Approve application requests for users per device**. 

For more information, see [Deploy applications](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).


### Package Conversion Manager 
<!--1357861-->
Package Conversion Manager is now an integrated tool that allows you to convert legacy packages into Configuration Manager current branch applications. Then you can use features of applications such as dependencies, requirement rules, and user device affinity.

For more information, see [Package Conversion Manager](../../../apps/pcm/package-conversion-manager.md).



## OS deployment

### Improvements to phased deployments

This release includes the following improvements to phased deployments:  

#### Create a phased deployment with manually configured phases
<!--1358148-->
For a task sequence, now manually configure the phases when you create a phased deployment. Add up to 10 additional phases from the **Phases** tab of the Create Phased Deployment wizard. You can still automatically create a default two-phase deployment. 

For more information, see [Create a phased deployment with manually configured phases](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_manual).

#### Phased deployment status
<!--1358577-->
Phased deployments now have a native monitoring experience. From the **Deployments** node in the **Monitoring** workspace, select a phased deployment, and then click **Phased Deployment Status** in the ribbon. 

For more information, see [Manage and monitor phased deployments](../../../osd/deploy-use/manage-monitor-phased-deployments.md).  

#### Gradual rollout during phased deployments
<!--1358578-->
During a phased deployment, the rollout in each phase can now happen gradually. This behavior helps mitigate the risk of deployment issues, and decreases the load on the network caused by the distribution of content to clients. The site can gradually make the software available depending on the configuration for each phase. Every client in a phase has a deadline relative to the time the software is made available. The time window between the available time and deadline is the same for all clients in a phase. 

For more information, see [Phase settings](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_settings).  


### Improvements to Windows 10 in-place upgrade task sequence
<!--1358500-->
The default task sequence template for Windows 10 in-place upgrade now includes another new group with recommended actions to add in case the upgrade process fails. These actions make it easier to troubleshoot. One such tool is Windows [SetupDiag](/windows/deployment/upgrade/setupdiag). It's a standalone diagnostic tool to obtain details about why a Windows 10 upgrade was unsuccessful. 

For more information, see [In-place upgrade recommendations](../../../osd/understand/in-place-upgrade-recommendations.md#run-actions-on-failure).


### Improvements to PXE-enabled distribution points
<!--1357580-->
On the **PXE** tab of the distribution point properties, check **Enable a PXE responder without Windows Deployment Service**. This new option enables a PXE responder on the distribution point, which doesn't require Windows Deployment Services (WDS). Because WDS isn't required, the PXE-enabled distribution point can be a client or server OS, including Windows Server Core. This new PXE responder service supports IPv6, and also enhances the flexibility of PXE-enabled distribution points in remote offices. 

For more information, see [enable PXE on the distribution point](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### Network access account not required for some scenarios
<!--1358278,1358279-->
The [Enhanced HTTP site system](#bkmk_ehttp) feature also removes some dependencies on the network access account. When you enable the new site option to **Use Configuration Manager-generated certificates for HTTP site systems**, the following scenarios don't require a network access account to download content from a distribution point:  

- Task sequences running from boot media or PXE
- Task sequences running from Software Center  

These task sequences can be for OS deployment or custom. It's also supported for workgroup computers.

For more information, see [Task sequences and the network access account](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#task-sequences-and-the-network-access-account).


### Other improvements to OS deployment

#### Mask sensitive data stored in task sequence variables
 <!--1358330-->
 In the **Set Task Sequence Variable** step, select the new option to **Do not display this value**. 

 For more information, see [Set Task Sequence Variable](../../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable). 

#### Mask program name during Run Command Step of a task sequence
 <!--1358493-->
 To prevent potentially sensitive data from being displayed or logged, configure the task sequence variable **OSDDoNotLogCommand**.  

 For more information, see [Task sequence variables](../../../osd/understand/task-sequence-variables.md#OSDDoNotLogCommand). 

#### Task sequence variable for DISM parameters when installing drivers
 <!--516679/2840016-->
 To specify additional command-line parameters for DISM, use the new task sequence variable **OSDInstallDriversAdditionalOptions**. 

 For more information, see [Task sequence variables](../../../osd/understand/task-sequence-variables.md#OSDInstallDriversAdditionalOptions). 

#### Option to use full disk encryption
 <!--SCCMDocs-pr issue 2671-->
 Both the **Enable BitLocker** and **Pre-provision BitLocker** steps now include an option to **Use full disk encryption**. By default, these steps encrypt used space on the drive. This default behavior is recommended, as it's faster and more efficient. 

 For more information see [Enable BitLocker](../../../osd/understand/task-sequence-steps.md#enable-bitlocker) and [Pre-provision BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker). 

#### Client provisioning mode isn't enabled with Windows 10 upgrade compatibility scan
 <!--SCCMDocs-pr issue 2812-->
 Now when you enable the option to **Perform Windows Setup compatibility scan without starting upgrade**, the **Upgrade Operating System** task sequence step doesn't put the Configuration Manager client into provisioning mode.

 For more information, see [Upgrade Operating System](../../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).

#### Revised documentation for task sequence variables
Two new articles are now available for understanding task sequence variables:  

- [How to use task sequence variables](../../../osd/understand/using-task-sequence-variables.md) is a new article that describes the different types of variables, methods to set the variables, and how to access them.  

- [Task sequence variables](../../../osd/understand/task-sequence-variables.md) is a reference for all available task sequence variables. This article combines the previous articles, which separated built-in variables from action variables. 



## Software Center

> [!Important]  
> To take advantage of new Configuration Manager features, first update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.


### Software Center infrastructure improvements
<!--1358309-->
Application catalog roles are no longer required to display user-available applications in Software Center. This change helps you reduce the server infrastructure required to deliver applications to users. Software Center now relies upon the management point to obtain this information, which helps larger environments scale better by assigning them to [boundary groups](../../servers/deploy/configure/boundary-groups-management-points.md).

For more information, see [Configure Software Center](../../../apps/plan-design/plan-for-software-center.md#configure-software-center)

> [!Note]  
> The application catalog website point and web service point roles are no longer *required* in 1806, but still *supported* roles. 
> 
> The **Silverlight user experience** for the application catalog website point is no longer supported. For more information, see [Removed and deprecated features](deprecated/removed-and-deprecated-cmfeatures.md).  


### Specify the visibility of the application catalog website link in Software Center
<!--1358214-->
Use client settings to control whether the link to **Open the Application Catalog web site** appears in the **Installation status** node of Software Center.  

For more information, see [Software Center client settings](../../clients/deploy/about-client-settings.md#software-center).

> [!Note]  
> The **Silverlight user experience** for the application catalog website point is no longer supported. For more information, see [Removed and deprecated features](deprecated/removed-and-deprecated-cmfeatures.md).  


### Custom tab for webpage in Software Center
<!--1358132-->
Use client settings to create a customized tab to open a webpage in Software Center. This feature allows you to show content to your end users in a consistent, reliable way. The following list includes a few examples:  

- Contact IT: information on how to contact your organization's IT department  

- IT Support Center: IT self-service actions such as searching a knowledge base or opening a support ticket.  

- End-user documentation: articles for users in your organization on various IT topics such as using applications or upgrading to Windows 10.  

For more information, see [Software Center client settings](../../clients/deploy/about-client-settings.md#software-center) and the [Software Center user guide](../../understand/software-center.md).


### Maintenance windows in Software Center
<!--1358131-->
Software Center now displays the next scheduled maintenance window. On the Installation Status tab, switch the view from All to Upcoming. It displays the time range and the list of deployments that are scheduled. If there are no future maintenance windows, the list is blank. 

For more information, see [How to use maintenance windows](../../clients/manage/collections/use-maintenance-windows.md) and the [Software Center user guide](../../understand/software-center.md).



## Software updates

### Third-party software updates
<!--1357605, 1352101, 1358714-->
Third-party software updates allow you to subscribe to partner catalogs in the Configuration Manager console and publish the updates to WSUS. You can then deploy these updates using the existing software update management process. 

For more information, see [Enable third-party updates](../../../sum/deploy-use/third-party-software-updates.md).


### Deploy software updates without content
<!--1357933-->
Deploy software updates to devices without first downloading and distributing content to distribution points. This feature is beneficial when dealing with extremely large update content, or when you always want clients to get content from the Microsoft Update cloud service. Clients in this scenario can also download content from peers that already have the necessary content. The Configuration Manager client continues to manage the content download, thus can utilize the Configuration Manager peer cache feature, or other technologies such as Delivery Optimization. This feature supports any update type supported by Configuration Manager software updates management, including Windows and Office updates. 

For more information, see the **No deployment package** option when you [Manually deploy software updates](../../../sum/deploy-use/manually-deploy-software-updates.md) or [Automatically deploy software updates](../../../sum/deploy-use/automatically-deploy-software-updates.md).


### Filter automatic deployment rules by software update architecture
 <!--1322266-->
You can now filter automatic deployment rules (ADR) to exclude architectures like Itanium and ARM64. On the **Software Updates** page of the Create Automatic Deployment Rule Wizard, the **Architecture** property filter is now available. 

For more information, see [Automatically deploy software updates](../../../sum/deploy-use/automatically-deploy-software-updates.md).


### Improved WSUS maintenance 
<!--1357898-->
The WSUS cleanup wizard now declines updates that are expired according to the supersedence rules defined on the software update point component properties. 

For more information, see [Software updates maintenance](../../../sum/deploy-use/software-updates-maintenance.md).



## Reporting

### New software updates compliance report
<!--1357775-->
Viewing reports for software updates compliance traditionally includes data from clients that haven't recently contacted the site. A new report, **Compliance 9 - Overall health and compliance**, lets you filter compliance results for a specific software update group by "healthy" clients. This report shows the more realistic compliance state of the active clients in your environment. 

For more information, see [Software updates reports](../../../sum/deploy-use/monitor-software-updates.md#BKMK_SUReports).



## Inventory

### <a name="bkmk_bigint"></a> Improvement to hardware inventory for large integer values
<!--1357880-->
Hardware inventory previously had a limit for integers larger than 4,294,967,296 (2^32). This limit could be reached for attributes such as hard drive sizes in bytes. The management point didn't process integer values above this limit, thus no value was stored in the database. Now in this release the limit is increased to 18,446,744,073,709,551,616 (2^64). 

For more information, see [Use of large integer values](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md#bkmk_bigint).


### Hardware inventory default unit revision
<!--514442-->
In [Configuration Manager version 1710](whats-new-in-version-1710.md#site-infrastructure), the default unit used in many reporting views changed from megabytes (MB) to gigabytes (GB). Due to [improvements to hardware inventory for large integer values](#bkmk_bigint), and based on customer feedback, this default unit is now MB again.



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## Configuration Manager console

### Product lifecycle dashboard
<!--1319632-->
The product lifecycle dashboard shows the state of the Microsoft Lifecycle Policy for Microsoft products installed on devices managed with Configuration Manager. It also provides you with information about Microsoft products in your environment, supportability state, and support end dates. Use the dashboard to understand the availability of support for each product. This information helps you plan for when to update the Microsoft products you use before their current end of support is reached.   

For more information, see [Product lifecycle dashboard](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


### Copy asset details from monitoring views
<!--1357856-->
The following areas of the **Monitoring** workspace now support copying text:  

- In the **Deployments** node, select a deployment, and click **View Status**. In the **Asset Details** pane of the Deployment Status view, select one or more devices.  

- Expand the **Distribution Status** node, and select **Content Status**. Select a piece of software, and click **View Status**. In the **Asset Details** pane of the Content Status view, select one or more distribution points. 

Right-click the asset, and select **Copy**. This action copies the selected assets as a comma-delimited list that includes the full details. The keyboard shortcut **CTRL** + **C** also works in these views. 

For more information, see [Console improvements in version 1806](../../servers/manage/admin-console-tips.md#copy-details-in-monitoring-views).


### Improvements to the Surface dashboard
<!--1358654-->
This release includes the following improvements to the Surface dashboard:  

- The Surface dashboard now displays a list of relevant devices when you select specific graph sections:  

   - Clicking on the **Percent of Surface Devices** tile opens a list of Surface devices.  

   - Clicking on a bar in the **Top Five Firmware Versions** tile opens a list of Surface devices with that specific firmware version.  

- When viewing these device lists from the Surface dashboard, right-click a device to perform common actions.  

For more information, see [Surface dashboard](../../clients/manage/surface-device-dashboard.md).


### View the currently signed on user for a device
<!--1358202-->
Now by default the **Devices** node of the **Assets and Compliance** workspace displays a column for the **Currently logged on user**. It also displays for any collection-specific device list. This value is as current as the [client status](../../clients/manage/monitor-clients.md#monitor-individual-clients). When the user signs off, the client clears this value. If no user is signed on, the value is blank. 

For more information, see [Console improvements in version 1806](../../servers/manage/admin-console-tips.md#view-users-for-a-device).


### Submit feedback from the Configuration Manager console  
<!--1357542-->

Send a smile! You can now directly tell the Configuration Manager team about your experiences. Sending feedback is easy from the Configuration Manager console. We want to hear all of your feedback: praise, problems, and suggestions. In the Configuration Manager console, click the smile button in the upper right corner above the ribbon. This feedback goes directly to the Microsoft product team for Configuration Manager. While using the Windows 10 Feedback Hub is still supported, you're encouraged to use the in-console feedback mechanism.  

For more information, see [Console improvements in version 1806](../../servers/manage/admin-console-tips.md#send-feedback) and [Product feedback](../../understand/product-feedback.md).



## Other updates

Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4459701).

For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [PowerShell 1806 Release Notes](/powershell/sccm/1806_release_notes).

The following update rollup (4462978) is available in the console starting on 24 October 2018: [Update rollup for Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4462978).


### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4346645](https://support.microsoft.com/help/4346645) | Update for Configuration Manager version 1806, first wave | 31 August 2018 | Yes |
| [4465865](https://support.microsoft.com/help/4465865) | Software updates do not download in Configuration Manager environment if WSUS is disconnected<br><br>This update is also in the update rollup (4462978) | 01 October 2018 | Yes |
| [4471892](https://support.microsoft.com/help/4471892) | PXE Responder doesn't work across subnets in Configuration Manager 1806 | 23 November 2018 | No |
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |


## Next steps

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 1806](../../servers/manage/checklist-for-installing-update-1806.md).

> [!TIP]  
> To install a new site, use a baseline version of Configuration Manager.  
>
> Learn more about:    
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)  
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known, significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).
