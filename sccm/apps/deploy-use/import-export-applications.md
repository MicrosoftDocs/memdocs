---

# Mandatory fields.
title: Import/Export Applications
titleSuffix: Configuration Manager
description: Import and export applications.
author: chriskibble
ms.author: NO VALUE SET # Microsoft employees only
ms.date: 5/6/2019
ms.topic: conceptual
ms.technology: configmgr-app
---
# Create applications in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager allows for the import and export of applications within the console.  This allows you to copy applications in to other environments, such as copying from a test environment into a production environment.

## <a name="bkmk_export"></a> Export an Application

1. Within the Configuration Manager console, right click on the application to export and select **Export**.
1. On the **General** screen, enter a path to a new ZIP file to export into.  Optionally define if you'd like to export *dependencies, supersedence relationships, conditions, and virtual environments* and also if you'd like to export *content for the selected applications and dependencies*.  Enter any administrator comments, if desired, and click **Next**.
1. Verify the application and any dependencies are listed on the **Related Objects** page and click **Next**.
1. On the Summary page, click **Next**.
1. Once the process is complete, the ZIP file will be created and you can click the **Close** button.

> [!IMPORTANT]
> If you're going to copy this to another environment, you'll need to take both the created ZIP file and the folder that accompanies it.  The ZIP file must exist in the same directory as the created folder.

## <a name="bkmk_import"></a> Import Export an Application

> [!NOTE]
> Applications can only be imported from UNC paths, you will not be able to import from your local disk directly.

1. Within the Configuration Manager console, right click on the application node in the left margin  **Import Application**.
1. Select the ZIP file that you'd like to import and click **Next**.
1. The File Content window will show what will happen with the application you're importing.  Click **Next**.
1. Review the summary screen and click **Next**.
1. On the Completion screen, click the **Close** button.  Your application has now been imported.

## <a name="bkmk_whatsnext"></a> What's Next
 
Automate the import and export of applications using PowerShell.

* [Import-CMApplication](https://docs.microsoft.com/en-us/powershell/module/configurationmanager/import-cmapplication)
* [Export-CMApplication](https://docs.microsoft.com/en-us/powershell/module/configurationmanager/export-cmapplication)