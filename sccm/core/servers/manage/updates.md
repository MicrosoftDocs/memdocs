---
title: Updates and servicing
titleSuffix: Configuration Manager
description: Learn about the in-console service method called Updates and Servicing that makes it easy to locate and install recommended updates.
ms.date: 11/16/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Updates and servicing for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager uses an in-console service method called **Updates and Servicing**. This in-console method makes it easy to find and install recommended updates for your Configuration Manager infrastructure. In-console servicing is supplemented by out-of-band updates such as hotfixes. The out-of-band updates are intended for customers who need to resolve issues that might be specific to their environment.  

> [!TIP]  
> The terms *upgrade*, *update*, and *install* are used to describe three separate concepts in Configuration Manager. For more information about how each term is used, see [About upgrade, update, and install](/sccm/core/understand/upgrade-update-install).  



##  <a name="bkmk_Baselines"></a> Baseline and update versions  

Use the latest baseline version when you install a new site in a new hierarchy. 
- Also use a baseline version to upgrade from System Center 2012 Configuration Manager.  

- After upgrading to Configuration Manager current branch, don't use baseline versions to stay current. Instead, only use [in-console updates](/sccm/core/servers/manage/install-in-console-updates) to update to the newest version.  

- Periodically, additional baseline versions are released. When you use the latest baseline version to install a new hierarchy, you avoid installing an outdated or unsupported version of Configuration Manager, followed by an additional upgrade of your infrastructure to bring it up-to-date.  

After you install a baseline version, additional versions of Configuration Manager are available as in-console updates. In-console updates update your infrastructure to the latest version of Configuration Manager.  

-   You install in-console updates to update the version of your top-level site.  

-   Updates you install at the central administration site automatically install at child primary sites. Control this timing by using a maintenance window at the primary site.  

-   Manually update secondary sites to a new update version from within the console.  

When you install an update, the update stores installation files for that version on the site server in a folder named **CD.Latest**. For more information about these files, see [The CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder).  

-   Use the files in the CD.Latest folder during site recovery. Also, when your hierarchy no longer runs a baseline version, use these files to install additional sites.  

-   You can't use installation files from CD.Latest to install the first site of a new hierarchy, or to upgrade a site from System Center 2012 Configuration Manager.  


### Version details

Some updates for Configuration Manager are available as both an in-console update version for existing infrastructure, and as a new baseline version.  

#### Supported versions
The following supported versions of Configuration Manager are currently available as a baseline, an update, or both:  

