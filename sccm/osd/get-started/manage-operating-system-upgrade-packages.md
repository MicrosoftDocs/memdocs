---
title: Manage OS upgrade packages
titleSuffix: Configuration Manager
description: Learn how to manage OS upgrade packages in Configuration Manager.
ms.date: 11/16/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Manage OS upgrade packages with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

An OS upgrade package in Configuration Manager contains the Windows setup source files to upgrade an existing OS on a computer. This article describes how to add, distribute, and service an OS upgrade package.



##  <a name="BKMK_AddOSUpgradePkgs"></a> Add an OS upgrade package  

Before you can use an OS upgrade package, first add it to your Configuration Manager site. 

1.  In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Operating System Upgrade Packages** node.  

2.  On the **Home** tab of the ribbon, in the **Create** group, select **Add Operating System Upgrade Package**. This action starts the Add Operating System Upgrade Wizard.  

3.  On the **Data Source** page, specify the following settings: 

    - The network **Path** to the installation source files of the OS upgrade package. For example, `\\server\share\path`.  

        > [!NOTE]  
        >  The installation source files contain setup.exe and other files and folders to install the OS.  

        > [!IMPORTANT]  
        >  Limit access to these installation source files to prevent unwanted tampering.  

    - If you want to pre-cache content on a client, specify the **Architecture** and **Language** of the image. For more information, see [Configure pre-cache content](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

4.  On the **General** page, specify the following information. This information is useful for identification purposes when you have more than one OS upgrade package.  

    -   **Name**: A unique name for the OS upgrade package.  

    -   **Version**: An optional version identifier. This property doesn't need to be the OS version of the upgrade package. It's often your organization's version for the package.  

    -   **Comment**: An optional brief description.  

5.  Complete the wizard.  


Next, distribute the OS upgrade package to distribution points.  



##  <a name="BKMK_Distribute"></a> Distribute content to a distribution point  

Distribute OS upgrade packages to distribution points the same as other content. Before you deploy the task sequence, distribute the OS upgrade package to at least one distribution point. For more information, see [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  



[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]



## Next steps

[Create a task sequence to upgrade an OS](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)