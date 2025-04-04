---
title: CMTrace
titleSuffix: Configuration Manager
description: Learn about how to use the CMTrace tool to view log files for Configuration Manager.
ms.date: 12/04/2024
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: Baladelli
ms.author: Baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# CMTrace

*Applies to: Configuration Manager (current branch)*

CMTrace is one of the [Configuration Manager tools](tools.md). It allows you to view and monitor log files, including the following types:

- Log files in Configuration Manager or Client Component Manager (CCM) format

- Plain ASCII or Unicode text files, such as Windows Installer logs

The tool helps to analyze log files by highlighting, filtering, and error lookup.

> [!NOTE]
> CMTrace isn't automatically registered with Windows to open the .log file extension. For more information, see [File associations](#file-associations).

Configuration Manager version 2107 includes multiple performance improvements to the CMTrace log viewer.<!--9607363-->

## Locations

Configuration Manager automatically installs CMTrace in the following locations:

- The site server's tools directory. For example: `cd.latest\SMSSETUP\Tools\CMTrace.exe`
- The Management point's installation directory. For example: `C:\SMS_CCM\CMTrace.exe`
- The client installation directory. For example: `C:\Windows\CCM\CMTrace.exe`
- OS deployment boot images. For example: `X:\sms\bin\x64\CMTrace.exe`

If you have a copy of CMTrace in another location, consider removing it and using a copy in one of the default paths. If it's in a custom location that meets your business requirements, then make sure you have a process to keep it up to date. If your custom location might be of benefit to other customers, file [product feedback](../understand/product-feedback.md).

