---
# required metadata

title: Microsoft Copilot for Intune features overview
description: Microsoft Copilot for Intune is an AI platform. It can help you create policies, get information about existing policies, and show more details on specific settings, including their impacts on users and devices. You can also use Copilot to troubleshoot device issues.
keywords: Security Copilot, Intune, Microsoft Intune, AI, Copilot, settings catalog, policies, device details, troubleshooting
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/13/2024
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

# Microsoft Copilot for Intune (public preview)

> [!WARNING]
> This article is being written.

This feature is in [public preview](public-preview.md).

Onboarding guide: https://microsoft.sharepoint-df.com/:w:/t/IntuneOpenAI/EV8cbwNpWWNHnTdBZcxKbREBxXm7BcU4jbzb6Wcfh9qHRw?e=TIz6Kx&wdOrigin=TEAMS-MAGLEV.p2p_ns.rwc&wdExp=TEAMS-TREATMENT&wdhostclicktime=1707782151969&web=1

[Microsoft Copilot for Security](/security-copilot/microsoft-security-copilot) is a generative-AI security analysis tool that can help your organization get information quickly, and help you make decisions that impact security and risk.

Copilot is built into the Intune admin center and is available for some features, including the settings catalog.

You can use Copilot to create settings catalog policies, get information about existing policies, learn more about individual settings and their impact, and get device-specific details.

You can use this data to help you manage your policies & settings, understand your security posture, and possibly troubleshoot device issues.

This article describes the Intune features that can use Copilot.

## Prerequisites

- Copilot in Microsoft Intune is licensed with Microsoft Copilot for Security. There aren't any additional user licensing requirements for using Copilot in Intune.

  For more information on the Microsoft Copilot for Security licensing requirements, go to [Get started with Microsoft Copilot](/security-copilot/get-started-security-copilot).

- To use Copilot in Intune, you need the following RBAC roles:
  
  - Policy and profile manager: If you're using Copilot to create or manage Intune policies, then at a minimum, sign in with an account that is a member of this built-in Intune role.
  - Intune Service Administrator ??
  - Intune Role Administrator ??

  Access to Copilot in Intune is managed through RBAC roles in Copilot for Security, not Intune??

## Tips for good prompts

- When creating a policy, use the **Generate**, **Draft**, or **Create** verbs as keywords for the open prompt to invoke policy generation skills.

- When you enter more context in a prompt, then you get output that is more accurate and complete. Copilot doesn't proactively ask for more information before making inferences about your policy intent. So, to make your desired outcome clear, provide as much detail as you can.

- Did you get an error? You can debug aspects of the prompt input, processing and output using Copilot for Security. to view more details on what went wrong, to to [Securitycopilot.microsoft.com](https://Securitycopilot.microsoft.com) and select the last session in your history.

## Settings catalog policy and settings

Copilot is embedded with the Intune settings catalog. You can use Copilot to:

- Create new settings catalog policies.
- Get more information about existing policies, including potential conflicts, security impact, and risk.
- Get more information about a specific setting, including its impact on users & devices, and recommended values.
- List the settings catalog policies and settings for a specific device, or compare existing policies.

For more information on using Copilot with the settings catalog, including sample prompts, go to [Use the settings catalog to create device configuration policies](../configuration/settings-catalog.md).

### Existing policy example

You can use Copilot to get more information about existing settings catalog policies. In this scenario, Copilot is in the scope of a specific policy.

For example, you can ask Copilot to show you the settings catalog policy and settings for a specific device, or compare settings catalog policies.

??Need more information. Experience isn't in Woodgrove yet. ??

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration**.
2. Select any existing settings catalog policy > **Copilot**.

TO DO: also update:

- DONE: /configuration/settings-catalog.md
- /configuration/administrative-templates.md
- /configuration/group-policy-analytics-migrate.md
- /configuration/device-profile-monitor.md#view-conflicts
- /configuration/device-profile-troubleshoot.md


## Device-specific info


1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **All devices**.
2. Select any existing device.
3. Select **Copilot** and then select one of the options, like **Explore device**:

    :::image type="content" source="./media/copilot-intune-overview/copilot-select-device.png" alt-text="Screenshot that shows selecting any device and then select Copilot in Microsoft Intune and Intune admin center.":::

## Microsoft Copilot for Security and Intune

[Microsoft Copilot for Security and Intune](security-copilot.md)




## Related content
