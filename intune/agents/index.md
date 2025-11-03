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

Security Copilot agents in Intune are AI-powered assistants designed to streamline and strengthen enterprise security operations. These agents automate critical tasks across endpoint protection, identity management, and threat intelligence, helping IT teams respond swiftly to vulnerabilities, policy gaps, and emerging threats. Each agent is tailored to a specific use case. For example, the Vulnerability Remediation Agent identifies and prioritizes fixes for CVEs affecting Intune-managed devices, while the Conditional Access Optimization Agent proactively scans for coverage gaps in Microsoft Entra ID (Entra ID) policies. By integrating deeply with Microsoft tools like Microsoft Defender (Defender) and Entra ID, these agents deliver actionable insights and remediation steps directly within the Intune admin experience.

Built on Microsoft Security Copilot's generative AI and automation capabilities, the agents observe, reason, and act with administrator oversight. They operate within a dedicated "agents" blade in Intune, using role-based access controls to ensure secure execution. Admins can configure agents to advise only or to perform safe changes automatically, with all actions logged for transparency. With prerequisites like Security Copilot licensing and appropriate product subscriptions, these agents can run on-demand or on a schedule, significantly reducing the time and effort required for routine security tasks. Ultimately, Security Copilot agents empower IT professionals to maintain robust security postures with greater speed, consistency, and control.

## Available agents

Intune provides the following agents:

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

The *Device Offboarding Agent* finds devices that you removed from Intune but might linger in Microsoft Entra. It provides steps to properly remove them from Microsoft Entra.

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

- You must have available [security compute units (SCU)](/copilot/security/manage-usage)
- Review [Privacy and data security in Microsoft Security Copilot](/copilot/security/privacy-data-security)

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