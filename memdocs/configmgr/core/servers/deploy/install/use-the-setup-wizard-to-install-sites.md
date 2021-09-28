---
title: Setup wizard
titleSuffix: Configuration Manager
description: Use the Configuration Manager setup wizard to install a new site.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Use the Setup Wizard to install Configuration Manager sites

*Applies to: Configuration Manager (current branch)*

To install a new Configuration Manager site by using a guided user interface, use the Configuration Manager Setup Wizard (setup.exe). The wizard supports installing a primary site or central administration site (CAS). You also use the wizard to [upgrade an evaluation installation](upgrade-an-evaluation-install-to-a-full-install.md) of Configuration Manager to a fully licensed installation. When you don't want to use the wizard, you can instead use an [installation script](use-a-command-line-to-install-sites.md) and run an unattended command-line installation.

Install a secondary site from within the Configuration Manager console. Secondary sites don't support a scripted command-line installation.

Before you install a site, be familiar with the details in the following articles:

- [Design a hierarchy of sites](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md)
- [Site and site system prerequisites](../../../plan-design/configs/site-and-site-system-prerequisites.md)
- [Prepare to install sites](prepare-to-install-sites.md)
- [Prerequisites for installing sites](prerequisites-for-installing-sites.md)
- Assess server readiness with the [Prerequisite Checker](prerequisite-checker.md)

