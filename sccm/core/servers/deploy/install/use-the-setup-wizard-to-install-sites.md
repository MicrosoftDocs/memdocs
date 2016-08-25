---
title: "Use the Setup Wizard to install System Center Configuration Manager sites"
ms.custom: na
ms.date: 2016-07-22
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
caps.latest.revision: 3
author: Brenduns
---
# Use the Setup Wizard to install System Center Configuration Manager sites

To install a new System Center Configuration Manager site using a guided user interface, you use the Configuration Manager Setup Wizard (setup.exe). The Wizard supports install of a primary site or central administration site. You also use the Wizard to [upgrade an Evaluation install](../../../../core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install.md) of Configuration Manager to a fully licensed installation.  When you do not want to use the Wizard you can instead use an [installation script](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md) and run an unattended command line installation. 

To install a secondary site, you must install the site from within the Configuration Manager console.  Secondary sites do not support a scripted command line install. 

## <a name="bkmk_primary"></a>  Install a central administration site or primary site
Use the following procedure to install a central administration site, a primary site, or to upgrade and evaluation site to a fully licensed Configuration Manager site.   

Before starting the site install, be familiar with the details in the following articles:
 -  [Prepare to install sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md)
 -  [Prerequisites for installing sites](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md)

If you are installing a central administration site as part of a site expansion scenario, review the [Expanding a stand-alone primary site](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) section of this topic before using the following procedure. 

### <a name="bkmk_installpri"></a>   To install a primary or central administration site
 
1.  On the computer where you want to install the site, run **<InstallationMedia\>\SMSSETUP\BIN\X64\Setup.exe** to start the **System Center Configuration Manager Setup Wizard**.  
  
    > [!NOTE]  
    >  When you install a central administration site to expand on a stand-alone primary site, or install a new child primary site in an existing hierarchy, you must use installation media (source files) that matches the version of the existing site or sites.  If you have installed in-console updates that have changed the version of the previously installed sites, do not use the original install media and instead use source files from the [CD.Latest folder](../../../../core/servers/manage/the-cd.latest-folder.md) of an updated site.  Configuration Manager requires you to use source files that match the version of the existing site your new site will connect to.  
  
2.  On the **Before You Begin** page, click **Next**.  
  
3.  On the **Getting Started**  page select the type of site you want to install:  
  
     **Central administration site** – as the first site of a new hierarchy, or when expanding a stand-alone primary site:  
  
    -   Select: **Install a Configuration Manager central administration site**  
  
         During a later step of this procedure, you are offered the choice to install a central administration site as the first site of a new hierarchy, or to install a central administration site to expand on a stand-alone primary site.  
  
     **Primary site** – as a stand-alone primary site which is the first site of a new hierarchy, or as a child primary:  
  
    -   Select: **Install a Configuration Manager primary site**  
  
        > [!TIP]  
        >  Typically, you only select the option **Use typical installation options for a stand-alone primary site** when you want to install a stand-alone primary site in a test environment. When you select this option:  
        >   
        > -   Setup automatically configures the site as a stand-alone primary site  
        > -   Uses a default installation path  
        > -   Uses a local installation of the default instance of SQL Server for the site database  
        > -   Installs a management point and a distribution point on the site server computer  
        > -   Configures the site with English and the display language of the operating system on the primary site server if it matches one of the languages that Configuration Manager supports  
  
4.  On the **Product Key** page, choose whether to install Configuration Manager as an evaluation edition or a licensed edition.  
  
    -   If you select a licensed edition, enter your product key and click **Next**.  
  
    -   If you select an evaluation edition, click **Next**. (You can upgrade an evaluation install to a full install at a later time.)  
  
5.  On the **Microsoft Software License Terms** page, read and accept the license terms.  
  
6.  On the **Prerequisite Licenses** page, read and accept the license terms for the prerequisite software.  Setup downloads and automatically installs the software on site systems or clients when it is required. You must select all check boxes before you can continue to the next page.  
  
7.  On the **Prerequisite Downloads** page, specify whether Setup must download the latest prerequisite redistributable files from the Internet or use previously downloaded files:  
  
    -   If you want Setup to download the files at this time, select **Download required files** and specify a location to store the files in.  
  
    -   If you previously downloaded the files by using [Setup Downloader](../../../../core/servers/deploy/install/setup-downloader.md), select **Use previously downloaded files** and specify the download folder.  
  
        > [!TIP]  
        >  If you use previously downloaded files, verify that the path to the download folder contains the most recent version of the files.  
  
