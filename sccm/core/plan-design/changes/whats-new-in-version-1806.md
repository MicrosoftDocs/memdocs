---
title: New current branch version 1806
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 1806 of Configuration Manager current branch.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# What's new in version 1806 of Configuration Manager current branch

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1806 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1706, 1710, or 1802. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

> [!Important]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in System Center Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4101375).
-->

<!--
The following additional updates to this release are also now available:
- [Update rollup for System Center Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4057517)
-->


The following sections provide details about the changes and new features in version 1806 of Configuration Manager current branch.  



<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1806 drops support for the following products:
-->



## Site infrastructure

### CMPivot
<!--1358456-->
Configuration Manager has always provided a large centralized store of device data, which customers use for reporting purposes. However, that data is only as good as the last time it was collected from clients. CMPivot is a new in-console utility that provides access to real-time state of devices in your environment. It immediately runs a query on all currently connected devices in the target collection and returns the results. You can then filter and group this data in the tool. By providing real-time data from online clients, you can more quickly answer business questions, troubleshoot issues, and respond to security incidents. For more information, see [CMPivot](/sccm/core/servers/manage/cmpivot).  


### Site server high availability
<!--1128774-->
High availability for a standalone primary site server role is a Configuration Manager-based solution to install an additional site server in passive mode. The site server in passive mode is in addition to your existing site server that is in active mode. A site server in passive mode is available for immediate use, when needed. For more information, see the following articles: 
- [Site server high availability](/sccm/core/servers/deploy/configure/site-server-high-availability) 
- [Flowchart - Set up a site server in passive mode](/sccm/core/servers/deploy/configure/passive-site-server-flowchart)
- [Flowchart - Promote site server (planned)](/sccm/core/servers/deploy/configure/promote-site-server-flowchart)
- [Flowchart - Promote site server (unplanned)](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart)


### Improvements to management insights
This release includes the following improvements to management insights:  

- Some management insights now have the option to take an action. This action is either navigating to the associated node in the console, or showing a filtered, query-based view.<!--1357930-->  

- A new group for Proactive Maintenance is available with six new rules, which help highlight potential configuration issues to avoid through regular upkeep.<!--1352184-->  

For more information, see [Management insights](/sccm/core/servers/manage/management-insights).


### Configuration Manager Toolkit
<!--1357145-->
The Configuration Manager server and client tools are now included on the server. Find them in the `CD.Latest\SMSSETUP\Tools` folder on the site server. No further installation required.


### Exclude Active Directory containers from discovery
<!--1358143-->
To reduce the number of discovered objects, exclude specific containers from Active Directory system discovery. 



## Content management

### Configure a remote content library for the site server
<!--1357525-->
To configure site server high availability or to free up hard drive space on your central administration or primary site servers, relocate the content library to another storage location. Move the content library to another drive on the site server, a separate server, or fault-tolerant disks in a storage area network (SAN). For more information, see the following articles: 
- [The content library](/sccm/core/plan-design/hierarchy/the-content-library)
- [Flowchart - Manage content library](/sccm/core/plan-design/hierarchy/manage-content-library-flowchart)


### Cloud distribution point support for Azure Resource Manager
<!--1322209-->
When creating a cloud distribution point, the wizard now provides the option to create an **Azure Resource Manager deployment**. Azure Resource Manager is a modern platform for managing all solution resources as a single entity, called a resource group. When deploying a cloud distribution point with Azure Resource Manager, the site uses Azure Active Directory to authenticate and create the necessary cloud resources. This modernized deployment doesn't require the classic Azure management certificate. 

The feature documentation for the cloud distribution point is also revised and enhanced. For more information, see the following articles:
- [Use a cloud distribution point](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)   
- [Install a cloud distribution point](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)  


### Pull-distribution points support cloud distribution points as source  
<!--1321554-->
Many customers use pull-distribution points in remote or branch offices, which download content from a source distribution point across the WAN. If your remote offices have a better connection to the internet, or to reduce load on your WAN links, you can now use a cloud distribution point in Microsoft Azure as the source. When you add a source on the **Pull Distribution Point** tab of the distribution point properties, any cloud distribution point in the site is now listed as an available distribution point. The behavior of both site system roles remains the same otherwise. For more information, see [Use a pull-distribution points](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).


### Enable distribution points to use network congestion control
<!--1358112-->
Windows Low Extra Delay Background Transport (LEDBAT) is a feature of Windows Server to help manage background network transfers. For distribution points running on supported versions of Windows Server, enable an option to help adjust network traffic. Clients only use network bandwidth when it's available. 


