---
title: Security Copilot Agents in Intune
description: Discover how Microsoft Security Copilot enhances Microsoft Intune through AI-powered security agents. Learn about available agents and explore their capabilities.
ms.date: 10/15/2025
ms.topic: overview
author: paolomatarazzo
ms.author: paoloma
ms.reviewer: 
---

# Security Copilot agents in Intune overview

Security Copilot agents in Intune are AI-powered assistants that enhance enterprise security by automating tasks across endpoint protection, identity management, and threat intelligence. They help IT teams quickly address vulnerabilities, policy gaps, and emerging threats.

Built on Microsoft Security Copilot's generative AI and automation capabilities, these agents observe, reason, and act under administrator oversight. Each agent is tailored to a specific use case and operates within a dedicated blade in the Intune admin center, using role-based access controls for secure execution.

## Available agents

Microsoft Intune includes specialized Security Copilot agents, each designed for a specific security scenario. 
The following agents are currently available:

:::row:::
:::column:::
#### Change Review Agent

:::image type="icon" source="icons/change-review-agent.svg" border="false":::

The *Change Review Agent* evaluates the effect of approval requests in Intune and makes recommendations for the actions you can take. 

> [!div class="nextstepaction"]
> [Learn more](change-review-agent.md)
:::column-end:::
:::column:::
#### Device Offboarding Agent

:::image type="icon" source="icons/device-offboarding-agent.svg" border="false":::

The *Device Offboarding Agent* identifies stale or misaligned devices across Intune, Entra ID, Defender, Autopilot, and Apple Business Manager, providing actionable insights and requiring admin approval before offboarding any devices.

> [!div class="nextstepaction"]
> [Learn more](device-offboarding-agent.md)
:::column-end:::
:::row-end:::

:::row:::
:::column:::
#### Policy Configuration Agent

:::image type="icon" source="icons/policy-configuration-agent.svg" border="false":::

With the *Policy Configuration Agent* you can import documents or write instructions in plain language. The agent uses your document as reference and matches those instructions to the Settings Catalog to help create a policy.

> [!div class="nextstepaction"]
> [Learn more](policy-configuration-agent.md)
:::column-end:::
:::column:::
#### Vulnerability Remediation Agent

:::image type="icon" source="icons/vulnerability-remediation-agent.svg" border="false":::

The *Vulnerability Remediation Agent* uses Defender data to monitor vulnerabilities and prioritize remediation with AI-driven risk assessments. 

> [!div class="nextstepaction"]
> [Learn more](vulnerability-remediation-agent.md)
:::column-end:::
:::row-end:::

## Getting started with agents

### Prerequisites

Before you begin, make sure you have:

- [Security compute units (SCU)](/copilot/security/manage-usage) available
- Reviewed the [Privacy and data security in Microsoft Security Copilot](/copilot/security/privacy-data-security) to understand how your data is handled.

### Setup process

1. Enable Security Copilot using the [Security Copilot setup guide](/copilot/security/get-started-security-copilot).
1. Sign in to the [Microsoft Intune admin center][INT-AC] using the least privileged role required for the agent you want to configure.
1. Browse to **Agents** and select **View details** for the agent you want to configure.

:::image type="content" source="images/security-copilot-agents.png" alt-text="Screenshot of the security copilot blade in the Intune admin center." lightbox="images/security-copilot-agents.png" border="false":::

## Agents in the Microsoft ecosystem

While this article focuses on Intune agents, similar agents are available across other Microsoft security products. For more information, see:

- [Microsoft Entra](/entra/security-copilot/entra-agents)
- [Microsoft Defender](/defender-xdr/security-copilot-agents-defender)
- [Microsoft Purview](/purview/copilot-in-purview-agents)

## Related content

- [Microsoft Security Copilot agents overview](/copilot/security/agents-overview)


<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431