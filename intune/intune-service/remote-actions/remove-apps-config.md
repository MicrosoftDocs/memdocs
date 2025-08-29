---
# required metadata

title: Remove Apps and Configuration
description: Learn how apps and configurations can be removed temporarily, then restored automatically or manually using the Remove apps and configuration device action by the IT administrator.
ms.date: 08/27/2025
ms.topic: how-to
#customerIntent: As an IT admin, I want to remove an app or a configuration using the Remove apps and configuration device action so that I can make changes on a device for troubleshooting or maintenance.
ms.reviewer: Jack Poehlman
ms.custom: intune-azure; get-started
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Remove apps and configuration from devices

**Remove apps and configuration** is a remote action used to uninstall applications and remove configurations from a device. With this action, Intune can temporarily remove apps and configurations from a single device. When ready, you can initiate a **Restore** action to return the removed item to the device. Removed items are automatically restored to devices in 8-24 hours in cases where an admin does not initiate a **Restore** action to ensure that devices remain consistent with assignment intents.

This action aims to resolve the issues that customers face outside of Intune and swiftly bring back end-user efficiency.

## Requirements

### :::image type="icon" source="../media/icons/headers/devices.svg" border="false"::: Platform requirements

> [!div class="checklist"]
> This remote action is supported on the following platforms:
>
> - Android
>     - Android Enterprise corporate-owned dedicated (COSU)
>     - Android Enterprise corporate-owned fully managed (COBO)
>     - Android Enterprise corporate-owned work profile (COPE)
> - iOS/iPadOS

### :::image type="icon" source="../media/icons/headers/rbac.svg" border="false"::: Role and permission requirements

> [!div class="checklist"]
> To execute this remote action, at a minimum, use an account that has one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Ramote tasks/Change assignments**
>   - Appropriate permissions that grant visibility into and access to devices within Intune (e.g., Managed devices/Read, Update)

## Supported items

**Applications**: Any Intune delivered application on the supported device platforms.

**Configuration**: Intune delivered configuration profiles.

#### [iOS](#tab/iOS)

- Profile type, Settings catalog: All
- Profile type
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

#### [Android](#tab/android)

- Profile Type:
  - Device restrictions
  - PKCS certificate
  - PKCS import certificate
  - SCEP certificate
  - Trusted certificate
  - VPN
  - Wi-Fi

---

## Permissions for Remove apps and configurations

The administrator can:

- select and remove assigned applications and configuration from a device.
- select and restore previously removed applications and configuration from a device.

For more information on custom roles, see: [Create a custom role in Intune]( ../fundamentals/create-custom-role.md)



**Scope Tags**: Remove Apps and Configuration will limit an admin's view of applications and configurations based on the Scope Tag assignments of the admin's role. For more information on Scope tags, see [Use role-based access control and scope tags for distributed IT]( ../fundamentals/scope-tags.md).

## How to remove apps and configuration?

1. Sign in to the [Microsoft Intune admin center]( https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Devices**, and then select **All devices or the device platform**.
1. From the list of devices you manage, select a device.
1. From the buttons, choose **Remove apps and configuration**. Use the **⋯** overflow menu.

  :::image type="content" alt-text="Remove apps and configuration" source="images/remove-apps-config.png" lightbox="images/remove-apps-config.png":::

1. Select **+ Add**, then select the type of item to remove; **Configuration Item** or **App**.

  :::image type="content" alt-text="Add apps or configuration to remove" source="images/remove-apps-config-add.png" lightbox="images/remove-apps-config-add.png":::
1. A list of applicable items is displayed with its current state on the device. Select an item to remove, and then use **Select**.
1. The list of selected items is displayed for review; add or delete using the check boxes and header controls. When satisfied with the item list, select **Next**.
1. The Review + Remove page is displayed for review, when ready to initiate the remove action, select **Remove**.
1. After the action is initiated, you'll be directed to the **Monitor and restore** page. The **Remove** action is initiated for devices that are powered and actively connected to an internet-enabled network; the selected items are removed as soon as possible.

  :::image type="content" alt-text="Status and action" source="images/remove-apps-config-action.png" lightbox="images/remove-apps-config-action.png":::

> [!IMPORTANT]
> Removal of items such as Wi-Fi, VPN, and Certificates could impact device connectivity, if the items are ultimately used for connectivity to the Intune service. **Remove apps and configuration** is intended to be used interactively by Intune admins working with impacted end users.  If connectivity is lost, end users may need to take actions on devices to restore connectivity; connect the device to a guest or alternate Wi-Fi or Cellular network.

## Monitoring the device action remove apps and configuration

After you initiate the **Remove apps and configuration** action on a device, the **Status** column of the **Overview** page displays the status of the action. The status is updated as the action progresses.

Removed items are automatically restored to devices in 8-24 hours in cases where an admin does not initiate a **Restore** action to ensure that devices remain consistent with assignment intents.

:::image type="content" alt-text="Monitor the device action - Remove apps and configuration" source="images/remove-apps-config-monitor.png" lightbox="images/remove-apps-config-monitor.png":::

> [!IMPORTANT]
> Removed items are reflected with an assignment status of *Removed*, but this status is not included in the count. Removals are temporary and will be automatically restored to devices.  The total count is not inclusive of devices with an active *Removed* status.

The monitoring page displays the following information:

#### [Available actions](#tab/available-actions)

**Add**: add more items for removal.

**Refresh**: refresh the list and track progression of remove / restore.

**Columns**: disable / enable columns.

**Restore all**: restore all removed items in the list. When you select the **Restore all** button in the table header, a confirmation box is displayed. When ready, select **Restore all** initiate restoration of all Removed apps or configurations to the device.

**Restore select items**: restore selected items in the list. Select one or more items using the selection check box and then select the **Restore** button to initiate the restore of selected items or Configurations to the device.

**Last refreshed on**: shows the timestamp of when the list was last refreshed.

#### [Display columns](#tab/display-columns)

**Name**: application or policy name

**Item type**: application or policy type

**Action**: current action for the item

**Started**: date/time stamp when the action was initiated

**Status**:

- **In Progress**: remove attempt to device initiated, pending response
- **Removed**: item removed from device
- **Restored**: item restored to device
- **Error**: action resulted in error, see status details

**Status time**: date/timestamp when the status was updated

**Status detail**: when populated, shows more details for the status

---

## Reference links

- Microsoft Graph API: [changeAssignments action][GRAPH-1] in the Microsoft Graph API documentation.

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[GRAPH-1]: /graph/api/intune-devices-manageddevice-changeassignments
