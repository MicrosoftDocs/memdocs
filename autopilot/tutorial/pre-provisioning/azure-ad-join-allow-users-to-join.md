---
title: Windows Autopilot for pre-provisioned deployment Microsoft Entra join - Step 2 of 9 - Allow users to join devices to Microsoft Entra ID
description: How to - Windows Autopilot for pre-provisioned deployment Microsoft Entra join - Step 2 of 9 - Allow users to join devices to Microsoft Entra ID.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/24/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Pre-provision Microsoft Entra join: Allow users to join devices to Microsoft Entra ID

Windows Autopilot for pre-provisioned deployment Microsoft Entra join steps:
- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
> [!div class="checklist"]
> - **Step 2: Allow users to join devices to Microsoft Entra ID**
- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
- Step 8: [Technician flow](azure-ad-join-technician-flow.md)
- Step 9: [User flow](azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment Microsoft Entra join workflow, see [Windows Autopilot for pre-provisioned deployment Microsoft Entra join overview](azure-ad-join-workflow.md#workflow)

> [!NOTE]
>
> If you have already allowed users to join devices to Microsoft Entra ID as part of the [Windows Autopilot user-driven Microsoft Entra join](../user-driven/azure-ad-join-workflow.md) scenario, you can skip this step and move on to [Step 3: Register devices as Autopilot devices](azure-ad-join-register-device.md).

<a name='allow-users-to-join-devices-to-azure-ad'></a>

## Allow users to join devices to Microsoft Entra ID

In order for Windows Autopilot to work, users need to be allowed to join devices to Microsoft Entra ID. Allowing users to join devices to Microsoft Entra ID can be configured in the Azure portal:

1. Sign in to the [Azure portal](https://portal.azure.com/).

1. Select **Microsoft Entra ID**.

1. In the **Overview** screen, under **Manage** in the left hand pane, select **Devices**.

1. In the **Devices | Overview** screen, select **Device Settings** in the left hand pane.

1. In the **Devices | Device settings** screen that opens, under **Users may join devices to Microsoft Entra**, select either **All** or **Selected**:

   - If **All** is selected, all users can join their devices to Microsoft Entra ID.

   - If **Some** is selected, only users specified under **Selected** can join their devices to Microsoft Entra ID. To add users:

      1. Select the link under **Selected**.

      1. In the **Members allowed to join devices** page that opens:

         1. Select **Add**.

         1. In the **Add members** window that opens:

            1. select the desired user(s) and/or group(s) to add.

            1. Once all of the desired users(s) and group(s) have been selected, select **Select** to close the **Add members** window.

         1. Select **OK**.

        > [!NOTE]
        >
        > Any selected groups must be a Microsoft Entra group that contains user objects.

1. In the **Devices | Overview** screen, if any changes were made, select **Save**.

> [!NOTE]
>
> This step of allowing users to join devices to Microsoft Entra ID is only needed for the Autopilot user-driven Microsoft Entra join and Autopilot for pre-provisioned deployment Microsoft Entra join scenarios. This setting doesn't apply to Microsoft Entra hybrid joined devices and Microsoft Entra joined devices using Windows Autopilot self-deployment mode as these methods work in a userless context.

## Next step: Register devices as Autopilot devices

> [!div class="nextstepaction"]
> [Step 3: Register devices as Autopilot devices](azure-ad-join-register-device.md)

## More information

For more information on allowing users to join devices to Microsoft Entra ID, see the following article(s):

- [Configure device settings](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
