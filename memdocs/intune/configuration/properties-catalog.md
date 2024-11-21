---
# required metadata

title: Properties catalog in Microsoft Intune
description: Configure Properties catalog policy to manage Device Inventory settings on Windows devices you manage with Intune.
keywords:
author: smbhardwaj
ms.author: smbhardwaj
manager: dougeby
ms.date: 11/14/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
ms.reviewer: abbystarr
---
# Properties catalog in Microsoft Intune

## Device inventory

With Intune, you can use Device inventory to collect and view more hardware properties from your managed devices to help you better understand the state of your devices and make business decisions.  

This article describes how to configure Device Inventory settings as part of an Intune device configuration profile. After you create a profile, you then assign or deploy that profile to your Windows devices.

This feature applies to:

Windows 11

Windows 10

## Prerequisites

- To use Inventory, devices must be corporate owned, Intune managed (includes co-managed), and Microsoft Entra joined.

- For a user to configure a policy to start collecting inventory data from devices, they must have the Device Configurations **Create** permission.

- For a user to view collected data about devices, they must have the Managed Devices **Read** permission.

## Supported platforms

Inventory is currently only supported on devices running Windows 10 and later. Inventory is only supported on the following minimum Windows versions:

- Windows 11, version 24H2
- Windows 11, version 23H2 (22631.2506 or later) with KB5031455
- Windows 11, version 22H2 (22621.2215 or later) with KB5029351
- Windows 11, version 21H2 (22000.2713 or later) with KB5034121
- Windows 10, version 22H2 (19045.3393 or later) with KB5030211
- Windows 10, version 21H2 (19044.3393 or later) with KB5030211

## How to use

To configure Inventory collection, create a new **Properties Catalog** profile in the Intune admin center. This profile allows you to select which properties you would like to collect from your devices.

After the profile is created, you can apply the profile to specific devices in the selected groups.

### Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New Policy**.

3. Enter the following properties:

   - **Platform**: Select **Windows 10 and later**.
   - **Profile type**: Select **Properties catalog**.

4. Select **Create**.

5. In **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the new profile.
   - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. Select **Add properties**.Expand out categories to view individual properties and then select which properties you would like to collect from the Properties Picker.

   When you're done, select **Next**.

8. On the **Scope (Tags)** page, select **Select scope tags** to open the *Select tags* pane to assign scope tags to the profile.
  
   Select **Next** to continue.

9. On the **Assignments** page, select the groups that receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   Select **Next**.

10. On the **Applicability Rules** page, use the **Rule**, **Property**, and **Value** options to define how this profile applies within assigned groups.

11. On the **Review + create** page, when you're done, choose **Create**. The profile is created and is shown in the list.

The next time each device checks in, the policy is applied.

### View collected data

To view collected inventory information, navigate to **Devices** > **Windows Devices** and select a device.

Under **Monitor** select **Resource Explorer**. Choose a category to view hardware information.

After a device syncs with Intune, it can take up to 24 hours for initial harvesting of inventory data.  

### Required Properties

Certain **required** properties are automatically collected when you collect any properties in that category.

The following properties are required:

- **Battery**: Instance Name
- **Bios Info**: Bios Name, Software Element ID, Software Element State, Target Operating System
- **Cpu**: Processor ID
- **Disk Drive**: Drive ID
- **Encryptable Volume**: Volume ID
- **Logical Drive**: Drive Identifier
- **Network Adapter**: Identifier
- **System Enclosure**: Serial Number
- **Video Controller**: Identifier
- **Windows Qfe**: Hot Fix ID

## Known Limitations

Collection of properties can only be stopped (deleted) at the category level. 

To stop collecting properties, navigate to the **Properties catalog** profile, and remove collection for every property in a particular category.

## Supported Properties

Inventory supports the following entities. To learn more about what properties are supported for each entity, see [Intune Data Platform Schema](../../analytics/data-platform-schema.md).

- Battery
- Bios Info
- Cpu
- Disk Drive
- Encryptable Volume
- Logical Drive
- Memory Info
- Network Adapter
- Os Version
- System Enclosure
- Time
- Tpm
- Video Controller
- Windows Qfe

## Frequently Asked Questions

### Is Resource Explorer different than the Hardware tab for a device?

Yes, the **Hardware** tab data and **Resource Explorer** data come from different places. We recommend using Inventory and Resource Explorer for the most up-to-date and comprehensive data about your devices. In the future, the data source for **Hardware** tab and the Resource Explorer will be the same.

### I'm using Co-management with Tenant Attach and I see two Resource Explorer nodes. Which one should I use?

You'll see a **Resource Explorer** tab for Intune collected data and a **Resource Explorer** tab for Configuration Manager collected data. Feel free to use the source that best fits your use case. In the future, we recommend using the Intune-based Resource Explorer.

### How can I troubleshoot this feature?

Client logs are available at `C:\Program Files\Microsoft Device Inventory Agent\Logs` and logs can also be collected via Collect MDM Diagnostics.
