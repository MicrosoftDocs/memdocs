---
title: Sample Queries for Software Updates
titleSuffix: Configuration Manager
description: Sample queries that show how to join software updates views to each other and to views from other view categories.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other #app client compliance hybrid osd protect sum
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 583e373f-1619-4385-8c86-0484820c6b02
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Sample Queries for Software Updates in Configuration Manager

The following sample queries demonstrate how to join software updates views to each other and to views from other view categories. Software updates views will most often use the **CI_ID** column when joining to other views.

## Joining Software Updates, Discovery, and Status Views

The following query retrieves the article ID, bulletin ID, software update title, last enforcement state for the update, the time of the last enforcement check, and the time that the last enforcement state message was sent by the Computer1 client. The results are sorted by state name and then by the last modified date for the software update. The query joins the **v_UpdateComplianceStatus** status view with the **v_UpdateInfo** software updates view by using the **CI_ID** column, the **v_UpdateComplianceStatus** status view with the **v_R_System** discovery view by using the **ResourceID** column, and the **v_UpdateComplianceStatus** status view with the **v_StateNames** status view by using the **LastEnforcementStatus** and **StateID** columns, respectively. The retrieved information is filtered by the topic type of 402, which includes state messages for configuration item enforcement, and a computer with the NetBIOS name of Computer1.

```sql
    SELECT v_UpdateInfo.ArticleID, v_UpdateInfo.BulletinID, v_UpdateInfo.Title, 
      v_StateNames.StateName, v_UpdateComplianceStatus.LastStatusCheckTime, 
      v_UpdateComplianceStatus.LastEnforcementMessageTime 
    FROM v_R_System INNER JOIN v_UpdateComplianceStatus ON 
      v_R_System.ResourceID = v_UpdateComplianceStatus.ResourceID INNER JOIN v_UpdateInfo ON 
      v_UpdateComplianceStatus.CI_ID = v_UpdateInfo.CI_ID INNER JOIN v_StateNames ON 
      v_UpdateComplianceStatus.LastEnforcementMessageID = v_StateNames.StateID 
    WHERE (v_StateNames.TopicType = 402) AND (v_R_System.Netbios_Name0 LIKE 'Computer1') 
    ORDER BY v_StateNames.StateName, v_UpdateInfo.DateLastModified 
```

## Joining Software Updates and Compliance Settings Views

The following query retrieves the software update deployments, by assignment ID (software update deployment ID) and assignment name (deployment name); the software updates that are contained in the deployment, by article ID, bulletin ID, and software update title; and the target collection for the deployment. The results are sorted by the assignment ID and then by article ID. The query joins the **v_UpdateInfo** software updates view with the **v_CIAssignmentToCI** compliance settings view by using the **CI_ID** column, and it joins the **v_CIAssignmentToCI** view to the **v_CIAssignment** compliance settings view by using the **AssignmentID** column.

```sql
    SELECT v_CIAssignment.AssignmentID, v_CIAssignment.AssignmentName, 
      v_UpdateInfo.ArticleID, v_UpdateInfo.BulletinID, v_UpdateInfo.Title, 
      v_CIAssignment.CollectionName, v_CIAssignment.CollectionID 
    FROM v_UpdateInfo INNER JOIN v_CIAssignmentToCI ON 
      v_UpdateInfo.CI_ID = v_CIAssignmentToCI.CI_ID INNER JOIN v_CIAssignment ON 
      v_CIAssignmentToCI.AssignmentID = v_CIAssignment.AssignmentID 
    ORDER BY v_CIAssignment.AssignmentID, v_UpdateInfo.ArticleID 
```

## Joining Software Updates, Compliance Settings, and Application Management Views

The following query retrieves the software updates that have been downloaded, by article ID, the software update title, deployment package ID, deployment package name, and the path to the package source files. The results are sorted by software update article ID. The query joins the **v_UpdateInfo** software updates view to the **v_BundledConfigurationItems** view by using the **CI_ID** column. The **v_BundledConfigurationItems** compliance settings view is joined with the **v_UpdatePrograms** software updates view by using the **BundledCI_ID** and **UpdateID** columns, respectively. The **v_UpdatePrograms** view is joined with the **v_Package** software distribution view by using the **PackageID** column. Because the **v_UpdateInfo** view contains the configuration item ID for software updates bundles or stand-alone software updates, but the **v_UpdatePrograms** view contains the configuration item ID for software updates that are part of a bundle or stand-alone software updates that have content associated with them, the **v_UpdateContents** view was needed to link the two. For example, a software update bundle might have a configuration item ID of 100, and the English version of the software update that is downloaded might have a configuration item ID of 99. The **v_UpdateInfo** view would contain configuration item ID 100 for the bundle, the **v_UpdatePrograms** view would contain configuration item ID 99 for the downloaded software update, and the **v_UpdateContents** would contain both configuration item IDs for the bundle and associated software update.

```sql
    SELECT v_UpdateInfo.ArticleID, v_UpdateInfo.Title, v_Package.PackageID, 
      v_Package.Name AS [Package Name], v_Package.PkgSourcePath 
    FROM v_UpdateInfo INNER JOIN v_UpdateContents ON 
      v_UpdateInfo.CI_ID = v_UpdateContents.CI_ID INNER JOIN v_UpdatePrograms ON 
      v_UpdateContents.ContentCI_ID = v_UpdatePrograms.UpdateID INNER JOIN v_Package ON 
      v_UpdatePrograms.PackageID = v_Package.PackageID 
    ORDER BY v_UpdateInfo.ArticleID 
```

## See Also

[Software Updates Views in Configuration Manager](software-updates-views-configuration-manager.md)