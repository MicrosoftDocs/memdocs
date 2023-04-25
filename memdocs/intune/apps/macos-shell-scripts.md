---
# required metadata

title: Use shell scripts on macOS devices in Microsoft Intune | Microsoft Docs
description: Create, assign, monitor, and troubleshoot shell scripts for macOS devices in Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/19/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- macOS
---

# Use shell scripts on macOS devices in Intune

Use shell scripts to extend device management capabilities in Intune, beyond what is supported by the macOS operating system.

> [!NOTE]
> Rosetta 2 is required to run x64 (Intel) version of apps on Apple Silicon Macs. To install Rosetta 2 on Apple Silicon Macs automatically, you can deploy a shell script in Endpoint Manager. To view a sample script, see [Rosetta 2 Installation Script](https://github.com/microsoft/shell-intune-samples/tree/master/macOS/Config/Rosetta2).

## Prerequisites

Ensure that the following prerequisites are met when composing shell scripts and assigning them to macOS devices.

- Devices are running macOS 10.13 or later.
- Devices are managed by Intune.
- Devices are connected directly to the Internet. Connection through a proxy is not supported. 
- Shell scripts begin with `#!` and must be in a valid location such as `#!/bin/sh` or `#!/usr/bin/env zsh`.
- Command-line interpreters for the applicable shells are installed.

## Important considerations before using shell scripts

- Shell scripts require that the Microsoft Intune management agent is successfully installed on the macOS device. For more information, see [Microsoft Intune management agent for macOS](../apps/lob-apps-macos-agent.md).
- Shell scripts run in parallel on devices as separate processes.
- Shell scripts that are run as the signed-in user will run for all currently signed-in user accounts on the device at the time of the run.
- An end user is required to sign in to the device to execute scripts running as a signed-in user.
- Root user privileges are required if the script requires making changes that a standard user account cannot.
- Shell scripts will attempt to run more frequently than the chosen script frequency for certain conditions, such as if the disk is full, if the storage location is tampered with, if the local cache is deleted, or if the Mac device restarts.

## Create and assign a shell script policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **macOS** > **Shell scripts** > **Add**.
3. In **Basics**, enter the following properties, and select **Next**:
   - **Name**: Enter a name for the shell script.
   - **Description**: Enter a description for the shell script. This setting is optional, but recommended.
4. In **Script settings**, enter the following properties, and select **Next**:
   - **Upload script**: Browse to the shell script. The script file must be less than 200 KB in size.
   - **Run script as signed-in user**: Select **Yes** to run the script with the user's credentials on the device. Choose **No** (default) to run the script as the root user.
   - **Hide script notifications on devices:** By default, script notifications are shown for each script that is run. End users see a *IT is configuring your computer* notification from Intune on macOS devices.
   - **Script frequency:** Select how often the script is to be run. Choose **Not configured** (default) to run a script only once. Scripts with a frequency set will also run after a device restart.
   - **Max number of times to retry if script fails:** Select how many times the script should be run if it returns a non-zero exit code (zero meaning success). Choose **Not configured** (default) to not retry when a script fails.
5. In **Scope tags**, optionally add scope tags for the script, and select **Next**. You can use scope tags to determine who can see scripts in Intune. For full details about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).
6. Select **Assignments** > **Select groups to include**. An existing list of Azure AD groups is shown. Select one or more user or device groups that are to receive the script. Choose **Select**. The groups you choose are shown in the list, and will receive your script policy.
    > [!NOTE]
    >
    > - Shell scripts assigned to user groups applies to any user logging in to the Mac.
    > - Updating assignments for shell scripts also updates assignments for [Microsoft Intune MDM Agent for macOS](../apps/lob-apps-macos-dmg.md).

7. In **Review + add**, a summary is shown of the settings you configured. Select **Add** to save the script. When you select **Add**, the script policy is deployed to the groups you chose.

The script you created now appears in the list of scripts. If needed, you can view the contents of macOS shell scripts after you upload them to Intune.

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

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Navigate to **Devices** > **Scripts** and select a macOS shell script.
3. In **Device status** or **User status** report, select a device.
4. Select **Collect logs**, provide folder paths of log files separated only by a semicolon (;) without spaces or newlines in between paths.<br>For example, multiple paths should be written as `/Path/to/logfile1.zip;/Path/to/logfile2.log`.

   >[!IMPORTANT]
   > Multiple log file paths separated using comma, period, newline or quotation marks with or without spaces will result in log collection error. Spaces are also not allowed as separators between paths.

5. Select **OK**. Logs are collected the next time the Intune management agent on the device checks in with Intune. This check-in usually occurs every 8 hours.

   >[!NOTE]
   >
   > - Collected logs are encrypted on the device, transmitted and stored in Microsoft Azure storage for 30 days. Stored logs are decrypted on demand and downloaded using Microsoft Intune admin center.
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

## Custom attributes for macOS

You can create custom attribute profiles which enable you to collect custom properties from managed macOS device using shell scripts.

