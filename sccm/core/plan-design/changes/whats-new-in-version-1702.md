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


**Support is dropped in version 1702 for the following products:**
- **SQL Server 2008 R2**, for site database servers. Deprecation of support was [first announced](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-support-for-sql-server-versions-as-a-site-database) on July 10,2015. This version of SQL Server remains supported when you use a Configuration Manager version prior to version 1702.
- **Windows Server 2008 R2**, for site system servers and most site system roles. Deprecation of support was [first announced](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) on July 10,2015. This version of Windows remains supported when you use a Configuration Manager version prior to version 1702.  
- **Windows Server 2008**,for site system servers and most site system roles. Deprecation of support was [first announced](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) on  July 10,2015.
- **Windows XP Embedded**, as a client operating system. Deprecation was [first announced](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) on  July 10,2015. This version of Windows remains supported when you use a Configuration Manager version prior to version 1702.


The following sections provide details about changes and new capabilities introduced in version 1702 of Configuration Manager.  



## Improvements for in-console search
The following are improvements to using search in the Configuration Manager console:
 - **Object Path:**  
  Many objects now support a column named **Object Path**.  When you search and include this column in your display results, you can view the path to each object. For example, if you run a search for apps in the Applications node and are also searching sub-nodes, the *Object Path* column in the results pane will show you the path to each object that is returned.   

- **Preservation of search text:**  
  When you enter text into the search text box, and then switch between searching a sub-node and the current node, the text that you typed will now persist and remain available for a new search without having to reenter it.

- **Preservation of your decision to search sub-nodes:**  
 The option that you choose for searching the *current node* or *all sub-nodes* now persists when you change the node you are working in. This new behavior means that you do not need to constantly reset this decision as you move around the console. By default, when you open the console the option is to search only the current node.


## Send feedback from the Configuration Manager console

 You can use the in-console feedback options to send feedback directly to the development team.

 You can find the **Feedback** option:
 -  In the ribbon, at the far left of the Home tab of each node.  
    ![Ribbon](./media/feedback-home.png)

 -  When you right-click on any object in the console.   
     ![Righ-click option](./media/feedback-option.png)   

 Choosing **Feedback** opens your browser to the [Configuration Manager UserVoice feedback website](https://go.microsoft.com/fwlink/?linkid=617029).



##  Changes for Updates and Servicing
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


## Data Warehouse service point
 Use the Data Warehouse service point to store and report on long-term historical data for your Configuration Manager deployment.

 The data warehouse supports up to 2 TB of data, with timestamps for change tracking. Storage of data is accomplished by automated synchronizations from the Configuration Manager site database to the data warehouse database. This information is then accessible from your Reporting Services point.

 For more information, see [The Data Warehouse service point](/sccm/core/servers/manage/data-warehouse).


## Peer Cache improvements
 Beginning with version 1702, a peer cache source computer will reject a request for content when the peer cache source computer meets any of the following conditions:  
  -  Is in low battery mode.
  -  CPU load exceeds 80% at the time the content is requested.
  -  Disk I/O has an *AvgDiskQueueLength* that exceeds 10.
  -  There are no more available connections to the computer.   
For more information, see **Limited access to a peer cache source** in [Peer Cache for Configuration Manager clients](/sccm/core/plan-design/hierarchy/client-peer-cache).   

Additionally, three new reports are added to your reporting point. You can use these reports to understand more details about rejected content requests, including which boundary group, computer, and content was involved. See [Monitoring](/sccm/core/plan-design/hierarchy/client-peer-cache#monitoring) in the peer cache topic.

## Content library cleanup tool
 Use the [content library cleanup tool](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) to remove content from distribution points when that content is no longer associated with an application.


## Use the OMS connector with the Azure Government cloud
You can use the OMS connector to connect to OMS Log Analytics in Microsoft Azure Government cloud. This requires you to modify a configuration file before you install the OMS connector so that the connector can work with the Government cloud. For more information, see [Use the OMS connector with the Azure Government cloud](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig).

## Software update points are added to boundary groups
Beginning with version 1702, clients use boundary groups to find a new software update point, and to fallback and find a new software update point if their current one is no longer accessible. You can add individual software update points to different boundary groups to control which servers a client can find. For more information, see [software update points](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) in the [configuring boundary groups](/sccm/core/servers/deploy/configure/boundary-groups) topic.