8.  On the **Server Language Selection** page, select the languages that are available for the  Configuration Manager console and for reports. (English is selected by default and cannot be removed.)  
  
9. On the **Client Language Selection** page, select the languages that are available to client computers, specify whether to enable all client languages for mobile device clients. (English is selected by default and cannot be removed.)  
  
    > [!IMPORTANT]  
    >  If you are installing a central administration site to expand a stand-alone primary site, you must select the same client languages that are installed at the stand-alone primary site.  
  
10. On the **Site and Installation Settings** page, specify the following for the new site you are installing:  
  
    -   **Site code:** [Each site code in a hierarchy must be unique](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_sitecodes) and be comprised of three alpha-numeric digits (A through Z and 0 through 9). Because the site code is used in folder names, do not use the following for the site, which includes Windows-reserved names:    
        -   AUX  
        -   CON    
        -   NUL    
        -   PRN    
        -   SMS  
  
        > [!NOTE]  
        >  Setup does not verify that the site code that you specify is not already in use, or if it a reserved name.  
  
    -   **Site name:** Each site requires this friendly name which can help you identify the site.  
  
    -   **Installation folder:** This is the folder path to the Configuration Manager installation. You cannot change the location after the site installs, and the path cannot contain Unicode characters, or trailing spaces.  
  
11. On  the **Site Installation** page, use the following option that matches your scenario:  
  
    -   **I am installing a central administration site:**  
  
         On the **Central Administration Site Installation** page, select **Install as the first site in a new hierarchy**, and then click **Next** to continue.  
  
    -   **I am expanding a stand-alone primary into a hierarchy with a central administration site:**  
  
         On the **Central Administration Site Installation** page, select **Expand an existing stand-alone primary into a hierarchy**, specify the FQDN of the stand-alone primary site server, and then click **Next** to continue.  
  
         The media you use to install the new central administration site must match the version of the primary site.  
  
    -   **I am installing a stand-alone primary site:**  
  
         On the **Primary Site Installation** page, select Ins**tall the primary site as a stand-alone site**, and then click **Next**.  
  
    -   **I am installing a child primary site:**  
  
         On the **Primary Site Installation** page, select **Join the primary site to an existing hierarchy**, specify the FQDN for the central administration site, and then click **Next**.  
  
12. On the Database Information page, specify the following information:  
  
    -   **SQL Server name (FQDN):** By default, this is set to be the site server computer.  
  
    -   **Instance name:** By default, this is blank which will use the default instance of SQL on the site server computer.  
  
    -   **Database name:** By default, this is set to CM_<Sitecode\>. You are free to use a different name you specify.  
  
    -   **Service Broker Port:** By default, this is set to use the default SQL Server Service Broker (SSB) port of 4022, and is used by SQL to communicate directly to the site database at other sites.  
  
13. On the second **Database Information** you can specify non-default locations for the SQL Server data file and SQL Server log file for the site database:  
  
    -   Default file locations for SQL server are provided  
  
    -   The option to specify non-default file locations is not available when you use a SQL Server cluster  
  
    -   The prerequisite checker does not run a check for free disk space for non-default file locations  
  
14. On the **SMS Provider Settings** page, specify the FQDN for the server where you want to install the SMS Provider.  
  
    -   By default, the site server is specified.  
  
    -   After the site installs, you can configure additional SMS Providers  
  
15. On the **Client Communication Settings** page, choose whether to configure all site systems to accept only HTTPS communication from clients or for the communication method to be configured for each site system role.  
  
    -   When you select **All site system roles accept only HTTPS communication from clients**, client computer must have a valid PKI certificate for client authentication. For more information about PKI certificate requirements, see PKI Certificate Requirements for Configuration Manager  
  
    > [!NOTE]  
    >  This step only applies when you install a primary site. If you are installing a central administration site, skip this step.  
  
