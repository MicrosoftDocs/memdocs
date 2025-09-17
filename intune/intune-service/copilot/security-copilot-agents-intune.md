---

title: Microsoft Security Copilot agents in Microsoft Intune
description: Learn about Security Copilot agents in Microsoft Intune
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/17/2025
ms.update-cycle: 180-days
ms.topic: overview
ms.service: security-copilot
ms.localizationpriority: high
ms.reviewer: idaewor
ms.collection:
- security-copilot
- msec-ai-copilot
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

The Vulnerability Remediation Agent runs manually on demand, and also supports a scheduled run every one to seven days.

#### Permissions

The Vulnerability Remediation Agent runs using the identity and permissions of the an administrative user. By default, this is the user who installs the agent. However, after the agent is set up, this identity can be changed to a different account.

#### Identity

The agent persistently runs in the identity of a user account. By default, this is the Intune administrative user who initially set up the agent.

This identity refreshes with each agent run and expires if the agent has not been run for 90 consecutive days. When the expiration date nears, each *Copilot owner* and *Copilot contributor* receives a warning banner about renewal of the agent identity when they view the agent overview page. If the agent authentication expires, subsequent agent runs fail until re-authentication. Renewal of the agent authentication can be performed by both owners and contributors before the expiration as well as after expiration.

When the agent authentication is renewed, the agent begins using the credentials of the individual who clicks on the *Renew authentication* button.

The agent also supports a manual change of the account used as its identity. To successfully assign a new agent identity requires sign-in and authentication of the new user account.



#### Products

The agent requires the following products:

- [Microsoft Intune Plan 1 subscription](https://www.microsoft.com/security/business/microsoft-intune-pricing?msockid=2da59cedebdd644e10a289a7ea67657a) *This subscription provides the core Intune capabilities*.
- [Microsoft Security Copilot](/copilot/security/microsoft-security-copilot) - *Security Copilot must share a Tenant with Intune, and you must have sufficient SCUs to power Security Copilot workloads, including agents.*
- [Microsoft Defender Vulnerability Management](../protect/advanced-threat-protection.md) *This capability is provided by Microsoft Defender for Endpoint P2 or Defender Vulnerability Management Standalone.*

#### Plugins

- Microsoft Intune
- [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management)

#### Role-based access

For an Intune administrator (admin) to successfully manage or use the Vulnerability Remediation Agent, they must be assigned the role-based access controls (RBAC) for Intune, Microsoft Defender, and Security Copilot as described in the following sections.

When assigning RBAC roles and permissions to admins to manage and use the agent, assign the least privileged built-in RBAC role or a custom role that includes the minimum permissions ￼required to complete their administrative tasks.

| Action | Microsoft Intune | Microsoft Defender | Security Copilot |
|--------|------------------|--------------------|------------------|
| **Set Up and Removal**        | Admin must be assigned an Intune license. Permissions (built-in or custom role) must include: <br><br> - Managed apps/read <br> - Mobile apps/read <br> - Device configurations/read <br><br>Least privileged Intune built-in role: [Read Only Operator](../fundamentals/role-based-access-control-reference.md#read-only-operator). | The admin must have permissions equal to the Microsoft Entra [Security reader](/defender-endpoint/prepare-deployment#role-based-access-control) role. | The admin must be a [Copilot owner](/copilot/security/authentication). |
| **Work with Installed Agent** | Admin must be assigned an Intune license. Permissions (built-in or custom role) must include: <br><br> - Managed apps/read <br> - Mobile apps/read <br> - Device configurations/read <br><br>Least privileged Intune built-in role: [Read Only Operator](../fundamentals/role-based-access-control-reference.md#read-only-operator). | The admin must have permissions equal to the Microsoft Entra [Security reader](/defender-endpoint/prepare-deployment#role-based-access-control) role. | The admin must be a [Copilot contributor](/copilot/security/authentication). |

> [!IMPORTANT]  
> Data that is reported by the agent and visible through agent suggestions might be visible to admins with access to view the agent within the Intune admin center, even when that data is outside the admins assigned Intune roles or scope.
