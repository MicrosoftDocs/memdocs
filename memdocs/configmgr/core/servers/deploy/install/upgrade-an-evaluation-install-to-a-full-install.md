---
title: Upgrade evaluation installs
titleSuffix: Configuration Manager
description: Learn how to upgrade an evaluation installation to a full installation of Configuration Manager.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Upgrade an evaluation installation of Configuration Manager to a full installation

*Applies to: Configuration Manager (current branch)*

If you installed Configuration Manager as an evaluation version, after 180 days the Configuration Manager console becomes read-only. You then need to activate the product from the **Site Maintenance** page in Setup. At any time before or after the 180-day period, you can upgrade to a full installation.

> [!NOTE]
> When you connect a Configuration Manager console to an evaluation installation of Configuration Manager, the window title bar displays the number of days that remain until it expires. The number of days in the window title doesn't automatically refresh. It only updates when you make a new connection to a site.

You can upgrade the following sites that run an evaluation installation:

- Central administration site (CAS)
- Primary site

Configuration Manager doesn't consider secondary sites as evaluation installations. So after you upgrade a primary parent site to a full installation, you don't need to modify a secondary site.

## Prerequisites

To upgrade an evaluation version to a licensed version, you need the following requirements:

- A valid product license key to use during the upgrade.

- **Administrator** rights on the site server.

## Process

1. On the site server, run **.\BIN\X64\Setup.exe** from the Configuration Manager installation folder. Use this copy of Setup because site maintenance options aren't available when you run Setup from source media.

1. On the **Before You Begin** page, select **Next**.

1. On the **Getting Started** page, select **Perform site maintenance or reset the Site**, and then select **Next**.

1. On the **Site Maintenance** page, select **Upgrade the evaluation edition to a licensed edition**. Then enter a valid product key, and select **Next**.

1. On the **Microsoft Software License Terms** page, read and accept the license terms, and then select **Next**.

1. On the **Configuration** page, select **Close** to complete the wizard.

> [!NOTE]
> Until you reconnect the console to the site, the title bar might indicate that the site is still an evaluation version.

## Next steps

[Configure sites and hierarchies](../configure/configure-sites-and-hierarchies.md)
