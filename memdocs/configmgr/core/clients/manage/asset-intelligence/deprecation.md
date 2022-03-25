---
title: Asset intelligence deprecation
titleSuffix: Configuration Manager
description: More information about the deprecation of the asset intelligence feature of Configuration Manager.
ms.date: 03/28/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.localizationpriority: medium
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Asset intelligence deprecation

*Applies to: Configuration Manager (current branch)*

Starting in November 2021, the asset intelligence feature of Configuration Manager is [deprecated](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 12454890 --> This article provides more detail about the specific functional areas of asset intelligence that are deprecated or still supported.

## Deprecated functionality

The following functional areas are deprecated and may be removed in a future version. Support for these areas will end November 2022.

- The [asset intelligence catalog](introduction-to-asset-intelligence.md#BKMK_AssetIntelligenceCatalog), which includes the following functionality:

  - Cloud updates to the predefined software title information such as product name and vendor

  - Cloud updates to the predefined [software categories](introduction-to-asset-intelligence.md#BKMK_SoftwareCategories) and [software families](introduction-to-asset-intelligence.md#BKMK_SoftwareFamilies) and the associated SQL views and reports

  - Cloud updates to the predefined [hardware requirements](introduction-to-asset-intelligence.md#BKMK_HardwareRequirements) for software titles and the associated SQL views and reports

- The [asset intelligence synchronization point](introduction-to-asset-intelligence.md#AssetIntelligenceSycnronizationPoint), which includes the following functionality:

  - Catalog synchronization

  - The ability to [request catalog updates](operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate) for uncategorized software

- The [Microsoft Volume License import and reconciliation](configuring-asset-intelligence.md#BKMK_ImportSoftwareLicenseInformation) including the associated SQL views and reports

## Supported functionality

The following functional areas aren't currently included in the deprecation and will remain supported:

- The [inventoried software titles](introduction-to-asset-intelligence.md#BKMK_InventoriedSoftwareTitles), which includes the following functionality:

  - [Asset intelligence hardware inventory reporting WMI classes](../../../../develop/reference/core/clients/client-classes/asset-intelligence-client-wmi-classes.md)

  - The associated SQL views:

    - [Asset intelligence hardware inventory views](../../../../develop/core/understand/sqlviews/asset-intelligence-views-configuration-manager.md#asset-intelligence-hardware-inventory-views)

    - [Asset intelligence status view](../../../../develop/core/understand/sqlviews/asset-intelligence-views-configuration-manager.md#asset-intelligence-status-view)

  - The associated reports

- The [product lifecycle dashboard](product-lifecycle-dashboard.md) and its associated reports

- The [General License Statement import and reconciliation](configuring-asset-intelligence.md#BKMK_CreateGeneralLicenseStatement) and the associated SQL views and reports

- The ability to view the asset intelligence inventory in the console from the **Inventoried Software** node

- The existing static, predefined software title information provided with setup for new and existing sites:

  - Product name
  - Vendor
  - Product category
  - Product family
  - Hardware requirement

- The ability to customize the inventoried software title information such as the product name and vendor

- The ability to add custom software categories, families, and labels to inventoried software titles

- The ability for an administrator to add custom hardware requirements to inventoried software titles

## References

[Asset intelligence reports](../../../servers/manage/list-of-reports.md#asset-intelligence)

[Asset intelligence client WMI classes](../../../../develop/reference/core/clients/client-classes/asset-intelligence-client-wmi-classes.md)

[Asset intelligence views](../../../../develop/core/understand/sqlviews/asset-intelligence-views-configuration-manager.md)
