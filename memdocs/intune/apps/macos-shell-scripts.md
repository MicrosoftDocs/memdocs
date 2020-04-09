---
# required metadata

title: Use shell scripts on macOS devices in Microsoft Intune | Microsoft Docs
description: Create, assign, monitor, and troubleshoot shell scripts for macOS devices in Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/06/2020
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

# Use shell scripts on macOS devices in Intune (Public Preview)

> [!NOTE]
> Shell scripts for macOS devices is currently in preview. Review the list of [known issues in preview](macos-shell-scripts.md#known-issues) before using this feature.

Use shell scripts to extend device management capabilities on Intune beyond what is supported by the macOS operating system. 

## Prerequisites
Ensure that the following prerequisites are met when composing shell scripts and assigning them to macOS devices. 
 - Devices are running macOS 10.12 or later.
 - Devices are managed by Intune. 
 - Shell scripts begin with `#!` and must be in a valid location such as `#!/bin/sh` or `#!/usr/bin/env zsh`.
 - Command-line interpreters for the applicable shells are installed.

## Important considerations before using shell scripts
 - Shell scripts require that Microsoft Intune MDM Agent is successfully installed on the macOS device. For more information, see [Microsoft Intune MDM Agent for macOS](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos).
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
6. Select **Assignments** > **Select groups to include**. An existing list of Azure AD groups is shown. Select one or more device groups that include the users whose macOS devices are to receive the script. Choose **Select**. The groups you choose are shown in the list, and will receive your script policy.
   > [!NOTE]
   > - Shell scripts in Intune can only be assigned to Azure AD device security groups. User group assignment is not supported in preview. 
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

## Frequently asked questions
### Why are assigned shell scripts not running on the device?
There could be several reasons:
* The agent might need to check-in to receive new or updated scripts. This check-in process occurs every 8 hours and is different from the MDM check-in. Make sure that the device is awake and connected to a network for a successful agent check-in and wait for the agent to check-in.
* The agent may not be installed. Check that the agent is installed at `/Library/Intune/Microsoft Intune Agent.app` on the macOS device.
* The agent may not be in a healthy state. The agent will attempt to recover for 24 hours, remove itself and reinstall if shell scripts are still assigned.

### How frequently is script run status reported?
Script run status is reported to Microsoft Endpoint Manager Admin Console as soon as script run is complete. If a script is scheduled to run periodically at a set  frequency, it only reports status the first time it runs.

### When are shell scripts run again?
A script is run again only when the **Max number of times to retry if script fails** setting is configured and the script fails on run. If the **Max number of times to retry if script fails** is not configured and a script fails on run, it will not be run again and run status will be reported as **failed**. 

### What Intune role permissions are required for shell scripts?
Your assigned-intune role requires **Device configurations** permissions to delete, assign, create, update, or read shell scripts.

## Microsoft Intune MDM Agent for macOS
 ### Why is the agent required?
 Microsoft Intune MDM Agent is necessary to be installed on managed macOS devices in order to enable advanced device management capabilities that are not supported by the native macOS operating system.
 
 ### How is the agent installed?
 The agent is automatically and silently installed on Intune-managed macOS devices that you assign at least one shell script to in Microsoft Endpoint Manager Admin Center. The agent is installed at `/Library/Intune/Microsoft Intune Agent.app` when applicable and doesn't appear in **Finder** > **Applications** on macOS devices. The agent appears as `IntuneMdmAgent` in **Activity Monitor** when running on macOS devices.

### What does the agent do?
 - The agent silently authenticates with Intune services before checking in to receive assigned shell scripts for the macOS device.
 - The agent receives assigned shell scripts and runs the scripts based on the configured schedule, retry attempts, notification settings, and other settings set by the admin.
 - The agent checks for new or updated scripts with Intune services usually every 8 hours. This check-in process is independent of the MDM check-in. 
 
 ### How can I manually initiate an agent check-in from a Mac?
On a managed Mac that has the agent installed, open **Terminal**, run the `sudo killall IntuneMdmAgent` command to terminate the `IntuneMdmAgent` process. The `IntuneMdmAgent` process will restart immediately, which will initiate a check-in with Intune.

Alternatively, you can do the following:
1. Open **Activity Monitor** > **View** > *select **All processes**.* 
2. Search for processes named `IntuneMdmAgent`. 
3. Quit the process running for **root** user. 

> [!NOTE]
> The **Check settings** action in Company Portal and the **Sync** action for devices in Microsoft Endpoint Manager Admin Console initiates an MDM check-in and does not force an agent check-in.

 ### When is the agent removed?
 There are several conditions that can cause the agent to be removed from the device such as:
 - Shell scripts are no longer assigned to the device. 
 - The macOS device is no longer managed.
 - The agent is in an irrecoverable state for more than 24 hours (device-awake time).

 ### How to turn off usage data sent to Microsoft for shell scripts?
 To turn off usage data sent to Microsoft from Intune MDM Agent, open Company Portal and select **Menu** > **Preferences** > *uncheck 'allow Microsoft to collect usage data'*. This will turn off usage data sent for both Intune MDM agent and Company Portal.

## Known issues
- **User group assignment:** Shell scripts assigned to user groups doesn't apply to devices. User group assignment is currently not supported in preview. Use device group assignment to assign scripts.
- **Collect logs:** "Collect logs" action is visible. But when log collection is attempted, it shows "an error occurred" and doesn't capture logs. Log collection is currently not supported in preview.
- **No script run status:** In the unlikely event that a script is received on the device and the device goes offline before the run status is reported, the device will not report run status for the script in the admin console.
- **User status report:** An empty report issue exists. In the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Monitor**. The user status shows an empty report.

## Next steps

- [Create a compliance policy in Microsoft Intune](..\protect\create-compliance-policy.md)
