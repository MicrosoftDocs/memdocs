---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/19/2024
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

1. In the **Overview** screen, under **Manage** in the left hand pane, select **Mobility (MDM and WIP)**.

1. In the **Mobility (MDM and WIP)** screen, under **Name** select **Microsoft Intune**.

1. In the **Microsoft Intune** page that opens, under **MDM user scope**, select either **All** or **Some**:

   - If **All** is selected, all users can automatically enroll their devices in Intune.

   - If **Some** is selected, only users in the groups specified in the link under **Groups** can automatically enroll their devices in Intune. To add groups:

      1. Select the link under **Groups**.

      1. In the **Select groups** window that opens, select the desired groups to add. Make sure that the groups selected are Microsoft Entra user groups that contain the desired users.

      1. Once all of the desired groups are selected, select **Select** to close the **Select groups** window.

1. In the **Microsoft Intune** screen, if any changes were made, select **Save**.
