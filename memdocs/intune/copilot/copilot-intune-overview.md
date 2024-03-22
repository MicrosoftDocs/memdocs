---
# required metadata

title: Microsoft Copilot for Intune features overview
description: Microsoft Copilot for Intune is an AI platform. It can help you create policies, get information about existing policies, and show more details on specific settings, including their impacts on users and devices. You can also use Copilot to troubleshoot device issues.
keywords: Security Copilot, Intune, Microsoft Intune, AI, Copilot, settings catalog, policies, device details, troubleshooting
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/21/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice:
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: rashok, mikedano, zadvor
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
- security-copilot
---

# Microsoft Copilot in Intune (public preview)

> [!IMPORTANT]
> This article is being updated for Copilot.

This feature is in [public preview](../fundamentals/public-preview.md).

[Microsoft Copilot for Security](/security-copilot/microsoft-security-copilot) is a generative-AI security analysis tool. It can help you and your organization get information quickly, and help you make decisions that impact security and risk.

Intune has capabilities that are powered by Copilot. These capabilities access your Intune data, and can help you manage your policies & settings, understand your security posture, and troubleshoot device issues.

There are two ways to access your Intune data using Copilot:

- **Microsoft Copilot in Intune** (this article): Copilot is embedded in Intune and is available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). The Copilot prompts and their output are in the context of Intune and your Intune data. This experience has an IT admin/IT Pro focus.

