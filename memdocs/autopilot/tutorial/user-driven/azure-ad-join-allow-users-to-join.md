---
title: Windows Autopilot user-driven Azure AD join - Step 2 of 7 - Allow users to join devices to Azure AD
description: How to - Windows Autopilot user-driven Azure AD join - Step 2 of 7 - Allow users to join devices to Azure AD.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 02/13/2023
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

In order for Windows Autopilot to work, users need to be allowed to join devices to Azure AD. This can be configured in the Azure portal:

1. Sign in to the [Azure portal](https://portal.azure.com/).

2. Select **Azure Active Directory**.

3. In the **Overview** screen, under **Manage**, select **Devices**.

4. In the **Devices | Overview** screen, select **Device Settings**.

5. In the **Devices | Device settings** screen, under **Users may join devices to Azure AD**, select either **All** or **Selected**:

   - If **All** is selected, all users can join their devices to Azure AD.

   - If **Some** is selected, only users specified under **Selected** can join their devices to Azure AD. To add users::

      1. Select the link under **Selected**.
      2. In the **Members alowed to join devices** page, select **Add**.
      3. In the **Add members** pane, select the desired user(s) and/or group(s) to add.
      4. Once all of the desired users(s) and group(s) have been selected, select **Select**.
      5. In the **Members alowed to join devices** page, select **OK**.

        > [!NOTE]
        >
        > If group(s) are selected, the group(s) must be an Azure AD group that contains user objects.

6. In the **Devices | Overview** screen, if any changes were made, select **Save**.

> [!NOTE]
>
> This step of allowing users to join devices to Azure AD is only needed for the user-driven Azure AD join scenario. This setting doesn't apply to hybrid Azure AD joined devices and Azure AD joined devices using Windows Autopilot self-deployment mode as these methods work in a userless context.

## Next step: Register devices as Autopilot devices

> [!div class="nextstepaction"]
> [Step 3: Register devices as Autopilot devices](azure-ad-join-register-device.md)

## More information

For more information on allowing users to join devices to Azure AD, see the following article(s):

- [Configure device settings](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
