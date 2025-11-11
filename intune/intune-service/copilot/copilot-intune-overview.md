---
title: Security Copilot in Intune features overview
description: Microsoft Security Copilot in Intune is an AI platform. It can help you create policies, get information about existing policies, and show more details on specific settings, including their impacts on users and devices. You can also use Copilot to troubleshoot device issues and query devices.
ms.date: 11/17/2025
ms.update-cycle: 180-days
ms.topic: get-started
ms.reviewer: ankurgoyal, rashok, zadvor
ms.collection:
- M365-identity-device-management
- highpri
- highseo
- security-copilot
- msec-ai-copilot
---

# Microsoft Copilot in Intune

[Microsoft Security Copilot](/copilot/security/microsoft-security-copilot) is a generative-AI security analysis tool. It can help you and your organization get information quickly and make decisions that affect security and risk.

Intune has capabilities that are powered by Security Copilot. These capabilities access your Intune data and help you manage your policies and settings, understand your security posture, and troubleshoot device issues.

There are two ways to access your Intune data using Copilot:

- **Microsoft Copilot in Intune** (this article): Copilot is embedded in Intune and is available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). The Copilot prompts and their output are in the context of Intune and your Intune and Windows 365 Cloud PC data. These capabilities access your Intune and Windows 365 Cloud PC data. They can help you manage your policies and settings, understand your security posture, and troubleshoot device issues, including Windows 365 Cloud PCs.

  This experience has an IT admin/IT Pro focus.

- **Microsoft Security Copilot**: This option is a standalone Copilot and is available in the [Microsoft Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989). You can use this portal to get insights from Security Copilot for all your enabled services, like Intune, Microsoft Defender, Microsoft Entra ID, Microsoft Purview, and more.

  This experience has a Security Operations Center (SOC) focus and can be used by IT admins. For more information, see [Security Copilot in Microsoft Intune](security-copilot.md).

This article focuses on Copilot in Intune and describes the Intune features that you can use with Copilot.

## Before you begin

To use Copilot in Intune, you should know the following information:

- **Copilot security compute units (SCUs)**: Copilot in Intune is included with Security Copilot. There aren't any other licensing requirements or Intune-specific licenses for using Copilot in Intune.

  For more information about SCUs, see:

  - [Get started with Security Copilot](/copilot/security/get-started-security-copilot)
  - [Manage capacity in Security Copilot](/copilot/security/manage-usage)

- **Copilot configuration**: Before you can use the Copilot features in Intune, Security Copilot must be configured, and you must complete the first run tour in the [Microsoft Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989). For the setup tasks, see [Get started with Microsoft Security Copilot](/copilot/security/get-started-security-copilot).

  You can check the status in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Copilot**.

  :::image type="content" source="./media/copilot-intune-overview/tenant-administration-copilot-enabled.png" alt-text="Screenshot that shows Copilot is enabled in the Microsoft Intune tenant and Intune admin center." lightbox="./media/copilot-intune-overview/tenant-administration-copilot-enabled.png":::

- **Copilot roles**: Access to Copilot in Intune is managed through Security Copilot or Microsoft Entra ID. To use Copilot in Intune, you or your admin team must be assigned the appropriate role in Security Copilot or Microsoft Entra ID. There isn't a built-in Intune role that has access to Copilot.

  The **Intune Administrator** role in Microsoft Entra ID has access to Copilot in Intune by default. Other roles can be assigned access to Copilot in Intune through Security Copilot.

  For more information, see [Roles and authentication in Microsoft Security Copilot](/copilot/security/authentication).

