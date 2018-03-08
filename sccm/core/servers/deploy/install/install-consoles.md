---
title: Install console
titleSuffix: Configuration Manager
description: Install the Configuration Manager console to connect to a central administration site or primary site.
ms.custom: na
ms.date: 03/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: 3
author: mestew
ms.author: mstewart
manager: dougeby
---
# Install the System Center Configuration Manager console

*Applies to: System Center Configuration Manager (Current Branch)*

Administrators use the Configuration Manager console to manage the Configuration Manager environment. Each Configuration Manager console can connect to a central administration site or to a primary site. You can't connect a Configuration Manager console to a secondary site.

> [!NOTE]  
>  An administrator sees objects in the console based on the permissions assigned to their user account. For more information about role-based administration, see [Fundamentals of role-based administration](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 When you install the site server, you can install the Configuration Manager console at the same time. To install the console separate from site server installation, run the standalone installer.  

 Use the following procedures to install the Configuration Manager console by using the standalone installer.  

## To install the Configuration Manager console by using the Setup Wizard  

1.  Verify that you meet these requirements:  

    -  You have local **Administrator** rights on the target computer for the console.  

    -   You have **Read** permissions to the location of the Configuration Manager console installation files.  

2.  Go to one of these locations:  

    -   On the site server, go to: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   From the Configuration Manager source media, go to: `<Configuration Manager source files>\Smssetup\Bin\I386`  

    > [!TIP]  
    >  As a best practice, start the Configuration Manager console installer from a site server rather than from the System Center Configuration Manager installation media. When you install a site server, it copies the Configuration Manager console installation files and supported language packs for the site to the **Tools\ConsoleSetup** subfolder. Installing the Configuration Manager console from the installation media always installs the English version. This behavior happens even if the site server supports different languages, or the target computer's OS is set to a different language. Optionally, you can copy the **ConsoleSetup** folder to an alternate location to start the installation.

3.  To open the Configuration Manager Console Setup Wizard, double-click **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Always install the Configuration Manager console by using **consolesetup.exe**. Although you can install the Configuration Manager console by running adminconsole.msi, this method doesn't run prerequisites or dependency checks. The installation might not install correctly.  

4.  In the wizard, select **Next**.  

5.  On the **Site Server** page, enter the fully qualified domain name (FQDN) of the site server to which the Configuration Manager console connects.  

6.  On the **Installation Folder** page, enter the installation folder for the Configuration Manager console. The folder path must not contain trailing spaces or Unicode characters.  

7.  On the **Customer Experience Improvement Program** page, select whether to join the Customer Experience Improvement Program (CEIP).  
    > [!Note]  
    > Starting in Configuration Manager version 1802 the CEIP feature is removed from the product.

8.  On the **Ready to Install** page, select **Install** to install the Configuration Manager console.  



## To install the Configuration Manager console from a command prompt  

1.  On the server from which you install the Configuration Manager console, open a command prompt window, and go to one of the following locations:  

    -   `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    > [!TIP]  
    >  Installing the Configuration Manager console from a command prompt always installs the English version. This behavior happens even if the target computer's OS is set to a different language. To install the Configuration Manager console in a language other than English, you must [install the Configuration Manager console by using the Setup Wizard](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  At the command prompt, type **consolesetup.exe**. Choose from the following command-line options:  

|  Command-line option     | Description     |
  |-------------|-------------|
  |/q|Installs the Configuration Manager console unattended. The **EnableSQM**, **TargetDir**, and **DefaultSiteServerName** options are required when you use this option.|  
  |/uninstall|Uninstalls the Configuration Manager console. Specify this option first when you use it with the **/q** option.|  
  |LangPackDir|Specifies the path to the folder that contains the language files. You can use **Setup Downloader** to download the language files. If you do not use this option, Setup looks for the language folder in the current folder. If the language folder is not found, Setup continues to install English only. For more information, see [Setup Downloader](setup-downloader.md).|  
  |TargetDir|Specifies the installation folder to install the Configuration Manager console. This option is required when you use the **/q** option.|  
  |EnableSQM|Specifies whether to join the Customer Experience Improvement Program (CEIP). Use a value of **1** to join the CEIP, and a value of **0** to not join the program. This option is required when you use the **/q** option.</br></br>Note: Starting in Configuration Manager version 1802 the CEIP feature is removed from the product.|  
  |DefaultSiteServerName|Specifies the FQDN of the site server to which the console connects when it opens. This option is required when you use the **/q** option.|  


  ### Examples

  -  `consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com`  

  -  `consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr Console" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com`  

  -  `consolesetup.exe /uninstall /q`  
