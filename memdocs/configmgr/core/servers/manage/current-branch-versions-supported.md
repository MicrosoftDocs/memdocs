---
title: Current branch versions
titleSuffix: Configuration Manager
description: Review the Configuration Manager version history, and learn about the phases of service offered.
ms.date: 04/08/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Support for Configuration Manager current branch versions

*Applies to: Configuration Manager (current branch)*

Microsoft plans to release updates for Configuration Manager current branch a few times per year. Each update version remains in support for 18 months from its general availability release date. Microsoft provides technical support for the entire period of support. There are two distinct servicing phases that depend on the availability of the latest current branch version:

- **Security and Critical Updates** servicing phase - When running the latest current branch version of Configuration Manager, you receive both Security and Critical Updates.

- **Security Updates (Only)** servicing phase - After the release of a new current branch version, Microsoft only supports security updates to older versions for the remainder of that version's support lifecycle.

> [!NOTE]
> The latest current branch version is always in the **Security and Critical Updates** servicing phase. This support statement means that if you encounter a code defect that warrants a critical update, you must have the latest current branch version installed in order to receive a fix. All other supported current branch versions are eligible to receive only security updates.
>
> All support ends after the 18-month lifecycle has expired for a current branch version.
>
> Update your Configuration Manager environment to the latest version before support for your current version expires.

For example, version 2203 releases in April 2022. Microsoft provides security and critical updates to that version for four months, through July 2022. It then switches to only security updates for the remaining 14 months of its support lifecycle, through September 2023.

> [!NOTE]
> A **Critical Update** specifies a widely released fix for a specific problem that addresses a critical, non-security-related bug. Security updates provide a severity rating for the updates, which includes the **Critical** rating. For more information about each, see [update classifications](/mem/configmgr/sum/get-started/configure-classifications-and-products#to-configure-classifications-and-products-to-synchronize) and [Security update severity](/troubleshoot/windows-client/installing-updates-features-roles/standard-terminology-software-updates#security-update)

For a list of the current branch versions, see [Version details](updates.md#version-details).

For more information about version numbers, and availability as an in-console update or as a baseline, see [Baseline and update versions](updates.md#bkmk_Baselines).
