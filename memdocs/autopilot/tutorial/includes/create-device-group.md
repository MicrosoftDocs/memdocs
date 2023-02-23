---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 02/23/2023
ms.localizationpriority: medium
---

Device groups are a collection of devices organized into a Azure AD group. Device groups are used in Autopilot to target devices for specific configurations such what policies to apply to a device and what applications to install on the device.

Device groups can either by dynamic or assigned:

- **Dynamic groups** - Devices are automatically added to the group based on rules
- **Assigned groups** - Devices are manually added to the group and are static

When configuring Autopilot, dynamic groups are primarily used since a large number of devices are usually involved. Adding the devices in automatically rules makes management of the group a lot easier. Adding a large amount of device in manually via an assigned group would be impractical. However, if there is a small number of devices, for example for testing purposes, an assigned group can also be used.

To create a dynamic device group for use with Autopilot, follow the below steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Groups** > **New group**.

3. In the **New Group** screen, configure the following properties:

    1. **Group type**: Select **Security**.

    2. **Group name** and **Group description**: Enter a name and description for the device group.

    3. **Azure AD roles can be assigned to the group**: Select **No**.

    4. **Membership type**: Select **Dynamic Device**.

    5. **Owners**: Select users that own the group.

    6. **Dynamic device members**: Select **Add dynamic query**. In the **Dynamic membership rules** screen, select **Add expression**.

      > [!NOTE]
      > When selecting **Dynamic Device** in step d, this field will change to **Dynamic device members**.

      Rules on what devices will be added to the device group are entered in the **Dynamic membership rules** screen under **Configure Rules**. Rules can be entered in the rule builder via the drop down boxes or the rule syntax can be directly entered via the **Edit** option in the **Rule syntax** section.

      The most common type of dynamic device group when using Autopilot is a device group that contains all Autopilot devices. A dynamic device group that contains all Autopilot devices has the following syntax:

      `(device.devicePhysicalIDs -any (_ -contains "[ZTDID]"))`

      This rule can be entered in by selecting the **Edit** option in the **Rule syntax** section and then pasting in the rule in the **Edit rule syntax** screen under **Rule syntax**. Once the rule has been pasted in, select **OK**, and then select **Save**.

      For more information on creating rules for dynamic groups, see [Dynamic membership rules for groups in Azure Active Directory](/azure/active-directory/enterprise-users/groups-dynamic-membership).

4. Once the dynamic rule has been entered and saved, in the **New Group** screen, select **Create**. This will finish creating the dynamic group.

> [!NOTE]
> The above steps are creating a dynamic group in Azure AD which is used by Intune and Autopilot. Although the groups can be accessed in the Intune portal, they are Azure AD groups.

> [!TIP]
> For Configuration Manager admins, device groups are similar to device based collections. Dynamic device groups are similar to query based device collections while assigned device groups are similar to direct membership device collections.

For more information on creating groups in Intune, see the following articles:

- [Create device groups](/mem/autopilot/enrollment-autopilot)
- [Add groups to organize users and devices](/mem/intune/fundamentals/groups-add)
- [Manage Azure Active Directory groups and group membership](/azure/active-directory/fundamentals/how-to-manage-groups)