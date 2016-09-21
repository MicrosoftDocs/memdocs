---
title: "Manage high-risk deployments | System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
caps.latest.revision: 6
author: Brenduns
translation.priority.ht: 
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Settings to manage high-risk deployments for System Center Configuration Manager
With System Center Configuration Manager you can configure site settings that will warn admins if they create a high-risk task sequence deployment. A high-risk deployment is:  
  
-   A deployment that is automatically installed  
  
-   Has the potential to cause unwanted results  
  
 For example, a task sequence that has a purpose of **Required** that deploys an operating system is considered high-risk.  
  
 To reduce the risk of an unwanted high-risk deployment, you can configure size limits in these deployment verification settings:  
  
-   **Collection size limits**: Hide collections that contain more clients than your limit when you create a deployment.  
  
    -   **Default size**: This setting hides collections, by default, with more clients than your limit when you create a deployment. You can still see these collections when creating the deployment, but they are hidden by default. The default value is 100. Enter a value of 0 to ignore this setting.  
  
    -   **Maximum size**: This setting always hides collections with more clients than your limit when you create a deployment. The default value is 0, which ignores this setting. The **Maximum size** value must be greater than the **Default size** value.  
  
     For example, you set **Default size** to 100 and the **Maximum size** to 1000. When you create a high risk deployment, the **Select Collection** window will only display collections that contain fewer than 100 clients. If you clear the **Hide collections with a member count greater than the site’s minimum size configuration** setting, the window will display collections that contain fewer than 1000 clients.  
  
-   **Collections with site system servers**: Block deployments, or require verification before creating the deployment, when the target collection contains a computer with a site system role. When a deployment is blocked, you must select a different collection that meets the deployment verification criteria.  
  
> [!NOTE]  
>  High-risk deployments are always limited to custom collections, collections that you create, and the built-in **Unknown Computers** collection. When you create a high-risk deployment, you cannot select a built-in collection such as **All Systems**.  
  
### To configure deployment verification for a site  
  
1.  In the Configuration Manager console, choose **Administration** >**Site Configuration** > **Sites**, and then select the primary site to configure.  
  
2.  On the **Home** tab, in the **Properties** group, choose **Properties**, and then choose the **Deployment Verification** tab.  
  
3.  After setting configurations you want to use, choose  **OK**  to save the configuration.  
  
### See also  
 [Configure sites and hierarchies for System Center Configuration Manager](../../core/servers/deploy/configure/configure-sites-and-hierarchies.md)