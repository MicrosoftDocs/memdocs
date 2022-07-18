---
title: Hotfix installer
titleSuffix: Configuration Manager
description: Find out when and how to install updates via the Hotfix Installer for Configuration Manager.
ms.date: 07/15/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Use the Hotfix Installer to install updates for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Some updates for Configuration Manager aren't available from the Microsoft cloud service. These updates are available out-of-band. An example is a limited release hotfix to address a specific issue.

When you need to install an update that you get from Microsoft:

- If the update has the simple file extension **.exe**: Use the hotfix installer that's included with that download. Install the update directly to the Configuration Manager site server.

- If the hotfix file has the **.update.exe** file extension: [Use the update registration tool to import hotfixes to Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).

## Overview

Hotfixes for Configuration Manager are similar to updates for other Microsoft products, such as SQL Server. They contain either one individual fix or a bundle, which is a rollup of fixes.

- Individual updates include a single focused update for a specific version of Configuration Manager.
- Update bundles include multiple updates for a specific version of Configuration Manager.
- When an update is a bundle, you can't install individual updates from that bundle.

If you plan to create deployments to install updates on other computers, install the update bundle on a central administration site (CAS) server or primary site server.

When you run the update bundle, the following process happens:

- It extracts the update files for each applicable component from the update bundle.

- Starts a wizard that guides you through a process to configure the updates and deployment options for the updates.

- After you complete the wizard, the updates in the bundle that apply to the site server are installed on the site server.

The wizard also creates deployments that you can use to install the updates on other computers. Deploy the updates to other computers by using a supported deployment method. For example, a software deployment package or System Center Updates Publisher.

When the wizard runs, it creates a **.cab** file on the site server for use with Updates Publisher. Optionally, you can configure the wizard to also create one or more packages for software deployment. You can use these deployments to install updates on components, such as clients or the Configuration Manager console. You can also install updates manually on computers that don't run the Configuration Manager client.

You can update the following three groups in Configuration Manager:

- Configuration Manager server roles, which include:

  - CAS

  - Primary site

  - Secondary site

  - Remote SMS Provider

- Configuration Manager console

- Configuration Manager client

> [!NOTE]
> Updates for site system roles are installed as part of the update for site servers. They are serviced by the site component manager. This behavior includes updates for the site database and the cloud management gateway (CMG).
>
> Pull-distribution points are serviced by distribution manager instead of the site component manager.

Each update bundle for Configuration Manager is a self-extractable .exe file (SFX). This file contains the files that are necessary to install the update on the applicable components of Configuration Manager. Typically, the SFX file can contain the following files:

|File|Details|
|----------|-------------|
|`<Product version>-QFE-KB<KB article ID>-<platform>-<language>.exe`|This file is the update. The command line for this file is managed by Updatesetup.exe. For example: `CM1511RTM-QFE-KB123456-X64-ENU.exe`|
|`Updatesetup.exe`|This MSI wrapper manages the installation of the update bundle. When you run the update, Updatesetup.exe detects the display language of the computer where it runs. By default, the user interface for the update is in English. However, when the display language is supported, the user interface displays in the computer's local language.|
|`License_<language>.rtf`|When applicable, each update contains one or more license files for supported languages.|
|`<Product&updatetype>-<product version>-<KB article ID>-<platform>.msp`|When the update applies to the Configuration Manager console or clients, the update bundle includes separate Windows Installer patch (.msp) files. For example: `ConfigMgr1511-AdminUI-KB1234567-i386.msp` for the console or `ConfigMgr1511-client-KB1234567-x64.msp` for the client.|

By default, the update bundle logs its actions to a .log file on the site server. The log file has the same name as the update bundle and is written to the `%SystemRoot%/Temp` folder.

When you run the update bundle, it extracts a file with the same name as the update bundle to a temporary folder on the computer, and then runs Updatesetup.exe. Updatesetup.exe starts the software update wizard.

As applicable to the scope of the update, the wizard creates a series of folders under the Configuration Manager installation folder on the site server. The folder structure is similar to the following example: `\Hotfix\<KB Number>\<Update Type>\<Platform>`

The following table provides details about the folders in the folder structure:

|Folder name|More information|
|-----------------|----------------------|
|`<KB Number>`|This folder is the ID number for this update bundle.|
|`<Update type>`|This folder is the type of update for Configuration Manager. The wizard creates a separate folder for each type of update in the bundle. They include the following types:<br/><br/>- **Server**: Includes updates to site servers, site database servers, and SMS Providers.<br/>- **Client**: Includes updates to the Configuration Manager client.<br />- **AdminConsole**: Includes updates to the Configuration Manager console<br/><br /> The wizard also creates a folder named **SCUP**, which contains the .cab file for Updates Publisher.|
|`<Platform>`|This folder is platform-specific. It contains update files that are specific to a type of processor. These folders include: **x64** and **I386**.|

