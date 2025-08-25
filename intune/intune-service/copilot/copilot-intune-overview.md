---
# required metadata

title: Microsoft Copilot in Intune features overview
description: Microsoft Copilot in Intune is an AI platform. It can help you create policies, get information about existing policies, and show more details on specific settings, including their impacts on users and devices. You can also use Copilot to troubleshoot device issues.
keywords: Security Copilot, Intune, Microsoft Intune, AI, Copilot, settings catalog, policies, device details, troubleshooting
author: MandiOhlinger
ms.author: mandia
manager: laurawi
ms.date: 07/01/2025
ms.update-cycle: 180-days
ms.topic: get-started
ms.service: microsoft-intune
ms.subservice:
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: rashok, mikedano, zadvor
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
- security-copilot
- msec-ai-copilot
---

# Microsoft Copilot in Intune

[Microsoft Security Copilot](/copilot/security/microsoft-security-copilot) is a generative-AI security analysis tool. It can help you and your organization get information quickly and make decisions that affect security and risk.

Intune has capabilities that are powered by Copilot. These capabilities access your Intune data and help you manage your policies and settings, understand your security posture, and troubleshoot device issues.

There are two ways to access your Intune data by using Copilot:

- **Microsoft Copilot in Intune** (this article): Copilot is embedded in Intune and is available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). The Copilot prompts and their output are in the context of Intune and your Intune data.

  This experience has an IT admin/IT Pro focus.

- **Microsoft Security Copilot**: This option is a standalone Copilot and is available in the [Microsoft Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989). You can use this portal to get insights from Security Copilot for all your enabled services, like Intune, Microsoft Defender, Microsoft Entra ID, Microsoft Purview, and more.

  This experience has a Security Operations Center (SOC) focus and can be used by IT admins. For more information, see [Access your Microsoft Intune data in Security Copilot](security-copilot.md).

This article focuses on Copilot in Intune and describes the Intune features that you can use with Copilot.

## Before you begin

To use Copilot in Intune, you should know the following information:

- **Copilot security compute units (SCUs)**: Copilot in Intune is included with Security Copilot. There aren't any other licensing requirements or Intune-specific licenses for using Copilot in Intune.

  For more information about SCUs, see:

  - [Get started with Microsoft Copilot](/copilot/security/get-started-security-copilot)
  - [Manage capacity in Security Copilot](/copilot/security/manage-usage)

- **Copilot configuration**: Before you can use the Copilot features in Intune, Microsoft Security Copilot must be configured, and you must complete the first run tour in the [Microsoft Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989). For the setup tasks, see [Get started with Microsoft Copilot](/copilot/security/get-started-security-copilot).

  You can check the status in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Copilot**.

  :::image type="content" source="./media/copilot-intune-overview/tenant-administration-copilot-enabled.png" alt-text="Screenshot that shows Copilot is enabled in the Microsoft Intune tenant and Intune admin center." lightbox="./media/copilot-intune-overview/tenant-administration-copilot-enabled.png":::

- **Copilot roles**: Access to Copilot in Intune is managed through Security Copilot or Microsoft Entra ID. To use Copilot in Intune, you or your admin team must be assigned the appropriate role in Security Copilot or Microsoft Entra ID. There isn't a built-in Intune role that has access to Copilot.

  For more information, see [Roles and authentication in Microsoft Security Copilot](/copilot/security/authentication).

- **Intune plug-in source**: To use Copilot in Intune, you need the Intune plug-in enabled in Security Copilot. This plug-in allows you to access your Intune data and use Copilot in the Intune admin center.

  Go to the [Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989) and select **Sources** (prompt bar > right corner).

  :::image type="content" source="./media/copilot-intune-overview/security-copilot-sources.png" alt-text="Screenshot that shows the plugin sources that are available, enabled, and disabled in Microsoft Security Copilot.":::

  In **Manage sources**, enable Microsoft Intune.

  :::image type="content" source="./media/copilot-intune-overview/intune-plug-in-enabled.png" alt-text="Screenshot that shows the Microsoft Intune plug-in source is enabled in the Microsoft Security Copilot portal.":::

  > [!TIP]
  > Some roles can enable or disable plug-ins. For more information, see [Manage plug-ins in Microsoft Security Copilot](/copilot/security/manage-plugins).

