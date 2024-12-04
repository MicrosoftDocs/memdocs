---
# required metadata

title: Remove apps and configurations from devices
titleSuffix: Microsoft Intune
description: Learn how apps and configurations can be removed temporarily, then restored automatically or manually using the Remove apps and configuration device action by the IT administrator.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 07/10/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#customerIntent: As an IT admin, I want to remove an app or a configuration using the Remove apps and configuration device action so that I can make changes on a device for troubleshooting or maintenance.
ms.reviewer: Jack Poehlman
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Remove apps and configurations from devices

**Remove apps and configuration** is a single device action used to uninstall applications or remove a configuration item from a device. With this new device action, Intune can temporarily remove applications and configuration from a single device. When ready, you can initiate a **Restore** action to return the removed item to the device. Removed items are automatically restored to devices in 8-24 hours in cases where an admin does not initiate a **Restore** action to ensure that devices remain consistent with assignment intents.  

This action aims to resolve the issues that customers face outside of Intune and swiftly bring back end-user efficiency.

## Supported platforms

- **iOS/iPadOS**: Applicable to any iOS or iPadOS Intune managed device.

- **Android Enterprise**: Applicable to dedicated devices, fully-managed, and corporate-owned work profile devices.  

> [!NOTE]
> Not supported:
> - Android Enterprise Personally-Owned Work Profile managed devices
> - Android device administrator (DA)
> - Android Open Source Project (AOSP)

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

**Permissions**: To use the **Remove apps and configuration** device action, you require the following permissions:
 
 - **Organization: Read** permission is needed.
 - **Remote tasks: Change assignments**. Set the Permission to **yes** to enable the action. With the permission set to **Yes**, IT admins can initiate a **Change Assignments** action. 

The administrator can:

- select and remove assigned applications and configuration from a device.

- select and restore previously removed applications and configuration from a device.

For more information on custom roles, see: [Create a custom role in Intune]( ../fundamentals/create-custom-role.md)

The **Change assignments** permission is granted to these [Built-In Intune roles]( ../fundamentals/scope-tags.md)

- School Administrator

- Help Desk Operator

**Scope Tags**: Remove Apps and Configuration will limit an admin's view of applications and configurations based on the Scope Tag assignments of the admin's role. For more information on Scope tags, see [Use role-based access control and scope tags for distributed IT]( ../fundamentals/scope-tags.md).

## How to remove apps and configuration?

1. Sign in to the [Microsoft Intune admin center]( https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices**, and then select **All devices or the device platform**.

3. From the list of devices you manage, select a [supported device](#supported-platforms).

4. From the buttons, choose **Remove apps and configuration**. Use the **⋯** overflow menu.

  :::image type="content" alt-text="Remove apps and configuration" source="./media/remove-apps-config/remove-apps-config.png" lightbox="./media/remove-apps-config/remove-apps-config.png":::

5. Select **+ Add**, then select the type of item to remove; **Configuration Item** or **App**.  
  
  :::image type="content" alt-text="Add apps or configuration to remove" source="./media/remove-apps-config/remove-apps-config-add.png" lightbox="./media/remove-apps-config/remove-apps-config-add.png":::
6. A list of applicable items is displayed with its current state on the device. Select an item to remove, and then use **Select**.

7. The list of selected items is displayed for review; add or delete using the check boxes and header controls. When satisfied with the item list, select **Next**.

8. The Review + Remove page is displayed for review, when ready to initiate the remove action, select **Remove**.

9. After the action is initiated, you'll be directed to the **Monitor and restore** page. The **Remove** action is initiated for devices that are powered and actively connected to an internet-enabled network; the selected items are removed as soon as possible.
  
  :::image type="content" alt-text="Status and action" source="./media/remove-apps-config/remove-apps-config-action.png" lightbox="./media/remove-apps-config/remove-apps-config-action.png":::

> [!IMPORTANT]
> Removal of items such as Wi-Fi, VPN, and Certificates could impact device connectivity, if the items are ultimately used for connectivity to the Intune service. **Remove apps and configuration** is intended to be used interactively by Intune admins working with impacted end users.  If connectivity is lost, end users may need to take actions on devices to restore connectivity; connect the device to a guest or alternate Wi-Fi or Cellular network.

## Monitoring the device action remove apps and configuration

After you initiate the **Remove apps and configuration** action on a device, the **Status** column of the **Overview** page displays the status of the action. The status is updated as the action progresses.  

Removed items are automatically restored to devices in 8-24 hours in cases where an admin does not initiate a **Restore** action to ensure that devices remain consistent with assignment intents.

:::image type="content" alt-text="Monitor the device action - Remove apps and configuration" source="./media/remove-apps-config/remove-apps-config-monitor.png" lightbox="./media/remove-apps-config/remove-apps-config-monitor.png":::

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

