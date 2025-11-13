---
title: Use the Policy Configuration Agent to create policies
description: Learn how to use the Policy Configuration Agent in Microsoft Intune to create policies. You can create policies on files you uploaded, natural language prompts, or industry baselines. The Policy Configuration Agent is a feature of Security Copilot in Intune.
ms.date: 11/13/2025
ms.topic: how-to
author: mandiohlinger
ms.author: mandia
ms.reviewer: aanavath
---

# Use the Policy Configuration Agent

> [!WARNING]
> This article is still being written. Do not use it or share any information from this article.

The [Policy Configuration Agent](policy-configuration-agent.md) is a generative AI feature in Intune. It helps IT admins translate complex requirements and industry standard documents into actionable Intune settings.

After you [set up the agent](policy-configuration-agent.md), the next step is to upload documents and benchmarks as **knowledge sources**. Or, enter natural language instructions on what to include in the policy draft. The agent analyzes these knowledge sources to suggest relevant Intune settings and then can create device configuration policies using these settings.

This article shows you how to use the Policy Configuration Agent, including:

- Adding, saving, and viewing a knowledge source
- Creating a policy from a knowledge source and natural language prompts

To learn about the agent and how to set it up, see [Set up the Policy Configuration Agent](policy-configuration-agent.md).

This feature applies to:

- Windows

## Before you begin

