---
title: Content library cleanup tool
titleSuffix: Configuration Manager
description: Use the content library cleanup tool to remove orphaned content no longer associated with a Configuration Manager deployment.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Content library cleanup tool

*Applies to: Configuration Manager (current branch)*

Use the content library cleanup command-line tool to remove content that's no longer associated with an object on a distribution point. This type of content is called *orphaned content*. This tool replaces older versions of similar tools released for past Configuration Manager products.

The tool only affects the content on the distribution point that you specify when you run the tool. The tool can't remove content from the content library on the site server.

If you remove content from a distribution point while the site system is offline, an orphaned record can exist in WMI. Over time, this behavior can eventually lead to a warning status on the distribution point. To mitigate the issue in version 2006 and earlier, you had to manually remove the orphaned entries from WMI. Making a mistake during this process could cause more severe issues with the server. Starting in version 2010, the tool can also remove orphaned content records from the WMI provider on a distribution point.<!--6887878-->

Find **ContentLibraryCleanup.exe** in `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` on the site server. For more information on this location, see [The CD.Latest folder](../../servers/manage/the-cd.latest-folder.md).

## Requirements

- Only run the tool against a single distribution point at a time.

- Run it directly on the server that hosts the distribution point to clean up, or remotely from another computer.

- The tool doesn't support removing content from the site server, which has a single content library. When the site server also has the distribution point role, if a package isn't targeted to the server, the package is still in the single content library.<!-- MEMDocs#905 -->

- The tool doesn't support a content-enabled cloud management gateway.

- The user account that runs the tool must have permissions the same as the **Full Administrator** security role in Configuration Manager.

## Modes of operation

Run the tool in the following two modes: [What-if](#what-if-mode) and [Delete](#delete-mode).

> [!TIP]
> Start with the *what-if* mode. When you're satisfied with the results, then run the tool in *delete* mode.

### What-if mode

If you don't specify the `/delete` parameter, the tool runs in what-if mode. This mode identifies the content that would be deleted from the distribution point.

- When run in this mode, the tool doesn't delete any data.

- The tool writes to the log file information about the content that it would delete. You're not prompted to confirm each potential deletion.

### Delete mode

When you run the tool with the `/delete` parameter, the tool runs in delete mode.

- When run in this mode, orphaned content that it finds on the specified distribution point can be deleted from the distribution point's content library.

- Starting in version 2010, it can also remove orphaned content records from the WMI provider on the distribution point.<!--6887878-->

- Before deleting each file, confirm that the tool should delete it. Select **Y** for yes, **N** for no, or **Yes to all** to skip further prompts and delete all orphaned content.

### Log file

When the tool runs in either mode, it automatically creates a log file. It names the file with the following information:

- The mode the tool runs in
- The name of the distribution point
- The date and time of operation

When the tool finishes, it automatically opens the log file in Windows.

By default, the tool writes the log file to the temp folder of the user account that runs the tool. This location is on the computer where you run the tool, which isn't always the target of the tool. Use the `/log` parameter to redirect the log file to another location, including a network share.

## Run the tool

To run the tool:

1. Open a command prompt as an administrator. Change directory to the folder that contains **ContentLibraryCleanup.exe**.

2. Enter a command line that includes the required [command-line parameters](#command-line-parameters), and any optional parameters you want to use.

## Command-line parameters

Use these command-line parameters in any order.

### Required parameters

|Parameter|Details|
|---------|-------|
| `/dp <distribution point FQDN>`  | Specify the fully qualified domain name (FQDN) of the distribution point to clean. |
| `/ps <primary site FQDN>` | *Required* only when cleaning content from a distribution point at a secondary site. The tool connects to the parent primary site to run queries against the SMS Provider. These queries let the tool determine what content should be on the distribution point. It can then identify the orphaned content to remove. This connection to the parent primary site must be made for distribution points at a secondary site because the required details aren't available directly from the secondary site.|
| `/sc <primary site code>`  | *Required* only when cleaning content from a distribution point at a secondary site. Specify the site code of the parent primary site. |

#### Example: Scan and log what content it would delete (what-if)

`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### Example: Scan and log content for a DP at a secondary site

`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC`

### Optional parameters

|Parameter|Details|
|---------|-------|
|`/delete`| Use this parameter when you're ready to delete content from the distribution point. It prompts you before it deletes content. </br></br> When you don't use this parameter, the tool logs results about what content it would delete. Without this parameter, it doesn't actually delete any content from the distribution point. |
| `/q` | This parameter runs the tool in a quiet mode that suppresses all prompts. These prompts include when it deletes content. It also doesn't automatically open the log file. |
| `/ps <primary site FQDN>` | Optional only when cleaning content from a distribution point at a primary site. Specify the FQDN of the primary site that the distribution point belongs to. |
| `/sc <primary site code>` | Optional only when cleaning content from a distribution point at a primary site. Specify the site code of the primary site that the distribution point belongs to. |
| `/log <log file directory>` | Specify the location where the tool writes the log file. This location can be a local drive or a network share.</br></br> When you don't use this parameter, the tool places the log file in the user's temp directory on the computer where the tool runs.|

#### Example: Delete content

`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### Example: Delete content without prompts

`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete`

#### Example: Log to local drive

`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop`

#### Example: Log to network share

`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`

### Known issue

In version 2103 and earlier, when any package or deployment has failed, or is in progress, the tool might return the following error:

`System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

To work around this issue, update the site to version 2107.<!-- 4411374 --> The tool can't reliably identify orphaned files, but will display a warning and continue.