## How to install updates

To install updates, first install the update bundle on a site server. When you install an update bundle, it starts an install wizard for that update. This wizard does the following actions:

- Extracts the update files

- Helps you configure deployments

- Installs applicable updates on the server components of the local computer

After you install the update bundle on a site server, you can then update other components for Configuration Manager. The following table describes update actions for these various components:

|Component|Instructions|
|---------------|------------------|
|Site server|Deploy updates to a remote site server when you don't choose to install the update bundle directly on that remote site server.|
|Site database|For remote site servers, deploy server updates that include an update to the site database if you don't install the update bundle directly on that remote site server.|
|Configuration Manager console|After initial installation of the Configuration Manager console, you can install updates for the console on each computer that runs it. You can't modify the console installation files to apply the updates during the initial installation of the console.|
|Remote SMS Provider|Install updates for each instance of the SMS Provider that runs on a computer other than the site server where you installed the update bundle.|
|Configuration Manager clients|After initial installation of the Configuration Manager client, you can install updates for the Configuration Manager client on each computer that runs the client.|

> [!NOTE]
> You can deploy updates only to computers that run the Configuration Manager client.

If you reinstall a client, Configuration Manager console, or SMS Provider, also reinstall the updates for these components.

### Update servers

Updates for servers can include updates for sites, the site database, and computers that run an instance of the SMS Provider.

#### Update a site

To update a Configuration Manager site, you can install the update bundle directly on the site server. You can also deploy the updates to a site server after you install the update bundle on a different site.

When you install an update on a site server, the update installation process manages other actions that are required to apply the update, such as updating site system roles. The exception is the site database. The next section contains information about how to update the site database.

#### Update a site database

To update the site database, the installation process runs a file named **update.sql** on the site database. You can configure the update process to automatically update the site database, or you can manually update the site database later.

##### Automatic update of the site database

When you install the update bundle on a site server, you can choose to automatically update the site database when the server update is installed. This decision applies only to the site server where you install the update bundle and doesn't apply to deployments that are created to install the updates on remote site servers.

> [!NOTE]
> When you choose to automatically update the site database, the process updates a database regardless whether the database is located on the site server or on a remote computer.

> [!IMPORTANT]
> Before you update the site database, create a backup of the site database. You can't uninstall an update to the site database. For information about how to create a backup for Configuration Manager, see [Backup and recovery for Configuration Manager](backup-and-recovery.md).

##### Manual update of the site database

If you choose not to automatically update the site database when you install the update bundle on the site server, the server update doesn't modify the database on the site server where the update bundle runs. However, deployments that use the package that is created for software deployment or that installs always update the site database.

> [!WARNING]
> When the update includes updates to both the site server and the site database, the update isn't functional until the update is completed for both the site server and site database. Until the update is applied to the site database, the site is in an unsupported state.

1. On the site server, stop the **SMS_SITE_COMPONENT_MANAGER** service. Then stop the **SMS_EXECUTIVE** service.

1. Close the Configuration Manager console.

1. Run the update script named **update.sql** on that site's database. For information about how to run a script to update a SQL Server database, see the documentation for the version of SQL Server that you use for your site database server.

    > [!TIP]
    > When the update bundle installs, it extracts **update.sql** to the following location on the site server: `\\<Server Name>\SMS_<Site Code>\Hotfix\<KB Number>\update.sql`.

1. Restart the services that you stopped in the previous step.

#### Update a computer that runs the SMS Provider

After you install an update bundle that includes updates for the SMS Provider, deploy the update to each computer that runs the SMS Provider. The only exception is the instance of the SMS Provider that was previously installed on the site server where you install the update bundle. The local instance of the SMS Provider on the site server is updated when you install the update bundle.

If you remove and then reinstall the SMS Provider on a computer, reinstall the update for the SMS Provider on that computer.

### Update clients

When you install an update that includes updates for the Configuration Manager client, you can automatically upgrade clients with the update installation, or manually upgrade clients at a later time. For more information about automatic client upgrade, see [How to upgrade clients for Windows computers](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).

