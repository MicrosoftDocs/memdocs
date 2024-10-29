---
title: Pre-release features
titleSuffix: Configuration Manager
description: Pre-release features are features that are in the current branch for early testing in a production environment.
ms.date: 12/05/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: PalikaSingh
ms.author: Palsi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Pre-release features in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Pre-release features are features that are in the current branch for early testing in a production environment. These features are fully supported, but still in active development. They might receive changes until they move out of the pre-release category.

## Give consent

Before using pre-release features, give consent to use pre-release features. Giving consent is a one-time action per hierarchy that you can't undo. Until you give consent, you can't enable new pre-release features included with updates. After you turn on a pre-release feature, you can't turn it off.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

2. In the ribbon, select **Hierarchy Settings**.

3. On the **General** tab of Hierarchy Settings Properties, enable the option to **Consent to use pre-release features**.

## Enable pre-release features

When you install an update that includes pre-release features, those features are visible in the Updates and Servicing Wizard with the regular features included in the update.

### If consent is given

In the Updates and Servicing Wizard, enable pre-release features. Select the pre-release features as you would any other feature.

Optionally, wait to enable pre-release features later from the **Features** node under **Updates and Servicing** in the **Administration** workspace. Select a feature, and then select **Turn on** in the ribbon. Until you give consent, this option isn't available for use.

### If you haven't given consent

In the Updates and Servicing Wizard, pre-release features are visible but you can't enable them. After the update is installed, these features are visible in the **Features** node. However, you can't enable them until you give consent.

> [!IMPORTANT]
> In a multi-site hierarchy, you can only enable optional or pre-release features from the central administration site. This behavior ensures there are no conflicts across the hierarchy. <!--507197-->
>
> If you gave consent at a stand-alone primary site, and then expand the hierarchy by installing a new central administration site, you must give consent again at the central administration site.

When you enable a pre-release feature, the Configuration Manager hierarchy manager (HMAN) must process the change before that feature becomes available. Processing of the change is often immediate. Depending on the HMAN processing cycle, it can take up to 30 minutes to complete. After the change is processed, restart the console before using the feature.

## List of pre-release features

<!--Note/tip for target article

> [!NOTE]
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](pre-release-features.md).

> [!TIP]
> This feature was first introduced in version 1702 as a [pre-release feature](pre-release-features.md). Beginning with version 1906, it's no longer a pre-release feature.

-->

<!-- With each current branch release, to help purge this list a bit, remove any entries that were added as a full feature in a version that's no longer supported -->
| Feature          | Added as pre-release | Added as a full feature |
|------------------|----------------------|-------------------------|
| [Cloud management gateway with virtual machine scale set](../../clients/manage/cmg/plan-cloud-management-gateway.md#virtual-machine-scale-sets) <!--3601040,8959690--> | Version 2010 | Version 2107 |
| [Orchestration groups](../../../sum/deploy-use/orchestration-groups.md) <!--3098816,290B66D8-C735-4895-B59A-DD732D84A697--> | Version 2002 | Version 2111 |
| [Task sequence deployment type](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!--3555953,CB0CDFFB-9C6F-4B18-8954-A43A387302A2--> | Version 2002 | ![Not yet](media/red-x.png) |
| [Task sequence debugger](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71--> | Version 1906 | Version 2203 |
| [Application groups](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D--> | Version 1906 | Version 2111 |

<!--Image used = ![Not yet](media/red-x.png) -->

> [!TIP]
> For more information on non-pre-release features that you must enable first, see [Enable optional features from updates](optional-features.md).
>
> For more information on features that are only available in the technical preview branch, see [Technical Preview](../../get-started/technical-preview.md).
