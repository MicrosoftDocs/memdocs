---
title: Cloud attach overview
titleSuffix: Configuration Manager
description: Cloud attach for Configuration Manager overview
ms.date: 11/19/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: high
---

# Cloud attach your Configuration Manager environment
<!--9251060-->
*Applies to: Configuration Manager (current branch)*

Attaching your Configuration Manager environment the cloud allows you to continue to modernizing and streamlining your management solution. Cloud attach allows you to transform your existing environment without having to worry about much disruption or risk. A Configuration Manager environment is considered cloud attached when it uses at least one of the three primary cloud attach features. You can enable these three features in any order you wish, or all at once.  

- [Tenant attach](#tenant-attach)
- [Endpoint analytics](#endpoint-analytics)
- [Co-management](#co-management)

[Cloud management gateway (CMG)](#bkmk_cmg) is an additional cloud feature that allows you to manage internet-based clients using your established workflows and processes. CMG helps minimize client management traffic through your VPN so that bandwidth is free for business critical traffic.

## Tenant attach

Tenant attach provides immediate value by having your device records in the cloud and being able to take actions on these devices from the cloud-based console. You can get real-time data from Configuration Manager clients including clients connected from the internet. When you upload your clients to Microsoft Endpoint Manager admin center, some of the features you may want to use include:

- Run PowerShell [scripts](../tenant-attach/scripts.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- Install [applications](../tenant-attach/applications.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- Query devices with [CMPivot](../tenant-attach/cmpivot-samples-attached.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- Display a [timeline](../tenant-attach/timeline.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) of events from the device

## Endpoint analytics

Endpoint analytics gives you insights for measuring the quality of the experience you're delivering to your users. Endpoint analytics can help identify policies or hardware issues that may be slowing down devices and help you proactively make improvements before end users generate a help desk ticket. Each of the reports provides scores for your organization's user experience. There are built-in baseline scores for the median of all other organizations, which allows you to compare your scores to a typical enterprise. You'll be given **Insights and recommendations** for improving your score. Endpoint analytics includes the following reports:

- [Work from anywhere](../../analytics/work-from-anywhere.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- [Startup performance](../../analytics/startup-performance.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- [Application reliability](../../analytics/app-reliability.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)

## Co-management

## <a name="bkmk_cmg"></a> Cloud management gateway (CMG)
