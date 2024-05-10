---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-deploy
ms.service: windows-client
ms.topic: include
ms.date: 05/09/2024
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
