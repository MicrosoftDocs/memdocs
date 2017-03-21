---
title: "New version 1702 | Microsoft Docs"
description: "Get details about changes and new capabilities introduced in version 1702 of System Center Configuration Manager."
ms.custom: na
ms.date:  03/27/2017
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: Brenduns
ms.author: brenduns
manager: angrobe
ROBOTS: "NOINDEX, NOFOLLOW"
---
# What&#39;s new in version 1702 of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1702 for System Center Configuration Manager current branch is available as an in-console update for previously installed sites that run version 1606 or 1610. It is also available as a baseline version you can use when installing a new deployment.
-
> [!TIP]  
> To install a new site, you must use a baseline version of Configuration Manager.  
>  Learn more about:    
>  -   [Installing new sites](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [Installing updates at sites](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

The following sections provide details about changes and new capabilities introduced in version 1702 of Configuration Manager.  

## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated features](/sccm/core/plan-design/changes/removed-and-deprecated-features).

Version 1702 drops support for the following products:
- **SQL Server 2008 R2**, for site database servers. Deprecation of support was [first announced](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-support-for-sql-server-versions-as-a-site-database) on July 10,2015. This version of SQL Server remains supported when you use a Configuration Manager version prior to version 1702.
- **Windows Server 2008 R2**, for site system servers and most site system roles. Deprecation of support was [first announced](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) on July 10,2015. This version of Windows remains supported when you use a Configuration Manager version prior to version 1702.  
- **Windows Server 2008**,for site system servers and most site system roles. Deprecation of support was [first announced](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) on  July 10,2015.
- **Windows XP Embedded**, as a client operating system. Deprecation was [first announced](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) on  July 10,2015. This version of Windows remains supported when you use a Configuration Manager version prior to version 1702.




## Site infrastructure

### Improvements for in-console search
The following are improvements to using search in the Configuration Manager console:
 - **Object Path:**  
  Many objects now support a column named **Object Path**.  When you search and include this column in your display results, you can view the path to each object. For example, if you run a search for apps in the Applications node and are also searching sub-nodes, the *Object Path* column in the results pane will show you the path to each object that is returned.   

- **Preservation of search text:**  
  When you enter text into the search text box, and then switch between searching a sub-node and the current node, the text that you typed will now persist and remain available for a new search without having to reenter it.

- **Preservation of your decision to search sub-nodes:**  
 The option that you choose for searching the *current node* or *all sub-nodes* now persists when you change the node you are working in. This new behavior means that you do not need to constantly reset this decision as you move around the console. By default, when you open the console the option is to search only the current node.


### Send feedback from the Configuration Manager console

 You can use the in-console feedback options to send feedback directly to the development team.

 You can find the **Feedback** option:
 -  In the ribbon, at the far left of the Home tab of each node.  
    ![Ribbon](./media/feedback-home.png)

 -  When you right-click on any object in the console.   
     ![Righ-click option](./media/feedback-option.png)   

 Choosing **Feedback** opens your browser to the [Configuration Manager UserVoice feedback website](https://go.microsoft.com/fwlink/?linkid=617029).


###  Changes for Updates and Servicing
The following are changes for Updates and Servicing:

- **Node location**   
  After installing version 1702, the **Updates and Servicing** node appears as a top-level node under **Administration**. It is no longer a child node below **Cloud Services**.

- **New update states**  
  When you view available updates in the console, there are two new states:  
  - **Available for install** - This is an update that has been downloaded and ready to install.
  - **Ready for download**  - This update is available, but has not been downloaded. You can choose to download this update, but it has been superseded by a more recent update.


- **Simpler update choices**  
  The next time your infrastructure qualifies for two or more updates, only the latest update is downloaded. For example, if your current site version is two or more older than the most recent version that is available, only that most recent update version is downloaded automatically.  

  You can choose to download and install the other available updates, even when they are not the most current version. If you download an older update, you will receive a warning that the update has been replaced by a newer one. To download an update that is *Available to Download*, select the update in the console and then click **Download**.

- **Improved cleanup of older updates**   
  We added an automatic clean-up function that deletes the unneeded downloads from the ‘EasySetupPayload’ folder on your site server.  


### Data Warehouse service point
 Use the Data Warehouse service point to store and report on long-term historical data for your Configuration Manager deployment.

 The data warehouse supports up to 2 TB of data, with timestamps for change tracking. Storage of data is accomplished by automated synchronizations from the Configuration Manager site database to the data warehouse database. This information is then accessible from your Reporting Services point.

 For more information, see [The Data Warehouse service point](/sccm/core/servers/manage/data-warehouse).


### Peer Cache improvements
 Beginning with version 1702, a peer cache source computer will reject a request for content when the peer cache source computer meets any of the following conditions:  
  -  Is in low battery mode.
  -  CPU load exceeds 80% at the time the content is requested.
  -  Disk I/O has an *AvgDiskQueueLength* that exceeds 10.
  -  There are no more available connections to the computer.   
For more information, see **Limited access to a peer cache source** in [Peer Cache for Configuration Manager clients](/sccm/core/plan-design/hierarchy/client-peer-cache).   

Additionally, three new reports are added to your reporting point. You can use these reports to understand more details about rejected content requests, including which boundary group, computer, and content was involved. See [Monitoring](/sccm/core/plan-design/hierarchy/client-peer-cache#monitoring) in the peer cache topic.

### Content library cleanup tool
 Use the [content library cleanup tool](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) to remove content from distribution points when that content is no longer associated with an application.


### Use the OMS connector with the Azure Government cloud
You can use the OMS connector to connect to OMS Log Analytics in Microsoft Azure Government cloud. This requires you to modify a configuration file before you install the OMS connector so that the connector can work with the Government cloud. For more information, see [Use the OMS connector with the Azure Government cloud](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig).

### Software update points are added to boundary groups
Beginning with version 1702, clients use boundary groups to find a new software update point, and to fallback and find a new software update point if their current one is no longer accessible. You can add individual software update points to different boundary groups to control which servers a client can find. For more information, see [software update points](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) in the [configuring boundary groups](/sccm/core/servers/deploy/configure/boundary-groups) topic.

## Protect data and infrastructure

- If you intend to store certificate profiles in the Windows Hello for Business key container, and the certificate profile uses the Smart Card Logon EKU, you must configure permissions for key registration to ensure the certificate is validated correctly.
For more information, see [Windows Hello for Business settings](/sccm/protect/deploy-use/windows-hello-for-business-settings).



<!-- ## Migration  -->

<!-- ## Client management  -->

<!-- ## Compliance settings  -->

<!-- ## Application Management   -->

## Operating system deployment

### Expire stand-alone media
When you create standalone media, there are new options to set optional start and expiration dates on the media. These settings are disabled by default. The dates are compared to the system time on the computer before the stand-alone media runs. When the system time is earlier than the start time or later than the expiration time, the stand-alone media is not started. These options are also available by using the New-CMStandaloneMedia PowerShell cmdlet. For details, see [Create stand-alone media](/sccm/osd/deploy-use/create-stand-alone-media).

### Package ID displayed in task sequence steps
Any task sequence step that references a package, driver package, operating system image, boot image, or operating system upgrade package will now display the package ID of the referenced object. When a task sequence step references an application it will display the object ID.

### Support for additional content in stand-alone media
Additional content is now supported in stand-alone media. You can select additional packages, driver packages, and applications to be staged on the media along with the other content referenced in the task sequence. Previously, only content referenced in the task sequence was staged on stand-alone media. For details, see [Create stand-alone media](/sccm/osd/deploy-use/create-stand-alone-media).

## Hardware inventory collects UEFI information
A new hardware inventory class (**SMS_Firmware**) and property (**UEFI**) are available to help you determine whether a computer starts in UEFI mode. When a computer is started in UEFI mode, the **UEFI** property is set to **TRUE**. This is enabled in hardware inventory by default. For more information about hardware inventory, see [How to configure hardware inventory](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## Improvements to Software Center settings and notification messages for high-impact task sequences
This release includes the following improvements to Software Center settings and notification messages for high-impact deployment task sequences:

- In the properties for the task sequence, you can now configure any task sequence, including non-operating system task sequences, as a high-risk deployment. Any task sequence that meets certain conditions is automatically defined as high-impact. For details, see [Manage high-risk deployments](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).
- In the properties for the task sequence, you can choose to use the default notification message or create your own custom notification message for high-impact deployments.
- In the properties for the task sequence, you can configure Software Center properties, which include make a restart required, the download size of the task sequence, and the estimated run time.
- The default high-impact deployment message for in-place upgrades now states that
your apps, data, and settings are automatically migrated. Previously, the default message for any operating system installation indicated that all apps, data, and settings would be lost, which was not true for an in-place upgrade.

For details, see [Configure high-impact task sequence settings](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)






## Improvements to operating system deployment
Beginning in version 1702, the following improvements to operating system deployment are available:
- Increased the maximum number of applications that you can install to 99 in the **Install Applications** task sequence step. The previous maximum number was 9 applications.
- When you add applications to the **Install Applications** task sequence step in the task sequence editor, you can now select multiple applications from the **Select the application to install** pane.
- [**Expire standalone media**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media): When you create standalone media, there are new options to set optional start and expiration dates on the media. These settings are disabled by default. The dates are compared to the system time on the computer before the stand-alone media runs. When the system time is earlier than the start time or later than the expiration time, the stand-alone media is not started. These options are also available by using the New-CMStandaloneMedia PowerShell cmdlet.

- [**Configurable timeout for Auto Apply Driver task sequence step**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout): New task sequence variables are now available to configure the timeout value on the Auto Apply Driver task sequence step when making HTTP catalog requests. The following variables and default values (in seconds) are available:
   - SMSTSDriverRequestResolveTimeOut
     Default: 60
   - SMSTSDriverRequestConnectTimeOut
     Default: 60
   - SMSTSDriverRequestSendTimeOut
     Default: 60
   - SMSTSDriverRequestReceiveTimeOut
     Default: 480
- [**Package ID is now displayed in task sequence steps**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste): Any task sequence step that references a package, driver package, operating system image, boot image, or operating system upgrade package will now display the package ID of the referenced object. When a task sequence step references an application it will display the object ID.
- **Windows 10 ADK tracked by build version**: The Windows 10 ADK is now tracked by build version to ensure a more supported experience when customizing Windows 10 boot images. For example, if the site uses the Windows ADK for Windows 10, version 1607, only boot images with version 10.0.14393 can be customized in the console. For details about customizing WinPE versions, see [Customize boot images](/sccm/osd/get-started/customize-boot-images).
- **Default boot image source path can no longer be changed**: Default boot images are managed by Configuration Manager and the default boot image source path can no longer be changed in the Configuration Manager console or by using the Configuration Manager SDK. You can continue to configure a custom source path for custom boot images.


### Pre-cache content for available deployments and task sequences
Beginning in version 1702, for available deployments and task sequences, you can choose to use the pre-cache feature to have clients download only relevant content before a user installs the content.

For example, let's say you want to deploy a Windows 10 in-place upgrade task sequence, only want a single task sequence for all users, and have multiple architectures and/or languages. In Current Branch, if you create an available deployment, and then the user clicks **Install** in Software Center, the content downloads at that time. This adds additional time before the installation is ready to start. Alternatively, in Current Branch if you create an available task sequence deployment, all content referenced in the task sequence is downloaded. This includes the operating system upgrade package for all languages and architectures. If each is roughly 3 GB in size, the download package can be quite large.

The pre-cache content feature gives you the option to allow the client to only download the applicable content as soon as it receives the deployment. Therefore, when the user clicks **Install** in Software Center, the content is ready and the installation starts quickly because the content is on the local hard drive.

#### To configure the pre-cache feature

1. Create operating system upgrade packages for specific architectures and languages. Specify the architecture and language on the **Data Source** tab of the package. For the language, use the decimal conversion (for example, 1033 is the decimal for English and 0x0409 is the hexadecimal equivalent). For details, see [Create a task sequence to upgrade an operating system](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    The architecture and language values are used to match task sequence step conditions that you will create in the next step to determine whether the operating system upgrade package should be pre-cached.
2. Create a task sequence with conditional steps for the different languages and architectures. For example, for the English version you could create a step like the following:

    ![pre-cache properties](media/precacheproperties2.png)

    ![pre-cache options](media/precacheoptions2.png)  

3. Deploy the task sequence. For the pre-cache feature, configure the following:
    - On the **General** tab, select **Pre-download content for this task sequence**.
    - On the **Deployment settings** tab, configure the task sequence with the **Available** for **Purpose**. If you create a **Required** deployment, the pre-cache functionality will not work.
    - On the **Scheduling** tab, for the **Schedule when this deployment will be available** setting, choose a time in the future that gives clients enough time to pre-cache the content before the deployment is made available to users. For example, you can set the available time to be 3 hours in the future to allow enough time for the content to be pre-cached.  
    - On the **Distribution Points** tab, configure the **Deployment options** settings. If the content is not pre-cached on a client before a user starts the installation, these settings are used.


#### User experience
- When the client receives the deployment policy, it will start to pre-cache the content. This includes all referenced content (any other package types) and only the operating system upgrade package that matches the client based on the conditions that you set in the task sequence.
- When the deployment is made available to users (setting on the **Scheduling** tab of the deployment), a notification displays to inform users about the new deployment and the deployment becomes visible in Software Center. The user can go to Software Center and click **Install** to start the installation.
- If the content is not fully pre-cached, then it will use the settings specified on the **Deployment Option** tab of the deployment. We recommend that there is sufficient time between when the deployment is created and the time in which the deployment becomes available to users to allow clients enough time to pre-cache the content.

<!-- ## Software updates  -->


### Deploy Office 365 apps to clients
Beginning in version 1702, from the Office 365 Client Management dashboard, you can start the Office 365 Installer that lets you configure Office 365 installation settings, download files from Office Content Delivery Networks (CDNs), and deploy the files as an application in Configuration Manager. For details, see [Manage Office 365 ProPlus updates](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).

> [!IMPORTANT]
> The Office 365 app that you create and deploy by using the Office 365 Application Wizard in Configuration Manager is not automatically managed by Configuration Manager until you enable the **Enable management of the Office 365 Client Again** software updates client agent setting. For details, see [About client settings](/sccm/core/clients/deploy/about-client-settings).

<!-- ## Reporting  -->

<!-- ## Inventory  -->

<!-- ## Mobile device management - on-premises and hybrid  -->


