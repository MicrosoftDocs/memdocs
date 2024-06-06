---
title: Prepare to install sites
titleSuffix: Configuration Manager
description: If you're planning to install multiple Configuration Manager sites, read this information to help you save time, and to prevent errors.
ms.date: 09/18/2019
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Prepare to install Configuration Manager sites

*Applies to: Configuration Manager (current branch)*

To prepare for a successful deployment of one or more Configuration Manager sites, become familiar with the details in this article. These steps can save you time during installation of multiple sites and help prevent missteps that might result in the need to reinstall one or more sites.

> [!TIP]
> When managing Configuration Manager site and hierarchy infrastructure, the terms *upgrade*, *update*, and *install* are used to describe three separate concepts. To learn how each term is used, see [About upgrade, update, and install](../../../understand/upgrade-update-install.md).

## <a name="bkmk_options"></a> Options for installing different types of sites
When you install a new Configuration Manager site, the version of the source files that you can use depends on the version of sites that are already in the hierarchy (if any). The installation methods that you can use depend on the type of site you want to install.  

Before installing a site, make sure you have planned your hierarchy, and that you understand the type of site you want to install. For more information, see [Design a hierarchy of sites](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).


### First site
The first site that you install in a hierarchy will be either a stand-alone primary site or a central administration site.