- **Intune plug-in source**: To use Copilot in Intune, you need the Intune plug-in enabled in Security Copilot. This plug-in allows you to access your Intune data and use Copilot in the Intune admin center.

  Go to the [Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989) and select **Sources** (prompt bar > right corner).

  :::image type="content" source="./media/copilot-intune-overview/security-copilot-sources.png" alt-text="Screenshot that shows the plugin sources that are available, enabled, and disabled in Microsoft Security Copilot." lightbox="./media/copilot-intune-overview/security-copilot-sources.png":::

  In **Manage sources**, enable Microsoft Intune.

  :::image type="content" source="./media/copilot-intune-overview/intune-plug-in-enabled.png" alt-text="Screenshot that shows the Microsoft Intune plug-in source is enabled in the Microsoft Security Copilot portal." lightbox="./media/copilot-intune-overview/intune-plug-in-enabled.png":::

  > [!TIP]
  > Some roles can enable or disable plug-ins. For more information, see [Manage plug-ins in Microsoft Security Copilot](/copilot/security/manage-plugins).

  To use Copilot in Intune for Windows 365 Cloud PCs, in the [Security Copilot portal](https://securitycopilot.microsoft.com) > **Sources**, enable **Windows 365**.

- **Your Intune data**: Copilot uses your Intune data. When an Intune admin submits a prompt, Copilot can only access the data that they have permissions to, which includes the [RBAC roles](../fundamentals/role-based-access-control.md) and [scope tags](../fundamentals/scope-tags.md) assigned to them.

> [!TIP]
> For some common questions asked about Copilot in Intune, go to [Copilot in Intune FAQ](copilot-intune-faq.md).

## Start using Copilot

To access Copilot in Intune, sign into the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). In the banner at the top, select **Copilot**.

:::image type="content" source="./media/copilot-intune-overview/copilot-banner.png" alt-text="Screenshot that shows the Intune admin center banner with the Copilot button in Microsoft Intune." lightbox="./media/copilot-intune-overview/copilot-banner.png":::

You can use Copilot in Intune for:

- Data exploration using natural language
- Policy and setting management
- Device details and troubleshooting
- Analyzing Endpoint Privilege Management (EPM) requests
- Troubleshooting Microsoft Surface devices
- Gaining insights about Windows 365 Cloud PCs

## Intune agents

Security Copilot agents in Intune are AI-powered assistants that help strengthen enterprise security by automating key tasks. These agents help streamline endpoint protection, identity management, threat intelligence, and device configuration.

Intune includes specialized agents for common scenarios:

- **[Change Review Agent](../../agents/change-review-agent.md)** – Evaluates multi-admin approval requests and recommends actions.
- **[Device Offboarding Agent](../../agents/device-offboarding-agent.md)** – Identifies stale or misaligned devices and provides insights before offboarding the devices.
- **[Policy Configuration Agent](../../agents/policy-configuration-agent.md)** – Converts plain-language instructions or documents into recommended settings and policies.
- **[Vulnerability Remediation Agent](../../agents/vulnerability-remediation-agent.md)** – Uses Defender data to monitor vulnerabilities and prioritize remediation with AI-driven risk assessments.

These agents help IT teams quickly address vulnerabilities, policy gaps, and emerging threats.

To learn more, see [Security Copilot agents in Intune overview](../../agents/index.md).

## Data exploration

Using natural language, you can query and explore your Intune data, including data about your devices, users, apps, policies, updates, and compliance. There are also built-in examples that help you understand the kinds of questions you can ask.

When you run a query, Copilot summarizes the results and recommends actions you can take based on the query results. You can also use the query output to add users or devices to groups, and create custom reports.

To learn more, see [Explore Intune data and get Copilot recommendations](copilot-intune-explorer.md).

## Copilot Chat prompt suggestions

Copilot Chat can be accessed from any page in Intune by selecting the Copilot button on the top banner.

When Copilot Chat opens, use natural language to ask Copilot a question. An intelligent search matches your request to available prompts that are built into Intune. These prompts are offered as suggestions.

:::image type="content" source="./media/copilot-intune-overview/copilot-chat-sample-suggestion.png" alt-text="Screenshot that shows the Copilot Chat prompt box and suggested prompts in Microsoft Intune." lightbox="./media/copilot-intune-overview/copilot-chat-sample-suggestion.png":::

The suggestions are dynamic and update as you type your question. You can continue typing to make your request more specific, or try a different natural language wording if you can't find what you're looking for.

The prompt suggestions are broken into three sections - **Suggestions**, **Explore your data**, and **Check documentation**.

### ✅ Suggestions

The prompts on this section are specific to Intune scenarios, like device troubleshooting and policy & setting management. This list also includes prompts to troubleshoot Microsoft Surface devices and get insights about your Windows 365 Cloud PCs.

For example, you can enter `summarize` to see a list of summarize-related suggestions:

