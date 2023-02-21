---
title: Technical preview 2302
titleSuffix: Configuration Manager
description: Learn about new features available in the Configuration Manager technical preview branch version 2302.
ms.date: 02/22/2023
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Features in Configuration Manager technical preview version 2302

*Applies to: Configuration Manager (technical preview branch)*

This article introduces the features that are available in the technical preview for Configuration Manager, version 2302. Install this version to update and add new features to your technical preview site.<!-- baseline only statement: When you install a new technical preview site, this release is also available as a baseline version.-->

Review the [technical preview](../technical-preview.md) article before installing this update. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.

The following sections describe the new features to try out in this version:

<!-- [!INCLUDE [Example feature name](includes/2201/1234567.md)] -->

[!INCLUDE [Dark theme extended to delete secondary site wizard](includes/2302/15942599.md)]
[!INCLUDE [Enable Windows features introduced via Windows servicing that are off by default](includes/2302/16834520.md)]

<!--## General known issues-->
<!--16822959-->
<!--Update to the default value of supersedence age in months for software updates.-->

<!--Removing SUP role in Admin Console does not reset the supersedence age property in WMI. As a result, while reconfiguring the role, the previously configured value is shown in the configuration window. This property needs to be reset to default value on role removal.-->
<!--  [!INCLUDE [11018755](includes/2112/known-issue-11018755.md)] -->
<!--## Other Updates
<!--15358429-->
<!--Offset for recurring monthly maintenance window schedules.-->
<!--Based upon your feedback, you can now offset monthly maintenance window schedules to better align deployments with the release of monthly security updates. For example, using a maximum offset of seven days after the second Tuesday of the month, sets the maintenance window for next Monday.-->  

## Next steps

For more information about installing or updating the technical preview branch, see [Technical preview](../technical-preview.md).

For more information about the different branches of Configuration Manager, see [Which branch of Configuration Manager should I use?](../../understand/which-branch-should-i-use.md).