**Installation media**:
To install a central administration site or a stand-alone primary site as the first site in a new hierarchy, you must [use a baseline version](../../../../core/servers/manage/updates.md#bkmk_Baselines) of Configuration Manager. Do not install the first site of a new hierarchy by using updated source files from the [CD.Latest folder](../../../../core/servers/manage/the-cd.latest-folder.md) of any site.

**Installation method**: You can install either type of site by using the [Configuration Manager Setup Wizard](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md), or you can configure a script to use with a [scripted command-line installation](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### Additional sites
After the initial site is installed, you can add more sites at any time. You have the following options for adding sites (up to [supported limits](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

|Site that you have|Additional site type you can install|
|---|---|
|Central administration site|Child primary site|
|Child primary site|Secondary site|
|Stand-alone primary site|Secondary site (you can expand the primary site, which converts the stand-alone primary site to a child primary site)|

**Installation media**: When you install a central administration site to expand a stand-alone primary site, or if you install a new child primary site in an existing hierarchy, you must use installation media (that contains source files) that matches the version of the existing site or sites.

> [!IMPORTANT]
> If you have installed in-console updates that have changed the version of the previously installed sites, do not use the original installation media. Instead, in that scenario, use source files from the [CD.Latest folder](../../../../core/servers/manage/the-cd.latest-folder.md) of an updated site. Configuration Manager requires you to use source files that match the version of the existing site that your new site will connect to.

A secondary site must be installed from the Configuration Manager console. This way, secondary sites are always installed by using source files from the parent primary site.

**Installation method**: The method you use to install additional sites depends on the type of site you want to install.
- **Add a central administration site**:  You can use the Configuration Manager Setup Wizard or a scripted command line to install the new central administration site as a parent site to your existing stand-alone primary site. For more information, see [Expanding a stand-alone primary site](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
- **Add a child primary site**:  You can use the Configuration Manager Setup Wizard or a command-line installation to add a child primary site below a central administration site.
- **Add a secondary site**:  Use the Configuration Manager console to install a secondary site as a child site below a primary site. Other methods are not supported for adding secondary sites.

## <a name="bkmk_tasks"></a>  Common tasks to complete before starting an installation
- **Understand the hierarchy topology you will use for your deployment**    
For more information, see [Design a hierarchy of sites for Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

- **Prepare and configure individual servers to meet prerequisites and supported configurations for use with Configuration Manager**         
For more information, see [Site and site system prerequisites](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

- **Install and configure SQL Server to host the site database**     
For more information, see [Support for SQL Server versions for Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

- **Prepare your network environment to support Configuration Manager**      
For more information, see [Configure firewalls, ports, and domains to prepare for Configuration Manager](../../../../core/plan-design/network/configure-firewalls-ports-domains.md).  

- **If you will use a public key infrastructure (PKI), prepare your infrastructure and certificates**      
For more information, see [PKI certificate requirements for Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).

- **Install the latest security updates on computers you will use as site servers or site system servers, and when necessary, restart them**

## <a name="bkmk_sitecodes"></a>  About site names and site codes
Site codes and site names are used to identify and manage the sites in a Configuration Manager hierarchy. In the Configuration Manager console, the site code and site name are displayed in the &lt;*site code*\> - &lt;*site name*\> format. Every site code that you use in your hierarchy must be unique. If the Active Directory schema is extended for Configuration Manager and your sites are publishing data, the site codes used within an Active Directory forest must be unique even if they are used in a different Configuration Manager hierarchy or if they have been used in earlier Configuration Manager installations. Be sure to carefully plan your site codes and site names before you deploy your hierarchy.

### Specify a site code and site name
When you run Configuration Manager Setup, you are prompted for a site code and site name for the central administration site, and for each primary site and secondary site installation. A site code must uniquely identify each site in the hierarchy. Because the site code is used in folder names, never use the following names for the site code, which include names reserved for Configuration Manager and Windows:
- AUX
- CON
- NUL
- PRN
- SMS
- ENV <!--SCCMDocs-1871 and 5399453-->

> [!NOTE]
> Configuration Manager Setup does not verify that a site code is not already in use.

To enter the site code for a site when you're running Configuration Manager Setup, you must enter three alphanumeric characters. Only the letters *A* through *Z* and the numbers *0* through *9*, in any combination, are allowed in site codes. The sequence of letters or numbers has no effect on the communication between sites. For example, it is not necessary to name a primary site *ABC* and a secondary site *DEF*.

The site name is a friendly name identifier for the site. You can only use the characters *A* through *Z*, *a* through *z*, *0* through *9*, and the hyphen (*-*) in site names.

> [!IMPORTANT]
> A change of the site code or site name after you install the site is not supported.

### Reuse a site code
Site codes cannot be used more than one time in a Configuration Manager hierarchy for a central administration site or for a primary site, even if the original site and site code have been uninstalled. If you reuse a site code, you risk having object ID conflicts in your hierarchy. You can reuse the site code for a secondary site if that secondary site and the site code are no longer in use in your Configuration Manager hierarchy or in the Active Directory forest.

## Limits and restrictions for installed sites
Before you install a site, it's important to understand the following limitations that apply to sites and site hierarchies:
- After running Setup, you cannot change the following site properties without uninstalling the site and then reinstalling it by using the new values:  
  - Program Files installation directory  
  - Site code  
  - Site description  
- When your hierarchy includes a central administration site:  
  - Configuration Manager does not support moving a child primary site out of a hierarchy to create a stand-alone primary site or to attach it to a different hierarchy. Instead, uninstall the child primary site, and then reinstall it as a new stand-alone primary site or as a child site of the central administration site of a different hierarchy.  


## <a name="bkmk_optionalsteps"></a>  Optional steps before running Setup
**Manually run [Setup Downloader](../../../../core/servers/deploy/install/setup-downloader.md)**

To download the updated Setup files for Configuration Manager, you can run Setup Downloader. If the computer where you will run Setup is not connected to the Internet, or if you expect to install multiple site servers, consider using Setup Downloader to download the required updates to Setup. Here's additional information:
- By default, Setup connects to the Internet to download updated Setup files.
- By default, the files are stored in the Redist folder.
- You can direct Setup to a location on your network where you have previously stored a copy of these files.

**Manually run [Prerequisite Checker](../../../../core/servers/deploy/install/prerequisite-checker.md)**

To identify and fix problems before you run Setup to install a site and before you install a site system role on a server, you can run Prerequisite Checker. Prerequisite Checker helps ensure that the computer meets the requirements to host the site or site system role. Here's additional information:
- By default, Setup runs Prerequisite Checker.
- If there are any errors, Setup stops until the issue is fixed.

**Identify optional ports**

You can identify optional ports for site systems and clients to use. Here's additional information:
- By default, site systems and clients use predefined ports to communicate.
- During Setup, you can configure alternate ports.

For more information, see [Ports used](../../../../core/plan-design/hierarchy/ports.md).
