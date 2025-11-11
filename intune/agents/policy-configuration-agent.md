---
title: Learn about Policy Configuration Agent and set it up
description: Learn about the Policy Configuration Agent in Microsoft Intune, its prerequisites, how it works, and how to set it up. The agent is a generative AI feature that helps create Intune policies based on uploaded documents or benchmarks. The Policy Configuration Agent is a feature of Security Copilot in Intune.
ms.date: 11/10/2025
ms.topic: overview
author: mandiohlinger
ms.author: mandia
ms.reviewer: aanavath, jubaptis
---

# Policy Configuration Agent in Microsoft Intune

> [!WARNING]
> This article is still being written. Do not use it or share any information from this article.

The Intune Policy Configuration Agent uses the generative AI-powered features in Security Copilot. It automates the task of reading through standards and finding the corresponding device configuration settings.

Admins can quickly generate Intune [settings catalog](../intune-service/configuration/settings-catalog.md) policies that align with organizational or regulatory baselines, including any hardening initiatives.

With the agent, you:

- Upload a document or industry benchmark, and the agent identifies relevant and matching Intune settings.

  You can upload compliance standards and common industry benchmarks, like Security Technical Implementation Guides (STIGs), National Institute of Standards and Technology (NIST) guidelines, Defense Information Systems Agency (DISA) STIGs, and Center for Internet Security (CIS) benchmarks.

- Can upload internal policy documents and baselines, like your organization's security policies or compliance requirements.
- Get relevant configuration settings and actionable suggestions based on your uploaded documents.

  The recommendations include explanations, answering the "why" behind each setting. Admins can learn from this information and improve their own knowledge of Intune settings and security principles.??Do they? Or was this removed??

- Can customize the suggestions to create a baseline that fits your environment. For example, if your organization has an exception to a CIS rule, you can remove that rule from the final policy.

The agent also guides you through creating a policy using the suggestions and helps configure each setting based on your organization's needs. It provides insights into each setting's benefits and potential implications, and can highlight supported, unsupported, and unmappable rules. You can also review and save these suggestions.

This article:

- Lists the prerequisites to use the agent
- Explains how the agent works
- Shows you how to set up the agent
- Shows you how to renew or remove the agent

To learn how to use the agent, see [Use the Policy Configuration Agent](policy-configuration-agent-use.md).

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [cloud](../includes/requirements/cloud.md)]

:::column-end:::
:::column span="3":::
> The agent is supported on the public cloud ony. It isn't supported on government clouds.

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::
> To use Security Copilot agents in Microsoft Intune, the following licenses are required:
>
> - [Microsoft Intune Plan 1 subscription](../intune-service/fundamentals/licenses.md)
> - [Microsoft Security Copilot](/copilot/security/get-started-security-copilot) with sufficient security compute units (SCUs)
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/plugins.md)]

