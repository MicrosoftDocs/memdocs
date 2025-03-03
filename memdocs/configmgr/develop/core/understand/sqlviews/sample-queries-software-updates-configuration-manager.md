---
title: Sample queries for software updates
titleSuffix: Configuration Manager
description: Sample queries that show how to join software updates views to each other and to views from other view categories.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to


ms.assetid: 583e373f-1619-4385-8c86-0484820c6b02
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Sample queries for software updates in Configuration Manager

The following sample queries demonstrate how to join software updates views to each other and to views from other view categories. Software updates views will most often use the **CI_ID** column when joining to other views.

## Joining software updates, discovery, and status views

The following query retrieves the article ID, bulletin ID, software update title, last enforcement state for the update, the time of the last enforcement check, and the time that the last enforcement state message was sent by the Computer1 client. The results are sorted by state name and then by the last modified date for the software update. The query joins the **v_UpdateComplianceStatus** status view with the **v_UpdateInfo** software updates view by using the **CI_ID** column, the **v_UpdateComplianceStatus** status view with the **v_R_System** discovery view by using the **ResourceID** column, and the **v_UpdateComplianceStatus** status view with the **v_StateNames** status view by using the **LastEnforcementStatus** and **StateID** columns, respectively. The retrieved information is filtered by the topic type of 402, which includes state messages for configuration item enforcement, and a computer with the NetBIOS name of Computer1.

```sql
    SELECT v_UpdateInfo.ArticleID, v_UpdateInfo.BulletinID, v_UpdateInfo.Title, 
    ��v_StateNames.StateName, v_UpdateComplianceStatus.LastStatusCheckTime, 
    ��v_UpdateComplianceStatus.LastEnforcementMessageTime 
    FROM v_R_System INNER JOIN v_UpdateComplianceStatus ON 
    ��v_R_System.ResourceID = v_UpdateComplianceStatus.ResourceID INNER JOIN v_UpdateInfo ON 
    ��v_UpdateComplianceStatus.CI_ID = v_UpdateInfo.CI_ID INNER JOIN v_StateNames ON 
    ��v_UpdateComplianceStatus.LastEnforcementMessageID = v_StateNames.StateID 
    WHERE (v_StateNames.TopicType = 402) AND (v_R_System.Netbios_Name0 LIKE 'Computer1') 
    ORDER BY v_StateNames.StateName, v_UpdateInfo.DateLastModified 
```

## Joining software updates and compliance settings views

The following query retrieves the software update deployments, by assignment ID (software update deployment ID) and assignment name (deployment name); the software updates that are contained in the deployment, by article ID, bulletin ID, and software update title; and the target collection for the deployment. The results are sorted by the assignment ID and then by article ID. The query joins the **v_UpdateInfo** software updates view with the **v_CIAssignmentToCI** compliance settings view by using the **CI_ID** column, and it joins the **v_CIAssignmentToCI** view to the **v_CIAssignment** compliance settings view by using the **AssignmentID** column.

```sql
    SELECT v_CIAssignment.AssignmentID, v_CIAssignment.AssignmentName, 
    ��v_UpdateInfo.ArticleID, v_UpdateInfo.BulletinID, v_UpdateInfo.Title, 
    ��v_CIAssignment.CollectionName, v_CIAssignment.CollectionID 
    FROM v_UpdateInfo INNER JOIN v_CIAssignmentToCI ON 
    ��v_UpdateInfo.CI_ID = v_CIAssignmentToCI.CI_ID INNER JOIN v_CIAssignment ON 
    ��v_CIAssignmentToCI.AssignmentID = v_CIAssignment.AssignmentID 
    ORDER BY v_CIAssignment.AssignmentID, v_UpdateInfo.ArticleID 
```


## See also

[Software updates views in Configuration Manager](software-updates-views-configuration-manager.md)
