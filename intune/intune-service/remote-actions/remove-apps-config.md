---
title: "Remote Device Action: Remove Apps and Configuration"
description: Learn how apps and configurations can be removed temporarily, then restored automatically or manually using the Remove apps and configuration device action with Intune.
ms.date: 10/27/2025
ms.topic: how-to
ms.reviewer: Jack Poehlman
zone_pivot_groups: 22f7442d-9384-49c8-abff-aaa058b30589
---

# Remote device action: remove apps and configuration

Use the *remove apps and configuration* remote action in Intune to uninstall apps and remove configuration profiles from a device. This action is useful for troubleshooting or temporarily removing settings that might be causing issues.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> This remote action supports the following platforms:
> - Android Enterprise corporate-owned dedicated (COSU)
> - Android Enterprise corporate-owned fully managed (COBO)
> - Android Enterprise corporate-owned work profile (COPE)
> - iOS/iPadOS

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::

[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> To execute this remote action, at a minimum, use an account that has one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Ramote tasks/Change assignments**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)
:::column-end:::
:::row-end:::
#### Admin permissions and scope tags for Remove apps and configuration

Admins can use the **Remove apps and configuration** remote action to:

- Select and remove assigned apps and configuration profiles from a device.
- Restore previously removed apps and configuration profiles.

##### Scope tags

Scope tags limit which apps and configurations an admin can view and manage. The visibility is based on the scope tag assignments defined in the admin's role. For more information, see [Use role-based access control and scope tags for distributed IT]( ../fundamentals/scope-tags.md).

## Supported apps and configuration profiles

This remote action supports the following items:

- **Applications**: Any Intune-delivered app on supported device platforms.
::: zone pivot="ios"
- **Configuration profiles**: Intune-delivered profiles, including:
  - Settings catalog: All
  - Custom
  - Devices features
  - Device restrictions
  - Email
  - PKCS certificate
  - PKCS import certificate
  - SCEP certificate
  - Trusted certificate
  - VPN
  - Wi-Fi

> [!NOTE]
> DDM-based policies are not supported for this device action.

::: zone-end
::: zone pivot="android"
- **Configuration profiles**: Intune-delivered profiles, including:
  - Device restrictions
  - PKCS certificate
  - PKCS import certificate
  - SCEP certificate
  - Trusted certificate
  - VPN
  - Wi-Fi
::: zone-end

## How to remove apps and configuration from the Intune admin center

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Remove apps and configuration**.

  :::image type="content" alt-text="Remove apps and configuration" source="images/remove-apps-config.png" lightbox="images/remove-apps-config.png":::

1. Select **+ Add**, then select the type of item to remove; **Configuration Item** or **App**.
1. A list of applicable items is displayed with its current state on the device. Select an item to remove, and then use **Select**.
1. The list of selected items is displayed for review; add or delete using the check boxes and header controls. When satisfied with the item list, select **Next**.
1. The **Review + Remove** page is displayed for review, when ready to initiate the remove action, select **Remove**.
1. After the action is initiated, you're redirected to the **Monitor and restore** page. The **Remove** action is initiated for devices that are powered and actively connected to an internet-enabled network; the selected items are removed as soon as possible.

> [!IMPORTANT]
> Removal of items such as Wi-Fi, VPN, and Certificates could impact device connectivity, if the items are ultimately used for connectivity to the Intune service. **Remove apps and configuration** is intended to be used interactively by Intune admins working with impacted users.  If connectivity is lost, users might need to take actions on devices to restore connectivity; connect the device to a guest or alternate Wi-Fi or cellular network.

## Monitoring the device action remove apps and configuration

After you initiate the **Remove apps and configuration** action on a device, the **Status** column of the **Overview** page displays the status of the action. The status is updated as the action progresses.

You can manually restore the removed items using the **Restore** action. If no restore is initiated, Intune automatically reapplies the apps and configurations within 8-24 hours to ensure the device remains aligned with assignment intent.

:::image type="content" alt-text="Monitor the device action - Remove apps and configuration" source="images/remove-apps-config-monitor.png" lightbox="images/remove-apps-config-monitor.png":::

> [!IMPORTANT]
> Removed items are reflected with an assignment status of *Removed*, but this status is not included in the count. Removals are temporary and will be automatically restored to devices.  The total count is not inclusive of devices with an active *Removed* status.

The monitoring page displays the following information:

- Available actions

    | Action | Description |
    |--|--|
    | **Add** | Add more items for removal |
    | **Refresh** | Refresh the list and track progression of remove/ restore. |
    | **Columns** | Enable/disable columns. |
    | **Restore all** | Restore all removed items in the list. When you select the **Restore all** button in the table header, a confirmation     box is displayed. When ready, select **Restore all** initiate restoration of all Removed apps or configurations to the device. |
    | **Restore select items** | Restore selected items in the list. Select one or more items using the selection check box and then select     the **Restore** button to initiate the restore of selected items or Configurations to the device. |
    | **Last refreshed on** | Shows the timestamp of when the list was last refreshed. |

- Display columns:

    | Column name | Description |
    |--|--|
    | **Name** | Application or policy name |
    | **Item type** | Application or policy type |
    | **Action** | Current action for the item |
    | **Started** | Date/time stamp when the action was initiated |
    | **Status** | - **In Progress**: remove attempt to device initiated, pending response<br>- **Removed**: item removed from device<br>-     **Restored**: item restored to device<br>- **Error**: action resulted in error, see status details |
    | **Status time** | Date/timestamp when the status was updated |
    | **Status detail** | When populated, shows more details for the status |

## Reference links

- Microsoft Graph API: [changeAssignments action][GRAPH-1] in the Microsoft Graph API documentation.

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[GRAPH-1]: /graph/api/intune-devices-manageddevice-changeassignments
