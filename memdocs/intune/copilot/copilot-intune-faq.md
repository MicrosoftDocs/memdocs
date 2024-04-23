---
# required metadata

title: Copilot in Intune FAQ
description: Get answers to common questions when using Copilot in Microsoft Intune.
keywords: security copilot, intune, microsoft intune, copilot, faq
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/01/2024
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

This article answers common questions about using Microsoft Copilot in Intune. For more information about Microsoft Copilot in Intune, go to [Microsoft Copilot in Intune overview](copilot-intune-overview.md).

## Access to Copilot

### How can I control access to Copilot in Intune?

When you set up Copilot for Security, you determine the Copilot role that your admins can have (owner vs. contributor), as described in [Roles and authentication in Microsoft Copilot for Security](/security-copilot/authentication). There are also Microsoft Entra roles that can control access to Copilot for Security.

The Copilot for Security roles and/or the Microsoft Entra roles that you configure control access to Copilot in Intune. There aren't any Intune-specific roles-based access controls (RBAC) for Copilot in Intune.

Once you enable Intune in Copilot for Security, then your Intune admins can see the Copilot features in the Intune admin center. But, they can only access the data that they have permissions to. Copilot honors existing [Intune RBAC roles](../fundamentals/role-based-access-control.md) and [Intune scope tags](../fundamentals/scope-tags.md) assigned to your admins.

So, if an admin tries access Intune data that they don't have permissions to, then they'll see the following error message:

`You don't have permission to access this feature. Reach out to your IT administrator for help.`

If you want access to Copilot in Intune, then contact the Copilot for Security workspace owner in your organization. If you want access to all your Intune data, then contact your Intune administrator.

### Can I use Copilot for Security if I'm not an Intune admin, and vice versa?

Yes. Access to Copilot for Security is managed using Copilot for Security and/or Microsoft Entra roles. For more information on the different roles, and what they can do, go to [Roles and authentication in Microsoft Copilot for Security](/security-copilot/authentication).

If you're an Intune admin and have the correct Copilot for Security or Microsoft Entra role assigned to you, then you can use Copilot for Security to get insights about your Intune data.

Copilot for Security is scoped to all your embedded services.

If your an Intune admin or IT admin, and only want Intune data, then you should use [Copilot in Intune](copilot-intune-overview.md). Its scope is only Intune data and its capabilities are integrated in the relevant areas in the Intune admin center. 

If you're a security admin, then you can use [Copilot in Intune](copilot-intune-overview.md) if you only want insights into your Intune data.

## Capabilities and cost

### How do I turn on Intune capabilities?

In the [Microsoft Copilot for Security portal](https://go.microsoft.com/fwlink/?linkid=2247989), select **Sources** (prompt bar > right corner), and enable the Microsoft Intune plug-in. This plug-in allows you to access your Intune data and use the Copilot features in the Intune admin center.

For more information on managing plugins, go to [Manage plugins in Copilot for Security](/security-copilot/manage-plugins).

### Can I use capabilities for other Copilot services in the Intune admin center?

No. Copilot in Intune in the Intune admin center is available only for Intune capabilities.

You can't get insights from other Microsoft services, like Microsoft Defender, Microsoft Entra, and Microsoft Purview. To get insights from other Microsoft services, you can use the [Copilot for Security portal](https://go.microsoft.com/fwlink/?linkid=2247989).

### How much does Copilot in Intune cost?

Copilot in Intune is included with Copilot for Security. Copilot for Security uses security compute units (SCUs). There aren't any other licensing requirements or Intune-specific licenses for using Copilot in Intune.

For more information on SCUs, go to:

- [Get started with Microsoft Copilot](/security-copilot/get-started-security-copilot)
- [Manage capacity in Copilot for Security](/security-copilot/manage-usage)

### Is there a limit on the prompt output?

Copilot in Intune is bound by any token limits in Copilot for Security. For more information, go to [Copilot for Security FAQ - Token limits](/security-copilot/faq-security-copilot#how-is-copilot-for-security-dealing-with-a-token-limit).

## Copilot for Security vs Copilot in Intune

### Does Copilot for Security give admins more access to Intune data than what's available in the Intune admin center?

No. The Intune capabilities in Copilot for Security are built using the existing Microsoft Graph APIs, which are the same APIs that the Intune admin center uses. Both Copilot experiences use the same Intune capabilities.

### To get Intune insights, should I use Copilot for Security or Copilot in Intune?

To use Copilot with your Intune data, you can use Copilot in Intune or Copilot for Security. Here's a comparison of the two experiences:

| Feature | Copilot in Intune | Copilot for Security |
|---|---|---|
| **Access and data insights** |  This Copilot is embedded in the Intune admin center, and is scoped to only show Intune data. <br/><br/> Intune admins should use Copilot in Intune for Intune-only tasks. | This Copilot is the standalone experience. It can access other embedded services, like Microsoft Defender, Microsoft Entra ID, Microsoft Purview, and Microsoft Intune. <br/><br/>It accesses the same Intune capabilities as Copilot in Intune. |
| **Open prompting** |  Intune provides a set of prompts you can use. There isn't an open prompt. There are plans to include an open prompt in the future (no ETA).| Can use open prompts or use [promptbooks](/security-copilot/using-promptbooks). |
| **Prompt history** |  The prompt/response history isn't available in the Intune admin center. To view the prompt history, use Copilot for Security. <br/><br/>The prompts can look different compared with the prompts shown in Intune, as Intune enters the prompt for you. | You can review the prompt/response history, even when the prompt is submitted in the standalone or embedded experience. |
| **Target audience** | Focus is the IT admin/IT Pro. | Focus is the Security Operations Center (SOC) and can be used by IT admins. |

## Feedback and troubleshooting Copilot

### Copilot appears to show the wrong info. How can I debug and validate?

If you think that the output is incorrect, then submit feedback and add details about what you're seeing. This feedback helps improve the Copilot experience.

In the Copilot prompt window in the Intune admin center, there's a **Feedback** button:

:::image type="content" source="./media/copilot-intune-overview/feedback-message-icon.png" alt-text="Screenshot that shows how to provide Copilot feedback in Microsoft Intune and Intune admin center.":::

Other things you can try:

- In Microsoft Edge, you can use the F12 developer tools to debug the issue. In the developer debug tool, select the **Network** view. In Copilot, select the prompt to get the output. In the developer debug tool, use the **logs** entries to look more closely at the steps between the prompt input and output.

- If you're working with Microsoft to debug the issue, then they might ask you for the session ID. To get the session ID, you can:

  - Use the F12 developer tools in your browser. This information shows the capability that Copilot uses.
  - In the [Copilot for Security portal](https://go.microsoft.com/fwlink/?linkid=2247989), you can view the prompt sessions and session IDs from the Intune embedded experience.

## Related articles

- [Microsoft Copilot for Security FAQ](/security-copilot/faq-security-copilot)
- [Microsoft Copilot in Intune](copilot-intune-overview.md)
