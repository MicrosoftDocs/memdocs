---
title: Windows Autopilot user-driven Azure AD join - Step 2 of 7 - Allow users to join devices to Azure AD
description: How to - Windows Autopilot user-driven Azure AD join - Step 2 of 7 - Allow users to join devices to Azure AD.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 03/08/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# User-driven Azure AD join: Allow users to join devices to Azure AD

Autopilot user-driven Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
> [!div class="checklist"]
> - **Step 2: Allow users to join devices to Azure AD**
- Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
- Step 4: [Create a device group](azure-ad-join-device-group.md)
- Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
- Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
- Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)

For an overview of the Windows Autopilot user-driven Azure AD join workflow, see [Windows Autopilot user-driven Azure AD join overview](azure-ad-join-workflow.md)

## Allow users to join devices to Azure AD

In order for Windows Autopilot to work, users need to be allowed to join devices to Azure AD. Allowing users to join devices to Azure Ad can be configured in the Azure portal:

1. Sign in to the [Azure portal](https://portal.azure.com/).

1. Select **Azure Active Directory**.

1. In the **Overview** screen, under **Manage** in the left hand pane, select **Devices**.

1. In the **Devices | Overview** screen, select **Device Settings** in the left hand pane.

1. In the **Devices | Device settings** screen that opens, under **Users may join devices to Azure AD**, select either **All** or **Selected**:

   - If **All** is selected, all users can join their devices to Azure AD.

   - If **Some** is selected, only users specified under **Selected** can join their devices to Azure AD. To add users:

      1. Select the link under **Selected**.

      1. In the **Members allowed to join devices** page that opens:
 
         1. Select **Add**.

         2. In the **Add members** window that opens:

            1. select the desired user(s) and/or group(s) to add.

            2. Once all of the desired users(s) and group(s) have been selected, select **Select** to close the **Add members** window.

         3. Select **OK**.

        > [!NOTE]
        >
        > Any selected groups must be an Azure AD group that contains user objects.

1. In the **Devices | Overview** screen, if any changes were made, select **Save**.

> [!NOTE]
>
> This step of allowing users to join devices to Azure AD is only needed for the user-driven Azure AD join scenario. This setting doesn't apply to hybrid Azure AD joined devices and Azure AD joined devices using Windows Autopilot self-deployment mode as these methods work in a userless context.

## Next step: Register devices as Autopilot devices

> [!div class="nextstepaction"]
> [Step 3: Register devices as Autopilot devices](azure-ad-join-register-device.md)

## More information

For more information on allowing users to join devices to Azure AD, see the following article(s):

- [Configure device settings](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