- **Microsoft Copilot for Security**: This option is the standalone Copilot and is available in the [Microsoft Copilot for Security portal](https://go.microsoft.com/fwlink/?linkid=2247989). You can use this portal to get insights from Copilot for Security and other embedded services, like Intune, Microsoft Defender, Microsoft Entra ID, Microsoft Purview, and more. This experience has a Security Operations Center (SOC) focus, and can be used by IT admins.

This article focuses on Copilot in Intune and describes the Intune features that can use Copilot.

For more information on Copilot for Security, go to [Microsoft Copilot for Security](security-copilot.md).

## Before you begin

To use Copilot in Intune, you need the following:

- **Copilot security compute units (SCUs)**: Copilot in Microsoft Intune is included with Microsoft Copilot for Security. There aren't any additional licensing requirements or Intune-specific licenses for using Copilot in Intune.

  For more information on SCUs, go to [Get started with Microsoft Copilot](/security-copilot/get-started-security-copilot).

- **Copilot configuration**: Microsoft Copilot for Security must be configured and you must complete the first run experience. For the specific setup tasks, go to [Get started with Microsoft Copilot](/security-copilot/get-started-security-copilot).

  You can check the status in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Copilot**.

  :::image type="content" source="./media/copilot-intune-overview/tenant-administration-copilot-enabled.png" alt-text="Screenshot that shows Copilot is enabled in the Microsoft Intune tenant and Intune admin center." lightbox="./media/copilot-intune-overview/tenant-administration-copilot-enabled.png":::

- **Copilot roles**: Access to Copilot in Intune is managed through Microsoft Entra ID. To use Copilot in Intune, you/your admin team must be a member of the appropriate role in Microsoft Entra ID. There isn't a built-in Intune role that has access to Copilot.

  For the specific Microsoft Entra roles, and what they can do with Copilot, go to [Get started with Microsoft Copilot](/security-copilot/get-started-security-copilot).

- **Intune plug-in**: To use Copilot in Intune, you need the Intune plug-in enabled in Copilot for Security. This plug-in allows you to access your Intune data and use Copilot in the Intune admin center.

  By default, Intune should be enabled. To confirm, in the [Microsoft Copilot for Security portal](https://go.microsoft.com/fwlink/?linkid=2247989), select **plugins** (bottom left corner):

  :::image type="content" source="./media/copilot-intune-overview/security-copilot-plugins.png" alt-text="Screenshot that shows the plugins that are available, enabled, and disabled in Microsoft Copilot for Security.":::

  In **Manage plugins**, confirm Microsoft Intune is on:

  :::image type="content" source="./media/copilot-intune-overview/intune-plug-in-enabled.png" alt-text="Screenshot that shows the Microsoft Intune plug-in is enabled in Microsoft Copilot for Security.":::

  > [!TIP]
  > Some roles can enable or disable plugins. For more information, go to [Manage plugins in Microsoft Copilot for Security](/security-copilot/manage-plugins).

## Start using Copilot in Intune

To access Copilot for Intune, sign into the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). The Home screen lists the ways to get started with Copilot:

:::image type="content" source="./media/copilot-intune-overview/copilot-home-page.png" alt-text="Screenshot that shows the Intune admin center homepage with Copilot features in Microsoft Intune." lightbox="./media/copilot-intune-overview/copilot-home-page.png":::

Currently, there are two areas to use Copilot in Intune:

- Policy and setting management
- Device details and troubleshooting

### Policy and setting management

Copilot is embedded on policy settings and with your existing policies.

✅ Use Copilot to learn more about individual settings, their impact, and recommended values.

When you create an Intune policy, you add settings and configure these settings to meet your organization requirements. When you add a setting, there's a Copilot tooltip::

:::image type="content" source="./media/copilot-intune-overview/compliance-policy-setting-copilot-tooltip.png" alt-text="Screenshot that shows Copilot settings tooltip in a compliance policy in Microsoft Intune and Intune admin center." lightbox="./media/copilot-intune-overview/compliance-policy-setting-copilot-tooltip.png":::

When you select the Copilot tooltip, the Copilot prompt window opens and gives more information about that setting:

:::image type="content" source="./media/copilot-intune-overview/compliance-policy-setting-prompt-results.png" alt-text="Screenshot that shows more information about a setting when you select the Copilot tooltip in a compliance policy in Microsoft Intune and Intune admin center.":::

In the Copilot window, there are more prompts that you can use. You can also select the prompt guide and select from an existing list of prompts:

:::image type="content" source="./media/copilot-intune-overview/compliance-policy-setting-copilot-prompt-guide.png" alt-text="Screenshot that shows the Copilot prompt guide when you add a setting in a compliance policy in Microsoft Intune and Intune admin center.":::

The Copilot prompts can help you understand the impact of the setting, look for potential conflicts, and provide a recommended value.

You can use the Copilot tooltips on the following policy types in Intune:

- Compliance policies
- Device configuration policies
- Endpoint security policies

✅ Use Copilot to summarize an existing policy

??START HERE

Get more information about existing policies, including security impact and risk.

Copilot can help you understand the impact of a policy on your users and devices. You can also use Copilot to get more information about existing policies, including security impact and risk.



For more information on using Copilot with the settings catalog, go to [Use the settings catalog to create device configuration policies](../configuration/settings-catalog.md).

?? TO DO: also update:

- DONE: /configuration/settings-catalog.md
- DONE: /configuration/administrative-templates.md
- /configuration/device-profile-monitor.md#view-conflicts
- /configuration/device-profile-troubleshoot.md
- device configuration
- compliance policies
- endpoint security policies


### Device details and troubleshooting

✅ Use Copilot to get device details and troubleshoot a device.

You can use Copilot to get device-specific information, like the installed apps, group membership, and more.

There's also a prompt to enter an error code to get more information about the error and how to resolve it. This feature can help your support team troubleshoot device issues.

For more information on using Copilot with your devices, go to [Use Microsoft Copilot in Intune to troubleshoot devices](../copilot/copilot-devices.md).

## Microsoft Copilot for Security and Intune

| Feature | Microsoft Copilot for Security | Microsoft Copilot in Intune |
|---|---|---|
| **Access** | Standalone experience | Embedded in Intune |
| **Insights** | Insights from multiple Microsoft services, including Intune | Insights from Intune data |
| **Prompt history** | Review prompt/response history | No prompt/response history |
| Open prompt | Yes | No open prompt; Scoped prompt to Intune feature; Select from an existing list of prompts |
| Audience | Sec Ops focus; can be used by IT admins | IT admin / IT Pro |
| Sessions | View the sessions executed in embedded experiences. Get the session ID | Session ID aren't visible in UI; Must do F12 |

Same Intune skills in both experiences.

create a table: intune copilot vs security copilot
help admins do their job

You can review prompt/response history in standalone, regardless of whether the prompt was submitted in standalone or an embedded experience. There's no way to see prompt/response history in Intune embedded.

governed by existing access

Intune sessions are visible in standalone, prompts might look different from embedded vs standalone
Focus on IT admin

[Microsoft Copilot for Security and Intune](security-copilot.md)

- Did you get an error? You can debug aspects of the prompt input, processing and output using Copilot for Security. to view more details on what went wrong, to to [Securitycopilot.microsoft.com](https://Securitycopilot.microsoft.com) and select the last session in your history.

## Related content

- [Use Microsoft Copilot in Intune to troubleshoot devices](../copilot/copilot-devices.md)
- [Use the settings catalog to create device configuration policies](../configuration/settings-catalog.md)