:::image type="content" source="./media/copilot-intune-overview/summarize-show-suggestions.png" alt-text="Screenshot that shows the Copilot Chat prompt box when you enter summarize and show the suggested prompts in Microsoft Intune." lightbox="./media/copilot-intune-overview/summarize-show-suggestions.png":::

If a prompt requires more information, you're prompted to enter that information. For example, if you select the **Summarize an Intune device** suggestion, you're prompted to enter the device ID:

:::image type="content" source="./media/copilot-intune-overview/copilot-chat-prompt-enter-device-id.png" alt-text="Screenshot that shows the Copilot Chat prompt box when you enter the device ID for the Summarize an Intune device suggestion in Microsoft Intune." lightbox="./media/copilot-intune-overview/copilot-chat-prompt-enter-device-id.png":::

### ✅ Explore your data

Copilot Chat includes all the prompts that you can use to explore your Intune data. In your prompt, you might see the **Explore further** option:

:::image type="content" source="./media/copilot-intune-overview/go-to-explorer.png" alt-text="Screenshot that shows the Explore further option in Copilot Chat in Microsoft Intune." lightbox="./media/copilot-intune-overview/go-to-explorer.png":::

When you select **Explore further**, you're redirected with your prompt already filled out in the Explorer prompt box. In our example, select **Platform** and then select your platform from the list:

:::image type="content" source="./media/copilot-intune-overview/explorer-redirect.png" alt-text="Screenshot that shows the Explorer prompt box with the filled-out prompt in Microsoft Intune." lightbox="./media/copilot-intune-overview/explorer-redirect.png":::

To learn more, see [Explore your Intune data](copilot-intune-explorer.md).

### ✅ Check documentation

Copilot Chat allows you to ask a question directly to the Microsoft documentation. As you type, the prompt in the **Check documentation** section dynamically updates to the question you're typing. Select this prompt to learn more in the Microsoft documentation.

:::image type="content" source="./media/copilot-intune-overview/check-documentation.png" alt-text="Screenshot that shows the Check documentation prompt in Copilot Chat in Microsoft Intune." lightbox="./media/copilot-intune-overview/check-documentation.png":::

## Policy and setting management

Copilot is embedded in policy settings and with your existing policies.

### ✅ Use Copilot to learn more about individual settings and recommended values

When you create an Intune policy, you add settings and configure these settings to meet your organization's requirements. When you add a setting, there's a Copilot tooltip.

:::image type="content" source="./media/copilot-intune-overview/compliance-policy-setting-copilot-tooltip.png" alt-text="Screenshot that shows Copilot settings tooltip in a compliance policy in Microsoft Intune and Intune admin center." lightbox="./media/copilot-intune-overview/compliance-policy-setting-copilot-tooltip.png":::

When you select the Copilot tooltip, the Copilot prompt window opens and provides more information about that setting.

:::image type="content" source="./media/copilot-intune-overview/compliance-policy-setting-prompt-results.png" alt-text="Screenshot that shows more information about a setting when you select the Copilot tooltip in a compliance policy in Microsoft Intune admin center.":::

You can get more insights about this setting by asking questions like:

- Has this setting been configured in any other policies?
- Does Microsoft recommend any particular value for this setting?
- How could this setting affect users?
- How could this setting affect security?

These Copilot prompts can help you understand the effect of the setting, look for potential conflicts, and provide a recommended value. For an example of how to use Copilot with the settings catalog, go to [Use the settings catalog to create device configuration policies](../configuration/settings-catalog.md).

You can use the Copilot tooltips on the following policy types in Intune:

- Compliance policies
- Device configuration policies, including the settings catalog
- Most endpoint security policies

### ✅ Use Copilot to summarize an existing device configuration policy

On your existing Intune configuration policies, you can use Copilot to summarize the policy. The summary describes what the policy does, the users and groups assigned to the policy, and the settings in the policy. This feature can help you understand the effect of a policy and its settings on your users and devices.

To use this feature in Intune, select an existing policy and then select **Summarize with Copilot**.

:::image type="content" source="./media/copilot-intune-overview/copilot-summarize-policy.png" alt-text="Screenshot that shows how to select the Summarize with Copilot feature in a device configuration policy in Microsoft Intune or Intune admin center.":::

