---
title: Import and export applications
titleSuffix: Configuration Manager
description: Learn how to import and export applications in Configuration Manager to share between separate hierarchies.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Import and export applications

*Applies to: Configuration Manager (current branch)*

Use Configuration Manager to import and export applications between two hierarchies. For example, copy an application from a test environment to a production environment.

## Export

1. In the Configuration Manager console, select the **Applications** node. In the Create group of the ribbon, choose **Export Application**.
1. On the **General** screen, enter a path to a new ZIP file to export into. Optionally, specify whether to export *dependencies, supersedence relationships, conditions, and virtual environments*, as well as *content for the selected applications and dependencies*.  Enter any administrator comments, if desired, and select **Next**.
1. Verify the application and any dependencies are listed on the **Related Objects** page and select **Next**.
1. On the Summary page, select **Next**.
1. Once the process completes, it creates the ZIP file, and you can close the wizard.

> [!IMPORTANT]
> If you're going to copy this application to another environment, take both the ZIP file and the folder that accompanies it. The ZIP file must exist in the same directory as the created folder.

## Import

> [!NOTE]
> You can only import applications from UNC paths, you can't directly import from your local disk.

1. In the Configuration Manager console, select the **Applications** node. In the Create group of the ribbon, choose **Import Application**.
1. Choose the ZIP file that you'd like to import and select **Next**.
1. The File Content window shows what happens when you import the application. Select **Next**.
1. Review the summary screen and select **Next**.
1. Close the wizard. The application is now available in the site.

## See also
 
Automate the import and export of applications using PowerShell.

* [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication)
* [Export-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmapplication)
