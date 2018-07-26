---
title: Configuration Manager Tools
titleSuffix: Configuration Manager
description: Learn about the tools to help you manage and troubleshoot your Configuration Manager infrastructure.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Configuration Manager Tools

*Applies to: System Center Configuration Manager (Current Branch)*

The Configuration Manager tools include [client-based](#client-tools) and [server-based tools](#server-tools). Use these tools to help support and troubleshoot your Configuration Manager infrastructure. 

Starting in Configuration Manager version 1806, these tools are included in the `CD.Latest\SMSSETUP\Tools` folder on the site server. No further installation is required.<!--1357145--> Use these versions of the tools with Configuration Manager version 1806 and later.

All Windows operating systems listed as supported clients in [Supported operating systems for clients and devices](https://docs.microsoft.com/en-us/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) are supported for use with these tools.

> [!Note]  
> The [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=50012) is still available from the Microsoft Download Center. For Configuration Manager version 1806 and later, use the versions of the tools in the CD.Latest folder on the site server. Some tools were formerly in the toolkit but not included in version 1806. These legacy tools are no longer supported.


## Client tools

- [CMTrace](/sccm/core/support/cmtrace): View, monitor, and analyze Configuration Manager log files  

- [Client Spy](/sccm/core/support/clispy): Troubleshoot issues related to software distribution, inventory, and metering

- [Deployment Monitoring Tool](/sccm/core/support/deployment-monitoring-tool): Troubleshoot applications, updates, and baseline deployments  

- [Policy Spy](/sccm/core/support/policy-spy): View policy assignments  

- [Power Viewer Tool](/sccm/core/support/power-viewer-tool): View status of power management feature  

- [Send Schedule Tool](/sccm/core/support/send-schedule-tool): Trigger schedules and evaluations of configuration baselines  

> [!Note]  
> The ClientTools folder also includes the file Microsoft.Diagnostics.Tracing.EventSource.dll. Several client tools require this library. You can't directly use it.  


## Server tools

- [DP Job Queue Manager](/sccm/core/support/dp-job-manager): Troubleshoots content distribution jobs to distribution points  

- [Collection Evaluation Viewer](/sccm/core/support/ceviewer): View collection evaluation details  

- [Content Library Explorer](/sccm/core/support/content-library-explorer): View contents of the content library single instance store  

- [Content Library Transfer](/sccm/core/support/content-library-transfer): Transfers content library between drives  

- [Content Ownership Tool](/sccm/core/support/content-ownership-tool): Changes ownership of orphaned packages. These packages exist in the site without an owning site server.  

- [Role-based Administration and Auditing Tool](/sccm/core/support/rbaviewer): Helps administrators audit roles configuration  

- [Run Meter Summarization Tool](/sccm/core/support/run-meter-summ): Run metering summarization task and analyze metering data

> [!Note]  
> The ServerTools folder also includes the following files 
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll. 
>
> Several server tools require these libraries. You can't directly use them.  



## Other tools

- [Content library cleanup tool](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool): Use **ContentLibraryCleanup.exe** in `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` to remove orphaned content from a distribution point.  

- [Hierarchy Maintenance Tool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe): Use **Preinst.exe** in the `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` shared folder on the site server to pass commands to the hierarchy manager component.  

- [Update reset tool](/sccm/core/servers/manage/update-reset-tool): Use **CMUpdateReset.exe** in `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` to fix issues when in-console updates have problems downloading or replicating.  

- [Service Connection Tool](/sccm/core/servers/manage/use-the-service-connection-tool): Use **ServiceConnectionTool.exe** in `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` to keep your site up-to-date when your service connection point is offline.  
