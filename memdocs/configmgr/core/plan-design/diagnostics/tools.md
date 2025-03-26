---
title: Diagnostic usage data for tools
titleSuffix: Configuration Manager
description: Learn about the diagnostics and usage data that Configuration Manager collects for its tools.
ms.date: 08/10/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: article
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Diagnostic usage data for tools

*Applies to: Configuration Manager (current branch)*

<!-- 9760004 -->

Some of the tools that are included with Configuration Manager collect usage data. Microsoft uses this data to improve the quality of these tools, and better understand customer usage. Microsoft collects data for the following Configuration Manager tools:

- Client tools
- Server tools
- Support Center
- CMTrace

For more general information about these tools, see [Configuration Manager Tools](../../support/tools.md).

> [!NOTE]
> The **ConfigurationManager** PowerShell module also collects usage data. For more information, see [Configuration Manager cmdlet library privacy statement](/powershell/sccm/privacy-statement).

The following data is collected for these tools:

- Version
- Start and stop times to calculate duration of use

Because these tools can run on any Windows device, they all use the Windows diagnostic data channel. They don't rely on Configuration Manager diagnostic data collection. The device on which the tool runs needs to be configured for at least **Optional** diagnostic data. If you configure the device for any other setting, Windows won't collect data for these Configuration Manager tools. For more information on these Windows diagnostic data levels, see the following articles:

- [Windows 10, version 1709 and newer optional diagnostic data](/windows/privacy/windows-diagnostic-data)
- [Configure Windows diagnostic data in your organization](/windows/privacy/configure-windows-diagnostic-data-in-your-organization)

Next, see the frequently asked questions about diagnostic and usage data for Configuration Manager:

> [!div class="nextstepaction"]
> [Frequently asked questions](frequently-asked-questions.yml)
