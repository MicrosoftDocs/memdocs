---
title: Content management views
titleSuffix: Configuration Manager
description: Provides the tools for you to manage content files for applications, packages, software updates, and operating system deployment.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 80e86983-2e3b-4a10-9755-5f0d98688462
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Content management views in Configuration Manager

Content management in Configuration Manager provides the tools for you to manage content files for applications, packages, software updates, and operating system deployment.

## Content management views

The content management views are described in the following table.

### v_ContentDistributionReport

Lists information about the content packages sent to each distribution point together with the status of the distribution and the current state of the distribution.
This view can be joined to other views by using the **PkgID** column.

### v_ContentDistributionMessages

Lists status returned by the content distribution process for Configuration Manager content packages, by ID. Returns the ID of the content package, recent status messages, and more.
This view can be joined to other views by using the **PkgID** column.

### v_DistributionPointInfoBase

Lists detailed information about each distribution point in the site, including the server name, the NAL path, any configured share name, whether it's Internet-facing and more.
This view can be joined to other views by using the **ServerName** column.

### v_DistributionPointMessages

List information about status messages sent by packages on each distribution point in the site. This info includes the last time that status was sent and the ID of the status message that was sent.
This view can be joined to other views by using the **ID**, **DPID**, or **PkgID** columns.

### v_DistributionPoints

Lists information about each distribution point in the Configuration Manager hierarchy, including the ID, the server name that hosts the distribution point, the site code, whether it's a pull distribution point, and more.
This view can be joined to other views by using the **DPID** column.

### v_DistributionStatus

Lists each content package and the current distribution status of the package. This includes the package ID, the ID of the distribution point, the time that status was last reported and more.
This view can be joined to other views by using the **PkgID** column.

### v_DistributionPointDriveInfo

Lists information about the location and the status of content on distribution points. This info includes the site code, NAL path, drive where the content is stored, total and free space on the drive, and more.
It's unlikely that this view will be joined to other views.

### v_DPGroupContentDetails

Lists information, by group ID about the content stored on distribution point groups. This includes the group ID, content package ID, number of packages pending install, number of packages successfully installed, and more.
This view can be joined to other views by using the **GroupID** or **PkgID** columns.

### v_DPGroupContentInfo

Lists, for each distribution point, the number of content packages installed, in progress, or failed.
This view can be joined to other views by using the **GroupID** column.

### v_DPGroupMembers

Lists, by group ID, the path to each distribution point in the group.
It's unlikely that this view will be joined to other views.

### v_DPGroupPackages

Lists, by group ID, the content packages that have been deployed to each distribution point group.
It's unlikely that this view will be joined to other views.

### v_DPStatusSummary

Lists, by NAL path, the summary status of each distribution point. This includes the number of packages distributed to the distribution point, the number of content distributions installed, in progress and failed.
This view can be joined to other views by using the **DPNalPath** column.

### v_Content

Lists, by package ID, each content package at the site, including the content ID, version, size of the source files in bytes, and more.
This view can be joined to other views by using the **PkgID** column.

### v_ContDistStatSummary

Lists, by package ID, each content package at the site, with details about which distribution points have been targeted with that content, together with the last status time, number if successful, pending and failed content distributions, and more.
This view can be joined to other views by using the **PkgID** column.

### v_ContentDistribution

Lists information about the content packages, by package ID, that have been sent to distribution points. This includes the ID of the distribution point, the current state and the date of the last status summary.
This view can be joined to other views by using the **PkgID** column.

### v_ContentDistributionHighlights

This view can be joined to other views by using the **PkgID** column.

### v_ContentDistributionReport_DP

Lists, sorted by distribution point NA: path, the current status of each distribution point. This includes the last status time, number of packages on the distribution point, number of content distributions in progress and the number of errors.
This view can be joined to other views by using the **DPNalPath** column.

### v_ContentDistributionVersions

Lists, by package ID, the package versions on each distribution point. This includes the site code, the NAL path of the distribution point, the latest source version and state, and more.
This view can be joined to other views by using the **PkgID** column.

### v_ContentInfo

This view lists information about content associated with an application or deployment. This includes the source location of the content, information about related content and more.
This view can be joined to other views by using the **Content_ID** column.

### v_SMS_DistributionPointGroup

Lists all distribution point groups in the site hierarchy by **GroupID**. Contains the name of the distribution point group, who created it and when, the number of distribution points in the group and more.
It's unlikely that this view will be joined to other views.

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)  
