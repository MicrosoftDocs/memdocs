---
title: Migration views
titleSuffix: Configuration Manager
description: Information about the tasks involved in migrating to a Configuration Manager site.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual


ms.assetid: 6be79f37-cc77-4ea0-8d1d-7fe8c98d601f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# Migration views in Configuration Manager

Migration views contain information about the tasks involved in migrating to a Configuration Manager site.

For more information about migration in Configuration Manager, see [Migrating hierarchies in Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).

## Migration views

The views for migration are shown in this section:

### v_MIG_SiteMapping

Lists the current migration source site. **SiteMappingID** is used to uniquely identify a migration source site.

> [!NOTE]
> If **IsDecommissioned** or **IsDeleted** has a value of true, it means this migration source site has either stopped migration data gathering or is deleted.

This view can be joined to other views by using the **SourceSiteCode** column.

### v_MIG_SiteRelation

This view is no longer used in Configuration Manager.

### v_MIG_MigratedDPs

Lists the shared distribution points from source sites. **AttachingSiteCode** is the source site code that the distribution point belongs to in the source hierarchy, and **SiteCode** is the site code of the destination site.
This view can be joined to other views by using the **NALPath** column.

### v_MIG_JobEntity

Lists the relationship between a migration job and objects for migration. This is useful for listing the objects contained in a migration job.
This view can be joined to other views by using the **JobID** column.

### v_MIG_Job

Lists the migration jobs that have been created. The **JobID** column uniquely identifies a migration job and is usually used to join with other migration job related tables or views.

### v_MIG_EntityState

Lists the state of migration objects.
This view can be joined to other views by using the **EntityID** column.

### v_MIG_EntityReference

Lists the migration object dependency relationship. This can be used to find out the dependent objects for an object.
This view can be joined to other views by using the **EntityID** column.

### v_MIG_Entities

Lists the objects available for migration in the source site.
This view can be joined to other views by using the **EntityID** column.

### v_MIG_Dashboard

Lists the overall migration status from a source site hierarchy. Migration status in the Configuration Manager console information is based on this view.

### v_MIG_Collections

Lists collection information in a source site. The **SiteID** column represents the source site ID.
This view can be joined to other views by using the **SiteID** column.

### v_MIG_ClientState

This view is no longer used in Configuration Manager.

### v_MIG_Clients

This view is no longer used in Configuration Manager.

### v_MIG_ClientGroupState

This view is no longer used in Configuration Manager.

### vSMS_MigrationSourceSite

Lists the source site information. This view is similar to **v_MIG_SiteMapping**, but only contains information about the source site.

### vSMS_MigrationCollectionInfo

This view is based on **v_MIG_Collections** and queries the list of collection information in a source site. Use this view to query collection information.

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)
