---
title: "Setup Downloader"
description: "Read about this standalone application designed to ensure your site installation uses current versions of key installation files."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
caps.latest.revision: 3
author: Brendunsms.author: brendunsmanager: angrobe
---
# Setup Downloader for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Before you run Setup to install or upgrade a System Center Configuration Manager site, you can use the Setup Downloader standalone application from the version of Configuration Manager that you want to install to download updated Setup files.  

Using updated Setup files ensures that your site installation uses current versions of key installation files. In oveview:   
-   When you use Setup Downloader to download files prior to starting setup, you specify a folder to contain the files.  
-   The account you use to run Setup Downloader must have **Full Control** permissions to the download folder.  
-   When you run Setup to install or upgrade a site, you can direct it to use this local copy of files you previously downloaded. This prevents Setup form having to connect to Microsoft when you start the site install or upgrade.  
-   You can use the same local copy of setup files for subsequent site installations or upgrades.  

The following types of files are downloaded by Setup Downloader:  
-   Required prerequisite redistributable files  
-   Language packs  
-   The latest product updates for Setup  

You have two options for running Setup Downloader:
- Run the application with the user interface
- For command-line options, run the application at a command prompt


## Run Setup Downloader with the user interface  

1.  On a computer that has Internet access, open Windows Explorer, and go to **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**.  

2.  To open Setup Downloader, double-click **Setupdl.exe**.   

3. Specify the path for the folder that will host the updated installation files, and then click **Download**. Setup Downloader verifies the files that are currently in the download folder. It downloads only files that are missing or that are newer than existing files. Setup Downloader creates subfolders for downloaded languages, and other required subfolders.  

4.  To review the download results, open the **ConfigMgrSetup.log** file in the root directory of drive C.  .  

## Run Setup Downloader from a command prompt  

1.  In a Command Prompt window, go to **&lt;*Configuration Manager installation media*\>\SMSSETUP\BIN\X64**.   

2.  To open Setup Downloader, run  **Setupdl.exe**.

    You can use the following command-line options with **Setupdl.exe**:   

    -   **/VERIFY**: Use this option to verify the files in the download folder, which include language files. Review the ConfigMgrSetup.log file in the root directory of drive C for a list of files that are outdated. No files are downloaded when you use this option.  

    -   **/VERIFYLANG**: Use this option to verify the language files in the download folder. Review the ConfigMgrSetup.log file in the root directory of drive C for a list of language files that are outdated.

    -   **/LANG**: Use this option to download only the language files to the download folder.  

    -   **/NOUI**: Use this option to start Setup Downloader without displaying the user interface. When you use this option, you must specify the **download path** as part of the command at the command prompt.  

    -   **&lt;DownloadPath\>**: You can specify the path to the download folder to automatically start the verification or download process. You must specify the download path when you use the **/NOUI** option. If you do not specify a download path, you must specify the path when Setup Downloader opens. Setup Downloader creates the folder if it does not exist.  

    Example commands:

    -   **setupd &lt;DownloadPath\>**  

        -   Setup Downloader starts, verifies the files in the specified download folder, and then downloads only the files that are missing or that have newer versions than existing files.     

    -   **setupdl /VERIFY &lt;DownloadPath\>**  

        -   Setup Downloader starts and verifies the files in the specified download folder.  

    -   **setupdl /NOUI &lt;DownloadPath\>**  

        -   Setup Downloader starts, verifies the files in the specified download folder, and then downloads only the files that are missing or that are newer than the existing files.  

    -   **setupdl /LANG  &lt;DownloadPath\>**  

        -   Setup Downloader starts, verifies the language files in the specified download folder, and then downloads only the language files that are missing or that are newer than the existing files.  

    -   **setupdl /VERIFY**  

        -   Setup Downloader starts, and then you must specify the path to the download folder. Next, after you click **Verify**, Setup Downloader verifies the files in the download folder.  

3.  To review the download results, open the **ConfigMgrSetup.log** file in the root directory of drive C.
