---
title: "Upgrade an Evaluation install of System Center Configuration Manager to a Full install"
ms.custom: na
ms.date: 07/22/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
caps.latest.revision: 3
author: Brenduns
---
# Upgrade an Evaluation install of System Center Configuration Manager to a Full install


 If you installed System Center Configuration Manager as an evaluation version, after 180 days the Configuration Manager console becomes read-only until you activate the product from the **Site Maintenance** page in Setup. At any time before or after the 180 day period, you have the option to upgrade an evaluation installation to a full installation.  

> [!NOTE]  
>  When you connect a Configuration Manager console to an evaluation installation of Configuration Manager, the title bar of the console displays the number of days that remain before the evaluation installation expires. The number of days does not automatically refresh and only updates when you make a new connection to a site.  

 **You can upgrade the following sites that run an Evaluation installation:**  

-   Central administration site  

-   Primary site  

Because secondary sites are not treated as evaluation installations, you do not need to modify a secondary site after its primary parent site upgrades to a full installation.  

**Prerequisites to upgrade an Evaluation edition to a Full edition:**  

-   You must have a valid product to use during the upgrade  

-   Your account must have **administrator** permissions to the computer where the site is installed  

### To upgrade an evaluation edition of Configuration Manager to a licensed edition  

1.  On the site server, locate and run  **SETUP.exe** (Configuration Manager setup)  from the Configuration Manager installation folder (**%path%\BIN\X64**).  You must run the copy of Setup that is located on the site server in the Configuration Manager folder because site maintenance options are not available when you run Setup from installation media.  

2.  On the **Before You Begin** page, click **Next**.  

3.  On the **Getting Started** page, select **Perform site maintenance or reset the Site**, and then click **Next**.  

4.  On the **Site Maintenance** page, select **Upgrade the evaluation edition to a licensed edition**, enter a valid product key, and then click **Next**.  

5.  On the **Microsoft Software License Terms** page, read and accept the license terms, and then click **Next**.  

6.  On the **Configuration** page, click **Close** to complete the wizard.  

    > [!NOTE]  
    >  The title bar of Configuration Manager consoles that remain  connected to the site that you  upgrade might indicate that the site is still an evaluation version until you reconnect the console to the site.  

