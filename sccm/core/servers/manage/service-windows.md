---
title: "Service Windows"
description: "Use service windows to control when System Center Configuration Manager sites install updates."
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
caps.latest.revision: 4
caps.handback.revision: 0
author: Dougebyms.author: dougebymanager: angrobe

---
#  Service windows for site servers*Applies to: System Center Configuration Manager (Current Branch)*
You can configure service windows at central administration sites and primary sites to control when in-console updates can install.  You can configure multiple windows, with the window allowed for installing updates being determined by a combination of all service windows for that site server.

When no service window is configured:
- **On your top-tier site** (a central administration site or stand-alone primary site) you choose when to start the update installation.
- **On a child-primary site**, the update automatically installs after the update completes installation at the central administration site.
- **On a secondary site**, updates never start automatically. Instead, you must manually start the update installation from within the console, after the parent primary site has installed the update.

When a service window is configured:
- **On your top-tier site**, you will not be able to start the installation of any new update from within the Configuration Manager console. Even with a service window configured, the site automatically downloads updates so they are ready to install.  
- **On a child-primary site**, updates that have installed at a central administration site will download to the primary site, but do not automatically start. You cannot manually start the install of an update during a time that is blocked by use of a service window. At a time when service windows no longer block update installation, the update install automatically starts.
- **Secondary sites** do not support service windows, and do not automatically install updates. After the primary parent site of a secondary site installs an update, you can start the update of the secondary site from within the console.

## To configure a service window

1.  In  Configuration Manager console open **Administration** > **Site Configuration** > **Sites**, and then select the site server where you want to configure a service window.  

2.  Next, edit the site servers **Properties** and select the **Service Window** tab, where you can then set one or more service windows for that site server.  
