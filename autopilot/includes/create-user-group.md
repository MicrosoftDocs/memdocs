---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/03/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

device-preparation/tutorial/user-driven/entra-join-user-group.md

Headings are driven by article context. -->

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Groups** in the left hand pane.

1. In the **Groups | All groups** screen, make sure **All groups** is selected, and then select **New group**.

1. In the **New Group** screen that opens:

    1. For **Group type**, select **Security**.

    1. For **Group name**, enter a name for the user group, such as **Windows Autopilot device preparation user group**.

    1. For **Group description**, enter a description for the user group.

    1. For **Microsoft Entra roles can be assigned to the group**, select **No**.

    1. For **Membership type**:

       - Select **Assigned** to create an assigned user group.
       - Select **Dynamic User** to create a dynamic user group.

    1. For **Owners**, select the **No owners selected** link.

    1. In the **Add owners** screen that opens:

       1. Scroll through the list of objects and select owners for the user group. Alternatively, use the **Search** bar to search for and select owners of the group.

       1. Once all of the desired owners are selected, select **Select**.

    1. For assigned user groups:

       1. For **Members**, select the **No members selected** link.

       1. In the **Add members** screen that opens:

          1. Scroll through the list of objects and select members that the Windows Autopilot device preparation profiles should be deployed to. Alternatively, use the **Search** bar to search for and select members for the group. Make sure to only select users or groups that only contain users.

          1. Once all of the desired users or user groups are selected that the Windows Autopilot device preparation profiles should be deployed to, select **Select**.

    1. For dynamic user groups:

       1. For **Dynamic user members**, select the **Add dynamic query** link.

       1. In the **Dynamic membership rules** screen that opens, create a rule that encompasses the users that should be members of the user group. For more information on creating rules, see [Dynamic membership rules for groups in Microsoft Entra ID](/entra/identity/users/groups-dynamic-membership).

        > [!NOTE]
        >
        > The linked article is in regards to creating dynamic membership rules in Microsoft Entra ID. However, dynamic user groups in Intune are also dynamic user groups in Microsoft Entra ID, so the rule syntax is the same.

    1. Select **Create** to finish creating user group.
