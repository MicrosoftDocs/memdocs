---
title: Technical preview 2401
titleSuffix: Configuration Manager
description: Learn about new features available in the Configuration Manager technical preview branch version 2401.
ms.date: 01/24/2024
ms.service: configuration-manager
ms.topic: conceptual
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ROBOTS: NOINDEX, NOFOLLOW
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Features in Configuration Manager technical preview version 2401

*Applies to: Configuration Manager (technical preview branch)*

This article introduces the features that are available in the technical preview for Configuration Manager, version 2401. Install this version to update and add new features to your technical preview site.<!-- baseline only statement: When you install a new technical preview site, this release is also available as a baseline version.-->

Review the [technical preview](../technical-preview.md) article before installing this update. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.

The following sections describe the new features to try out in this version:

<!-- [!INCLUDE [Example feature name](includes/2201/1234567.md)] -->
[!INCLUDE [Automated diagnostic Dashboard for Software Update Issues](includes/2401/17668422.md)]
[!INCLUDE [Introducing Centralized Search box: Effortlessly Find What You Need in the Console!](includes/2401/24501008.md)]
[!INCLUDE [Microsoft Azure Active Directory re-branded to Microsoft Entra ID](includes/2401/24269502.md)]
[!INCLUDE [Enhancement in Deploying Software Packages with Dynamic Variables](includes/2401/24334765.md)]
[!INCLUDE [Enabling Auto-Image Patching for CMG Virtual Machine Scale Sets](includes/2401/14350148.md)]
[!INCLUDE [Window 11 Readiness dashboard to support Windows 23H2](includes/2401/26021246.md)]
[!INCLUDE [HTTPS or Enhanced HTTP should be enabled for client communication from this version of Configuration Manager](includes/2401/25601199.md)]
[!INCLUDE [Upgrade to CM 2403 is blocked if CMG V1 is running as a cloud service (classic)](includes/2401/25990812.md)]
[!INCLUDE [Windows Server 2012/2012 R2 operating system site system roles are not supported from this version of Configuration Manager](includes/2401/9519162.md)]
[!INCLUDE [Improvements to Bitlocker](includes/2401/17667730.md)]
<!--17667730,21659899,26419721-->


## General known issues

Upgrading from TP 2311 to 2401 may encounter a prereq check failure if the Resource Access slider is already in Intune. This regression is caused by the previous TP. To resolve this issue, follow these steps:

   - Move any other slider (Apps/Endpoint) to Configuration Manager (CM) or Intune.
   - Choose to apply the changes and click 'Ok.'
   - Proceed with upgrading the site to TP 2401.
   - Once the upgrade is complete, you can revert the (Apps/Endpoint) slider back to its old settings."

<!--## Other Updates-->



## Next steps

For more information about installing or updating the technical preview branch, see [Technical preview](../technical-preview.md).

For more information about the different branches of Configuration Manager, see [Which branch of Configuration Manager should I use?](../../understand/which-branch-should-i-use.md).

