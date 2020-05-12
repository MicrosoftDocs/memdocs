---
title: Manage OS upgrade packages
titleSuffix: Configuration Manager
description: Learn how to manage OS upgrade packages in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Manage OS upgrade packages with Configuration Manager

*Applies to: Configuration Manager (current branch)*

An OS upgrade package in Configuration Manager contains the Windows setup source files to upgrade an existing OS on a computer. This article describes how to add, distribute, and service an OS upgrade package.

> [!NOTE]
> OS upgrade packages can also be used for new installations of Windows. However it is dependent on drivers being compatible with this method. When performing new installations of Windows from an OS upgrade package, drivers are installed while still in Windows PE versus simply being injected while in Windows PE. Some drivers are not compatible with being installed while in Windows PE. If drivers are not compatible with being installed while in Windows PE, then use an [OS image](manage-operating-system-images.md), such as **install.wim**, instead.

## <a name="BKMK_AddOSUpgradePkgs"></a> Add an OS upgrade package  

Before you can use an OS upgrade package, first add it to your Configuration Manager site.

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Operating System Upgrade Packages** node.  

2. On the **Home** tab of the ribbon, in the **Create** group, select **Add Operating System Upgrade Package**. This action starts the Add Operating System Upgrade Wizard.  

3. On the **Data Source** page, specify the following settings:

    - The network **Path** to the installation source files of the OS upgrade package. For example, `\\server\share\path`.  

        > [!NOTE]  
        >  The installation source files contain setup.exe and other files and folders to install the OS.  

        > [!IMPORTANT]  
        >  Limit access to these installation source files to prevent unwanted tampering.  

    - **Extract a specific image index from install.wim file of selected upgrade package** and then select an image index from the list.<!--4931110--> Starting in version 1910, this option automatically imports a single index rather than all image indexes in the file. Using this option results in a smaller image file, and faster offline servicing. It also supports the process to [Optimize image servicing](#bkmk_resetbase), for a smaller image file after applying software updates.  

        > [!IMPORTANT]  
        > Configuration Manager overwrites the existing install.wim in the OS upgrade package. It extracts the image index to a temporary location, and then moves it into the original source directory. Before you import an OS upgrade package and enable this option, make sure to backup the original source files.

    - If you want to pre-cache content on a client, specify the **Architecture** and **Language** of the image. For more information, see [Configure pre-cache content](../deploy-use/configure-precache-content.md).  

4. On the **General** page, specify the following information. This information is useful for identification purposes when you have more than one OS upgrade package.  

    - **Name**: A unique name for the OS upgrade package.  

    - **Version**: An optional version identifier. This property doesn't need to be the OS version of the upgrade package. It's often your organization's version for the package.  

    - **Comment**: An optional brief description.  

5. Complete the wizard.  

Next, distribute the OS upgrade package to distribution points.  

## <a name="BKMK_Distribute"></a> Distribute content to a distribution point  

Distribute OS upgrade packages to distribution points the same as other content. Before you deploy the task sequence, distribute the OS upgrade package to at least one distribution point. For more information, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]

## Next steps

[Create a task sequence to upgrade an OS](../deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
