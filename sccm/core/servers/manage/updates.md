---
title: "Updates"
titleSuffix: "Configuration Manager"
description: "Learn about an in-console service method called **Updates and Servicing** that makes it easy to locate and install recommended updates."
ms.custom: na
ms.date: 11/20/2017
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
author: mstewart
ms.author: mstewart
manager: angrobe

---
# Updates for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager uses an in-console service method called **Updates and Servicing**. This in-console method makes it easy to find and install recommended updates for your Configuration Manager infrastructure. In-console servicing is supplemented by out-of-band updates such as hotfixes that are intended for customers who need to resolve issues that might be specific to their environment.  

> [!TIP]  
> When managing System Center Configuration Manager site and hierarchy infrastructure, the terms *upgrade*, *update*, and *install* are used to describe three separate concepts. To learn how each term is used, see [About upgrade, update, and install](/sccm/core/understand/upgrade-update-install).


 **The following topics can help you understand how to find and install the different update types for System Center Configuration Manager:**  

-   [Install in-console updates for System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  

-   [Use the Service Connection Tool for System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [Use the Update Registration Tool to import hotfixes to System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [Use the Hotfix Installer to install updates for System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


If you use the Technical Preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview) for additional information that is specific to that branch.


##  <a name="bkmk_Baselines"></a> Baseline and update versions  
 The first release of System Center Configuration Manager current branch was version 1511, which was a baseline version. More recent baseline versions include version 1606, and 1702:

-   Use the latest baseline version when you install a new site in a new hierarchy.  

-   You use a baseline version to upgrade from System Center 2012 Configuration Manager. After upgrading to System Center Configuration Manager, you can no longer use baseline versions to stay current and instead only use [in-console updates](/sccm/core/servers/manage/install-in-console-updates) to update to the newest version.  

-   Periodically, additional baseline versions are released. When you use the latest baseline version to install a new hierarchy, you avoid installing an outdated version of Configuration Manager followed by an additional upgrade of your infrastructure to bring it up to date.  

After you install a baseline version, additional versions of Configuration Manager are available as in-console updates. In-console updates update your infrastructure to the latest version of Configuration Manager.  

-   You install in-console updates to update the version of your top-level site.  

-   Updates you install at central administration site automatically install at child primary sites, unless blocked by a maintenance window you have configured at the primary site.  

-   You manually update secondary sites to a new update version from within the console.  

When you install an update, the update stores installation files for that version on the site server in a folder named CD.Latest. For more information about these files, see [The CD.Latest folder for System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md).  

-   You use the files in the CD.Latest folder during Site Recovery and to install additional sites in a hierarchy that no longer runs a baseline version.  

-   You cannot use installation files from CD.Latest to install the first site of a new hierarchy, or to upgrade a site from System Center 2012 Configuration Manager.  

Some updates for Configuration Manager are available as both an in-console update version for existing infrastructure, and as a new baseline version.  

The following versions of Configuration Manager are available as a baseline, an update, or both:  

|Version |Availability date|[Support end date](/sccm/core/servers/manage/current-branch-versions-supported) |Baseline|in-console update|  
|-------------|-----------|------------|--------------|------------------------|  
|[1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)<br /><br /> 5.00.8577.1000|November 20, 2017|May 20, 2019|No|Yes|
|[1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)<br /><br /> 5.00.8540.1000|July 31, 2017|July 31, 2018|No|Yes|
|[1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)<br /><br /> 5.00.8498.1000|March 27, 2017| March 27, 2018|Yes|Yes|
|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)<br /><br /> 5.00.8458.1000|November 18, 2016| November 18, 2017|No|Yes|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)<br /><br /> 5.00.8412.1000|July 22, 2016| July 22, 2017|No|Yes|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606) with the 1606 hotfix rollup (KB3186654) </br></br>5.00.8412.1307 *(Note 1)* |October 12, 2016| October 12, 2017|Yes|No|
| 1602<br /><br /> 5.00.8355.1000|March 11, 2016| March 11, 2017|No|Yes|
| 1511 <br /><br /> 5.00.8325.1000|December 8, 2015| December 8, 2016|Yes|No|  


*(Note 1)* The 1606 and 1702 baseline media are available as part of the Microsoft System Center 2016 or System Center Configuration Manager (Current Branch and Long-Term Servicing Branch) releases on the [Volume License Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC). For example, on the VLSC you can search for *System Center Config Mgr (current branch and LTSB)*, and both 1606 and 1702 version baseline media are returned, and available for download.

To check the version of your Configuration Manager site, in the console go to **About System Center Configuration Manager** at the top-left corner of the console where the new site and console version displays.  

##  <a name="bkmk_inconsole"></a> In-console updates and servicing  
 When you use a production ready installation of System Center Configuration Manager, also referred to as the current branch, most updates you install are available using the Updates and Servicing channel. This method identifies, downloads, and makes available the updates that apply to your current infrastructure version and configuration, and includes only updates that Microsoft recommends for all customers.   
 These include:  

-   New versions, like version 1610, 1702, or 1706.  

-   Updates, that include new features for your current version.

-   Hotfixes, for your version of Configuration Manager and that all customers should install.

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
Some hotfixes release with limited availability to address specific issues, or are applicable to all customers but cannot install using the in-console method. These fixes are delivered out-of-band and not discovered from the Microsoft cloud service.  

Typically, you learn about out-of-band hotfixes from Microsoft customer support services, a Knowledge Base article, or from the [System Center Configuration Manager Team blog](https://blogs.technet.microsoft.com/configmgrteam) when you are seeking to fix or address a problem with your deployment of Configuration Manager.  

You install these fixes manually, using one of two methods:  

-   **Update Registration Tool:** This tool manually imports the hotfix into your Configuration Manager console where you can then install the update as you would in-console updates that are discovered automatically. This method is used for updates that use the following file name structure: **.update.exe**.  The full file name for this type of hotfix resembles: **&lt;Product\>-&lt;product version\>-&lt;KB article ID\>-ConfigMgr.Update.exe**.  

     For more information, see [Use the Update Registration Tool to import hotfixes to System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

-   **Hotfix Installer:** This tool is used to manually install a hotfix that cannot be installed using the in-console method. This method is used for fixes that use the following file name structure: **&lt;Product\>-&lt;product version\>-&lt;KB article ID\>-&lt;platform\>-&lt;language\>.exe**.

     For more information, see [Use the Hotfix Installer to install updates for System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md).
