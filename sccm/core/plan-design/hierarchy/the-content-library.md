---
title: The content library
titleSuffix: Configuration Manager
description: Learn about the content library that Configuration Manager uses to reduce the overall size of distributed content.
ms.date: 07/30/2018
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
>  To move the content library to a different location on a distribution point after the installation, use the **Content Library Transfer** tool in the Configuration Manager tools. For more information, see the [Content Library Transfer tool](/sccm/core/support/content-library-transfer).  



## About the content library on the central administration site  
By default, Configuration Manager creates a content library on the central administration site when the site is installed. The content library is placed on the drive of the site server that has the most free disk space. Because you can't install a distribution point on the central administration site, you can't prioritize the drives for use by the content library. Similar to the content library on other site servers and on distribution points, when the drive that contains the content library runs out of available disk space, the content library automatically spans to the next available drive.  

Configuration Manager uses the content library on the central administration site in the following scenarios:  

- You create content on the central administration site  

- You migrate content from another Configuration Manager site, and assign the central administration site as the site that manages that content  

> [!NOTE]  
>  When you create content at a primary site and then distribute it to a different primary site or a secondary site below a different primary site, the central administration site temporarily stores that content in the scheduler inbox on the central administration site but doesn't add that content to its content library.  

Use the following options to manage the content library on the central administration site:  

- To prevent the content library from being installed on a specific drive, create an empty file named **no_sms_on_drive.sms**. Copy it to the root of the drive before the content library is created.  

- After the content library has been created, use the **Content Library Transfer** tool from the Configuration Manager tools to manage the location of the content library. For more information, see the [Content Library Transfer tool](/sccm/core/support/content-library-transfer).  

> [!Note]  
> Cloud distribution points don't use single-instance storage. The site encrypts packages before sending to Azure, and each package has a unique encrypted key. Even if two files were identical, the encrypted versions wouldn't be the same.  



## <a name="bkmk_remote"></a> Configure a remote content library for the site server  
<!--1357525-->
Starting in version 1806, to configure [site server high availability](/sccm/core/servers/deploy/configure/site-server-high-availability) or to free up hard drive space on your central administration or primary site servers, relocate the content library to another storage location. Move the content library to another drive on the site server, a separate server, or fault-tolerant disks in a storage area network (SAN). A SAN is recommended, because it's highly available, and provides elastic storage that grows or shrinks over time to meet your changing content requirements. For more information, see [High availability options](/sccm/protect/understand/high-availability-options).

A remote content library is a prerequisite for [site server high availability](/sccm/core/servers/deploy/configure/site-server-high-availability). 

> [!Note]  
> This action only moves the content library on the site server. It doesn't impact the location of the content library on distribution points. 

> [!Tip]  
> Also plan for managing package source content, which is external to the content library. Every software object in Configuration Manager has a package source on a network share. Consider centralizing all sources to a single share, but make sure this location is redundant and highly available. 
> 
> If you move the content library to the same storage volume as your package sources, you can't mark this volume for data deduplication. While the content library supports data deduplication, the package sources volume doesn't support it. For more information, see [Data deduplication](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmmk_datadedup).<!--SCCMDOcs issue #831-->  


### Prerequisites  

- The site server computer account needs **read** and **write** permissions to the network path to which you're moving the content library. No components are installed on the remote system.  

- The site server can't have the distribution point role. The distribution point also uses the content library, and this role doesn't support a remote content library. After moving the content library, you can't add the distribution point role to the site server.  

> [!Important]  
> Don't reuse a shared network location between multiple sites. For example, don't use the same path for both a central administration site and a child primary site. This configuration has the potential to corrupt the content library, and require you to rebuild it.<!--SCCMDocs-pr issue 2764-->  


### Process to manage the content library

1. Create a folder in a network share as the target for the content library. For example, `\\server\share\folder`.  

2. In the Configuration Manager console, switch to the **Administration** workspace. Expand **Site Configuration**, select the **Sites** node, and select the site. On the **Summary** tab at the bottom of the details pane, notice a new column for the **Content Library**.  

3. Click **Manage Content Library** on the ribbon.   

4. In the Manage Content Library window, the **Current Location** field shows the local drive and path. Enter a valid network path for the **New Location**. This path is the location to which the site moves the content library. It must include a folder name that already exists on the share, for example, `\\server\share\folder`. Click **OK**.  

