---
title: "New in 1610 | System Center Configuration Manager"
description: "Get details about changes and new capabilities introduced in version 1610 of System Center Configuration Manager."
ms.custom: na
ms.date:  
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
caps.latest.revision: 40
author: Brendunsms.author: brendunsmanager: angrobe
ROBOTS: "NOINDEX, NOFOLLOW"
---
# What&#39;s new in version 1610 of System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Update 1610 for System Center Configuration Manager current branch is an update that is available as an in-console update for previously installed sites that run version 1511, 1602, or 1606. Version 1511 is the initial baseline version you use to install new Configuration Manager sites.
> [!TIP]  
>  Learn more about:  
>   
>  -   [Installing new sites](https://technet.microsoft.com/library/mt590197.aspx) (using a baseline version like 1511)  
>  -   [Installing updates at sites](https://technet.microsoft.com/library/mt607046.aspx) (like update 1602 or 1606)  

The following sections provide details about changes and new capabilities introduced in version 1610 of Configuration Manager.  

## Customizable Branding for Software Center Dialogs

Custom branding for the Software Center was introduced in Configuration Manager version 1602. In version 1610, that branding is now extended to all associated dialog boxes to provide a more consistent experience to Software Center users.

Custom branding for the Software Center is applied according to the following rules:

1. If the Application Catalog website point site server role is not installed, then Software Center will display the organization name specified in the **Computer Agent** client setting **Organization name displayed in Software Center**. For instructions, see [How to configure client settings](../../core/clients/deploy/configure-client-settings.md).

2. If the Application Catalog website point site server role is installed, then Software Center will display the organization name and color specified in the Application Catalog website point site server role properties. For more information, see [Configuration options for Application Catalog website point](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#Application-Catalog-website-point).

3. If a Microsoft Intune subscription is configured and connected to the Configuration Manager environment, then Software Center will display the organization name, color and company logo specified in the Intune subscription properties. For more information, see [Configuring the Microsoft Intune subscription](../../mdm/deploy-use/setup-hybrid-mdm.md#step-3-configure-intune-subscription).

## Exclude clients from automatic upgrade

You can exclude Windows clients from getting upgraded with new versions of the client software. To do this, you include the client computers in a collection that is specified to be excluded from upgrade. Client in the excluded collection ignore requests to update the client software.  For more information, see [Exclude Windows clients from upgrades](../../clients/manage/upgrade/exclude-clients-windows.md).
