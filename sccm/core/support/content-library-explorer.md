---
title: Content Library Explorer
titleSuffix: Configuration Manager
description: Use the Content Library Explorer to view and troubleshoot the content library on a Configuration Manager distribution point. 
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Content Library Explorer

*Applies to: System Center Configuration Manager (Current Branch)*

Content Library Explorer is one of the [Configuration Manager tools](/sccm/core/support/tools). Use the tool for the following activities:  

- Explore the content library on a specific distribution point  

- Troubleshoot issues with the content library  

- Copy packages, contents, folders, and files out of the content library  

- Redistribute packages to the distribution point  

- Validate packages on remote distribution points  



## Requirements

- Run the tool using an account that has administrative access to:  

    - The target distribution point  

    - The WMI provider on the site server  

    - The Configuration Manager provider  

- Only the **Full Administrator** and **Read-Only Analyst** roles have sufficient rights to view all information from this tool.  

    - Other roles, such as **Application Administrator**, can view partial information. For more information, see [Disabled packages](#bkmk_disabled-packages).  

    - The **Read-Only Analyst** can't redistribute packages from this tool.  

- Run the tool from any computer, as long as it can connect to:  

    - The target distribution point  

    - The primary site server  

    - The Configuration Manager provider  

- If the distribution point is colocated with the site server, it's still necessary to have administrative access to the site server.  



## Usage 

When you start **ContentLibraryExplorer.exe**, enter the fully qualified domain name (FQDN) of the target distribution point. It then connects to the distribution point. If the distribution point is part of a secondary site, it prompts you for the FQDN of the primary site server, and the primary site code.

In the left pane, view the packages that are distributed to this distribution point. Expand the packages, and explore their folder structure. This structure matches the folder structure from which you created the package.

When you select a folder, it displays in the right pane any files within the folder. This view includes the following information: 
- File name
- File size
- Which drive it's on
- Other packages that use the same file on the drive
- When the file was last changed on the distribution point

The tool also connects to the Configuration Manager provider. This connection is to determine which packages are distributed to the distribution point, and whether they're actually in the distribution point’s content library. For instance, a package that's pending distribution may not yet exist in the content library. Such a package would appear as "PENDING" in the tool, and no actions are enabled for this package.


### <a name="bkmk_disabled-packages"></a> Disabled packages

Some packages are present on the distribution point but not visible in the Configuration Manager console. These packages are marked with an asterisk (\*). No actions may be performed on these packages. Other packages may also be marked with an asterisk and have actions disabled. 

There are three primary reasons for disabled packages:  

- The package is the Configuration Manager client upgrade. This package includes "ccmsetup.exe".  

- Your user account can't access the package, likely due to role-based administration. For instance, the **Application Author** role can't see driver packages in the console, so any driver packages on the distribution point are marked as disabled.  

- The package is orphaned on the distribution point.  


### Validate packages

Validate packages by using **Package** > **Validate** on the toolbar. First select a package node in the left pane Don't select a content or a folder. The tool connects to the WMI provider on the distribution point for this action. When the tool starts, packages that are missing one or more contents are marked invalid. Validating the package reveals which content is missing. If all content is present but the data is corrupted, validation detects the corruption.


### Redistribute packages

Redistribute packages using **Package** > **Redistribute** on the toolbar. First select a package node in the left pane. This action requires permissions to redistribute packages.


### Other actions

Use **Edit** > **Copy** to copy packages, contents, folders, and files out of the content library to a specified folder. You can't copy the content library itself. Select more than one file, but you can't select multiple folders.

Search for packages using **Edit** > **Find Package**. This action searches for your query in the package name and package ID.



## Limitations

- The tool can't manipulate the content library directly in any way. Changes to the content library may result in malfunctions.  

- The tool can redistribute packages, but only to the target distribution point.  

- When you colocate the distribution point with the site server, you can't validate package data. Use the Configuration Manager console instead. The tool still inspects the package to make sure that all the content is present, though not necessarily intact.  

- You can't delete content with this tool.



## See also

- [Fundamental concepts for content management](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [The content library](/sccm/core/plan-design/hierarchy/the-content-library)
