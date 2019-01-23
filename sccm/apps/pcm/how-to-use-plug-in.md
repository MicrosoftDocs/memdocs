---
title: How to use the conversion plug-in
titleSuffix: Configuration Manager
description: Use the Package Conversion Manager plug-in to customize the analysis and conversion processes.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
---

# How to use the Package Conversion Manager plug-in

*Applies to: System Center Configuration Manager (Current Branch)*

<!--1357861-->

The Package Conversion Manager plug-in helps you customize the analysis and conversion processes. To use the Package Conversion Manager plug-in, write an executable or script file that performs custom operations. Then edit the configuration file, Microsoft.ConfigurationManagement.exe.config, to call the executable or script. The most common languages used to write the script are VBScript or PowerShell.

The Package Conversion Manager plug-in runs once for each package. If you analyze or convert multiple packages at one time, the Package Conversion Manager plug-in runs each time.

> [!NOTE]  
> For more information on the Package Conversion Manager elements in the Configuration Manager configuration file, see [Technical reference for the Package Conversion Manager plug-in configuration XML](/sccm/apps/pcm/plugin-config-xml).



## Default process

By default, Package Conversion Manager does the following actions:

1.  Read a Configuration Manager package.  

2.  Create an application from the package, and add default attributes.  

3.  Analyze the application and determine a package readiness state.  

4.  Take one of the following actions, depending on the Package Conversion Manager operation:  

    - **Analyze**: Display the package readiness state in the Configuration Manager console.  

    - **Convert**: Write the application to the Configuration Manager database.  


## Plug-in-based process 

When you use the plug-in, Package Conversion Manager does the following actions:

1.  Read a Configuration Manager package.  

2.  Create an application from the package, and add default attributes.  

3.  Convert the application to XML. Then save the file to disk.  

4.  Run the plug-in script to modify the application XML. For more information, see [Technical reference for the Package Conversion Manager plug-in configuration XML](/sccm/apps/pcm/plugin-config-xml).  

5.  Convert the application XML into a Configuration Manager application.  

6.  Analyze the application, and determine a package readiness state.  

7.  Take one of the following actions, depending on the Package Conversion Manager operation:  

    - **Analyze**: Display the package readiness state in the Configuration Manager console.  

    - **Convert**: Write the application to Configuration Manager database.  



## See also

[Technical reference for the Package Conversion Manager plug-in configuration XML](/sccm/apps/pcm/plugin-config-xml)
