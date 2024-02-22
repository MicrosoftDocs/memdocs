---
# required metadata

title: Microsoft Copilot for Intune features overview
description: Microsoft Copilot for Intune is an AI platform. It can help you create policies, get information about existing policies, and show more details on specific settings, including their impacts on users and devices. You can also use Copilot to troubleshoot device issues.
keywords: Security Copilot, Intune, Microsoft Intune, AI, Copilot, settings catalog, policies, device details, troubleshooting
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/22/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
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

> [!WARNING]
> This article is being written. Waiting for new UI experience to be added to Woodgrove. Outstanding tasks:
>
> - Add this article to toc.yml
> - Finish writing based on UI changes

This feature is in [public preview](public-preview.md).

Onboarding guide: https://microsoft.sharepoint-df.com/:w:/t/IntuneOpenAI/EV8cbwNpWWNHnTdBZcxKbREBxXm7BcU4jbzb6Wcfh9qHRw?e=TIz6Kx&wdOrigin=TEAMS-MAGLEV.p2p_ns.rwc&wdExp=TEAMS-TREATMENT&wdhostclicktime=1707782151969&web=1

[Microsoft Copilot for Security](/security-copilot/microsoft-security-copilot) is a generative-AI security analysis tool that can help your organization get information quickly, and help you make decisions that impact security and risk.

Copilot is built into the Microsoft Intune admin center and is available for some features, like the settings catalog.

Security Copilot gets insights from your Intune data. You can use these insights to help you manage your policies & settings, understand your security posture, and troubleshoot device issues.

This article describes the Intune features that can use Copilot.

## Prerequisites

To use Copilot in Intune, you need the following:

- **Copilot license**: Copilot in Microsoft Intune is licensed with Microsoft Copilot for Security. There aren't any additional licensing requirements or Intune-specific licenses for using Copilot in Intune.

  For more information on Microsoft Copilot licensing, go to [Get started with Microsoft Copilot](/security-copilot/get-started-security-copilot).

- **Copilot configuration**: Microsoft Copilot must be configured in your Microsoft Entra tenant. For the specific setup tasks, go to [Get started with Microsoft Copilot](/security-copilot/get-started-security-copilot).

  To confirm Copilot is set up, you can check the status in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Copilot**.

  INSERT SCREEN SHOT

- **Copilot roles**: Access to Copilot in Intune is managed through Microsoft Entra ID. To use Copilot in Intune, you/your admin team must be a member of the appropriate role in Entra ID. There isn't a built-in Intune role that has access to Copilot.

  For the specific Entra roles, and what they can do with Copilot, go to [Get started with Microsoft Copilot](/security-copilot/get-started-security-copilot).

## Tips for good prompts

- When creating a policy, use the **Generate**, **Draft**, or **Create** verbs as keywords for the open prompt to invoke policy generation skills.

- When you enter more context in a prompt, then you get output that is more accurate and complete. Copilot doesn't proactively ask for more information before making inferences about your policy intent. So, to make your desired outcome clear, provide as much detail as you can.

- Did you get an error? You can debug aspects of the prompt input, processing and output using Copilot for Security. to view more details on what went wrong, to to [Securitycopilot.microsoft.com](https://Securitycopilot.microsoft.com) and select the last session in your history.

## Settings catalog policy and settings

Copilot is embedded in the Intune settings catalog. You can use Copilot to:

- Create new settings catalog policies.
- Get more information about existing policies, including potential conflicts, security impact, and risk.
- Learn more about individual settings, including their impact on users & devices, and recommended values.
- List the settings catalog policies and settings for a specific device, or compare existing policies.

For more information on using Copilot with the settings catalog, including sample prompts, go to [Use the settings catalog to create device configuration policies](../configuration/settings-catalog.md).

### Existing policy example

You can use Copilot to get more information about existing settings catalog policies. In this scenario, Copilot is in the scope of a specific policy.

For example, you can ask Copilot to show you the settings catalog policy and settings for a specific device, or compare settings catalog policies.

??Need more information. Experience isn't in Woodgrove yet. ??

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration**.
2. Select any existing settings catalog policy > **Copilot**.

TO DO: also update:

- DONE: /configuration/settings-catalog.md
- DONE: /configuration/administrative-templates.md
- /configuration/group-policy-analytics-migrate.md
- /configuration/device-profile-monitor.md#view-conflicts
- /configuration/device-profile-troubleshoot.md


## Device details and troubleshooting

Copilot is also embedded in the Intune device details. You can use Copilot to get device-specific information, like the installed apps, group membership, and more.

There's also a prompt to enter an error code to get more information about the error and how to resolve it. This feature can help your support team troubleshoot device issues.

For more information on using Copilot with your devices, go to [Use Microsoft Copilot for Security to troubleshoot devices in Microsoft Intune](../fundamentals/copilot-devices.md).

## Microsoft Copilot for Security and Intune

[Microsoft Copilot for Security and Intune](security-copilot.md)




## Related content