### Partial download support in client peer cache to reduce WAN utilization
<!--1357346-->
Client peer cache sources can now divide content into parts. These parts minimize the network transfer to reduce WAN utilization. The management point provides more detailed tracking of the content parts. It tries to eliminate more than one download of the same content per boundary group. In Hierarchy Settings, enable the option to **Configure client peer cache sources to divide content into parts**. 


### Boundary group options for peer downloads
<!--1356193-->
Boundary groups now include additional settings to give you more control over content distribution in your environment. This release adds the following options:  

- **Allow peer downloads in this boundary group**: This setting is enabled by default. The management point provides clients a list of content locations that includes peer sources. This setting also affects applying Group IDs for Delivery Optimization.  

- **During peer downloads, only use peers within the same subnet**: This setting is dependent upon the one above. If you enable this option, the management point only includes in the content location list peer sources that are in the same subnet as the client.  



<!-- ## Migration  -->



## Client management

### Improvement to client push security
<!--1358204-->
When using the client push method of installing the Configuration Manager client, the site can now require Kerberos mutual authentication. This enhancement helps to secure the communication between the server and the client. For more information, see [How to install clients with client push](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).


### Enhanced HTTP site system
<!--1356889,1358228-->
Using HTTPS communication is recommended for all Configuration Manager communication paths, but can be challenging for some customers due to the overhead of managing PKI certificates. The introduction of Azure Active Directory (Azure AD) integration reduces some but not all of the certificate requirements. 

This release includes improvements to how clients communicate with site systems. On the site properties, **Client Computer Communication** tab, select the option for **HTTPS or HTTP**, and then enable the new option to **Use Configuration Manager-generated certificates for HTTP site systems**. This is a [pre-release feature](/sccm/core/servers/manage/pre-release-features).

This option supports the following primary scenarios:  

- **Client to HTTP management point**<!--1356889-->: [Azure AD-joined devices](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) can communicate through a cloud management gateway (CMG) with a management point configured for HTTP. The site server generates a certificate for the management point allowing it to communicate via a secure channel.   

- **Client to HTTP distribution point**<!--1358228-->: A workgroup or Azure AD-joined client can download content over a secure channel from a distribution point configured for HTTP.   


### Azure AD device identity 
<!--1358460-->
An [Azure AD-joined](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) or [hybrid Azure AD device](https://docs.microsoft.com/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices) without an Azure AD user signed in can securely communicate with its assigned site. The cloud-based device identity is now sufficient to authenticate with the CMG and management point.  


### CMTrace installed with client
<!--1357971-->
The CMTrace log viewing tool is now automatically installed along with the Configuration Manager client. It's added to the client installation directory, which by default is `%WinDir%\ccm\cmtrace.exe`.


### Cloud management dashboard
<!--1358461-->
The new cloud management dashboard provides a centralized view for cloud management gateway (CMG) usage. When the site is onboarded with Azure AD, it also displays data about cloud users and devices. In the Configuration Manager console, go to the **Monitoring** workspace. Select the **Cloud Management** node, and view the dashboard tiles.  

This feature also includes the **CMG connection analyzer** for real-time verification to aid troubleshooting. The in-console utility checks the current status of the service, and the communication channel through the CMG connection point to any management points that allow CMG traffic. In the Configuration Manager console, go to the **Administration** workspace. Expand **Cloud Services**, and select **Cloud management gateway**. Select the target CMG instance, and then click **Connection analyzer** in the ribbon.


### Improvements to cloud management gateway

Version 1806 includes the following improvements to the cloud management gateway (CMG):

#### Simplified client bootstrap command line
<!--1358215-->
When installing the Configuration Manager client on the internet via a CMG, fewer command-line properties are now required. For more information on one example of this scenario, see the [Command line to install Configuration Manager client](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client) when preparing for co-management. 

The following command-line properties are required in all scenarios:
  - CCMHOSTNAME  
  - SMSSITECODE  

The following properties are required when using Azure AD for client authentication instead of PKI-based client authentication certificates:
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

The following property is required if the client will roam back to the intranet:
  - SMSMP  

The following example includes all of the above properties:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

For more information, see [Client installation properties](/sccm/core/clients/deploy/about-client-installation-properties).

#### Download content from a CMG
<!--1358651-->
Previously, you had to deploy a cloud distribution point and CMG as separate roles. A CMG can now also serve content to clients. This functionality reduces the required certificates and cost of Azure VMs. To enable this feature, enable the new option to **Allow CMG to function as a cloud distribution point and serve content from Azure storage** on the **Settings** tab of the CMG properties. 

#### Trusted root certificate isn't required with Azure AD
<!--503899-->
When you create a CMG, you're no longer required to provide a [trusted root certificate](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-trusted-root-certificate-to-clients) on the Settings page. This certificate isn't required when using Azure Active Directory (Azure AD) for client authentication, but used to be required in the wizard. If you're using PKI client authentication certificates, then you still must add a trusted root certificate to the CMG.



## Co-management

### Sync MDM policy from Microsoft Intune for a co-managed device
<!--1357377-->
When you [switch a co-management workload](/sccm/core/clients/manage/co-management-switch-workloads), the co-managed devices automatically synchronize MDM policy from Microsoft Intune. This sync also happens when you initiate the **Download Computer Policy** action from Client Notifications in the Configuration Manager console. For more information, see [Initiate client policy retrieval using client notification](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).


### Transition new workloads to Intune using co-management
The following workloads are now able to transition from Configuration Manager to Intune after enabling co-management:  

- **Device configuration**<!--1357903-->: This workload lets you use Intune to deploy MDM policies, while continuing to use Configuration Manager for deploying applications.  

- **Office 365**<!--1357841-->: Devices don't install Office 365 deployments from Configuration Manager.  

- **Mobile apps**<!--1357892-->: Any available apps deployed from Intune are available in the Company Portal. Apps that you deploy from Configuration Manager are available in Software Center.  

To transition these workloads, go to the co-management properties page and move the workload slider bar from Configuration Manager to **Pilot** or **All**. For more information, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview).


