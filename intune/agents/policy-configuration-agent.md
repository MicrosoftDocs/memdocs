---
title: Learn about Policy Configuration Agent and set it up
description: Learn about the Policy Configuration Agent in Microsoft Intune, its prerequisites, how it works, and how to set it up. The agent is a generative AI feature that helps create Intune policies based on uploaded documents or benchmarks.
ms.date: 11/06/2025
ms.topic: overview
author: mandiohlinger
ms.author: mandia
ms.reviewer: aanavath, jubaptis
---

# Policy Configuration Agent in Microsoft Intune

> [!WARNING]
> This article is still being written. Do not use it or share any information from it.

The Intune Policy Configuration Agent uses the generative AI-powered features in Security Copilot. It automates the traditionally manual task of reading through standards and finding the corresponding device configuration settings. Adminis can quickly generate Intune policy profiles that align with organizational or regulatory baselines, including any hardening initiatives.

With the agent, you:

- Upload a document or industry benchmark, and the agent identifies relevant and matching Intune settings. You can upload compliance standards and common industry benchmarks, like Security Technical Implementation Guides (STIGs), National Institute of Standards and Technology (NIST) guidelines, Defense Information Systems Agency (DISA) STIGs, and Center for Internet Security (CIS) benchmarks.
- Can upload internal policy documents and baselines, like your organization's security policies or compliance requirements.
- Get relevant configuration settings and actionable suggestions based on your uploaded documents. The recommendations include explanations, answering the "why" behind each setting. Over time, admins can learn from this information and improve their own knowledge of Intune settings and security principles.
- Can customize the suggestions to create a baseline that fits your environment. For example, if your organization has an exception to a CIS rule, you can remove that rule from the final policy.

The agent also guides you through creating a policy using the suggestions and helps configure each setting based on your organization's needs. It provides insights into each setting's benefits and potential implications, and can highlight supported, unsupported, and unmappable rules. You can also review and save these suggestions.

This article:

- Lists the prerequisites to use the agent
- Explains how the agent works
- Shows you how to set up the agent
- Shows you how to renew or remove the agent

To learn how to use the agent, see [Use the Policy Configuration Agent](policy-configuration-agent-use.md).

This feature applies to:

- Windows

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
> To use Security Copilot agents in Microsoft Intune, your organization must meet specific licensing requirements.
>
> Required licenses:
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
> Plugins enable Security Copilot agents to connect with Microsoft services and perform specialized actions. If you use Copilot in the Intune, then the Intune plugin is already enabled.
>
> This agent requires the following plugin:
>
> - [!INCLUDE [plugin-intune](includes/plugin-intune.md)]
>
> [Learn more about plugins](https://go.microsoft.com/fwlink/?linkid=2316474).

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
> Role requirements vary based on whether you're configuring the agent or using it, and on the specific actions performed.
>
> ---
>
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
> :::image type="icon" source="../media/icons/admin-center/intune.svg" border="false"::: Roles:
> - [Copilot Contributor Security Copilot role](/copilot/security/authentication#security-copilot-roles)
> - [Policy and Profile manager Intune role](../intune-service/fundamentals/role-based-access-control-reference.md#policy-and-profile-manager) or a [Custom Intune role](../intune-service/fundamentals/role-based-access-control.md#custom-roles) with the following permissions:
>   - Device configurations/Create
>   - Device configurations/Update

:::column-end:::
:::row-end:::

## How the agent works

:::image type="content" source="./media/policy-agent-workflow.svg" alt-text="Diagram that shows different steps and stages of the policy configuration agent workflow in Microsoft Intune.":::

At a high level, the agent does the following steps:

1. **Input ingestion**: You give the agent an input that has your policy requirements. It can be a document you upload or direct text input, like `All laptops must have BitLocker enabled with AES-256 encryption`.

    The agent supports well-known baseline formats, like official CIS benchmarks or DISA STIG checklists, custom documents, and bulleted lists of requirements.

2. **Natural language processing and parsing**: When you run the agent against your input, the agent uses Security Copilot's natural language-to-policy mapping skill and parses the input. It reads through the language and identifies individual policy rules or settings that the text describes.

    For example, if the document says "Disallow use of USB storage devices", then the agent interprets the text as a distinct requirement about external storage policy.

    Security Copilot is tuned to recognize common policy statements and technical controls from textual descriptions. It can handle complex wording or varied formats.

3. **Maps rules to Intune settings**: For each parsed requirement, the agent attempts to find a corresponding settings catalog setting or other Intune policy (??) that achieves that goal. The agent uses built-in knowledge of Intune's capabilities to choose the correct setting and the setting value that meets the requirement. The agent classifies each rule into the following categories:

    - **Supported** – There's a direct Intune setting available. The agent maps the rule to that setting and proposes a configuration. For example, `Disable USB storage` maps to the **Removable Storage: Deny write access = Enabled** in a device restriction policy. ??This won't find an SC policy??
    - **Unsupported** – There isn't a built-in Intune setting for this requirement. The agent notes that the rule is unsupported, meaning Intune alone can't enforce it. For example, a rule about a very niche OS setting that Intune can't manage would be flagged.
    - **Unmappable/Ambiguous** – The agent couldn't confidently determine a matching setting. It highlights these settings so admins can review. In some cases, it can happen due to ambiguous phrasing or a requirement that needs clarification.

    The agent also generates a confidence score for each mapping. If the text clearly matches a known setting (high confidence), then it proceeds. If not, it marks the suggestion as low confidence, suggesting you should confirm that mapping.

4. **Generates policy suggestions**: The agent compiles the mapping results into a draft Intune configuration profile (or set of profiles) with the recommended settings.

    For each setting, the agent shows:

    - The name of the Intune policy setting
    - The proposed value
    - The original requirement text it maps to
    - An AI-generated rationale that explains why the setting meets the requirement or any assumptions made

    For example, you can see something like **Setting X is enabled to enforce Y, as required by your policy document's section 3.1**.

    If any settings are unsupported, then they're listed with an explanation, like **Intune cannot enforce requirement Z directly; consider alternate controls**. The suggestion can also include metadata like the platform it applies to, relevant scope (if deducible), and the confidence level.

5. **Admin review and confirmation**: Before anything is applied, you review the agent's output. In the admin center, select the agent's suggestion to see the details. You might see a list of recommended settings (supported mappings) and separate lists for unsupported or unmapped items. At this stage, you can:

    - **View Details**: You can drill into each recommended setting to read the rationale and adjust. For instance, if the agent suggests a password length of 14 characters because the baseline said `at least 12`, then you might increase it to 15. You can make edits to the proposed values before saving.
    - **Remove or Exclude**: If there are certain suggestions you don't want to implement, then you can remove them from the draft policy.
    - **Acknowledge Unsupported Items**: For any requirements that Intune can't enforce, document how you plan to handle them outside of Intune, or acknowledge them. The agent's role is informational and to make sure you're aware of any gaps.

6. **Policy creation**: After you confirm the suggestions, select **Accept and create policy** to automatically create a new configuration profile with all the recommended settings. This policy isn't enforced until you assign it, just like any Intune policy you manually create.

    At this stage, the policy is a normal Intune policy. You can assign it to the appropriate groups and name the policy. You might be able to save the mappings as a reusable baseline object (an AI-mapped template) without immediately creating a policy. This feature allows you to generate an audit report or use the mappings in other policies later.

7. **Deploy and monitor**: Once the policy is assigned, devices start reporting compliance with the new settings. The agent's job is done until you run it again.

    Any agent suggestions you apply are tracked. If you rerun the agent with the same baseline file later (maybe the baseline is updated in six months), it can compare the applied settings so it doesn't duplicate suggestions.

## Set up the agent

The agent runs under the identity and permissions of the account used during this setup. Its actions are limited to the permissions of that account, and the identity refreshes with each run. So, any changes to the account's permissions affect the agent's capabilities during its next run. We recommend you sign in with the Intune Administrator Microsoft Entra role to set up the agent.

Use the following steps to set up the agent.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Policy Configuration Agent**.
1. In **Overview**, select **Set up agent**.

    The **Set up Policy Configuration Agent** pane lists the required permissions to set up the agent, and provides more information about the setup requirements.

1. Select **Set up agent**.

[!INCLUDE [renew](includes/renew.md)]

[!INCLUDE [remove](includes/remove.md)]

## Related content

- [Use the Policy Configuration Agent](policy-configuration-agent-use.md)
- [Security Copilot agents in Intune - An overview](index.md)
- [Security Copilot in Intune - An overview](../intune-service/copilot/copilot-intune-overview.md)