You can deploy updates with Updates Publisher or a software deployment package. You can also manually install the update on each client. For more information about how to use deployments to install updates, see [Deploy updates for Configuration Manager](#deploy-updates-for-configuration-manager).

> [!IMPORTANT]
> When you install updates for clients and the update bundle includes updates for servers, install the server updates on the primary site to which the clients are assigned.

To manually install the client update, run **Msiexec.exe** on each Configuration Manager client. Include the platform-specific client update MSP file in the command line. For example, you can use the following command line for a client update:

`msiexec.exe /p \\<ServerName>\SMS_<SiteCode>\Hotfix\<KB Number>\Client\<Platform>\<msp> /L\*v <logfile> REINSTALLMODE=mous REINSTALL=ALL`

### Update Configuration Manager consoles

To update a Configuration Manager console, install the update on the computer that runs the console.

> [!IMPORTANT]
> When you install updates for the Configuration Manager console, and the update bundle includes updates for servers, also install the server updates on the site that you use with the Configuration Manager console.

If the computer that you update runs the Configuration Manager client:

- You can use a deployment to install the update. For more information about how to use deployments to install updates, see [Deploy updates for Configuration Manager](#deploy-updates-for-configuration-manager).

- If you're signed in to the client computer, run the installation interactively.

To manually install the Configuration Manager console update, run **Msiexec.exe**. Include the Configuration Manager console update MSP file in the command line. For example, you can use the following command line to update a Configuration Manager console:

`msiexec.exe /p \\<ServerName>\SMS_<SiteCode>\Hotfix\<KB Number>\AdminConsole\<Platform>\<msp> /L\*v <logfile> REINSTALLMODE=mous REINSTALL=ALL`

## Deploy updates for Configuration Manager

After you install the update bundle on a site server, you can use one of the following three methods to deploy updates to other computers.

### Use Updates Publisher to install updates

When you install the update bundle on a site server, the installation Wizard creates a catalog file for Updates Publisher. You can use this file to deploy the updates to applicable computers. The wizard always creates this catalog, even when you select the option **Use package and program to deploy this update**.

The catalog for Updates Publisher is named **SCUPCatalog.cab**. It's in the following location on the computer where you ran the update bundle: `\\<ServerName>\SMS_<SiteCode>\Hotfix\<KB Number>\SCUP\SCUPCatalog.cab`

> [!IMPORTANT]
> The SCUPCatalog.cab file is created by using paths that are specific to the site server where the update bundle is installed. It can't be used on other site servers.

After the wizard is finished, import the catalog to Updates Publisher. Then use software updates to deploy the updates. For more information, see [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).

#### Import the updates to Updates Publisher

1. Start the Updates Publisher console and select **Import**.

1. On the **Import Type** page of the Import Software Updates Catalog Wizard, select **Specify the path to the catalog to import**. Then specify the SCUPCatalog.cab file.

1. Select **Next**, and then select **Next** again.

1. In the **Security Warning - Catalog Validation** window, select **Accept**. Close the wizard after it's finished.

1. Select the update that you want to deploy, and then select **Publish**.

1. On the **Publish Options** page of the Publish Software Updates Wizard, select **Full Content**, and then select **Next**.

1. Complete the wizard to publish the updates.

### Use software deployment to install updates

When you install the update bundle on the site server of a primary site or CAS, you can configure the installation Wizard to create update packages for software deployment. Then deploy each package to a collection of computers that you want to update.

To create a software deployment package, on the **Configure Software Update Deployment** page of the wizard, select each update package type that you want to update. The available types can include servers, Configuration Manager consoles, and clients. A separate package is created for each type of update that you select.

> [!NOTE]
> The package for servers contains updates for the following components:
>
> - Site server
> - SMS Provider
> - Site database

Next, on the **Configure Software Update Deployment Method** page of the wizard, select the option **I will use software distribution**.

After the wizard is finished, view the packages in the Configuration Manager console. Go to the **Packages** node in the **Software Library** workspace. Use your standard process to deploy software packages to Configuration Manager clients. When a package runs on a client, it installs the updates to the applicable components of Configuration Manager on the client computer.

For more information about how to deploy packages to Configuration Manager clients, see [Packages and programs](../../../apps/deploy-use/packages-and-programs.md).

### Create collections for deploying updates to Configuration Manager

You can deploy specific updates to applicable clients. The following information can help you to create device collections for the different components for Configuration Manager.

|Component of Configuration Manager|Instructions|
|----------------------------------------|------------------|
|CAS server|Create a direct membership query and add the CAS server.|
|All primary site servers|Create a direct membership query and add each primary site server.|
|All secondary site servers|Create a direct membership query and add each secondary site server.|
|All x86 clients|Create a collection with the following query criteria: `Select * from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X86-based PC"`|
|All x64 clients|Create a collection with the following query criteria: `Select * from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X64-based PC"`|  
|All computers that run the Configuration Manager console|Create a direct membership query and add each computer.|
|Remote computers that run an instance of the SMS Provider|Create a direct membership query and add each computer.|

> [!NOTE]
> To update a site database, deploy the update to the site server for that site.

For more information, see [How to create collections](../../../core/clients/manage/collections/create-collections.md).
