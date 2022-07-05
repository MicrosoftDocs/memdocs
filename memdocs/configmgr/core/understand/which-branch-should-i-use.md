---
title: Which branch should I use
titleSuffix: Configuration Manager
description: Learn the differences between available branches of Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Which branch of Configuration Manager should I use?

*Applies to: Configuration Manager (current branch & technical preview branch) & System Center Configuration Manager (long-term servicing branch)*

There are three branches of Configuration Manager available:

- Current branch
- Long-term servicing branch
- Technical preview branch

Use this article to help you choose the right branch.

> [!TIP]  
> All sites in a hierarchy must run the same branch. It isn't supported to have a hierarchy with different branches at different sites.

## Current branch

This branch is licensed for use in a production environment. Use this branch to get the latest features and functionalities. If you have one of the following licenses, you can use this branch:  

- System Center Datacenter
- System Center Standard
- System Center Configuration Manager
- Equivalent subscription rights  

For more information about Software Assurance and licensing options, see [Licensing and branches for Configuration Manager](learn-more-editions.md) and [Frequently asked questions for Configuration Manager branches and licensing](product-and-licensing-faq.yml).

Microsoft plans to release updates for Configuration Manager current branch a few times per year. Each update version remains in support for 18 months from its general availability (GA) release date. Technical support is provided for the entire period of support. However, our support structure is dynamic, evolving into two distinct servicing phases that depend on the availability of the latest current branch version. (For more information, see [Support for Configuration Manager current branch versions](../servers/manage/current-branch-versions-supported.md). Updates to newer versions are available as in-console updates.

To install the current branch as a new site, use [baseline media](../servers/manage/updates.md#bkmk_Baselines). Also use baseline media to upgrade from System Center 2012 Configuration Manager with Service Pack 2 or System Center 2012 R2 Configuration Manager with Service Pack 1. Access to this media depends on how your organization licenses Configuration Manager.

You can also use the baseline media to install a new site that is an evaluation edition of the current branch. The evaluation edition doesn't require a license. You can use the evaluation edition for 180 days. It supports upgrade to a licensed edition of the current branch. To install only an evaluation edition, get it from the [Evaluation Center](https://www.microsoft.com/evalcenter/download-microsoft-endpoint-configuration-manager).


<!--
> [!NOTE]
<<<<<<< HEAD
> The Evaluation Center is currently unavailable. As a workaround you can download the ConfigMgr 2203 Current Branch Eval exe here : ( https://aka.ms/MECM2203CB-Eval).
-->
>
> Use baseline media to install sites for a new Configuration Manager hierarchy. If you previously installed a baseline version, use in-console updates to update your sites to a new version.  
>
> Sites that are updated using in-console updates result in sites that are the same as the new site installed using the baseline media.
>
> For more information, see [Updates for Configuration Manager](../servers/manage/updates.md).  

### Features of the current branch

- Receives [in-console updates](../servers/manage/install-in-console-updates.md) that make new features available for use.
- Receives in-console updates that deliver security and quality fixes to existing features.
- Supports out-of-band updates when necessary. For more information, see [Use the update registration tool](../servers/manage/use-the-update-registration-tool-to-import-hotfixes.md) or [Use the hotfix installer](../servers/manage/use-the-hotfix-installer-to-install-updates.md).
- Integrates with cloud-based services.
- Supports [migration of data](../migration/migrate-data-between-hierarchies.md) to and from other Configuration Manager installations.
- Supports upgrade from previous versions of Configuration Manager.
- Supports installation as an evaluation edition, from which you can later upgrade to a fully licensed installation.

Microsoft recommends that you update to the newest version soon after its release. You can wait up to 18 months before updating to a newer version. You can also skip an update to install the newest version available. Because each version is cumulative, if you skip over an update and install the newest version, you still get access to all features and improvements from previous versions.

For more information, see [Support for current branch versions](../servers/manage/current-branch-versions-supported.md).

### Current branch update options

- With active Software Assurance, you can install in-console updates for current branch versions.  
- There's no option to convert the current branch to a technical preview branch. Technical preview branches are separate installations that don't require a license.
- There's no option to convert your current branch to the long-term servicing branch (LTSB). You must uninstall the current branch and then install the LTSB as a new installation.

## Long-term servicing branch

This branch is licensed for use in production for Configuration Manager customers who are using the current branch and have allowed their Configuration Manager Software Assurance (SA) or equivalent subscription rights to expire after October 1, 2016. For more about Software Assurance and licensing options, see [Licensing and branches for Configuration Manager](learn-more-editions.md) and [Frequently asked questions for Configuration Manager branches and licensing](product-and-licensing-faq.yml).

The LTSB is based on version 1606. This branch doesn't receive in-console updates that deliver new features or update existing capabilities. However, critical security fixes are provided. To install the LTSB, you must use the version 1606 [baseline media](../servers/manage/updates.md#bkmk_Baselines) that you get with System Center 2016. Later baseline versions don't support install of the LTSB.

To install the LTSB as a new site or as an upgrade from a supported System Center 2012 Configuration Manager site, use the version 1606 [baseline media](../servers/manage/updates.md#bkmk_Baselines) that you get with System Center 2016. You can use baseline media to install a new site that runs version 1606 of the current branch, or a new site that runs the long-term servicing branch.

> [!TIP]  
> To learn about System Center 2016, see [System Center 2016 documentation](/system-center/index). This documentation also identifies how to get System Center 2016, which requires a Microsoft license agreement or similar rights.  
>  
> To find Configuration Manager version 1606 in the Volume Licensing Service Center (VLSC), go to the **Downloads and Keys** tab of the [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), search for `System Center 2016`, and then select either **System Center 2016 Datacenter** or **System Center 2016 Standard**.  

>  
> You can also get an evaluation edition of System Center 2019 from the [Evaluation Center](https://www.microsoft.com/evalcenter/download-system-center-2019).  

<!--
> [!NOTE]
> The Evaluation Center is currently unavailable. As a workaround you can download the ConfigMgr TP 2202 Baseline here : ( https://aka.ms/MECM2202TP-Baseline).
-->

### Features of the LTSB

- Receives in-console updates that deliver critical security fixes.
- Provides an installation option when your SA agreement or equivalent rights to Configuration Manager have expired.
- Supports upgrade (conversion) to the current branch when you have a current SA agreement or equivalent rights to Configuration Manager.

### LTSB limitations

The LTSB is based on the current branch version 1606 and has the following limitations:

- The LTSB is supported for 10 years of critical security updates after its general availability (October 2016), after which, support for this branch expires. For more information about the support lifecycle, see [Microsoft Lifecycle Policy](https://support.microsoft.com/lifecycle).
- Supports a limited set list of server and client operating systems and related technologies, like SQL Server versions. For more information, see [Supported configurations for the long-term servicing branch](supported-configurations-for-ltsb.md).
- Doesn't receive updates for new features
- Doesn't support the following capabilities:
  - Cloud-attached features like co-management or Desktop Analytics
  - On-premises MDM
  - The Windows servicing dashboard, servicing plans, or Windows release channels
  - Future releases of Windows 10 LTSB and Windows Server
  - Asset intelligence
  - Any pre-release features

### LTSB update options

- You can convert your LTSB install to a current branch installation. Conversion to the current branch is supported before or after support for the LTSB expires.

  To convert, you must have an active Software Assurance agreement with Microsoft. For more information, see the following articles:

  - [Upgrade the long-term servicing branch to the current branch](convert-to-current-branch.md)
  - [Licensing and branches for Configuration Manager](learn-more-editions.md)
  - [Baseline and update versions](../servers/manage/updates.md#bkmk_Baselines)

- There's no option to convert the LTSB to a technical preview branch. Technical preview branches are separate installations that don't require a license.

- You can't upgrade an evaluation edition of the current branch to an LTSB installation.

## Technical preview branch

The technical preview branch is for use in a lab environment. Learn about and try out the newest features being developed for Configuration Manager. It isn't supported in a production environment, and doesn't require you to have a Software Assurance license agreement.

To install a new site that runs the technical preview branch, use the latest [baseline media for the technical preview branch](../get-started/technical-preview.md#bkmk_install). After you install the technical preview branch, new versions are available as in-console updates each month.

### Features of the technical preview branch

- Based on recent baseline versions of the current branch
- Receives in-console updates that update your installation to the latest technical preview branch version
- Includes new features that are being developed, and for which Microsoft wants your feedback
- Receives updates that apply only to the technical preview branch

### Technical preview limitations

- [Support is limited](../get-started/technical-preview.md#bkmk_reqs), including only a single primary site and up to 10 clients.  
- You can't upgrade or migrate it to a current branch or LTSB installation.
- Doesn't support the following behaviors:
  - Use migration to import or export data to another Configuration Manager installation
  - Upgrade from a previous version of Configuration Manager
  - Install as an evaluation edition

Features that are first introduced in a technical preview branch are often added to the current branch in a later update. Each new technical preview branch version includes the features from previous technical preview branches, even after those features have been added to the current branch.

For more information, see the [Technical preview for Configuration Manager](../get-started/technical-preview.md).

### Technical preview update options

- You can install any in-console update for a new technical preview branch version.

- There's no option to convert a technical preview branch to the current branch or LTSB.

## Identify your version and branch

### Version

To check the version of your site, in the console go to **About Configuration Manager** at the upper-left corner of the console. This dialog displays the **Site version**. For a list of site versions, see [Baseline and update versions](../servers/manage/updates.md#bkmk_Baselines).

### Branch

To confirm the branch of your site, in the console go to **Administration** > **Site Configuration** > **Sites**, and open **Hierarchy Settings**. If there's an active option to convert to the current branch, the site runs the LTSB version. When the site runs the current branch, the console disables this option.

For more information about the different versions of Configuration Manager, see [Baseline and update versions](../servers/manage/updates.md#bkmk_Baselines).