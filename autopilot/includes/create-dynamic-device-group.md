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

tutorial/pre-provisioning/azure-ad-join-device-group.md
tutorial/pre-provisioning/hybrid-azure-ad-join-device-group.md
tutorial/self-deploying/self-deploying-device-group.md
tutorial/user-driven/azure-ad-join-device-group.md
tutorial/user-driven/hybrid-azure-ad-join-device-group.md
device-preparation/tutorial/user-driven/entra-join-automatic-enrollment.md

Headings are driven by article context. -->

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Groups** in the left hand pane.

1. In the **Groups | All groups** screen, make sure **All groups** is selected, and then select **New group**.

1. In the **New Group** screen that opens:

    1. For **Group type**, select **Security**.

    1. For **Group name**, enter a name for the device group.

    1. For **Group description**, enter a description for the device group.

    1. For **Microsoft Entra roles can be assigned to the group**, select **No**.

    1. For **Membership type**, select **Dynamic Device**. Setting the **Membership type** option to **Dynamic Device** changes the option **Members** to **Dynamic device members**.

    1. For **Owners**, select the **No owners selected** link.

    1. In the **Add owners** screen that opens:

       1. Scroll through the list of objects and select owners for the user group. Alternatively, use the **Search** bar to search for and select owners of the group.

       1. Once all of the desired owners are selected, select **Select**.

    1. For **Dynamic device members**, select **Add dynamic query**. The **Dynamic membership rules** screen opens.

    1. In the **Dynamic membership rules** screen:

        1. Make sure that **Configure Rules** is selected at the top.

        1. Select **Add expression**. Rules and expressions can be added that defines what devices are added to the device group.

            Rules can be entered in the rule builder via the drop-down boxes. Alternatively, the rule syntax can be entered directly via the **Edit** option in the **Rule syntax** section.

            The most common type of dynamic device group when using Windows Autopilot is a device group that contains all Windows Autopilot devices. A dynamic device group that contains all Windows Autopilot devices has the following syntax:

            `(device.devicePhysicalIDs -any (_ -startsWith "[ZTDid]"))`

            To enter in this rule:

            1. Select the **Edit** option in the **Rule syntax** section.

            1. Paste in the following rule in the **Edit rule syntax** screen under **Rule syntax**:

                `(device.devicePhysicalIDs -any (_ -startsWith "[ZTDid]"))`

            1. Once the rule is pasted in, select **OK**.

        1. Once the desired rule is entered, select **Save** on the toolbar to close the **Dynamic membership rules** window.

            For more information on creating rules for dynamic groups, see [Dynamic membership rules for groups in Microsoft Entra ID](/azure/active-directory/enterprise-users/groups-dynamic-membership).

    1. Select **Create** to finish creating the dynamic device group.

> [!NOTE]
>
> The above steps are creating a dynamic group in Microsoft Entra that is used by Intune and Windows Autopilot solutions. Although the groups can be accessed in the Intune portal, they're Microsoft Entra groups.

> [!TIP]
>
> For Configuration Manager admins, device groups are similar to device based collections. Dynamic device groups are similar to query based device collections while assigned device groups are similar to direct membership device collections.
