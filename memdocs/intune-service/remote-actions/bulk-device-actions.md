---
# required metadata

title: Use bulk device actions in Microsoft Intune device.
titleSuffix:
description: Use bulk remote device actions.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 02/27/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jlynn 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Use bulk device actions

You can use bulk device actions for the following remote actions:

- [Autopilot reset](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [Collect diagnostics](collect-diagnostics.md)
- [Custom notifications](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [Delete](devices-wipe.md#delete-devices-from-the-intune-admin-center)
- [Rename](device-rename.md)
- [Restart](device-restart.md)
- [Retire](devices-wipe.md#retire)
- [Sync](device-sync.md)
- [Wipe](devices-wipe.md#wipe)
- [Update cellular data plan](update-cellular-data-plan.md)

Most actions support up to 100 devices. For specific details of each remote action, like options or platform support, see the help page for each.

## Use a bulk device action

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Choose **Devices** > **All devices** > **Bulk Device Actions**.
![Bulk device actions](./media/bulk-device-actions/bulk-device-actions.png)
3. On the **Bulk device action** page, select an **OS** and **Device action**. Some device actions have more options or fields to populate. Choose **Next**.
4. On the **Devices** page, select up to maximum number of devices that the action supports > **Next**.
5. On the **Review + create** page, select **Create**.

## Next steps

[Device management overview.](device-management.md)
