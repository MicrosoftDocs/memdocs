---
# required metadata

title: Microsoft Copilot in Intune features overview
description: Microsoft Copilot in Intune is an AI platform. It can help you create policies, get information about existing policies, and show more details on specific settings, including their impacts on users and devices. You can also use Copilot to troubleshoot device issues.
keywords: Security Copilot, Intune, Microsoft Intune, AI, Copilot, settings catalog, policies, device details, troubleshooting
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/01/2024
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
- magic-ai-copilot
---

# Microsoft Copilot in Intune (public preview)

This feature is in [public preview](../fundamentals/public-preview.md).

[Microsoft Copilot for Security](/security-copilot/microsoft-security-copilot) is a generative-AI security analysis tool. It can help you and your organization get information quickly and make decisions that affect security and risk.

Intune has capabilities that are powered by Copilot. These capabilities access your Intune data and help you manage your policies and settings, understand your security posture, and troubleshoot device issues.

There are two ways to access your Intune data by using Copilot:

- **Microsoft Copilot in Intune** (this article): Copilot is embedded in Intune and is available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). The Copilot prompts and their output are in the context of Intune and your Intune data.

  This experience has an IT admin/IT Pro focus.

- **Microsoft Copilot for Security**: This option is a standalone Copilot and is available in the [Microsoft Copilot for Security portal](https://go.microsoft.com/fwlink/?linkid=2247989). You can use this portal to get insights from Copilot for Security for all your enabled services, like Intune, Microsoft Defender, Microsoft Entra ID, Microsoft Purview, and more.

  This experience has a Security Operations Center (SOC) focus and can be used by IT admins. For more information, see [Access your Microsoft Intune data in Copilot for Security](security-copilot.md).

This article focuses on Copilot in Intune and describes the Intune features that you can use with Copilot.

## Before you begin

To use Copilot in Intune, you should know the following information:

- **Copilot security compute units (SCUs)**: Copilot in Intune is included with Copilot for Security. There aren't any other licensing requirements or Intune-specific licenses for using Copilot in Intune.

  For more information about SCUs, see:

  - [Get started with Microsoft Copilot](/security-copilot/get-started-security-copilot)
  - [Manage capacity in Copilot for Security](/security-copilot/manage-usage)

- **Copilot configuration**: Before you can use the Copilot features in Intune, Microsoft Copilot for Security must be configured, and you must complete the first run tour in the [Microsoft Copilot for Security portal](https://go.microsoft.com/fwlink/?linkid=2247989). For the setup tasks, see [Get started with Microsoft Copilot](/security-copilot/get-started-security-copilot).

  You can check the status in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Copilot**.

  :::image type="content" source="./media/copilot-intune-overview/tenant-administration-copilot-enabled.png" alt-text="Screenshot that shows Copilot is enabled in the Microsoft Intune tenant and Intune admin center." lightbox="./media/copilot-intune-overview/tenant-administration-copilot-enabled.png":::

- **Copilot roles**: Access to Copilot in Intune is managed through Copilot for Security or Microsoft Entra ID. To use Copilot in Intune, you or your admin team must be assigned the appropriate role in Copilot for Security or Microsoft Entra ID. There isn't a built-in Intune role that has access to Copilot.

  For more information, see [Roles and authentication in Microsoft Copilot for Security](/security-copilot/authentication).

- **Intune plug-in source**: To use Copilot in Intune, you need the Intune plug-in enabled in Copilot for Security. This plug-in allows you to access your Intune data and use Copilot in the Intune admin center.

  Go to the [Copilot for Security portal](https://go.microsoft.com/fwlink/?linkid=2247989) and select **Sources** (prompt bar > right corner).

  :::image type="content" source="./media/copilot-intune-overview/security-copilot-sources.png" alt-text="Screenshot that shows the plugin sources that are available, enabled, and disabled in Microsoft Copilot for Security.":::

  In **Manage sources**, enable Microsoft Intune.

  :::image type="content" source="./media/copilot-intune-overview/intune-plug-in-enabled.png" alt-text="Screenshot that shows the Microsoft Intune plug-in source is enabled in the Microsoft Copilot for Security portal.":::

  > [!TIP]
  > Some roles can enable or disable plug-ins. For more information, see [Manage plug-ins in Microsoft Copilot for Security](/security-copilot/manage-plugins).

- **Your Intune data**: Copilot uses your Intune data. When an Intune admin submits a prompt, Copilot can only access the data that they have permissions to, which includes the [RBAC roles](../fundamentals/role-based-access-control.md) and [scope tags](../fundamentals/scope-tags.md) assigned to them.

> [!TIP]
> For some common questions asked about Copilot in Intune, go to [Microsoft Copilot in Intune FAQ](copilot-intune-faq.md).

## Start using Copilot in Intune

To access Copilot in Intune, sign into the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). The home screen lists the ways to get started with Copilot.

:::image type="content" source="./media/copilot-intune-overview/copilot-home-page.png" alt-text="Screenshot that shows the Intune admin center homepage with Copilot features in Microsoft Intune." lightbox="./media/copilot-intune-overview/copilot-home-page.png":::

Currently, there are three areas to use Copilot in Intune:

- Policy and setting management
- Device details and troubleshooting
- Device query

### Policy and setting management

Copilot is embedded in policy settings and with your existing policies.

#### ✅ Use Copilot to learn more about individual settings and recommended values

When you create an Intune policy, you add settings and configure these settings to meet your organization's requirements. When you add a setting, there's a Copilot tooltip.

:::image type="content" source="./media/copilot-intune-overview/compliance-policy-setting-copilot-tooltip.png" alt-text="Screenshot that shows Copilot settings tooltip in a compliance policy in Microsoft Intune and Intune admin center." lightbox="./media/copilot-intune-overview/compliance-policy-setting-copilot-tooltip.png":::

When you select the Copilot tooltip, the Copilot prompt window opens and provides more information about that setting.

:::image type="content" source="./media/copilot-intune-overview/compliance-policy-setting-prompt-results.png" alt-text="Screenshot that shows more information about a setting when you select the Copilot tooltip in a compliance policy in Microsoft Intune admin center.":::

In the Copilot window, there are more prompts that you can use. You can also select the prompt guide and select from an existing list of options.

:::image type="content" source="./media/copilot-intune-overview/compliance-policy-setting-copilot-prompt-guide.png" alt-text="Screenshot that shows the Copilot prompt guide when you add a setting in a compliance policy in Microsoft Intune and Intune admin center.":::

The Copilot prompts can help you understand the impact of the setting, look for potential conflicts, and provide a recommended value. For an example of how to use Copilot with the settings catalog, go to [Use the settings catalog to create device configuration policies](../configuration/settings-catalog.md).

You can use the Copilot tooltips on the following policy types in Intune:

- Compliance policies
- Device configuration policies, including the settings catalog
- Most endpoint security policies

#### ✅ Use Copilot to summarize an existing policy

On your existing Intune policies, you can use Copilot to summarize the policy. The summary describes what the policy does, the users and groups assigned to the policy, and the settings in the policy. This feature can help you understand the impact of a policy and its settings on your users and devices.

To use this feature in Intune, select an existing policy and then select **Summarize with Copilot**.

:::image type="content" source="./media/copilot-intune-overview/copilot-summarize-policy.png" alt-text="Screenshot that shows how to select the Summarize with Copilot feature in a policy in Microsoft Intune or Intune admin center.":::

You can use this feature on the following policy types in Intune:

- Compliance policies
- Device configuration policies, including the settings catalog
- Most endpoint security policies

### Device details and troubleshooting

#### ✅ Use Copilot to get device details and troubleshoot a device

You can use Copilot to get device-specific information, like the installed apps, group membership, and more.

To use this feature in Intune, select a device, and then select **Explore with Copilot**.

:::image type="content" source="./media/copilot-intune-overview/explore-with-copilot.png" alt-text="Screenshot that shows where you select any device and then select Explore with Copilot in Microsoft Intune and Intune admin center.":::

When the Copilot window opens, select a prompt and enter any required or optional input, if needed. You can also open the prompt guide for some follow-up questions.

:::image type="content" source="./media/copilot-intune-overview/device-prompt-guide.png" alt-text="Screenshot that shows the Copilot prompt guide after you select a device in Microsoft Intune or Intune admin center.":::

For more information about using Copilot with your devices, go to [Use Microsoft Copilot in Intune to troubleshoot devices](../copilot/copilot-devices.md).

> [!TIP]
> You can also use Copilot to help you troubleshoot device issues using device query. For more details see the [following section](#query-with-copilot-in-device-query).

### Query with Copilot in device query

You can use Copilot to help you create Kusto Query Language (KQL) queries to run when using device query in Intune.

> [!NOTE]
> To use Device query in your tenant, you must have a license that includes Microsoft Intune Advanced Analytics. For more information, see [Intune add-ons](../fundamentals/intune-add-ons.md#microsoft-intune-advanced-analytics).

To use this feature in Intune, select a device, select **Device query**, and then select **Query with Copilot**.

When the Copilot window opens, enter your question about the device. If device query supports the properties needed to answer the question, Copilot will generate a KQL query that you can use to get the data that you require.

:::image type="content" source="./media/copilot-intune-overview/copilot-device-query.png" alt-text="Screenshot that shows the Copilot window with your prompt for device query." lightbox="./media/copilot-intune-overview/copilot-device-query.png":::

To use the query that Copilot generates, select **Add to editor** to add it to the query editor in device query, or select **Add and run** to add it to the editor and automatically run it. Select **How was this query generated?** to see an explanation generated by Copilot for how it created a query in response to your request.

Here are some example queries you can try:

- Is Defender running on this device?
- Show me the last 5 app crash events on this device.
- What are the top 10 processes using the most memory on this device?
- Show me expired certificates on this device.
- Show me the last 20 most recently created files in C:\Windows\folderPath
- Does this device support TPM 2.0?
- Show me drivers on this device grouped by provider name.

    > [!NOTE]
    > Copilot can only generate queries for requests related to the properties that are supported by device query. You cannot use this feature to ask Copilot for details about the device beyond what is available in device query.
For a full list of supported properties in device query, go to [Device query](../../analytics/device-query.md).

## Related content

- [Use Microsoft Copilot in Intune to troubleshoot devices](../copilot/copilot-devices.md).
- [Use the settings catalog to create device configuration policies](../configuration/settings-catalog.md).
- [Learn more about Intune capabilities in Microsoft Copilot for Security](security-copilot.md).