For more information, see [Direct links to Community hub items](../servers/manage/community-hub.md#bkmk_deeplink).

## Usage

Run **CMTrace.exe**. The first time you run the tool, you see a prompt for file association. For more information, see [File associations](#file-associations).

You take most actions in CMTrace from the following menus:

- [File](#file-menu)
- [Tools](#tools-menu)

### File menu

The following actions are available in the **File** menu:

- [Open](#open)
- [Open on Server](#open-on-server)
- [Print](#print)
- [Preferences](#preferences)

The File menu also lists the last eight recent files. Quickly reopen one of these logs by selecting it from the File menu.

#### Open

Displays the Open dialog box to browse for a log file.

Filter the view for files of the following types:

- Log files (\*.log)
- Old log files (\*.lo_)
- All files (\*.\*)

The following two options aren't selected by default:

- **Ignore existing lines**: When selected, CMTrace ignores the existing contents of the selected log file and displays new lines only as they're added. Use this option to monitor only new actions when you don't need the full history of the log file.

- **Merge selected files**: If you enable this option and select more than one log file, CMTrace merges the selected logs in the view. It displays them as if they're a single log file. The merged log updates the same, and supports all other CMTrace features as if it's a single log file.

#### Open on Server

Browse the Configuration Manager logs folder on a site system computer with the standard Browse dialog box. You can also browse the network for a remote computer.

When you select a remote computer to browse, CMTrace checks for the Configuration Manager share. If it can't find a share with Configuration Manager log files, it displays an error message.

To connect directly to a known computer without browsing, use the [Open](#open) action. Then enter a server name and share using the UNC format.

#### Print

Display the standard Windows Print dialog box. This action sends the current log file to a printer. It formats the output according to the settings on the Printing tab of CMTrace Preferences.

#### Preferences

Configure settings for CMTrace. The following options are available:

- **General** tab

    - **Update Interval**: Controls how often CMTrace checks for changes to log files and loads new lines. By default, this value is 500 milliseconds.

    - **Highlight**: Sets the color that CMTrace uses when highlighting log lines that you choose. By default, this color is basic yellow (Red: 255, Green: 255, Blue: 0).

    - **Columns**: Configures the columns that are visible in the log view and the order in which they appear. By default, it displays Log Text, Component, Date/Time, and Thread.

- **Printing** tab

    - **Columns**: Configure which columns it uses when printing log files and the order in which they appear. By default, it prints the same columns as it displays.

    - **Orientation**: Sets the default print orientation when printing log files. Override this setting in the Print dialog box. By default, it uses Portrait orientation.

- **Advanced** tab

    - **Refresh Interval**: Forces CMTrace to update the log view at a specified interval when loading a large number of lines. By default, this option is disabled with a value of zero.

        > [!NOTE]
        > In general, don't modify the **Refresh Interval**. It can significantly increase the amount of time it takes to open large log files.

### Tools menu

The following actions are available in the **Tools** menu:

- [Find](#find)
- [Find Next](#find-next)
- [Copy to Clipboard](#copy-to-clipboard)
- [Highlight](#highlight)
- [Filter](#filter)
- [Error Lookup](#error-lookup)
- [Pause](#pause)
- [Show/Hide Details](#showhide-details)
- [Show/Hide Info Pane](#showhide-info-pane)

#### Find

Search the open log file for a specified text string.

#### Find Next

Finds the next matching string, as you previously specified in the Find dialog box.

#### Copy to Clipboard

Copies the selected lines as plain text to the Windows clipboard. If you're examining Configuration Manager and CCM log files, it copies the columns in the same order as the view. It separates each column by a tab character. Use this action when copying logs into email messages or other documents.

#### Highlight

Enter a string that CMTrace uses to search the text of each log entry. It then highlights any log text that matches the string you enter.

- The highlight uses the color you specified in Preferences.

- To turn off highlighting, clearing the string from this field.

- If you enter a decimal or hexadecimal number, CMTrace tries to match the value to the Thread column. Use this behavior to highlight the processing of a single thread, without filtering out other threads that might interact with it.

- To compare strings by case, enable the option for **Case sensitive**.

#### Filter

Show or hide log lines based on the specified criteria. Apply filters to any of the four columns regardless of whether they're visible. These settings apply to each opened log file.

Examples:
<!--SCCMDocs issue #603-->

- Filter **smsts.log** on entry text containing "the action" or "the group".
- Filter **InventoryAgent.log** where entry text contains "destination".

#### Error Lookup

Type or paste an error code in either decimal or hexadecimal format to display a description. Possible error sources include: Windows, WMI, or Winhttp.

#### Pause

Suspend or restart log monitoring. The following use cases are some of the possible reasons to use this action:

- When CMTrace is displaying log file information too quickly

- When you pause log monitoring, the information that CMTrace displays isn't lost if the current file rolls over to a new log

- When you want to stop CMTrace from displaying new data while you examine the log file

#### Show/Hide Details

Show or hide all columns other than the log text. It also expands the log text column to the width of the window. Use this action when you're viewing logs on a computer with low display resolution. It displays more of the log text.

> [!NOTE]
> When viewing plain-text files, CMTrace automatically hides details because they're always empty.

#### Show/Hide Info Pane

Show or hide the Info pane. Use this action when you're viewing logs on a computer with low display resolution. It displays more logging details.

## Log pane

The log pane is at the top of the CMTrace window. It displays lines from log files.

When you select a line, it's temporarily highlighted using the Windows selection color scheme.

Highlighted lines match the criteria you define with the **Highlight** option in the **Tools** menu. The highlight uses the color that you specify in **Preferences**.

CMTrace displays lines with errors using a red background and yellow text color. In CCM-format logs, log entries have an explicit type value that indicates the entry as an error. For other log formats, CMTrace does a case-insensitive search in each entry for any text string matching "error".

It displays lines with warnings using a yellow background. In CCM-format logs, log entries have an explicit type value that indicates the entry as a warning. For other log formats, CMTrace does a case-insensitive search in each entry for any text string matching "warn".

## Info pane

The Info pane is at the bottom of the CMTrace window. It includes the following features:

- Details about the currently selected log entry

- A text box that displays the log text

- It displays carriage returns so that formatted text is easier to read

- Easier to read long entries that aren't fully visible in the Log pane

Show or hide the Info pane with the **Show/Hide Info Pane** option on the **Tools** menu. If the Info pane takes up more than half of the log window, CMTrace automatically hides it.

### Progress bar

When you first open a log file, CMTrace replaces the Info pane by a progress bar. This progress indicates how much of the existing file contents it's loaded. The progress reaches 100 percent, CMTrace removes the progress bar, and replaces it with the Info pane. When you load large files, this behavior provides you with an indication of how long the load might take.

### Status bar

For Configuration Manager-format and CCM-format log files, the status bar displays the elapsed time for the selected log entries. If you select a single entry, the tool displays the time from the first log entry to the selected entry. If you select multiple entries, it calculates the time from the top-most selected entry to the bottom-most selected entry. CMTrace formats this information as follows:

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`

## Windows shell integration

CMTrace supports [file associations](#file-associations) and [drag-and-drop](#drag-and-drop).

### File associations

CMTrace can associate itself with .log and .lo_ file name extensions. When the program starts, it checks the registry to determine whether it's already associated with these file name extensions. If CMTrace isn't already associated with any file name extensions, you're prompted to associate the file name extensions with CMTrace. If you select **Do not ask me this again**, CMTrace skips this check whenever it's run on this computer.

### Drag-and-drop

CMTrace supports basic drag-and-drop functionality. Drag a log file from Windows Explorer into CMTrace to open it.

## Other tips

### Last Directory registry key

<!--511280-->
By default, CMTrace saves the last log location that you opened. This behavior is useful on the site server, as it defaults to the logs path every time.

The first time you launch it on a client, it defaults to the current working directory. This location may be the path where you saved CMTrace, or a path like `%userprofile%\Desktop`.

The **Last Directory** value in the registry key `HKEY_CURRENT_USER\Software\Microsoft\Trace32` controls this default location. If you set this value to `%windir%\CCM\Logs` on your clients, then CMTrace opens files in the client log location the first time you run it.

## Next steps

- [Log files](../plan-design/hierarchy/log-files.md)

- [Support Center log file viewer](support-center.md#support-center-log-file-viewer)

**OneTrace** is the log viewer with Support Center. It works similarly to CMTrace, with improvements. For more information, see [Support Center OneTrace](support-center-onetrace.md).
