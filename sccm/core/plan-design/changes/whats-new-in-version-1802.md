---
title: "New version 1802 | Microsoft Docs"
titleSuffix: "Configuration Manager"
description: "Get details about changes and new capabilities introduced in version 1802 of System Center Configuration Manager."
ms.custom: na
ms.date:  03/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: mestew
ms.author: mstewart
manager: dougeby
---
# What's new in version 1802 of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1802 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1702, 1706, or 1710. <!-- baseline only statement: -->When installing a new site, it's also available as a baseline version.

> [!TIP]  
> To install a new site, you must use a baseline version of Configuration Manager.  
>  Learn more about:    
>   - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Installing updates at sites](/sccm/core/servers/manage/updates)  
>   - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

The following sections provide details about the changes and new capabilities in version 1802 of Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1802 drops support for the following products:
-->


## Site infrastructure

### Reassign distribution point
<!-- 1306937 -->
Many customers have large Configuration Manager infrastructures, and are reducing primary or secondary sites to simplify their environment. They still need to retain distribution points at branch office locations to serve content to managed clients. These distribution points often contain multiple terabytes or more of content. This content is costly in terms of time and network bandwidth to distribute to these remote servers. This feature lets you reassign a distribution point to another primary site without redistributing the content. This action updates the site system assignment while persisting all of the content on the server. For more information, see [reassign a distribution point](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_reassign).

### Configure Windows Delivery Optimization to use Configuration Manager boundary groups
<!-- 1324696 -->
You use Configuration Manager boundary groups to define and regulate content distribution across your corporate network and to remote offices. [Windows Delivery Optimization](/windows/deployment/update/waas-delivery-optimization) is a cloud-based, peer-to-peer technology to share content between Windows 10 devices. Starting in this release, configure Delivery Optimization to use your boundary groups when sharing content among peers. A new client setting applies the boundary group identifier as the Delivery Optimization group identifier on the client. When the client communicates with the Delivery Optimization cloud service, it uses this identifier to locate peers with the desired content. For more information, see [fundamental concepts for content management](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).

### Support for Windows 10 ARM64 devices
<!-- 1353704 -->
Starting in this release the Configuration Manager client is supported on Windows 10 ARM64 devices. Existing client management features should work with these new devices. For example, hardware and software inventory, software updates, and application management. Operating system deployment is currently not supported. 

### Improved support for CNG certificates
<!-- 1357314 -->
Configuration Manager (current branch) version 1710 supports [Cryptography: Next Generation (CNG) certificates](/sccm/core/plan-design/network/cng-certificates-overview). Version 1710 limits support to client certificates in several scenarios. 

Starting in this release, use CNG certificates for the following HTTPS-enabled server roles:
- Management point
- Distribution point
- Software update point