### Support for multiple hierarchies to one Intune tenant
<!--1357944-->
Some customers have several Configuration Manager hierarchies and want to consolidate in the future to a single tenant for Azure Active Directory and Microsoft Intune. Co-management now supports connecting more than one Configuration Manager environment to the same Intune tenant.

 

## Compliance settings

### Configure Windows Defender SmartScreen settings for Microsoft Edge
<!--1353701-->
The [Microsoft Edge browser compliance settings policy](/sccm/compliance/deploy-use/browser-profiles) adds the following three settings for Windows Defender SmartScreen: 
- Allow SmartScreen
- Users can override SmartScreen prompt for sites
- Users can override SmartScreen prompt for files


### SCAP extensions
<!--1357552-->
Convert Security Content Automation Protocol (SCAP) content to compliance settings baselines and generate SCAP reports using a console extension. This feature also includes a new dashboard to visualize the client compliance as well as XCCDF rule compliance. For more information, see [About the SCAP extensions](/sccm/compliance/plan-design/scap/about-scap).



## Application management

### Phased deployment of applications
<!--1358147-->
Create a phased deployment for an application. Phased deployments allow you to orchestrate a coordinated, sequenced rollout of software based on customizable criteria and groups. For example, deploy the application to a pilot collection, and then automatically continue the rollout based on success criteria. 

For more information, see the following articles:  

