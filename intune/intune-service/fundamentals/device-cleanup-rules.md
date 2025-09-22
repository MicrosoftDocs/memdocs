---
title: Automatically remove devices with cleanup rules
description: Intune's device cleanup rules offer a simple, automated way to ensure that only actively managed devices remain visible in the admin center. Learn more about device cleanup rules and how to configure them.
ms.date: 09/22/2025
ms.topic: how-to
author: paolomatarazzo
ms.author: paoloma
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Device cleanup rules

Managing a dynamic device fleet means constantly tracking devices that come and go—due to upgrades, user turnover, or inactivity. Intune's device cleanup rules help keep the admin center clean by automatically removing stale records.

## How it works

Device cleanup rules in Intune automatically remove records of devices that haven't checked in for a specified period (for example, 90 days). These rules:

- Do not wipe or retire devices.
- Soft delete records—devices are hidden from the Intune portal and reports but preserved in the backend for potential recovery.
- Run periodically and auto-recover devices that check in again (for example, after extended leave).
- Don't trigger BitLocker suspension when Intune manages BitLocker encryption.
- Aren't available for Jamf-managed devices.


⚠️ Devices removed from Intune are not deleted from Entra ID. An Entra ID admin must manually remove them from Azure AD.



## Before you begin


## Requirements

[!INCLUDE [rbac-requirements](../includes/h3/rbac-requirements.md)]

> [!div class="checklist"]
> To configure device cleanup rules, use an account with at least one of the following roles:
>
> - Intune Service Administrator
> - [Custom role][INT-RC] that includes:
>   - The permission **Managed Device Cleanup Rules/Update**
>   - The permission **Managed Device Cleanup Settings/Update**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

## How to create a device cleanup rule

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Organize devices** > **Device cleanup rules**.
1. Select **Create**.
1. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the rule.
    - **Description**: Enter a description for the rule. This setting is optional.
    - **Platform**: Select the platform that the rule applies to. The options are:
        - All platforms
        - Android (AOSP)
        - Android (fully managed/dedicated/corporate-owned work profile)
        - Android (device administrator)
        - Android (personally-owned work profile)
        - ChromeOS
        - iOS/iPadOS
        - macOS
        - Windows
        - Windows Holographic
        - visionOS
        - tvOS

    You can create one rule per platform. The rule applies to all devices in your organization with the platform you select.

1. Select **Next**.
1. In **Rule settings** > **Remove devices that haven't checked in for this many days**, enter a number between 30 and 270.

    This setting determines how many days a device must check in with the Intune service before the device is considered stale or inactive. If a device fails to check in before the period ends, the device is cleaned up.

    > [!TIP]
    > Select **Preview affected devices** to get a list of devices that didn't check in during the specified number of days.

1. Select **Next**.
1. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the rule applies.

## Device cleanup rules behavior

When a device cleanup rule runs, it hides the affected devices from Intune reports. It doesn't trigger any actions on the devices.

If a cleaned up device checks in before its device certification expires, it reappears in the Intune admin center. Once the device certification expires, the device must go through a re-enrollment process for it to show in the Intune admin center.

## Device cleanup rules logging

The [Intune audit logs](monitor-audit-logs.md) show the devices hidden by the device cleanup rules. In the logs, filter by **Activity name** > **Device set to be hidden from admin by Device Cleanup Rule [*Your Rule Name*]**.

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role