---

title: Microsoft Security Copilot agents in Microsoft Intune
description: Learn about Security Copilot agents in Microsoft Intune Microsoft Intune
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/27/2025
ms.topic: overview
ms.service: security-copilot
ms.localizationpriority: high
ms.collection:
- security-copilot
- magic-ai-copilot
- tier1
- essentials
- get-started

search.appverid: MET150
keywords: NOCSH
audience: ITPro

---

# Microsoft Security Copilot agents in Microsoft Intune

Microsoft Security Copilot agents are available in Microsoft Intune.
<!-- There are various agents you can use in Intune to help you .... -->

## Agent terminology

| Field | Description |
| ----- | ----------- |
| Trigger | An event or condition that tells an agentic system to initiate an action or series of actions. |
| Permissions | The level of authorization an AI agent is given by an admin during configuration that enables it to access specific information or carry out its tasks. |
| Identity | The credentials that the agent will use when it runs. |
| Plugins | A component that extends what an agent can do by giving it access to capabilities in first- and third-party services and public websites through APIs. |
 
## Available agents

- [Vulnerability Remediation Agent in Microsoft Intune](../protect/vulnerability-remediation-agent.md)

## Vulnerability Remediation Agent in Microsoft Intune

<!-- *Placeholder: Description of agent with use-case in focus. Ideally, this section will focus on what the user will get out of the agent. For example, for the Threat Intelligence briefing agent, customers will get an analysis of all the latest threat intelligence tailored to their industry, company, and geolocation, and recommendations on how to mitigate it* -->

The Vulnerability Remediation Agent in Intune uses data from [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management) to identify the individual Common Vulnerabilities and Exposures (CVEs) on your managed devices and provides prioritized remediation guidance for those threats. For each identified CVE threat, the agent includes the following information:

- Severity
- Exploitability
- Affected systems
- Organizational exposure

Use of this Copilot Agent by your security team can reduce the time it takes to investigate, identify, and remediate threats from hours to only a few minutes.

### Trigger

*Placeholder: An event or condition that tells an agentic system to initiate an action or series of actions.*

### Permissions

*Placeholder: The level of authorization an AI agent is given by an admin during configuration that enables it to access specific information or carry out its tasks.*

### Identity
*Placeholder: Identity that the agent will use to run. Definition still in discussion.*

### Products
*Placeholder: If there are other products needed for the agent to run.*

### Plugins
*Placeholder: A component that extends what an agent can do by giving it access to capabilities in first- and third-party services and public websites through APIs.*

### Role-based access 
*Placeholder: Who can see the agent's results and manage it.*

