---
# Required metadata
# For more information, see https://learn.microsoft.com/en-us/help/platform/learn-editor-add-metadata
# For valid values of ms.service, ms.prod, and ms.topic, see https://learn.microsoft.com/en-us/help/platform/metadata-taxonomies

title: 'Device Action: Enhanced Log Collection - Microsoft Intune | Microsoft Learn'
description: Triggering and cancelling enhanced logging on Apple devices
author:      beflamm # GitHub alias
ms.author:   beflamm # Microsoft alias
ms.service: microsoft-intune
ms.topic: how-to
ms.date:     08/20/2026
ms.reviewer: beflamm
---

# Device action: Enhanced logging

Enhanced log collection is a remote device action in Microsoft Intune that lets you trigger a deep diagnostic log capture on a supervised Apple device without physically accessing it or asking the user to manually capture logs. Intune sends the request to the device by using Apple's `Trigger Enhanced Log Collection Command`, the device gathers a detailed log bundle in the background, and the logs are uploaded directly to the corresponding AppleCare case. Intune tracks and reports the status of the collection so you always know whether it's pending, in progress, or complete.

Enhanced log collection is designed for advanced troubleshooting scenarios that require Apple engineering to review low-level system, security, and device management logs—most commonly when you're working an escalation with AppleCare Support.

## When to use enhanced log collection

- AppleCare or Apple Enterprise Support asks you to collect enhanced logs or a sysdiagnose for an open support case.
- You're troubleshooting a recurring MDM, DDM, or OS-level issue on a supervised Mac, iPhone, or iPad and need logs beyond what [Collect diagnostics](collect-diagnostics.md) provides.
- You need to capture logs remotely, at scale, without disrupting the end user or requiring them to run Terminal commands or hold specific buttons.

## Prerequisites

**Device platform requirements**

The Trigger enhanced logging and Cancel enhanced logging actions support the following platforms:

- macOS 27 and later (supervised)

- iOS/iPadOS 27 and later (supervised)

**Roles requirements**

> To run these actions, use an account with the following permissions assigned:
> 
>   - **Remote tasks/Trigger enhanced log collection**
>   - **Remote tasks/Cancel enhanced log collection**

## How to trigger enhanced log collection from the Intune admin center

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices**, then select the supervised Apple device you want to collect logs from.
1. On the device overview page, select **More** (**...**) > **Trigger enhanced log collection**.
1. Enter the token provided by AppleCare in the **AppleCare token** field.

1. Select **Yes** to confirm

## How to cancel enhanced log collection from the Intune admin center

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** > **All devices**, then select the supervised Apple device on which you want to cancel enhanced logging.

1. On the device overview page, select **More** (**...**) > **Cancel enhanced log collection**.
1. Select **Yes** to confirm

### Monitor the status of the action

1. On the device's **Overview** page, go to the **Device actions status** section.
1. Find **Trigger enhanced log collection** or **Cancel enhanced log collection** in the list of recent device actions.
1. The status reports one of the following states, reported back to Intune through the DDM status channel:
   - **Pending** – The command has been queued but not yet delivered to the device.
   - **Acknowledged** – The device received the command and started collecting logs.
   - **Completed** – Logs finished collecting and were uploaded to Apple, or Enhanced Logging was successfully cancelled.
      
   - **Failed** – The device couldn't complete the collection (for example, it went offline, isn't supervised, or is running a version below OS 27).
      
You can also review enhanced log collection requests in the [audit logs](/intune/intune-service/fundamentals/monitor-audit-logs), including which administrator triggered the action and, if applicable, who approved it.

> [!NOTE]
> Enhanced log collection uploads logs directly from the device to Apple. The Intune admin center doesn't provide a copy of the log bundle for you to download—use the AppleCare Support case to review the collected diagnostics with Apple.

## Related Apple documentation

For more detail on the underlying command and status reporting, see Apple's developer documentation:

- [Trigger Enhanced Log Collection command](https://developer.apple.com/documentation/devicemanagement/trigger-enhanced-log-collection-command) – the MDM command Intune sends to the device to start collection.

## Next steps

- [Collect diagnostics](collect-diagnostics.md)
- [Device actions overview](index.md)

- [Manage devices with Intune remote actions](/intune/intune-service/remote-actions/device-management)