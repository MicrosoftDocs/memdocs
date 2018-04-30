---
title: "Create App-V virtual environments"
titleSuffix: "Configuration Manager"
description: "Create virtual environments with Microsoft Application Virtualization so apps can share data with each other."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Create App-V virtual environments in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

In a Microsoft Application Virtualization (App-V) virtual environment in System Center Configuration Manager (Configuration Manager), deployed virtual applications can share the same file system and registry on client Windows PCs. Unlike standard virtual applications, these applications can share data with each other. Virtual environments are created or modified on client PCs when the application is installed or when clients next evaluate their installed applications. You can order these applications so that when multiple applications try to modify a file system or registry value, the application with the highest order takes priority.  

> [!IMPORTANT]  
>  Do not rely on App-V virtual environments to provide security protection, such as from malware.  

 Use the following procedure to create an App-V virtual environment in Configuration Manager.  

## Create an App-V virtual environment  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **App-V Virtual Environments**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Virtual Environment**.  

4.  In the **Create Virtual Environment** dialog box, enter the following information:  

    -   **Name**.  Enter a unique name for the virtual environment (maximum 128 characters).  

    -   **Description**. (Optional) Enter a description for the virtual environment.  

5.  To add a new deployment type to the virtual environment, choose **Add**. You must add at least one deployment type.  

6.  In the **Add Applications** dialog box, specify a **Group name** (maximum 128 characters). You'll use this name to refer to the group of applications that you add to the virtual environment.  

7.  Choose **Add**, select the App-V 5 applications and deployment types that you want to add to the group, and then choose **OK**.  

8.  In the **Add Applications** dialog box, you can select **Increase Order** or **Decrease Order** to set the application that takes priority if multiple applications attempt to modify file system or registry settings in the same virtual environment.  

9. To return to the **Create Virtual Environment** dialog box, choose **OK**.  

10. When you're done adding groups, choose **OK** to create the virtual environment. The new virtual environment is displayed in the **App-V Virtual Environments** node of the Configuration Manager console. You can monitor the status of your virtual environments by using the App-V Virtual Environment Status report.  

    > [!NOTE]  
    >  The virtual environment is added or modified on client PCs when the application is installed or when the client next evaluates installed applications.  
