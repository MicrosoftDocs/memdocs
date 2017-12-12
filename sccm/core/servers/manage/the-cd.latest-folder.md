---
title: "The CD.Latest folder"
titleSuffix: "Configuration Manager"
description: "Learn about the new update process that delivers updates to the product from within the Configuration Manager console."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
caps.latest.revision: 6
author: mestew
ms.author: mstewart
manager: angrobe

---
# The CD.Latest folder for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager introduces a new update process which delivers updates to the product from within the Configuration Manager console. To support this new method of updating Configuration Manager, a new folder is created named **CD.Latest** that contains a copy of the Configuration Manager installation files for the updated version of your site.  

Beginning with update 1606, the CD.Latest folder contains a folder named **Redist** which contains the redistributable files that setup downloads and uses. These files are matched to the version of Configuration Manager files found in that CD.Latest folder. When you run Setup from a CD.Latest folder, you must use files that are matched to that version of Setup. To do so you can either direct Setup to download new and current files from Microsoft, or direct Setup to use the files from the Redist folder included in the CD.Latest folder.

However, baseline media, like the baseline version 1606 that released in October of 2016, does not include a Redist folder. The Redist folder will not be created until you install an in-console update. In the meantime, use the Redist folder that you used when installing sites from the baseline media.  

> [!TIP]
> If you have not yet installed version 1606, you must ensure redist files you use are current. If you have not downloaded redist files recently, plan to allow Setup to do so from Microsoft.   

 The following are scenarios that create or update the CD.Latest folder on a central administration site or primary site server:  

-   You install an update or hotfix from within the Configuration Manager console: The folder is created or updated in the Configuration Manager installation folder.  

-   You run the built-in Configuration Manager backup task: The folder is created or updated under the designated backup folder location.  

-  Beginning with version 1606, the CD.Latest folder is created when you install a new site using baseline media (like version 1606 or 1702).

The source files from the CD.Latest folder are supported for the following:  

1.  **Backup and recovery:** To recover a site, you must use the source files from a CD.Latest folder that matches your site. When you run a site backup using the built-in site backup task, the CD.Latest folder is included as part of the backup.

    -   **When you reinstall a site as part of a site recovery,** you install the site from the CD.Latest folder included in your backup. This installs the site using the file versions that match your site backup and site database.  If you do not have access the correct CD.Latest folder version, you can obtain a CD.Latest folder with the correct file versions by installing a site in a lab environment, and then updating that site to match the version you want to recover.

        > [!IMPORTANT]  
        >  If you do not have the correct CD.Latest folder and its contents available, you cannot recover a site and it must be reinstalled.  

    -   When you do not have a CD.Latest folder but do have a working child primary site or central administration site, you can use that site as a reference site for a site recovery.  

2.  **To install a child primary site:** When you want to install a new child primary site below a central administration site that has installed one or more in-console updates, you must use Setup and the source files from the CD.Latest folder from the central administration site. When Setup runs from a copy of the CD.Latest folder from the central administration site, it uses installation source files that match the version of the central administration site. For more information see [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  

3.  **To expand a stand-alone primary site:** When you are expanding a stand-alone primary site by installing a new central administration site, you must use Setup and the source files from the CD.Latest folder from the primary site to install the new central administration site. When run from a copy of the CD.Latest folder from the primary site, it uses installation source files that match the version of the primary site. For more information see [Expand a stand-alone primary site](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)) in [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)

> [!IMPORTANT]  
>  The updated CD.Latest source files are not supported for:  
>   
>  -   Installing a new site for a new hierarchy  
>  -   Upgrading a Microsoft System Center 2012 Configuration Manager site to System Center Configuration Manager
