---
title: The content library
titleSuffix: Configuration Manager
description: Learn about the content library that Configuration Manager uses to reduce the overall size of distributed content.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# The content library in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The content library is a single-instance store of content in Configuration Manager. The site uses it to reduce the overall size of the combined body of content that you distribute. The content library stores all content files for software deployments, for example: software updates, applications, and OS deployments.  

- The site automatically creates and maintains a copy of the content library on each site server and each distribution point.  

- Before Configuration Manager adds content files to the site server or copies the files to distribution points, it verifies whether each content file is already in the content library.  

- If the content file is available, Configuration Manager doesn't copy the file. It instead associates the existing content file with the application or package.  

On distribution point servers, configure the following options:

- One or more disk drives on which you want to create the content library.  

- A priority for each drive that you use.  

Configuration Manager copies content files to the drive with the highest priority until that drive contains less than a minimum amount of free space that you specify.  

- You configure the drive settings during the distribution point installation.  

- You can't configure the drive settings in the distribution point properties after the installation has finished.  


For more information about how to configure the drive settings for the distribution point, see [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  


>  [!IMPORTANT]  
>  To move the content library to a different location on a distribution point after the installation, use the **Content Library Transfer** tool in the Configuration Manager Toolkit. Starting in version 1806, the toolkit is now available on the site server. For more information, see [Configuration Manager Toolkit](/sccm/core/support/toolkit). Otherwise, download the toolkit from the [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkId=279566). 



## About the content library on the central administration site  
By default, Configuration Manager creates a content library on the central administration site when the site is installed. The content library is placed on the drive of the site server that has the most free disk space. Because you can't install a distribution point on the central administration site, you can't prioritize the drives for use by the content library. Similar to the content library on other site servers and on distribution points, when the drive that contains the content library runs out of available disk space, the content library automatically spans to the next available drive.  

Configuration Manager uses the content library on the central administration site in the following scenarios:  

- You create content on the central administration site  

- You migrate content from another Configuration Manager site, and assign the central administration site as the site that manages that content  

> [!NOTE]  
>  When you create content at a primary site and then distribute it to a different primary site or a secondary site below a different primary site, the central administration site temporarily stores that content in the scheduler inbox on the central administration site but doesn't add that content to its content library.  

Use the following options to manage the content library on the central administration site:  

- To prevent the content library from being installed on a specific drive, create an empty file named **no_sms_on_drive.sms**. Copy it to the root of the drive before the content library is created.  

- After the content library has been created, use the **Content Library Transfer** tool from the Configuration Manager Toolkit to manage the location of the content library. Starting in version 1806, the toolkit is now available on the site server. For more information, see [Configuration Manager Toolkit](/sccm/core/support/toolkit). Otherwise, download the toolkit from the [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkId=279566).  



## <a name="bkmk_remote"></a> Configure a remote content library for the site server  
<!--1357525-->
Starting in version 1806, to free up hard drive space on your central administration or primary site servers, relocate the content library to another storage location. Move the content library to another drive on the site server, a separate server, or fault-tolerant disks in a storage area network (SAN). A SAN is recommended, because it's highly available, and provides elastic storage that grows or shrinks over time to meet your changing content requirements. For more information, see [High availability options](/sccm/protect/understand/high-availability-options).

A remote content library is a prerequisite for [site server high availability](/sccm/core/servers/deploy/configure/site-server-high-availability). 

> [!Note]  
> This action only moves the content library on the site server. It doesn't impact the location of the content library on distribution points. 


### Prerequisites  
The site server computer account needs **read** and **write** permissions to the network path to which you're moving the content library. No components are installed on the remote system. 


### Process to manage the content library
1. In the Configuration Manager console, switch to the **Administration** workspace. Expand **Site Configuration** and select **Sites**. On the **Summary** tab at the bottom of the details pane, notice a new column for the **Content Library**.  

2. Click **Manage content library** on the ribbon.  

3. Select **On a network share** and enter a valid network path. This path is the location to which the site moves the content library. Click **OK**.  

4. Note the **Status** property in the Content Library column on the details pane. It updates to show the site's progress in moving the content library. When in progress it displays the percentage complete. If there's an error state, it displays the error. Common errors include `access denied` or `disk full`. When complete it displays `OK`. See the **distmgr.log** for details. For more information, see [Site server and site system server logs](/sccm/core/plan-design/hierarchy/log-files#BKMK_SiteSiteServerLog).  

For more information on this process, see [Flowchart - Manage content library](/sccm/core/plan-design/hierarchy/manage-content-library-flowchart).

The site actually *copies* the content library files to the remote location. This process doesn't delete the content library files at the original location on the site server. To free up space, an administrator must manually delete these original files.

If you need to move the content library back to the site server, repeat this process but select the option **Local to the site server**. When the original content still exists, the process quickly moves the configuration to the location local to the site server. 

> [!Tip]  
> To move the content to another drive on the site server, use the **Content Library Transfer** tool. For more information, see [Configuration Manager Toolkit](/sccm/core/support/toolkit).  

