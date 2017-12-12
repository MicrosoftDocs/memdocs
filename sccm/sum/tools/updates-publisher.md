---
title: "Updates Publisher"
titleSuffix: "Configuration Manager"
description: "Use System Center Updates Publisher to manage custom updates"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
caps.latest.revision: 1
author: mestew
ms.author: mstewart
manager: angrobe
robots: NOINDEX, NOFOLLOW  
---
# System Center Updates Publisher

*Applies to: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) is a stand-alone tool that enables independent software vendors or line-of-business application developers to manage custom updates. This includes updates that have dependencies, like drivers and update bundles.

Using Updates Publisher, you can:

-   Import updates from external catalogs (non-Microsoft update catalogs).
-   Modify update definitions including applicability, and deployment metadata.
-   Export updates to external catalogs.
-   Publish updates to an update server.

After you publish updates to an update server, you can then use System Center Configuration Manager to detect and deploy those updates to your managed devices.

> [!TIP]  
> The previous version, [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/?LinkId=848111), remains in support. This updated version retains the same functionality, but supports additional operating systems, new features to simplify some tasks, and has an updated user interface.

## Workspaces
When you open Updates Publisher, it defaults to the Overview node of the *Updates Workspace.*

![Updates Publisher console](media/console1.png)   


Updates Publisher has four workspaces to help organize it.


**Updates Workspace:** Use this workspace to [create](/sccm/sum/tools/create-updates-with-updates-publisher) and [manage](/sccm/sum/tools/manage-updates-with-updates-publisher) software updates and update bundles. This includes assigning updates and bundles to a publication, publishing, and exporting to another Updates Publisher repository.

**Publications Workspace:** This is where you [manage publications](/sccm/sum/tools/updates-publisher-publications). A publication is group of updates you create to simplify the export and publishing of the updates.

Managing publications includes publishing updates to a server so your clients can find and install them, exporting updates and bundles for use by other Updates Publisher installations, or modifying the contents of or details of a publication.



**Rules Workspace:** Here is where you [manage applicability rules](/sccm/sum/tools/updates-publisher-applicability-rules) that can be saved and then used with updates you deploy. There are two types of rules:

-   Installable rules – These rules help determine if a client should install an update.
-   Installed rules – These rules verify if an update is already installed.

**Catalogs Workspace:** Use this workspace to add and [manage software update catalogs](/sccm/sum/tools/updates-publisher-catalogs). This includes the import of software updates from those catalogs to the Updates Publisher repository.
## First steps
To get started, first [install](/sccm/sum/tools/install-updates-publisher), and then [configure options](/sccm/sum/tools/updates-publisher-options) for Updates Publisher.
