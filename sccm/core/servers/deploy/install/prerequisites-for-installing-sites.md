---
title: Prerequisites for sites
titleSuffix: Configuration Manager
description: Learn about prerequisites for installing the different types of Configuration Manager sites.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Prerequisites for installing Configuration Manager sites

*Applies to: System Center Configuration Manager (Current Branch)*

Before you begin a site installation, learn about the prerequisites for installing the different types of Configuration Manager sites.



## Primary sites and the central administration site

The following prerequisites apply to installing one of the following types:
- A central administration site as the first site of a hierarchy
- A stand-alone primary site
- A child primary site

If you're installing a central administration site as part of a hierarchy expansion, see [Expanding a stand-alone primary site](#bkmk_expand).


###  <a name="bkmk_PrereqPri"></a> Prerequisites for installing a primary site or a central administration site  

- The user account that installs the site must have the following rights:  

    - **Administrator** on the following servers:  
        - The site server  
        - Each server that hosts the **site database**  
        - Each instance of the **SMS Provider** for the site  

    - **Sysadmin** on the instance of SQL Server that hosts the site database  

        > [!IMPORTANT]  
        >  When Configuration Manager setup finishes, both the user account that runs setup and the site server computer account must retain sysadmin rights to SQL Server. Don't remove the sysadmin rights from these accounts.  

- If you're installing a primary site, you need the following additional rights:  

    - **Administrator** on additional servers where you install the initial management point and distribution point, if not on the site server  

- If you're installing a new child primary site below a central administration site, you need the following additional rights:  

    - **Administrator** on the server that hosts the central administration site  

    - Role-based administration rights within Configuration Manager that are equivalent to the security role of **Infrastructure Administrator** or **Full Administrator**  

- Use the correct installation source files, and run setup from that location. For information about the correct source files to use to install different types of sites, see [Options for installing different types of sites](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options).  

- The site server must have access to updated setup files from Microsoft, in one of the following ways:  

    - Before you start the install, download and store a copy of these files on your local network. For more information, see [Setup Downloader](/sccm/core/servers/deploy/install/setup-downloader).  

    - If a local copy of these file isn't available, the site server must have internet access. It downloads these files from Microsoft during the installation.  

- The site server and site database server must meet all prerequisite configurations. Before starting Configuration Manager setup, [manually run Prerequisite Checker](/sccm/core/servers/deploy/install/prerequisite-checker) to identify and fix problems.  


### <a name="bkmk_expand"></a> Prerequisites to expand a stand-alone primary site

A stand-alone primary site must meet the following prerequisites before you can expand it into a hierarchy with a central administration site:

#### Source file version matches site version
Install the new central administration site using media from a CD.Latest folder that matches the version of the stand-alone primary site. To make sure the versions match, use the source files found in the [CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder) on the stand-alone primary site. 

For more information about the correct source files to use to install different sites, see [Options for installing different types of sites](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options).  

#### Stop active migration from another hierarchy
You can't configure the stand-alone primary site to migrate data from another Configuration Manager hierarchy. Stop active migration to the stand-alone primary site from other Configuration Manager hierarchies and remove all configurations for migration. These configurations include: 
- Migration jobs that haven't completed  
- Data gathering  
- The configuration of the active source hierarchy  

This configuration is necessary because Configuration Manager migrates data from the top-level site of the hierarchy. When you expand a stand-alone primary site, the configurations for migration don't transfer to the central administration site.  

After you expand the stand-alone primary site, if you reconfigure migration at the primary site, the central administration site performs the migration operations. 

For more information about how to configure migration, see [Configure source hierarchies and source sites for migration](/sccm/core/migration/configuring-source-hierarchies-and-source-sites-for-migration).  

#### Computer account as Administrator
The computer account of the server that hosts the new central administration site must be a member of the **Administrator** group on the stand-alone primary site server. 

To successfully expand the stand-alone primary site, the computer account of the new central administration site must have **Administrator** rights on the stand-alone primary site. This is required only during site expansion. When site expansion finishes, you can remove the account from the user group on the primary site.  

#### Installation account permissions
The user account that runs Configuration Manager setup to install the new central administration site must have role-based administration rights at the stand-alone primary site.

To install a central administration site as part of a site expansion, the user account that runs setup to install the central administration site must be defined in role-based administration at the stand-alone primary site as either a **Full Administrator** or an **Infrastructure Administrator**.  

#### Top-level site roles
Before you expand the site, uninstall the following site system roles from the stand-alone primary site:

- Asset Intelligence sync point  
- Endpoint Protection point  
- Service connection point  

Configuration Manager only supports these roles at the top-level site of the hierarchy. Uninstall these site system roles before you expand the stand-alone primary site. After you expand the site, reinstall these site system roles at the central administration site.  

All other site system roles can remain installed at the primary site.  

#### Open the SQL Server Service Broker port
The network port must be open for the SQL Server Service Broker (SSB) between the stand-alone primary site and the server for the central administration site.  

To successfully replicate data between a central administration site and a primary site, Configuration Manager requires an open port between the two sites for SSB to use. When you install a central administration site and expand a stand-alone primary site, the prerequisite check does'ot verify that the port you specify for the SSB is open on the primary site.  

#### Known issues with Azure services
When you use one of the following Azure services with Configuration Manager, after expanding the site, remove and then recreate the connection to that service.

- [Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics)  
- [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-readiness)  
- [Microsoft Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)  

Use the following steps to resolve this issue:
 1. In the Configuration Manager console, delete the Azure service from the **Azure Services** node.  

 2. In the Azure portal, delete the tenant that's associated with the service from the Azure Active Directory tenants node. This action also deletes the Azure AD web app that's associated with the service.  

 3. Reconfigure the connection to the Azure service for use with Configuration Manager.  



## <a name="bkmk_secondary"></a> Secondary sites

The following are prerequisites for installing secondary sites:

- The administrator who configures the installation of the secondary site in the Configuration Manager console must have role-based administration rights that are equivalent to the security role of **Infrastructure Administrator** or **Full Administrator**.  

- The computer account of the parent primary site must be an **Administrator** on the secondary site server.  

- When the secondary site uses a previously installed instance of SQL Server to host the secondary site database:  

    - The computer account of the parent primary site must have **sysadmin** rights on the instance of SQL Server on the secondary site server.  

    - The **Local System** account of the secondary site server computer must have **sysadmin** rights on the instance of SQL Server on the secondary site server.  

        > [!IMPORTANT]  
        >  When Configuration Manager setup finishes, both accounts must retain sysadmin rights to SQL Server. Don't remove the sysadmin rights from these accounts.  

- The secondary site server must meet all prerequisite configurations. These configurations include SQL Server and the default site system roles of the management point and distribution point.  
