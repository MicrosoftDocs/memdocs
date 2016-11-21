---
title: "Update and retire applications | Microsoft Docs"
description: "Revise, supersede, or uninstall deployed applications by using System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
caps.latest.revision: 9
author: robstackmsftms.author: robstack
manager: angrobe

---
# Update and retire applications with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*

Eventually, you will likely want to make changes to an application, uninstall it, or replace an already deployed application with a new application. System Center Configuration Manager includes these capabilities to help you with this:  

-   **Revise applications** - When you make changes to an application or deployment type, Configuration Manager maintains a history of these changes. You can revert the application to a previous revision at any time. You can also view its properties, restore a previous revision of an application, or delete an old revision.  

     For more information, see [Application revisions](/sccm/apps/deploy-use/revise-and-supersede-applications#application-revisions).  

-   **Supersede applications** - Lets you upgrade or replace existing applications by using a supersedence relationship. When you supersede an application, you can specify a new deployment type to replace the deployment type of the superseded application and also configure whether to upgrade or uninstall the superseded application before the superseding application is installed.  

     For more information, see [Application supersedence](/sccm/apps/deploy-use/revise-and-supersede-applications#application-supersedence).  

-   **Uninstall applications** - Configuration Manager makes uninstalling an application easy. This can be accomplished silently, without any intervention from the end user.  

For more information, see [Uninstall applications](../../apps/deploy-use/uninstall-applications.md).  
