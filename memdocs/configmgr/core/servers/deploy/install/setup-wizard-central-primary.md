---
title: Install a CAS or primary site
titleSuffix: Configuration Manager
description: Use the Configuration Manager setup wizard to install a new central administration site (CAS) or primary site.
ms.date: 05/02/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Use the setup wizard to install a central administration or primary site

*Applies to: Configuration Manager (current branch)*

Use this procedure to install a central administration site (CAS) or a primary site. Also use it to upgrade an evaluation site to a fully licensed Configuration Manager site.

First, review the [overview for using the setup wizard](use-the-setup-wizard-to-install-sites.md). It includes links to important prerequisite articles.

If you're installing a CAS as part of a site expansion scenario, first read [Expand a stand-alone primary site](#expand-a-stand-alone-primary-site) before using the following procedure.

## Process to install a CAS or primary site

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

    > [!IMPORTANT]
    > Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

    - **All site system roles accept only HTTPS communication from clients**: When you select this option, clients must have a valid PKI certificate for client authentication. For more information, see [PKI certificate requirements](../../../plan-design/network/pki-certificate-requirements.md).

    - **Configure the communication method on each site system role**: Starting in version 2203, when you select this option, setup configures the site to use [Enhanced HTTP](../../../plan-design/hierarchy/enhanced-http.md).<!-- 13237187 -->

    > [!NOTE]
    > This page only applies when you install a primary site. If you're installing a CAS, skip this page.

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

    - If setup fails, you can **Report update error to Microsoft**. For more information, see [Report setup and upgrade failures to Microsoft](../../manage/post-in-console-updates.md#report-setup-and-upgrade-failures-to-microsoft).

## Expand a stand-alone primary site

When you've installed a stand-alone primary site as your first site, you can later install a CAS to expand that site into a larger hierarchy. This process is also called _site expansion_. The main reason to expand to a hierarchy is for scale. A hierarchy allows you to support more clients than a stand-alone primary site can support. For more information, see [Size and scale numbers](../../../plan-design/configs/size-and-scale-numbers.md).

When you expand a stand-alone primary site, you install a new CAS that uses the existing stand-alone primary site database as a reference. After the new CAS installs, the stand-alone primary site functions as a child primary site.

- You can only expand a stand-alone primary site into a new hierarchy.

- You can only expand one stand-alone primary site into a specific hierarchy. You can't use this option to join other stand-alone primary sites into the same hierarchy. Instead, use the Migration Wizard to migrate data from one hierarchy into another. For more information, see [Migrate data between hierarchies](../../../migration/migrate-data-between-hierarchies.md).

- After you expand a stand-alone site into a hierarchy with a CAS, you can install other child primary child sites.

- To remove a primary site from a hierarchy with a CAS, first uninstall the primary site.

Before you start, first see the [prerequisites to expand a site](prerequisites-for-installing-sites.md#bkmk_expand).

To expand the site, use the [process to install a CAS or primary site](#process-to-install-a-cas-or-primary-site) with the following caveats:

- Install the CAS by using the same version of Configuration Manager as the stand-alone primary site.

- On the **Getting Started** page of the Setup Wizard, select the option to install a CAS. At a later stage of Setup, you'll choose an option to expand an existing stand-alone primary site.

- On the **Client Language Selection** page for the new CAS, select the same client languages that you configured on the original primary site.

- On the **Site Installation** page, select the option to expand the stand-alone primary site.

- If you enable Endpoint Analytics for devices uploaded to Microsoft Endpoint Manager, in version 2107 or later, re-enable this option. <!--13772757,  10362047-->

## Next steps

[Use the setup wizard to install a secondary site](setup-wizard-secondary.md)

[Configure sites and hierarchies](../configure/configure-sites-and-hierarchies.md)

[Install consoles](install-consoles.md)