You can use this feature on device configuration policies, including the settings catalog, and most endpoint security policies.

### ✅ Use Copilot to analyze compliance policies

On your existing Intune compliance policies, you can use Copilot to analyze different aspects of the policy. The prompt guide can help summarize what the policy does, effect of the policy and its settings on your users, and security. You can also use Copilot to help get compliance policies that have conflicting settings.

:::image type="content" source="./media/copilot-intune-overview/compliance-policy-prompt-options.png" alt-text="Screenshot that shows the Copilot prompt options for compliance policies in Microsoft Intune or Intune admin center." lightbox="./media/copilot-intune-overview/compliance-policy-prompt-options.png":::

## Device details and troubleshooting

### ✅ Use Copilot to get device details and troubleshoot a device

You can use Copilot to get device-specific information, like the installed apps, group membership, and more.

To use this feature in Intune, select a device, and then select **Summarize with Copilot**. Copilot Chat opens and executes the prompt:

:::image type="content" source="./media/copilot-intune-overview/summarize-with-copilot.png" alt-text="Screenshot that shows you can select any device and then select Summarize with Copilot in Microsoft Intune and Intune admin center.":::

This step automatically opens Copilot chat (if it's not already open), and executes the prompt.

For more information about using Copilot with your devices, go to [Use Copilot in Intune to troubleshoot devices](../copilot/copilot-devices.md).

### ✅ Use Copilot to create KQL queries to get device details

You can use Copilot to help you create Kusto Query Language (KQL) queries to run when using device query in Intune.

> [!NOTE]
> To use Device query in your tenant, you must have a license that includes Microsoft Intune Advanced Analytics. For more information, see [Intune add-ons](../fundamentals/intune-add-ons.md#microsoft-intune-advanced-analytics).

You can use this feature for an individual device or for many devices.

#### Query a single device

To query a single device in Intune, go to **Devices** > **All devices** > select a device, and then select **Monitor** > **Device query**.

In Copilot Chat, enter your question about the device. If device query supports the properties needed to answer the question, then Copilot generates a KQL query that you can use.

:::image type="content" source="./media/copilot-intune-overview/single-device-query.png" alt-text="Screenshot that shows Copilot Chat with your prompt for a single device KQL query in Microsoft Intune." lightbox="./media/copilot-intune-overview/single-device-query.png":::

You can use the suggested query or enter your own query to generate the KQL. Copilot generates the KQL and also provides an explanation of how Copilot created a query in response to your request.

The following examples are some queries you can try:

- Is Defender running on this device?
- Show me the last 5 app crash events on this device.
- What are the top 10 processes using the most memory on this device?
- Show me expired certificates on this device.
- Show me the last 20 most recently created files in C:\Windows\folderPath
- Does this device support TPM 2.0?
- Show me drivers on this device grouped by provider name.

> [!NOTE]
> Copilot can only generate queries for requests related to the properties that device query supports. You can't use this feature to ask Copilot for details about the device beyond what is available in device query. For a full list of supported properties in device query, go to [Device query](../../analytics/device-query.md).

#### Query many devices

To query data across many devices in Intune, select **Devices** > **Device query**.

In Copilot Chat, enter your question about the devices. If device query supports the properties needed to answer the question, then Copilot generates a KQL query that you can use.

:::image type="content" source="./media/copilot-intune-overview/multiple-device-query.png" alt-text="Screenshot that shows Copilot Chat for querying many devices using KQL in Microsoft Intune." lightbox="./media/copilot-intune-overview/multiple-device-query.png":::

You can select the options that Copilot generates to quickly generate a KQL query. Or, you can enter your question or request other device data. To make a new request, ask your new question in Copilot Chat.

The following examples are some queries you can try:

- Which devices aren't encrypted?
- Show me Windows 11 devices.
- Which devices have a hot fix?
- Show me TPM 2.0 devices.
- Show me devices sorted by manufacturer.
- Which devices haven't been patched in the last 30 days?

## Related content

- [Use Copilot in Intune to troubleshoot devices](../copilot/copilot-devices.md).
- [Use the settings catalog to create device configuration policies](../configuration/settings-catalog.md).
- [Learn more about Intune capabilities in Microsoft Security Copilot](security-copilot.md).
