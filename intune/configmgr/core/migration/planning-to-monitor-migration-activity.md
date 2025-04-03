---
title: Monitor migration
titleSuffix: Configuration Manager
description: Learn how to use the Configuration Manager console to monitor the progress and success of migration jobs.
ms.date: 10/06/2016
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: upgrade-and-migration-article
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Planning to monitor migration activity in Configuration Manager

*Applies to: Configuration Manager (current branch)*

With Configuration Manager, you can monitor migration in the Configuration Manager console that connects to the destination hierarchy. In the Configuration Manager console in the **Administration** workspace, you can use the **Migration** node to monitor the progress and success of migration jobs. You can view summary information for each migration job that identifies objects that have migrated, those objects that have not yet migrated, and the number of objects that are excluded from a migration job. You will also see details about any migration problems.  

## View Migration Progress  
 To view the progress of a migration job, use any of the following actions:  

-   In the **Administration** workspace of the Configuration Manager console, expand the **Migration Jobs** node, select a migration job, and then select the **Objects in Job** tab.  

-   Use the Configuration Manager log files to review the migration progress or to identify any problems. Migration Manager is the Configuration Manager process that tracks migration actions and records these in the migmctrl.log file in the **\&lt;InstallationPath\>\\LOGS** folder on the site server.  

    > [!NOTE]  
    >  If a migration job fails, review the details in the migmctrl.log file as soon as possible. The migration log entries are continually added to the file and overwrite old details. If the entries are overwritten, you might not be able to identify whether any problems that you might encounter with the migrated objects relate to migration issues. Migration activity is logged at the top\-level site of the hierarchy regardless of the site your Configuration Manager console connects to when you configure migration.  

-   Use Configuration Manager reporting. Configuration Manager provides several built\-in reports for migration, or you can edit those reports to fit your requirements. For more information about Configuration Manager reports, see [Introduction to reporting](../servers/manage/introduction-to-reporting.md).  
