---
title: Wake On LAN views
titleSuffix: Configuration Manager
description: Information about the objects that have Wake On LAN enabled.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual


ms.assetid: c31b2528-de90-4a60-8a99-75990b9ad0ea
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
---

# Wake On LAN views in Configuration Manager

The Configuration�Manager Wake On LAN views contain information about the objects, such as application management, software updates, and task sequence deployments, that have Wake On LAN enabled, as well as the clients that are Wake On LAN enabled, and clients that have deployments that are Wake On LAN enabled. There is also a status view that contains information about the Wake On LAN error messages that have been reported. Most often, the Wake On LAN views will be joined to discovery views by using the **ResourceID** column, and to application management and compliance settings views by using the **ObjectID** column.

The following sections provide detailed information about Wake On LAN views and the Wake On LAN status view.

## Wake On LAN views

The Wake On LAN views are described in this section.

### v_WOLClientTimeZones

Lists the time zone offsets for all Wake On LAN�enabled clients.
It is unlikely that this view will be joined with other views.

### v_WOLCommunicationHistory

Lists the Wake On LAN communication history, including the message description, time of the communication, status message attribute, and so on. The **BatchID**, **ObjectType**, and **ID** columns contain status message attributes, such as a deployment ID or unique configuration item ID.
The view can be joined to other views by using the **BatchID**, **ObjectType**, and **ID** columns.

### v_WOLEnabledAdvertisements

Lists the software deployments, by name and advertisement ID that have Wake On LAN enabled. The **ObjectType** value for software deployment is **1**, the **ObjectName** column contains the name of the advertisement, and the **ObjectID** column contains the advertisement ID of the advertisement.
The view can be joined to other views by using the **ObjectID** column.

### v_WOLEnabledAssignments

Lists the software update deployments, by name and unique deployment ID that have Wake On LAN enabled. The **ObjectType** value for software updates is 2, the **ObjectName** column contains the name of the deployment, and the **ObjectID** column contains the unique assignment ID of the deployment.
The view can be joined to other views by using the **ObjectID** column.

### v_WOLEnabledObjects

Lists the objects, by name and object ID, that have Wake On LAN enabled, as well as the object type. For example, a software update deployment that has Wake On LAN enabled will be listed with an **ObjectType=2**, the deployment name will be listed in the **ObjectName** column, and the assignment unique ID will be listed in the **ObjectID** column.
The view can be joined to other views by using the **ObjectID** column and to the **v_WOLGetSupportedObjects** view by using the **ObjectType** column.

### v_WOLEnabledTaskSequences

Lists the task sequence advertisements, by object type, name and ID that have Wake On LAN enabled. The **ObjectType** value for task sequence is 3, the **ObjectName** column contains the name of the task sequence advertisement, and the **ObjectID** column contains the advertisement ID of the task sequence advertisement.
The view can be joined to other views by using the **ObjectID** column.

### v_WOLGetPendingObjectSchedules

Lists the objects, by the object ID that are scheduled for mandatory assignment, including the object type, target collection, schedule, and so on.
The view can be joined to other views by using the **Object** column, which is the same as the **ObjectID** columns in other Wake On LAN views, and to the **v_WOLGetSupportedObjects** view by using the **ObjectType** column.

### v_WOLGetSupportedObjects

Lists the Wake On LAN object types, by object type and object name. For example, object type 1 is for software distribution, object type 2 is for software updates, and object type 3 is for task sequence.
The view can be joined to other Wake On LAN views by using the **ObjectType** column.

### v_WOLGetWOLEnabledSites

Lists the sites where Wake On LAN is enabled, by site code and site server name.
It is unlikely that this view will be joined with other views.

### v_WOLSUMTargetedClients

Lists the Configuration Manager clients, by **ResourceID**, where a software deployment that has Wake On LAN enabled targets the client. The object type, object ID (unique assignment ID of the deployment), assigned site, and current time zone are also listed.
The view can be joined to other views by using the **ResourceID** and **ObjectID** columns.

### v_WOLSWDistTargetedClients

Lists the Configuration Manager clients, by **ResourceID**, where a software deployment that has Wake On LAN enabled targets the client. The object type, object ID (advertisement ID of the deployment), assigned site, and current time zone are also listed.
The view can be joined to other views by using the **ResourceID** and **ObjectID** columns.

### v_WOLTargetedClients

Lists the Configuration Manager clients, by ResourceID, where an object that has Wake On LAN enabled targets the client, such as a software deployment, software update, or task sequence deployment. The object type, object ID, assigned site, and current time zone are also listed.
The view can be joined to other views by using the **ResourceID** and **ObjectID** columns, and to the **v_WOLGetSupportedObjects** view by using the **ObjectType** column.

### v_WOLTSTargetedClients

Lists the Configuration Manager clients, by **ResourceID**, where a task sequence deployment that has Wake On LAN enabled targets the client. The object type, object ID (advertisement ID of the task sequence deployment), assigned site, and current time zone are also listed.
The view can be joined to other views by using the **ResourceID** and **ObjectID** columns.

### v_WOLWorkstationInfo

Lists all Wake On LAN�enabled clients, by **ResourceID** and **MachineName**, the assigned site, and the current time zone.
The view can be joined to other views by using the **ResourceID** column.

## Wake On LAN status views

The Wake On LAN status view contains information about the Wake On LAN error messages. For more information about the status views, see [Status and Alert Views in Configuration Manager](status-alert-views-configuration-manager.md). The status view that contains Wake On LAN information is described in this section.

### v_WOLCommunicationErrorStatus

Lists the Wake On LAN error status messages that have been reported, including message description and time of the error. The **BatchID**, **ObjectType**, and **ID** columns contain status message attributes, such as an advertisement ID or unique configuration item ID.
The view can be joined to other views by using the **BatchID**, **ObjectType**, and **ID** columns.

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)
