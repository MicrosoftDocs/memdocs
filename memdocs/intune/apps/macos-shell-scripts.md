---
# required metadata

title: Use shell scripts on macOS devices in Microsoft Intune | Microsoft Docs
description: Create, assign, monitor, and troubleshoot shell scripts for macOS devices in Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use shell scripts on macOS devices in Intune

Use shell scripts to extend device management capabilities on Intune beyond what is supported by the macOS operating system. 

## Prerequisites
Ensure that the following prerequisites are met when composing shell scripts and assigning them to macOS devices. 
 - Devices are running macOS 10.12 or later.
 - Devices are managed by Intune. 
 - Shell scripts begin with `#!` and must be in a valid location such as `#!/bin/sh` or `#!/usr/bin/env zsh`.
 - Command-line interpreters for the applicable shells are installed.

## Important considerations before using shell scripts
 - Shell scripts require that the Microsoft Intune management agent is successfully installed on the macOS device. For more information, see [Microsoft Intune management agent for macOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).
 - Shell scripts run in parallel on devices as separate processes.
 - Shell scripts that are run as the signed-in user will run for all currently signed-in user accounts on the device at the time of the run.
 - An end user is required to sign in to the device to execute scripts running as a signed-in user.
 - Root user privileges are required if the script requires making changes that a standard user account cannot.
 - Shell scripts will attempt to run more frequently than the chosen script frequency for certain conditions, such as if the disk is full, if the storage location is tampered with, if the local cache is deleted, or if the Mac device restarts.
 
## Create and assign a shell script policy
1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **macOS** > **Scripts** > **Add**.
3. In **Basics**, enter the following properties, and select **Next**:
   - **Name**: Enter a name for the shell script.
   - **Description**: Enter a description for the shell script. This setting is optional, but recommended.
4. In **Script settings**, enter the following properties, and select **Next**:
   - **Upload script**: Browse to the shell script. The script file must be less than 200 KB in size.
   - **Run script as signed-in user**: Select **Yes** to run the script with the user's credentials on the device. Choose **No** (default) to run the script as the root user. 
   - **Hide script notifications on devices:** By default, script notifications are shown for each script that is run. End users see a *IT is configuring your computer* notification from Intune on macOS devices.
   - **Script frequency:** Select how often the script is to be run. Choose **Not configured** (default) to run a script only once.
   - **Max number of times to retry if script fails:** Select how many times the script should be run if it returns a non-zero exit code (zero meaning success). Choose **Not configured** (default) to not retry when a script fails.
5. In **Scope tags**, optionally add scope tags for the script, and select **Next**. You can use scope tags to determine who can see scripts in Intune. For full details about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).
6. Select **Assignments** > **Select groups to include**. An existing list of Azure AD groups is shown. Select one or more user or device groups that are to receive the script. Choose **Select**. The groups you choose are shown in the list, and will receive your script policy.
   > [!NOTE]
   > - Shell scripts assigned to user groups applies to any user logging in to the Mac.  
   > - Updating assignments for shell scripts also updates assignments for [Microsoft Intune MDM Agent for macOS](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos).

7. In **Review + add**, a summary is shown of the settings you configured. Select **Add** to save the script. When you select **Add**, the script policy is deployed to the groups you chose.

The script you created now appears in the list of scripts. 

## Monitor a shell script policy
You can monitor the run status of all assigned scripts for users and devices by choosing one of the following reports:
- **Scripts** > **select the script to monitor** > **Device status**
- **Scripts** > **select the script to monitor** > **User status**

>[!IMPORTANT]
> Irrespective of the selected **Script frequency**, the script run status is reported only the first time a script is run. Script run status is not updated on subsequent runs. However, updated scripts are treated as new scripts and will report the run status again.

Once a script runs, it returns one of the following statuses:
- A script run status of **Failed** indicates that the script returned a non-zero exit code or the script is malformed. 
- A script run status of **Success** indicated that the script returned zero as the exit code. 

## Troubleshoot macOS shell script policies using log collection

You can collect device logs to help troubleshoot script issues on macOS devices. 

### Requirements for log collection
The following items are required to collect logs on a macOS device:
- You must specify the full absolute log file path.
- File paths must be separated using only a semicolon (;).
- The maximum log collection size to upload is 60 MB (compressed) or 25 files, whichever occurs first.
- File types that are allowed for log collection include the following extensions: *.log, .zip, .gz, .tar, .txt, .xml, .crash, .rtf*

#### Collect device logs
1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. In **Device status** or **User status** report, select a device.
3. Select **Collect logs**, provide folder paths of log files separated only by a semicolon (;) without spaces or newlines in between paths.<br>For example, multiple paths should be written as `/Path/to/logfile1.zip;/Path/to/logfile2.log`. 

   >[!IMPORTANT]
   > Multiple log file paths separated using comma, period, newline or quotation marks with or without spaces will result in log collection error. Spaces are also not allowed as separators between paths.

4. Select **OK**. Logs are collected the next time the Intune management agent on the device checks in with Intune. This check-in usually occurs every 8 hours.

   >[!NOTE]
   > 
   > - Collected logs are encrypted on the device, transmitted and stored in Microsoft Azure storage for 30 days. Stored logs are decrypted on demand and downloaded using Microsoft Endpoint Manager admin center.
   > - In addition to the admin-specified logs, the Intune management agent logs are also collected from these folders: `/Library/Logs/Microsoft/Intune` and `~/Library/Logs/Microsoft/Intune`. The agent log file-names are `IntuneMDMDaemon date--time.log` and `IntuneMDMAgent date--time.log`. 
   > - If any admin-specified file is missing or has the wrong file-extension, you will find these file-names listed in `LogCollectionInfo.txt`.     

