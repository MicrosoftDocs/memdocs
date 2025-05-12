---

title: Microsoft Security Copilot agents in Microsoft Intune
description: Learn about Security Copilot agents in Microsoft Intune
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/19/2025
ms.topic: overview
ms.service: security-copilot
ms.localizationpriority: high
ms.reviewer: idaewor
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

## Available agents

### Vulnerability Remediation Agent in Microsoft Intune

The [Vulnerability Remediation Agent in Intune](../protect/vulnerability-remediation-agent.md) uses data from [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management) to identify the individual Common Vulnerabilities and Exposures (CVEs) and Windows vulnerabilities on your managed devices. The results are prioritized for remediation and include step-by-step instructions to guide you in using Intune to remediate the threat. Use of this Copilot Agent by your security team can help you reduce the time it takes to investigate, identify, and remediate threats from hours to only a few minutes.

Use of this Copilot Agent by your security team can reduce the time it takes to investigate, identify, and remediate threats from hours to only a few minutes.

#### Trigger

The Vulnerability Remediation Agent runs manually, on demand.

#### Permissions

The Vulnerability Remediation Agent runs using the identity of the user who installed the agent in Intune. To change this identity, the agent must be uninstalled, and then reinstalled.

#### Identity

The agent persistently runs in the identity of the user who initially set up the agent.

#### Products

The agent requires the following products:

- [Microsoft Intune Plan 1 subscription](https://www.microsoft.com/en-us/security/business/microsoft-intune-pricing?msockid=2da59cedebdd644e10a289a7ea67657a) *This subscription provides the core Intune capabilities*.
- [Microsoft Intune Suite](https://www.microsoft.com/security/business/microsoft-intune-pricing?msockid=2da59cedebdd644e10a289a7ea67657a) - *Intune Suite standalone solution add-on licenses including Intune Endpoint Privilege Management, Enterprise Application Management, and Intune Plan 2 do not meet this prerequisite.*
- [Microsoft Security Copilot](/copilot/security/microsoft-security-copilot) - *Security Copilot must share a Tenant with Intune, and you must have sufficient SCUs to power Security Copilot workloads, including agents.*
- [Microsoft Defender Vulnerability Management](../protect/advanced-threat-protection.md) *This capability is provided by Microsoft Defender for Endpoint P2 or Defender Vulnerability Management Standalone.*

#### Plugins

- Microsoft Intune
- [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management)

#### Role-based access

To set up or remove the agent from the Intune admin center your account must be assigned an Intune license and have permissions equal to the following:

- **Microsoft Intune**: Users must be assigned a built-in rule or custom role that includes the following permissions:  
  - Managed apps/read
  - Mobile apps/read
  - Device configurations/read 
  
   The least privileged Intune built-in role that provides these permissions is [Read Only Operator](../fundamentals/role-based-access-control-reference.md#read-only-operator), or equivalent permissions.

- **Microsoft Defender**: The user must have permissions equal to the Endpoint Defender role [Security reader](/defender-endpoint/prepare-deployment#role-based-access-control).

- **Security Copilot**: The user must be a [Copilot owner](/copilot/security/authentication).

To work with the agent in the Intune admin center after the agent is installed, your account must be assigned an Intune license and have permissions equal to the following, including running the agent, viewing results, and managing agent suggestions:

- **Microsoft Intune**: Users must be assigned a built-in rule or custom role that includes the following permissions:  
  - Managed apps/read
  - Mobile apps/read
  - Device configurations/read 
    
  The least privileged Intune built-in role that provides these permissions is [Read Only Operator](../fundamentals/role-based-access-control-reference.md#read-only-operator), or equivalent permissions.

- **Microsoft Defender**: The user must have permissions equal to the Endpoint Defender role [Security reader](/defender-endpoint/prepare-deployment#role-based-access-control).

- **Security Copilot**: The user must be a [Copilot contributor](/copilot/security/authentication).

