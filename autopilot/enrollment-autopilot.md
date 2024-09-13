---
title: Create device groups for Windows Autopilot
description: Learn how to create device groups for Windows Autopilot.
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/28/2024
ms.topic: how-to
ms.localizationpriority: high
ms.service: windows-client
ms.subservice: autopilot
ms.suite: ems
search.appverid: MET150
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - M365-identity-device-management
  - highpri
  - tier1
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a>
---

# Create device groups for Windows Autopilot

> [!NOTE]
>
> HoloLens 2 devices require Windows Autopilot self-deploying mode. For more information about using Windows Autopilot to deploy HoloLens 2 devices, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot). **Assign to User** isn't applicable for self-deployment Autopilot mode on HoloLens 2.

## Create an Autopilot device group using Intune

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Groups** > **New group**.

1. In **New Group**, configure the following properties:

    - **Group type**: Select **Security**.

    - **Group name** and **Group description**: Enter a name and description for the group.

    - **Microsoft Entra roles can be assigned to the group**: Select **No**, Microsoft Entra roles aren't assigned to this group.

      For more information, see [Use cloud groups to manage role assignments in Microsoft Entra ID](/azure/active-directory/roles/groups-concept).

    - **Membership type**: Select how devices become members of this group. Select **Dynamic Device**. For more information, see [Add groups to organize users and devices](/mem/intune/fundamentals/groups-add).

    - **Owners**: Select users that own the group. Owners can also delete this group.

    - **Dynamic device members**: Select **Add dynamic query** > **Add expression**.

      Create rules using Autopilot device attributes. Autopilot devices that meet these rules are automatically added to the group. Creating an expression using non-autopilot attributes doesn't guarantee that devices included in the group are registered to Autopilot.

      When creating expressions:

      - To create a group that includes all of the Autopilot devices, enter: `(device.devicePhysicalIDs -any (_ -startsWith "[ZTDid]"))`.

      - Intune's group tag field maps to the `OrderID` attribute on Microsoft Entra devices. To create a group that includes all Autopilot devices with a specific group tag (the Microsoft Entra device `OrderID`), enter: `(device.devicePhysicalIds -any (_ -eq "[OrderID]:179887111881"))`.

      - To create a group that includes all the Autopilot devices with a specific Purchase Order ID, enter: `(device.devicePhysicalIds -any (_ -eq "[PurchaseOrderId]:76222342342"))`

      **Save** the expressions.

1. Select **Create**.

> [!NOTE]
>
> Anything assigned to these attributes is only assigned if the device is registered with Autopilot.

For a detailed tutorial on creating a device group for each of the Windows Autopilot scenarios using Intune, see the following links:

- [User-driven Microsoft Entra join: Create a device group](tutorial/user-driven/azure-ad-join-device-group.md).
- [User-driven Microsoft Entra hybrid join: Create a device group](tutorial/user-driven/hybrid-azure-ad-join-device-group.md).
- [Pre-provision Microsoft Entra join: Create a device group](tutorial/pre-provisioning/azure-ad-join-device-group.md).
- [Pre-provision Microsoft Entra hybrid join: Create a device group](tutorial/pre-provisioning/hybrid-azure-ad-join-device-group.md).
- [Self-deploying mode: Create a device group](tutorial/self-deploying/self-deploying-device-group.md).

## Add devices

The dynamic device group that includes Autopilot devices automatically adds existing Autopilot devices to the device group. To manually add new devices as Windows Autopilot devices using a CSV file so that they become part of the device group, see [Manually register devices with Windows Autopilot](add-devices.md).

## Assign a user to a specific Autopilot device

A licensed Intune user can be assigned to a specific Autopilot device. For supported OEMs, this assignment will:

- Pre-populate the Microsoft Entra user Principal Name (UPN) under the pre-provisioning landing page and Microsoft Entra sign-in page.
- Allows setting of a custom greeting name.

For more information including a list of supported OEMs, see [Return of key functionality for Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/return-of-key-functionality-for-windows-autopilot-sign-in-and/ba-p/3583130).

> [!NOTE]
>
> Assigning a licensed user to a specific Autopilot device only affects pre-populating the UPN and setting of a custom greeting name. It doesn't affect assigned policies and applications that are deployed to the device or to the user. The assigned policies and applications are still deployed regardless of the OEM. For more information, see [Windows Autopilot for pre-provisioned deployment](pre-provision.md#preparation).

> [!IMPORTANT]
>
> Assigning a user to a specific Autopilot device doesn't work if using Active Directory Federation Services (ADFS).

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Devices**.

1. In the **Windows Autopilot devices** screen, select a device, and then in the toolbar select **Assign user**.

1. Select a Microsoft Entra ID user licensed to use Intune and select **Select**.

