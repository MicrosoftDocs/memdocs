---
title: Use the Policy Configuration Agent to create policies
description: Learn how to use the Policy Configuration Agent in Microsoft Intune.
ms.date: 11/06/2025
ms.topic: how-to
author: mandiohlinger
ms.author: mandia
ms.reviewer: aanavath
---

# Use the Policy Configuration Agent

> [!WARNING]
> This article is still being written. Do not use it or share any information from it.

The [Policy Configuration Agent](policy-configuration-agent.md) is a generative AI feature in Intune. It helps you automate the creation of Intune policies based on your organization's requirements or industry benchmarks.

After you [set up the agent](policy-configuration-agent.md), the next step is to upload documents and benchmarks as **knowledge sources**. The agent analyzes these knowledge sources to suggest relevant Intune settings and then can create device configuration policies using these settings.

This article shows you how to use the Policy Configuration Agent, including:

- Adding, saving, and viewing a knowledge source
- Creating a policy from a knowledge source

To learn about the agent and how to set it up, see [Use the Policy Configuration Agent](policy-configuration-agent.md).

This feature applies to:

- Windows

## Before you begin

- Make sure you meet the prerequisites to use the [Policy Configuration Agent](policy-configuration-agent.md#prerequisites), including signing in with an account that has the [Copilot Contributor Security Copilot role](/copilot/security/authentication#security-copilot-roles) and [Policy and Profile manager Intune role](../intune-service/fundamentals/role-based-access-control-reference.md#policy-and-profile-manager).
- You can upload one knowledge source file at a time. If you have multiple baseline documents, run them separately through the agent.
- Well-structured, well-written policies result in better mappings. If a document is poorly formatted or uses unclear language, the agent can produce low-confidence matches. We recommend you review your source documents for clarity.
- You can add text or JSON files up to 100 KB in size. Large or complex documents with hundreds of pages of requirements might challenge the agent's ability to process them effectively.

## Add, save, and view a knowledge source

Knowledge sources are text or JSON files that you upload. These files describe the device configuration requirements in natural language. They can be internal policy documents and baselines, like security and compliance policies and frameworks, industry standards that describe settings, or risk assessment guidelines for device configurations.

For example, you can upload compliance standards and common industry benchmarks, like Security Technical Implementation Guides (STIGs), National Institute of Standards and Technology (NIST) guidelines, Defense Information Systems Agency (DISA) STIGs, and Center for Internet Security (CIS) benchmarks.

To add a knowledge source, use the following steps:

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Policy Configuration Agent**.
2. Select **Create new** > **Knowledge source**.
3. Configure the following settings:

    - **Reference name**: Enter a name for the knowledge source.
    - **Description**: Optional. Enter a description for the knowledge source.
    - **Upload reference file**: Browse for your file or drag-and-drop the file. You can add text or JSON files up to 100 KB in size.

4. Select **Create**. The agent runs immediately and analyzes the knowledge source you uploaded.

    When the agent finishes, it shows the suggestions for the next step, which is for you to review a policy draft with suggested settings based on the knowledge source you uploaded. Select the policy draft to open it.

    ??INSERT SCREEN SHOT??

5. In the **Identified settings** tab, each setting mapping and its recommended configured value is shown. You can select a setting to get more details.

6. You can also **Save this mapping** to save the suggested policy with its configured settings. The saved policy is shown in **Devices** > **Manage devices** > **Configuration**.

    When you save, the policy is created but it's not assigned. You can always change the policy and you can assign it later.

At this point, the policy is a normal Intune policy. You can change it and assign it to your users and groups.

### View your existing knowledge sources

You can view your existing knowledge sources in the Intune admin center. Use the following steps:

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Policy Configuration Agent**.
2. In the **Knowledge** tab, you can see a list of your existing knowledge sources. Select a knowledge source to view its settings and their configured values.
3. You can **Delete** a knowledge source and **Export** its settings.

## Create a policy

The agent can create a device configuration policy based on a knowledge source you uploaded, using a natural language prompt, or using an industry baseline.

To create a policy using the agent, use the following steps:

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Policy Configuration Agent**.
2. Select **Create new** > **Policy draft**.
3. Configure the following settings:

    - **Name**: Enter a name for the policy draft.
    - **Description**: Optional. Enter a description for the policy.
    - **Source**: Select the knowledge source you want to use for this policy draft. Your options:

      - **Natural language prompt**: Enter a prompt that describes the device configuration settings you want to include in the policy. For example, enter `Create a device configuration policy that enforces strong password requirements and enables BitLocker encryption on Windows devices`.

      - **Knowledge source**: Select a knowledge source that you previously uploaded. For example, you might choose your organization's security policy document that outlines specific device configuration requirements.

      - **Industry baseline**: Select an industry baseline that you want to use for this policy draft. For example, you might choose a baseline for Windows devices that enforces specific security settings. ??

4. Select **Generate**. The agent runs and creates a policy draft based on your selected source.

    If you selected **Natural language prompt**, you can update the prompt to make changes, like exempting certain users or settings. Then, you can regenerate the policy draft by selecting **Generate again**.

5. Select **Create** to save the policy draft. The saved policy is shown in **Devices** > **Manage devices** > **Configuration**.

    When you save, the policy is created but it's not assigned. You can always change the policy and you can assign it later.

### View your existing policy drafts

You can view your existing policy drafts in the Intune admin center. Use the following steps:

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Agents** > **Policy Configuration Agent**.

??Figma is unclear on this part and seems to show new buttons??

## Related content

- [Policy Configuration Agent in Intune](policy-configuration-agent.md)
- [Security Copilot agents in Intune - An overview](index.md)
- [Security Copilot in Intune - An overview](../intune-service/copilot/copilot-intune-overview.md)