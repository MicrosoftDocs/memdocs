---
title: Service connection tool
titleSuffix: Configuration Manager
description: Learn about this tool that enables you to connect to the Configuration Manager cloud service to manually upload usage information.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Use the service connection tool for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use the **service connection tool** when your service connection point is in offline mode. You can also use it when your Configuration Manager site system servers aren't connected to the internet. The tool can help you keep your site up to date with the latest updates to Configuration Manager.

When you run the tool, it connects to the Configuration Manager cloud service, uploads usage information for your hierarchy, and downloads updates. Uploading usage data is necessary to enable the cloud service to provide the correct updates for your environment.

## Prerequisites

- The site has a service connection point, and you configure it for an **Offline, on-demand connection**.

- Run the tool from a command prompt as an administrator. There's no user interface.

- You run the tool from the service connection point and a computer that can connect to the internet. Each of these computers needs to have a x64-bit OS, and have the following components:

  - Both the **Visual C++ Redistributable** x86 and x64 files. By default, Configuration Manager installs the x64 version on the computer that hosts the service connection point. To download this component, see [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784).

  - Starting in version 2107, this tool requires .NET version 4.6.2, and version 4.8 is recommended.<!--10402814--> In version 2103 and earlier, this tool requires .NET 4.5.2 or later. For more information, [Site and site system prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md).

- The account you use to run the tool needs the following permissions:

  - **Local administrator** on the computer that hosts the service connection point

  - **Read** permissions to the site database

- You need a method to transfer the files between the computer with internet access and the service connection point. For example, a USB drive with sufficient free space to store the files and updates.

## Overview

1. **Prepare**: Run the tool on the service connection point. It puts your usage data into a .cab file at the location you specify. Copy the data file to the computer with an internet connection.

2. **Connect**: Run the tool on the computer with an internet connection. It uploads your usage data, and then downloads Configuration Manager updates. Copy the downloaded updates to the service connection point.

    You can upload multiple data files at one time, each from a different hierarchy. You can also specify a proxy server and a user for the proxy server.

3. **Import**: Run the tool on the service connection point. It imports the updates, and adds them to your site. You can then view and [install those updates](install-in-console-updates.md) in the Configuration Manager console.

### Upload multiple data files

- Put all exported data files from separate hierarchies into the same folder. Give each file a unique name. If necessary, you can manually rename them.

- When you run the tool to upload data to Microsoft, you specify the folder that contains the data files.

- When you run the tool to import data, the tool only imports the data for that hierarchy.

### Specify a proxy server

