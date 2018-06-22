---
title: Best practices for software updates
titleSuffix: Configuration Manager
description: Use these best practices for software updates in Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/13/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
---
# Best practices for software updates in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article includes best practices for software updates in Configuration Manager. The information is sorted into best practices for initial installation and for ongoing operations.  



## <a name="bkmk_install"></a> Installation best practices  

Use the following best practices when you install software updates in Configuration Manager.  


### <a name="bkmk_shared-susdb"></a> Use a shared WSUS database for software update points  

When you install more than one software update point at a primary site, use the same WSUS database for each software update point in the same Active Directory forest. If you share the same database, it significantly mitigates, but doesn't completely eliminate, the client and the network performance impact that you might experience when clients switch to a new software update point. A delta scan still occurs when a client switches to a new software update point that shares a database with the old software update point, but the scan is much smaller than it would be if the WSUS server has its own database. For more information about software update point switching, see [Software update point switching](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  

> [!IMPORTANT]  
>  Also share the local WSUS content folders when you use a shared WSUS database for software update points.  

For more information on sharing the WSUS database, see the following blog posts:  

- [How to implement a shared SUSDB for Configuration Manager software update points](https://blogs.technet.microsoft.com/configurationmgr/2016/10/12/how-to-implement-a-shared-susdb-for-configuration-manager-software-update-points/)  

- [Considerations for multiple WSUS instances sharing a content database when using System Center Configuration Manager](https://blogs.technet.microsoft.com/wsus/2014/03/22/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb/)  


### <a name="bkmk_sql-instance"></a> When Configuration Manager and WSUS use the same SQL Server, configure one to use a named instance and the other to use the default instance  

When the Configuration Manager and WSUS databases share the same instance of SQL Server, you can't easily determine the resource usage between the two applications. Use different SQL Server instances for Configuration Manager and WSUS. This configuration makes it easier to troubleshoot and diagnose resource usage issues that might occur for each application.  


### <a name="bkmk_store-local"></a> Specify the "Store updates locally" setting  

When you install WSUS, select the setting to **Store updates locally**. This setting causes WSUS to download the license terms that are associated with software updates. It downloads the terms during the synchronization process and stores them on the local hard drive for the WSUS server. If you don't select this setting, client computers might fail compliance scans for software updates that have license terms. The **WSUS Synchronization Manager** component of the software update point verifies that this setting is enabled every 60 minutes, by default.  



## <a name="bkmk_operation"></a> Operational Best Practices  

Use the following best practices when you use software updates:  


### <a name="bkmk_object-limit"></a> Limit software updates to 1000 in a single software update deployment  

Limit the number of software updates to 1000 in each software update deployment. When you create an automatic deployment rule, verify that the specified criteria doesn't result in more than 1000 software updates. If you manually deploy software updates, don't select more than 1000 updates.  


### <a name="bkmk_new-group"></a> Create a new software update group each time an ADR runs for "Patch Tuesday" and for general deployments  

There's a limit of 1000 software updates in a deployment. When you create an automatic deployment rule (ADR), you specify whether to use an existing update group or create a new update group each time the rule runs. If you specify criteria in an ADR that results in multiple software updates, and the rule runs on a recurring schedule, create a new software update group each time the rule runs. This behavior prevents the deployment from surpassing the limit of 1000 software updates per deployment.  


### <a name="bkmk_same-group"></a> Use an existing software update group for ADRs for Endpoint Protection definition updates  

When you use an ADR to deploy Endpoint Protection definition updates on a frequent basis, always use an existing software update group. Otherwise, the ADR potentially creates hundreds of software update groups over time. Definition update publishers typically set definition updates to expire when they're superseded by four newer updates. Therefore, the software update group that's created by the ADR never contains more than four definition updates for the publisher: one active, and three superseded.  



## See Also  
 [Plan for software updates](/sccm/sum/plan-design/plan-for-software-updates)
