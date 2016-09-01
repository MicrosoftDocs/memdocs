---
title: "Prepare to install System Center Configuration Manager sites"
ms.custom: na
ms.date: 2016-07-22
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
caps.latest.revision: 5
author: Brenduns
---
# Prepare to install System Center Configuration Manager sites
To prepare for a successful deployment of one or more System Center Configuration Manager sites, become familiar with the details in this article. These steps can save you time during installation of multiple sites and help prevent missteps that might result in the need to reinstall one or more sites.
 > [!TIP]
 >  The following scenarios are similar to, but distinct from installing a System Center Configuration Manager current branch site: 
 > -  **Upgrade**: Install System Center Configuration Manager to **upgrade** from System Center 2012 Configuration Manager, see [Upgrade to System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) 
 > -  **Update**: Use in-console updates to install a new **update version** to an existing System Center Configuration Manager site, see [Updates for System Center Configuration Manager](../../../../core/servers/manage/updates.md)
 > -  **Migrate**: To **migrate data** from another Configuration Manager hierarchy to your current System Center Configuration Manager hierarchy, see [Planning for migration to System Center Configuration Manager](../../../../core/migration/planning-for-migration.md)

      
         
 ## <a name="bkmk_options"></a> Options for installing different types of sites
 When you install a new Configuration Manager, the version of the source files you can use depends on the version of sites that are already in the hierarchy (if any), and the installation methods available to you depend on the type of site you want to install.  

Before installing sites, ensure you have planned your hierarchy and understand the type of site you want to install. For more information, see [Design a hierarchy of sites](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).


### First site
The first site you will install for a hierarchy will be either a stand-alone primary site, or a central administration site. 