1. In the **User Friendly Name** box, enter a friendly name or just accept the default.

1. Select **Save**.

For a detailed tutorial on assigning a user for each of the Windows Autopilot scenarios via Intune, see the following articles:

- [User-driven Microsoft Entra join: Assign Autopilot device to a user](tutorial/user-driven/azure-ad-join-assign-device-to-user.md).
- [User-driven Microsoft Entra hybrid join: Assign Autopilot device to a user](tutorial/user-driven/hybrid-azure-ad-join-assign-device-to-user.md).
- [Pre-provision Microsoft Entra join: Assign Autopilot device to a user](tutorial/pre-provisioning/azure-ad-join-assign-device-to-user.md).
- [Pre-provision Microsoft Entra hybrid join: Assign Autopilot device to a user](tutorial/pre-provisioning/hybrid-azure-ad-join-assign-device-to-user.md).

## Using Autopilot in other portals

If there isn't interest in mobile device management (MDM), Autopilot can be used in other portals. While using other portals is an option, Microsoft recommends only using Intune to manage Autopilot deployments. When Intune is used with another portal, Intune isn't able to:

- Display changes to profiles created in Intune, but edited in another portal.
- Synchronize profiles created in another portal.
- Display changes to profile assignments done in another portal.
- Synchronize profile assignments done in another portal.
- Display changes to the device list that were made in another portal.

## Windows Autopilot for existing devices

When enrolling Windows devices via [Autopilot for existing devices](tutorial/existing-devices/existing-devices-workflow.md), a correlator ID can be used to group the Windows devices. The correlator ID is a parameter of the Autopilot configuration file. The [Microsoft Entra device attribute enrollmentProfileName](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) is automatically set to equal **OfflineAutopilotprofile-\<correlator ID\>**. Arbitrary Microsoft Entra dynamic groups can be created when using the correlator ID from the **enrollmentprofileName** attribute.

> [!WARNING]
>
> Because the correlator ID isn't pre-listed in Intune, the device might report any correlator ID they want. If the user creates a correlator ID matching an Autopilot or Apple ADE profile name, the device is added to any dynamic Microsoft Entra device group based off the enrollmentProfileName attribute. To avoid this conflict:
>
> - Always create dynamic group rules matching against the *entire* **enrollmentProfileName** value.
> - Never name Autopilot or Apple ADE profiles beginning with **OfflineAutopilotprofile-**.

If all devices in the groups should automatically register to Autopilot, in any Autopilot profiles assigned to the groups, set the setting **Convert all targeted devices to Autopilot** to **Yes**. All non-Autopilot devices in assigned groups register with the Autopilot deployment service. Allow 48 hours for the registration to be processed. When the device is unenrolled and reset, Autopilot enrolls it again. After a device is registered in this way, disabling this setting or removing the profile assignment won't remove the device from the Autopilot deployment service. The device must be removed by deregistering the device from Autopilot. For more information on how to properly deregister a device, see [Deregister a device](registration-overview.md#deregister-a-device).

For a full tutorial on Windows Autopilot for existing devices, see the following article:

- [Step by step tutorial for Windows Autopilot deployment for existing devices in Intune and Configuration Manager](tutorial/existing-devices/existing-devices-workflow.md).

## Next steps

After a device group is created, a Windows Autopilot deployment profile can be configured and deployed to each device in the group. Deployment profiles determine the deployment mode, and customize the OOBE for the end users. For more information, see [Configure deployment profiles](profiles.md).

For a detailed tutorial on configuring and assigning a Windows Autopilot deployment profile, see the following articles. Each article has detailed instructions on configuring and assigning a Windows Autopilot deployment profile in Intune for each of the Autopilot scenarios:

- [User-driven Microsoft Entra join: Create and assign user-driven Microsoft Entra join Autopilot profile](tutorial/user-driven/azure-ad-join-autopilot-profile.md).
- [User-driven Microsoft Entra hybrid join: Create and assign user-driven Microsoft Entra hybrid join Autopilot profile](tutorial/user-driven/hybrid-azure-ad-join-autopilot-profile.md).
- [Pre-provision Microsoft Entra join: Create and assign a pre-provisioned Microsoft Entra join Autopilot profile](tutorial/pre-provisioning/azure-ad-join-autopilot-profile.md).
- [Pre-provision Microsoft Entra hybrid join: Create and assign a pre-provisioned Microsoft Entra hybrid join Autopilot profile](tutorial/pre-provisioning/hybrid-azure-ad-join-autopilot-profile.md).
- [Self-deploying mode: Create and assign self-deploying Autopilot profile](tutorial/self-deploying/self-deploying-autopilot-profile.md).

For more information about managing Windows Autopilot devices, see [What is Microsoft Intune device management?](/mem/intune/remote-actions/device-management).