### Create and assign a custom attribute for macOS devices

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **macOS** > **Custom attributes** > **Add**.
3. In **Basics**, enter the following properties, and select **Next**:
   - **Name**: Enter a name for the script.
   - **Description**: Enter a description for the script. This setting is optional, but recommended.
4. In **Attribute settings**, enter the following properties, and select **Next**:
   - **Data type of attribute**: Select the data type of the result that the script returns. Available values are **String**, **Integer**, and **Date**.
   - **Script**: Select a script file.

   Additional details:
   - The shell script must echo the attribute to be reported and the data type of the output must match the data type of attribute in the custom attribute profile.
   - The result returned by the shell script must be 20KB or less.

   > [!NOTE]
   > When using `Date` type attributes, ensure that the shell script returns dates in ISO-8601 format. See the examples below.
   >
   > **To print an ISO-8601-compliant date with time-zone:**
   >
   > ``` Shell
   > #!/bin/sh
   > var=$(date +"%Y-%m-%dT%H:%M:%S%z")
   > echo $var # Prints an ISO-8601 compliant date with time-zone
   > ```
   >
   > **To print an ISO-8601-compliant date in UTC time:**
   >
   > ``` Shell
   > #!/bin/sh
   > var=$(date -u +"%Y-%m-%dT%H:%M:%SZ")
   > echo $var # Prints an ISO-8601 compliant date in UTC time
   > ```

5. In **Assignments**, click **Select groups to include**. When you choose **Select groups to include** an existing list of Azure AD groups is shown. Select one or more user or device groups that are to receive the script. Choose **Select**. The groups you choose are shown in the list, and will receive your script policy. Alternatively, you can choose to select **All users**, **All devices**, or **All users and all devices** by selecting one of these options in the dropdown box next to **Assign to**.
   > [!NOTE]
   >
   > - Scripts assigned to user groups applies to any user logging in to the Mac.

6. In **Review + add**, a summary is shown of the settings you configured. Select **Add** to save the script. When you select **Add**, the script policy is deployed to the groups you chose.

The script you created now appears in the list of custom attributes. If needed, you can view the contents of custom attributes after you upload them to Intune.

## Monitor a custom attribute policy

You can monitor the run status of all assigned custom attribute profiles for users and devices by choosing one of the following reports:

- **Custom attributes** > *select the custom attribute profile to monitor* > **Device status**
- **Custom attributes** > *select the custom attribute profile to monitor* > **User status**

> [!IMPORTANT]
> Shell scripts provided in custom attribute profiles are run every 8 hours on managed Macs and reported.

Once a custom attribute profile runs, it returns one of the following statuses:

- A status of **Failed** indicates that the script returned a non-zero exit code or the script is malformed. The error is reported in the **Result** column.
- As status of **Success** indicates that the script returned zero as the exit code. The output echoed by the script is reported in the **Result** column.

## Frequently asked questions

### Why are assigned shell scripts not running on the device?

There could be several reasons:

- The agent might need to check in to receive new or updated scripts. This check-in process occurs every 8 hours and is different from the MDM check-in. Make sure that the device is awake and connected to a network for a successful agent check-in and wait for the agent to check in. You can also request the end user to open Company Portal on the Mac, select the device and click **Check settings**.
- The agent may not be installed. Check that the agent is installed at `/Library/Intune/Microsoft Intune Agent.app` on the macOS device.
- The agent may not be in a healthy state. The agent will attempt to recover for 24 hours, remove itself and reinstall if shell scripts are still assigned.

### How frequently is script run status reported?

Script run status is reported to Microsoft Intune admin center as soon as script run is complete. If a script is scheduled to run periodically at a set frequency, it only reports status the first time it runs.

### When are shell scripts run again?

A script is run again only when the **Max number of times to retry if script fails** setting is configured and the script fails on run. If the **Max number of times to retry if script fails** is not configured and a script fails on run, it will not be run again and run status will be reported as **failed**.

### What Intune role permissions are required for shell scripts?

Your assigned-intune role requires **Device configurations** permissions to delete, assign, create, update, or read shell scripts.

## Known issues

- **No script run status:** In the unlikely event that a script is received on the device and the device goes offline before the run status is reported, the device will not report run status for the script in the admin center.

## Additional information

When you deploy shell scripts or custom attributes for macOS devices from Microsoft Endpoint Manager, it deploys the new universal version of the Intune management agent app that runs natively on Apple Silicon Mac machines. The same deployment will install the x64 version of the app on Intel Mac machines. Rosetta 2 is required to run x64 (Intel) version of apps on Apple Silicon Macs. To install Rosetta 2 on Apple Silicon Macs automatically, you can deploy a shell script in Endpoint Manager. To view a sample script, see [Rosetta 2 Installation Script](https://github.com/microsoft/shell-intune-samples/tree/master/macOS/Config/Rosetta2).

## Next steps

- [Create a compliance policy in Microsoft Intune](..\protect\create-compliance-policy.md)
