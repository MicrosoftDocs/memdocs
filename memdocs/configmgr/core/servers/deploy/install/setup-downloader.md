---
title: Setup downloader tool
titleSuffix: Configuration Manager
description: Use the standalone tool to download current versions of key installation files for setup.
ms.date: 02/16/2022
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

# Setup Downloader for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Before you run Configuration Manager setup to install or upgrade a site, you can use the setup downloader standalone tool to download updated setup files. Run the tool from the version of Configuration Manager that you want to install. Use updated setup files to make sure your site installation uses current versions of key installation files.

When you use setup downloader, you specify a folder to contain the files. The account you use to run the tool must have **Full Control** permissions to the download folder. When you run setup to install or upgrade a site, you can specify this local copy of files you previously downloaded. This behavior prevents setup from connecting to Microsoft when you start the site install or upgrade. You can use the same local copy of setup files for other site installations or upgrades of the same version.

The setup downloader tool downloads the following types of files:

- Required prerequisite redistributable files
- Language packs
- The latest product updates for setup

You have two options to run setup downloader:

- Run the application with the user interface
- Run the application at a command prompt for additional command-line options

If your organization restricts network communication with the internet using a firewall or proxy device, you need to allow the tool to access internet endpoints. The device where you'll run the tool requires internet access the same as the service connection point. For more information, see [Internet access requirements](../../../plan-design/network/internet-endpoints.md#updates-and-servicing).<!-- SCCMDocs#677 -->

## <a name="bkmk_ui"></a> Run setup downloader with the user interface

1. On a computer that has internet access, browse to the installation media for the version of Configuration Manager that you want to install.

1. In the **SMSSETUP\BIN\X64** subfolder, run **Setupdl.exe**.

1. Specify the path for the folder to store the updated installation files, and then select **Download**. Setup downloader verifies the files that are currently in the download folder. It downloads only files that are missing or that are newer than existing files. It creates subfolders for downloaded languages, and other required components.

1. To review the download results, see **C:\ConfigMgrSetup.log**.

## <a name="bkmk_cmd"></a> Run setup downloader from a command prompt

1. Open a command prompt, and change directory to the installation media for the version of Configuration Manager that you want to install.

1. Change directory to the **SMSSETUP\BIN\X64** subfolder, and run **Setupdl.exe** with the necessary options.

1. To review the download results, see **C:\ConfigMgrSetup.log**.

### Command-line options

You can use the following command-line options with **Setupdl.exe**:

- `/VERIFY`: Verify the files in the download folder, which include language files. For the list of outdated files, review **C:\ConfigMgrSetup.log**. When you use this option, it doesn't download any files.

- `/VERIFYLANG`: Only verify the language files in the download folder. For the list of outdated language files, review **C:\ConfigMgrSetup.log**.

- `/LANG`: Download only the language files to the download folder.

- `/NOUI`: Start setup downloader without the user interface. When you use this option, the **download path** is required.

- **Download path**: To automatically start the verification or download process, specify the path to the download folder. When you use the `/NOUI` option, the download path is required. If you don't specify a download path, setup downloader prompts you to specify the path. If the folder doesn't exist, setup downloader creates it.

### Example commands

#### Example 1

Setup downloader verifies the files in the specified download folder, and then downloads files.

`setupdl.exe C:\Download`

#### Example 2

Setup downloader only verifies the files in the specified download folder.

`setupdl.exe /VERIFY C:\Download`

#### Example 3

Setup downloader verifies the files in the specified download folder, and then downloads files. The tool doesn't show any user interface.

`setupdl.exe /NOUI C:\Download`

#### Example 4

Setup downloader verifies the language files in the specified download folder, and then downloads only the language files.

`setupdl.exe /LANG C:\Download`

## <a name="bkmk_cp-files"></a> Copy setup downloader files to another computer

1. In Windows Explorer, go to either one of the following locations:

    - **&lt;Configuration Manager installation media>\SMSSETUP\BIN\X64**

    - **&lt;Configuration Manager installation path>\BIN\X64**

1. Copy the following files to the same destination folder on the other computer:

    - **setupdl.exe**

    - **.\\&lt;language>\\setupdlres.dll**

        > [!NOTE]
        > This file is in the subfolder for the install language. For instance, English is in the `00000409` subfolder.

    The destination folders on your device should look like the following example:

    - `C:\ConfigManInstall\setupdl.exe`

    - `C:\ConfigManInstall\00000409\setupdlres.dll`

1. Run the setup downloader from the destination computer. Use either the [user interface](#bkmk_ui) or the [command prompt](#bkmk_cmd).
