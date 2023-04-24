---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 04/24/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-device-group.md
pre-provisioning/hybrid-azure-ad-join-device-group.md
self-deploying/self-deploying-device-group.md
user-driven/azure-ad-join-device-group.md
user-driven/hybrid-azure-ad-join-device-group.md

Headings are driven by article context. -->

Device groups are a collection of devices organized into an Azure AD group. Device groups are used in Autopilot to target devices for specific configurations such as what policies to apply to a device and what applications to install on the device. They're also used by Autopilot to target Enrollment Status Page (ESP) configurations, Autopilot profile configurations, and domain join profiles to devices.

Device groups can be either dynamic or assigned:

- **Dynamic groups** - Devices are automatically added to the group based on rules
- **Assigned groups** - Devices are manually added to the group and are static

When an admin configures Autopilot in an enterprise environment, dynamic groups are primarily used since a large number of devices are usually involved. Adding the devices in automatically using rules makes management of the group a lot easier. Adding a large amount of device in manually via an assigned group would be impractical. However, if there's only a few devices, for example for testing purposes, an assigned group can also be used.

To create a dynamic device group for use with Autopilot, follow these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Groups** in the left hand pane.

3. In the **Groups | All groups** screen, make sure **All groups** is selected, and then select **New group**.

4. In the **New Group** screen that opens:

    1. For **Group type**, select **Security**.

    2. For **Group name**, enter a name for the device group.

    3. For **Group description**, enter a description for the device group.

    4. For **Azure AD roles can be assigned to the group**, select **No**.

    5. For **Membership type**, select **Dynamic Device**.

    6. For **Owners**, select users that own the group.

    7. For **Dynamic device members** (available once **Dynamic Device** is selected for **Membership type**), select **Add dynamic query**. Selecting **Add dynamic query** opens the **Dynamic membership rules** screen:

        1. Make sure that **Configure Rules** is selected at the top.

        2. Select **Add expression**. Rules and expressions can be added that defines what devices are added to the device group.

            Rules can be entered in the rule builder via the drop-down boxes or the rule syntax can be directly entered via the **Edit** option in the **Rule syntax** section.

            The most common type of dynamic device group when using Autopilot is a device group that contains all Autopilot devices. A dynamic device group that contains all Autopilot devices has the following syntax:

            `(device.devicePhysicalIDs -any (_ -contains "[ZTDID]"))`

            This rule can be entered in by selecting the **Edit** option in the **Rule syntax** section and then pasting in the rule in the **Edit rule syntax** screen under **Rule syntax**. Once the rule has been pasted in, select **OK**.

        3. Once the desired rule has been entered, select **Save** on the toolbar to close the **Dynamic membership rules** window.

            For more information on creating rules for dynamic groups, see [Dynamic membership rules for groups in Azure Active Directory](/azure/active-directory/enterprise-users/groups-dynamic-membership).

5. In the **New Group** screen, select **Create** which finishes creating the dynamic group.

> [!NOTE]
> The above steps are creating a dynamic group in Azure AD which is used by Intune and Autopilot. Although the groups can be accessed in the Intune portal, they are Azure AD groups.

> [!TIP]
> For Configuration Manager admins, device groups are similar to device based collections. Dynamic device groups are similar to query based device collections while assigned device groups are similar to direct membership device collections.
