---
title: Use the Device Offboarding Agent
description: Learn how to use the Device Offboarding Agent in Microsoft Intune to identify and offboard devices that are no longer in use.
ms.date: 10/15/2025
ms.topic: how-to
author: paolomatarazzo
ms.author: paoloma
ms.reviewer: rishitasarin
---

# Use the Device Offboarding Agent

Use the Device Offboarding Agent in Microsoft Intune to identify and manage devices removed from Intune that might still exist in Microsoft Entra ID or other connected services.

This article provides sample responses to show how the agent helps with device offboarding.

## Prerequisites

Before you begin, make sure you meet the requirements detailed in the [Get Started with the Device Offboarding Agent](device-offboarding-agent.md) article.

## Run the agent

To start using the Device Offboarding Agent, first run an evaluation of your device inventory. This action resets the agent's suggestions, status, and their assignments.

To manually run the Device Offboarding Agent:

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Offboarding Agent (preview)**.
1. Select **Run**.  

The agent runs until it completes its evaluation. You can't stop or pause the process.

> [!NOTE]
> Each time the agent runs, it uses the identity and permissions of the Intune administrator it's configured to use.

## Refresh agent view

Select **Refresh** to update the agent's view with the latest data from its most recent run. This action doesn't trigger a new evaluation; it only refreshes the displayed information to reflect any changes since the last run.

## View the agent's suggestions

After running the agent, review its findings to see which devices may need offboarding.

1. In the [Microsoft Intune admin center][INT-AC], go to **Agents** > **Device Offboarding Agent (preview)**.
2. View the agent's suggestions in the **Overview** or **Suggestions** tab.

:::image type="content" source="images/device-offboarding-agent/suggestions.png" alt-text="Screenshot of the suggestions tab of the Device Offboarding Agent." border="false" lightbox="images/device-offboarding-agent/suggestions.png":::

### Review suggestion details and take action

For each suggestion, you can view more details and take recommended actions to offboard devices.

1. In the [Microsoft Intune admin center][INT-AC], go to **Agents** > **Device Offboarding Agent (preview)**.
2. Select the **Suggestions** tab to view the list of recommendations.
3. Select a suggestion to see more details, including the rationale and steps for offboarding the device.
   - To update the status, select **Manage suggestion** and choose whether the offboarding action is in progress or completed.
   - To assign the offboarding action, select **Add to tasks list** and assign it to an individual or team for tracking and management.

:::image type="content" source="images/device-offboarding-agent/suggestion.png" alt-text="Screenshot of a suggestion of the Device Offboarding Agent showing the details and options." border="false" lightbox="images/device-offboarding-agent/suggestion.png":::

## Examples of recommended actions

The following examples illustrate typical responses and actions you might receive from the agent.

### Remove Windows corporate devices

```agent-response
Summary:
There are 23 corporate Windows devices that are no longer in Intune but still in other portals. These devices should be removed.

Factors:
- Users accessing corporate apps without MDM enrollment.
- Cannot enforce compliance policies or data protection.
- Personal devices may have corporate data without proper controls.
- Conditional access limited to user-based policies only.

Recommended Actions:
1. Download affected device list >
2. Back up BitLocker recovery keys (recommended) >
3. Back up Local Admin Password Solution (LAPS) (recommended) >
4. Remove devices from Microsoft Defender portal >
5. Remove devices from Autopilot >
6. Disable devices in Microsoft Entra >
```

### Remove iOS/iPad corporate devices

```agent-response
Summary:
There are 5 personal iOS/iPad devices that are no longer in Intune but still in other portals. These devices should be removed.

Factors:
- Devices are not present in Intune for management.
- Corporate devices operating without MDM oversight.
- Cannot enforce corporate compliance policies.
- Company data accessible without proper security controls.

Recommended Actions:
1. Download affected device list >
2. Remove devices from Apple Business/School Manager (ABM/ASM) >
3. Disable devices in Microsoft Entra >

```

### Remove Android personal (BYOD) devices

```agent-response
Summary:
There are 5 personal Android devices that are no longer in Intune but still in other portals. These devices should be removed.

Factors:
- Devices are not present in Intune for management.
- Users accessing corporate email and apps without MDM.
- No work profile separation between personal and corporate data.
- Cannot enforce mobile application management policies.
- Data loss prevention policies cannot be applied.

Recommended Actions:
1. Download affected device list >
2. Remove devices from Microsoft Defender portal >
3. Disable devices in Microsoft Entra >
```

## Device Offboarding Agent logs

You can track agent activity and troubleshoot issues using the available logs.

All agent management actions (create, delete, run) and any permission failures are available in Security Copilot logs. Logs do not include which devices were offboarded or when recommended actions were completed.

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431