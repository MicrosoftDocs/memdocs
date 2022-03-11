---
title: Setup command-line options
titleSuffix: Configuration Manager
description: Create automation scripts to install Configuration Manager from a command line.
ms.date: 02/16/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Command-line options for Configuration Manager setup

*Applies to: Configuration Manager (current branch)*

Use this information to configure scripts or to install Configuration Manager from a command line. For more information on how to use these command-line options, see [Command-line overview](use-a-command-line-to-install-sites.md).

Run `setup.exe` from the `\BIN\X64` directory of the Configuration Manager installation path on the site server.

> [!TIP]
> You can also use `setupwpf.exe` from the same folder, but it doesn't include basic prerequisite checks.

## `/DEINSTALL`

Uninstall the site. Run setup from the site server computer.

## `/DONTSTARTSITECOMP`

Install a site, but prevent the Site Component Manager service from starting. Until the Site Component Manager service starts, the site isn't active. The Site Component Manager is responsible for installing and starting the SMS_Executive service, and for other processes at the site. After the site install is finished, when you start the Site Component Manager service, it installs the SMS_Executive service and other processes that are necessary for the site to operate.

## `/HIDDEN`

Hide the user interface during setup. Only use this option with the `/SCRIPT` option. The unattended script file must provide all required options or setup fails.

## `/NOUSERINPUT`

Disable user input during setup, but display the setup wizard. Only use this option with the `/SCRIPT` option. The unattended script file must provide all required options or setup fails.

## `/RESETSITE`

Run a site reset. This action resets the database and service accounts for the site. For more information, see [Run a site reset](../../manage/modify-your-infrastructure.md#bkmk_reset).

## `/SQLMOVE`

Move the site database. This action moves the site database to a new instance of SQL Server on the same computer, or to a different computer that runs a supported version of SQL Server. For more information, see [Modify the site database configuration](../../manage/modify-your-infrastructure.md#bkmk_dbconfig).

Provide the SQL server name, database name and instance name in the following format:

`/SQLMOVE <SQL Server FQDN>:<Database Name>:<SSB Port>`

`/SQLMOVE <SQL Server FQDN>:<InstanceName>\<Database Name>:<SSB Port>`

## `/TESTDBUPGRADE`

Run a test on a backup of the site database to make sure that the database can upgrade.

> [!IMPORTANT]
> The test upgrade is no longer a required or recommend step for most sites.
>
> If your database is suspect, or is modified by customizations not explicitly supported by Configuration Manager, continue to use this process.
>
> Don't run this command-line option on your production site database. Running this command-line option on your production site database upgrades the site database and could render your site inoperable.

Provide the instance name and database name for the site database. If you specify only the database name, setup uses the default instance name.

`/TESTDBUPGRADE <Instance name>\<Database name>`

`/TESTDBUPGRADE CM_ABC`

`/TESTDBUPGRADE Named\CM_ABC`

For more information, see [Test the database upgrade when installing an update](../../manage/test-database-upgrade.md).

## `/UPGRADE`

Run an unattended upgrade of a site. Specify the product key including the dash (`-`) delimiters. Also specify the path to the previously downloaded setup prerequisite files.

For example: `/UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx C:\Setup\prereqs`

For more information about setup prerequisite files, see [Setup Downloader](setup-downloader.md).

## `/SCRIPT`

Run an unattended installation. Use a setup initialization file with this option. For more information about how to run setup unattended, see [Install sites using a command line](use-a-command-line-to-install-sites.md). For more information on the script file keys and values, see [Unattended setup script file keys](command-line-script-file.md).

For example: `/SCRIPT C:\Setup\setup.ini`

## `/SDKINST`

Install the SMS Provider on the specified server. Provide the fully qualified domain name (FQDN) for the SMS Provider computer. For more information about the SMS Provider, see [Plan for the SMS Provider](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).

For example: `/SDKINST cm02.contoso.com`

## `/SDKDEINST`

Uninstall the SMS Provider on the specified computer. Provide the FQDN for the SMS Provider computer.

For example: `/SDKDEINST cm01.contoso.com`

## `/MANAGELANGS`

Manage the languages that are installed at a previously installed site. Provide the location for the language script file that contains the language settings. For more information, see the [Keys to manage languages](command-line-script-file.md#manage-languages).

For example: `/MANAGELANGS C:\Setup\langsetup.ini`

## Next steps

[Unattended setup script file keys](command-line-script-file.md)