| Version | Availability date | [Support end date](/sccm/core/servers/manage/current-branch-versions-supported) | Baseline | In-console update |  
|-------------|-----------|------------|--------------|------------------------|  
| [1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)<br /><br /> 5.00.8740.1000 | November 26, 2018 | May 26, 2020 | No | Yes |
| [1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)<br /><br /> 5.00.8692.1000 | July 31, 2018 | January 31, 2020 | No | Yes |
| [1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)<br /><br /> 5.00.8634.1000 | March 22, 2018 | September 22, 2019 | Yes<sup>[Note 1](#bkmk_note1)</sup> | Yes |
| [1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)<br /><br /> 5.00.8577.1000 | November 20, 2017 | May 20, 2019 | No | Yes |

<a name="bkmk_note1"></a> 

> [!Note]  
> <sup>**Note 1:**</sup> The 1802 baseline media is available as part of the following releases on the [Volume License Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC):
> - System Center Config Mgr (current branch)
> - System Center 2016 Datacenter
> - System Center 2016 Standard  
> 
> For example, search the VLSC for `System Center Config Mgr (current branch)`. Find the 1802 baseline media in the list of files, and download for that release.  

#### Historical versions
The following table lists historical versions of Configuration Manager current branch that are out of support:

| Version | Availability date | Support end date | Baseline | In-console update |  
|-------------|-----------|------------|--------------|------------------------|  
| 1706 <br /><br /> 5.00.8540.1000 | July 31, 2017 | July 31, 2018 | No | Yes |
| 1702 <br /><br /> 5.00.8498.1000 | March 27, 2017 | March 27, 2018 | Yes | Yes |
| 1610 <br /><br /> 5.00.8458.1000 | November 18, 2016 | November 18, 2017 | No | Yes |
| 1606 <br /><br /> 5.00.8412.1000 | July 22, 2016 | July 22, 2017 | No | Yes |
| 1606 with the 1606 hotfix rollup (KB3186654) <br><br>5.00.8412.1307 | October 12, 2016 | October 12, 2017 | Yes | No |
| 1602<br /><br /> 5.00.8355.1000 | March 11, 2016 | March 11, 2017 | No | Yes |
| 1511 <br /><br /> 5.00.8325.1000 | December 8, 2015 | December 8, 2016 | Yes | No |  

#### How to check the version
To check the version of your Configuration Manager site, in the console go to **About System Center Configuration Manager** at the top-left corner of the console. This dialog displays the site and console versions.  

 > [!Note]  
 > Starting in version 1802, the console version is now slightly different from the site version. The minor version of the console now corresponds to the Configuration Manager release version. For example, in Configuration Manager version 1802 the initial site version is 5.0.8634.1000, and the initial console version is 5.**1802**.1082.1700. The build (1082) and revision (1700) numbers may change with future hotfixes to the 1802 release.



##  <a name="bkmk_inconsole"></a> In-console updates and servicing  

When you use a production-ready installation of Configuration Manager current branch, most updates are available using the **Updates and Servicing** channel. This method identifies, downloads, and makes available the updates that apply to your current infrastructure version and configuration. It includes only updates that Microsoft recommends for all customers.   

These updates include:  

-   New versions, like version 1802, 1806, or 1810.  

-   Updates that include new features for your current version.

-   Hotfixes for your version of Configuration Manager and that all customers should install.

The in-console updates deliver increased stability and resolve common issues. They replace the update types seen for previous product versions such as service packs, cumulative updates, hotfixes that are applicable to all customers, and the extension for Microsoft Intune. 

The in-console updates can apply to one or more of the following systems:  

-   Primary and central administration site servers  

-   Site system roles and site system servers  

-   Instances of the SMS Provider  

-   Configuration Manager consoles  

-   Configuration Manager clients  

Configuration Manager discovers new updates for you. Synchronize your Configuration Manager service connection point with the Microsoft cloud service, noting the following behaviors:  

-   When your service connection point is in online mode, your site synchronizes with Microsoft every day. It automatically identifies new updates that apply to your infrastructure. To download updates and redistributable files, the computer that hosts the service connection point site system role uses the **System** context to access the following internet locations: go.microsoft.com and download.microsoft.com. For more information about additional locations used by the service connection point, see [Internet access requirements](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls).  

-   When your service connection point is in offline mode, use the service connection tool to manually sync with the Microsoft cloud. For more information, see [Use the service connection tool](/sccm/core/servers/manage/use-the-service-connection-tool).  

-   In-console updates replace the need to independently locate and install individual updates, service packs, and new features.  

-   Install only the in-console updates you choose. When installing some updates, you can select individual features to enable and use. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

When you install an in-console update, the following process occurs:  

-   It automatically runs a prerequisite check. You can also manually run this check prior to starting the installation.  

-   It installs at the top-level site in your environment. This site is the central administration site if you have one. In a hierarchy, the update automatically installs at primary sites. Control when each primary site server is allowed to update by using [Service windows for site servers](/sccm/core/servers/manage/service-windows).  

-   After a site server updates, all affected site system roles automatically update. These roles include instances of the SMS Provider. After the site installs the update, Configuration Manager consoles also prompt the console user to update the console.  

-   If an update includes the Configuration Manager client, you're offered the option to test the update in pre-production, or to apply the update to all clients immediately.  

-   After a primary site is updated, secondary sites don't automatically update. Instead, you must manually initiate the secondary site update.  

> [!NOTE]  
>  The Configuration Manager current branch, the long-term servicing branch, and the technical preview branch are different releases. Therefore, updates that apply for one branch aren't available as in-console updates for the other branches. For more information about available branches, see [Which branch of Configuration Manager should I use?](/sccm/core/understand/which-branch-should-i-use)



##  <a name="bkmk_outofband"></a> Out-of-band hotfixes  

Some hotfixes release with limited availability to address specific issues. Other hotfixes are applicable to all customers but can't install using the in-console method. These fixes are delivered out-of-band and not discovered from the Microsoft cloud service.  

Typically, when you're seeking to fix or address a problem with your deployment of Configuration Manager, you can learn about out-of-band hotfixes from Microsoft customer support services, a Microsoft support knowledge base article, or [posts from the System Center Configuration Manager team](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) on the Enterprise Mobility + Security blog. 

Install these fixes manually, using one of the following two methods:  

#### Update Registration Tool
This tool manually imports the hotfix into your Configuration Manager console. Then install the update as you would in-console updates that are discovered automatically.  

This method is used for hotfixes that use the following file name structure:  
  `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`    

For more information, see [Use the update registration tool to import hotfixes](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes).  

#### Hotfix Installer
Use this tool to manually install a hotfix that can't be installed using the in-console method.  

This method is used for fixes that use the following file name structure:   
   `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

For more information, see [Use the hotfix installer to install updates](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).  



## Next steps

The following articles can help you understand how to find and install the different update types for Configuration Manager:  

-   [Install in-console updates](/sccm/core/servers/manage/install-in-console-updates)  

-   [Use the service connection tool](/sccm/core/servers/manage/use-the-service-connection-tool)  

-   [Use the update registration tool to import hotfixes](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)  

-   [Use the hotfix installer to install updates](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates)  


For more information about the technical preview branch, see [Technical preview](/sccm/core/get-started/technical-preview).
