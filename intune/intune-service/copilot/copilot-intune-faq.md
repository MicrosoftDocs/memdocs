---
title: FAQ for Microsoft Copilot in Intune
description: Get answers to common questions when using Copilot in Microsoft Intune, including accessing Copilot, licensing, and more.
ms.date: 09/17/2025
ms.update-cycle: 180-days
ms.topic: how-to
ms.reviewer: ankurgoyal, rashok
ms.collection:
- M365-identity-device-management
- msec-ai-copilot
---

# Microsoft Copilot in Intune FAQ

This article answers common questions about using Microsoft Copilot in Intune. To learn more about Copilot in Intune and to get started, see [Microsoft Copilot in Intune overview](copilot-intune-overview.md).

## Access to Copilot

### How can I control access to Copilot in Intune?

When you set up Security Copilot, you determine the Copilot role that your admins can have (**owner** or **contributor**), as described in [Roles and authentication in Microsoft Security Copilot](/copilot/security/authentication). There are also Microsoft Entra roles that can control access to Security Copilot.

The Security Copilot roles or the Microsoft Entra roles that you configure control access to Copilot in Intune. There aren't any Intune-specific roles-based access controls (RBAC) for Copilot in Intune.

After you enable Intune in Security Copilot, your Intune admins can see the Copilot features in the Intune admin center. But they can only access the data that they have permission to. Copilot honors existing [Intune RBAC roles](../fundamentals/role-based-access-control.md) and [Intune scope tags](../fundamentals/scope-tags.md) that are assigned to your admins.

So, if an admin tries to access Intune data that they don't have permissions to, they get the following error message:

`You don't have permission to access this feature. Reach out to your IT administrator for help.`

**Key info**:

- If you want access to Copilot in Intune, contact the Security Copilot workspace owner in your organization. Other roles can be assigned access to Copilot in Intune through Security Copilot.

- If you want access to all your Intune data, contact your Intune administrator. By default, the **Intune Administrator** role in Microsoft Entra ID has access to Copilot in Intune.

### Can I use Security Copilot if I'm not an Intune admin, and vice versa?

Yes. Access to Security Copilot is managed by using Security Copilot or Microsoft Entra roles. For more information, see [Roles and authentication in Microsoft Security Copilot](/copilot/security/authentication).

If you're an admin for Intune and have the correct Security Copilot or Microsoft Entra role assigned to you, you can use Security Copilot to get insights about your Intune data.

Security Copilot is scoped to all your embedded services.

If you're an Intune admin or IT admin and only want Intune data, you should use [Copilot in Intune](copilot-intune-overview.md). Its scope is only Intune data, and its capabilities are integrated into the relevant areas of the Intune admin center.

If you're a security admin, you can use [Copilot in Intune](copilot-intune-overview.md) if you only want insights into your Intune data.

## Capabilities and cost

### How do I turn on Intune capabilities?

In the [Microsoft Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989), select **Sources** (prompt bar > right corner), and enable the Microsoft Intune plug-in. This plug-in allows you to access your Intune data and use the Copilot features in the Intune admin center.

For more information about managing plug-ins, see [Manage plug-ins in Security Copilot](/copilot/security/manage-plugins).

### Can I use capabilities for other Copilot services in the Intune admin center?

No. Copilot in Intune in the Intune admin center is available only for Intune capabilities.

You can't get insights from other Microsoft services, like Microsoft Defender, Microsoft Entra, and Microsoft Purview. To get insights from other Microsoft services, you can use the [Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989).

### How much does Copilot in Intune cost?

Copilot in Intune is included with Security Copilot. Security Copilot uses security compute units (SCUs). There aren't any other licensing requirements or Intune-specific licenses for using Copilot in Intune.

You need Security Copilot enabled to access Copilot in Intune features. Some Copilot in Intune capabilities can use little to none of your provisioned SCUs, while other capabilities can use more. Usage will also change as Copilot in Intune capabilities are changed and improved over time.

For more information about SCUs, see:

- [Get started with Security Copilot](/copilot/security/get-started-security-copilot)
- [Manage capacity in Security Copilot](/copilot/security/manage-usage)

