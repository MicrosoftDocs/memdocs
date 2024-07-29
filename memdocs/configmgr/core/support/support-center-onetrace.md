---
title: Support Center OneTrace
titleSuffix: Configuration Manager
description: OneTrace is a new log viewer with Support Center that has improvements over CMTrace.
ms.date: 12/01/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Support Center OneTrace

<!--3555962-->

OneTrace is a new log viewer with Support Center. It works similarly to CMTrace, with the following improvements:

- A tabbed view
- Dockable windows
- Improved search capabilities
- Ability to enable filters without leaving the log view
- Scrollbar hints to quickly identify clusters of errors
- Fast log opening for large files
- Windows jump lists for recently opened files (version 2103 and later)
- Status messages are displayed in an easy to read format (version 2111 and later) 
   - Entries starting with `>>` are status messages that are automatically converted into a readable format when a log is opened. Search or filter on the `>>` string to find status messages in the log.

:::image type="content" source="media/3555962-onetrace.png" alt-text="Screenshot of Support Center OneTrace log viewer." lightbox="media/3555962-onetrace.png":::

OneTrace works with many types of log files, such as:

- Configuration Manager client logs
- Configuration Manager server logs
- Status messages
- Windows Update ETW log file on Windows 10 or later
- Windows Update log file on Windows 7 & Windows 8.1

## Prerequisites

Starting in version 2107, the all site and client components require .NET version 4.6.2, and version 4.8 is recommended.<!--10402814--> For more information, [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md#net-version-requirements).

In version 2103 and earlier, this tool requires .NET 4.6 or later.

## Install

OneTrace installs with Support Center. Find the Support Center installer on the site server at the following path: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

By default, the OneTrace application is installed at `C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe`.

> [!NOTE]
> Support Center Log File Viewer and OneTrace use Windows Presentation Foundation (WPF). This component isn't available in Windows PE. Continue to use [CMTrace](cmtrace.md) in boot images with task sequence deployments.

## Log groups

<!--5559993-->

OneTrace supports customizable log groups, similar to the feature in Support Center. Log groups allow you to open all log files for a single scenario. OneTrace currently includes groups for the following scenarios:

- Application management
- Compliance settings (also referred to as Desired Configuration Management)
- Software updates

To show log groups, go to the **View** menu, and select **Log groups**.

:::image type="content" source="media/5559993-onetrace-log-groups.png" alt-text="Screenshot of Support Center OneTrace log group for application management.":::

### Customize log groups

You can customize these groups by modifying the configuration XML, which by default is in the following path: `C:\Program Files (x86)\Configuration Manager Support Center\LogGroups.xml`.

The following example is one portion of the default configuration file:

``` XML
<LogGroups>
  <LogGroup Name="Desired Configuration Management" GroupType="1" GroupFilePath="">
    <LogFile>CIAgent.log</LogFile>
    <LogFile>CIDownloader.log</LogFile>
    <LogFile>CIStateStore.log</LogFile>
    <LogFile>CIStore.log</LogFile>
    <LogFile>CITaskMgr.log</LogFile>
    <LogFile>ccmsdkprovider.log</LogFile>
    <LogFile>DCMAgent.log</LogFile>
    <LogFile>DCMReporting.log</LogFile>
    <LogFile>DcmWmiProvider.log</LogFile>
  </LogGroup>
</LogGroups>
```

The `GroupType` property accepts the following values:

- `0`: Unknown or other
- `1`: Configuration Manager client logs
- `2`: Configuration Manager server logs

The `GroupFilePath` property can include an explicit path for the log files. If it's blank, OneTrace relies upon the registry configuration for the group type. For example, if you set `GroupType=1`, by default OneTrace will automatically look in `C:\Windows\CCM\Logs` for the logs in the group. In this example, you don't need to specify `GroupFilePath`.

## Open recent files

<!--6991505-->

Starting in version 2103, OneTrace supports Windows jump lists for recently opened files. Jump lists let you quickly go to previously opened files, so you can work faster.

There are three methods to open recent files in OneTrace:

- Windows taskbar jump list
- Windows Start menu recently opened list
- In OneTrace from **File** menu or **Recently opened** tab.

### Windows taskbar jump list

When the OneTrace icon is on the Windows taskbar, right-click it, and then select a file from the **Recently opened** list.

:::image type="content" source="media/6991505-onetrace-jump-list.png" alt-text="Support Center OneTrace jump list from Windows taskbar with recently opened list.":::

### Windows Start menu recently opened list

Go to the **Start** menu, and type `onetrace`. Select a file from the **Recently opened** list.

:::image type="content" source="media/6991505-onetrace-start-menu.png" alt-text="Support Center OneTrace in Windows Start menu with recently opened list.":::

### OneTrace recently opened list

There are two locations in OneTrace that show the list of recently opened files:

- The **Recently opened** tab in the lower right corner.
- Go to the **File** menu and select a file at the bottom of the menu.

:::image type="content" source="media/6991505-onetrace-recently-opened.png" alt-text="Support Center OneTrace recently opened lists.":::

## Next steps

[User interface reference](support-center-ui-reference.md)
