---
# required metadata

title: Understanding Microsoft Intune management agent for macOS
titleSuffix:
description: Learn about the Microsoft Intune management agent for macOS.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/07/2023
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
- tier1
- M365-identity-device-management
- macOS
- highpri
---

# Microsoft Intune management agent for macOS

## Why is the agent required?

The Microsoft Intune management agent is necessary to be installed on managed macOS devices in order to enable advanced device management capabilities that aren't supported by the native macOS operating system.

## How is the agent installed?

 The agent is automatically and silently installed on Intune-managed macOS devices that you assign at least one shell script to in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). The agent is installed at `/Library/Intune/Microsoft Intune Agent.app` when applicable and doesn't appear in **Finder** > **Applications** on macOS devices. The agent appears as `IntuneMdmAgent` in **Activity Monitor** when running on macOS devices.

## What does the agent do?

- The agent silently authenticates with Intune services before checking in to receive assigned shell scripts for the macOS device.
- The agent receives assigned shell scripts and runs the scripts based on the configured schedule, retry attempts, notification settings, and other settings set by the admin.
- The agent checks for new or updated scripts with Intune services usually every 8 hours. This check-in process is independent of the MDM check-in.

## How can I manually initiate an agent check-in from a Mac?

On a managed Mac that has the agent installed, open **Company Portal**, select the local device, select **Check settings**. This initiates an MDM check-in as well as an agent check-in.

Alternatively, open **Terminal**, run the `sudo killall IntuneMdmAgent` command to terminate the `IntuneMdmAgent` process. The `IntuneMdmAgent` process restarts immediately, which will initiate a check-in with Intune.

> [!NOTE]
> The **Sync** action for devices in Microsoft Intune admin center initiates an MDM check-in and does not force an agent check-in.

## When is the agent removed?

 There are several conditions that can cause the agent to be removed from the device such as:

- Shell scripts are no longer assigned to the device.
- The macOS device is no longer managed.
- The agent is in an irrecoverable state for more than 24 hours (device-awake time).

## Why are scripts running even though the Mac is no longer managed?

 When a Mac with assigned scripts is no longer managed, the agent isn't removed immediately. The agent detects that the Mac isn't managed at the next agent check-in (usually every 8 hours) and cancels scheduled script-runs. So, any locally stored scripts scheduled to run more frequently than the next scheduled agent check-in will run. When the agent is unable to check in, it retries checking in for up to 24 hours (device-awake time) and then removes itself from the Mac.

## How to turn off usage data sent to Microsoft for shell scripts?

 To turn off usage data sent to Microsoft from the Intune management agent, open Company Portal and select **Menu** > **Preferences** > *uncheck 'allow Microsoft to collect usage data'*. This will turn off usage data sent for both the agent and Company Portal.

## Next steps

- The app you've created is displayed in the apps list. You can now assign it to the groups you choose. For help, see [How to assign apps to groups](apps-deploy.md).
- Learn more about the ways in which you can monitor the properties and assignment of your app. For more information, see [How to monitor app information and assignments](apps-monitor.md).
- Learn more about the context of your app in Intune. For more information, see [Overview of device and app lifecycles](../fundamentals/device-lifecycle.md)
