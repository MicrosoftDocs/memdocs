---
title: Sample queries for status and alerts
titleSuffix: Configuration Manager
description: Sample queries that show how to join some of the most commonly used status message views to other views.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual


ms.assetid: 61c9b4be-4656-413a-8fb1-c6e72d89fbaa
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
---

# Sample queries for status and alerts in Configuration Manager

The following sample queries demonstrate how to join some of the most commonly used status message views to other views.

## Joining the status message and status message attribute views

The following query lists status messages, by status message ID, the component that created the status message, the count of the status message reported by the component, the attribute value, and the computer name where the component is installed. The attribute value could be a package ID for a package status message, a collection ID for a collection status message, a user name for a status message concerning a user, and so forth. The **v_StatusMessage** view is joined to the **v_StatMsgAttributes** view by using the **RecordID** column.

```sql
    SELECT SM.Component, SM.MessageID, 
    ��COUNT(*) AS 'Count', SMA.AttributeValue, SM.MachineName 
    FROM v_StatusMessage SM LEFT OUTER JOIN v_StatMsgAttributes SMA 
    ��ON SM.RecordID = SMA.RecordID 
    GROUP BY SM.Component, SM.MessageID, SM.MachineName, SMA.AttributeValue 
    ORDER BY SM.Component, SM.MessageID 
```

## Joining the distribution point status and package views

The following query lists the distribution points that have been selected for each package and the installation status for the distribution point. The **v_PackageStatusDistPointSumm** view is joined to the **v_Package** view by using the **PackageID** column.

```sql
    SELECT DPS.PackageID, PCK.Name, PCK.SourceSite, 
    ��DPS.ServerNALPath, DPS.InstallStatus 
    FROM v_PackageStatusDistPointsSumm DPS INNER JOIN v_Package PCK 
    ��ON DPS.PackageID = PCK.PackageID 
    ORDER BY DPS.PackageID 
```

## Joining the deployment status, deployment, collection, and resource views

The following query lists the clients that have been targeted for a deployment, the deployment ID, the deployment name, the collection that was targeted in which the client is a member, and the last status message received from the client for the deployment. The **v_ClientAdvertisementStatus** view is joined to the **v_R_System** view by using the **ResourceID** column and the **v_Advertisement** view by using the **AdvertisementID** column. The **v_Advertisement** view is joined to the **v_Collection** view by using the **CollectionID** column. The results are sorted by NetBIOS name and then by advertisement ID.

```sql
    SELECT SYS.Netbios_Name0, ADV.AdvertisementID, ADV.AdvertisementName, 
    ��COL.Name AS TargetedCollection, CAS.LastStatusMessageIDName 
    FROM v_ClientAdvertisementStatus CAS INNER JOIN v_R_System SYS 
    ��ON CAS.ResourceID = SYS.ResourceID INNER JOIN v_Advertisement ADV 
    ��ON CAS.AdvertisementID = ADV.AdvertisementID INNER JOIN 
    ��v_Collection COL ON ADV.CollectionID = COL.CollectionID 
    ORDER BY SYS.Netbios_Name0, ADV.AdvertisementID
```

## Joining the software metering status, software inventory, and resource views

The following query lists the software metering usage data for files defined in the software metering rules. The NetBIOS name of the client, file name, file path, how many times the file has run on the computer, and last usage date are retrieved. The results are sorted by NetBIOS name, and then file name, and then file path. The **v_MonthlyUsageSummary** view is joined to the **v_R_System** view by using the **ResourceID** column and to the **v_GS_SoftwareFile** view by using the **FileID** column.

```sql
    SELECT SYS.Netbios_Name0, SF.FileName, SF.FilePath, 
    ��MUS.UsageCount, MUS.LastUsage 
    FROM v_MonthlyUsageSummary MUS INNER JOIN v_R_System SYS 
    ��ON MUS.ResourceID = SYS.ResourceID INNER JOIN v_GS_SoftwareFile SF 
    ��ON MUS.FileID = SF.FileID 
    ORDER BY SYS.Netbios_Name0, SF.FileName, SF.FilePath 
```

## Joining the software updates status and discovery views

The following query lists the enforcement state reported by the VISTACLIENT1 client computer for all software updates that have been assigned to the client. The article ID, bulletin ID, and title for the software update are listed, as well as the enforcement state, the date for the last enforcement scan on the client, and the date when the last enforcement state message was sent from the client. The results are filtered by a topic type of 402, which is the topic type for enforcement state messages, and for the VISTACLIENT1 client. The results are also sorted by state name, and then by the date the software update was last modified. The **v_UpdateComplianceStatus** status view is joined to the **v_R_System** discovery view by using the **ResourceID** column. The **v_UpdateComplianceStatus** view is joined to the **v_UpdateInfo** software updates view by using the **CI_ID** column. The **v_UpdateComplianceStatus** view is joined to the **v_StateNames** status view by using the **LastEnforcementMessageID** and **StateID** columns, respectively.

```sql
    SELECT v_UpdateInfo.ArticleID, v_UpdateInfo.BulletinID, v_UpdateInfo.Title, 
    ��v_StateNames.StateName, v_UpdateComplianceStatus.LastStatusCheckTime, 
    ��v_UpdateComplianceStatus.LastEnforcementMessageTime 
    FROM v_R_System INNER JOIN v_UpdateComplianceStatus ON 
    ��v_R_System.ResourceID = v_UpdateComplianceStatus.ResourceID INNER JOIN v_UpdateInfo ON 
    ��v_UpdateComplianceStatus.CI_ID = v_UpdateInfo.CI_ID INNER JOIN v_StateNames ON 
    ��v_UpdateComplianceStatus.LastEnforcementMessageID = v_StateNames.StateID 
    WHERE (v_StateNames.TopicType = 402) AND (v_R_System.Netbios_Name0 LIKE 'VISTACLIENT1') 
    ORDER BY v_StateNames.StateName, v_UpdateInfo.DateLastModified 
```

## See also

[Status and alert views in Configuration Manager](status-alert-views-configuration-manager.md)
