---
title: Install console
titleSuffix: Configuration Manager
description: Install the Configuration Manager console to connect to a central administration site or primary site.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby


---

# Install the Configuration Manager console

*Applies to: Configuration Manager (current branch)*

Administrators use the Configuration Manager console to manage the Configuration Manager environment. Each Configuration Manager console can connect to a central administration site (CAS) or to a primary site. You can't connect a Configuration Manager console to a secondary site.

The Configuration Manager console is always installed on the site server for the CAS or a primary site. To install the console separate from site server installation, run the standalone installer.  



## Prerequisites

- You have local **Administrator** rights on the target computer for the console.  

- You have **Read** permissions to the location of the Configuration Manager console installation files.  



## Source paths

Decide which source path to use:  

- ConsoleSetup folder on the site server: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    When you install a site server, it copies the console installation files and supported language packs for the site to the **Tools\ConsoleSetup** subfolder. Optionally, you can copy the **ConsoleSetup** folder to an alternate location to start the installation. When you update the site, it always keeps its local version up to date.  

- Configuration Manager installation media: `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    Installing the Configuration Manager console from the installation media always installs the English version. This behavior happens even if the site server supports different languages, or the target computer's OS is set to a different language.  

When possible, start the console installer from the **ConsoleSetup** folder rather than from the source media.

> [!Important]  
> Don't install the console using the **CD.Latest** source files. It's an unsupported scenario, and may cause problems with the console installation. For more information, see [The CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder#unsupported-scenarios).<!-- SCCMDocs issue 1359 -->  

If you create a package for installing the console on other computers, make sure the package includes the following files:<!--3612513-->

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab (starting in version 1902)
- ConfigMgr.AC_Extension.amd64.cab (starting in version 1902)



## Use the Setup Wizard  

1. Browse to the source path, and open **ConsoleSetup.exe**.  

    > [!IMPORTANT]  
    > Always install the console by using **ConsoleSetup.exe**. Although you can install the Configuration Manager console by running AdminConsole.msi, this method doesn't run prerequisites or dependency checks. The installation might not install correctly.  

2. In the wizard, select **Next**.  

3. On the **Site Server** page, enter the fully qualified domain name (FQDN) of the site server to which the Configuration Manager console connects.  

4. On the **Installation Folder** page, enter the installation folder for the Configuration Manager console. The folder path can't include trailing spaces or Unicode characters.  

5. On the **Customer Experience Improvement Program** page, select whether to join the Customer Experience Improvement Program (CEIP).  

    > [!Note]  
    > Starting in Configuration Manager version 1802, the CEIP feature is removed from the product.

6. On the **Ready to Install** page, select **Install**.  



## Install from a command prompt  

> [!TIP]  
> Installing the Configuration Manager console from a command prompt always installs the English version. This behavior happens even if the target computer's OS is set to a different language. To install the Configuration Manager console in a language other than English, [use the Setup Wizard](#use-the-setup-wizard).  


### ConsoleSetup.exe command-line options

#### /q

Installs the Configuration Manager console unattended. The **EnableSQM**, **TargetDir**, and **DefaultSiteServerName** options are required when you use this option.

#### /uninstall

Uninstalls the Configuration Manager console. Specify this option first when you use it with the **/q** option.

#### LangPackDir

Specifies the path to the folder that contains the language files. You can use **Setup Downloader** to download the language files. If you don't use this option, Setup looks for the language folder in the current folder. If the language folder isn't found, Setup continues to install English only. For more information, see [Setup Downloader](setup-downloader.md).

#### TargetDir

Specifies the installation folder to install the Configuration Manager console. This option is required when you use the **/q** option.

#### EnableSQM

Specifies whether to join the Customer Experience Improvement Program (CEIP). Use a value of **1** to join the CEIP, and a value of **0** to not join the program. This option is required when you use the **/q** option.

> [!Important]  
> Starting in Configuration Manager version 1802, the CEIP feature is removed from the product. Using the parameter will cause the install to fail.

#### DefaultSiteServerName

Specifies the FQDN of the site server to which the console connects when it opens. This option is required when you use the **/q** option.


### Examples

> [!Important]  
> For version 1802 and later, don't include the **EnableSQM** parameter

#### Silent install

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### Silent install with language packs

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### Silent uninstall

`ConsoleSetup.exe /uninstall /q`  



## See also

An administrator sees objects in the console based on the permissions assigned to their user account. For more information, see [Fundamentals of role-based administration](/sccm/core/understand/fundamentals-of-role-based-administration).

For more information on the fundamentals of navigating the Configuration Manager console, see [Using the console](/sccm/core/servers/manage/admin-console).
