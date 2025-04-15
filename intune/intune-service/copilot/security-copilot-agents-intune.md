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

<!-- 
## Agent terminology

| Field | Description |
|-------|-------------|
| Trigger | An event or condition that tells an agentic system to initiate an action or series of actions. |
| Permissions | The level of authorization an AI agent is given by an admin during configuration that enables it to access specific information or carry out its tasks. |
| Identity | The credentials that the agent will use when it runs. |
| Plugins | A component that extends what an agent can do by giving it access to capabilities in first- and third-party services and public websites through APIs. |
-->

## Available agents

### Vulnerability Remediation Agent in Microsoft Intune

The Vulnerability Remediation Agent in Intune uses data from [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management) to identify the individual Common Vulnerabilities and Exposures (CVEs) on your managed devices. The results are prioritized for remediation and include step-by-step instructions to guide you in using Intune to remediate the threat. Use of this Copilot Agent by your security team can help you reduce the time it takes to investigate, identify, and remediate threats from hours to only a few minutes.

Use of this Copilot Agent by your security team can reduce the time it takes to investigate, identify, and remediate threats from hours to only a few minutes.

#### Trigger

The Vulnerability Remediation Agent runs manually, on demand.

#### Permissions

*Placeholder: The level of authorization an AI agent is given by an admin during configuration that enables it to access specific information or carry out its tasks.*

#### Identity
*Placeholder: Identity that the agent will use to run. Definition still in discussion.*

#### Products

The agent requires the following products:

- [Microsoft Intune Plan 1 subscription](https://www.microsoft.com/en-us/security/business/microsoft-intune-pricing?msockid=2da59cedebdd644e10a289a7ea67657a) - *core Intune capabilities*.
- [Microsoft Intune Suite](https://www.microsoft.com/security/business/microsoft-intune-pricing?msockid=2da59cedebdd644e10a289a7ea67657a) - *Intune Plan 2 and standalone add-ons are not sufficient for this prerequisite.*
- [Microsoft Security Copilot](/copilot/security/microsoft-security-copilot) - *Security Copilot must share a Tenant with Intune.*
- [Microsoft Defender for Endpoint](../intune-service/protect/advanced-threat-protection) - *Defender for Endpoint must be integrated with Intune.*
- [Microsoft Defender Vulnerability Management](../intune-service/protect/advanced-threat-protection) *Available as part of Defender for Endpoint Plan 2, or as an add-on to Defender for Endpoint Plan 1.*


#### Plugins

- [Microsoft Defender for Endpoint](/defender-endpoint/microsoft-defender-endpoint)
- [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management)

#### Role-based access 
*Placeholder: Who can see the agent's results and manage it.*

