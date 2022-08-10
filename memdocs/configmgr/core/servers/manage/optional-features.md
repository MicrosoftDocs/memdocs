---
title: Optional features
titleSuffix: Configuration Manager
description: Updates to Configuration Manager include optional features, which you have to enable before use.
ms.date: 08/12/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: paasin
ms.author: paasin
manager: apoorvseth
ms.localizationpriority: medium
---

# Optional features in Configuration Manager

*Applies to: Configuration Manager (current branch)*

When an update includes one or more optional features, you can enable those features in your hierarchy. Enable features when the update installs, or return to the console later to enable the optional features.

To view available features and their status, in the console go to the **Administration** workspace, expand **Updates and Servicing**, and select the **Features** node. To enable a feature, select it in the list, and then select **Turn on** in the ribbon.

Your user account requires permissions to view and enable optional features. For more information, see [Permissions for in-console updates](prepare-in-console-updates.md#permissions).

When a feature isn't optional, it's automatically available for use. It doesn't appear in the **Features** node.

> [!IMPORTANT]
> In a multi-site hierarchy, enable optional or pre-release features only from the central administration site (CAS). This behavior makes sure there are no conflicts across the hierarchy.<!--507197-->

When you enable a new feature or pre-release feature, the Configuration Manager hierarchy manager (HMAN) must process the change before that feature becomes available. Processing of the change is often immediate. Depending on the HMAN processing cycle, it can take up to 30 minutes to complete. After the change is processed, restart the console before you can use the feature.

When new cloud-based features are available in the Microsoft Endpoint Manager admin center, or other attached cloud services for your on-premises Configuration Manager installation, you can opt in to these new features in the Configuration Manager console.<!--5834830-->

## List of optional features

The following features are optional in the latest version of Configuration Manager:<!--505213-->

<!--Note to include in target articles

> [!NOTE]
> Configuration Manager doesn't enable this optional feature by default. Before using it, you need to enable this feature. For more information, see [Enable optional features from updates](optional-features.md).

-->
<!-- Optional features means status = off in console-->

- [Remove the central administration site](../deploy/install/remove-central-administration-site.md) <!-- 3607277 -->
- [BitLocker management](../../../protect/plan-design/bitlocker-management.md) <!-- 3601034,6DD56E46-C3EC-4E38-A16F-E98644BB6434 -->
- [Application groups](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D-->

> [!TIP]
> For more information on features that require consent to enable, see [pre-release features](pre-release-features.md).
>
> For more information on features that are only available in the technical preview branch, see [Technical Preview](../../get-started/technical-preview.md).

## Next steps

The current branch includes pre-release features for early testing in a production environment. For more information, see [pre-release features](pre-release-features.md).

For answers to common questions, see [In-console updates FAQ](updates-faq.yml).
