---
title: Troubleshoot scripts for devices uploaded to the admin center
titleSuffix: Configuration Manager
description: "Troubleshooting scripts for Configuration Manager tenant attach"
ms.date: 09/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: a0eb1e8f-2c85-4f48-a0b5-945b3e5f63f3
manager: dougeby
author: mestew
ms.author: mstewart
---

# Troubleshoot scripts (preview) for devices uploaded to the admin center
<!--6024392-->
*Applies to: Configuration Manager (current branch)*

Use the following to troubleshoot scripts in the Microsoft Endpoint Manager admin center:

> [!Important]
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

## Common issues

### <a name="bkmk_version"></a> Configuration Manager doesn't meet the minimum version prerequisite

**Error message:** Configuration Manager doesn't meet the minimum version prerequisite.

**Possible causes:** Your Configuration Manager sites are not running the minimum version of Configuration Manager 2006 with [KB4580678 - Tenant attach rollup for Configuration Manager current branch, version 2006](https://support.microsoft.com/help/4580678) installed. Verify the following:
 - Configuration Manager version 2006 or higher is installed.
 - That [KB4580678](https://support.microsoft.com/help/4580678) on sites running Configuration Manager version 2006.
 - That every site in the hierarchy meets the minimums listed above.

## Known issues

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]
