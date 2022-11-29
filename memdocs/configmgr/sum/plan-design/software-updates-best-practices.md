---
title: Best practices for software updates
titleSuffix: Configuration Manager
description: Use these best practices for software updates in Configuration Manager.
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.date: 09/16/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---
# Best practices for software updates in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article includes best practices for software updates in Configuration Manager. The information is sorted into best practices for initial installation and for ongoing operations.  



## <a name="bkmk_install"></a> Installation best practices  

Use the following best practices when you install software updates in Configuration Manager.  


### <a name="bkmk_shared-susdb"></a> Use a shared WSUS database for software update points  

When you install more than one software update point at a primary site, use the same WSUS database for each software update point in the same Active Directory forest. If you share the same database, it significantly mitigates, but doesn't completely eliminate, the client and the network performance impact that you might experience when clients switch to a new software update point. A delta scan still occurs when a client switches to a new software update point that shares a database with the old software update point, but the scan is much smaller than it would be if the WSUS server has its own database. For more information about software update point switching, see [Software update point switching](plan-for-software-updates.md#BKMK_SUPSwitching).  

> [!IMPORTANT]  
>  Also share the local WSUS content folders when you use a shared WSUS database for software update points.  

For more information on sharing the WSUS database, see the following blog posts:  

- [How to implement a shared SUSDB for Configuration Manager software update points](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103)  

- [Considerations for multiple WSUS instances sharing a content database when using Configuration Manager](/archive/blogs/wsus/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb).


### <a name="bkmk_sql-instance"></a> When Configuration Manager and WSUS use the same SQL Server, configure one to use a named instance and the other to use the default instance  

When the Configuration Manager and WSUS databases share the same instance of SQL Server, you can't easily determine the resource usage between the two applications. Use different SQL Server instances for Configuration Manager and WSUS. This configuration makes it easier to troubleshoot and diagnose resource usage issues that might occur for each application.  


### <a name="bkmk_store-local"></a> Specify the "Store updates locally" setting  

When you install WSUS, select the setting to **Store updates locally**. This setting causes WSUS to download the license terms that are associated with software updates. It downloads the terms during the synchronization process and stores them on the local hard drive for the WSUS server. If you don't select this setting, client computers might fail compliance scans for software updates that have license terms. The **WSUS Synchronization Manager** component of the software update point verifies that this setting is enabled every 60 minutes, by default.  

### <a name="bkmk_ssl"></a> Configure your software update points to use TLS/SSL
Configuring Windows Server Update Services (WSUS) servers and their corresponding software update points to use TLS/SSL may reduce the ability of a potential attacker to remotely compromise a client and elevate privileges. To ensure that the best security protocols are in place, we highly recommend that you use the TLS/SSL protocol to help secure your software update infrastructure. For more information, see the [Configure a software update point to use TLS/SSL with a PKI certificate tutorial](../get-started/software-update-point-ssl.md).

## <a name="bkmk_operation"></a> Operational Best Practices  

Use the following best practices when you use software updates:  


### <a name="bkmk_object-limit"></a> Limit software updates to 1000 in a single software update deployment  

Limit the number of software updates to 1000 in each software update deployment. When you create an automatic deployment rule, verify that the specified criteria doesn't result in more than 1000 software updates. If you manually deploy software updates, don't select more than 1000 updates.  


### <a name="bkmk_new-group"></a> Create a new software update group each time an ADR runs for "Patch Tuesday" and for general deployments  

There's a limit of 1000 software updates in a deployment. When you create an automatic deployment rule (ADR), you specify whether to use an existing update group or create a new update group each time the rule runs. If you specify criteria in an ADR that results in multiple software updates, and the rule runs on a recurring schedule, create a new software update group each time the rule runs. This behavior prevents the deployment from surpassing the limit of 1000 software updates per deployment.  


### <a name="bkmk_same-group"></a> Use an existing software update group for ADRs for Endpoint Protection definition updates  

When you use an ADR to deploy Endpoint Protection definition updates on a frequent basis, always use an existing software update group. Otherwise, the ADR potentially creates hundreds of software update groups over time. Definition update publishers typically set definition updates to expire when they're superseded by four newer updates. Therefore, the software update group that's created by the ADR never contains more than four definition updates for the publisher: one active, and three superseded.  



## See Also  
 [Plan for software updates](plan-for-software-updates.md)