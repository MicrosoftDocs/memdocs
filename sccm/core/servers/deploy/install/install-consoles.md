---
title: "Install consoles | System Center Configuration Manager"
description: "Read about installing Configuration Manager consoles to connect to a central administration site or a primary site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: 3
author: Brendunsms.author: brendunsmanager: angrobe
---
# Install System Center Configuration Manager consoles*Applies to: System Center Configuration Manager (Current Branch)*

Administrative users use the System Center Configuration Manager console to manage the Configuration Manager environment. Each Configuration Manager console can connect to a central administration site or a primary site. You cannot connect a Configuration Manager console to a secondary site.


> [!NOTE]  
>  The objects that are displayed for the administrative user who is running the console depend on the rights that are assigned to the administrative user. For more information about role-based administration, see [Fundamentals of role-based administration for System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 You can install the Configuration Manager console during the site server installation in the Setup Wizard, or run the stand-alone application.  

 Use the following procedure to install a Configuration Manager console by using the stand-alone application.  

## To install a Configuration Manager console  

1.  Verify that the administrative user who runs the Configuration Manager console application has the following security rights:  

    -   **Local Administrator** rights on the computer on which the console will run.  

    -   **Read** permission to the location for the Configuration Manager console installation files.  

2.  Browse to one of the following locations:  

    -   From the Configuration Manager source media, browse to **&lt;ConfigMgrSourceFiles\>\Smssetup\Bin\I386**  

    -   On the site server, browse to **&lt;ConfigMgrSiteServerInstallationPath\>\Tools\ConsoleSetup**  

    > [!TIP]  
    >  As a best practice, initiate the Configuration Manager console installation from a site server rather than the System Center Configuration Manager installation media. The site server installation method copies the Configuration Manager console installation files and the supported language packs for the site to the **Tools\ConsoleSetup** subfolder. If you install the Configuration Manager console from the installation media, this installation method always installs the English version, regardless of the supported languages on the site server or the language settings for the operating system that is running on the computer. Optionally, you can copy the **ConsoleSetup** folder to an alternate location to start the installation.  

3.  Double-click **consolesetup.exe**. The Configuration Manager Console Setup Wizard opens.  

    > [!IMPORTANT]  
    >  Always install the Configuration Manager console by using consolesetup.exe. Although the Configuration Manager console can be installed by running AdminConsole.msi, this method does not run prerequisite or dependency checks and the installation might not install correctly.  

4.  On the opening page, click **Next**.  

5.  On the **Site Server** page, specify the fully qualified domain name (FQDN) of the site server to which the Configuration Manager console will connect.  

6.  On the **Installation Folder** page, specify the installation folder for the Configuration Manager console. The folder path must not contain trailing spaces or Unicode characters.  

7.  On the **Customer Experience Improvement Program** page, choose whether to join the Customer Experience Improvement Program.  

8.  On the **Ready to Install** page, click **Install** to install the Configuration Manager console.  

## To install a Configuration Manager console from a command prompt  

1.  On the server from which you install the Configuration Manager console, open a command prompt window and browse to one of the following locations:  

    -   **&lt;ConfigMgrSiteServerInstallationPath\>\Tools\ConsoleSetup**  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  When you install a Configuration Manager console from a command prompt, it always installs the English version regardless of the language setting for the operating system that is running on the computer. To install the Configuration Manager console in another language, you must use the previous procedure to install it.  

2.  Type **consolesetup.exe** and choose from the following command-line options.  

|  Command-line option     | Description     |
  | :------------- | :------------- |
  |/q|Installs the Configuration Manager console unattended. The **EnableSQM**, **TargetDir**, and **DefaultSiteServerName** options are required when you use this option.|  
  |/uninstall|Uninstalls the Configuration Manager console. You must specify this option first when you use it with the **/q** option.|  
  |LangPackDir|Specifies the path to the folder that contains the language files. You can use **Setup Downloader** to download the language files. If you do not use this option, Setup looks for the language folder in the current folder. If the language folder is not found, Setup continues to install English only. For more information, see [Setup Downloader](/sccm/core/servers/deploy/install/setup-downloader).|  
  |TargetDir|Specifies the installation folder to install the Configuration Manager console. This option is required when you use the **/q** option.|  
  |EnableSQM|Specifies whether to join the Customer Experience Improvement Program (CEIP). Use a value of 1 to join the Customer Experience Improvement Program, and a value of 0 to not join the program. This option is required when you use the **/q** option.|  
  |DefaultSiteServerName|Specifies the FQDN of the site server to which the console connects when it opens. This option is required when you use the **/q** option.|  


  **Usage examples:**  
  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  
