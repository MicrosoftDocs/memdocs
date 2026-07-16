---
title: "Collect Device Hardware Info With the Properties Catalog"
description: "Use the properties catalog in Microsoft Intune to collect device hardware info like BIOS version, TPM status, and disk details on managed Windows devices. Get deeper visibility into your device inventory and troubleshoot issues."
ms.date: 06/03/2026
ms.topic: how-to
ms.reviewer: abbystarr, madisoncooks
---

# Use the Intune properties catalog to get device hardware properties

In Microsoft Intune, you can use the **properties catalog** to collect and view hardware properties from your managed Windows devices. When you create the policy, you can select specific properties to collect.

For example, you can:

- Discover local AI agents, like OpenClaw, running on your Windows devices.
- Get the BIOS version and TPM status to identify devices that might need firmware updates or aren't compliant with security policies.
- Identify devices that lack encryption, which might violate security policies.
- Identify devices that need to be replaced based on hardware properties, like disk size or memory.
- Detect outdated firmware or hardware that could expose vulnerabilities.
- Collect battery health information to help monitor device performance and lifespan.
- Retrieve network adapter configurations to troubleshoot connectivity issues.

Use this information to get deeper visibility into your device inventory, including detailed hardware and system information.

This article shows you how to configure a properties catalog policy, view the data collected by the policy, and lists the available properties. After you create a profile, assign or deploy that profile to your Windows devices.

This feature applies to:

- Windows

> [!NOTE]
> On Android and Apple devices, device properties are collected automatically.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
> This feature supports the following platforms:
>
> - Windows
> - Devices must be corporate owned, Intune managed (includes co-managed), Microsoft Entra Hybrid joined, and Microsoft Entra joined.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> To configure this policy and start collecting inventory data from devices, use an account with at least one of the following roles:
>
> - [!INCLUDE [minimum-rbac-role-policy-profile-manager](../includes/minimum-rbac-role-policy-profile-manager.md)]
> - A [custom role](./templates/configure-custom-settings.md) that includes the **Device Configurations** > **Create** permission and the **Organization** > **Read** permission.
> - For a user to view collected data about devices, they must have the **Managed Devices** > **Read** permission. This permission is included in many built-in roles. For a list, see [Built-in role permissions for Microsoft Intune](../fundamentals/role-based-access-control/ref-built-in-roles.md).
:::column-end:::
:::row-end:::

## Create the policy

Use the following steps to create a properties catalog profile and assign it to your Windows devices.

1. Sign in to the [Microsoft Intune admin center].

2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New Policy**.

3. Enter the following properties and select **Create**:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Properties catalog**.

4. In **Basics**, enter the following properties and select **Next**:

    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

5. Select **Add properties** and select the properties you want to collect. You can select multiple properties from multiple categories.

    Some required properties are automatically added. For a list, see [Required properties](#available-and-required-properties) (in this article).

    Select **Next**.

6. Optional. In **Scope (Tags)**, select any scope tags you want to assign to the profile. To learn more about scope tags, see [Use scope tags for distributed IT](../fundamentals/role-based-access-control/scope-tags.md).

    Select **Next**.

7. In **Assignments**, select the groups that receive this profile. For more information on assigning profiles, see [Assign user and device profiles](./assign-device-profile.md).

   Select **Next**.

8. In **Review + create**, review your settings, and select **Create**.

    When you select **Create**, the profile is assigned to the groups you specified. The profile is also created and shown in the list.

The next time each device checks in with the Intune service, the policy applies. It can take up to 24 hours for the initial collection of inventory data.

## Available and required properties

You can collect the following properties. To learn more about the different properties, see [Intune Data Platform Schema](../advanced-analytics/ref-data-platform-schema.md).

When you create the policy, select any of the following property categories to collect. The **required** properties are automatically collected when you collect any property in that category.

| Category | Required properties |
| --- | --- |
| Application Properties | App Name<br/>App Version<br/>Architectures<br/>Install Scope<br/>Install Scope Platform User ID<br/>Install Scope User ID<br/>Publisher |
| Battery | Instance Name |
| Bios Info | Bios Name<br/>Software Element ID<br/>Software Element State<br/>Target Operating System |
| CPU | Processor ID |
| Disk Drive | Drive ID |
| Encryptable Volume | Volume ID |
| Local AI Agent | Agent Name<br/>Install Location<br/>Install Scope <br/><br/>Microsoft recommends collecting **Host process**, as OpenClaw can run in different process names, like `node.exe`, `wsl.exe`, etc. |
| Logical Drive | Drive Identifier |
| Memory Info | |
| Network Adapter | Identifier |
| OS Version | |
| Sim Info | Windows eSIM ID |
| System Enclosure | Serial Number |
| System Info | |
| Time | |
| TPM | |
| Video Controller | Identifier |
| Windows QFE | Hot Fix ID |

## View collected data

Use the following steps to view the collected device inventory information:

1. Sign in to the [Microsoft Intune admin center].
2. Go to **Devices** > **By platform** > **Windows Devices** and select a device.
3. In **Monitor**, select **Device Inventory**. Select a category to view the hardware information.

## What you need to know

- **Local AI Agent** helps you discover OpenClaw running on your Windows devices. After you deploy the properties catalog policy and start collecting data, the next steps are:

  - Use [Device Query](../advanced-analytics/device-query-multiple-devices.md) to view devices with a Local AI Agent.
  - Use the [Local AI Agent Baseline - OpenClaw](../device-security/security-baselines/ref-openclaw-settings.md) to block users from using OpenClaw.

- You can stop (delete) the collection of properties only at the category level. To stop collecting properties, go to the **properties catalog** profile, and remove the collection for every property in the category.

  If you delete a properties catalog policy, you can see the last-collected data in Device Inventory for up to 28 days.

- If you use co-management with tenant attach, you see the **Resource Explorer** and **Device Inventory** nodes.

  For Intune collected data, you see a **Device Inventory** tab. For Configuration Manager collected data, you see a **Resource Explorer** tab. Use the source that best fits your use case. In the future, use the Intune-based **Device Inventory**.

- The client logs are at `C:\Program Files\Microsoft Device Inventory Agent\Logs`. You can also collect the logs by using the [Remote device action: collect diagnostics](../device-management/actions/collect-diagnostics.md). Use these logs to help troubleshoot.

## Related content

- [Intune Data Platform Schema and property info](../advanced-analytics/ref-data-platform-schema.md)

<!--links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431