- This feature is in [public preview](../intune-service/fundamentals/public-preview.md).
- Make sure you meet the [Policy Configuration Agent](policy-configuration-agent.md#prerequisites) prerequisites, including signing in with an appropriate account.
- You can upload one knowledge source file at a time. If you have multiple baseline documents, run them separately through the agent.
- Well-structured, well-written input results in better mappings. If a document is poorly formatted or uses unclear language, the agent can produce low-confidence matches. We recommend you review your source documents for clarity.
- You can add text files up to 25 KB in size. Large or complex documents with hundreds of pages of requirements might challenge the agent's ability to process them effectively.

## Explore the agent

To explore and use the agent, open the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Policy Configuration Agent**.

The following tabs are available:

# [Overview](#tab/overview)

The **Overview** tab is the landing page for the agent. It provides a summary of the agent's policy suggestions and recent activity.

After the agent completes a run, this tab updates with the agent's suggestions. Only new and in progress policy suggestions are shown.

You can also:

- View the agent's availability.
- View the suggestions based on the information you uploaded or entered. You can select any suggestion to see more details and save the setting mapping for future use.
- View the activity section to see the agent's current and past run activity.

# [Knowledge](#tab/knowledge)

The **Knowledge** tab shows the knowledge sources you uploaded and other important information about the source, like its status.

In this tab, you can:

- Search and filter to find specific knowledge sources.
- View the knowledge source status, like New, In progress, Completed, and Dismissed.
- Select a knowledge source to see all the settings and their recommended values.
- Delete a knowledge source.

# [Suggestions](#tab/suggestions)

The **Suggestions** tab shows a list of the agent's suggestions based on the input you selected, including any natural language prompts. After the agent completes a run, this tab updates with the agent's suggestions.

In this tab, you can:

- Search and filter to find specific suggestions.
- View the suggestion status, like New, In progress, Completed, and Dismissed.
- Select a suggestion to see the settings and their recommended values. When you select a suggestion, you can also save the setting mapping for future use.

# [Settings](#tab/settings)

The **Settings** tab shows the agent's settings, like the required permissions, the identity running the agent, and more requirements. In this tab, you can update the identity running the agent.

---

## Add, save, and view a knowledge source

**Knowledge sources** are files that you upload. These files describe the device configuration requirements in natural language. They can be internal policy documents and baselines, like security and compliance policies and frameworks, industry standards that describe settings, or risk assessment guidelines for device configurations.

For example, you can upload compliance standards and common industry benchmarks, like:

- Security Technical Implementation Guides (STIGs)
- National Institute of Standards and Technology (NIST) guidelines

You can save the agent suggestions so you can create device configuration policies when you're ready.

To add a knowledge source, use the following steps:

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Policy Configuration Agent**.
2. Select **Create new** > **Knowledge source**.
3. Configure the following settings:

    - **Knowledge source name** - Enter a name for the knowledge source.
    - **Description** - Optional. Enter a description for the knowledge source.
    - **Upload document** - Browse for your file or drag-and-drop the file. The agent supports well-known baseline formats, custom documents, and bulleted lists of requirements.

4. Select **Review**. The agent runs immediately and analyzes the knowledge source you uploaded. Select the link to open it.

    :::image type="content" source="./media/policy-configuration-agent-suggestion.png" alt-text="Diagram that shows a sample policy draft created with the Copilot Policy Configuration Agent in Microsoft Intune." lightbox="./media/policy-configuration-agent-suggestion.png":::

    You see suggested settings mapped to the knowledge source you uploaded.

5. In the **Policy details** > **Identified settings** tab, your data is mapped to Intune settings. For each setting, the agent shows:

    - The name of the Intune policy setting
    - The proposed value of the setting
    - The original requirement text it maps to
    - The confidence score for the mapping

    The agent classifies each mapping rule into the following categories:

    - **Supported** – There's a direct Intune setting available. The agent maps the rule to that setting and proposes a configuration.
    - **Unsupported** – There isn't a built-in Intune setting for this requirement. The agent notes that the rule is unsupported, meaning Intune alone can't enforce it. For example, a rule about a very niche OS setting that Intune can't manage would be flagged.

      If any settings are unsupported, then they're listed.

    **We recommend you review and confirm every mapping, especially the low-confidence mappings**.

6. You can also **Save this mapping** to save the suggested mappings and use them in other policies later.

    After you save the mapping, you can choose to create a device configuration profile.

7. After you review the suggestions, select **Manage suggestion**. Use this option to update the suggestion status.

    These statuses are for your tracking purposes only. They help you track the suggestions you reviewed and the suggestions you need to address. The **Dismissed** status removes the suggestion from the **Suggestions** tab.

### View your existing knowledge sources

When you upload a knowledge source, it's available in the **Knowledge** tab. To view your existing knowledge sources, use the following steps:

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Policy Configuration Agent**.
2. In the **Knowledge** tab, there's a list of your existing knowledge sources. Select a knowledge source to view its settings and their configured values.
3. You can **Delete** a knowledge source and **Export** its settings.

## Create and view a policy draft

The agent can create a settings catalog device configuration policy based on a knowledge source you uploaded or using a natural language prompt.

To create a policy using the agent, use the following steps:

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Policy Configuration Agent**.
2. Select **Create new** > **Policy draft**.
3. Configure the following settings:

    - **Policy name** - Enter a name for the policy draft.
    - **Description** - Optional. Enter a description for the policy.
    - **Knowledge source** - Select the knowledge source you want to use for this policy draft.

      If it's blank, then no knowledge sources are uploaded. Select **add a document** to upload a file that contains your instructions.
    - **Instructions** - In natural language, describe the device configuration settings you want to include in the policy. For example, enter `Create a device configuration policy that enforces strong password requirements and enables BitLocker encryption on Windows devices`.

4. Select **Create**. The agent runs and creates a policy draft based on your selected source.

5. In the **Overview** and **Suggestions** tabs, your policy draft is shown as a suggested next step. Select the draft link.

    An AI Summary describes the policy draft and provides more helpful insights. The policy details show the settings suggested by the agent and its configured values. You can also export the settings as a `.csv` file.

    **In this step, review each setting and its value to ensure they meet your requirements**. You can start with the settings that have a low confidence score.

6. After you review the suggestions, select **Manage suggestion**. Use this option to update the suggestion status.

    These statuses are for your tracking purposes only. They help you track the suggestions you reviewed and the suggestions you need to address. The **Dismissed** status removes the suggestion from the **Suggestions** tab.

7. Select **Create configuration policy** to save the policy draft as a device configuration policy. This step takes you to the settings catalog, and is prepopulated with the agent-generated configuration. The saved policy is shown in **Devices** > **Manage devices** > **Configuration**.

    The agent also automatically adds any required settings to the policy, including parent and child settings. So, the settings count can be different between the agents policy draft and the device configuration policy.

    At this stage, the policy is a normal Intune policy. You can change the policy name, update the policy settings, and assign the policy when you're ready.

    **In this step, review each setting and its value to ensure they meet your requirements**.

### View your existing policy drafts

You can view your existing policy drafts. Use the following steps:

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Policy Configuration Agent**.
1. In the **Overview** and **Suggestions** tabs, your policy drafts are shown as suggested next steps. Select a policy draft to view its settings and their configured values.

To update any settings and their values in the policy draft, you must create a device configuration policy from the draft. After you create the policy, you can edit it like any other Intune device configuration policy.

## Related content

- [Policy Configuration Agent in Intune - Overview and set up](policy-configuration-agent.md)
- [Security Copilot agents in Intune - An overview](index.md)
- [Security Copilot in Intune - An overview](../intune-service/copilot/copilot-intune-overview.md)