- [Create a phased deployment](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Manage and monitor phased deployments](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  


### Provision Windows app packages for all users on a device
<!--1358310-->
Provision an application with a Windows app package for all users on the device. One common example of this scenario is provisioning an app from the Microsoft Store for Business and Education, like Minecraft: Education Edition, to all devices used by students in a school. Previously, Configuration Manager only supported installing these applications per user. After signing in to a new device, a student would have to wait to access an app. Now when the app is provisioned to the device for all users, they can be productive more quickly.


### Office Customization Tool integration with the Office 365 Installer
<!--1358149-->
The Office Customization Tool is now integrated with the Office 365 Installer in the Configuration Manager console. When creating a deployment for Office 365, dynamically configure the latest Office manageability settings. The Office Customization Tool is updated at the same time as the release of new builds of Office 365. This allows you to take advantage of new manageability settings in Office 365 as soon as they are available. 


### Support for new Windows app package formats
<!--1357427-->
Configuration Manager now supports the deployment of new Windows 10 app package (.msix) and app bundle (.msixbundle) formats.


### Uninstall application on approval revocation
<!--1357891-->
The behavior has changed when you revoke approval for an application. Now when you deny the request for the application, the client uninstalls the application from the user's device. This behavior requires that you enable the [optional feature](https://docs.microsoft.com/en-us/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Approve application requests for users per device**.


### Package Conversion Manager 
<!--1357861-->
Package Conversion Manager is now an integrated tool that allows you to convert legacy Configuration Manager 2007 packages into Configuration Manager current branch applications. Then you can use features of applications such as dependencies, requirement rules, and user device affinity.

Start with the following actions from the **Packages** node in the Configuration Manager console:  

   - **Analyze Package**: Start the conversion process by analyzing the package.  

   - **Convert Package**: Some packages can easily be converted into applications with this action.  

   - **Fix and Convert**: Some packages require issues to be fixed before converting into applications.  

Then go to the **Package Conversion Status** dashboard in the **Monitoring** workspace. This new dashboard shows the overall analysis and conversion state of packages in the site.



## OS deployment

### Improvements to phased deployments

This release includes the following improvements to phased deployments:  

#### Create a phased deployment with manually configured phases
<!--1358148--> 
For a task sequence, now manually configure the phases when you create a phased deployment. Add up to 10 additional phases from the **Phases** tab of the Create Phased Deployment wizard. You can still automatically create a default two-phase deployment. For more information, see [Create a phased deployment with manually configured phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_manual).

#### Phased deployment status
<!--1358577-->
Phased deployments now have a native monitoring experience. From the **Deployments** node in the **Monitoring** workspace, select a phased deployment, and then click **Phased Deployment Status** in the ribbon. For more information, see [Manage and monitor phased deployments](/sccm/osd/deploy-use/manage-monitor-phased-deployments).  

#### Gradual rollout during phased deployments
<!--1358578-->
During a phased deployment, the rollout in each phase can now happen gradually. This behavior helps mitigate the risk of deployment issues, and decreases the load on the network caused by the distribution of content to clients. The site can gradually make the software available depending on the configuration for each phase. Every client in a phase has a deadline relative to the time the software is made available. The time window between the available time and deadline is the same for all clients in a phase. For more information, see [Phase settings](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_settings).  


### Improvements to Windows 10 in-place upgrade task sequence
<!--1358500-->
The default task sequence template for Windows 10 in-place upgrade now includes another new group with recommended actions to add in case the upgrade process fails. These actions make it easier to troubleshoot. One such tool is Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). It's a standalone diagnostic tool to obtain details about why a Windows 10 upgrade was unsuccessful. 

For more information, see [Create a task sequence to upgrade an OS](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-on-failure).



## Software Center

### Specify the visibility of the application catalog website link in Software Center
<!--1358214-->
Use client settings to control whether the link to **Open the Application Catalog web site** appears in the **Installation status** node of Software Center.  

> [!Note]  
> The Application Catalog website user experience isn't supported in version 1806. For more information, see [Removed and deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### Custom tab for webpage in Software Center
<!--1358132-->
Use client settings to create a customized tab to open a webpage in Software Center. This feature allows you to show content to your end users in a consistent, reliable way. The following list includes a few examples:  

- Contact IT: information on how to contact your organization's IT department  

- IT Support Center: IT self-service actions such as searching a knowledge base or opening a support ticket.  

- End-user documentation: articles for users in your organization on various IT topics such as using applications or upgrading to Windows 10.  


### Maintenance windows in Software Center
<!--1358131-->
Software Center now displays the next scheduled maintenance window. On the Installation Status tab, switch the view from All to Upcoming. It displays the time range and the list of deployments that are scheduled. If there are no future maintenance windows, the list is blank. 



## Software updates

### Third party software updates
<!--1357605, 1352101, 1358714-->
Third-party software updates allow you to subscribe to partner catalogs in the Configuration Manager console and publish the updates to WSUS. You can then deploy these updates using the existing software update management process. For more information see [Enable third-party updates](/sccm/sum/deploy-use/third-party-software-updates.md).


### Deploy software updates without content
<!--1357933-->
You can now deploy software updates to devices without first downloading and distributing software update content to distribution points. This feature is beneficial when dealing with extremely large update content, or when you always want clients to get content from the Microsoft Update cloud service. Clients in this scenario can also download content from peers that already have the necessary content. The Configuration Manager client continues to manage the content download, thus can utilize the Configuration Manager peer cache feature, or other technologies such as Delivery Optimization. This feature supports any update type supported by Configuration Manager software updates management, including Windows and Office updates. For more information, see the **No deployment package** option when you [Manually deploy software updates](/sccm/sum/deploy-use/manually-deploy-software-updates) or [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).


