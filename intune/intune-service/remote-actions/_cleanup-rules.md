---
# required metadata

title: "Intune Cleanup Rules"
description: Learn about cleanup rules in Microsoft Intune.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Cleanup rules in Intune

You can configure Intune to automatically clean up devices that appear to be inactive, stale, or unresponsive. These cleanup rules continuously monitor your device inventory so that your device records stay current. Devices cleaned up in this way are concealed and hidden from some Intune reports. This setting affects all devices managed by Intune, not just specific devices.

## Before you begin

- The device cleanup rule doesn't trigger a BitLocker suspension when BitLocker encryption is managed by Intune. To create a BitLocker profile, see [Manage BitLocker policy for Windows devices with Intune](../protect/encrypt-devices.md).
- Device cleanup rules aren't available for Jamf-managed devices.
- To update device cleanup rules, you need the **Managed Device Cleanup Settings** > **Update** permission set to **Yes**. This permission is part of [Intune role-based access control (RBAC)](../fundamentals/role-based-access-control.md).

  :::image type="content" source="images/managed-device-cleanup-rules-permission.png" alt-text="Screenshot that shows the Managed Device Cleanup Settings permission in RBAC set to Yes in Microsoft Intune.":::

## Create a device cleanup rule

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices** > **Organize devices** > **Device cleanup rules** > **Create**.
1. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the rule.
    - **Description**: Enter a description for the rule. This setting is optional, but recommended.
    - **Platform**: Select the platform that the rule applies to. Your options:
        - All platforms
        - Android (AOSP)
        - Android Enterprise
        - iOS/iPadOS
        - macOS
        - Windows

    You can create one rule per platform. The rule applies to all devices in your organization with the platform you select.

1. Select **Next**.
1. In **Rule settings** > **Remove devices that haven't checked in for this many days**, enter a number between 30 and 270.

    This setting determines how many days a device must check in with the Intune service before the device is considered stale or inactive. If a device fails to check-in before the period ends, the device is cleaned up.

1. Select **Next**.
1. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the rule applies. The rule is also shown in the cleanup rules list.

When a device cleanup rule runs, it conceals the device from Intune reports. This action doesn't trigger a Wipe or Retire action.

The [Intune audit logs](../fundamentals/monitor-audit-logs.md) show the devices concealed by your device cleanup rules. In the logs, filter by **Activity name** > **Device set to be hidden from admin by Device Cleanup Rule [*YourRuleName*]**.

If a cleaned up device checks in before its device certification expires, it reappears in the Intune admin center. Once the device certification expires, the device must go through a re-enrollment process for it to show in the Intune admin center.
