---
title: Technical preview releases
titleSuffix: Configuration Manager
description: Learn about the technical preview branch to test-drive new functionality and capabilities in Configuration Manager.
ms.date: 05/25/2023
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
ms.localizationpriority: medium
ms.collection: tier3
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
> `https://learn.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us` -->

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

- **Technical preview version 2302**

Download a baseline version from the [Evaluation Center](https://www.microsoft.com/en-in/evalcenter/evaluate-microsoft-endpoint-configuration-manager-technical-preview).

<!--
> [!NOTE]
> The Evaluation Center is currently unavailable. As a workaround you can download the ConfigMgr TP 2202 Baseline here : ( https://aka.ms/MECM2202TP-Baseline).
-->


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

### Technical preview version 2305

-[OSD preferred MP option for PXE boot scenario](2023/technical-preview-2305.md) <!--2839966-->
-[New Site Maintenance task “Delete Aged Task Execution Status Messages” is now available on primary servers to cleanup data older than 30 days or configured number of days](2023/technical-preview-2305.md) <!-- 6167745 -->
-[CMG creation using 3rd PartyApp via Console](2023/technical-preview-2305.md) <!--15627214 -->
-[CMG creation using 3rd Party ServerApp via PowerShell](2023/technical-preview-2305.md) <!--17186203 -->
-[Attack Surface Reduction (ASR) capability now marks Server SKU as compliant only after enforcement](2023/technical-preview-2305.md) <!--9217349-->
-[Enhancing security for External service notifications URL](2023/technical-preview-2305.md) <!--10060597-->
-[Enable Bitlocker through ProvisionTS](2023/technical-preview-2305.md) <!--15620822-->
-[Client certificate state in console (self-signed) to match state in control panel(PKI)](2023/technical-preview-2305.md) <!--10278780-->


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

### Technical preview version 2303

- [SQL Server 2022 version support added for Configuration Manager](2023/technical-preview-2303.md#bkmk_SQlodbc) <!--17276757-->
- [Dark theme extended to one customer voice (OCV) wizard](2023/technical-preview-2303.md#bkmk_dark) <!-- 17433655 -->
- [Prerequisites for the site server roles now include ODBC driver for SQL Server](2023/technical-preview-2303.md#bkmk_SQl2022) <!--9081772 -->


### Technical preview version 2302

- [Dark theme extended to delete secondary site wizard](2023/technical-preview-2302.md#bkmk_dark) <!--15942599-->
- [Enable Windows features introduced via Windows servicing that are off by default](2023/technical-preview-2302.md#bkmk_winfeatures) <!-- 16834520 -->

### Technical preview version 2301

- [Removing Microsoft Store for Business and Education new config capability](2023/technical-preview-2301.md#bkmk_msfb) <!--10901602-->
- [Update to the default value of supersedence age in months for software updates](2023/technical-preview-2301.md#bkmk_softwareupdates) <!--16441147-->
- [Microsoft Configuration Manager product branding](2023/technical-preview-2301.md#bkmk_branding)<!-- 15885998. -->
- [Improvements to Cloud Sync (Collections to Azure Active Directory Group Synchronization) feature](2023/technical-preview-2301.md#bkmk_coll_aad_group_sync)<!-- 14716797 -->

### Technical preview version 2211

- [Authorization failure message in admin service now shown in Status message viewer](2022/technical-preview-2211.md#bkmk_audit-admin-service) <!-- 13022894 -->
- [Network Access Account (NAA) account usage alert](2022/technical-preview-2211.md#bkmk_naa-account)<!-- 14538358 -->
- [Improvements to Cloud Sync (Collections to Azure Active Directory Group Synchronization) feature](2022/technical-preview-2211.md#bkmk_coll_aad_group_sync)<!-- 14716797 -->

### Technical preview version 2210

- [Featured Apps in Software Center](2022/technical-preview-2210.md#bkmk_featured-apps-software-center) <!--3601183-->


### Technical preview version 2209

- [Improvements to the console](2022/technical-preview-2209.md#bkmk_improvements-to-the-console) <!--14908615-->
- [Improvements to the dark theme](2022/technical-preview-2209.md#bkmk_improvements-to-the-dark-theme) <!--15346075-->
- [Other Updates](2022/technical-preview-2209.md#bkmk_other-updates) <!--14975011-->

### Technical preview version 2208

- [Intune RBAC for tenant attached devices](2022/technical-preview-2208.md#bkmk_enable-intune) <!--8126836-->
- [Dark theme is now extended to additional dashboards](2022/technical-preview-2208.md#bkmk_improvements-to-the-dark-theme) <!--14917369-->

### Technical preview version 2207

- [Distribution point content migration](2022/technical-preview-2207.md#bkmk_dpconmig) <!--10928371-->
- [Improvements to Configuration Manager policies for Microsoft Defender Application Guard](2022/technical-preview-2207.md#bkmk_app-guard) <!--14059872-->
- [PowerShell release notes preview](2022/technical-preview-2207.md#bkmk_powershell) <!--14637353-->

### Technical preview version 2206

- [Default site boundary group behavior to support cloud source selection](2022/technical-preview-2206.md#bkmk_dbgmp) <!--10674394-->
- [PowerShell release notes preview](2022/technical-preview-2206.md#bkmk_powershell) <!--14431761-->

### Technical preview version 2205

- [Offset for reoccurring monthly maintenance window schedules](2022/technical-preview-2205.md#bkmk_offset) <!--3601127-->
- [Improvements to cloud management gateway (CMG) workflow](2022/technical-preview-2205.md#bkmk_cmg) <!--13351390-->
- [Script execution timeout for compliance settings](2022/technical-preview-2205.md#bkmk_timeout) <!--14120481-->
- [Microsoft Defender for Endpoint onboarding for Windows Server 2012 R2 and Windows Server 2016](2022/technical-preview-2205.md#bkmk_downlevel) <!--9265511-->
- [PowerShell release notes preview](2022/technical-preview-2205.md#bkmk_powershell) <!--14046376-->

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

## Next steps

For more information, see the following articles:

- [Evaluate Configuration Manager in a lab](evaluate-with-lab-environment.md)
- [What's new in Configuration Manager incremental versions](../plan-design/changes/whats-new-incremental-versions.md)
- [Introduction to Configuration Manager](../understand/introduction.md)

> [!TIP]
> For more information on current branch features that require consent to enable, see [pre-release features](../servers/manage/pre-release-features.md).
>
> For more information on current branch features that you must enable first, see [Enable optional features from updates](../servers/manage/optional-features.md).