:::column-end:::
:::column span="3":::
> Plugins enable Security Copilot agents to connect with Microsoft services and perform specialized actions. This agent requires the following plugin:
>
> - [!INCLUDE [plugin-intune](includes/plugin-intune.md)]
>
> If you use Copilot in the Intune, then the Intune plugin is already enabled. [Learn more about plugins](https://go.microsoft.com/fwlink/?linkid=2316474).

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
> This feature supports the following platforms:
>
> - Windows
> - Devices must be corporate owned, enroled in Intune (includes co-managed), and Microsoft Entra joined.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> To **enable and configure** the agent, use an account with the following roles:
>
> :::image type="icon" source="../media/icons/admin-center/entra.svg" border="false"::: Microsoft Entra roles:
> - [Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator)
>
> :::image type="icon" source="../media/icons/admin-center/copilot.svg" border="false"::: Security Copilot roles:
> - [Copilot owner](/copilot/security/authentication#security-copilot-roles)
>
> ---
>
> To **use** the agent and create policies, use an account with the following roles:
>
> :::image type="icon" source="../media/icons/admin-center/copilot.svg" border="false"::: Security Copilot roles:
> - [Copilot Contributor](/copilot/security/authentication#security-copilot-roles)
>
> :::image type="icon" source="../media/icons/admin-center/intune.svg" border="false"::: Intune roles:
> - [Policy and Profile manager](../intune-service/fundamentals/role-based-access-control-reference.md#policy-and-profile-manager) or a [Custom role](../intune-service/fundamentals/role-based-access-control.md#custom-roles) with the following permissions:
>   - Device configurations/Create
>   - Device configurations/Update

:::column-end:::
:::row-end:::

## How the agent works

:::image type="content" source="./media/policy-agent-workflow-svg.png" alt-text="Diagram that shows different steps and stages of the policy configuration agent workflow in Microsoft Intune." lightbox="./media/policy-agent-workflow-svg.png":::

At a high level, the agent does the following steps.

1. **Input ingestion**: You give the agent an input that has your policy requirements. It can be a document you upload or direct text input, like `All laptops must have BitLocker enabled with AES-256 encryption`.

    The agent supports well-known baseline formats, like official CIS benchmarks or DISA STIG checklists, custom documents, and bulleted lists of requirements.

2. **Natural language processing and parsing**: When you run the agent against your input, the agent uses Security Copilot's natural language-to-policy mapping skill and parses the input. It reads through the language and identifies individual settings that the text describes.

    For example, if the document says "Disallow use of USB storage devices", then the agent interprets the text as a requirement about external storage policy.

    Security Copilot is tuned to recognize common policy statements and technical controls from textual descriptions. It can handle complex wording or varied formats.

3. **Maps rules to Intune settings**: For each parsed requirement, the agent attempts to find a corresponding settings catalog setting that achieves that goal. The agent uses built-in knowledge of Intune's capabilities to choose the correct setting and the setting value that meets the requirement.

4. **Generates policy suggestions**: The agent compiles the mapping results into a draft Intune configuration profile (or set of profiles) with the recommended settings.

5. **Admin review and confirmation**: Before anything is applied, you review the agent's output. In the admin center, select the agent's suggestion to see the details. You might see a list of recommended settings (supported mappings) and separate lists for unsupported or unmapped items.

    At this stage, you should:

    - **View Details** - You can drill into each recommended setting to read the rationale and adjust. For instance, if the agent suggests a password length of 14 characters because the baseline said `at least 12`, then you might increase it to 15 in the final policy.
    - **Remove or Exclude** - If there are certain suggestions you don't want to implement, then you can remove them from the final policy.
    - **Acknowledge Unsupported Items** - For any requirements that Intune can't enforce, document how you plan to handle them, or acknowledge them. The agent's role is informational and to make sure you're aware of any gaps.

6. **Policy creation**: After you confirm the suggestions, you can select to automatically create a new configuration profile with all the recommended settings. This settings catalog policy isn't enforced until you assign it, just like any Intune policy you manually create.

    At this stage, the policy is a normal Intune policy. You can assign it to the appropriate groups and name the policy. You might be able to save the mappings and reuse them as a baseline, like an AI-mapped template, without creating a policy. This feature allows you to generate an audit report or use the mappings in other policies later.

7. **Deploy and monitor**: Once the policy is assigned, devices start reporting compliance with the new settings. The agent's job is done until you run it again.

    Any agent suggestions you apply are tracked. If you rerun the agent with the same baseline file later, like when the baseline is updated in six months, it can compare the applied settings so it doesn't duplicate suggestions.

## Set up the agent

The agent runs under the identity and permissions of the account used during this setup. Its actions are limited to the permissions of that account, and the identity refreshes with each run. So, any changes to the account's permissions affect the agent's capabilities during its next run.

We recommend you sign in with the **Intune Administrator** Microsoft Entra role to set up the agent.

Use the following steps to set up the agent.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Policy Configuration Agent**.
1. In **Overview**, select **Set up agent**.

    The **Set up Policy Configuration Agent** pane lists the required permissions to set up the agent, and provides more information about the setup requirements.

1. Select **Set up agent**.

When it's finished, the agent is ready to use. To learn more about using the agent, see [Use the Policy Configuration Agent](policy-configuration-agent-use.md).

[!INCLUDE [renew](includes/renew.md)]

[!INCLUDE [remove](includes/remove.md)]

## Related content

- [Use the Policy Configuration Agent](policy-configuration-agent-use.md)
- [Security Copilot agents in Intune - An overview](index.md)
- [Security Copilot in Intune - An overview](../intune-service/copilot/copilot-intune-overview.md)