### Log collection errors
Log collection may not be successful due to any of the following reasons provided in the table below. To resolve these errors, follow the remediation steps.

| Error code (hex) | Error code (dec) | Error message | Remediation steps |
|------------------|------------------|---------------|-------------------|
| 0X87D300D1 | 2016214834 | Log file size cannot exceed 60 MB. | Ensure that compressed logs are less than 60 MB in size. |
| 0X87D300D1 | 2016214831 | The provided log file path must exist. The system user folder is an invalid location for log files. | Ensure that the provided file path is valid and accessible. |
| 0X87D300D2 | 2016214830 | Log collection file upload failed due to expiration of upload URL. | Retry the **Collect logs** action. |
| 0X87D300D3, 0X87D300D5, 0X87D300D7 | 2016214829, 2016214827, 2016214825 | Log collection file upload failed due to encryption failure. Retry log upload. | Retry the **Collect logs** action. |
| | 2016214828 | The number of log files exceeded the allowed limit of 25 files. | Only up to 25 log files can be collected at a time. |
| 0X87D300D6 | 2016214826 | Log collection file upload failed due to zip error. Retry log upload. | Retry the **Collect logs** action. |
| | 2016214740 | The logs couldn't be encrypted as compressed logs were not found. | Retry the **Collect logs** action. |
| | 2016214739 | The logs were collected but couldn't be stored. | Retry the **Collect logs** action. |

## Frequently asked questions
### Why are assigned shell scripts not running on the device?
There could be several reasons:
* The agent might need to check-in to receive new or updated scripts. This check-in process occurs every 8 hours and is different from the MDM check-in. Make sure that the device is awake and connected to a network for a successful agent check-in and wait for the agent to check-in. You can also request the end-user to open Company Portal on the Mac, select the device and click **Check settings**.
* The agent may not be installed. Check that the agent is installed at `/Library/Intune/Microsoft Intune Agent.app` on the macOS device.
* The agent may not be in a healthy state. The agent will attempt to recover for 24 hours, remove itself and reinstall if shell scripts are still assigned.

### How frequently is script run status reported?
Script run status is reported to Microsoft Endpoint Manager Admin Console as soon as script run is complete. If a script is scheduled to run periodically at a set frequency, it only reports status the first time it runs.

### When are shell scripts run again?
A script is run again only when the **Max number of times to retry if script fails** setting is configured and the script fails on run. If the **Max number of times to retry if script fails** is not configured and a script fails on run, it will not be run again and run status will be reported as **failed**. 

### What Intune role permissions are required for shell scripts?
Your assigned-intune role requires **Device configurations** permissions to delete, assign, create, update, or read shell scripts.

## Microsoft Intune management agent for macOS
 ### Why is the agent required?
The Microsoft Intune management agent is necessary to be installed on managed macOS devices in order to enable advanced device management capabilities that are not supported by the native macOS operating system.
 
 ### How is the agent installed?
 The agent is automatically and silently installed on Intune-managed macOS devices that you assign at least one shell script to in Microsoft Endpoint Manager Admin Center. The agent is installed at `/Library/Intune/Microsoft Intune Agent.app` when applicable and doesn't appear in **Finder** > **Applications** on macOS devices. The agent appears as `IntuneMdmAgent` in **Activity Monitor** when running on macOS devices.

### What does the agent do?
 - The agent silently authenticates with Intune services before checking in to receive assigned shell scripts for the macOS device.
 - The agent receives assigned shell scripts and runs the scripts based on the configured schedule, retry attempts, notification settings, and other settings set by the admin.
 - The agent checks for new or updated scripts with Intune services usually every 8 hours. This check-in process is independent of the MDM check-in. 
 
 ### How can I manually initiate an agent check-in from a Mac?
On a managed Mac that has the agent installed, open **Company Portal**, select the local device, click on **Check settings**. This initiates an MDM check-in as well as an agent check-in.

Alternatively, open **Terminal**, run the `sudo killall IntuneMdmAgent` command to terminate the `IntuneMdmAgent` process. The `IntuneMdmAgent` process will restart immediately, which will initiate a check-in with Intune.

> [!NOTE]
> The **Sync** action for devices in Microsoft Endpoint Manager Admin Console initiates an MDM check-in and does not force an agent check-in.

 ### When is the agent removed?
 There are several conditions that can cause the agent to be removed from the device such as:
 - Shell scripts are no longer assigned to the device. 
 - The macOS device is no longer managed.
 - The agent is in an irrecoverable state for more than 24 hours (device-awake time).

 ### Why are scripts running even though the Mac is no longer managed?
 When a Mac with assigned scripts is no longer managed, the agent is not removed immediately. The agent detects that the Mac is not managed at the next agent check-in (usually every 8 hours) and cancels scheduled script-runs. So, any locally stored scripts scheduled to run more frequently than the next scheduled agent check-in will run. When the agent is unable to check-in, it retries checking in for up to 24 hours (device-awake time) and then removes itself from the Mac.
 
 ### How to turn off usage data sent to Microsoft for shell scripts?
 To turn off usage data sent to Microsoft from the Intune management agent, open Company Portal and select **Menu** > **Preferences** > *uncheck 'allow Microsoft to collect usage data'*. This will turn off usage data sent for both the agent and Company Portal.

## Known issues
- **No script run status:** In the unlikely event that a script is received on the device and the device goes offline before the run status is reported, the device will not report run status for the script in the admin console.

## Next steps

- [Create a compliance policy in Microsoft Intune](..\protect\create-compliance-policy.md)
