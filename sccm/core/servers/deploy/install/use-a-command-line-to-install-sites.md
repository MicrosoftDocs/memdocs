---
title: "Command-line install"
titleSuffix: "Configuration Manager"
description: "Learn how to run System Center Configuration Manager Setup at a command prompt for a variety of site installations."
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Use a command-line to install System Center Configuration Manager sites

*Applies to: System Center Configuration Manager (Current Branch)*

 You can run System Center Configuration Manager Setup at a command prompt to install a variety of site types.

## Supported tasks for command-line installations
 This method of running Setup supports the following site installation and site maintenance tasks:

- **Install a central administration site or primary site from a command prompt**  
  View [Command-line options for Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

- **Modify the languages in use at a central administration site or primary site**  
   To modify the languages that are installed at a site from a command prompt (including languages for mobile devices), you must:  

  - Run Setup from **&lt;ConfigMgrInstallationPath\>\Bin\X64** on the site server,
  - Use the **/MANAGELANGS** command-line option,
  - Specify a language script file that specifies the languages you want to add or remove,  

    For example, use the following command syntax: **setupwpf.exe /MANAGELANGS &lt;language script file\>**  

    To create the language script file, use the information in [Command line options to manage languages](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)  

- **Use an installation script file for unattended site installations or site recovery**  
   You can run Setup from a command prompt by using an installation script, and you run an unattended site installation. You can also use this option to recover a site.    

   To use a script with Setup:  

  - Run Setup with the command line-option **/SCRIPT** and specify a script file.  

  - The script file must be configured with required keys and values.  

    For an unattended installation of a central administration site or primary site, the script file must have the following sections:  

  - Identification    
  - Options    
  - SQLConfigOptions    
    -   HierarchyOptions    
  - CloudConnectorOptions   

    To recover a site, you must also include the following sections of the script file:  

  - Identification  
  - Recovery

For more information, see [Unattended site recovery for Configuration Manager](/sccm/protect/understand/unattended-recovery).  

For a list of keys and values to use in an unattended installation script file, see [Unattended Setup script file keys](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended).  

## About the command-line script file  
 For unattended installations of Configuration Manager, you can run Setup with the command-line option **/SCRIPT**, and specify a script file that contains  installation options. The following tasks are supported by using this method:  

-   Install a central administration site  
-   Install a primary site  
-   Install a configuration Manager console  
-   Recover a site  

> [!NOTE]  
>  You cannot use the unattended script file to upgrade an evaluation site to a licensed installation of Configuration Manager.  

### The CDLatest key name
When you use media from the CD.Latest folder to run a scripted install of the following four installation options, your script  must include the **CDLatest** key with a value of  **1**:
- Install a new central administration site
- Install a new primary site
- Recover a central administration site
- Recover a primary site

This value is not supported for use with installation media that you get from the Microsoft Volume License site.
See [command-line options](/sccm/core/servers/deploy/install/command-line-options-for-setup) for information on how to use this key name in the script file.



### Create the script
The installation script is automatically created when you [run Setup to install a site using the user interface](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  When you confirm the settings on the **Summary** page of the wizard, the following happens:  

-   Setup creates the script **%TEMP%\ConfigMgrAutoSave.ini**.  You can rename this file before you use it, but it must retain the .ini file extension.  
-   The unattended installation script contains the settings that you selected in the wizard.  
-   After the script is created, you can modify the script to install other sites in your hierarchy.  
-   You can then use this script to perform an unattended setup of Configuration Manager.  

This script file provides the same information that the Setup Wizard prompts for, except that there are no default settings.   
You must specify all values for the Setup keys that apply to the type of installation that you are using.   

When Setup creates the unattended installation script, it's populated with the product key value that you enter during Setup. This can be a valid product key, or **EVAL** when you install an evaluation version of Configuration Manager. The product key value in the script is populated so that the prerequisite check can finish.   

When Setup starts the actual site installation, the automatically created script is written to again to clear the product key value in the script that it creates. Before using the script for an unattended installation of a new site, you can edit the script to provide a valid product key or to specify an evaluation installation of Configuration Manager.  

### Section names, key names, and values
The script contains section names, key names, and values. Note the following information:
-   Required section key names vary depending on the installation type that you are scripting.
-   The order of the keys within sections and the order of sections within the file is not important.     
-   The keys are not case-sensitive.  
-   When you provide values for keys, the name of the key must be followed by an equal sign (=) and the value for the key.    

> [!TIP]  
>  To view the full set of options, see  [Command-line options for Setup and scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## Use the /SCRIPT Setup command-line option

-   You must use a Setup script file and specify the file name after the **/SCRIPT** Setup command-line option. Note the following information:   
    -   The name of the file must have the **.ini** file name extension.  
    -   When you reference the Setup script file at the command prompt, you must provide the full path to the file. For example, if your Setup initialization file is named Setup.ini, and it is stored in the C:\Setup folder, at the command prompt, type:  **setup /script c:\setup\setup.ini**.  

-   The account that runs Setup must have **Administrator** rights on the computer. When you run Setup with the unattended script, open the Command Prompt window by using the **Run as administrator** option.   
