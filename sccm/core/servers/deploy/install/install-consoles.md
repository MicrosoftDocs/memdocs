---
title: "Install console"
titleSuffix: "Configuration Manager"
description: "Read about installing the Configuration Manager console to connect to a central administration site or primary site."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Install the System Center Configuration Manager console

*Applies to: System Center Configuration Manager (Current Branch)*

Administrators use the System Center Configuration Manager console to manage the Configuration Manager environment. Each Configuration Manager console can connect to a central administration site or to a primary site. You cannot connect a Configuration Manager console to a secondary site.

> [!NOTE]  
>  Which objects an administrator who is running the console sees depends on the permissions that are assigned to their user account. For more information about role-based administration, see [Fundamentals of role-based administration for System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 You can install the Configuration Manager console during the site server installation through the Setup Wizard, or you can run a standalone installation application that uses the Setup Wizard.  

 Use the following procedure to install a Configuration Manager console by using the standalone application.  

## To install the Configuration Manager console by using the Setup Wizard  

1.  Verify that you meet these requirements:  

    -  You have **Local Administrator** rights on the computer on which the console will run.  

    -   You have **Read** permissions to the location of the Configuration Manager console installation files.  

2.  Go to one of these locations:  

    -   On the site server, go to **<*Configuration Manager site server installation path*>\Tools\ConsoleSetup**.  

    -   From the Configuration Manager source media, go to **<*Configuration Manager source files*>\Smssetup\Bin\I386**.  

    > [!TIP]  
    >  As a best practice, initiate the Configuration Manager console installation from a site server rather than from the System Center Configuration Manager installation media. The site server installation method copies the Configuration Manager console installation files and supported language packs for the site to the **Tools\ConsoleSetup** subfolder. Installing the Configuration Manager console from the installation media always installs the English version, regardless of the supported languages on the site server or the language settings of the operating system that is running on the computer. Optionally, you can copy the **ConsoleSetup** folder to an alternate location to start the installation.

3.  To open the Configuration Manager Console Setup Wizard, double-click **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Always install the Configuration Manager console by using consolesetup.exe. Although the Configuration Manager console can be installed by running adminconsole.msi, this method does not run prerequisites or dependency checks, and the installation might not install correctly.  

4.  In the wizard, select **Next**.  

5.  On the **Site Server** page, enter the fully qualified domain name (FQDN) of the site server to which the Configuration Manager console will connect.  

6.  On the **Installation Folder** page, enter the installation folder for the Configuration Manager console. The folder path must not contain trailing spaces or Unicode characters.  

7.  On the **Customer Experience Improvement Program** page, select whether to join the Customer Experience Improvement Program (CEIP).  

8.  On the **Ready to Install** page, select **Install** to install the Configuration Manager console.  

## To install the Configuration Manager console from a command prompt  

1.  On the server from which you install the Configuration Manager console, open a Command Prompt window and go to one of the following locations:  

    -   **<*Configuration Manager site server installation path*>\Tools\ConsoleSetup**  

    -   **<*Configuration Manager installation media*>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  When you install the Configuration Manager console from a command prompt, the English version is always installed, regardless of the language setting of the operating system that is running on the computer. To install the Configuration Manager console in a language other than English, you must [install the Configuration Manager console by using the Setup Wizard](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  At the command prompt, type **consolesetup.exe**. Choose from the following command-line options.  

|  Command-line option     | Description     |
  | :------------- | :------------- |
  |/q|Installs the Configuration Manager console unattended. The **EnableSQM**, **TargetDir**, and **DefaultSiteServerName** options are required when you use this option.|  
  |/uninstall|Uninstalls the Configuration Manager console. You must specify this option first when you use it with the **/q** option.|  
  |LangPackDir|Specifies the path to the folder that contains the language files. You can use **Setup Downloader** to download the language files. If you do not use this option, Setup looks for the language folder in the current folder. If the language folder is not found, Setup continues to install English only. For more information, see [Setup Downloader](setup-downloader.md).|  
  |TargetDir|Specifies the installation folder to install the Configuration Manager console. This option is required when you use the **/q** option.|  
  |EnableSQM|Specifies whether to join the Customer Experience Improvement Program (CEIP). Use a value of **1** to join the CEIP, and a value of **0** to not join the program. This option is required when you use the **/q** option.|  
  |DefaultSiteServerName|Specifies the FQDN of the site server to which the console connects when it opens. This option is required when you use the **/q** option.|  


  **Examples:**

  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  
