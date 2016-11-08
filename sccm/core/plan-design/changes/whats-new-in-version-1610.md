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

## In-console monitoring of update installation status
Beginning with version 1610, when you install an update pack and monitor the installation in the console, there is a new phase: **Post Installation**. This phase includes status for tasks like restarting key services, and initialization of replication monitoring. (This phase is not available in the console until after your site updates to version 1610.) For more information about update installation status, see [Install in-console updates](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

## Improvements to the Windows 10 Edition Upgrade Policy

In this release, the following improvements have been made to this policy type:

- You can now use the edition upgrade policy with Windows 10 PCs that run the Configuration Manager client in addition to Windows 10 PCs are enrolled with Microsoft Intune.
- You can upgrade from Windows 10 Professional to any of the platforms in the wizard that are compatible with your hardware.

## Improvements for boundary groups
Version 1610 introduces important changes to boundary groups and how they work with distribution points. These changes can simplify the design of your content infrastructure while giving you more control over how and when clients fallback to search additional distribution points as content source locations. This includes both on-premises and cloud-based distribution points.
These improvements replace concepts and behaviors you might be familiar with today (like configuring distribution points to be fast or slow) and replaces them with a new model that should be easier to setup and maintain. These changes are also groundwork for future changes that will improve other site system roles you associate to boundary groups.

When you update to version 1610, the update converts your current boundary group configurations to fit the new model so that these changes do not disturb your existing content distribution configurations.

For more information, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


## Migrate multiple shared distribution points at the same time
You can now use the option to **Reassign Distribution Point** to have Configuration Manager process in parallel the reassignment of up to 50 shared distribution points at the same time. Prior to this release, reassigned distribution points were processed one at a time. For more information see, [Migrate multiple shared distribution points at the same time](/sccmn/core/migration/planning-a-content-deployment-migration-strategy#mictrage-multiple-shared-distributionpoints-at-the-same-time).