16. On the **Site System Roles** page, choose whether to install a management point or distribution point. For each role you choose to have installed by Setup:  
  
    -   You must enter the **FQDN** for the computer that will host the role and choose the client connection method that server will support (HTTP or HTTPS).  
  
    -   If you selected **All site system roles accept only HTTPS communication from clients** on the previous page, the client connection settings are automatically configured for HTTPS and cannot be changed unless you go back and change the setting.  
  
    > [!NOTE]  
    >  This step only applies when you install a primary site. If you are installing a central administration site, skip this step.  
  
    > [!NOTE]  
    >  To install site system roles, Setup uses the **site system installation account**. By default, this uses the primary site’s computer account.  This account must be a local administrator on a remote computer to install the site system role. If this account lacks the required permissions, uncheck the site system roles and install them later from within the Configuration Manager console, after configuring additional accounts to use as site system installation accounts.  
  
17. On the **Usage Data** page, review the information about data Microsoft collects, and then click **Next**.  
  
18. The **Service Connection Point Setup** page is only available during Setup when:  
  
    -   You are installing a stand-alone primary site  
  
    -   You are installing a central administration site  
  
    > [!NOTE]  
    >  If you are installing a child primary site, skip this step (This page is not available).  
  
     If you are installing a central administration site as part of a site expansion scenario and this role is already installed at the stand-alone primary site, you must uninstall this role from the stand-alone primary site. Only one instance of this role is permitted in a hierarchy, and it is only permitted at the top-tier site of the hierarchy.  
  
     After you select a configuration for the **Service Connection Point**, click **Next**. (After Setup completes, you can change this configuration from within the Configuration Manager console.)  
  
19. On the **Settings Summary** page, review the setting you have selected and when ready, click **Next** to start Prerequisite Checker.  
  
