---
title: "Upgrade evaluation installs"
titleSuffix: "Configuration Manager"
description: "Learn how to upgrade an evaluation installation to a full installation of System Center Configuration Manager."
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Upgrade an evaluation installation of System Center Configuration Manager to a full installation

*Applies to: System Center Configuration Manager (Current Branch)*

If you installed System Center Configuration Manager as an evaluation version, after 180 days, the Configuration Manager console becomes read-only until you activate the product from the **Site Maintenance** page in Setup. At any time before or after the 180-day period, you have the option to upgrade an evaluation installation to a full installation.  

> [!NOTE]  
>  When you connect a Configuration Manager console to an evaluation installation of Configuration Manager, the console title bar displays the number of days that remain until the evaluation installation expires. The number of days does not automatically refresh and it only updates when you make a new connection to a site.  

 You can upgrade the following sites that run an evaluation installation:  

-   Central administration site  
-   Primary site  

Because secondary sites are not treated as evaluation installations, you do not need to modify a secondary site after its primary parent site upgrades to a full installation.  

Prerequisites to upgrading an evaluation version to a licensed version:  

-   You must have a valid product to use during the upgrade.  
-   Your account must have **Administrator** rights on the computer where the site is installed.  

### To upgrade an evaluation version of Configuration Manager to a licensed version  

1.  On the site server, run **Setup.exe** (Configuration Manager setup) from the Configuration Manager installation folder (**%path%\BIN\X64**). You must run the copy of Setup that is located on the site server in the Configuration Manager folder because site maintenance options are not available when you run Setup from installation media.  
2.  On the **Before You Begin** page, select **Next**.  
3.  On the **Getting Started** page, select **Perform site maintenance or reset the Site**, and then select **Next**.  
4.  On the **Site Maintenance** page, select **Upgrade the evaluation edition to a licensed edition**, enter a valid product key, and then select **Next**.  
5.  On the **Microsoft Software License Terms** page, read and accept the license terms, and then select **Next**.  
6.  On the **Configuration** page, select **Close** to complete the wizard.  

    > [!NOTE]  
    >  The title bar of a Configuration Manager console that remains connected to the site that you upgrade might indicate that the site is still an evaluation version until you reconnect the console to the site.  
