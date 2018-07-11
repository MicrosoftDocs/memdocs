---
title: Manage high-risk deployments
titleSuffix: Configuration Manager
description: Learn how to configure deployment verification site settings in Configuration Manager to warn admins if they create a high-risk deployment.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Settings to manage high-risk deployments for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


With Configuration Manager, you can configure deployment verification site settings. These settings warn administrators if they create a high-risk task sequence deployment. A high-risk deployment is:  

-   A deployment that's automatically installed  

-   Has the potential to cause unwanted results  

For example, a task sequence with a purpose of **Required** that deploys an operating system is considered high-risk.  

To reduce the risk of an unwanted high-risk deployment, you can configure size limits in these deployment verification settings:  

-   **Collection size limits**: When you create a deployment, hide collections that include more clients than your limit.  

     -   **Default size**: When you create a deployment, this setting hides collections by default that include more clients than this limit. You can still see these collections when creating the deployment, but they're hidden by default. The default value is **100**. To ignore this setting, enter a value of **0**.  

     -   **Maximum size**: When you create a deployment, this setting always hides collections with more clients than this limit. The default value is **0**, which ignores this setting. The **Maximum size** value must be greater than the **Default size** value.  

     For example, you set **Default size** to 100 and the **Maximum size** to 1000. When you create a high-risk deployment, the **Select Collection** window only displays collections that include fewer than 100 clients. If you clear the setting to **Hide collections with a member count greater than the site's minimum size configuration**, the window displays collections that include fewer than 1000 clients.  

-   **Collections with site system servers**: When the target collection includes a computer with a site system role, block deployments or require verification before creating the deployment. When a deployment is blocked, select a different collection that meets the deployment verification criteria to continue creating the deployment.  

> [!NOTE]  
>  High-risk deployments are always limited to custom collections, collections that you create, and the built-in **Unknown Computers** collection. When you create a high-risk deployment, you can't select a built-in collection such as **All Systems**.  

### Configure deployment verification for a site  

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, select **Sites**, and then select the primary site to configure.  

2.  Click **Properties** in the ribbon, and then switch to the **Deployment Verification** tab.  

3.  After setting configurations you want to use, click **OK** to save the configuration.  


### See also  
 [Configure sites and hierarchies](/sccm/core/servers/deploy/configure/configure-sites-and-hierarchies)
