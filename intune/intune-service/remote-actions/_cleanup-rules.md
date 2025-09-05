---
title: Device cleanup Rules in Microsoft Intune
description: Intune's device cleanup rules offer a simple, automated way to ensure that only actively managed devices remain visible in the admin center. Learn more about device cleanup rules and how to configure them.
ms.date: 08/27/2025
ms.topic: how-to

ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Device cleanup rules in Intune

<!--
Managing a dynamic fleet of devices across an organization can be a daunting task for IT professionals. As devices come and go—whether due to upgrades, user turnover, or inactivity—keeping the Microsoft Intune admin center clean and accurate becomes essential. That's where Intune's device cleanup rules come into play.

For IT professionals managing diverse environments, keeping the device inventory clean is essential for operational clarity, security hygiene, and compliance. Intune's cleanup rules offer a simple, automated way to ensure that only actively managed devices remain visible in the admin center.

Cleanup rules are automated policies in Microsoft Intune that remove device records from the admin console when those devices haven't checked in for a defined period (e.g., 90 days). These rules do not trigger a wipe or retire action. Instead, they simply hide the device record from the Intune portal and reports.

Even after removal, the device remains encrypted (e.g., via BitLocker) and present in Microsoft Entra ID, ensuring that the security posture is preserved.

From portal:

Create rules to remove Intune-enrolled devices that are inactive or unresponsive. These rules are applied every 24 hours. Once a device checks in again, it will still be enrolled without further action from you.

Under **Rule settings**, configure the number of days (30-270).

Description: "Once you create the rule, all devices inactive for the number of days you set will be removed from Intune. Intune will keep removing devices that are inactive for that number of days."


From blog:

"Device clean-up rules provides the ability to configure the automatic cleanup rule for the devices that are inactive, orphaned and have not checked in recently. The rule allows administrators to choose between 30 and 270 days to remove the inactive device records from Intune automatically.

For configuring the rule in the environment, navigate to the Devices blade in Microsoft Endpoint Manager admin center and click on Device clean-up rules. Administrator will be able to enable the cleanup rule to delete the devices that have not checked in for {X} days (30-270).


What happens behind the scenes for Device Clean-up rules?

After the Intune Service Administrator enables the rule, Intune services run a background job every few hours to remove all applicable devices from the Intune portal and they will not show up in any Intune blade or device list anymore. The device removal is only applicable to Intune portal and devices do not get removed from Azure AD. Azure AD tenant administrator has  to perform the device cleanup task in Azure AD portal to remove the stale record permanently.


What device types get affected from this device clean-up?

Device cleanup rules are applicable for Android, IOS, Windows, MacOS and Linux. The devices that were unable (user abandonment, etc.) to complete the enrollment process are also cleaned up as well.

Does this device clean-up rule perform device wipe or retire?

No, this automatic rule only removes the devices from the Intune portal which are orphaned devices. It means these devices are no longer checking in with the service for the last x days chosen by the administrator before getting removed from the Intune portal.


Is it possible to have devices removed by  the device clean-up rule to come back in some scenarios?

Yes, it is possible that some devices can come back in the Intune portal as there is a service criterion to auto-recover the cleaned-up devices if they successfully check-in to the Intune service subsequently. The purpose of this behavior is to recover devices owned by the employees that took a long leave (e.g., Extended vacation, sabbatical, maternity leaves) and the devices were not communicating with the service during their absence. The threshold for devices to show up in the Intune portal is 180 days provided the Intune device certificate is not expired. Please note that Intune service only does the soft delete of inactive device records and the records are still preserved at the backend for certain period to enable such auto recovery.
-->

You can configure Intune to automatically clean up devices that appear to be inactive, stale, or unresponsive. These cleanup rules continuously monitor your device inventory so that your device records stay current. Devices cleaned up in this way are concealed and hidden from some Intune reports. This setting affects all devices managed by Intune, not just specific devices.

## Requirements

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To configure device cleanup rules, you must use an account that has at least one of the following roles:
>
> - Intune Service Administrator
> - [Custom role][INT-RC] that includes:
>   - The permission **Managed Device Cleanup Rules/Update**
>   - The permission **Managed Device Cleanup Settings/Update**
>   - Permissions that provide visibility into and access to managed devices in Intune (e.g. Organization/Read, Managed devices/Read)

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

    Tip: Select **Preview affected devices** to obtain a list of devices that haven't checked in the specified number of 30 days.

1. Select **Next**.
1. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the rule applies. The rule is also shown in the cleanup rules list.

## Device cleanup rules behavior

When a device cleanup rule runs, it conceals the device from Intune reports. It doesn't trigger any actions on the device.

If a cleaned up device checks in before its device certification expires, it reappears in the Intune admin center. Once the device certification expires, the device must go through a re-enrollment process for it to show in the Intune admin center.

## Device cleanup rules logging

The [Intune audit logs](../fundamentals/monitor-audit-logs.md) show the devices concealed by the device cleanup rules. In the logs, filter by **Activity name** > **Device set to be hidden from admin by Device Cleanup Rule [*YourRuleName*]**.

<!--links-->

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role