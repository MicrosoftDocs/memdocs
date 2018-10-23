---
title: Manage operating system upgrade packages
titleSuffix: "Configuration Manager"
description: "Learn how to manage operating system upgrade packages in System Center Configuration Manager."
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Manage operating system upgrade packages with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

An upgrade package in System Center Configuration Manager contains the Windows Setup source files that are used to upgrade an existing operating system on a computer. Use the following  sections manage operating system upgrade packages in Configuration Manager.

##  <a name="BKMK_AddOSUpgradePkgs"></a> Add operating system upgrade packages to Configuration Manager  
 Before you can use an operating system upgrade package, you must add the package to a Configuration Manager site. Use the following procedure to add an operating system upgrade package  to a site.  

#### To add an operating system upgrade package  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Operating System upgrade packages**.  

3.  On the **Home** tab, in the **Create** group, click **Add Operating System Upgrade Package** to start the Add Operating System Upgrade Wizard.  

4.  On the **Data Source** page, specify the network path to the installation source files of the operating system upgrade package. For example, specify the UNC **\\\server\path** to where the installation source files are located.  

    > [!NOTE]  
    >  The installation source files contain Setup.exe and other files and folders to install the operating system.  

    > [!IMPORTANT]  
    >  Limit access to the  installation source files to prevent unwanted tampering.  

5.  On the **General** page, specify the following information, and then click **Next**. This information is useful for identification purposes when you have multiple operating system installers.  

    -   **Name**: Specify the name of the operating system installer.  

    -   **Version**: Specify the version of the operating system installer.  

    -   **Comment**: Specify a brief description of the operating system installer.  

6.  Complete the wizard.  

 You can now distribute the operating system installer to the distribution points that are accessed by your deployment task sequences.  

##  <a name="BKMK_DistributeBootImages"></a> Distribute operating system images to a distribution point  
 Operating system images are distributed to distribution points in the same way as you distribute other content. In most cases, you must distribute the operating system image to at least one distribution point before you deploy the operating system. For the steps to distribute an operating system image, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

##  <a name="BKMK_OSUpgradePkgApplyUpdates"></a> Apply software updates to an operating system upgrade package  
 Beginning in Configuration Manager version 1602, you can apply new software updates to the operating system image in your operating system upgrade package. Before you can apply software updates to an upgrade package you must have your software updates infrastructure in place, have successfully synchronized software updates, and downloaded the software updates to the content library on the site server. For more information, see [Deploy software updates](../../sum/deploy-use/deploy-software-updates.md).  

 You can apply applicable software updates to an upgrade package on a specified schedule. On the schedule that you specify, Configuration Manager applies the software updates that you select to the operating system upgrade package, and then optionally distributes the updated upgrade package to distribution points. Information about the operating system upgrade package is stored in the site database, including the software updates that were applied at the time of the import. Software updates that have been applied to the upgrade package since it was initially added are also stored in the site database. When you start the wizard to apply software updates to the operating system upgrade package, the wizard retrieves a list of applicable software updates that have not yet been applied to the upgrade package for you to select. Configuration Manager copies the software updates from the content library on the site server and applies the software updates to the operating system upgrade package.  

 Use the following procedure to apply software updates to an operating system upgrade package.  

#### To apply software updates to an operating system upgrade package  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Operating System upgrade packages**.  

3.  Select the operating system upgrade package to which to apply software updates.  

4.  On the **Home** tab, in the **Operating System Upgrade Packages** group, click **Schedule Updates** to start the wizard.  

5.  On the **Choose Updates** page, select the software updates to apply to the operating system image, and then click **Next**.  

6.  On the **Set Schedule** page, specify the following settings, and then click **Next**.  

    1.  **Schedule**: Specify the schedule for when the software updates are applied to the operating system image.  

    2.  **Continue on error**:  Select this option to continue to apply software updates to the image even when there is an error.  

    3.  **Distribute the image to distribution points**: Select this option to update the operating system image on distribution points after the software updates are applied.  

7.  On the **Summary** page, verify the information, and then click **Next**.  

8.  On the **Completion** page, verify that the software updates were successfully applied to the operating system image.  

> [!NOTE]  
>  To minimise the payload size, the servicing of Operating System Upgrade and Operating System Install packages removes the older     version.  
