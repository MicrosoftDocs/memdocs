---
title: Collect device hardware info with the properties catalog
description: Use the properties catalog in Microsoft Intune view and collect enhanced device hardware info on Windows devices you manage with Intune. You can collect info like BIOS version, TPM status, disk info, memory details, and network adapter configurations. Use this information to get deeper visibility into your device inventory and troubleshoot issues.
author: MandiOhlinger
ms.author: mandia
ms.date: 10/20/2025
ms.topic: how-to
ms.collection:
- M365-identity-device-management
ms.reviewer: abbystarr, madisoncooks
---

# Use the Intune properties catalog to get device hardware properties

In Microsoft Intune, you can use the **properties catalog** to collect and view hardware properties from your managed Windows devices. When you create the policy, you can select specific properties to collect, such as BIOS version, disk information, memory details, and network adapter configurations.

You can use this information to get deeper visibility into your device inventory, including detailed hardware and system information.

For example, you can:

- Get the BIOS version and TPM status to identify devices that might need firmware updates or aren't compliant with security policies.
- Identify devices that lack encryption, which might violate security policies.
- Identify devices that need to be replaced based on hardware properties, like disk size or memory.
- Detect outdated firmware or hardware that could expose vulnerabilities.
- Collect battery health information to help monitor device performance and lifespan.
- Retrieve network adapter configurations to troubleshoot connectivity issues.

This article shows you how to configure a properties catalog policy, view the data collected by the policy,  and lists the available properties. After you create a profile, you then assign or deploy that profile to your Windows devices.

This feature applies to:

- Windows

> [!NOTE]
> On Android and Apple devices, device properties are collected automatically.

## Prerequisites

[!INCLUDE [platform-requirements](../../includes/h3/platform-requirements.md)]

> [!div class="checklist"]
> This feature supports the following platforms:
>
> - Windows
> - Devices must be corporate owned, Intune managed (includes co-managed), and Microsoft Entra joined.

[!INCLUDE [rbac-requirements](../../includes/h3/rbac-requirements.md)]

> [!div class="checklist"]
> To configure this policy and start collecting inventory data from devices, use an account with at least one of the following roles:
>
> - [!INCLUDE [minimum-rbac-role-policy-profile-manager](../includes/minimum-rbac-role-policy-profile-manager.md)]
> - A [custom role](custom-settings-configure.md) that includes the **Device Configurations** > **Create** permission and the **Organization** > **Read** permission.
> - For a user to view collected data about devices, they must have the **Managed Devices** > **Read** permission. This permission is included in many built-in roles. For a list, see [Built-in role permissions for Microsoft Intune](../fundamentals/role-based-access-control-reference.md).

## Create the policy and view the collected data

Use the following steps to create a properties catalog profile and assign it to your Windows devices.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New Policy**.

3. Enter the following properties and select **Create**:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Properties catalog**.

4. In **Basics**, enter the following properties and select **Next**:

    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

5. Select **Add properties** and select the properties you want to collect. You can select multiple properties from multiple categories.

    There are some required properties that are automatically added. For a list, see [Required properties](#available-and-required-properties) (in this article).

    Select **Next**.

6. Optional. In **Scope (Tags)**, select any scope tags you want to assign to the profile. To learn more about scope tags, see [Use scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

7. In **Assignments**, select the groups that receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   Select **Next**.

8. In **Review + create**, review your settings, and select **Create**.

    When you select create, the profile is assigned to the groups you specified. The profile is also created and is shown in the list.

The next time each device checks in with the Intune service, the policy applies. It can take up to 24 hours for the initial collection of inventory data.

### View collected data

Use the following steps to view the collected device inventory information:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices** > **By platform** > **Windows Devices** and select a device.
3. In **Monitor**, select **Device Inventory**. Select a category to view the hardware information.

## Available and required properties

The following properties are available for you to collect. To learn more about the different properties, see [Intune Data Platform Schema](../../analytics/data-platform-schema.md).

# [Available property categories](#tab/available)

When you create the policy, you can select any of the following property categories to collect:

- Battery
- Bios Info
- Cpu
- Disk Drive
- Encryptable Volume
- Logical Drive
- Memory Info
- Network Adapter
- Os Version
- Sim Info
- System Enclosure
- System Info
- Time
- TPM
- Video Controller
- Windows Qfe

# [Required properties](#tab/required)

When you create the policy, the following **required** properties are automatically collected when you collect any property in that category.

- Battery - Instance Name
- Bios Info:
  - Bios Name
  - Software Element ID
  - Software Element State
  - Target Operating System
- Cpu - Processor ID
- Disk Drive - Drive ID
- Encryptable Volume - Volume ID
- Logical Drive - Drive Identifier
- Network Adapter - Identifier
- System Enclosure - Serial Number
- Video Controller - Identifier
- Windows QFE - Hot Fix ID

---

## What you need to know

- Collection of properties can only be stopped (deleted) at the category level. To stop collecting properties, go to the **properties catalog** profile, and remove collection for every property in the category.

  If you delete a properties catalog policy, you can see the last-collected data in Device Inventory for up to 28 days.

- When you select a device, you see a **Device Inventory** tab and a **Hardware** tab. They're different and their data comes from different places. We recommend using the properties catalog for the most up-to-date and comprehensive data about your devices.

  In the future, the data source for the **Hardware** and **Device Inventory** tabs will be the same.

- If you use co-management with tenant attach, you see the **Resource Explorer** and **Device Inventory** nodes.

  For Intune collected data, you see a **Device Inventory** tab. For Configuration Manager collected data, you see a **Resource Explorer** tab. Use the source that best fits your use case. In the future, we recommend using the Intune-based **Device Inventory**.

- The client logs are available at `C:\Program Files\Microsoft Device Inventory Agent\Logs`. The logs can also be collected using the [Remote device action: collect diagnostics](../remote-actions/collect-diagnostics.md). You can use these logs to help troubleshoot.

## Related content

- [Intune Data Platform Schema and property info](../../analytics/data-platform-schema.md)