20. On the **Prerequisite Installation Check** page, any problems that can be identified will be listed.  
  
    -   When Prerequisite Checker finds a problem, click an item in the list for details about how to resolve the problem.  
  
    -   You must resolve each item with a status of **Failed** before continuing to install the site. Items with a status of **Warning** should be resolved, but do not block installation of the site.  
  
    -   After resolving issues, click **Run Check** to rerun the prerequisite checker.  
  
     When the prerequisite checker runs and no checks receive a **Failed** status, you can click **Begin Install** to start the site installation.  
  
    > [!TIP]  
    >  In addition to the feedback provided in the Wizard, you can find additional information about prerequisite issues when you view the **ConfigMgrPrereq.log** file in the root of the system drive of the computer you are installing.  For a list of installation prerequisite rules and descriptions, see [List of Prerequisite Checks for System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  
  
21. On the **Installation** page, Setup displays the installation status. When the core site server installation is complete you will have the option to **Close** the installation Wizard. When you close the Wizard, the installation and initial site configurations continue in the background.  
  
    -   You can connect a Configuration Manager console to the site before setup is complete. This console connects as read-only, and lets you view objects and settings, but not introduce edits.  
  
    -   After Setup completes, you will be able to connect a console that can edit objects and settings.  


## <a name="bkmk_expand"></a> Expand a stand-alone primary site
When you have installed a stand-alone primary site as your first site, you have the option at a later time to expand that site into a larger hierarchy by installing a central administration site.   

When you expand a stand-alone primary site, you install a new central administration site that uses the existing stand-alone primary site’s database as a reference. After the new central administration site installs, the stand-alone primary site functions as a child primary site. 

  
-   Only a stand-alone primary site can be expanded into a new hierarchy.  
  
-   Only one stand-alone primary site can be expanded into a specific hierarchy. You cannot use this option to join additional stand-alone primary sites into the same hierarchy. Instead, use Migration to migrate data from one hierarchy into another.  
  
-   After you expand a stand-alone site into a hierarchy with a central administration site, you can add additional child primary child sites.  
  
-   To remove a primary site from a hierarchy with a central administration site, you must uninstall the primary site.  
  
 To expand the site, you use the System Center Configuration Manager Setup Wizard to install a new central administration site with the following caveats:  
  
-   You must install the central administration site using the same version of Configuration Manager as the stand-alone primary site.  
  
-   On the Getting Started page of the Setup wizard, you select the option to install a central administration site. At a later stage of Setup you will choose an option to expand an existing stand-alone primary site.  
  
-   When you configure the Client Language Selection page for the new central administration site, you must select the same client languages that are configured for the stand-alone primary site you are expanding.  
  
-   On the Site Installation page, you select the option to expand the stand-alone primary site.  
  
 To expand a stand-alone primary site, use the procedure *[To install a primary or central administration site](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_installpri)*, found earlier in this article. 


## <a name="bkmk_secondary"></a> Install a secondary site
 You use the Configuration Manager console to install a secondary site.  
  
-   If the console you use is not connected to the primary site that will be the parent site to the new secondary site, the command to install the site will be replicated to the correct primary site.  
  
-   Before starting the site installation, ensure your user account has the prerequisite permissions, and that the computer that will host the new secondary site meets all of the prerequisites for use as a secondary site server.  
  
-   When you install the secondary site, Configuration Manager will configure the new site to use the client communication ports that are configured at the parent primary site.  

### <a name="bkmk_installsecondary"></a> To install a secondary site  

  
1.  In the Configuration Manager console, navigate to **Administration** > **Site Configuration** > **Sites**, and select the site that will be the parent primary site of the new secondary site  
  
2.  Click **Create Secondary Site** to start the **Create Secondary Site Wizard**.  
  
3.  On the **Before You Begin** page, confirm that the primary site that is listed is the site that you want to be the parent of the new secondary site, and then click **Next**.  
  
4.  On the **General** page, specify the following:  
  
    -   **Site code**: Each site code in a hierarchy must be unique and be comprised of three alpha-numeric digits (A through Z and 0 through 9). Because the site code is used in folder names, do not use Windows-reserved names for the site including:  
  
        -   AUX    
        -   CON    
        -   NUL    
        -   PRN  
        -   SMS  
        > [!NOTE]  
        >  Setup does not verify that the site code that you specify is not already in use, or if it a reserved name.  
  
    -   **Site server name**: This is the FQDN of the server where the new secondary site will install.  
  
    -   **Site name**: Each site requires this friendly name which can help you identify the site.  
  
    -   **Installation folder**: This is the folder path to the Configuration Manager installation. You cannot change the location after the site installs, and the path cannot contain Unicode characters, or trailing spaces.  
  
    > [!IMPORTANT]  
    >  After you specify details on this page, you can click **Summary** to use the default settings for the remainder of the secondary site options, and to go directly to the **Summary** page of the wizard.  
    >   
    >  -   Only use this option when you are familiar with the default settings in this wizard, and they are the settings you want to use.  
    > -   Boundary groups are not associated with the distribution point when you use the default settings. Therefore, until you configure boundary groups that include the secondary site server, clients will not use the distribution point that is installed on this secondary site as a content source location.  
  
5.  On the **Installation Source Files** page, choose how the secondary site computer obtains source files for installing the site.  
  
     When you use source files stored on the network, or stored on the secondary site computer:  
  
    -   The source file location must include a folder named **Redist** which includes all of the files previously downloaded by using Setup Downloader.  
  
    -   If any of the files from **Redist** are not available, Setup will fail to install the secondary site.  
  
    -   The computer account of the secondary site computer must have **Read** permissions to the source file folder and share.  
  
6.  On the **SQL Server Settings** page, specify the version of SQL Server to use, and then configure related settings.  
  
    > [!NOTE]  
    >  Setup does not validate the information that you enter on this page until it starts the installation. Before you continue, verify these settings.  
  
     **Install and configure a local copy of SQL Express on the secondary site computer**  
  
    -   **SQL Server Service port**: Specify the SQL Server service port for SQL Server Express to use. The service port is typically configured to use TCP port 1433, but you can configure another port.  
  
    -   **SQL Server Broker port**: Specify the SQL Server Service Broker (SSB) port for SQL Server Express to use. The Service Broker is typically configured to use TCP port 4022, but you can configure a different port. You must specify a valid port that no other site or service is using, and that no firewall restrictions block.  
  
    > [!IMPORTANT]  
    >  When Configuration Manager installs SQL Server Express, it installs SQL Server Express 2012 with no service pack:  
    >   
    >  -   For the secondary site to be supported, after it installs you must upgrade SQL Server Express 2012 by installing service pack 2 (or later).  
    > -   Additionally, if the new secondary site install fails to finish but first completes the installation of SQL Server Express 2012, you must update that instance of SQL Server Express before Configuration Manager can successfully retry the secondary site install.  
  
     **Use an existing SQL Server instance**  
  
    -   **SQL Server FQDN**: Review the FQDN for the SQL Server computer. You must use a local SQL Server to host the secondary site database and cannot modify this setting.  
  
    -   **SQL Server instance**: Specify the instance of SQL Server to use as the secondary site database. Leave this option blank to use the default instance.  
  
    -   **ConfigMgr site database name**: Specify the name to use for the secondary site database.  
  
    -   **SQL Server Broker port**: Specify the SQL Server Service Broker (SSB) port for SQL Server to use. You must specify a valid port that no other site or service is using, and that no firewall restrictions block.  
  
    > [!TIP]  
    >  See [Support for SQL Server versions](../../../../core/plan-design/configs/support-for-sql-server-versions.md) for a list of the SQL Server versions supported with System Center Configuration Manager.  
  
7.  On the **Distribution Point** page, configure settings for the distribution point that will be installed on the secondary site server.  
  
     **Required settings:**  
  
    -   **Specify how client devices communicate with the distribution point** – Choose between HTTP and HTTPS.  
  
    -   **Create a self-signed certificate or import a PKI client certificate** – Choose between using a self-signed certificate (which lets you also allow anonymous connections from Configuration Manager clients to the content library) or importing a certificate from your PKI.  
  
         The certificate is used to authenticate the distribution point to a management point before the distribution point sends status messages.  
  
         For information about the certificate requirements, see PKI Certificate Requirements for Configuration Manager.  
  
     **Optional settings:**  
  
    -   **Install and configure IIS if required by Configuration Manager** -  Select this setting to let Configuration Manager install and configure Internet Information Services (IIS) on the server if it is not already installed. IIS must be installed on all distribution points.  
  
        > [!NOTE]  
        >  Although this setting is optional, IIS must be installed on the server before a distribution point can be  installed successfully.  
  
    -   **Enable and configure BranchCache for this distribution point** •  
  
    -   **Description** – this is a friendly description for the distribution point to help you recognize it.  
  
    -   **Enable this distribution point for prestaged content**  
  
8.  On the **Drive Settings** page, specify the drive settings for the secondary site distribution point.  
  
     You can configure up to two disk drives for the content library and two disk drives for the package share, although Configuration Manager can use additional drives when the first two reach the configured drive space reserve. The **Drive Settings** page configures the priority for the disk drives and the amount of free disk space to remain on each disk drive.  
  
    -   **Drive space reserve (MB)**: The value that you configure for this setting determines the amount of free space on a drive before Configuration Manager chooses a different drive and continues the copy process to that drive. Content files can span multiple drives.  
  
    -   **Content Locations**: Specify the content locations for the content library and package share. Configuration Manager copies content to the primary content location until the amount of free space reaches the value that is specified for **Drive space reserve (MB)**. By default, the content locations are set to **Automatic**, and the primary content location will be set to the disk drive that has the most disk space at installation and the secondary location that is assigned the disk drive that has the second most free disk space. When the primary and secondary drives reach the drive space reserve, Configuration Manager selects another available drive with the most free disk space and continues the copy process.  
  
9. On the **Content Validation** page, specify whether to validate the integrity of content files on the distribution point.  
  
    -   When you enable content validation on a schedule, Configuration Manager initiates the process at the scheduled time, and all content on the distribution point is verified.  
  
    -   You can also configure the **Content validation priority**.  
  
    -   To view the results of the content validation process, in Configuration Manager console navigate to **Monitoring** >  **Distribution Status** >  **Content Status**. The content for each package type (for example, Application, Software Update Package, and Boot Image) is displayed.  
  
10. On the **Boundary Groups** page, manage the boundary groups for which this distribution point is assigned:  
  
    -   During content deployment, clients must be in a boundary group that is associated with the distribution point to use it as a source location for content.  
  
    -   You can select the **Allow fallback source location for content** option to allow clients outside these boundary groups to fall back and use the distribution point as a source location for content when no preferred distribution points are available.  
  
     For  information about preferred distribution points, see the [Fundamental concepts for content management](../../../../core/plan-design/hierachy/fundamental-concepts-for-content-management.md) topic.  
  
11. On the **Summary** page, verify the settings, and then click **Next** to install the secondary site. When the wizard presents  the **Completion** page, you can close the wizard. The secondary site installation continues in the background.  


### <a name="bkmk_verify"></a> To verify the secondary site installation status  
  
1.  In the Configuration Manager console, navigate to **Administration** > **Site Configuration** > **Sites**.  
  
2.  Select the secondary site server you are installing, and then click **Show Install Status**.  
  
    > [!TIP]  
    >  When you install more than one secondary site at a time, the prerequisite check runs against a single site at a time, and must complete for a site before it starts to check the next site.  
  


## See Also
[Installing System Center Configuration Manager sites](../../../../core/servers/deploy/install/installing-sites.md)
