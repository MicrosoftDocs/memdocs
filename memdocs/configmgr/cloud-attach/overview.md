---
title: Cloud attach overview
titleSuffix: Configuration Manager
description: Cloud attach for Configuration Manager overview
ms.date: 12/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: high
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Cloud attach your Configuration Manager environment
<!--9251060-->
*Applies to: Configuration Manager (current branch)*

Attaching your Configuration Manager environment to the cloud allows you to continue to modernize and streamline your management solution. Cloud attach allows you to transform your existing environment without having to worry about much disruption or risk. A Configuration Manager environment is considered cloud attached when it uses at least one of the three primary cloud attach features. You can enable these three features in any order you wish, or all at once.

- [Tenant attach](#tenant-attach)
- [Endpoint analytics](#endpoint-analytics)
- [Co-management](#co-management)

## Tenant attach

Tenant attach provides immediate value by having your device records in the cloud and being able to take actions on these devices from the cloud-based console. You can get real-time data from Configuration Manager clients including clients connected from the internet. When you upload your clients to Microsoft Intune admin center, some of the features you may want to use include:

- Run PowerShell [scripts](../tenant-attach/scripts.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- Install [applications](../tenant-attach/applications.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- Query devices with [CMPivot](../tenant-attach/cmpivot-samples-attached.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- Display a [timeline](../tenant-attach/timeline.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) of events from the device

## Endpoint analytics

Endpoint analytics gives you insights for measuring the quality of the experience you're delivering to your users. Endpoint analytics can help identify policies or hardware issues that may be slowing down devices and help you proactively make improvements before end users generate a help desk ticket. Each of the reports provides scores for your organization's user experience. There are built-in baseline scores for the median of all other organizations, which allows you to compare your scores to a typical enterprise. You'll be given **Insights and recommendations** for improving your organization's user experience and your score. Endpoint analytics includes the following reports:

- [Work from anywhere](../../analytics/work-from-anywhere.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- [Startup performance](../../analytics/startup-performance.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- [Application reliability](../../analytics/app-reliability.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)

## Co-management

Co-management transforms your on-premises Configuration Manager environment without having to go through a large migration effort. Co-management helps simplify device management by giving you the ability to manage workloads from the cloud. You can specify which workloads to move, such as compliance policy to enable Conditional Access. [Conditional Access](../comanage/quickstart-conditional-access.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) combines granular control over organizational data while maintaining a consistent user experience on any device from any location. Enforcing compliance policy from Intune is a critical part of developing your [Zero Trust](/security/zero-trust/) architecture. Use [Windows Autopilot](../../autopilot/windows-autopilot.md) with co-management to simplify the complex process of provisioning devices from the cloud.  

## <a name="bkmk_cmg"></a> Cloud management gateway (CMG)

[Cloud management gateway (CMG)](../core/clients/manage/cmg/overview.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json) is an additional cloud feature that allows you to manage internet-based clients using your established workflows and processes. CMG helps minimize the management traffic from Configuration Manager to clients through your VPN. When you enable CMG, you maintain a connection to your devices wherever they are on the internet. This connection enables you to keep up with your usual software deployments, device configuration, and software updates processes for internet clients without having to make large infrastructure investments.

## Next steps

[Enable cloud attach](enable.md)
