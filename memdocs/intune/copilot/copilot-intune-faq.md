---
# required metadata

title: Copilot in Intune FAQ
description: Get answers to common questions when using Copilot in Microsoft Intune.
keywords: security copilot, intune, microsoft intune, copilot, faq
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/08/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice:
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: rashok
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- magic-ai-copilot
---

# Microsoft Copilot in Intune FAQ

This article answers common questions about using Microsoft Copilot in Intune. For more information, see [Microsoft Copilot in Intune overview](copilot-intune-overview.md).

## Access to Copilot

### How can I control access to Copilot in Intune?

When you set up Security Copilot, you determine the Copilot role that your admins can have (owner or contributor), as described in [Roles and authentication in Microsoft Security Copilot](/security-copilot/authentication). There are also Microsoft Entra roles that can control access to Security Copilot.

The Security Copilot roles or the Microsoft Entra roles that you configure control access to Copilot in Intune. There aren't any Intune-specific roles-based access controls (RBAC) for Copilot in Intune.

After you enable Intune in Security Copilot,  your Intune admins can see the Copilot features in the Intune admin center. But they can only access the data that they have permission to. Copilot honors existing [Intune RBAC roles](../fundamentals/role-based-access-control.md) and [Intune scope tags](../fundamentals/scope-tags.md) that are assigned to your admins.

So, if an admin tries to access Intune data that they don't have permissions to, they get the following error message:

`You don't have permission to access this feature. Reach out to your IT administrator for help.`

If you want access to Copilot in Intune, contact the Security Copilot workspace owner in your organization. If you want access to all your Intune data, contact your Intune administrator.

### Can I use Security Copilot if I'm not an Intune admin, and vice versa?

Yes. Access to Security Copilot is managed by using Security Copilot or Microsoft Entra roles. For more information, see [Roles and authentication in Microsoft Security Copilot](/security-copilot/authentication).

If you're an Intune admin and have the correct Security Copilot or Microsoft Entra role assigned to you, you can use Security Copilot to get insights about your Intune data.

Security Copilot is scoped to all your embedded services.

If you're an Intune admin or IT admin and only want Intune data, you should use [Copilot in Intune](copilot-intune-overview.md). Its scope is only Intune data, and its capabilities are integrated into the relevant areas of the Intune admin center. 

If you're a security admin, you can use [Copilot in Intune](copilot-intune-overview.md) if you only want insights into your Intune data.

## Capabilities and cost

### How do I turn on Intune capabilities?

In the [Microsoft Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989), select **Sources** (prompt bar > right corner), and enable the Microsoft Intune plug-in. This plug-in allows you to access your Intune data and use the Copilot features in the Intune admin center.

For more information about managing plug-ins, see [Manage plug-ins in Security Copilot](/security-copilot/manage-plugins).

### Can I use capabilities for other Copilot services in the Intune admin center?

No. Copilot in Intune in the Intune admin center is available only for Intune capabilities.

You can't get insights from other Microsoft services, like Microsoft Defender, Microsoft Entra, and Microsoft Purview. To get insights from other Microsoft services, you can use the [Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989).

### How much does Copilot in Intune cost?

Copilot in Intune is included with Security Copilot. Security Copilot uses security compute units (SCUs). There aren't any other licensing requirements or Intune-specific licenses for using Copilot in Intune.

For more information about SCUs, see:

- [Get started with Microsoft Copilot](/security-copilot/get-started-security-copilot)
- [Manage capacity in Security Copilot](/security-copilot/manage-usage)

### Is there a limit on the prompt output?

Copilot in Intune is bound by any token limits in Security Copilot. For more information, see [Security Copilot FAQ - Token limits](/security-copilot/faq-security-copilot#how-is-copilot-for-security-dealing-with-a-token-limit).

## Security Copilot vs. Copilot in Intune

### Does Security Copilot give admins more access to Intune data than is available in the Intune admin center?

No. The Intune capabilities in Security Copilot are built using the existing Microsoft Graph APIs, which are the same APIs that the Intune admin center uses. Both Copilot experiences use the same Intune capabilities.

### To get Intune insights, should I use Security Copilot or Copilot in Intune?

To use Copilot with your Intune data, you can use Copilot in Intune or Security Copilot. Here's a comparison of the two experiences:

| Feature | Copilot in Intune | Security Copilot |
|---|---|---|
| **Access and data insights** |  This Copilot is embedded in the Intune admin center and is scoped to only show Intune data.<br/><br/> Intune admins should use Copilot in Intune for Intune-only tasks. | This Copilot is a standalone experience. It can access other embedded services, like Microsoft Defender, Microsoft Entra ID, Microsoft Purview, and Microsoft Intune. <br/><br/>It accesses the same Intune capabilities as Copilot in Intune. |
| **Open prompting** |  Intune provides a set of prompts you can use. There isn't an open prompt. There are plans to include an open prompt in the future (no ETA).| Can use open prompts or use [promptbooks](/security-copilot/using-promptbooks). |
| **Prompt history** |  The prompt/response history isn't available in the Intune admin center. To view the prompt history, use Security Copilot.<br/><br/>The prompts can look different compared with the prompts shown in Intune, as Intune enters the prompt for you. | You can review the prompt/response history even when the prompt is submitted in the standalone or embedded experience. |
| **Target audience** | Focus is the IT admin/IT Pro. | Focus is the Security Operations Center (SOC) and can be used by IT admins. |

## Feedback and troubleshooting Copilot

### Copilot appears to show the wrong info. How can I debug and validate?

If you think that the output is incorrect, submit feedback and include details about what you're seeing. This feedback helps improve the Copilot experience.

In the Copilot prompt window in the Intune admin center, there's a **Feedback** button.

:::image type="content" source="./media/copilot-intune-overview/feedback-message-icon.png" alt-text="Screenshot that shows how to provide Copilot feedback in Microsoft Intune and Intune admin center.":::

Other things you can try:

- In Microsoft Edge, you can use the F12 developer tools to debug the issue. In the developer debug tool, select the **Network** view. In Copilot, select the prompt to get the output. In the developer debug tool, use the **logs** entries to look more closely at the steps between the prompt input and output.

- If you're working with Microsoft to debug the issue, support might ask you for the session ID. To get the session ID, you can:

  - Use the F12 developer tools in your browser. This information shows the capabilities that Copilot uses.
  - In the [Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989), you can view the prompt sessions and session IDs from the Intune embedded experience.

## Related articles

- [Microsoft Security Copilot FAQ](/security-copilot/faq-security-copilot)
- [Microsoft Copilot in Intune](copilot-intune-overview.md)