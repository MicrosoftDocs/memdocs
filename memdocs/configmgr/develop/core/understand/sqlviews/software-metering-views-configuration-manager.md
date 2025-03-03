---
title: Software metering views
titleSuffix: Configuration Manager
description: Information such as the software metering rules that are created in the Configuration Manager hierarchy.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference


ms.assetid: e88c5f27-7ce1-48b3-bf3d-e4e6f5100b19
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Software metering views in Configuration Manager

The software metering views contain information such as the software metering rules that are created in the Configuration Manager hierarchy, which files to meter, the products in which the files belong, the users that have used the metered files, and more. Several of the status and status summarizer views also provide information about file usage. Most often, the software metering views can be joined to other views by using the **FileID** and **ResourceID** columns.

The following sections provide detailed information about software metering views and software metering status views.

## Software metering views

The software metering views are described in this section.

### v_GS_SoftwareUsageData

Lists the Configuration Manager client computers, by resource ID, that have used metered files. The view contains the start time, end time, user name, file ID, file name, file description, file version, file size, product name, product version, and more.
The view can be joined to other views by using the **ResourceID**, **FileID**, and **UserName** columns.

### v_MeterData

Lists all software metering data, including the meter data ID, time span for the data, file ID, resource ID, user ID, and more.
The view can be joined to other views by using the **FileID**, **ResourceID**, and **MeteredUserID** columns.

### v_MeteredFiles

Lists all files that are configured in the software metering rules and metered on clients. The view contains the software metering rule ID, security key, product name, site code, file name, file version, metered file ID, metered product ID, and more.
The view can be joined to other views by using the **RuleID**, **SecurityKey**, **MeteredProductID**, and **MeteredFileID** columns.

### v_MeteredProductRule

Lists all software metering rules that have been configured in the Configuration Manager site hierarchy. The view contains the software metering rule ID, security key, product name, file name, file version, site code, and more.
The view can be joined to other views by using the **RuleID** and **SecurityKey** columns.

### v_MeteredUser

Lists all users who have used metered files. The view contains the metered user ID, full user name (domain\user name), domain, and user name.
The view can be joined to other views by using the **MeteredUserID** and **FullName** columns.

### v_MeterRuleInstallBase

Lists all metered files for system resources that match files by FileID that are also in software inventory. The view contains the rule ID, product name, metered file ID, and resource ID.
The view can be joined to other views by using the **RuleID**, **MeteredFileID**, and **ResourceID** columns.

## Software metering status views

The software metering status views contain status summary information about the file usage for metered files. For more information about the status views, see [Status and Alert Views in Configuration Manager](status-alert-views-configuration-manager.md). The status views that contain software metering information are described in this section.

### v_FileUsageSummary

Lists software metering summary status information for file usage by site.
The view can be joined to other views by using the **FileID** column.

### v_FileUsageSummaryIntervals

Lists software metering summary interval information for file usage.
It is unlikely that this view will be joined to other views.

### v_MonthlyUsageSummary

Lists the Configuration Manager client computers, by resource ID, and the usage summary for metered files, as well as the logged-on user name, usage time, and time of last usage.
The view can be joined to other views by using the **ResourceID**, **FileID**, and **MeteredUserID** columns.

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)
