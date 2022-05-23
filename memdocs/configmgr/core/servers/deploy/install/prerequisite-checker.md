---
title: Prerequisite checker
titleSuffix: Configuration Manager
description: Learn how to use prerequisite checker to identify and fix problems that might block a site or site system role installation.
ms.date: 02/16/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---
# Prerequisite Checker for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Before you run Setup to install or upgrade a Configuration Manager site, or before you install a site system role on a new server, you can use this stand-alone application (**Prereqchk.exe**) from the version of Configuration Manager that you want use to verify server readiness. Use Prerequisite Checker to identify and fix problems that would block a site or site system role installation.

> [!NOTE]
> Prerequisite Checker always runs as part of Setup.

By default, when Prerequisite Checker runs:

- It validates the server where it runs.
- The local computer is scanned for an existing site server, and only the checks that are applicable to the site are run.
- If no existing sites are detected, all prerequisite rules are run.
- It checks rules to verify that software and settings required for setup are installed. It's possible that some prerequisites require other configurations or software updates that the tool doesn't check.
- It logs its results in the **ConfigMgrPrereq.log** file on the system drive of the computer. The log file might contain more information that doesn't appear in the tool.

When you run Prerequisite Checker at a command prompt and specify specific command-line options:

- Prerequisite Checker only runs the checks that are associated with the site server or site systems that you specify in the command line.
- To check a remote computer, your user account must have Administrator rights to the remote computer.

For more information, see [List of prerequisite checks](list-of-prerequisite-checks.md).

## Source folders

By default, the prerequisite checker tool is in one of the following locations:

- `<Configuration Manager installation media>\SMSSETUP\BIN\X64`
- `<Configuration Manager installation path>\BIN\X64`

## Copy to another computer

1. In Windows Explorer, go to one of the `X64` source folders.

1. Copy the following files to the destination folder on the other computer:

    - prereqchk.exe
    - prereqcore.dll
    - prereqchkres.dll
      This file is in the subfolder for the install language. For example, English is in the `00000409` subfolder. <!--586808-->
    - basesql.dll
    - basesvr.dll
    - baseutil.dll

## Run with default checks

1. In Windows Explorer, go to one of the `X64` source folders.

1. Run **prereqchk.exe** to start Prerequisite Checker.

  > [!NOTE]
  > The tool requires administrative permissions on the local computer.

Prerequisite Checker detects existing sites, and if found, runs the checks for upgrade readiness. If no sites are found, it runs all checks. The **Site Type** column provides information about the site server or site system with which the rule is associated.

In the Prerequisite Checker user interface, Prerequisite Checker creates a list of discovered problems in the **Prerequisite result** section.

- Select an item in the list for details about how to resolve the problem.
- Before you install the component, resolve all items in the list that have an **Error** status.
- To review results after you close the tool, open the **ConfigMgrPrereq.log** file in the root of the system drive. The log file might contain more information that's not displayed in the tool.

:::image type="content" source="media/prereq-checker.png" alt-text="Configuration Manager installation prerequisite check tool.":::

## Run from a command prompt

1. Open a Windows command prompt as an administrator and change directory to one of the `X64` source folders.

1. To start Prerequisite Checker and run all prerequisite checks on the server, run the following command: `prereqchk.exe /LOCAL`

You can also run it with other command-line options. For example, to check a primary site:

`prereqchk.exe /PRI /SQL sql01.contoso.com /SDK cmprov01.contoso.com /JOIN cas.contoso.com /MP mp01.contoso.com /DP dp01.contoso.com`

## Command-line options

There are four installation scenarios. The following list summarizes all of the command-line options for each scenario:

- **Central administration site (CAS)**
  - _Required_
    - `/CAS`
    - `/SDK`
    - `/SQL`
  - _Optional_
    - `/EXPAND`
    - `/INSTALLDIR`
    - `/NOUI`
    - `/SCP`
    - `/SSBPORT`
- **Primary site**
  - _Required_
    - `/PRI`
    - `/SDK`
    - `/SQL`
  - _Optional_
    - `/DP`
    - `/INSTALLDIR`
    - `/JOIN`
    - `/MP`
    - `/NOUI`
    - `/SCP`
    - `/SSBPORT`
