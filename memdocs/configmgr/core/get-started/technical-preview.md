---
title: Technical preview releases
titleSuffix: Configuration Manager
description: Learn about the technical preview branch to test-drive new functionality and capabilities in Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Technical preview for Configuration Manager

*Applies to: Configuration Manager (technical preview branch)*

This article provides details about the monthly technical preview branch of Configuration Manager. The technical preview introduces new functionality that Microsoft is working on. It introduces new features that aren't yet included in the current branch of Configuration Manager. These features might eventually be included in an update to the current branch. Before we finalize the features, we want you to try them out and give us feedback.

Because this release is a technical preview, details and functionality are subject to change.

This information applies to all versions of the Configuration Manager technical preview branch. This article lists each new feature along with the technical preview version in which it first appears. For example, version **2001** for January (`01`) of 2020 (`20`). Separate articles dedicated to each preview version detail the individual features.

For information about what's new in the *current branch* of Configuration Manager, see [What's new in Configuration Manager incremental versions](../plan-design/changes/whats-new-incremental-versions.md).

> [!Tip]
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="bkmk_reqs"></a> Requirements and limitations

> [!IMPORTANT]
> The technical preview is licensed for use only in a lab environment. Microsoft may not provide support services and certain features may not be available in technical previews. Additionally, technical preview software may have reduced or different security, privacy, accessibility, availability, and reliability standards relative to commercially provided software.

For most product prerequisites, use the information in the [Supported configurations](../plan-design/configs/supported-configurations.md). The following exceptions apply to the technical preview branch:

- Each install is active for 90 days before it becomes inactive.

- English is the only language supported.

- It only supports the following setup command-line parameters:

  - `/silent`
  - `/testdbupgrade`

- The service connection point installs to online mode. It doesn't support offline mode.

- The separate articles for each specific version of the technical preview include additional limitations or requirements, as applicable.

- The following features aren't supported with the technical preview branch:

  - [Migration](../migration/migrate-data-between-hierarchies.md) to or from this preview branch.

  - [Upgrade](../servers/deploy/install/upgrade-to-configuration-manager.md) to this preview branch.

  - [Site recovery](../servers/manage/recover-sites.md) from the cd.latest folder.<!--507106-->

- There's no support for updating to current branch from this preview branch.

    > [!Note]
    > When updates are available for a preview version, you still find and install them from the **Updates and Servicing** node of the Configuration Manager console. For a video of the in-console upgrade process, see [Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8) on youtube.com.

- It only supports a standalone primary site. There's no support for a central administration site, multiple primary sites, or secondary sites.

The technical preview branch of Configuration Manager supports the following products and technologies:

- Unless otherwise noted, the technical preview branch supports the same versions of SQL Server as the current branch. For more information, see [Supported SQL Server versions](../plan-design/configs/support-for-sql-server-versions.md).

- The site supports up to 10 clients, which can run any [supported client OS version](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).<!-- SCCMDocs#1656 -->

> [!Note]
> The inclusion of these products in this content doesn't imply an extension of support for a version that's beyond its support lifecycle. Configuration Manager doesn't support products that are beyond their support lifecycle. For more information, see [Microsoft Lifecycle Policy](https://support.microsoft.com/lifecycle).

## <a name="bkmk_install"></a> Install and update

The Configuration Manager technical preview branch for lab use is distinct from the Configuration Manager current branch for production use.

First install a baseline version of the technical preview branch. After installing a baseline version, then use in-console updates to bring your installation up to date with the most recent preview version. Typically, new versions of the technical preview are available each month.

Microsoft supports each technical preview version up until three successive versions are available. For example, when version 1908 released, version 1904 was no longer in support. Versions 1905, 1906, and 1907 remained in support. When a baseline falls out of support, it's still supported for installing a new technical preview site, assuming you immediately update to a supported version. The older baseline is supported until a new baseline version is available. Update to the latest available version from the baseline, and then repeat the update process until you install the latest technical preview version.

> [!TIP]
> When you install an update to the technical preview, you update your preview installation to that new technical preview version. A technical preview installation never has the option to upgrade to a current branch installation. It also never receives updates from the current branch release.
>
> Several times throughout the year, there are technical preview branch and current branch versions with the same version number. For example, there is a technical preview version 1910 and a current branch version 1910.

### Active baseline versions

Install a baseline version for up to one year after its release. When you install a new technical preview site, use the latest baseline version. The following Configuration Manager technical preview branch versions are available as both in-console updates and as new baseline versions:

- **Technical preview version 2007**