> [!TIP]
> If you need assistance with site installation, see the [Support options and community resources](../../../understand/find-help.md#support-options-and-community-resources). For example, the Microsoft Q&A forum for [Configuration Manager site and client deployment](/answers/topics/mem-cm-site-deployment.html).

## <a name="bkmk_primary"></a> Install a central administration or primary site

Use the following procedure to install a CAS or a primary site. Also use it to upgrade an evaluation site to a fully licensed Configuration Manager site.

If you're installing a CAS as part of a site expansion scenario, review [Expanding a stand-alone primary site](#bkmk_expand) before using the following procedure.

### <a name="bkmk_installpri"></a> Process to install a primary or CAS

1. On the computer where you want to install the site, run `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` to start the **Configuration Manager Setup Wizard**.

    > [!NOTE]
    > When you install a CAS to expand on a stand-alone primary site, or install a new child primary site in an existing hierarchy, use installation media (source files) that match the version of the existing site or sites. If you've installed in-console updates that have changed the version of the previously installed sites, don't use the original installation media. Instead, use source files from the [CD.Latest folder](../../manage/the-cd.latest-folder.md) of an updated site. Configuration Manager requires you to use source files that match the version of the existing site that your new site will connect to.

1. On the **Before You Begin** page, choose **Next**.

1. On the **Getting Started** page, select the type of site that you want to install:

    - _Central administration site_, as the first site of a new hierarchy, or when expanding a stand-alone primary site:

        Select **Install a Configuration Manager central administration site**.

        Later in this process, you'll choose to install a CAS for a new hierarchy, or to expand a stand-alone primary site.

    - _Primary site_, as a stand-alone primary site that is the first site of a new hierarchy, or as a child primary:

        Select **Install a Configuration Manager primary site**.

        > [!TIP]
        > Typically, you only select the option **Use typical installation options for a stand-alone primary site** when you want to install a stand-alone primary site in a test environment. When you select this option, setup does the following actions:
        >
        > - Automatically configures the site as a stand-alone primary site.
        > - Uses a default installation path.
        > - Uses a local installation of the default instance of SQL Server for the site database.
        > - Installs a management point and a distribution point on the site server computer.
        > - Configures the site with English and the display language of the OS on the primary site server if it matches one of the languages that Configuration Manager supports.

1. On the **Product Key** page:

    - Choose whether to install Configuration Manager as an evaluation edition or a licensed edition.

        - If you select a licensed edition, enter your product key, and choose **Next**.

        - If you select an evaluation edition, choose **Next**. You can upgrade an evaluation installation to a full installation later.

    - You can also specify the **Software Assurance expiration date** of your licensing agreement. It's a convenient reminder of that date. If you don't enter this date during Setup, you can specify it later from within the Configuration Manager console.

        > [!NOTE]
        > Microsoft doesn't validate the expiration date that you entered and doesn't use this date for license validation. You can use it as a reminder of your expiration date. This date is useful because Configuration Manager periodically checks for new software updates offered online. Your software assurance license status should be current so that you're eligible to use these additional updates.

    For more information, see [Licensing and branches](../../../understand/learn-more-editions.md).

1. On the **Microsoft Software License Terms** page, read and accept the license terms.

1. On the **Prerequisite Licenses** page, read and accept the license terms for the prerequisite software. Setup downloads and automatically installs the software on site systems or clients when it's required. Accept all of the terms before you continue to the next page.

1. On the **Prerequisite Downloads** page, specify whether Setup must download the latest prerequisite redistributable files from the internet or use previously downloaded files:

    - If you want Setup to download the files at this time, select **Download required files**. Then specify a location to store the files.

    - If you previously downloaded the files by using [Setup Downloader](setup-downloader.md), select **Use previously downloaded files**. Then specify the download folder.

        > [!TIP]
        > If you use previously downloaded files, verify that the path to the download folder contains the most recent version of the files.

1. On the **Server Language Selection** page, select the languages that are available for the Configuration Manager console and for reports. The wizard selects English by default and you can't remove it. For more information, see [Language packs](language-packs.md).

1. On the **Client Language Selection** page, select the languages that are available to client computers. Also specify whether to enable all client languages for mobile device clients. The wizard selects English by default and you can't remove it.

    > [!IMPORTANT]
    > When you use a CAS, make sure that client languages you configure at the CAS include all client languages that you configure at each child primary site. Clients that install from a distribution point have access to the client languages from the top-tier site, while clients that install from a management point have access to the client languages from their assigned primary site.

1. On the **Site and Installation Settings** page, specify the following settings for the new site that you're installing:

    - **Site code**: [Each site code in a hierarchy must be unique](prepare-to-install-sites.md#bkmk_sitecodes). Use three alpha-numeric characters: `A` through `Z` and `0` through `9`. Because the site code is used in folder names, don't use the following Windows-reserved names:

        - `AUX`
        - `CON`
        - `NUL`
        - `PRN`
        - `SMS`

        > [!NOTE]
        > Setup doesn't verify whether the site code that you specify is already in use, or if it's a reserved name.

    - **Site name**: Each site requires this friendly name, which can help you identify the site.

    - **Installation folder**: This folder is the path to the Configuration Manager installation. You can't change the location after the site installs. The path can't contain Unicode characters or trailing spaces.

        > [!NOTE]
        > Consider whether you want to use the default installation folder. If you use the default OS partition in a production environment, you may experience the following issues in the future:
        >
        > - If Configuration Manager uses the additional free disk space on the OS partition, neither Windows or Configuration Manager will operate properly. If you install Configuration Manager on a separate partition, its disk consumption won't impact the OS.
        > - Configuration Manager performance is better with a fast disk. Some server designs don't optimize the OS disk for speed.
        > - You can service, restore, or reinstall the OS without impacting your Configuration Manager installation.

1. On the **Site Installation** page, use the following option that matches your scenario:

    - _I'm installing a CAS:_

        On the **Central Administration Site Installation** page, select **Install as the first site in a new hierarchy**, and then choose **Next** to continue.

    - _I'm expanding a stand-alone primary into a hierarchy with a CAS:_

        On the **Central Administration Site Installation** page, select **Expand an existing stand-alone primary into a hierarchy**. Then specify the FQDN of the stand-alone primary site server, and choose **Next** to continue.

        The media that you use to install the new CAS must match the version of the primary site.

    - _I'm installing a stand-alone primary site:_

        On the **Primary Site Installation** page, select **Install the primary site as a stand-alone site**, and then choose **Next**.

    - _I'm installing a child primary site:_

        On the **Primary Site Installation** page, select **Join the primary site to an existing hierarchy**. Then specify the FQDN for the CAS, and choose **Next**.

1. On the **Database Information** page, specify the following information:

    - **SQL Server name (FQDN)**: By default, this value is set to the site server computer.

        If you use a custom port, add that port to the FQDN of the SQL Server. Follow the FQDN of the SQL Server with a comma and then the port number. For example, for server **SQLServer1.fabrikam.com**, use the following string to specify custom port **1551**: `SQLServer1.fabrikam.com,1551`

    - **Instance name**: By default, this value is blank. It uses the default instance of SQL Server on the site server computer.

    - **Database name**: By default, this value is set to `CM_<Sitecode>`. You can customize this value.

    - **Service Broker Port**: By default, this value is set to use the default SQL Server Service Broker (SSB) port of 4022. SQL Server uses it to communicate directly to the site database at other sites.

1. On the second **Database Information** page, you can specify custom locations for the SQL Server data file and the SQL Server log file for the site database:

    - By default, it uses the default file locations for SQL Server.

    - When you use a SQL Server Always On failover cluster instance, the option to specify custom file locations isn't available.

    - The prerequisite checker doesn't run a check for free disk space for custom file locations.

1. On the **SMS Provider Settings** page, specify the FQDN for the server where you want to install the SMS Provider.

    - By default, it specifies the site server.

    - After the site installs, you can configure more SMS Providers. For more information, see [Plan for the SMS Provider](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).

1. On the **Client Communication Settings** page, choose how clients will communicate with site systems. The more secure option is to require all site systems to use HTTPS. Otherwise, you individually configure the communication method for each site system role.

    When you select **All site system roles accept only HTTPS communication from clients**, the client computer must have a valid PKI certificate for client authentication. For more information, see [PKI certificate requirements](../../../plan-design/network/pki-certificate-requirements.md).

    > [!NOTE]
    > This step only applies when you install a primary site. If you're installing a CAS, skip this step.

1. On the **Site System Roles** page, choose whether to install a management point or distribution point. For each role that you choose to have installed by Setup:

    > [!NOTE]
    > This step only applies when you install a primary site. If you're installing a CAS, skip this step.

    - Enter the **FQDN** for the server that will host the role. Then choose the client connection method that the server will support: HTTP or HTTPS.

    - If you selected **All site system roles accept only HTTPS communication from clients** on the previous page, the wizard automatically configures the client connection settings for HTTPS. You can't change this setting unless you go back to the previous page.

    > [!NOTE]  
    > To install site system roles, Setup uses the **site system installation account**. By default, it uses the primary site's computer account. This account must be a local administrator on the remote computer to install the role. If this account lacks the required permissions, don't install the roles during Setup. After you configure additional accounts to use as site system installation accounts, install the roles from the Configuration Manager console. For more information, see [Accounts](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).

1. On the **Usage Data** page, review the information about data that Microsoft collects, and then choose **Next**. For more information, see [Diagnostics and usage data](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).

1. The **Service Connection Point Setup** page is only available when you're installing a stand-alone primary site or a CAS.

    > [!NOTE]
    > If you're installing a child primary site, skip this step.

    If you're installing a CAS as part of a site expansion scenario, and the stand-alone primary site already has this role, first uninstall it from the stand-alone primary site. Configuration Manager can only have one instance of the service connection point in a hierarchy. It's only supported at the top-tier site of the hierarchy.

    After you select a configuration for the **Service Connection Point**, choose **Next**. After Setup completes, you can change this configuration from the Configuration Manager console. For more information, see [About the service connection point](../configure/about-the-service-connection-point.md).

1. On the **Settings Summary** page, review the setting that you've selected. When you're ready, choose **Next** to start the Prerequisite Checker.

1. On the **Prerequisite Installation Check** page, it lists any problems that the checker can identify.

    - When the Prerequisite Checker finds a problem, choose an item in the list for details about how to resolve the problem.

    - Before you can continue to install the site, resolve any **Failed** items. Try to resolve all **Warning** items, but they don't block installation.

    - After you resolve any issues, choose **Run Check** to rerun the Prerequisite Checker.

        When the Prerequisite Checker runs, and no checks receive a **Failed** status, you can choose **Begin Install** to start the site installation.

    > [!TIP]
    > In addition to the feedback that the wizard provides, you can find additional information about prerequisite issues in the **ConfigMgrPrereq.log** file. It's in the root of the system drive on the server. For more information, see [List of prerequisite checks](list-of-prerequisite-checks.md).

1. On the **Installation** page, Setup displays the installation status. When the core site server installation is complete, you can **Close** the installation wizard. When you close the wizard, the installation and initial site configurations continue in the background.

    - You can connect a Configuration Manager console to the site before Setup is complete. This console connects as read-only, and lets you view objects and settings, but you can't modify anything.

    - After Setup completes, you can connect a console to edit objects and settings.

    - Starting in Configuration Manager version 2010, if setup fails, you can **Report update error to Microsoft**. For more information, see [Report setup and upgrade failures to Microsoft](../../manage/post-in-console-updates.md#report-setup-and-upgrade-failures-to-microsoft).

## <a name="bkmk_expand"></a> Expand a stand-alone primary site

When you've installed a stand-alone primary site as your first site, you can later install a CAS to expand that site into a larger hierarchy. This process is also called _site expansion_. The main reason to expand to a hierarchy is for scale. A hierarchy allows you to support more clients than a stand-alone primary site can support. For more information, see [Size and scale numbers](../../../plan-design/configs/size-and-scale-numbers.md).

When you expand a stand-alone primary site, you install a new CAS that uses the existing stand-alone primary site database as a reference. After the new CAS installs, the stand-alone primary site functions as a child primary site.

- You can only expand a stand-alone primary site into a new hierarchy.

- You can only expand one stand-alone primary site into a specific hierarchy. You can't use this option to join other stand-alone primary sites into the same hierarchy. Instead, use the Migration Wizard to migrate data from one hierarchy into another. For more information, see [Migrate data between hierarchies](../../../migration/migrate-data-between-hierarchies.md).

- After you expand a stand-alone site into a hierarchy with a CAS, you can install other child primary child sites.

- To remove a primary site from a hierarchy with a CAS, first uninstall the primary site.

Before you start, first see the [prerequisites to expand a site](prerequisites-for-installing-sites.md#bkmk_expand).

To expand the site, use the procedure [to install a primary or central administration site](use-the-setup-wizard-to-install-sites.md#bkmk_installpri) with the following caveats:

- Install the CAS by using the same version of Configuration Manager as the stand-alone primary site.

- On the **Getting Started** page of the Setup Wizard, select the option to install a CAS. At a later stage of Setup, you'll choose an option to expand an existing stand-alone primary site.

- On the **Client Language Selection** page for the new CAS, select the same client languages that you configured on the original primary site.

- On the **Site Installation** page, select the option to expand the stand-alone primary site.

## <a name="bkmk_secondary"></a> Install a secondary site

Use the Configuration Manager console to install a secondary site.

- In a hierarchy, you don't have to connect the console to the parent primary site. If the console isn't connected to the parent primary site for the new secondary site, Configuration Manager replicates the command to install the secondary site to the correct primary site.

- Before you start the secondary site installation, make sure that your user account has the prerequisite permissions. Also make sure that the server that will host the new secondary site meets all the prerequisites for use as a secondary site server. For more information, see [Prerequisites for installing sites](prerequisites-for-installing-sites.md#bkmk_secondary) and [Site and site system prerequisites](../../../plan-design/configs/site-and-site-system-prerequisites.md#secondary-site-server).

- When you install the secondary site, Configuration Manager configures the new site to use the same client communication ports as the parent primary site.

### <a name="bkmk_installsecondary"></a> Process to install a secondary site

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. Select the site that will be the parent primary site of the new secondary site.

1. In the ribbon, select **Create Secondary Site**. This action starts the **Create Secondary Site Wizard**.

1. On the **Before You Begin** page, confirm that the listed server is the primary site that you want to be the parent of the new secondary site. Then choose **Next**.

1. On the **General** page, specify the following settings:

    - **Site code**: [Each site code in a hierarchy must be unique](prepare-to-install-sites.md#bkmk_sitecodes). Use three alpha-numeric characters: `A` through `Z` and `0` through `9`. Because the site code is used in folder names, don't use the following Windows-reserved names:

        - `AUX`
        - `CON`
        - `NUL`
        - `PRN`
        - `SMS`

    > [!NOTE]  
    > Setup doesn't verify whether the site code that you specify is already in use, or if it's a reserved name.  

    - **Site server name**: This value is the FQDN of the server for the new secondary site.

    - **Site name**: Each site requires this friendly name, which can help you identify the site in the console.

    - **Installation folder**: This folder is the path to the Configuration Manager installation. You can't change the location after the site installs. The path can't contain Unicode characters or trailing spaces.

    > [!IMPORTANT]
    > After you specify details on this page, you can choose **Summary** to skip to the end of the wizard. This action uses the default settings for the remainder of the secondary site options.
    >
    > - Only use this option when you're familiar with the default settings in this wizard, and they're the settings you want to use.
    >
    > - When you use the default settings, boundary groups aren't associated with the distribution point. Until you configure boundary groups that include the secondary site server, clients won't use the distribution point that's installed on this secondary site as a content source location.

1. On the **Installation Source Files** page, choose how the secondary site server gets the source files to install the site.

    When you use CD.Latest source files that are shared on the network or copied locally to the target secondary site server:

    - The CD.Latest source file location includes a folder named **Redist**. Move this **Redist** folder as a subfolder under the **SMSSETUP** folder.

    - Copy the following files from the **Redist** folder to the **SMSSETUP\BIN\X64** folder:

        - SharedManagementObjects.msi
        - SQLSysClrTypes.msi
        - sqlncli.msi

    - If any of the files from **Redist** aren't available, Setup fails to install the secondary site.

    - The computer account of the secondary site server needs **Read** permissions to the source file folder and share.

1. On the **SQL Server Settings** page, specify the version of SQL Server to use:

    > [!NOTE]
    > Setup doesn't validate the information that you enter on this page until it starts the installation. Before you continue, verify these settings.

    - **Install and configure a local copy of SQL Express on the secondary site computer**

        - **SQL Server Service port**: Specify the SQL Server service port for SQL Server Express to use. The service port is typically configured to use TCP port 1433, but you can configure another port.

        - **SQL Server Broker port**: Specify the SQL Server Service Broker (SSB) port for SQL Server Express to use. The Service Broker is typically configured to use TCP port 4022, but you can configure a different port. Specify a valid port that no other site or service is using, and that the firewall doesn't block.

    - **Use an existing SQL Server instance**

        - **SQL Server FQDN**: Review the FQDN for the computer running SQL Server. Use a local server running SQL Server to host the secondary site database, and you can't modify this setting.

        - **SQL Server instance**: Specify the instance of SQL Server to use as the secondary site database. Leave this option blank to use the default instance.

        - **ConfigMgr site database name**: Specify the name to use for the secondary site database.

        - **SQL Server Broker port**: Specify the SQL Server Service Broker (SSB) port for SQL Server to use. Specify a valid port that no other site or service is using, and that the firewall doesn't block.

    > [!TIP]
    > For a list of the SQL Server versions that Configuration Manager supports, see [Supported SQL Server versions](../../../plan-design/configs/support-for-sql-server-versions.md).

1. On the **Distribution Point** page, configure settings for the distribution point that Setup will install on the secondary site server.

    - _Required settings:_

        - **Specify how client devices communicate with the distribution point**: Choose between HTTP and HTTPS.

        - **Create a self-signed certificate or import a PKI client certificate**: Choose between using a self-signed certificate or importing a certificate from your PKI. A self-signed certificate lets you also allow anonymous connections from Configuration Manager clients to the content library. The certificate is used to authenticate the distribution point to a management point before the distribution point sends status messages. For more information, see [PKI certificate requirements](../../../plan-design/network/pki-certificate-requirements.md).

    - _Optional settings:_

        - **Install and configure IIS if required by Configuration Manager**: Select this setting to let Configuration Manager install and configure Internet Information Services (IIS) on the server. Configuration Manager only installs IIS if it's not already installed on the server. IIS is required on all distribution points.

            > [!NOTE]
            > Although this setting is optional, IIS is required to add the distribution point role.

        - **Enable and configure BranchCache for this distribution point**

        - **Description**: This value is a friendly description for the distribution point to help you recognize it in the console.

        - **Enable this distribution point for prestaged content**

1. On the **Drive Settings** page, specify the drive settings for the secondary site distribution point.

    You can configure up to two disk drives for the content library and two disk drives for the package share. However, Configuration Manager can use other drives when the first two reach the configured drive space reserve. Use this **Drive Settings** page to configure the priority for the disk drives and the amount of free disk space to remain on each disk drive.

    - **Drive space reserve (MB)**: The value that you configure for this setting determines the amount of free space on a drive before Configuration Manager chooses a different drive and continues the copy process to that drive. Content files can span multiple drives.

    - **Content Locations**: Specify the content locations for the content library and package share. Configuration Manager copies content to the primary content location until the amount of free space reaches the value that's specified for **Drive space reserve (MB)**.

    By default, the content locations are set to **Automatic**. The primary content location is set to the disk drive that has the most space at installation time. The secondary location is set to the disk drive that has the most free disk space after the primary drive. When the primary and secondary drives reach the drive space reserve, Configuration Manager selects another available drive with the most free disk space and continues the copy process.

1. On the **Content Validation** page, specify whether to validate the integrity of content files on the distribution point.

    - When you enable content validation on a schedule, Configuration Manager starts the process at the scheduled time. It verifies all content on the distribution point.

    - You can also configure the **Content validation priority**.

1. On the **Boundary Groups** page, manage the boundary groups for this distribution point:

    - **Allow fallback source location for content**: This option allows clients outside these boundary groups to fall back and use the distribution point as a source location for content when no preferred distribution points are available.

    For more information, see the [Fundamental concepts for content management](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).

1. On the **Summary** page, verify the settings, and then choose **Next** to install the secondary site. When the wizard shows the **Completion** page, you can close the wizard. The secondary site installation continues in the background.

### <a name="bkmk_verify"></a> How to verify the secondary site installation status

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

1. Select the new secondary site, and then choose **Show Install Status** in the ribbon.

    > [!TIP]
    > When you install more than one secondary site at a time, the Prerequisite Checker runs against a single site at a time. It finishes a site before it starts to check the next site.

## Next steps

[Configure sites and hierarchies](../configure/configure-sites-and-hierarchies.md)

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

[Install consoles](install-consoles.md)

[Release notes](release-notes.md)