The list of [unsupported scenarios](/sccm/core/plan-design/network/cng-certificates-overview#unsupported-scenarios) remains the same.

### Boundary group fallback for management points
<!-- 1324594 -->
Configure fallback relationships for management points between [boundary groups](/sccm/core/servers/deploy/configure/boundary-groups). This behavior provides greater control for the management points that clients use. For more information, see [configure boundary groups](/sccm/core/servers/deploy/configure/boundary-groups#management-points).


### Cloud distribution point site affinity
<!--503719-->
This feature benefits customers with a multi-site, geographically-dispersed hierarchy using cloud distribution points. When an internet-based client searches for content, previously there was no order to the list of cloud distribution points received by the client. This behavior could result in internet-based clients receiving content from geographically-distant cloud distribution points. Downloading content from such a distant server is typically slower than a closer server.
 
With cloud distribution point site affinity, an internet-based client receives an ordered list. This list prioritizes cloud distribution points from the client's assigned site. This behavior allows the administrator to preserve their design intent for content downloads from site resources.
 



<!-- ## Migration  -->



## Client management

### Cloud management gateway support for Azure Resource Manager
<!-- 1324735 -->
When creating an instance of the [cloud management gateway](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG), the wizard now provides the option to create an **Azure Resource Manager deployment**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) is a modern platform for managing all solution resources as a single entity, called a [resource group](/azure/azure-resource-manager/resource-group-overview#resource-groups). When deploying CMG with Azure Resource Manager, the site uses Azure Active Directory (Azure AD) to authenticate and create the necessary cloud resources. This modernized deployment does not require the classic Azure management certificate. For more information, see [CMG requirements](/sccm/core/clients/manage/plan-cloud-management-gateway#requirements-for-cloud-management-gateway).

> [!IMPORTANT]
> This capability does not enable support for Azure Cloud Service Providers (CSP). The CMG deployment with Azure Resource Manager continues to use the classic cloud service, which the CSP does not support. For more information, see [available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  



<!-- ## Co-management -->



## Compliance settings

### Microsoft Edge browser policies
<!-- 1357310 -->
For customers who use the [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) web browser on Windows 10 clients, create a Configuration Manager compliance settings policy to configure several Microsoft Edge settings. For more information, see [create Microsoft Edge browser profile](/sccm/compliance/deploy-use/browser-profiles). 



## Application Management

### Allow user interaction when installing an application
<!-- 1356976 -->
Allow an end user to interact with an application installation during the running of the task sequence. For example, run a setup process that prompts the end user for various options. Some application installers can't silence user prompts, or the installation process may require specific configuration values only known to the user. This feature allows you to handle these installation scenarios. For more information, see [Specify user experience options for the deployment type](/sccm/apps/deploy-use/create-applications#specify-user-experience-options-for-the-deployment-type).

### Do not automatically upgrade superseded applications
<!-- 1351266 -->
Configure an application deployment to not automatically upgrade any superseded version. Now when creating the deployment, on the **Deployment Settings** page of the **Deploy Software Wizard**, for either **Available** or **Required** install purpose, you can enable or disable the option to **Automatically upgrade any superseded versions of this application**. For more information, see [Specify deployment settings](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings).

### Approve application requests for users per device
<!-- 1357015 -->
Starting in this release, when a user requests an application that requires approval, the specific device name is now a part of the request. If the administrator approves the request, the user is only able to install the application on that device. The user must submit another request to install the application on another device. For more information, see [Specify deployment settings](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings).



## Operating system deployment

### Windows 10 in-place upgrade task sequence via cloud management gateway
<!-- 1357149 -->
The Windows 10 [in-place upgrade task sequence](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version) now supports deployment to internet-based clients managed through the [cloud management gateway](/sccm/core/clients/manage/plan-cloud-management-gateway). This ability allows remote users to more easily upgrade to Windows 10 without needing to connect to the corporate network. For more information, see [deploy a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).

### Improvements to Windows 10 in-place upgrade task sequence
<!-- 1357425 -->
The default task sequence template for Windows 10 in-place upgrade now includes additional groups with recommended actions to add before and after the upgrade process. These actions are common among many customers who are successfully upgrading devices to Windows 10. For more information, see [create a task sequence to upgrade an OS](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

### Improvements to PXE-enabled distribution points
<!-- 1357580 -->
On the **PXE** tab of the distribution point properties, check **Enable a PXE responder without Windows Deployment Service**. This new option enables a PXE responder on the distribution point, which does not require Windows Deployment Services (WDS). Because WDS is not required, the PXE-enabled distribution point can be a client or server operating system, including Windows Server Core. This new PXE responder service supports IPv6, and also enhances the flexibility of PXE-enabled distribution points in remote offices. For more information, see [prepare distribution points for OS deployments](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments).

### Improvements to operating system deployment
This release includes the following improvements to operating system deployment:
 - In Windows PE, when launching cmtrace.exe, you are no longer prompted to choose whether to make this program the default viewer for log files. <!-- SMS 500897 -->
 - Add boot images to the [Download Package Content](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent) task sequence step.
 - Improvements to the [Run Task Sequence](/sccm/osd/understand/task-sequence-steps#child-task-sequence) step: <!-- 1261338 -->   
     - Support for all operating system deployment scenarios from Software Center, PXE, and media.
     - Improvements to console actions such as copy, import, export, and warning during object deletion.
     - Support for the [Create Prestaged Content File](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent) wizard.
     - Integration with deployment verification. For more information, see [high-risk task sequence deployments](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS). 
     - The Run Task Sequence step can now be used across multiple levels of task sequences, not just a single parent-child relationship. Multi-level relationships increase the complexity, so use with caution. These relationships are still checked for circular references.
    


## Software Center

### Install multiple applications in Software Center
<!-- 1357126 -->
If an end user or desktop technician needs to install multiple applications on a device, Software Center now supports installing multiple selected applications. This behavior allows the user to be more efficient while not waiting for one installation to finish before starting the next.

### Use Software Center to browse and install user-available applications on Azure AD-joined devices
<!-- 1322613 -->
If you deploy applications as available to users, they can now browse and install them through Software Center on Azure Active Directory (Azure AD) devices. <!-- For more information, see [](). -->




<!-- ## Software updates -->



## Reporting

### Report for default browser counts
<!-- 1357830 -->
Now there is a new report to show the count of clients with a specific web browser as the Windows default. See the **Default Browser counts** report in the **Software - Companies and Products** reports group. For more information, see the [list of reports](/sccm/core/servers/manage/list-of-reports#software---companies-and-products).

### Report on Windows AutoPilot device information
<!-- 1351442 -->
Windows AutoPilot is a solution for onboarding and configuring new Windows 10 devices in a modern way. For more information, see an [overview of Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). One method of registering existing devices with Windows AutoPilot is to upload device information to the Microsoft Store for Business and Education. This information includes the device serial number, Windows product identifier, and a hardware identifier. Use Configuration Manager to collect and report this device information with the new report, **Windows AutoPilot Device Information**, in the **Hardware - General** reports node. For more information, see [new Windows 10 devices](/sccm/core/clients/manage/co-management-prepare#new-windows-10-devices) in preparing for co-management.



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



<!-- ## Protect devices -->



## Configuration Manager console

### Improvements to the Configuration Manager console 
This release includes the following improvements to the Configuration Manager console.
- Device lists under Assets and Compliance, Devices, now display the primary user by default. This column only displays in the Devices node. The last logged on user can also be added as an optional column.<!-- 1357280 --> Enable [user and device affinity](/sccm/core/clients/deploy/about-client-settings#user-and-device-affinity) client settings for the site to associate a primary user with a device.
- If a collection is a member of another collection and it is renamed, then the new name is updated under membership rules.<!--1357282--> 
- When using remote control on a client with multiple monitors at different resolutions, the mouse cursor now correctly maps between them. <!--433170-->



## Next Steps
When you're ready to install this version, see [Updates for Configuration Manager](/sccm/core/servers/manage/updates).
