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

This article describes how to use the Device Offboarding Agent in Microsoft Intune to identify and manage devices that were removed from Intune but might still exist in Microsoft Entra.

Different prompts can be used to get different results from the agent. The article includes sample prompts and responses to illustrate how the agent can help offboarding devices.

## Prerequisites

Before you get started, ensure you meet the requirements listed in the overview article: [Device Offboarding Agent overview](device-offboarding-agent.md).

## Run the agent

Running the agent resets your current suggestions, status, and assignments for this view. You can use the Tasks page to track progress of suggestions you've added.

To manually run the Device Offboarding Agent:

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Offboarding Agent (preview)**.
1. Select **Run**.  

When an agent run starts, the agent runs until it completes its evaluation. It can't be stopped or paused. 

> [!NOTE]
> Each time the agent runs, it runs under the identity and permissions of the Intune administrator that its been configured to use. 

## Refresh

Executing the **Refresh** action updates the agent's current view with the latest data from its most recent run. This action doesn't trigger a new evaluation; it simply refreshes the displayed information to reflect any changes or updates since the last run.

## Review suggestions and take action

1. In the [Microsoft Intune admin center][INT-AC], select **Agents** > **Device Offboarding Agent (preview)**.
1. Select the **Suggestions** tab to view the list of recommendation.
1. Select a suggestion to view more details, including the rationale behind the recommendation and steps for offboarding the device.
  1. You can change the status of a suggestion by selecting **Manage suggestion** and selecting whether the offboarding action is in progress or completed.
  1. You can select the option **Add to tasks list** to assign the offboarding action to an individual or team for tracking and management.

:::image type="content" source="images/device-offboarding-agent/suggestion.png" alt-text="Screenshot of a suggestion of the Device Offboarding Agent showing the details and options." border="false" lightbox="images/device-offboarding-agent/suggestion.png":::

## Recommended actions examples

The following examples describe sample responses from the Device Offboarding Agent.

### Remove Windows corporate devices

```agent-response
Summary:
There are 23 corporate Windows devices that are no longer in Intune but still in other portals. These devices should be removed.

Factors:
- Users accessing corporate apps without MDM enrollment.
- Cannot enforce compliance policies or data protection.
- Personal devices may have corporate data without proper controls.
- Conditional access limited to user-based policies only.

Recommended actions:
1. Download device list
2. Back up BitLocker recovery keys (recommended)
3. Back up Local Admin Password Solution (LAPS) (recommended)
4. Remove devices from Microsoft Defender portal
5. Remove devices from Autopilot
6. Disable devices in Microsoft Entra
```

### Remove iOS/iPad corporate devices

```agent-response
Summary:
There are 5 personal iOS/iPad devices that are no longer in Intune but still in other portals. These devices should be removed.

Factors:
- Devices are not present in Intune for management
- Corporate devices operating without MDM oversight
- Cannot enforce corporate compliance policies
- Company data accessible without proper security controls

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
- Devices are not present in Intune for management
- Users accessing corporate email and apps without MDM
- No work profile separation between personal and corporate data
- Cannot enforce mobile application management policies
- Data loss prevention policies cannot be applied

Recommended Actions:
1. Download affected device list >
2. Remove devices from Microsoft Defender portal >
3. Disable devices in Microsoft Entra >
```

## Device Offboarding Agent logs 

All agent management, create, delete, run, and any permission failures are available in Security Copilot logs. Logging of which devices were offboarded or when a recommended actions were complete aren't available. Instead, use the options to mark a suggestion as complete.  

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431