---
title: Step by step tutorial for Windows Autopilot user-driven Azure AD join mode in Intune
description: Step by step tutorial for Windows Autopilot user-driven Azure AD join mode in Intune.
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

# Step by step tutorial for Windows Autopilot user-driven Azure AD join mode in Intune

*Applies to:*

- Windows 11
- Windows 10

## Overview

This step by step tutorial will guide you through using Intune to perform a Windows Autopilot user-driven scenario when the devices will be strictly Azure AD joined. The purpose of this tutorial is to provide in one article a step by step guide for all the steps required for a successful Autopilot user-driven Azure AD join deployment using Intune.

Before beginning, refer to the [How to: Plan your Azure AD join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all prerequisites are met for joining devices to Azure AD.

## Workflow

 Create device group > Configure and assign Autopilot Enrollment Status Page (ESP) > Create Autopilot profile > Assign Autopilot profile to device group > Import device > Assign Autopilot profile to device > Assign User to device (optional)

## Create a device group

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

## Configure and assign Autopilot Enrollment Status Page (ESP)

The next step is to make a decision regarding whether the Enrollment Status Page (ESP) will be used. The main feature of the ESP is that it displays progress and current status to the end user while the device is being set up and enrolled. It can also be used to block a user from using the device until all required policies and applications are installed. The ESP is recommended if the device has many policies and applications that need to be installed. If the ESP is not enabled in these scenarios, it may make end users think that that the device is hung during the setup process due to the amount of time it is taking with no progress or status being displayed.

To show the Autopilot Enrollment Status Page (ESP) during Autopilot, follow the below steps to configure and assign an ESP:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **By platform: Windows**

3. Select **Windows enrollment** > **General: Enrollment Status Page**.

4. In the **Enrollment Status Page**, select **Create**.

5. In the **Create profile** screen, under **Basics**, enter a **Name** and **Description** for the ESP profile, and then select **Next**.

6. In the **Create profile** screen, under **Settings**, toggle the option **Show app and profile configuration progress** to **Yes**.

7. After toggling the option **Show app and profile configuration progress** to **Yes**, several new options will appear. Configure these options based on the desired behavior for the ESP. Details on each of these options can be found in the article [Set up the Enrollment Status Page](/mem/intune/enrollment/windows-enrollment-status#create-new-profile).

8. Once the different ESP options under **Settings** have been configured as desired, select **Next**.

9. Under **Assignments**, select **Add groups**.

10. In the the **Select groups to include** pane, select the device group(s) to target the ESP profile. This normally would be the device group created in the section [Create a device group](#create-a-device-group). After selecting the device group, select **Select**.

    > [!TIP]
    >
    > After selecting the device group(s), you can select the **Edit filter** option on each device group added to the assignment to further refine what devices are targeted for the ESP profile. For example, this can be useful if you want to exclude some of the devices that are members in the device group(s) selected.

11. Select **Next**.  

12. Optionally, in **Scope tags**, assign a tag to limit profile management to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. Then select **Next**.   

    > [!NOTE]
    > Scope tags limit who can see and reprioritize ESP profiles in the admin center. A scoped user can tell the relative priority of their profile even if they can't see all of the other profiles in Intune. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](../../intune/fundamentals/scope-tags.md).  

13. In **Review + create**, review your settings. After you select **Create**, your changes are saved, and the profile is assigned. Once deployed, the profile will be applied the next time the devices check in. You can access the profile from your profiles list. 

> [!TIP]
> For Configuration Manager admins, an ESP is similar and analogous to ConfigMgr client settings.

[Windows Autopilot Enrollment Status Page](/mem/autopilot/enrollment-status)
[Set up the Enrollment Status Page](/mem/intune/enrollment/windows-enrollment-status)

## Create Autopilot profile

## Assign Autopilot profile to device group

## Import device

## Assign Autopilot profile to device

## More info

[Windows Autopilot user-driven mode](/mem/autopilot/user-driven)