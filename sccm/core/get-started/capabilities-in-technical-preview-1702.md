---
title: "Capabilities in Technical Preview 1702 Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1702."
ms.custom: na
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
caps.latest.revision: 5
author: Brendunsms.author: brendunsmanager: angrobe
---
# Capabilities in Technical Preview 1702 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*



This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1702. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  

##  Send feedback from the Configuration Manager console
This preview introduces new feedback options in the Configuration Manager console. The Feedback options lets you send feedback directly to the development team, by way of the Configuration Manager UserVoice feedback website.  

You can find the **Feedback** option:
-  In the ribbon, at the far left of the Home tab of each node.  
   ![Ribbon](./media/feedback-home.png)

-  When you right-click on any object in the console.   
    ![Righ-click option](./media/feedback-option.png)   

Choosing **Feedback** opens your browser to the Configuration Manager UserVoice feedback website, at https://configurationmanager.uservoice.com/forums/300492-ideas.

##  Changes for Updates and Servicing
The following are introduced with this preview.

**Simpler update choices**  
The next time your infrastructure qualifies for two or more updates, only the latest update is downloaded. For example, if your current site version is two or more older than the most recent version that is available, only that most recent update version is downloaded automatically.  

You have the option to download and install the other available updates, even when they are not the most current version, however you will receive a warning that the update has been replaced by a newer one. To download additional updates, select the update in the console and then click Download

**Improved cleanup of older updates**   
We added an automatic clean-up function that deletes the unneeded downloads from the ‘EasySetupPayload’ folder on your site server.  


## Peer Cache improvements
Starting with this release, a peer cache source computer will reject a request for content when the source computer meets any of the following conditions:
 - Low battery
 - Excessive CPU load
 - Excessive disk I/O
 - No connections to the computer are available

When the computer rejects a request for the content, the computer seeking content will attempt the next alternate source in its pool of available content source locations.  

In addition to this behavior, a new report is available to provide more details about peer cache request rejections:
