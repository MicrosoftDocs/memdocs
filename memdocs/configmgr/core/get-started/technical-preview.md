---
title: Technical preview releases
titleSuffix: Configuration Manager
description: Learn about the technical preview branch to test-drive new functionality and capabilities in Configuration Manager.
ms.date: 05/23/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
ms.collection: highpri
---

# Technical preview for Configuration Manager

*Applies to: Configuration Manager (technical preview branch)*

This article provides details about the monthly technical preview branch of Configuration Manager. The technical preview introduces new functionality that Microsoft is working on. It introduces new features that aren't yet included in the current branch of Configuration Manager. These features might eventually be included in an update to the current branch. Before we finalize the features, we want you to try them out and give us feedback.

Because this release is a technical preview, details and functionality are subject to change.

This information applies to all versions of the Configuration Manager technical preview branch. This article lists each new feature along with the technical preview version in which it first appears. For example, version **2201** for January (`01`) of 2022 (`22`). Separate articles dedicated to each preview version detail the individual features.

For information about what's new in the *current branch* of Configuration Manager, see [What's new in Configuration Manager incremental versions](../plan-design/changes/whats-new-incremental-versions.md).

> [!TIP]
> You can use RSS to be notified when this page is updated. For more information, see [How to use the docs](../../../use-docs.md#notifications).
<!-- > To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us` -->

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

    > [!NOTE]
    > You may need to allow specific internet URLs, some of which are specific to the technical preview branch. For more information, see [Internet access requirements](../plan-design/network/internet-endpoints.md).

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
> Several times throughout the year, there are technical preview branch and current branch versions with the same version number. For example, there is a technical preview version 2006 and a current branch version 2006.

### Active baseline versions

Install a baseline version for up to one year after its release. When you install a new technical preview site, use the latest baseline version:

- **Technical preview version 2202**

> [!NOTE]
> The Evaluation Center is currently unavailable. As a workaround you can download the latest technical preview branch baseline build from [aka.ms/MECM2202TP-Baseline](https://aka.ms/MECM2202TP-Baseline).<!-- 14437681 -->

## <a name="BKMK_TPFeedback"></a> Providing feedback

We love to hear your feedback about the new features in the technical preview. For more information, see [Product feedback](../understand/product-feedback.md).

If you have ideas about new features you would like to see, let us know! Submit new ideas and vote on the ideas by others: [Feedback for Configuration Manager](https://feedbackportal.microsoft.com/feedback/forum/4669adfc-ee1b-ec11-b6e7-0022481f8472).<!-- 10948264 -->

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="bkmk_tpCaps"></a> Features in the most recent version

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2021/technical-preview-2101.md) <!-- ID -->

The following features are available with the most recent Configuration Manager technical preview version:

### Technical preview version 2205

- [Offset for reoccurring monthly maintenance window schedules](2022/technical-preview-2205.md#bkmk_offset) <!--3601127-->
- [Improvements to cloud management gateway (CMG) workflow](2022/technical-preview-2205.md#bkmk_cmg) <!--13351390-->
- [Script execution timeout for compliance settings](2022/technical-preview-2205.md#bkmk_timeout) <!--14120481-->
- [Microsoft Defender for Endpoint onboarding for Windows Server 2012 R2 and Windows Server 2016](2022/technical-preview-2205.md#bkmk_downlevel) <!--9265511-->
- [PowerShell release notes preview](2022/technical-preview-2205.md#bkmk_powershell) <!--14046376-->

> [!NOTE]
> Features that were available in a previous version of the technical preview remain available in later versions. Similarly, features that are added to the Configuration Manager current branch remain available in the technical preview branch.

## Features in recent technical previews

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

The following features were released with previous versions of the Configuration Manager technical preview branch since the latest current branch version:

> [!TIP]
> When a new current branch version is available, features that are available in that version are listed in the latest *What's new* article. For more information, see [What's new in incremental versions](../plan-design/changes/whats-new-incremental-versions.md#supported-versions).

<!-- ### Technical preview version 2111 -->

### Technical preview version 2204

- [Administration Service Management option](2022/technical-preview-2204.md#bkmk_administration) <!--12952905-->
- [Folders for automatic deployment rules (ADRs)](2022/technical-preview-2204.md#bkmk_folder) <!--13507410-->

### Technical preview version 2203

- [Dark theme for the console](2022/technical-preview-2203.md#bkmk_dark) <!--9070525-->
- [Escrow BitLocker recovery password to the site during a task sequence](2022/technical-preview-2203.md#bkmk_blmts) <!--10454717-->
- [PowerShell release notes preview](2022/technical-preview-2203.md#bkmk_powershell) <!--13395691-->

### Technical preview version 2202

- [Delete collection references](2022/technical-preview-2202.md#bkmk_delcollref) <!--9708999-->
- [Pre-download content for available software updates](2022/technical-preview-2202.md#bkmk_pre-download) <!--4497776-->
- [Added folder support for nodes in the Software Library](2022/technical-preview-2202.md#bkmk_folder) <!--3601129-->
- [New client health checks](2022/technical-preview-2202.md#bkmk_health) <!--10954111-->
- [Improvements to implicit uninstall](2022/technical-preview-2202.md#bkmk_implicit) <!--12488148-->
- [Improvements for sending feedback](2022/technical-preview-2202.md#bkmk_feedback) <!--11754191-->
- [Improvements to Management Insights](2022/technical-preview-2202.md#bkmk_insights) <!--10875436-->
- [Improvements to dashboards](2022/technical-preview-2202.md#bkmk_webview2) <!--10024154-->
- [ADR scheduling improvements for deployments](2022/technical-preview-2202.md#bkmk_adr) <!--12707738-->
- [Console improvements](2022/technical-preview-2202.md#bkmk_console) <!--9575773-->
- [PowerShell release notes preview](2022/technical-preview-2202.md#bkmk_powershell) <!--13040432-->

### Technical preview version 2201

- [Visualize content distribution status](2022/technical-preview-2201.md#bkmk_contentviz) <!--9495651-->
- [Custom icon support for task sequences and packages](2022/technical-preview-2201.md#bkmk_tsico) <!--12486335-->
- [Prefer cloud-based software update points on switching](2022/technical-preview-2201.md#bkmk_cmgsup) <!--7759984-->
- [LEDBAT support for software update points](2022/technical-preview-2201.md#bkmk_ledbat) <!--4639895-->
- [Improvements to Power BI Report Server Integration](2022/technical-preview-2201.md#bkmk_reports) <!--12487076-->
- [Tenant attach features are generally available](2022/technical-preview-2201.md#bkmk_ta) <!--6374854-->
- [Deployment Status client notification actions](2022/technical-preview-2201.md#bkmk_notify) <!--7079837-->
- [Sort by icon in the console](2022/technical-preview-2201.md#bkmk_sortico) <!--3877839-->
- [PowerShell release notes preview](2022/technical-preview-2201.md#bkmk_powershell) <!--12654996-->
- [Improved notice for content on task sequence media](2022/technical-preview-2201.md#bkmk_tsmedia) <!--12895956-->

### Technical preview version 2112
<!-- all items are in 2111 CB -->

- [Customize maximum run time for other software update types](2021/technical-preview-2112.md#bkmk_maxruntime) <!--12770887-->
- [Console and user experience improvements](2021/technical-preview-2112.md#bkmk_ux) <!--12726153-->
- [Exclude data warehouse reporting tables from synchronization](2021/technical-preview-2112.md#bkmk_warehouse) <!--12441118-->
- [A new remote assistance tool](2021/technical-preview-2112.md#bkmk_cmgrc) <!--4575930-->


## Features in previous technical previews

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

The following features were released with previous versions of the Configuration Manager technical preview branch. These features remain available in later versions, but aren't yet available in the current branch.

| Feature        | Technical preview version |
|----------------|---------------------------|
|Customize maximum run time for other software update types <!--12770887--> | [Tech preview 2112](2021/technical-preview-2112.md#bkmk_maxruntime)|
|Console and user experience improvements <!--12726153-->| [Tech preview 2112](2021/technical-preview-2112.md#bkmk_ux)|
|Exclude data warehouse reporting tables from synchronization <!--12441118--> | [Tech preview 2112](2021/technical-preview-2112.md#bkmk_warehouse)|
| Branding in the Windows Update native reboot experience <!--10543514--> | [Tech preview 2110](2021/technical-preview-2110.md#bkmk_brand) |
| Tenant attach: Software updates information <!--6024419--> | [Tech preview 2107](2021/technical-preview-2107.md#bkmk_sum) |
| Intune role-based access control for tenant attach <!--8126836--> | [Tech preview 2106](2021/technical-preview-2106.md#bkmk_rbac) |
| Windows Update native experience for software updates <!--4316341--> | [Tech preview 2105.2](2021/technical-preview-2105-2.md#bkmk_wu) |
| Support Center dark and light themes <!--8218853--> | [Tech preview 2105](2021/technical-preview-2105.md#bkmk_dark) |
| Community hub support for application content <!--7983035--> | [Tech preview 2012](2020/technical-preview-2012.md#bkmk_hubapp) |
| Improvements to multicast-enabled distribution points <!--3785535--> | [Tech preview 1908.2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Phased deployment templates <!--4961086--> | [Tech preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Client-based PXE responder service <!--3556018, fka 1357148--> | [Tech preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| PXE network boot support for IPv6 <!--3601254, fka 1269793--> |[Tech preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Use Azure Active Directory <!--3607315, fka 1322145--> | [Tech preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Improvements to Asset Intelligence <!--3601024, fka 1307390--> | [Tech preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## Next steps

For more information, see the following articles:

- [Evaluate Configuration Manager in a lab](evaluate-with-lab-environment.md)
- [What's new in Configuration Manager incremental versions](../plan-design/changes/whats-new-incremental-versions.md)
- [Introduction to Configuration Manager](../understand/introduction.md)

> [!TIP]
> For more information on current branch features that require consent to enable, see [pre-release features](../servers/manage/pre-release-features.md).
>
> For more information on current branch features that you must enable first, see [Enable optional features from updates](../servers/manage/optional-features.md).
