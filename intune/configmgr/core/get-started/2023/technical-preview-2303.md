---
title: Technical preview 2303
titleSuffix: Configuration Manager
description: Learn about new features available in the Configuration Manager technical preview branch version 2303.
ms.date: 03/17/2023
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: whats-new
author: LauraWi
ms.author: laurawi
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart
---

# Features in Configuration Manager technical preview version 2303

*Applies to: Configuration Manager (technical preview branch)*

This article introduces the features that are available in the technical preview for Configuration Manager, version 2303. Install this version to update and add new features to your technical preview site.<!-- baseline only statement: When you install a new technical preview site, this release is also available as a baseline version.-->

Review the [technical preview](../technical-preview.md) article before installing this update. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.

The following sections describe the new features to try out in this version:

<!-- [!INCLUDE [Example feature name](includes/2201/1234567.md)] -->

[!INCLUDE [SQL Server 2022 version support added for Configuration Manager](includes/2303/17276757.md)]
[!INCLUDE [Dark theme extended to one customer voice(OCV) wizard](includes/2303/17433655.md)]
[!INCLUDE [Prerequisites for the site server roles now include ODBC driver for SQL Server](includes/2303/9081772.md)]

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


