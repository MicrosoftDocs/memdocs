---
title: "Update reset tool"
description: "Use the update reset tool for in-console updates for System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
caps.latest.revision: 0
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Update reset tool

*Applies to: System Center Configuration Manager (Current Branch)*  


Beginning with version 1706, Configuration Manager primary sites, and central administration sites include the Configuration Manager Update Reset Tool, **CMUpdateReset.exe**. Use the tool to fix issues when in-console updates have problems downloading or replicating. The tool is found in the ***\cd.latest\SMSSETUP\TOOLS*** folder of the site server.

You can use this tool with any version of the current branch that remains in support.

Use this tool when an [in-console update](/sccm/core/servers/manage/install-in-console-updates) has not yet installed and is in a failed state. A failed state means that the update download is in progress but stuck or taking an excessively long time. A long time is considered to be hours longer than your historical expectations for update packages of similar size. It can also be a failure to replicate the update to child primary sites.  

When you run the tool, it runs against the update that you specify. By default, the tool does not delete successfully installed or downloaded updates.  

### Prerequisites
The account you use to run the tool requires the following permissions:
-   **Read** and **Write** permissions to the site database of the central administration site and to each primary site in your hierarchy. To set these permissions, you can add the user account as a member of the **db_datawriter** and **db_datareader** [fixed database roles](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) on the Configuration Manager database of each site. The tool does not interact with secondary sites.
-   **Local Administrator** on the top-level site of your hierarchy.
-   **Local Administrator** on the computer that hosts the service connection point.

You need the GUID of the update package that you want to reset. To get the GUID:
  1.   In the console, go to **Administration** > **Updates and Servicing**.
  2.   In the display pane, right-click the heading of one of the columns (like **State**), then select **Package Guid** to add that column to the display.
  3.   The column now shows the update package GUID.

> [!TIP]  
> To copy the GUID, select the row for the update package you want to reset, and then use CTRL+C to copy that row. If you paste your copied selection into a text editor, you can then copy only the GUID for use as a command-line parameter when you run the tool.

### Run the tool    
The tool must be run on the top-level site of the hierarchy.

When you run the tool, use command-line parameters to specify:
  -   The SQL Server at the top-tier site of the hierarchy.
  -   The site database name at the top-tier site.
  -   The GUID of the update package you want to reset.

Based on the status of the update, the tool identifies the additional servers it needs to access.   

If the update package is in a *post download* state, the tool does not clean up the package. As an option, you can force the removal of a successfully downloaded update by using the force delete parameter (See command-line parameters later in this topic).

After the tool runs:
-   If a package was deleted, restart the SMS_Executive service at the top-tier site. Then, check for updates so you can download the package again.
-   If a package was not deleted, you do not need to take any action. The update reinitializes and then restarts replication or installation.

**Command-line parameters:**  

| Parameter        |Description                 |  
|------------------|----------------------------|  
|**-S &lt;FQDN of the SQL Server of your top-tier site>** | *Required* <br> Specify the FQDN of the SQL Server that hosts the site database for the top-tier site of your hierarchy.    |  
| **-D &lt;Database name>**                        | *Required* <br> Specify the name of the database at the top-tier site.  |  
| **-P &lt;Package GUID>**                         | *Required* <br> Specify the GUID for the update package you want to reset.   |  
| **-I &lt;SQL Server instance name>**             | *Optional* <br> Identify the instance of SQL Server that hosts the site database. |
| **-FDELETE**                              | *Optional* <br> Force deletion of a successfully downloaded update package. |  
 **Examples:**  
 In a typical scenario, you want to reset an update that has download problems. Your SQL Servers FQDN is *server1.fabrikam.com*, the site database is *CM_XYZ*, and the package GUID is *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  You run: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 In a more extreme scenario, you want to force deletion of problematic update package. Your SQL Servers FQDN is *server1.fabrikam.com*, the site database is *CM_XYZ*, and the package GUID is *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  You run: ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***