- **Secondary site**
  - _Required_
    - `/SEC`
  - _Optional_
    - `/INSTALLDIR`
    - `/INSTALLSQLEXPRESS`
    - `/NOUI`
    - `/SECUPGRADE`
    - `/SOURCEDIR`
    - `/SQLPORT`
    - `/SSBPORT`
- **Configuration Manager console**
  - `/ADMINUI`

For more information on these options, see the following sections.

### `/AdminUI`

_Applies to: Console_

Required. This option verifies that the local computer meets the requirements for installing the Configuration Manager console. It doesn't check any server requirements. You can't combine this option with any other option.

### `/CAS`

_Applies to: CAS_

Required. This option verifies that the local server meets the requirements for the CAS. You can't combine it with the `/PRI` or `/SEC` options.

### `/DP`

_Applies to: Primary_

Optional. Specify the FQDN of the server to host the distribution point role, for example: `/PRI /DP dp01.contoso.com`

This option verifies that the specified server meets the requirements for the distribution point site system role. This option can be used alone or with the `/PRI` option.

### `/Expand`

_Applies to: CAS_

Optional. Specify the FQDN of a primary site, for example: `/CAS /EXPAND cmprimary.contoso.com`

This option verifies that the referenced primary site meets the requirements to expand a hierarchy with a CAS.

### `/InstallDir`

_Applies to: CAS, Primary, Secondary_

Optional. Specify the local installation path, for example `/InstallDir C:\ConfigMgr`

This option verifies the minimum disk space for site installation.

### `/InstallSQLExpress`

_Applies to: Secondary_

Optional. This option verifies that SQL Server Express can be installed on the specified secondary site server.

### `/Join`

_Applies to: Primary_

Optional. Specify the FQDN of the CAS server, for example, `/PRI /JOIN cas.contoso.com`

This option verifies that the local server meets the requirements for connecting to the CAS server.

### `/MP`

_Applies to: Primary_

Optional. Specify the FQDN of the server to host the management point role, for example: `/PRI /MP mp01.contoso.com`

This option verifies that the specified server meets the requirements for the management point site system role. This option can be used alone or with the `/PRI` option.

### `/NoUI`

_Applies to: CAS, Primary, Secondary_

Optional. This option starts the prerequisite checker without displaying the user interface. Specify this option before any other option in the command line.

### `/Pri`

_Applies to: Primary_

Required. This option verifies that the local server meets the requirements for a primary site. You can't combine it with the `/CAS` or `/SEC` options.

### `/SCP`

_Applies to: CAS, Primary_

Optional. Specify the FQDN of the server to host the service connection point. This server may be the same as the site server.

Starting in version 2111<!--11104731-->, this option verifies that the specified computer meets the requirements for the service connection point site system role. You can use this option alone or with the `/PRI` or `/CAS` options.

### `/SDK`

_Applies to: CAS, Primary_

Required. Specify the FQDN of the server to host the SMS Provider role. This server may be the same as the site server.

This option verifies that the specified server meets the requirements for the SMS Provider.

### `/Sec`

_Applies to: Secondary_

Required. Specify the FQDN of the secondary site server, for example: `/SEC sec01.contoso.com`

This option verifies that the specified server meets the requirements for the secondary site. You can't combine it with the `/CAS` or `/PRI` options.

### `/SecUpgrade`

_Applies to: Secondary_

Optional. Specify the FQDN of the secondary site server, for example: `/SECUPGRADE sec01.contoso.com`

This option verifies that the specified server meets the requirements for the secondary site upgrade. You can't combine it with the `/CAS`, `/PRI`, or `/SEC` options.

### `/SourceDir`

_Applies to: Secondary_

Optional. This option verifies that the computer account of the secondary site can access the folder that hosts the source files for Configuration Manager setup.

### `/SQL`

_Applies to: CAS, Primary_

Required. Specify the fully qualified domain name (FQDN) of the SQL Server, for example `/SQL sql01.contoso.com`

This option verifies that the specified server meets the requirements for SQL Server to host the Configuration Manager site database.

### `/SQLPort`

_Applies to: Secondary_

Optional. This option verifies that a firewall exception exists to allow communication for the SQL Server service port. It also checks that the port isn't in use by another named instance of SQL Server. The default port is 1433.

### `/SSBPort`

_Applies to: CAS, Primary, Secondary_

Optional. This option verifies that a firewall exception exists to allow communication on the SQL Server Service Broker (SSB) port. The default SSB port is 4022.
