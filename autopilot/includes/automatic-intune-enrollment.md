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

tutorial/pre-provisioning/azure-ad-join-automatic-enrollment.md
tutorial/pre-provisioning/hybrid-azure-ad-join-automatic-enrollment.md
tutorial/self-deploying/self-deploying-automatic-enrollment.md
tutorial/user-driven/azure-ad-join-automatic-enrollment.md
tutorial/user-driven/hybrid-azure-ad-join-automatic-enrollment.md
device-preparation/tutorial/user-driven/entra-join-automatic-enrollment.md

Headings are driven by article context. -->

1. Sign in to the [Azure portal](https://portal.azure.com/).

1. Select **Microsoft Entra ID**.

1. In the **Overview** screen, under **Manage** in the left hand pane, select **Mobility (MDM and MAM)**.

1. In the **Mobility (MDM and MAM)** screen, select **Microsoft Intune**.

1. In the **Configure** page that opens, next to **MDM user scope**, select either **All** or **Some**:

   - If **All** is selected, all users can automatically enroll their devices in Intune.

   - If **Some** is selected, only users specified in the group(s) next to **Groups** can automatically enroll their devices in Intune. To add groups:

      1. Select the link next to **Groups**.
      1. In the **Select groups** window that opens, select the desired group(s) to add.
      1. Once all of the desired group(s) have been selected, select **Select** to close the **Select groups** window.

        > [!NOTE]
        >
        > The group(s) selected must be a Microsoft Entra group that contains user objects.

1. In the **Configure** screen, if any changes were made, select **Save**.

> [!TIP]
>
> For Configuration Manager Admins, this process is similar to the Configuration Manager client automatically registering with a site so that the device can be managed.