5. Note the **Status** value in the Content Library column on the Summary tab of the details pane. It updates to show the site's progress in moving the content library.  

    - While **In progress**, the **Move Progress (%)** value displays the percentage complete.  

    - If there's an error state, the status displays the error. Common errors include **access denied** or **disk full**.  

    - When complete it displays **Complete**.  
    
    See the **distmgr.log** for details. For more information, see [Site server and site system server logs](/sccm/core/plan-design/hierarchy/log-files#BKMK_SiteSiteServerLog).  

For more information on this process, see [Flowchart - Manage content library](/sccm/core/plan-design/hierarchy/manage-content-library-flowchart).

The site actually *copies* the content library files to the remote location. This process doesn't delete the content library files at the original location on the site server. To free up space, an administrator must manually delete these original files.

If you need to move the content library back to the site server, repeat this process, but enter a local drive and path for the **New Location**. It must include a folder name that already exists on the drive, for example, `D:\SCCMContentLib`. When the original content still exists, the process quickly moves the configuration to the location local to the site server. 

> [!Tip]  
> To move the content to another drive on the site server, use the **Content Library Transfer** tool. For more information, see the [Content Library Transfer tool](/sccm/core/support/content-library-transfer).  



## Inside the content library

> [!Warning]  
> The following section is provided for informational purposes only. Don't alter, add, or remove any files or folders in the content library. Doing so could corrupt packages, contents, or the content library as a whole. If you suspect any missing, corrupt, or otherwise invalid data, use the validation feature in the Configuration Manager console to detect such issues. Then redistribute the affected content to correct the issues. 

By default, the content library is stored on the root of a drive in a folder called **SCCMContentLib**. This folder is shared by default as **SCCMContentLib$**. The folder and share have restricted permissions to prevent accidental damage. All changes should be made from the Configuration Manager console. Within this folder are the following objects:  

- The package library (**PkgLib** folder): Information about what packages are present on the distribution point.  

- The data library (**DataLib** folder): Information about the original structure of the packages.  

- The file library (**FileLib** folder): The original files in the package. This folder is typically what uses the bulk of the storage.  

![Diagram overview of Configuration Manager content library](media/content-library-overview.png)

> [!Tip]  
> Use the **Content Library Explorer** tool from the Configuration Manager tools to browse the contents of the content library. You can't use this tool to modify the contents. It provides insight into what's present, as well as allowing validation and redistribution. For more information, see the [Content Library Explorer](/sccm/core/support/content-library-explorer).  


### Package library
The package library folder, **PkgLib**, includes one file for each package distributed to the distribution point. The file name is the package ID, for example, `ABC00001.INI`. In this file under the `[Packages]` section is a list of content IDs that are part of the package, as well as other information such as the version. For example, **ABC00001** is a legacy package at version **1**. The content ID in this file is `ABC00001.1`.


### Data library
The data library folder, **DataLib**, includes one file and one folder for each of the contents in each package. For example, this file and folder are named `ABC00001.1.INI` and `ABC00001.1`, respectively. The file includes information for validation. The folder recreates the folder structure from the original package. 

The files in the data library are replaced by INI files with the name of the original file in the package. For example, `MyFile.exe.INI`. These files include information about the original file, such as the size, time modified, and the hash. Use the first four characters of the hash to locate the original file in the file library. For example, the hash in MyFile.exe.INI is **DEF98765**, and the first four characters are **DEF9**.


### File library
If the content library spans across multiple drives, the package files could be in the file library folder, **FileLib**, on any of these drives.

Locate a specific file using the first four characters from the hash found in the data library. Inside the file library folder are many folders, each with a four-character name. Find the folder that matches the first four characters from the hash. Once you find this folder, it includes one or more sets of three files. These files share the same name, but one has the extension INI, one has the extension SIG, and one has no file extension. The original file is the one with no extension whose name is equal to the hash from the data library.

For example, folder **DEF9** includes `DEF98765.INI`, `DEF98765.SIG`, and `DEF98765`. `DEF98765` is the original `MyFile.exe`. The INI file includes a list of "users" or content IDs that share the same file. The site doesn't remove a file unless all of these contents are also removed.


### Drive spanning

The content library can be spanned across multiple drives. You choose these drives when creating the distribution point. By default, Configuration Manager automatically chooses the drives when spanning the content library.

When you choose the drives, select a primary and secondary drive. The site stores all metadata on the primary drive. It only spans the file library across to the secondary drive. The folder's share name for secondary drives includes the drive letter. For example, if D: and E: are secondary drives for the content library, the share names are **SCCMContentLibD$** and **SCCMContentLibE$**.

If you chose the **Automatic** option, Configuration Manager selects the drive with the most available free space as its primary drive. It stores all of the metadata on this drive. The site only spans the file library across to secondary drives. 

You specify a reserve space amount during configuration. Configuration Manager attempts to use a secondary disk once the best available disk has only this reserve space amount left free. Each time a new drive is selected for use, the drive with the most available free space is selected.

You can't specify that a distribution point should use all drives except for a specific set. Prevent this behavior by creating an empty file on the root of the drive, called `NO_SMS_ON_DRIVE.SMS`. Place this file before Configuration Manager selects the drive for use. If Configuration Manager detects this file on the root of the drive, it doesn't use the drive for the content library. 



## Troubleshooting

The following tips may help you troubleshoot issues with the content library:  

- Review the logs on the site server (**distmgr.log** and **PkgXferMgr.log**) and the distribution point (**smsdpprov.log**) for any pointers to the failures.  

- Use the [Content Library Explorer](/sccm/core/support/content-library-explorer) tool.  

- Check for file locks by other processes, such as antivirus software. Exclude the content library on all drives from automatic antivirus scans, as well as the temporary staging directory, **SMS_DP$**, on each drive.  

- To see if there are any hash mismatches, validate the package from the Configuration Manager console.  

- As a last option, redistribute the content. This action should resolve most issues.  

