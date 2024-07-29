---
title: Install a secondary site
titleSuffix: Configuration Manager
description: Use the Configuration Manager setup wizard to install a new secondary site.
ms.date: 04/08/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Use the setup wizard to install a secondary site

*Applies to: Configuration Manager (current branch)*

Use this procedure to install a secondary site. Install a secondary site from within the Configuration Manager console. Secondary sites don't support a scripted command-line installation.

- In a hierarchy, you don't have to connect the console to the parent primary site. If the console isn't connected to the parent primary site for the new secondary site, Configuration Manager replicates the command to install the secondary site to the correct primary site.

- Before you start the secondary site installation, make sure that your user account has the prerequisite permissions. Also make sure that the server that will host the new secondary site meets all the prerequisites for use as a secondary site server. For more information, see [Prerequisites for installing sites](prerequisites-for-installing-sites.md#bkmk_secondary) and [Site and site system prerequisites](../../../plan-design/configs/site-and-site-system-prerequisites.md#secondary-site-server).

- When you install the secondary site, Configuration Manager configures the new site to use the same client communication ports as the parent primary site.

Before you start, review the [overview for using the setup wizard](use-the-setup-wizard-to-install-sites.md). It includes links to important prerequisite articles.

## Process to install a secondary site

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

            > [!IMPORTANT]
            > Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

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

### How to verify the secondary site installation status

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

1. Select the new secondary site, and then choose **Show Install Status** in the ribbon.

    > [!TIP]
    > When you install more than one secondary site at a time, the Prerequisite Checker runs against a single site at a time. It finishes a site before it starts to check the next site.

## Next steps

[Configure sites and hierarchies](../configure/configure-sites-and-hierarchies.md)

[Install consoles](install-consoles.md)
