---
title: "Update Registration Tool"
titleSuffix: "Configuration Manager"
description: "Find out when and how to use the update registration tool to manually import an update to the Configuration Manager console."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
caps.latest.revision: 8
author: Brendunsms.author: brendunsmanager: angrobe

---
# Use the Update Registration Tool to import hotfixes to System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Some updates for Configuration Manager are not available from the Microsoft cloud service and are only obtained out-of-band. An example is a limited release hotfix to address a specific issue.   
When you must install an out-of-band release, and the update or hotfix file name ends with the extension **update.exe**, you use the **update registration tool** to manually import the update to the Configuration Manager console. The tool enables you to extract and transfer the update package to the site server, and register the update with the Configuration Manager console.  

 If the hotfix file has the **.exe** file extension (not **update.exe**), see [Use the Hotfix Installer to install updates for System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  

> [!NOTE]  
>  This topic provides general guidance about how to install hotfixes that update System Center Configuration Manager. For details about a specific hotfix or update, refer to its corresponding Knowledge Base (KB) article at Microsoft Support.  

 **Prerequisites for using the update registration tool:**  

-   Only out-of-band updates that end with the **.update.exe** extension can be installed using this tool  

-   The tool is self-contained with the individual updates you get directly from Microsoft  

-   The tool does not have a dependency on the mode of the service connection point  

-   The tool must be run on the computer that hosts the service connection point  

-   The computer where the tool runs (the service connection point computer) must have the .NET Framework 4.52 installed  

-   The account you use to run the tool must have **local administrator** permissions on the computer that hosts the service connection point (where the tool is run)  

-   The account you use to run the tool must have **write** permissions to the following folder on the computer that hosts the service connection point:  **&lt;ConfigMgr Installation directory\>\EasySetupPayload\offline**  

### To use the update registration tool  

1.  On the computer that hosts the service connection point:  

    -   Open a command prompt with administrative privileges, and then change directories to the location that contains **&lt;Product\>-&lt;product version\>-&lt;KB article ID\>-ConfigMgr.Update.exe**  

2.  Run the following command to start the update registration tool:  

    -   **&lt;Product\>-&lt;product version\>-&lt;KB article ID\>-ConfigMgr.Update.exe**  

    After the hotfix is registered, it appears as a new update in the console within 24 hours.  You can accelerate the process:

    - Open  the Configuration Manager console and go to  to **Administration** > **Updates and Servicing**, and then click **Check for Updates**. (Prior to version 1702, Updates and Servicing was under **Administration** > **Cloud Services**.) 

    The update registration tool logs its actions to a .log file on the local computer. The log file has the same name as the hotfix .exe file and is written to the **%SystemRoot%/Temp** folder.  

     After the update is registered, you can close the update registration tool.  

3.  Open the Configuration Manager console and navigate to **Administration** > **Updates and Servicing**. Hotfixes that were imported are now available to install. (Prior to version 1702, Updates and Servicing was under **Administration** > **Cloud Services**.)

 For information about installing updates, see [Install in-console updates for System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  
