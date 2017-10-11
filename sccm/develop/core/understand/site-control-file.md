---
title: "Site Control File"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 850699d9-71ad-49ba-96c9-8597cd1d391esearchScope: - ConfigMgr SDK
caps.latest.revision: 15
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager Site Control File
Site control in System Center Configuration Manager defines the settings for a specific site. The settings for each site are contained in the database and are accessed through Windows Management Instrumentation (WMI) when working with scripting languages, and through the managed SMS Provider library when working with a managed language.  

> [!NOTE]
>  Previous releases of Configuration Manager had a physical file that was processed for site settings referred to as the site control file. System Center Configuration Manager stores site settings directly in the site database; however, very little has changed when programmatically configuring a site.  

## Site Control File topics  

-   [About the Configuration Manager Site Control File](../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)  

-   [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)  

-   [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)  

-   [How to Read a Configuration Manager Site Control File Embedded Property List](../../../develop/core/understand/how-to-read-a-configuration-manager-site-control-file-embedded-property-list.md)  

-   [How to Deploy a Site System Role (Example:  Fallback Status Point)](../../../develop/core/understand/how-to-deploy-a-site-system-role--example---fallback-status-point-.md)  

## Other Resources  

-   [Configuration Manager Programming Fundamentals](../../../develop/core/understand/configuration-manager-programming-fundamentals.md)  

-   [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md)  

-   [Configuration Manager Hierarchy Server WMI Classes](../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)  

## See Also  
 [Configuration Manager Programming Fundamentals](../../../develop/core/understand/configuration-manager-programming-fundamentals.md)
