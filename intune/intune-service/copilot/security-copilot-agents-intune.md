---
title: Microsoft Security Copilot agents in Microsoft Intune
description: Learn about Security Copilot agents in Microsoft Intune
ms.date: 09/26/2025
ms.update-cycle: 180-days
ms.topic: overview
ms.reviewer: idaewor
ms.collection:
- security-copilot
- msec-ai-copilot
- essentials
- get-started

---

# Microsoft Security Copilot agents in Microsoft Intune

Microsoft Security Copilot agents are available in Microsoft Intune.

## Available agents

### Vulnerability Remediation Agent in Microsoft Intune

The [Vulnerability Remediation Agent in Intune](../protect/vulnerability-remediation-agent.md) uses data from [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management) to identify the individual Common Vulnerabilities and Exposures (CVEs) and Windows vulnerabilities on your managed devices. The results are prioritized for remediation and include step-by-step instructions to guide you in using Intune to remediate the threat. Use of this Copilot Agent by your security team can help you reduce the time it takes to investigate, identify, and remediate threats from hours to only a few minutes.

Use of this Copilot Agent by your security team can reduce the time it takes to investigate, identify, and remediate threats from hours to only a few minutes.

| Attribute | Description |
|---|---|
| Identity | Runs as the user who first set up the agent and requires reauthentication after 90 days |
| Licenses | [Microsoft Intune Plan 1](https://www.microsoft.com/security/business/microsoft-intune-pricing?msockid=2da59cedebdd644e10a289a7ea67657a)<br>[Microsoft Defender for Endpoint P2]() or [Defender Vulnerability Management Standalone](/defender-vulnerability-management/defender-vulnerability-management-capabilities) |
| Permissions | Run hunting queries<br>Read vulnerability data from Defender<br>Read managed apps in Intune<br>Read device configurations in Intune |
| Products | [Security Copilot](/copilot/security/get-started-security-copilot)<br>[Microsoft Intune]()<br> [Microsoft Defender Vulnerability Management](../protect/microsoft-defender-with-intune.md) |
| Plugins | [Intune](security-copilot.md)<br>[Microsoft Defender](/defender-xdr/security-copilot-in-microsoft-365-defender)|
| Role-based access | **Microsoft Intune**: [Intune Read Only Operator](../fundamentals/role-based-access-control.md#built-in-roles)<br>**Microsoft Defender XDR**:<br>- With Unified RBAC: [Microsoft Entra ID Security Reader](/entra/identity/role-based-access-control/permissions-reference#security-reader)<br>- With granular RBAC: A [custom role](../fundamentals/create-custom-role.md) with permissions equivalent to the Unified RBAC Security Reader |
| Trigger | Runs manually, on demand |