### Filter automatic deployment rules by software update architecture
 <!--1322266-->
You can now filter automatic deployment rules (ADR) to exclude architectures like Itanium and ARM64. On the **Software Updates** page of the Create Automatic Deployment Rule Wizard, the **Architecture** property filter is now available. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).


### Improved WSUS maintenance 
<!--1357898-->
The WSUS cleanup wizard now declines updates that are expired according to the supersedence rules defined on the software update point component properties. For more information, see [Software updates maintenance](../../../sum/deploy-use/software-updates-maintenance.md).



## Reporting

### New software updates compliance report
<!--1357775-->
Viewing reports for software updates compliance traditionally includes data from clients that haven't recently contacted the site. A new report, **Compliance 9 - Overall health and compliance**, lets you filter compliance results for a specific software update group by "healthy" clients. This report shows the more realistic compliance state of the active clients in your environment. 



## Inventory

### Improvement to hardware inventory for large integer values
<!--1357880-->
Hardware inventory currently has a limit for integers larger than 4,294,967,296 (2^32). This limit can be reached for attributes such as hard drive sizes in bytes. The management point doesn't process integer values above this limit, thus no value is stored in the database. Now in this release the limit is increased to 18,446,744,073,709,551,616 (2^64). 

For a property with a value that doesn't change, like total disk size, you may not immediately see the value after upgrading the site. Most hardware inventory is a delta report. The client only sends values that change. To work around this behavior, add another property to the same class. This action causes the client to update all properties in the class that changed. 



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## Configuration Manager console

### Product lifecycle dashboard
<!--1319632-->
The new [product lifecycle dashboard](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard) shows the state of the Microsoft Lifecycle Policy for Microsoft products installed on devices managed with Configuration Manager. It also provides you with information about Microsoft products in your environment, supportability state, and support end dates. Use the dashboard to understand the availability of support for each product. This information helps you plan for when to update the Microsoft products you use before their current end of support is reached.   

To access the product lifecycle dashboard, in the Configuration Manager console go to the **Assets and Compliance** workspace, expand **Asset Intelligence**, and select the **Product Lifecycle** node.


### Copy asset details from monitoring views
<!--1357856-->
The following areas of the **Monitoring** workspace now support copying text:  

- In the **Deployments** node, select a deployment, and click **View Status**. In the **Asset Details** pane of the Deployment Status view, select one or more devices.  

- Expand the **Distribution Status** node, and select **Content Status**. Select a piece of software, and click **View Status**. In the **Asset Details** pane of the Content Status view, select one or more distribution points. 

Right-click the asset, and select **Copy**. This action copies the selected assets as a comma-delimited list that includes the full details. The keyboard shortcut **CTRL** + **C** also works in these views. 


### Improvements to the Surface dashboard
<!--1358654-->
This release includes the following improvements to the [Surface dashboard](/sccm/core/clients/manage/surface-device-dashboard):  

- The Surface dashboard now displays a list of relevant devices when you select specific graph sections:  

   - Clicking on the **Percent of Surface Devices** tile opens a list of Surface devices.  

   - Clicking on a bar in the **Top Five Firmware Versions** tile opens a list of Surface devices with that specific firmware version.  

- When viewing these device lists from the Surface dashboard, right-click a device to perform common actions.  


### View the currently signed on user for a device
<!--1358202-->
Now by default the **Devices** node of the **Assets and Compliance** workspace displays a column for the **Currently logged on user**. It also displays for any collection-specific device list. This value is as current as the [client status](/sccm/core/clients/manage/monitor-clients#bkmk_indStatus). When the user signs off, the client clears this value. If no user is signed on, the value is blank. 


### Submit feedback from the Configuration Manager console  
<!--1357542-->

Send a smile! You can now directly tell the Configuration Manager team about your experiences. Sending feedback is easy from the Configuration Manager console. We want to hear all of your feedback: praise, problems, and suggestions. In the Configuration Manager console, click the smile button in the upper right corner above the ribbon. This feedback goes directly to the Microsoft product team for Configuration Manager. While using the Windows 10 Feedback Hub is still supported, you're encouraged to use the in-console feedback mechanism.  



## Next steps
When you're ready to install this version, see [Installing updates for Configuration Manager](/sccm/core/servers/manage/updates).

> [!TIP]  
> To install a new site, use a baseline version of Configuration Manager.  
>
>  Learn more about:    
>   - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

