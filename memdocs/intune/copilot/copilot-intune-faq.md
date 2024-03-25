---
# required metadata

title: Copilot in Intune FAQ
description: Get answers to common questions when using Copilot in Microsoft Intune.
keywords: security copilot, intune, microsoft intune, copilot, faq
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/25/2024
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
---

# Copilot in Intune FAQ

> [!IMPORTANT]
> This article is being updated for Copilot.

This article answers common questions about using Microsoft Copilot in Intune.

## FAQ

### open prompting

### Does Copilot for Security give admins more access to Intune data than what's available in the Intune admin center?

No. The Intune capabilities in Copilot for Security are built using the existing Microsoft Graph API's, which are the same API's that the Intune admin center uses. Both Copilot experiences use the same Intune capabilities.

Access to Copilot for Security is managed using Microsoft Entra roles. To access Intune data in Copilot for Intune and/or Copilot for Security, Copilot honors existing [Intune RBAC roles](../fundamentals/role-based-access-control.md) and [Intune scope tags](../fundamentals/scope-tags.md) assigned to admins when getting data.

So, your Intune admins are governed by existing access to Intune data.

`You don't have permission to access this feature. Reach out to your IT administrator for help.`

### Can I use Copilot for Security if I'm not an Intune admin, and vice versa?

Yes. Access to Copilot for Security is managed using Microsoft Entra roles. For more information on the different Copilot roles, and what they can do, go to [Roles and authentication in Microsoft Copilot for Security](/security-copilot/authentication).

If you're an Intune admin, you can use Copilot for Security to get insights into your Intune data. But, it's recommended to use Copilot in Intune. Copilot in Intune is scoped to only your Intune data and can use less security compute units (SCUs).

If you're a security admin, then use Copilot for Intune if you want to get insights into your Intune data. Copilot for Security is scoped to all your embedded services and can use more SCUs.

### Is there any way to limit which Intune admins see the Copilot experience?

No. All users of the Intune admin center can see the Copilot features. But, Intune admins can only access the data that they have permissions to, which includes the [RBAC roles](../fundamentals/role-based-access-control.md) and [scope tags](../fundamentals/scope-tags.md) assigned to them.

### Can I use other Microsoft Copilot for Security capabilities from other services, like Defender, Microsoft Entra and Purview from within the Intune admin center?

No. Copilot in Intune is available only for Intune capabilities. To get insights from other Microsoft services, you can use the [Copilot for Security portal](https://go.microsoft.com/fwlink/?linkid=2247989).

### Copilot appears to show the wrong info. How can I debug and validate this?

If you think that the output is incorrect, you can:

- Use the F12 developer tools in Microsoft Edge to debug the issue. In the developer debug tool, select the **Network** view. In Copilot, select the prompt to get the output. In the developer debug tool, use the **logs** entries to look more closely at the steps between the prompt input and output.

- If you're using Copilot to get more information about a specific device, then please provide feedback and add details about what you're seeing. There's a **Feedback** button in the Copilot prompt:

  :::image type="content" source="./media/copilot-intune-overview/feedback-message-icon.png" alt-text="Screenshot that shows how to provide Copilot feedback in Microsoft Intune and Intune admin center.":::

- If you're working with Microsoft to debug the issue, then they may ask you to enable F12 developer tools in your browser. This information shows the capability that Copilot uses.

  session ID

Intune: Session ID aren't visible in UI; Must do F12
Security:  Can view the prompt sessions from the standalone and embedded experiences. Also shows the session ID, which is helpful when troubleshooting w/MSFT

- Did you get an error? You can debug aspects of the prompt input, processing and output using Copilot for Security. to view more details on what went wrong, to to [Securitycopilot.microsoft.com](https://Securitycopilot.microsoft.com) and select the last session in your history.

## token limit on output
