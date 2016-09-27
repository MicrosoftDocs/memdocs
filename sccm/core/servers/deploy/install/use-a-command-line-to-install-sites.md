---
title: "Command line install | System Center Configuration Manager"
ms.custom: na
ms.date: 07/22/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
caps.latest.revision: 3
author: Brenduns
---
# Use a command line to install System Center Configuration Manager sites
 If you choose, you can run System Center Configuration Manager Setup from a command prompt for a variety of site installation.

 ## Supported tasks for command-line installs
 This method of running Setup supports the following site installation and site maintenance tasks:

-   **Install a central administration site or primary site from a command line:**  
  View [Command-line options for Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

 -  **Modify the languages in use at a central administration site or primary site:**  
    To modify the languages that are installed at a site from a command line (including languages for mobile devices) you must:  

     -   Run Setup from **&lt;ConfigMgrInstallationPath\>\Bin\X64** on the site server
     -   Use the **/MANAGELANGS** command-line option
     -   Specify a language script file that specifies the languages you want to add or remove  

    For example, use the following command syntax: **setupwpf.exe /MANAGELANGS &lt;language script file\>**  

    To create the language script file, use the information in [Command line options to manage languages](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)  

 -  **Use an installation script file for unattended site installations or site recovery:**  
    You can run Setup from a command-line and direct Setup to use an installation script, and run an unattended site installation. You can also use this option to recover a site.    

    To use a script with Setup:  

    -   Run Setup with the command line-option **/SCRIPT** and specify a script file  

    -   The script file must be configured with required keys and values  

    For an unattended installation of a central administration site or primary site, the script file must be configured with the following  sections:  

    -   Identification    
    -   Options    
    -   SQLConfigOptions    
    -   HierarchyOptions    

    -   CloudConnectorOptions  

    To recover a site you must use the following sections of the script file:  

    -   Identification  

    -   Recovery

     For more information about for backup and recovery, see the Unattended Site Recovery Script File Keys section in the Backup and Recovery in Configuration Manager topic.  

    View [Unattended Setup script file keys](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended) for a list of keys and values to use in an unattended installation script file.  

## About the command-line script file  

 For unattended installations of Configuration Manager you can run Setup with the command line option **/SCRIPT** and specify a script file that contains  installation options. The following tasks are supported by this method:  

-   Install a central administration site  

-   Install a primary site  

-   Install a configuration Manager console  

-   Recover a site  

> [!NOTE]  
>  You cannot use the unattended script file to upgrade an evaluation site to a licensed installation of Configuration Manager.  

**To create the script**:  
The installation script is automatically created when you [run Setup to install a site using the user interface](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  When you confirm the settings on the **Summary** page of the wizard:  

-   Setup creates the script **%TEMP%\ConfigMgrAutoSave.ini**.  You can rename this file before you use it, but it must retain the .ini file extension.  

-   The unattended installation script contains the settings that you selected in the wizard.  

-   After the script is created, you can modify the script to install other sites in your hierarchy.  

-   You can then use this script to perform an unattended setup of Configuration Manager.  

This script file provides the same information that the Setup Wizard prompts for, except that there are no default settings.   
All values must be specified for the setup keys that apply to the type of installation that you are using.  

When Setup creates the unattended installation script, it is populated with the product key value that you enter during setup. This can be a valid product key, or it is equal to EVAL when you install an evaluation version of Configuration Manager. The product key value in the script is populated to enable the prerequisite check to finish.  

When Setup starts the actual site installation, the automatically created script is written to again to clear the product key value in the script that it creates. Before using the script for an unattended installation of a new site, you can edit the script to provide a valid product key or specify an evaluation installation of Configuration Manager.  

**The script contains section names, key names, and values:**  

-   Required section key names vary depending on the installation type that you are scripting  

-   The order of the keys within sections, and the order of sections within the file, is not important  

-   The keys are not case sensitive  

-   When you provide values for keys, the name of the key must be followed by an equals sign (=) and the value for the key  

> [!TIP]  
>  To view the full set of options, see  [Command-line options for Setup and scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_cmdtop).  

## To use the /SCRIPT Setup command-line option:

-   You must use a setup script file and specify the file name after the **/SCRIPT** Setup command-line option.  

    -   The name of the file must have the **.ini** file name extension  

    -   When you reference the Setup script file at the command prompt, you must provide the full path to the file. For example, if your Setup initialization file is named Setup.ini, and it is stored in the C:\Setup folder, at the command prompt, type:  **setup /script c:\setup\setup.ini**  

-   The account that runs setup must have administrative credentials on computer. When you run Setup with the unattended script, start the command prompt by using **Run as administrator**  
