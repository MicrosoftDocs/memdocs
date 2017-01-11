---
title: "Updates | Microsoft Docs"
description: "Learn about an in-console service method called **Updates and Servicing** that makes it easy to locate and install recommended updates."
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
caps.latest.revision: 51
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Updates for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager uses an in-console service method called **Updates and Servicing** that makes it easy to find and install recommended updates for your Configuration Manager infrastructure. This in-console servicing method is supplemented by out-of-band updates such as hotfixes that are intended for customers who need to resolve issues that might be specific to their environment.  

> [!TIP]
> When managing System Center Configuration Manager site and hierarchy infrastructure, the terms *upgrade*, *update*, and *install* are used to describe three separate concepts.. To learn how each term is used, see [About upgrade, update, and install](/sccm/core/understand/upgrade-update-install).


 **The following topics can help you understand how to find and install the different update types for System Center Configuration Manager:**  

-   [Install in-console updates for System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  

-   [Use the Service Connection Tool for System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [Use the Update Registration Tool to import hotfixes to System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [Use the Hotfix Installer to install updates for System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


If you use the Technical Preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview) for additional information that is specific to that branch.


##  <a name="bkmk_Baselines"></a> Baseline and update versions  
 The initial release of System Center Configuration Manager current branch is version 1511. This is a baseline version:  

-   Use the latest baseline version when you install a new site in a new hierarchy.  

-   You must use a baseline version to upgrade from System Center 2012 Configuration Manager.  

-   Periodically, new baseline versions will be released. When you use a newer baseline version to install a new hierarchy you avoid installing the original 1511 baseline followed by an upgrade of your infrastructure.  

After you install a baseline version, additional versions of Configuration Manager are available as in-console updates. In-console updates update your infrastructure to the latest version of Configuration Manager.  

-   You install in-console updates to update the version of your top-level site.  

-   Updates you install at central administration site will automatically install at child primary sites, unless blocked by a maintenance window you have configured at the primary site.  

-   You must manually update secondary sites to a new update version from within the console.  

When you install an update, the update stores installation files for that version on the site server in a folder named CD.Latest. See [The CD.Latest folder for System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md) for more information about these files.  

-   You use the files in the CD.Latest folder during site recovery and to install additional sites in a hierarchy that no longer runs a baseline version.  

-   You cannot use installation files from CD.Latest to install the first site of a new hierarchy, or to upgrade a site from System Center 2012 Configuration Manager.  

Some updates for Configuration Manager are available as both an in-console update version for existing infrastructure, and as a new baseline version.  

The following versions of Configuration Manager are available as a baseline, an update, or both:  

|Version|Availability date|Baseline|in-console update|  
|-------------|-----------------------|--------------|------------------------|  
|**1511**<br /><br /> 5.00.8325.1000|12/8/2015|Yes|No|  
|**1602**<br /><br /> 5.00.8355.1000|3/11/2016|No|Yes|
|**1606**<br /><br /> 5.00.8412.1000|7/22/2016|No|Yes|
|**1606** with the 1606 hotfix rollup (KB3186654) </br></br>5.00.8412.1307 *(Note 1)* |10/12/2016|Yes|No|
|**1610**<br /><br /> 5.00.8458.1000|11/18/2016|No|Yes|
*(Note 1)* This 1606 baseline media is available as part of Microsoft System Center 2016 or System Center Configuration Manager (Current Branch and Long-Term Servicing Branch 1606) release.

To check the version of your Configuration Manager site, in the console go to **About System Center Configuration Manager** at the top-left corner of the console where the new site and console version displays.  

##  <a name="bkmk_inconsole"></a> In-console updates and servicing  
 When you use a production ready installation of System Center Configuration Manager, also referred to as the current branch, most updates you install are available using the Updates and Servicing channel. This method identifies, downloads, and makes available the updates that apply to your current infrastructure version and configuration, and includes only updates that Microsoft recommends for all customers.   
 These include:  

-   New versions, like version 1602  

-   Updates, that include new features for your current version  

-   Hotfixes, for your version of Configuration Manager and that all customers should install  

The in-console updates deliver increased stability and resolve common issues. They replace the update types seen for previous product versions for service packs, cumulative updates, hotfixes that are applicable to all customers,  and Extension for Microsoft Intune. These updates can apply to one or more of the following:  

-   Primary and central administration site servers  

-   Site system roles and site system servers  

-   Instances of the SMS Provider  

-   Configuration Manager consoles  

-   Configuration Manager clients  

Configuration Manager discovers new updates for you when you synchronize your service connection point site system role with the Microsoft cloud service and download center:  

-   When your service connection point is in online mode, your site synchronizes with Microsoft every day to automatically identify new updates that apply to your infrastructure.  To download updates and redist files for updates, the computer that hosts the Service Connection Point site system role uses the **System** context to  access the following Internet locations: go.microsoft.com and download.microsoft.com. For information about additional locations the service connection point connects to, see [Internet access requirements](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls) in [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   When your service connection point is in offline mode, you use the service connection tool to manually sync with the Microsoft cloud. For more information, see [Use the Service Connection Tool for System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

-   In-console updates replace the need to independently locate and install individual updates, service packs, and new features.  

-   You install only the in-console updates you choose, and when installing some updates you can select the individual features you want to enable and use. For more information, see [Enable optional features from updates](../../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

When you install an in-console update:  

-   It automatically runs a prerequisite check. You can also run this check prior to starting the installation.  

-   It installs at the central administration site (if you have one), and at primary sites automatically. You can control when each primary site server is allowed to update its infrastructure by using [Service windows for site servers](../../../core/servers/manage/service-windows.md).  

-   After a site server updates, all affected site system roles (including instances of the SMS Provider) automatically update. Configuration Manager consoles also prompt the console user to update the console, after the site installs the update.  

-   If an update includes the Configuration Manager client, you are offered the option to test the update in pre-production, or to apply the update to all clients immediately.  

-   After a primary site is updated, secondary sites do not automatically update. Instead, you must initiate the secondary site update.  

> [!NOTE]  
>  The production release of System Center Configuration Manager (current branch), the Long-Term Servicing Branch, and the Technical Preview for System Center Configuration Manager are different releases. Therefore, updates that apply for one branch are not available as in-console updates for the other branches. For more information about available branches, see [Which branch of Configuration Manager should I use?](/sccm/core/understand/which-branch-should-i-use)

##  <a name="bkmk_outofband"></a> Out-of-band hotfixes  
Some hotfixes are released with limited availability to address specific issues, or are applicable to all customers but cannot be installed using the in-console method. These fixes are delivered out-of-band and not discovered from the Microsoft cloud service.  

Typically, you learn about out-of-band hotfixes from Microsoft customer support services, a Knowledge Base article, or from the [System Center Configuration Manager Team blog](https://blogs.technet.microsoft.com/configmgrteam) when you are seeking to fix or address a problem with your deployment of Configuration Manager.  

You install these fixes manually, using one of two methods:  

-   **Update Registration Tool:** This tool manually imports the hotfix into your Configuration Manager console where you can then install the update as you would in-console updates that are discovered automatically. This method is used for updates that use the following file name structure: **.update.exe**.  The full file name for this type of hotfix resembles: **&lt;Product\>-&lt;product version\>-&lt;KB article ID\>-ConfigMgr.Update.exe**.  

     For more information, see [Use the Update Registration Tool to import hotfixes to System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

-   **Hotfix Installer:** This tool is used to manually install a hotfix that cannot be installed using the in-console method. This method is used for fixes that use the following file name structure: **&lt;Product\>-&lt;product version\>-&lt;KB article ID\>-&lt;platform\>-&lt;language\>.exe**.

     For more information, see [Use the Hotfix Installer to install updates for System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md).
