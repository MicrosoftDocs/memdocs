---
title: New version 1802
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 1802 of Configuration Manager.
ms.date: 10/09/2019
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# What's new in version 1802 of Configuration Manager

*Applies to: Configuration Manager (current branch)*

Update 1802 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1702, 1706, or 1710. <!-- baseline only statement: -->When installing a new site, it's also available as a baseline version.

Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 1802](https://support.microsoft.com/help/4101375).

The following additional updates to this release are also now available:
- [Update rollup for Configuration Manager current branch, version 1802](https://support.microsoft.com/help/4163547)

> [!TIP]  
> To install a new site, you must use a baseline version of Configuration Manager.  
>
> Learn more about:    
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)  
> - [Installing updates at sites](../../servers/manage/updates.md)  
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

The following sections provide details about the changes and new capabilities in version 1802 of Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1802 drops support for the following products:
-->


## Site infrastructure

### Reassign distribution point
<!-- 1306937 -->
Many customers have large Configuration Manager infrastructures, and are reducing primary or secondary sites to simplify their environment. They still need to retain distribution points at branch office locations to serve content to managed clients. These distribution points often contain multiple terabytes or more of content. This content is costly in terms of time and network bandwidth to distribute to these remote servers. This feature lets you reassign a distribution point to another primary site without redistributing the content. This action updates the site system assignment while persisting all of the content on the server. For more information, see [Reassign a distribution point](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_reassign).

### Configure Windows Delivery Optimization to use Configuration Manager boundary groups
<!-- 1324696 -->
You use Configuration Manager boundary groups to define and regulate content distribution across your corporate network and to remote offices. [Windows Delivery Optimization](/windows/deployment/update/waas-delivery-optimization) is a cloud-based, peer-to-peer technology to share content between Windows 10 devices. Starting in this release, configure Delivery Optimization to use your boundary groups when sharing content among peers. A new client setting applies the boundary group identifier as the Delivery Optimization group identifier on the client. When the client communicates with the Delivery Optimization cloud service, it uses this identifier to locate peers with the desired content. For more information, see [Fundamental concepts for content management](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).

### Support for Windows 10 ARM64 devices
<!-- 1353704 -->
Starting in this release the Configuration Manager client is supported on Windows 10 ARM64 devices. Existing client management features should work with these new devices. For example, hardware and software inventory, software updates, and application management. Operating system deployment is currently not supported. 

### Improved support for CNG certificates
<!-- 1357314 -->
Configuration Manager (current branch) version 1710 supports [Cryptography: Next Generation (CNG) certificates](../network/cng-certificates-overview.md). Version 1710 limits support to client certificates in several scenarios. 

Starting in this release, use CNG certificates for the following HTTPS-enabled server roles:
- Management point
- Distribution point
- Software update point
- State migration point  


### Boundary group fallback for management points
<!-- 1324594 -->
Configure fallback relationships for management points between [boundary groups](../../servers/deploy/configure/boundary-groups.md). This behavior provides greater control for the management points that clients use. For more information, see [Configure boundary groups](../../servers/deploy/configure/boundary-groups-management-points.md).


### Cloud distribution point site affinity
<!--503719-->
This feature benefits customers with a multi-site, geographically dispersed hierarchy using cloud distribution points. When an internet-based client searches for content, previously there was no order to the list of cloud distribution points received by the client. This behavior could result in internet-based clients receiving content from geographically distant cloud distribution points. Downloading content from such a distant server is typically slower than a closer server.
 
With cloud distribution point site affinity, an internet-based client receives an ordered list. This list prioritizes cloud distribution points from the client's assigned site. This behavior allows the administrator to preserve their design intent for content downloads from site resources.
 

## Management insights
<!-- 1353967 -->
Management insights in Configuration Manager provide information about the current state of your environment. The information is based on analysis of data from the site database. Insights help you to better understand your environment and take action based on the insight. For details see, [Management Insights](../../servers/manage/management-insights.md)

In Configuration Manager 1802, the following insights are available:
- Applications:
    - Applications without deployments
- Cloud Services: <!--1356412-->
    - Assess co-management readiness 
    - Enable your devices to be hybrid Azure Active Directory-joined
    - Modernize your identity and access infrastructure
    -  Upgrade your clients to Windows 10, version 1709 or above 
- Collections:
    - Empty Collections
- Simplified Management:  <!--1355148-->
    - Outdated client versions  
- Software Center: 
    - Direct users to Software Center instead of Application Catalog  
    - Use the new version of Software Center 
- Windows 10: <!--1357421-->
    - Configure Windows telemetry and commercial ID key 
    - Connect Configuration Manager to Upgrade Readiness 
   
<!-- ## Migration  -->



## Client management

### Cloud management gateway support for Azure Resource Manager
<!-- 1324735 -->
When creating an instance of the [cloud management gateway](../../clients/manage/cmg/overview.md) (CMG), the wizard now provides the option to create an **Azure Resource Manager deployment**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) is a modern platform for managing all solution resources as a single entity, called a [resource group](/azure/azure-resource-manager/resource-group-overview#resource-groups). When deploying CMG with Azure Resource Manager, the site uses Azure Active Directory (Azure AD) to authenticate and create the necessary cloud resources. This modernized deployment doesn't require the classic Azure management certificate. For more information, see [CMG topology design](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).

> [!IMPORTANT]
> This capability doesn't enable support for Azure Cloud Service Providers (CSP). The CMG deployment with Azure Resource Manager continues to use the classic cloud service, which the CSP doesn't support. For more information, see [Available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### Improvements to cloud management gateway  

- Starting in this release, the **cloud management gateway** is no longer a pre-release feature.  

- The feature documentation is revised and enhanced. For more information, see the following articles:
    - [Plan for the cloud management gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md)
    - [Cloud management gateway size and scale numbers](../configs/size-and-scale-numbers.md#bkmk_cmg)
    - [Security and privacy for cloud management gateway](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md)
    - [Frequently asked questions about the cloud management gateway](../../clients/manage/cmg/cloud-management-gateway-faq.yml)
    - [Set up cloud management gateway](../../clients/manage/cmg/setup-cloud-management-gateway.md)  


### Configure hardware inventory to collect strings larger than 255 characters
<!-- 1357389 -->
You can configure the length of strings to be greater than 255 characters for hardware inventory properties. This change applies only to newly added classes and for hardware inventory properties that aren't keys. For details, see the [Extend hardware inventory](../../clients/manage/inventory/extend-hardware-inventory.md#collect-strings-larger-than-255-characters) article. 

 ### Deprecation announcement for Linux and Unix client support
 <!--510139-->
Microsoft intends to deprecate the Linux and UNIX client support in Configuration Manager roughly one year from now, such that the clients will not be included in version 1902 in early calendar 2019. The Configuration Manager 1810 release, in late calendar 2018, will be the last release to include the Linux and UNIX clients, and they will be supported for the full lifecycle of Configuration Manager 1810. After Configuration Manager 1810, customers should consider Microsoft Azure Management for managing Linux servers. Azure solutions have extensive Linux support that in most cases exceed Configuration Manager functionality, including end-to-end patch management for Linux.

### Surface device dashboard
<!--1355788-->
The Surface device dashboard provides information about the Surface devices found in your environment. In the console, go to **Monitoring** > **Surface Devices**. You can view the  items:
- Percent of Surfaces
- Percent of Surface models
- Top five firmware versions

For details, see the [Surface dashboard](../../clients/manage/surface-device-dashboard.md) article.

### Change in the Configuration Manager client install
<!--1356195-->
Starting in this release, Silverlight is no longer installed on client devices automatically. For more information, see [Prerequisites for deploying clients to Windows computers](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)

## Co-management

### Transition Endpoint Protection workload to Intune using co-management
<!-- 1357365 -->
 The Endpoint Protection workload can be transitioned to Intune after enabling co-management. To transition the Endpoint Protection workload, go to the co-management properties page and move the slider bar from Configuration Manager to **Pilot** or **All**. For details about the workloads, see [Co-management workloads](../../../comanage/workloads.md). For more information about co-management, see [Co-management for Windows 10 devices](../../../comanage/overview.md).
 
### Co-management dashboard in Configuration Manager
<!--1356648-->
Beginning in this release, you can view a dashboard with information about co-management. The dashboard helps you review machines that are co-managed in your environment. The graphs can help identify devices that might need attention. For details, see the [Co-management dashboard](../../../comanage/how-to-monitor.md#co-management-dashboard) article. 


## Compliance settings

### Microsoft Edge browser policies
<!-- 1357310 -->
For customers who use the [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge) web browser on Windows 10 clients, create a Configuration Manager compliance settings policy to configure several Microsoft Edge settings. For more information, see [Create Microsoft Edge browser profile](../../../compliance/deploy-use/browser-profiles.md). 



## Application Management

### Allow user interaction when installing an application
<!-- 1356976 -->
Allow an end user to interact with an application installation during the running of the task sequence. For example, run a setup process that prompts the end user for various options. Some application installers can't silence user prompts, or the installation process may require specific configuration values only known to the user. This feature allows you to handle these installation scenarios. For more information, see [Specify user experience options for the deployment type](../../../apps/deploy-use/create-applications.md#bkmk_dt-ux).

### Do not automatically upgrade superseded applications
<!-- 1351266 -->
Configure an application deployment to not automatically upgrade any superseded version. Now when creating the deployment, on the **Deployment Settings** page of the **Deploy Software Wizard**, for **Available** install purpose, you can enable or disable the option to **Automatically upgrade any superseded versions of this application**. For more information, see [Specify deployment settings](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).

### Approve application requests for users per device
<!-- 1357015 -->
Starting in this release, when a user requests an application that requires approval, the specific device name is now a part of the request. If the administrator approves the request, the user is only able to install the application on that device. The user must submit another request to install the application on another device. For more information, see [Specify deployment settings](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).

 > [!Note]  
 > This is an optional feature. For more information, see [Enable optional features from updates](../../servers/manage/optional-features.md).  


### Run scripts improvements 
<!-- 1236459 -->
 Starting in this release, **Run Scripts** is no longer a pre-release feature. The script output now returns using JSON formatting. For more information, see [Create and run PowerShell scripts from the Configuration Manager console](../../../apps/deploy-use/create-deploy-scripts.md).


## Operating system deployment

### Windows 10 in-place upgrade task sequence via cloud management gateway
<!-- 1357149 -->
The Windows 10 [in-place upgrade task sequence](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) now supports deployment to internet-based clients managed through the [cloud management gateway](../../clients/manage/cmg/overview.md). This ability allows remote users to more easily upgrade to Windows 10 without needing to connect to the corporate network. For more information, see [Deploy a task sequence](../../../osd/deploy-use/deploy-a-task-sequence.md).

### Improvements to Windows 10 in-place upgrade task sequence
<!-- 1357425 -->
The default task sequence template for Windows 10 in-place upgrade now includes additional groups with recommended actions to add before and after the upgrade process. These actions are common among many customers who are successfully upgrading devices to Windows 10. For more information, see [In-place upgrade recommendations](../../../osd/understand/in-place-upgrade-recommendations.md#prepare-for-upgrade).

### Improvements to operating system deployment
This release includes the following improvements to operating system deployment:
- In Windows PE, when launching cmtrace.exe, you are no longer prompted to choose whether to make this program the default viewer for log files. <!-- SMS 500897 -->
- Add boot images to the [Download Package Content](../../../osd/understand/task-sequence-steps.md#BKMK_DownloadPackageContent) task sequence step.
- Improvements to the [Run Task Sequence](../../../osd/understand/task-sequence-steps.md#child-task-sequence) step: <!-- 1261338 -->   
  - Support for all operating system deployment scenarios from Software Center, PXE, and media.
  - Improvements to console actions such as copy, import, export, and warning during object deletion.
  - Support for the [Create Prestaged Content File](../hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent) wizard.
  - Integration with deployment verification. For more information, see [High-risk task sequence deployments](../../../osd/deploy-use/deploy-a-task-sequence.md). 
  - The Run Task Sequence step can now be used across multiple levels of task sequences, not just a single parent-child relationship. Multi-level relationships increase the complexity, so use with caution. These relationships are still checked for circular references.

### Deployment templates for task sequences
<!-- 1357391 -->
The [deployment wizard for task sequences](../../../osd/deploy-use/deploy-a-task-sequence.md) can now create a deployment template. The deployment template can be saved and applied to an existing or new task sequence to create a deployment. 

### Phased deployments for task sequences
<!--1356837-->
 Phased deployments is a [pre-release feature](../../servers/manage/pre-release-features.md). Phased deployments automate a coordinated, sequenced rollout of a task sequence across multiple collections. You can [create phased deployments](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) with the default of two phases, or manually configure multiple phases. Phased deployment of task sequences does not support PXE or media installation.




## Software Center

### Install multiple applications in Software Center
<!-- 1357126 -->
If an end user or desktop technician needs to install multiple applications on a device, Software Center now supports installing multiple selected applications. This behavior allows the user to be more efficient while not waiting for one installation to finish before starting the next. For more information, see [Install multiple applications](../../understand/software-center.md#install-multiple-applications) in the new Software Center user guide.

### Use Software Center to browse and install user-available applications on Azure AD-joined devices
<!-- 1322613 -->
If you deploy applications as available to users, they can now browse and install them through Software Center on Azure Active Directory (Azure AD) devices. For more information, see [Prerequisites to deploy user-available applications](../../../apps/plan-design/prerequisites-deploy-user-available-apps.md).

### Hide installed applications in Software Center
<!--1357592-->
Installed applications can now be hidden in Software Center. Applications that are already installed will no longer show in the Applications tab when this option is enabled under client settings. This option is set as the default when you install or upgrade to Configuration Manager 1802.  Installed applications are still available for review under the installation status tab. [Hide installed applications in Software Center](../../clients/deploy/about-client-settings.md#software-center-settings) has additional details.   

### Hide unapproved applications in Software Center
 <!--1355146-->
When this client setting option is enabled, user available applications that require approval are hidden in Software Center.  [Hide unapproved applications in Software Center](../../clients/deploy/about-client-settings.md#software-center-settings) has additional details.  

### Software Center shows user additional compliance information
<!-- 1235616 -->
 When using Device Health Attestation status as a compliance policy rule for Conditional Access to company resources, Software Center now shows the user the Device Health Attestation setting that is not compliant.


 ## Software updates 

### Schedule automatic deployment rule evaluation to be offset from a base day. 
<!--1357133-->
Automatic deployment rules can be scheduled to evaluate offset from a base day. Meaning, if patch Tuesday actually falls on Wednesday for you, the evaluation schedule can be set for the second Tuesday of the month offset by one day. For details, see [Automatically deploy software updates](../../../sum/deploy-use/automatically-deploy-software-updates.md#BKMK_CreateAutomaticDeploymentRule). 



## Reporting

### Report for default browser counts
<!-- 1357830 -->
Now there is a new report to show the count of clients with a specific web browser as the Windows default. See the **Default Browser counts** report in the **Software - Companies and Products** reports group. For more information, see the [List of reports](../../servers/manage/list-of-reports.md#software---companies-and-products).

### Report on Windows Autopilot device information
<!-- 1351442 -->
Windows Autopilot is a solution for onboarding and configuring new Windows 10 devices in a modern way. For more information, see an [Overview of Windows Autopilot](/windows/deployment/windows-autopilot/windows-10-autopilot). One method of registering existing devices with Windows Autopilot is to upload device information to the Microsoft Store for Business and Education. This information includes the device serial number, Windows product identifier, and a hardware identifier. Use Configuration Manager to collect and report this device information with the new report, **Windows Autopilot Device Information**, in the **Hardware - General** reports node. For more information, see [How to prepare internet-based devices for co-management](../../../comanage/how-to-prepare-Win10.md#windows-autopilot) in preparing for co-management.

### Report on Windows 10 Servicing details for a specific collection
<!--1357653-->
The **Windows 10 Servicing details for a specific collection** report displays general information about Windows 10 servicing for a specific collection. This report shows Resource ID, NetBIOS name, OS name, OS release name, build, OS branch, and servicing state for Windows 10 devices. For more information, see the [List of reports](../../servers/manage/list-of-reports.md#operating-system)



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## Protect devices

### Improvements to Configuration Manager Policies for Windows Defender Exploit Guard
<!-- 1356220 -->
Additional policy settings for the [Attack Surface Reduction](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_ASR) and [Controlled folder access](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_CFA) components have been added in Configuration Manager for [Windows Defender Exploit Guard](/windows/security/threat-protection/microsoft-defender-atp/configure-attack-surface-reduction).

### New host interaction settings for Windows Defender Application Guard
<!-- 1356256 -->
For Windows 10 version 1709 and later devices, there are two new host interaction settings for [Windows Defender Application Guard](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_HIS): 
- Websites can be given access to the host's virtual graphics processor. 
- Files downloaded inside the container can be persisted on the host. 




## Configuration Manager console

### Improvements to the Configuration Manager console 
This release includes the following improvements to the Configuration Manager console.
- Device lists under Assets and Compliance, Devices, now display the primary user by default. This column only displays in the Devices node. The last logged on user can also be added as an optional column.<!-- 1357280 --> Enable [user and device affinity](../../clients/deploy/about-client-settings.md#user-and-device-affinity) client settings for the site to associate a primary user with a device.
- If a collection is a member of another collection and it is renamed, then the new name is updated under membership rules.<!--1357282--> 
- When using remote control on a client with multiple monitors at different DPI scaling, the mouse cursor now correctly maps between them. <!--433170-->
- The [Office 365 Client Management dashboard](../../../sum/deploy-use/office-365-dashboard.md) displays a list of relevant devices when graph sections are selected. <!--1357281 --> 



## Next Steps
When you're ready to install this version, see [Updates for Configuration Manager](../../servers/manage/updates.md).