- **Your Intune data**: Copilot uses your Intune data. When an Intune admin submits a prompt, Copilot can only access the data that they have permissions to, which includes the [RBAC roles](../fundamentals/role-based-access-control.md) and [scope tags](../fundamentals/scope-tags.md) assigned to them.

> [!TIP]
> For some common questions asked about Copilot in Intune, go to [Microsoft Copilot in Intune FAQ](copilot-intune-faq.md).

## Start using Copilot

To access Copilot in Intune, sign into the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). The home screen lists the ways to get started with Copilot.

:::image type="content" source="./media/copilot-intune-overview/copilot-home-page.png" alt-text="Screenshot that shows the Intune admin center homepage with Copilot features in Microsoft Intune." lightbox="./media/copilot-intune-overview/copilot-home-page.png":::

You can use Copilot in Intune for:

- Data exploration using natural language
- Policy and setting management
- Device details and troubleshooting

## Data exploration

Using natural language, you can query and explore your Intune data, including data about your devices, users, apps, policies, updates, and compliance. There are also built-in examples that help you understand the kinds of questions you can ask.

When you run a query, Copilot summarizes the results and recommends actions you can take based on the query results. You can also use the query output to add users or devices to groups, and create custom reports.

To learn more, see [Explore Intune data and get Microsoft Copilot recommendations](copilot-intune-explorer.md).

## Policy and setting management

Copilot is embedded in policy settings and with your existing policies.

### ✅ Use Copilot to learn more about individual settings and recommended values

When you create an Intune policy, you add settings and configure these settings to meet your organization's requirements. When you add a setting, there's a Copilot tooltip.

:::image type="content" source="./media/copilot-intune-overview/compliance-policy-setting-copilot-tooltip.png" alt-text="Screenshot that shows Copilot settings tooltip in a compliance policy in Microsoft Intune and Intune admin center." lightbox="./media/copilot-intune-overview/compliance-policy-setting-copilot-tooltip.png":::

When you select the Copilot tooltip, the Copilot prompt window opens and provides more information about that setting.

:::image type="content" source="./media/copilot-intune-overview/compliance-policy-setting-prompt-results.png" alt-text="Screenshot that shows more information about a setting when you select the Copilot tooltip in a compliance policy in Microsoft Intune admin center.":::

In the Copilot window, there are more prompts that you can use. You can also select the prompt guide and select from an existing list of options.

:::image type="content" source="./media/copilot-intune-overview/compliance-policy-setting-copilot-prompt-guide.png" alt-text="Screenshot that shows the Copilot prompt guide when you add a setting in a compliance policy in Microsoft Intune and Intune admin center.":::

The Copilot prompts can help you understand the effect of the setting, look for potential conflicts, and provide a recommended value. For an example of how to use Copilot with the settings catalog, go to [Use the settings catalog to create device configuration policies](../configuration/settings-catalog.md).

You can use the Copilot tooltips on the following policy types in Intune:

- Compliance policies
- Device configuration policies, including the settings catalog
- Most endpoint security policies

### ✅ Use Copilot to summarize an existing policy

On your existing Intune policies, you can use Copilot to summarize the policy. The summary describes what the policy does, the users and groups assigned to the policy, and the settings in the policy. This feature can help you understand the effect of a policy and its settings on your users and devices.

To use this feature in Intune, select an existing policy and then select **Summarize with Copilot**.

:::image type="content" source="./media/copilot-intune-overview/copilot-summarize-policy.png" alt-text="Screenshot that shows how to select the Summarize with Copilot feature in a policy in Microsoft Intune or Intune admin center.":::

You can use this feature on the following policy types in Intune:

- Compliance policies
- Device configuration policies, including the settings catalog
- Most endpoint security policies

## Device details and troubleshooting

