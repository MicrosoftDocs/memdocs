---
title: Technical preview releases
titleSuffix: Configuration Manager
description: Learn about the technical preview branch to test-drive new functionality and capabilities in Configuration Manager.
ms.date: 02/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
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

For information about what's new in the *current branch* of Configuration Manager, see [What's new in Configuration Manager incremental versions](/sccm/core/plan-design/changes/whats-new-incremental-versions).

> [!Tip]
> To get notified when this page is updated, copy and paste the following URL into your RSS feed reader:
> `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="bkmk_reqs"></a> Requirements and limitations

> [!IMPORTANT]
> The technical preview is licensed for use only in a lab environment. Microsoft may not provide support services and certain features may not be available in technical previews. Additionally, technical preview software may have reduced or different security, privacy, accessibility, availability, and reliability standards relative to commercially provided software.

For most product prerequisites, use the information in the [Supported configurations](/sccm/core/plan-design/configs/supported-configurations). The following exceptions apply to the technical preview branch:

- Each install is active for 90 days before it becomes inactive.

- English is the only language supported.

- It only supports the following setup command-line parameters:

  - `/silent`
  - `/testdbupgrade`

- The service connection point installs to online mode. It doesn't support offline mode.

- The separate articles for each specific version of the technical preview include additional limitations or requirements, as applicable.

- The following features aren't supported with the technical preview branch:

  - [Migration](/sccm/core/migration/migrate-data-between-hierarchies) to or from this preview branch.

  - [Upgrade](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) to this preview branch.

  - [Site recovery](/sccm/core/servers/manage/recover-sites) from the cd.latest folder.<!--507106-->

- There's no support for updating to current branch from this preview branch.

    > [!Note]
    > When updates are available for a preview version, you still find and install them from the **Updates and Servicing** node of the Configuration Manager console. For a video of the in-console upgrade process, see [Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8) on youtube.com.

- It only supports a standalone primary site. There's no support for a central administration site, multiple primary sites, or secondary sites.

The technical preview branch of Configuration Manager supports the following products and technologies:

- It only supports the following versions of **SQL Server**:

  - SQL Server 2017 (with cumulative update 2 or later)
  - SQL Server 2016 (with no service pack or later)
  - SQL Server 2014 (with service pack 1 or later)
  - SQL Server 2012 (with service pack 3 or later)

- The site supports up to 10 clients, which can run any [supported client OS version](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).<!-- SCCMDocs#1656 -->

> [!Note]
> The inclusion of these products in this content doesn't imply an extension of support for a version that's beyond its support lifecycle. Configuration Manager doesn't support products that are beyond their support lifecycle. For more information, see [Microsoft Lifecycle Policy](https://go.microsoft.com/fwlink/p/?LinkId=208270).

## <a name="bkmk_install"></a> Install and update

The Configuration Manager technical preview branch for lab use is distinct from the Configuration Manager current branch for production use.

First install a baseline version of the technical preview branch. After installing a baseline version, then use in-console updates to bring your installation up to date with the most recent preview version. Typically, new versions of the technical preview are available each month.

Microsoft supports each technical preview version up until three successive versions are available. For example, when version 1908 released, version 1904 was no longer in support. Versions 1905, 1906, and 1907 remained in support. When a baseline falls out of support, it's still supported for installing a new technical preview site, assuming you immediately update to a supported version. The older baseline is supported until a new baseline version is available. Update to the latest available version from the baseline, and then repeat the update process until you install the latest technical preview version.

> [!TIP]
> When you install an update to the technical preview, you update your preview installation to that new technical preview version. A technical preview installation never has the option to upgrade to a current branch installation. It also never receives updates from the current branch release.
>
> Several times throughout the year, there are technical preview branch and current branch versions with the same version number. For example, there is a technical preview version 1910 and a current branch version 1910.

### Active baseline versions

Install a baseline version for up to one year after its release. When you install a new technical preview site, use the latest baseline version.

- **Technical preview version 1911**: The Configuration Manager technical preview branch version 1911 is available as both an in-console update and as a new baseline version.

Download a baseline version from the [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="BKMK_TPFeedback"></a> Providing feedback

We love to hear your feedback about the new features in the technical preview. For more information, see [Product feedback](/sccm/core/understand/find-help#product-feedback).

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
<!-- - [title](/sccm/core/get-started/2020/technical-preview-2002#bkmk_anchor) <!--ID-->

The following features are available with the most recent Configuration Manager technical preview version:

### Technical preview version 2002

- [Evaluate software updates after a servicing stack update](/sccm/core/get-started/2020/technical-preview-2002#bkmk_ssu) <!--4639943-->
- [Office 365 updates for disconnected software update points](/sccm/core/get-started/2020/technical-preview-2002#bkmk_O365) <!--4065163-->
- [Improvements to Microsoft Edge management](/sccm/core/get-started/2020/technical-preview-2002#bkmk_edge) <!--4561024-->
- [Improvements to Orchestration Groups](/sccm/core/get-started/2020/technical-preview-2002#bkmk_orch) <!--3098816-->
- [Proxy support for Azure Active Directory discovery and group sync](/sccm/core/get-started/2020/technical-preview-2002#bkmk_aad) <!--5913817-->
- [Improvements to BitLocker management](/sccm/core/get-started/2020/technical-preview-2002#bkmk_bitlocker) <!--5925683-->
- [Additional improvements to task sequence progress](/sccm/core/get-started/2020/technical-preview-2002#bkmk_tsprogress) <!--5932692-->

> [!NOTE]  
> Features that were available in a previous version of the technical preview remain available in later versions. Similarly, features that are added to the Configuration Manager current branch remain available in the technical preview branch.  

## Features in recent technical previews

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

The following features were released with previous versions of the Configuration Manager technical preview branch since current branch version 1910:

### Technical preview version 2001.2

- [Token based authentication for cloud management gateway](/sccm/core/get-started/2020/technical-preview-2001-2#bkmk_cmg) <!--5686290-->
- [Improvements to orchestration groups](/sccm/core/get-started/2020/technical-preview-2001-2#bkmk_orch) <!--3098816-->
- [New cmdlets for phased deployments](/sccm/core/get-started/2020/technical-preview-2001-2#bkmk_pod-psh) <!--6104290-->
- [Exclude certain subnets for peer content download](/sccm/core/get-started/2020/technical-preview-2001-2#bkmk_subnet) <!--3555777-->
- [Send a smile improvements](/sccm/core/get-started/2020/technical-preview-2001-2#bkmk_sendsmile) <!--5891852-->
- [Improvements to task sequence as a deployment type](/sccm/core/get-started/2020/technical-preview-2001-2#bkmk_tsdt) <!--3555953-->
- [Improvements to Microsoft Edge Management dashboard](/sccm/core/get-started/2020/technical-preview-2001-2#bkmk_edge) <!--3871913-->
- [Improvements to cloud-connected services](/sccm/core/get-started/2020/technical-preview-2001-2#bkmk_cloud) <!--4963230, 4963383, 5566763-->
- [Additional improvement to task sequence progress](/sccm/core/get-started/2020/technical-preview-2001-2#bkmk_tsprogress) <!--2356386, 5932692-->

### Technical preview version 2001

- [Microsoft Edge management dashboard](/sccm/core/get-started/2020/technical-preview-2001#bkmk_edge-dash) <!--3871913-->
- [Improvements to orchestration groups](/sccm/core/get-started/2020/technical-preview-2001#bkmk_orch) <!--3098816-->
- [Improvements to Check Readiness task sequence step](/sccm/core/get-started/2020/technical-preview-2001#bkmk_tsready) <!--6005561-->
- [Integrate Power BI Report Server](/sccm/core/get-started/2020/technical-preview-2001#bkmk_powerbi) <!--3721603-->
- [OneTrace log groups](/sccm/core/get-started/2020/technical-preview-2001#bkmk_onetrace) <!--5559993-->
- [Improvements to administration service](/sccm/core/get-started/2020/technical-preview-2001#bkmk_rest) <!--5728365-->
- [Wake up a device from the central administration site](/sccm/core/get-started/2020/technical-preview-2001#bkmk_wake) <!--6030715-->
- [Improvements to task sequence progress](/sccm/core/get-started/2020/technical-preview-2001#bkmk_tsprogress) <!--5932692, fka 2356386-->

### Technical preview version 1912

- [Bootstrap a task sequence immediately after client registration](/sccm/core/get-started/2019/technical-preview-1912#bkmk_provisionts) <!--5526972-->
- [Expand Microsoft Defender Advanced Threat Protection (ATP) onboarding](/sccm/core/get-started/2019/technical-preview-1912#bkmk_atp) <!--5229962-->
- [New management insight rules from Microsoft Services](/sccm/core/get-started/2019/technical-preview-1912#bkmk_rules) <!--3607758-->
- [Client log collection](/sccm/core/get-started/2019/technical-preview-1912#client-log-collection) <!--4226618-->
- [Improvements to CMPivot](/sccm/core/get-started/2019/technical-preview-1912#improvements-to-cmpivot) <!--5870934-->
- [Improvements to OS deployment](/sccm/core/get-started/2019/technical-preview-1912#bkmk_osd) <!--5842295,5573175,5690481-->

> [!TIP]
> When a new current branch version is available, features that are available in that version are listed in the latest *What's new* article. For more information, see [What's new in incremental versions](/sccm/core/plan-design/changes/whats-new-incremental-versions#supported-versions).

## Features in previous technical previews

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

The following features were released with previous versions of the Configuration Manager technical preview branch. These features remain available in later versions, but aren't yet available in the current branch.

| Feature        | Technical preview version |
|----------------|---------------------------|
| Attach files to feedback <!--3556011--> | [Tech preview 1910](/sccm/core/get-started/2019/technical-preview-1910#attach-files-to-feedback) |
| Orchestration Groups <!--3098816--> | [Tech preview 1909](/sccm/core/get-started/2019/technical-preview-1909#bkmk_OGs) |
| Improvements to multicast-enabled distribution points <!--3785535--> | [Tech preview 1908.2](/sccm/core/get-started/2019/technical-preview-1908-2#bkmk_multicast) |
| Phased deployment templates <!--4961086--> | [Tech preview 1908](/sccm/core/get-started/2019/technical-preview-1908#phased-deployment-templates) |
| Remote control anywhere using cloud management gateway <!--4575930--> | [Tech Preview 1906](/sccm/core/get-started/2019/technical-preview-1906#remote-control-anywhere-using-cloud-management-gateway) |
| Improvements to Community Hub <!--3555935--> | [Tech Preview 1906](/sccm/core/get-started/2019/technical-preview-1906#bkmk_hub) |
| Task sequence as an app model deployment type <!--3555953--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdt) |
| Improvements to Community Hub <!--4224401--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_hub) |
| Community Hub and GitHub <!--3555935--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#community-hub-and-github) |
| Cloud services cost estimator <!--3555774--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_cmg) |
| Download reports from the Community Hub <!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Community Hub <!--3556020, fka 1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| Client-based PXE responder service <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| PXE network boot support for IPv6 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Use Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Improvements to Asset Intelligence <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## See also

For more information, see the following articles:

- [Evaluate Configuration Manager in a lab](/sccm/core/get-started/evaluate-with-lab-environment)
- [What's new in Configuration Manager incremental versions](/sccm/core/plan-design/changes/whats-new-incremental-versions)
- [Introduction to Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]
> For more information on current branch features that require consent to enable, see [pre-release features](/sccm/core/servers/manage/pre-release-features).
>
> For more information on current branch features that you must enable first, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).
