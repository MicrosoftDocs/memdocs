---
title: "The content library"
description: "Learn about the content library that System Center Configuration Manager uses to reduce the overall size of distributed content."
ms.custom: na
ms.date: 2/14/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# The content library in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The content library is a single-instance store of content that System Center Configuration Manager uses to reduce the overall size of the combined body of content that you distribute. The content library stores all content files for software updates, applications, operating system deployments, and so on.

 - A copy of the content library is automatically created and maintained on each **site server** and on each **distribution point**.

 - Before Configuration Manager downloads content files to the site server or copies the files to distribution points, Configuration Manager verifies whether each content file is already in the content library.
 - If the content file is available, Configuration Manager does not copy the file and instead associates the existing content file with the application or package.

On computers where you install a distribution point, you can configure:

- One or more disk drives on which you want to create the content library.
- A priority for each drive that you use.

When Configuration Manager copies content files, it copies them to the drive with the highest priority until that drive contains less than a minimum amount of free space that you specify.
- You configure the drive settings during the distribution point installation.
- You cannot configure the drive settings in the distribution point properties after the installation has finished.


For more information about how to configure the drive settings for the distribution point, see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


>  [!IMPORTANT]  
>  To move the content library to a different location on a distribution point after the installation, use the **Content Library Transfer tool** in the System Center 2012 R2 Configuration Manager Toolkit. You can download the toolkit from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=279566).  

## About the content library on the central administration site  
 By default, Configuration Manager creates a content library on the central administration site when the site is installed. The content library is placed on the drive of the site server that has the most free disk space. Because you cannot install a distribution point on the central administration site, you cannot prioritize the drives for use by the content library. Similar to the content library on other site servers and on distribution points, when the drive that contains the content library runs out of available disk space, the content library automatically spans to the next available drive.  

 Configuration Manager uses the content library on the central administration site in the following scenarios:  

-   When you create content on the central administration site.  

-   When you migrate content from another Configuration Manager site and assign the central administration site as the site that manages that content.  

> [!NOTE]  
>  When you create content at a primary site and then distribute it to a different primary site or a secondary site below a different primary site, the central administration site temporarily stores that content in the scheduler inbox on the central administration site but does not add that content to its content library.  

 Use the following options to manage the content library on the central administration site:  

-   To prevent the content library from being installed on a specific drive, create an empty file named **no_sms_on_drive.sms**, and then copy it to the root folder of the drive before the content library is created.  

-   After the content library has been created, use **Content Library Transfer tool** from the System Center 2012 R2 Configuration Manager Toolkit to manage the location of the content library. You can download the toolkit from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=279566).  