### ✅ Use Copilot to get device details and troubleshoot a device

You can use Copilot to get device-specific information, like the installed apps, group membership, and more.

To use this feature in Intune, select a device, and then select **Summarize with Copilot**.

:::image type="content" source="./media/copilot-intune-overview/summarize-with-copilot.png" alt-text="Screenshot that shows where you select any device and then select Summarize with Copilot in Microsoft Intune and Intune admin center.":::

When the Copilot window opens, select a prompt and enter any required or optional input, if needed. You can also open the prompt guide for some follow-up questions.

:::image type="content" source="./media/copilot-intune-overview/device-prompt-guide.png" alt-text="Screenshot that shows the Copilot prompt guide after you select a device in Microsoft Intune or Intune admin center.":::

For more information about using Copilot with your devices, go to [Use Microsoft Copilot in Intune to troubleshoot devices](../copilot/copilot-devices.md).

### ✅ Use Copilot to create KQL queries to get device details

You can use Copilot to help you create Kusto Query Language (KQL) queries to run when using device query in Intune.

> [!NOTE]
> To use Device query in your tenant, you must have a license that includes Microsoft Intune Advanced Analytics. For more information, see [Intune add-ons](../fundamentals/intune-add-ons.md#microsoft-intune-advanced-analytics).

You can use this feature for either an individual device, or for multiple devices.

#### Query a single device

To query a single device in Intune, select a device, select **Device query**, and then select **Query with Copilot**.

When the Copilot window opens, enter your question about the device. If device query supports the properties needed to answer the question, Copilot generates a KQL query that you can use to get the data that you require.

:::image type="content" source="./media/copilot-intune-overview/copilot-device-query.png" alt-text="Screenshot that shows the Copilot window with your prompt for device query." lightbox="./media/copilot-intune-overview/copilot-device-query.png":::

To use the query that Copilot generates, select **Add to editor** to add it to the query editor in device query, or select **Add and run** to add it to the editor and automatically run it. To see a Copilot-generated explanation for how Copilot created a query in response to your request, select **How was this query generated?**.

The following examples are some queries you can try:

- Is Defender running on this device?
- Show me the last 5 app crash events on this device.
- What are the top 10 processes using the most memory on this device?
- Show me expired certificates on this device.
- Show me the last 20 most recently created files in C:\Windows\folderPath
- Does this device support TPM 2.0?
- Show me drivers on this device grouped by provider name.

    > [!NOTE]
    > Copilot can only generate queries for requests related to the properties that device query support. You can't use this feature to ask Copilot for details about the device beyond what is available in device query. For a full list of supported properties in device query, go to [Device query](../../analytics/device-query.md).

#### Query multiple devices

To query data across multiple devices in Intune, select **Devices** > **Device query** > **Query with Copilot**.

When the Copilot window opens, enter your question about the device. If device query supports the properties needed to answer the question, Copilot generates a KQL query that you can use to get the data that you require.

:::image type="content" source="./media/copilot-intune-overview/copilot-devices-query.png" alt-text="Screenshot that shows the Copilot window for querying multiple devices." lightbox="./media/copilot-intune-overview/copilot-devices-query.png":::

You can select the options that Copilot generates to quickly generate a KQL query, or you can enter your question or request other device data. Once Copilot generates the query, select **Add to editor** to add it to the query editor, or select **Add and run** to add it to the editor and automatically run it. To make a new request, select **Query with Copilot** to display the Copilot pane.

The following examples are some queries you can try:

- Which devices haven't been encrypted?
- Show me Windows 11 devices.
- Which devices have a hot fix?
- Show me TPM 2.0 devices.
- Show me devices sorted by manufacturer.
- Which devices haven't been patched in the last 30 days?

## Related content

- [Use Microsoft Copilot in Intune to troubleshoot devices](../copilot/copilot-devices.md).
- [Use the settings catalog to create device configuration policies](../configuration/settings-catalog.md).
- [Learn more about Intune capabilities in Microsoft Security Copilot](security-copilot.md).
