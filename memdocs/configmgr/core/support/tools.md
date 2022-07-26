---
title: Configuration Manager Tools
titleSuffix: Configuration Manager
description: Learn about the tools to help you manage and troubleshoot your Configuration Manager infrastructure.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Configuration Manager Tools

*Applies to: Configuration Manager (current branch)*

The Configuration Manager tools primarily include [client-based](#client-tools) and [server-based tools](#server-tools). Use these tools to help support and troubleshoot your Configuration Manager infrastructure.

These tools are included in the `CD.Latest\SMSSETUP\Tools` folder on the site server. No further installation is required.<!--1357145--> Use these versions of the tools with supported versions of Configuration Manager current branch.

All Windows operating systems listed as supported clients in [Supported operating systems for clients and devices](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) are supported for use with these tools.

> [!NOTE]
> The System Center 2012 R2 Configuration Manager Toolkit is still available from the Microsoft Download Center. For supported versions of Configuration Manager current branch, use the versions of the tools in the CD.Latest folder on the site server. Some tools were formerly in the toolkit but not included current branch. These legacy tools are no longer supported.

## Client tools

These tools are in the `ClientTools` subfolder:

- [Client Spy](clispy.md): Troubleshoot issues related to software distribution, inventory, and metering

- [Deployment Monitoring Tool](deployment-monitoring-tool.md): Troubleshoot applications, updates, and baseline deployments

- [Policy Spy](policy-spy.md): View policy assignments

- [Power Viewer Tool](power-viewer-tool.md): View status of power management feature

- [Send Schedule Tool](send-schedule-tool.md): Trigger schedules and evaluations of configuration baselines

> [!NOTE]
> The `ClientTools` folder also includes the file Microsoft.Diagnostics.Tracing.EventSource.dll. Several client tools require this library. You can't directly use it.

## Server tools

These tools are in the `ServerTools` subfolder:

- [DP Job Queue Manager](dp-job-manager.md): Troubleshoots content distribution jobs to distribution points

- [Collection Evaluation Viewer](ceviewer.md): View collection evaluation details

  > [!IMPORTANT]
  > Starting in Configuration Manager version 2103, this standalone tool isn't supported.<!-- 8509484 --> The tool is no longer included with the Configuration Manager installation source. Starting in version 2010, its functionality is built-in to the console. For more information, see, [How to view collection evaluation](../clients/manage/collections/collection-evaluation-view.md).

- [Content Library Explorer](content-library-explorer.md): View contents of the content library single instance store

- [Content Library Transfer](content-library-transfer.md): Transfers content library between drives

- [Content Ownership Tool](content-ownership-tool.md): Changes ownership of orphaned packages. These packages exist in the site without an owning site server.

- [Role-based Administration and Auditing Tool](rbaviewer.md): Helps administrators audit roles configuration

  > [!NOTE]
  > Starting in version 2107, RBAViewer has moved from `<installdir>\tools\servertools\rbaviewer.exe`. It's now located in the Configuration Manager console directory. After you install the console, RBAViewer.exe will be in the same directory. The default location is `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\rbaviewer.exe`.<!--9579789-->

- [Run Meter Summarization Tool](run-meter-summ.md): Run metering summarization task and analyze metering data

> [!NOTE]
> The ServerTools folder also includes the following files:
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> Several server tools require these libraries. You can't directly use them.

## More tools in the folder

The following tools are in the `CD.Latest\SMSSETUP\TOOLS` folder on the site server:

- [CMTrace](cmtrace.md): View, monitor, and analyze Configuration Manager log files.

- [CMPivot](../servers/manage/cmpivot.md): Use the standalone version of this tool to query real-time data from clients.

- [Update reset tool](../servers/manage/update-reset-tool.md): Fix issues when in-console updates have problems downloading or replicating.

- [Configuration Manager group policy administrative template](../clients/deploy/deploy-clients-to-windows-computers.md#configure-and-assign-client-installation-properties-by-using-a-group-policy-object): Configure and assign client installation properties by using a group policy object.

- [Content library cleanup tool](../plan-design/hierarchy/content-library-cleanup-tool.md): Remove orphaned content from a distribution point.

- [Desktop Analytics log collector](../../desktop-analytics/log-collector.md): Helps to troubleshoot Desktop Analytics device enrollment issues.

- [Extend and migrate on-premises site to Microsoft Azure](azure-migration-tool.md): Helps you to programmatically create Azure virtual machines (VMs) for Configuration Manager. <!--3556022-->

- [Synchronize Microsoft 365 Apps updates from a disconnected software update point](../../sum/get-started/synchronize-office-updates-disconnected.md) (OfflineUpdateExporter): Import Microsoft 365 Apps updates from an internet connected WSUS server into a disconnected Configuration Manager environment.

- [Configure client communication ports](../clients/deploy/configure-client-communication-ports.md): Reconfigure the port numbers for existing clients.

- [Service Connection Tool](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): Keep your site up to date when your service connection point is offline.

- [Support Center](support-center.md): Gather information from clients for easier analysis when troubleshooting.

    **OneTrace** is a modern log viewer with Support Center. It works similarly to CMTrace, with improvements. For more information, see [Support Center OneTrace](support-center-onetrace.md).

- [Send feedback that you saved for later submission](../understand/product-feedback.md#send-feedback-that-you-saved-for-later-submission) (UploadOfflineFeedback): Save your product feedback locally and submit it later.

## Other tools

- [Hierarchy Maintenance Tool](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): Use **Preinst.exe** in the `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` shared folder on the site server to pass commands to the hierarchy manager component.

- [Microsoft Deployment Toolkit (MDT)](../../mdt/use-the-mdt.md): A collection of tools, processes, and guidance for automating desktop and server OS deployments.

- [System Center Updates Publisher (SCUP)](../../sum/tools/updates-publisher.md): A stand-alone tool to manage and import custom software updates.

- [Package Conversion Manager](../../apps/pcm/package-conversion-manager.md): Convert legacy packages into applications.
