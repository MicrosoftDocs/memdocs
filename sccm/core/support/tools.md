---
title: Configuration Manager Tools
titleSuffix: Configuration Manager
description: Learn about the tools to help you manage and troubleshoot your Configuration Manager infrastructure.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
---

# Configuration Manager Tools

*Applies to: Configuration Manager (current branch)*

The Configuration Manager tools include [client-based](#client-tools) and [server-based tools](#server-tools). Use these tools to help support and troubleshoot your Configuration Manager infrastructure.

Starting in Configuration Manager version 1806, these tools are included in the `CD.Latest\SMSSETUP\Tools` folder on the site server. No further installation is required.<!--1357145--> Use these versions of the tools with Configuration Manager version 1806 and later.

All Windows operating systems listed as supported clients in [Supported operating systems for clients and devices](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) are supported for use with these tools.

> [!Note]  
> The [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012) is still available from the Microsoft Download Center. For Configuration Manager version 1806 and later, use the versions of the tools in the CD.Latest folder on the site server. Some tools were formerly in the toolkit but not included in version 1806. These legacy tools are no longer supported.


## Client tools

These tools are in the `ClientTools` subfolder:

- [CMTrace](cmtrace.md): View, monitor, and analyze Configuration Manager log files  

- [Client Spy](clispy.md): Troubleshoot issues related to software distribution, inventory, and metering

- [Deployment Monitoring Tool](deployment-monitoring-tool.md): Troubleshoot applications, updates, and baseline deployments  

- [Policy Spy](policy-spy.md): View policy assignments  

- [Power Viewer Tool](power-viewer-tool.md): View status of power management feature  

- [Send Schedule Tool](send-schedule-tool.md): Trigger schedules and evaluations of configuration baselines  

> [!Note]  
> The `ClientTools` folder also includes the file Microsoft.Diagnostics.Tracing.EventSource.dll. Several client tools require this library. You can't directly use it.  


## Server tools

These tools are in the `ServerTools` subfolder:

- [DP Job Queue Manager](dp-job-manager.md): Troubleshoots content distribution jobs to distribution points  

- [Collection Evaluation Viewer](ceviewer.md): View collection evaluation details  

- [Content Library Explorer](content-library-explorer.md): View contents of the content library single instance store  

- [Content Library Transfer](content-library-transfer.md): Transfers content library between drives  

- [Content Ownership Tool](content-ownership-tool.md): Changes ownership of orphaned packages. These packages exist in the site without an owning site server.

- [Role-based Administration and Auditing Tool](rbaviewer.md): Helps administrators audit roles configuration  

- [Run Meter Summarization Tool](run-meter-summ.md): Run metering summarization task and analyze metering data

> [!Note]  
> The ServerTools folder also includes the following files:
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> Several server tools require these libraries. You can't directly use them.  

## Other tools and toolkits

- [Support Center](support-center.md): Gather information from clients for easier analysis when troubleshooting.

    Starting in version 1906, **OneTrace** is a new log viewer with Support Center. It works similarly to CMTrace, with improvements. For more information, see [Support Center OneTrace](support-center-onetrace.md).

- [Extend and migrate on-premises site to Microsoft Azure](azure-migration-tool.md): Helps you to programmatically create Azure virtual machines (VMs) for Configuration Manager. <!--3556022--> 

- [Content library cleanup tool](../plan-design/hierarchy/content-library-cleanup-tool.md): Use **ContentLibraryCleanup.exe** in `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` to remove orphaned content from a distribution point.  

- [Hierarchy Maintenance Tool](../../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): Use **Preinst.exe** in the `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` shared folder on the site server to pass commands to the hierarchy manager component.  

- [Update reset tool](../servers/manage/update-reset-tool.md): Use **CMUpdateReset.exe** in `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` to fix issues when in-console updates have problems downloading or replicating.  

- [Service Connection Tool](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): Use **ServiceConnectionTool.exe** in `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` to keep your site up-to-date when your service connection point is offline.   

- [Microsoft Deployment Toolkit (MDT)](../../mdt/use-the-mdt.md): A collection of tools, processes, and guidance for automating desktop and server OS deployments.

- [System Center Updates Publisher (SCUP)](../../sum/tools/updates-publisher.md): A stand-alone tool to manage and import custom software updates.

- [Package Conversion Manager](../../apps/pcm/package-conversion-manager.md): Convert legacy packages into applications.