### Is there a limit on the prompt output?

Copilot in Intune is bound by any token limits in Security Copilot. For more information, see [Security Copilot FAQ - Token limits](/copilot/security/faq-security-copilot#how-is-copilot-for-security-dealing-with-a-token-limit).

## Security Copilot vs. Copilot in Intune

### Does Security Copilot give admins more access to Intune data than is available in the Intune admin center?

No. The Intune capabilities in Security Copilot are built using the existing Microsoft Graph APIs, which are the same APIs that the Intune admin center uses. Both Copilot experiences use the same Intune capabilities.

### To get Intune insights, should I use Security Copilot or Copilot in Intune?

To use Copilot with your Intune data, you can use Copilot in Intune or Security Copilot. Here's a comparison of the two experiences:

| Feature | Copilot in Intune | Security Copilot |
|---|---|---|
| **Access and data insights** |  This Copilot is embedded in the Intune admin center and is scoped to only show Intune data.<br/><br/> Intune admins should use Copilot in Intune for Intune-only tasks. | This Copilot is a standalone experience. It can access other embedded services, like Microsoft Defender, Microsoft Entra ID, Microsoft Purview, and Microsoft Intune. <br/><br/>It accesses the same Intune capabilities as Copilot in Intune. |
| **Open prompting** |  Intune has built-in prompts you can use and access from Copilot Chat in Intune. In Copilot Chat, you can enter a query. Copilot summarizes the results and recommends built-in prompts based on the text you enter. <br/><br/>There isn't an open prompt. There are plans to include an open prompt in the future (no ETA). | Can use open prompts or use [promptbooks](/copilot/security/using-promptbooks). |
| **Prompt history** |  The prompt/response history isn't available in the Intune admin center. To view the prompt history, use Security Copilot.<br/><br/>The prompts can look different compared with the prompts shown in Intune, as Intune enters the prompt for you. | You can review the prompt/response history even when the prompt is submitted in the standalone or embedded experience. |
| **Target audience** | Focus is the IT admin/IT Pro. | Focus is the Security Operations Center (SOC) and can be used by IT admins. |

## Feedback and troubleshooting Copilot

### Copilot appears to show the wrong info. How can I debug and validate?

If you think that the output is incorrect, submit feedback in your Copilot Chat session in Intune, and include details about what you're seeing.

Every Copilot response has two feedback buttons – a thumbs up when the response is what you expect, and a thumbs down when the response isn't what you expect. This feedback helps improve the Copilot experience.

:::image type="content" source="./media/copilot-intune-faq/thumbs-up-thumbs-down.png" alt-text="Screenshot that shows how to provide Copilot feedback in Microsoft Intune and Intune admin center.":::

Other things you can try:

- In Microsoft Edge, you can use the F12 developer tools to debug the issue. In the developer debug tool, select the **Network** view. In Copilot, select the prompt to get the output. In the developer debug tool, use the **logs** entries to look more closely at the steps between the prompt input and output.

- If you're working with Microsoft to debug the issue, support might ask you for the session ID. To get the session ID, you can:

  - Use the F12 developer tools in your browser. This information shows the capabilities that Copilot uses.
  - In the [Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989), you can view the prompt sessions and session IDs from the Intune embedded experience.

To learn more about privacy and data security, what data is collected as part of feedback, and how to disable feedback, see [Privacy and data security in Security Copilot](/copilot/security/privacy-data-security).

### Can I use Give Feedback to submit feedback?

In the admin center, if you select the three dots (...) in the top right corner, you see the **Give Feedback** option. This option is for general feedback about Microsoft Azure, not for Copilot in Intune. Don't use this option to provide any feedback related to Security Copilot in Intune.

:::image type="content" source="./media/copilot-intune-faq/azure-give-feedback.png" alt-text="Screenshot that shows how the Azure feedback option in Microsoft Intune and Intune admin center.":::

To disable the Microsoft Azure **Give Feedback** form, see [Manage access to Microsoft Copilot in Azure](/azure/copilot/manage-access).

## Related articles

- [Security Copilot FAQ](/copilot/security/faq-security-copilot)
- [Copilot in Intune](copilot-intune-overview.md)
