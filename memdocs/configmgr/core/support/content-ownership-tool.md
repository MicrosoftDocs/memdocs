---
title: Content Ownership Tool
titleSuffix: Configuration Manager
description: Use the Content Ownership Tool to change ownership of orphaned packages in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.author: baladell 
author: BalaDelli
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Content Ownership Tool

*Applies to: Configuration Manager (current branch)*

Content Ownership Tool is one of the [Configuration Manager tools](tools.md). It changes ownership of orphaned packages in Configuration Manager. Orphaned packages don't have an owning site server. Packages can become orphaned by removing the site server while they're still owned by this site server.

Run the Content Ownership Tool on any site server in the Configuration Manager hierarchy. Sign in as an administrative user with sufficient package permissions.  

> [!Tip]  
> Use **ContentLibraryCleanup.exe** in `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` to *remove* orphaned content from a distribution point. For more information, see [Content library cleanup tool](../plan-design/hierarchy/content-library-cleanup-tool.md).  



## Features

- Display all orphaned packages  

- Display all packages, even if they're not orphaned  

- View the status of the connection to a site  

- Filter packages by name, site code, or package type  

- Sort by any displayed column  

- Change assignment of one or more packages with a single action  

- View progress of the ownership transfer activity  



## Usage

Run **ContentOwnershipTool.exe** to start the tool. Local administrator permissions on the computer aren't required to run the tool.

There are no command-line parameters.

> [!Important]   
> This tool changes the ownership of an orphaned package. The package itself doesn't move from the distribution point that it's stored on. This ownership change doesn't cause the package to update on distribution points. It also doesn't cause clients to reevaluate policy for deployment of the package. After the ownership changes, make sure that the new site server can access the source files. It should have at least **Read** permissions to the source files of each package. 



## See also

- [Fundamental concepts for content management](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [The content library](../plan-design/hierarchy/the-content-library.md)
