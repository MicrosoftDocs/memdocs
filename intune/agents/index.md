---
title: Security Copilot Agents
description: Discover how Microsoft Security Copilot enhances Microsoft Intune through AI-powered security agents. Learn about available agents and explore their capabilities.
ms.date: 10/15/2025
ms.topic: overview
author: paolomatarazzo
ms.author: paoloma
ms.reviewer: 
---

# Security Copilot agents in Microsoft Intune

<!-- placeholder intro to update-->

Security Copilot agents in Intune are AI-powered assistants designed to streamline and strengthen enterprise security operations. These agents automate critical tasks across endpoint protection, identity management, and threat intelligence, helping IT teams respond swiftly to vulnerabilities, policy gaps, and emerging threats. Each agent is tailored to a specific use case—for example, the Vulnerability Remediation Agent identifies and prioritizes fixes for CVEs affecting Intune-managed devices, while the Conditional Access Optimization Agent proactively scans for coverage gaps in Entra ID policies. By integrating deeply with Microsoft tools like Defender and Entra ID, these agents deliver actionable insights and remediation steps directly within the Intune admin experience.

Built on Microsoft Security Copilot's generative AI and automation capabilities, the agents observe, reason, and act with administrator oversight. They operate within a dedicated "agents" blade in Intune, using role-based access controls to ensure secure execution. Admins can configure agents to advise only or to perform safe changes automatically, with all actions logged for transparency. With prerequisites like Security Copilot licensing and appropriate product subscriptions, these agents can run on-demand or on a schedule, significantly reducing the time and effort required for routine security tasks. Ultimately, Security Copilot agents empower IT professionals to maintain robust security postures with greater speed, consistency, and control.

:::image type="content" source="images/security-copilot-agents.png" alt-text="Screenshot of the security copilot blade in the Intune admin center." lightbox="images/security-copilot-agents.png" border="false":::

## Available agents

The following agents are available in Intune:

:::row:::
:::column:::
#### Approver agent

:::image type="icon" source="icons/approver-agent.svg" border="false":::

The *approver agent* evaluates the effect of approval requests in Intune and makes recommendations for the actions you can take. 

> [!div class="nextstepaction"]
> [Learn more](approver-agent.md)
:::column-end:::
:::column:::
#### Device Offboarding Agent

:::image type="icon" source="icons/device-offboarding-agent.svg" border="false":::

The *Device Offboarding Agent* can find devices that were removed from Intune, but might linger in Microsoft Entra. It provides steps to properly remove them from Entra.

> [!div class="nextstepaction"]
> [Learn more](device-offboarding-agent.md)
:::column-end:::
:::row-end:::

:::row:::
:::column:::
#### Policy agent

:::image type="icon" source="icons/policy-agent.svg" border="false":::

The *policy agent* translates complex regulatory standards into actionable Intune settings. 

> [!div class="nextstepaction"]
> [Learn more](policy-agent.md)
:::column-end:::
:::column:::
#### Vulnerability remediation agent

:::image type="icon" source="icons/vulnerability-remediation-agent.svg" border="false":::

The *vulnerability remediation agent* uses Microsoft Defender data to monitor vulnerabilities and prioritize remediation with AI-driven risk assessments. 

> [!div class="nextstepaction"]
> [Learn more](vulnerability-remediation-agent.md)
:::column-end:::
:::row-end:::