**Install media**: 
To install a central administration site or a stand-alone primary site as the first site in a new hierarchy, you must [use a baseline version](../../../../core/servers/manage/updates.md#bkmk_Baselines) of Configuration Manager. Do not install the first site of a new hierarchy using updated source files from the [CD.Latest folder](../../../../core/servers/manage/the-cd.latest-folder.md) of any site. 

**Install method**: You can install either type of site by using the [Configuration Manager Setup wizard](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) or you can configure a script to use with a [scripted command line installation](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### Additional sites
After the initial site is installed, you can add additional sites at any time. The following options exist to add additional sites (up to [supported limits](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

Site that you have          |Additional sites you can install  
---------                   |---------
Central administration site |   Install a child primary site            
Child primary site          |   Install a secondary site        
Stand-alone primary site    |   Install a secondary site<br />Expand the primary site, which converts the stand-alone primary site into a child primary site

**Install media**: When you install a central administration site to expand on a stand-alone primary site, or install a new child primary site in an existing hierarchy, you must use installation media (source files) that matches the version of the existing site or sites. 
> [!IMPORTANT]
> If you have installed in-console updates that have changed the version of the previously installed sites, do not use the original install media and instead use source files from the [CD.Latest folder](../../../../core/servers/manage/the-cd.latest-folder.md) of an updated site.  Configuration Manager requires you to use source files that match the version of the existing site your new site will connect to.

 
A secondary site must be installed from within the Configuration Manager console, and therefore always installs using source files from the parent primary site. 
 
**Install method**: The method you use to install additional sites depends on the type of site you want to install.
-   **Adding a central administration site**:  
You can use the Configuration Manager Setup wizard, or a scripted command line to install the new central administration site as a parent site to your existing stand-alone primary site.  For more information, see [Expand a stand-alone primary site](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
-   **Adding a child primary site**:  
You can use the Configuration Manager Setup wizard, or a command line installation to add a child primary site below a central administration site.
-   **Adding a secondary site**:   
You use the Configuration Manager console to install a secondary site as a child site below a primary site. Other methods are not supported for secondary sites.



## <a name="bkmk_tasks"></a>  Common tasks to complete before starting an install
-   Understand the hierarchy topology you will use for your deployment    
     (see [Design a hierarchy of sites for System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md))  
  
-   Prepare and configure individual servers to meet prerequisites and supported configurations for use with Configuration Manager (see [Site and site system prerequisites](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md))  
  
-   Install and configure SQL Server to host the site database (see    
    [Support for SQL Server versions for System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md))  
  
-   Prepare your network environment to support Configuration Manager (see [Prepare your network environment for System Center Configuration Manager](../Topic/Prepare%20your%20network%20environment%20for%20System%20Center%20Configuration%20Manager.md))  
  
-   If you will use a PKI, prepare your infrastructure and certificates (see [PKI certificate requirements for Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md)
  
-   Install the latest security updates on computers you will use as site servers or site system servers, and when necessary, restart them.



## <a name="bkmk_sitecodes"></a>  About site names and site codes
Site codes and site names are used to identify and manage the sites in a Configuration Manager hierarchy. In the Configuration Manager console, the site code and site name are displayed in the <site code\> - <site name\> format. Every site code that you use in your hierarchy must be unique. If the Active Directory schema is extended for Configuration Manager, and sites are publishing data, the site codes used within an Active Directory forest must be unique even if they are used in a different Configuration Manager hierarchy or if they have been used in previous Configuration Manager installations. Be sure to carefully plan your site codes and site names before you deploy your hierarchy.

### specify a site code and site name
During Configuration Manager Setup, you are prompted for a site code and site name for the central administration site, and each primary and secondary site installation. The site code must uniquely identify each site in the hierarchy. Because the site code is used in folder names, never use the following names for the site code, which include Configuration Manager reserved names and Windows-reserved names: 
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS
> [!NOTE]
> Configuration Manager Setup does not verify that the site code that you specify is not already in use.



To enter the site code for a site during Configuration Manager Setup, you must enter three alphanumeric characters. Only the letters A through Z, numbers 0 through 9, or combinations of the two are allowed when specifying site codes. The sequence of letters or numbers has no effect on the communication between sites. For example, it is not necessary to name a primary site ABC and a secondary site DEF.

The site name is a friendly name identifier for the site. Use only the standard characters A through Z, a through z, 0 through 9, and the hyphen (-) in site names.
> [!IMPORTANT]
> Changing the site code or site name after installation is not supported.

### Reuse a site code
Site codes cannot be used more than one time in a Configuration Manager hierarchy for a central administration site or primary sites, even if the original site and site code have been uninstalled. If you reuse a site code, you run the risk of having object ID conflicts in your hierarchy. You can reuse the site code for a secondary site if that secondary site and site code are no longer in use in yourConfiguration Manager hierarchy or in the Active Directory forest.


## Limits and restrictions for installed sites
Before installing sites, understand the following limitations that apply to sites and hierarchies:
-   After Setup is finished, you cannot change the following site properties without uninstalling the site and then reinstalling it with the new values:  
    -   The program files installation directory  
    -   Site code  
    -   Site description  
-   When your hierarchy includes a central administration site:  
    -   Configuration Manager does not support moving a child primary site out of a hierarchy to create a stand-alone primary site or to attach it to a different hierarchy. Instead, you uninstall the child primary site, and then reinstall it as a new stand-alone primary site, or child of central administration site of a different hierarchy.  


## <a name="bkmk_optionalsteps"></a>  Optional steps to run before starting Setup
**You can manually run [Setup Downloader](../../../../core/servers/deploy/install/setup-downloader.md)** to download the updated Setup files for Configuration Manager. 

When the computer where you will run Setup is not connected to the Internet, or when you expect to install multiple site servers, consider using Setup Downloader to download the required updates to Setup files: 

-  By default, Setup will connect to the Internet to download updated Setup files
-  By default, the files are stored in a folder named Redist
-  You can direct Setup to a location on your network where you have previously stored a copy of these files


**You can manually run the [Prerequisite Checker](../../../../core/servers/deploy/install/prerequisite-checker.md)** to identify and fix problems before running Setup. Prior to staring Setup to install a site, and before installing a site system role on a server, you can run Prerequisite Checker to ensure the computer meets the requirements to host the site or site system role. 
 -  By default, Setup will run the prerequisite checker.
 -  If there are any Errors, Setup will halt until the issue is fixed.


**Identify optional ports** to use for site systems and clients.
 -  By default, site systems and clients use pre-defined ports to communicate.
 -  During Setup, you can configure alternate ports. 
 -  For more information, see [Ports used in System Center Configuration Manager](../../../../core/plan-design/hierarchy/ports.md)


## See Also:
[Installing System Center Configuration Manager sites](../../../../core/servers/deploy/install/installing-sites.md)



 