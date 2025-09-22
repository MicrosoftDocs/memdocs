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

The Vulnerability Remediation Agent runs using the identity and permissions of an administrative user. By default, this is the user who installs the agent. However, after the agent is set up, this identity can be changed to a different account.

#### Identity

The agent persistently runs in the identity of a user account. By default, this is the Intune administrative user who initially set up the agent.

The agent also supports a manual change of the account used as its identity. To successfully assign a new agent identity requires sign-in and authentication of the new user account.

The agent identity refreshes with each agent run and expires if the agent doesn't run for 90 consecutive days. When the expiration date nears, each Copilot owner and Copilot contributor receives a warning banner about renewal of the agent identity when they view the agent overview page. If the agent authentication expires, subsequent agent runs fail until authentication is renewed. For more information about renewing authentication, see Renew the agent later in this article

When the agent authentication is renewed, the agent begins using the credentials of the individual who clicks on the *Renew authentication* button.

#### Products

The agent requires the following products:

- [Microsoft Intune Plan 1 subscription](https://www.microsoft.com/security/business/microsoft-intune-pricing?msockid=2da59cedebdd644e10a289a7ea67657a) *This subscription provides the core Intune capabilities*.
- [Microsoft Security Copilot](/copilot/security/microsoft-security-copilot) - *Security Copilot must share a Tenant with Intune, and you must have sufficient SCUs to power Security Copilot workloads, including agents.*
- [Microsoft Defender Vulnerability Management](../protect/advanced-threat-protection.md) *This capability is provided by Microsoft Defender for Endpoint P2 or Defender Vulnerability Management Standalone.*

#### Plugins

- Microsoft Intune
- [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management)

#### Role-based access
**Intune Requirements:**  
To set up the agent or view agent results, admins must be assigned an Intune license and be assigned either a built-in or custom Intune role-based access control (RBAC) role that grants the following permissions:

- Managed apps / read
- Mobile apps / read
- Device configurations / read

The least privileged built-in role that includes these permissions is [Read Only Operator](../fundamentals/role-based-access-control-reference.md#read-only-operator).

**Microsoft Defender Requirements:**  
The account used by the agent for its identity must be assigned permissions that align with the following Microsoft Defender XDR RBAC configurations. The specific configuration depends on whether your Defender XDR implementation uses [Unified RBAC](/defender-xdr/manage-rbac) or a [granular RBAC](/defender-endpoint/rbac) configuration:

- **Unified RBAC:** Assign the Microsoft Entra ID *Security Reader* to the agent's identity account. This role provides read-only access to Defender Vulnerability Management data and automatically enforces device group scoping.
  
  For details about mapping permissions to the Unified RBAC Security Reader role, see [Microsoft Entra Global roles access](/defender-xdr/compare-rbac-roles#microsoft-entra-global-roles-access) in the *Map Microsoft Defender XDR Unified role-based access control (RBAC)* article in the Defender documentation.

- **Granular RBAC:** Assign a custom RBAC role with permissions equivalent to the Unified RBAC *Security Reader* role. For example, the permission **View data – Defender Vulnerability Management** is required, as it maps to the Unified RBAC permission of **Security posture / Posture management / Vulnerability management (read)**.

Ensure the agent’s identity is scoped to include all relevant device groups. The agent can't access or report on devices outside its assigned scope.

**Security Copilot Roles:**  
- To set up or remove an agent, the admin must be a [Copilot **owner**](/copilot/security/authentication).
- To work with the installed agent, the admin must be a [Copilot **contributor**](/copilot/security/authentication).

<!--  
For an Intune administrator (admin) to successfully manage or use the Vulnerability Remediation Agent, they must be assigned the role-based access controls (RBAC) for Intune, Microsoft Defender, and Security Copilot as described in the following sections.

When assigning RBAC roles and permissions to admins to manage and use the agent, assign the least privileged built-in RBAC role or a custom role that includes the minimum permissions ￼required to complete their administrative tasks.

| Action | Microsoft Intune | Microsoft Defender | Security Copilot |
|--------|------------------|--------------------|------------------|
| **Set Up and Removal**        | Admin must be assigned an Intune license. Permissions (built-in or custom role) must include: <br><br> - Managed apps/read <br> - Mobile apps/read <br> - Device configurations/read <br><br>Least privileged Intune built-in role: [Read Only Operator](../fundamentals/role-based-access-control-reference.md#read-only-operator). | The admin must have permissions equal to the Microsoft Entra [Security reader](/defender-endpoint/prepare-deployment#role-based-access-control) role. | The admin must be a [Copilot owner](/copilot/security/authentication). |
| **Work with Installed Agent** | Admin must be assigned an Intune license. Permissions (built-in or custom role) must include: <br><br> - Managed apps/read <br> - Mobile apps/read <br> - Device configurations/read <br><br>Least privileged Intune built-in role: [Read Only Operator](../fundamentals/role-based-access-control-reference.md#read-only-operator). | The admin must have permissions equal to the Microsoft Entra [Security reader](/defender-endpoint/prepare-deployment#role-based-access-control) role. | The admin must be a [Copilot contributor](/copilot/security/authentication). |     --> 

> [!IMPORTANT]  
> Data that the agent reports is made visible through agent suggestions. This data might be visible to admins with access to view the agent within the Intune admin center, even when that data is outside the admins assigned Intune roles or scope.
