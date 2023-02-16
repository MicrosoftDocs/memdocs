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

Register/import devices as Autopilot devices > Create device group > Configure and assign Autopilot Enrollment Status Page (ESP) > Create Autopilot profile > Assign Autopilot profile to device group > Assign Autopilot profile to device > Assign User to device (optional)

## Register devices as Autopilot devices

Before a device can use Autopilot, it must be registered as an Autopilot device. Registering a devices as an Autopilot device can be thought of as importing the device into Autopilot so that Autopilot can be used on the device. It does not mean that the device has ever used the Autopilot service. It just makes the Autopilot service available to the device.

Also note that an Autopilot device is not the same thing as a registered or enrolled device in either Intune or in Azure AD. An Autopilot device can either be an existing registered/enrolled device in Intune/Azure AD, or it can be a new device that has not been registered/enrolled in Intune/Azure AD yet. For example the device can be a newly shipped device from an OEM that has never accessed the environment in the past.

There are several methods to register a device as an Autopilot device in Intune:

- Manually registering devices into Intune as an Autopilot device via the hardware hash. The hardware hash of a device can be collected via one of the following methods:

  - [Configuration Manager](/mem/configmgr/comanage/how-to-prepare-Win10#windows-autopilot)
  - [PowerShell script](/mem/autopilot/add-devices#powershell)
  - [Diagnostics page hash export](/mem/autopilot/add-devices#diagnostics-page-hash-export)
  - [Desktop hash export](/mem/autopilot/add-devices#desktop-hash-export)
  
  The above methods of obtaining the hardware hash of a device well documented. The corresponding documentation can be reached by selecting the appropriate option listed above.

- Automatically registering device by either an [OEM](/mem/autopilot/oem-registration), including [Microsoft Surface](/surface/surface-autopilot-registration-support) devices, or a [partner](/mem/autopilot/partner-registration)

  Registering a device via an OEM or partner is also well documented. The corresponding documentation can be reached by selecting the appropriate option listed above.

For most organizations, using an OEM or partner to register devices as Autopilot devices is the preferred, most common, and more secure method. However for smaller organizations, for testing/lab scenarios, and for emergency scenarios, manually registering devices as Autopilot devices via the hardware hash is also often used.

Several of the above methods on obtaining the hardware hash when manually registering devices as Autopilot devices will produce a CSV file with the hardware hash. This CSV file needs to be imported into Intune to register the device as an Autopilot device.

After the CSV files has been created, it can be imported into Intune via the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **By platform: Windows**.

3. Select **Windows enrollment** > **Windows Autopilot Deployment Program: Devices**.

4. In the **Windows Autopilot devices** screen, select **Import**.

5. In the **Add Windows Autopilot devices** pane, under **Specify the path to the list you want to import.**, select the blue select a file folder.

6. Browse to the CSV file obtained using one of the above methods to obtain the hardware hash of a device.

7. After selecting the CSV file, verify that the correct CSV file is selected under **Specify the path to the list you want to import.**, and then select **Import**. Importing can take several minutes.



8. After import is complete, select **Devices** > **Windows** > **Windows enrollment** > **Devices** (under **Windows Autopilot Deployment Program**) > **Sync**. 

   A message says that the synchronization is in progress. The process might take a few minutes to complete, depending on how many devices are being synchronized.

9. Refresh the view to see the new devices.

For more information on registering devices as Autopilot devices, see the following articles:

[Manually register devices with Windows Autopilot](/mem/autopilot/add-devices)

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

6. Under **Settings**, toggle the option **Show app and profile configuration progress** to **Yes**.

7. After toggling the option **Show app and profile configuration progress** to **Yes**, several new options will appear. Configure these options based on the desired behavior for the ESP. Details on each of these options can be found in the article [Set up the Enrollment Status Page](/mem/intune/enrollment/windows-enrollment-status#create-new-profile).

8. Once the different ESP options under **Settings** have been configured as desired, select **Next**.

9. Under **Assignments**, select **Add groups**.

10. In the the **Select groups to include** pane, select the device group(s) to target the ESP profile. This normally would be the device group(s) created in the section [Create a device group](#create-a-device-group). After selecting the device group, select **Select**.

    > [!TIP]
    >
    > After selecting the device group(s), you can select the **Edit filter** option on each device group added to the assignment to further refine what devices are targeted for the ESP profile. For example, this can be useful if you want to exclude some of the devices that are members in the device group(s) selected.

    > [!NOTE]
    >
    > As explained in this step, ESPs are assigned to device groups and not directly to individual devices. To assign an ESP to a specific device, the device must be a member of a device group that has the ESP assigned to it.

11. Select **Next**.  

12. Under **Scope tags**, select **Next**.

    > [!NOTE]
    > **Scope tags** are optional and are a method to control who has access to the ESP configuration. For the purpose of this tutorial, scope tags is being skipped and left at the default scope tag. However if a custom scope tag needs to be specified, do so at this screen. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](/mem/intune/fundamentals/scope-tags).

13. Under **Review + create**, review the settings and verify everything is correct and configured as desired. Once verified, select **Create** to save the changes and assign the ESP profile.

> [!TIP]
> For Configuration Manager admins, an ESP is similar and analogous to ConfigMgr client settings.

For more information on the Enrollment Status Page (ESP), see the following articles:

[Windows Autopilot Enrollment Status Page](/mem/autopilot/enrollment-status)
[Set up the Enrollment Status Page](/mem/intune/enrollment/windows-enrollment-status)

## Create Autopilot profile

## Assign Autopilot profile to device group

## Assign Autopilot profile to device

## More info

[Windows Autopilot user-driven mode](/mem/autopilot/user-driven)