If the computer with an internet connection requires a proxy server, the tool supports a basic proxy configuration. Use the optional parameters **-proxyserveruri** and **-proxyusername**. For more information, see [Command-line parameters](#bkmk_cmd).

### Specify the type of updates to download

The tool supports options to control what files you download. By default, the tool downloads only the latest available update that applies to the version of your site. It doesn't download hotfixes.

To modify this behavior, use one of the following parameters to change what files it downloads:

- **-downloadall**: Download all updates, including updates and hotfixes, whatever the version of your site.
- **-downloadhotfix**: Download all hotfixes whatever the version of your site.
- **-downloadsiteversion**: Downloads updates and hotfixes with a later version than the version of your site.

    > [!IMPORTANT]
    > Because of a known issue in Configuration Manager version 2002, the default behavior doesn't work as expected. Update to version 2006, or use the **-downloadsiteversion** parameter to download the necessary updates for version 2002.<!-- 7594517 -->

For more information, see [Command-line parameters](#bkmk_cmd).

> [!TIP]
> The tool determines the version of your site from the data file. To verify the version, look in the .cab file for the text file named with the site version.

## Use the tool  

The service connection tool is in the Configuration Manager installation media at the following path: `SMSSETUP\TOOLS\ServiceConnectionTool\ServiceConnectionTool.exe`. Always use the service connection tool that matches the version of Configuration Manager that you use. All of these files must be in the same folder for the service connection tool to work.

Copy the **ServiceConnectionTool** folder with all of its contents to the computer with an internet connection.

In this procedure, the command-line examples use the following file names and folder locations. You don't need to use these paths and file names. You can use alternatives that match your environment and preferences.

- The path to the Configuration Manager installation media source files on the service connection point: `C:\Source`

- The path to a USB drive where you store the data to transfer between computers: `D:\USB\`

- The name of the data file that you export from the site: `UsageData.cab`

- The name of the empty folder where the tool stores downloaded updates for Configuration Manager: `UpdatePacks`

### Prepare

1. On the computer that hosts the service connection point, open a command prompt as an administrator, and change directory to the tool location. For example:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Run the following command to prepare the data file:

    `ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

    > [!NOTE]
    > If you'll upload data files from more than one hierarchy at the same time, give each data file a unique name. If necessary, you can rename files later.

    The data in the file is based on the level of diagnostic and usage data that you configure for the site. For more information, see [Overview of diagnostics and usage data](../../plan-design/diagnostics/diagnostics-and-usage-data.md). You can use the tool to export the data to a CSV file to view the contents. For more information, see [-export](#-export).

1. After the tool finishes exporting the usage data, copy the data file to a computer that has access to the internet.

### Connect

1. On the computer with internet access, open a command prompt as an administrator, and change directory to the tool location. This location is a copy of the entire **ServiceConnectionTool** folder. For example:

    `cd D:\USB\ServiceConnectionTool\`

1. Run the following command to upload the data file and download the Configuration Manager updates:

    `ServiceConnectionTool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

    For more examples, see [Command line parameters](#bkmk_cmd).

    > [!NOTE]  
    > When you run this command line, you might see the following error:
    >
    > **Unhandled Exception: System.UnauthorizedAccessException: Access to the path 'C:\Users\jqpublic\AppData\Local\Temp\extractmanifestcab\95F8A562.sql' is denied.**
    >
    > You can safely ignore this error. Close the error window to continue.

1. After the tool finishes downloading the updates, copy them to the service connection point.

### Import

1. On the computer that hosts the service connection point, open a command prompt as an administrator, and change directory to the tool location. For example:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Run the following command to import the updates:

    `ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

1. After the import completes, close the command prompt. It only imports updates for the applicable hierarchy.

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Updates and Servicing** node. Imported updates are now available to install. For more information, see [Install in-console updates](install-in-console-updates.md).

## Log files

- **ServiceConnectionTool.log**: Each time you run the service connection tool, it writes to this log file. The path of the log file is always the same location as the tool. This log file provides simple details about the tool usage based on the parameters you use. Each time you run the tool, the tool replaces any existing log file.

- **ConfigMgrSetup.log**: During the [Connect](#connect) phase, the tool writes to this log file at the root of the system drive. This log file provides more detailed information. For example, what files the tool downloads, and if the hash checks are successful.

## <a name="bkmk_cmd"></a> Command-line parameters

This section lists in alphabetical order all of the available parameters for the service connection tool.

### -connect

Use during the [Connect](#connect) phase on the computer with internet access. It connects to the Configuration Manager cloud service to upload the data file, and download updates.

It requires the following parameters:

- **-usagedatasrc**: The location of the data file to upload
- **-updatepackdest**: A path for the downloaded updates

You can also use the following optional parameters:

- **-proxyserveruri**: The FQDN of the proxy server
- **-proxyusername**: A user name for the proxy server
- **-downloadall**: Download everything, including updates and hotfixes, whatever the version of your site.
- **-downloadhotfix**: Download all hotfixes, whatever the version of your site.
- **-downloadsiteversion**: Download updates and hotfixes that have a later version than the version of your site.

#### Example of connect without a proxy server

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks`

#### Example of connect with a proxy server

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itproxy.contoso.com -proxyusername jqpublic`

#### Example of connect to download only site version applicable updates

`ServiceConnectionTool.exe -connect -downloadsiteversion -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

### -dest

A required parameter with the **-export** parameter to specify the path and file name of the CSV file to export. For more information, see [-export](#-export).

### -downloadall

An optional parameter with the **-connect** parameter to download everything, including updates and hotfixes, whatever the version of your site. For more information, see [-connect](#connect).

### -downloadhotfix

An optional parameter with the **-connect** parameter to only download all hotfixes, whatever the version of your site. For more information, see [-connect](#-connect).

### -downloadsiteversion

An optional parameter with the **-connect** parameter to only download updates and hotfixes that have a later version than the version of your site. For more information, see [-connect](#-connect).

### -export

Use during the [Prepare](#prepare) phase to export usage data to a CSV file. Run it as an administrator on the service connection point. This action lets you review the contents of the usage data before you upload to Microsoft. It requires the **-dest** parameter to specify the location of the CSV file.

#### Example of export

`-export -dest D:\USB\usagedata.csv`

### -import

Use during the [Import](#import) phase on the service connection point to import the updates to the site. It requires the **-updatepacksrc** parameter to specify the location of the downloaded updates.

#### Example of import

`ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

### -prepare

Use during the [Prepare](#prepare) phase on the service connection point to export usage data from the site. It requires the **-usagedatadest** parameter to specify the location of the exported data file.

#### Example of prepare

`ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

### -proxyserveruri

An optional parameter with the **-connect** parameter to specify the FQDN of your proxy server. For more information, see [-connect](#-connect).

### -proxyusername

An optional parameter with the **-connect** parameter to specify the username to authenticate with your proxy server. For more information, see [-connect](#-connect).

### -updatepackdest

A required parameter with the **-connect** parameter to specify a path for the downloaded updates. For more information, see [-connect](#-connect).

### -updatepacksrc

A required parameter with the **-import** parameter to specify a path of the downloaded updates. For more information, see [-import](#-import).

### -usagedatadest

A required parameter with the **-prepare** parameter to specify a path and file name of the exported data file. For more information, see [-prepare](#-prepare).

## Next steps

[Install in-console updates](install-in-console-updates.md)

[How to view diagnostics and usage data](../../plan-design/diagnostics/view-diagnostics-and-usage-data.md)
