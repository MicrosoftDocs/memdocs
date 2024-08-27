---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/19/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

tutorial/pre-provisioning/azure-ad-join-allow-users-to-join.md
tutorial/user-driven/azure-ad-join-allow-users-to-join.md
device-preparation/tutorial/user-driven/entra-join-allow-users-to-join.md

Headings are driven by article context. -->

1. Sign in to the [Azure portal](https://portal.azure.com/).

1. Select **Microsoft Entra ID**.

1. In the **Overview** screen, under **Manage** in the left hand pane, select **Devices**.

1. In the **Devices | Overview** screen, under **Manage** in the left hand pane, select **Device Settings**.

1. In the **Devices | Device settings** screen that opens, under **Users may join devices to Microsoft Entra**, select either **All** or **Selected**:

   - If **All** is selected, all users can join their devices to Microsoft Entra ID.

   - If **Some** is selected, only users specified under **Selected** can join their devices to Microsoft Entra ID. To add users:

      1. Select the link under **Selected**.

      1. In the **Members allowed to join devices** page that opens:

         1. Select **Add**.

         1. In the **Add members** window that opens:

            1. Select the desired users and/or groups to add.

            1. Once all of the desired users and groups are selected, select **Select** to close the **Add members** window.

         1. Select **OK**.

        > [!NOTE]
        >
        > Any selected groups must be a Microsoft Entra group that contains user objects.

1. In the **Devices | Overview** screen, if any changes were made, select **Save**.