Download a baseline version from the [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="BKMK_TPFeedback"></a> Providing feedback

We love to hear your feedback about the new features in the technical preview. For more information, see [Product feedback](../understand/find-help.md#product-feedback).

If you have ideas about new features you would like to see, let us know! Submit new ideas and vote on the ideas by others: [Configuration Manager UserVoice](https://configurationmanager.uservoice.com).

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="bkmk_tpCaps"></a> Features in the most recent version

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2007.md) <!--ID-->

The following features are available with the most recent Configuration Manager technical preview version:

### Technical preview version 2008

- [Collection query preview](2020/technical-preview-2008.md#collection-query-preview) <!--7380401-->
- [Analyze SetupDiag errors for feature updates](2020/technical-preview-2008.md#bkmk_setupdiag) <!--4385028-->
- [Monitor scenario health](2020/technical-preview-2008.md#bkmk_health) <!--7699463-->
- [Collection evaluation view](2020/technical-preview-2008.md#bkmk_colleval) <!--6251274-->
- [See task sequence size in the console](2020/technical-preview-2008.md#bkmk_tssize) <!--7645732-->
- [Delete Aged Collected Diagnostic Files task](2020/technical-preview-2008.md#bkmk_logs) <!--6503308-->
- [Import objects to current folder](2020/technical-preview-2008.md#bkmk_folder) <!--6601203-->

> [!NOTE]
> Features that were available in a previous version of the technical preview remain available in later versions. Similarly, features that are added to the Configuration Manager current branch remain available in the technical preview branch.

## Features in recent technical previews

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

The following features were released with previous versions of the Configuration Manager technical preview branch since current branch version 2006:

> [!TIP]
> When a new current branch version is available, features that are available in that version are listed in the latest *What's new* article. For more information, see [What's new in incremental versions](../plan-design/changes/whats-new-incremental-versions.md#supported-versions).

### Technical preview version 2007

- [Tenant attach: View hardware inventory in Microsoft Endpoint Manager admin center](2020/technical-preview-2007.md#bkmk_mem) <!--6479284-->
- [Improvements to client data sources dashboard](2020/technical-preview-2007.md#bkmk_content) <!--7102084-->
- [Fixed-width font now used in some console areas](2020/technical-preview-2007.md#bkmk_font) <!--7632637-->
- [Manage task sequence policy size](2020/technical-preview-2007.md#bkmk_tspol) <!--6888853-->
- [Improvements to device timeline in the admin center](2020/technical-preview-2007.md#bkmk_timeline)<!--7141381-->

## Features in previous technical previews

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

The following features were released with previous versions of the Configuration Manager technical preview branch. These features remain available in later versions, but aren't yet available in the current branch.

| Feature        | Technical preview version |
|----------------|---------------------------|
| Use the Company Portal app on co-managed devices <!--3601237--> | [Tech preview 2006](2020/technical-preview-2006.md#bkmk_portal) |
| Improvements to available apps via CMG <!--7033501--> | [Tech preview 2006](2020/technical-preview-2006.md#bkmk_availapp) |
| Tenant Attach: Improvements to Configuration Manager actions in Microsoft Endpoint Manager admin center <!--7518897--> | [Tech preview 2006](2020/technical-preview-2006.md#bkmk_apps) |
| Tenant attach: Device timeline in the admin center <!--7141381--> | [Tech preview 2005](2020/technical-preview-2005.md#bkmk_timeline) |
| Tenant attach: Install an application from the admin center <!--6024389--> | [Tech preview 2005](2020/technical-preview-2005.md#bkmk_apps) |
| Tenant attach: CMPivot from the admin center <!--6024392--> | [Tech preview 2005](2020/technical-preview-2005.md#bkmk_cmpivot) |
| Tenant attach: Run Scripts from the admin center <!--6234688--> | [Tech preview 2005](2020/technical-preview-2005.md#bkmk_scripts) |
| Improvements to cloud management gateway cmdlets <!--6978300--> | [Tech preview 2005](2020/technical-preview-2005.md#bkmk_pwshcmg) |
| Report setup and upgrade failures to Microsoft <!--5622909--> | [Tech preview 2005](2020/technical-preview-2005.md#report-setup-and-upgrade-failures-to-microsoft) |
| Improvements to the content library cleanup tool <!--6887878--> | [Tech preview 2005](2020/technical-preview-2005.md#bkmk_content) |
| Copy discovery data from the console <!--6890051--> | [Tech preview 2004](2020/technical-preview-2004.md#bkmk_copydisco) |
| Support for PowerShell version 7 <!--6023299--> | [Tech preview 2004](2020/technical-preview-2004.md#bkmk_pwsh7) |
| New feedback wizard <!--3180826--> | [Tech preview 2003](2020/technical-preview-2003.md#bkmk_feedback) |
| Query for feedback sent to Microsoft <!--6488450--> | [Tech preview 2003](2020/technical-preview-2003.md#bkmk_smile) |
| Attach files to feedback <!--3556011--> | [Tech preview 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Improvements to multicast-enabled distribution points <!--3785535--> | [Tech preview 1908.2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Phased deployment templates <!--4961086--> | [Tech preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Remote control anywhere using cloud management gateway <!--4575930--> | [Tech Preview 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Cloud services cost estimator <!--3555774--> | [Tech Preview 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| Client-based PXE responder service <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| PXE network boot support for IPv6 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Use Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Improvements to Asset Intelligence <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## See also

For more information, see the following articles:

- [Evaluate Configuration Manager in a lab](evaluate-with-lab-environment.md)
- [What's new in Configuration Manager incremental versions](../plan-design/changes/whats-new-incremental-versions.md)
- [Introduction to Configuration Manager](../understand/introduction.md)

> [!Tip]
> For more information on current branch features that require consent to enable, see [pre-release features](../servers/manage/pre-release-features.md).
>
> For more information on current branch features that you must enable first, see [Enable optional features from updates](../servers/manage/install-in-console-updates.md#bkmk_options).
