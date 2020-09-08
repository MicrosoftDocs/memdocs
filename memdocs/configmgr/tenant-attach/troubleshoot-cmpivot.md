---
title: Troubleshoot CMPivot for devices uploaded to the admin center
titleSuffix: Configuration Manager
description: "Troubleshooting CMPivot for Configuration Manager tenant attach"
ms.date: 09/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 86f97154-c9fc-4efd-9d49-4a253cef5953
manager: dougeby
author: mestew
ms.author: mstewart
---

# Troubleshoot CMPivot for devices uploaded to the admin center (preview)
<!--6024392-->
*Applies to: Configuration Manager (current branch)*

Use the following to troubleshoot CMPivot in the Microsoft Endpoint Manager admin center:

> [!Important]
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

## Common issues






## Known issues

### Inconsistent results for some operators with Configuration Manager version 2002
<!--7784718, 7884272-->
When using CMPivot from the Microsoft Endpoint Manager admin center with Configuration Manager version 2002, you may get inconsistent results for the following operators:

- Summarize by
- Take
- Order by
- Top
- Count
- Distinct

**Resolution**: Install [KB4578123 - CMPivot queries return unexpected results in Configuration Manager current branch, version 2002](https://support.microsoft.com/help/4578123).

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## Next steps

[Troubleshoot tenant attach](troubleshoot.md)
