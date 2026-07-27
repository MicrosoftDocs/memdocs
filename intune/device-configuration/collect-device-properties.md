---
title: Collect Device Properties With Intune Properties Catalog
description: Use Microsoft Intune properties catalog to collect device properties—including hardware, registry values, and security signals—from Windows devices.
ms.date: 07/01/2026
ms.topic: how-to
ai-usage: ai-assisted
ms.reviewer: abbystarr, madisoncooks
---

# Use Intune properties catalog to collect device properties from Windows devices

In Microsoft Intune, use the **properties catalog** to collect device properties—including hardware details, configuration data, and application signals—from managed Windows devices.

For example, you can:

- Discover local AI agents, like OpenClaw, running on your Windows devices.
- Collect selected Windows registry key values from managed Windows devices, such as configuration settings, application state, or security posture signals.
- Get the BIOS version and TPM status to identify devices that might need firmware updates or aren't compliant with security policies.
- Identify devices that lack encryption, which might violate security policies.
- Identify devices that need to be replaced based on hardware properties, like disk size or memory.
- Detect outdated firmware or hardware that could expose vulnerabilities.
- Collect battery health information to help monitor device performance and lifespan.
- Retrieve network adapter configurations to troubleshoot connectivity issues.

This visibility helps you make informed decisions about device compliance, lifecycle management, and troubleshooting.

In this article, you'll learn how to create a properties catalog policy, view the collected data, and explore the available hardware properties. After creating a profile, you can assign it to your Windows devices.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
> This feature supports Windows devices only.
>
> On Android and Apple devices, device properties are collected automatically.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../includes/requirements/device-configuration.md)]

:::column-end:::
:::column span="3":::
> This feature supports devices that are:
>
> - Managed by Intune
> - Co-managed (Intune + Configuration Manager)
> - Microsoft Entra joined
> - Microsoft Entra hybrid joined
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> Role requirements vary based on the tasks being performed.
>
> ---
>
> To configure the properties catalog policy, use an account with at least one of the following Intune roles:
>
> - [Policy and Profile Manager](../fundamentals/role-based-access-control/ref-built-in-roles.md#policy-and-profile-manager)
> - A [custom role] that includes the permissions:
>   - **Organization/Read** and **Managed Devices/Read** — Required for device visibility.
>   - **Device configurations/Create, Read, Assign** — Required to create and assign the data collection policy.
>
> ---
>
> To view the collected data, use an account with the permission **Managed Devices/Read**.
:::column-end:::
:::row-end:::

## Available and required properties

You can collect the following properties. To learn more about the different properties, see [Intune Data Platform Schema](../advanced-analytics/ref-data-platform-schema.md).

When you create the policy, select any of the following property categories to collect. The **required** properties are automatically collected when you collect any property in that category.

| Category | Required properties |
|--|--|
| Application Properties | App Name<br/>App Version<br/>Architectures<br/>Install Scope<br/>Install Scope Platform User ID<br/>Install Scope User ID<br/>Publisher |
| Battery | Instance Name |
| Bios Info | Bios Name<br/>Software Element ID<br/>Software Element State<br/>Target Operating System |
| CPU | Processor ID |
| Disk Drive | Drive ID |
| Encryptable Volume | Volume ID |
| Local AI Agent | Agent Name<br/>Install Location<br/>Install Scope <br/><br/>Microsoft recommends collecting **Host process**, as OpenClaw can run in different process names, like `node.exe`, `wsl.exe`, etc. |
| Logical Drive | Drive Identifier |
| Memory Info | — |
| Network Adapter | Identifier |
| OS Version | — |
| Sim Info | Windows eSIM ID |
| Registry | Registry keys |
| System Enclosure | Serial Number |
| System Info | — |
| Time | — |
| TPM | — |
| Video Controller | Identifier |
| Windows QFE | Hot Fix ID |

## Create the collection policy

Use the following steps to create a properties catalog profile and assign it to your Windows devices.

1. In the [Microsoft Intune admin center], select **Devices** > **Windows**.
1. Under **Manage devices**, select **Configuration** > **Create** > **New Policy**.
1. Select the following properties and select **Create**:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Properties catalog**.

1. In **Basics**, enter the following properties and select **Next**:

    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

1. Select **Add properties** and select the properties you want to collect. You can select multiple properties from multiple categories.

    Some required properties are automatically added. For a list, see [Required properties](#available-and-required-properties).

    Select **Next**.

1. Optional. In **Scope (Tags)**, select any scope tags you want to assign to the profile. To learn more about scope tags, see [Use scope tags for distributed IT](../fundamentals/role-based-access-control/scope-tags.md).

    Select **Next**.

1. In **Assignments**, select the groups that receive this profile. For more information on assigning profiles, see [Assign policies in Microsoft Intune](./assign-device-profile.md).

   Select **Next**.

1. In **Review + create**, review your settings, and select **Create**.

When you select **Create**, the profile is assigned to the groups you specified. The profile is also created and shown in the list. The next time each device checks in with the Intune service, the policy applies.

> [!NOTE]
> It can take up to 24 hours for the initial collection of inventory data.

## View collected data

Use the following steps to view the collected device inventory information:

1. In the [Microsoft Intune admin center], select **Devices** > **Windows**.
1. From the devices list, select a device.
1. Under **Tools**, select **Device Inventory**.
1. Select a category to view the collected information.

## Feature details and usage

:::row:::
:::column span="1":::
**Local AI agent**

:::column-end:::
:::column span="3":::
> Helps you discover OpenClaw running on your Windows devices. After you deploy the properties catalog policy and start collecting data, the next steps are:
>
> - Use [Device Query](../advanced-analytics/device-query-multiple-devices.md) to view devices with a Local AI Agent.
> - Use the [Local AI Agent Baseline - OpenClaw](../device-security/security-baselines/ref-openclaw-settings.md) to block users from using OpenClaw.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
**Registry key inventory**

:::column-end:::
:::column span="3":::
>Lets you collect selected Windows registry data through the properties catalog for configuration visibility and troubleshooting. Here are some important details about this feature:
> - Supported collection methods include a single value, all values directly under a key (non-recursive), and the same value across immediate subkeys.
> - Registry key inventory isn't intended to collect sensitive or confidential values and includes detection logic to help prevent potentially sensitive values from being ingested. If a value is flagged as potentially sensitive, it isn't collected.
> - To view collected registry data, use Device Inventory.
> - Initial release limitations include HKLM-only collection and enforced value (6KB) and per-device (100 registry keys) collection limits.
:::column-end:::
:::row-end:::

## Stop collecting properties

You can stop (delete) the collection of properties only at the category level. To stop collecting properties, go to the **properties catalog** profile, and remove the collection for every property in the category.

> [!NOTE]
> If you delete a properties catalog policy, you can see the last-collected data in Device Inventory for up to 28 days.

## Troubleshooting

To troubleshoot issues with the properties catalog, review the client logs at `C:\Program Files\Microsoft Device Inventory Agent\Logs`. You can also collect the logs by using the [Device Action: Collect Diagnostics](../device-management/actions/collect-diagnostics.md).

## Related content

- [Intune data platform schema](../advanced-analytics/ref-data-platform-schema.md)
- [Device query](../advanced-analytics/device-query.md)
- [Device query for multiple devices](../advanced-analytics/device-query-multiple-devices.md)

<!--Intune admin center links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431


<!--Intune roles-->

[Custom role]: ../fundamentals/role-based-access-control/create-custom-role.md