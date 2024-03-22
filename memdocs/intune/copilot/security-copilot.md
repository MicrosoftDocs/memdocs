---
# required metadata

title: Use Copilot for Security to get device and policy information
description: You can use Copilot for Security to get information about your Intune data, including devices, apps, policies, and groups managed in Intune. You can also compare policies, get device specific details, and get target info for policies.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice:
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: rashok
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

# Microsoft Copilot for Security and Intune

> [!IMPORTANT]
> This article is being updated for Copilot.

Copilot for Security is a cloud-based AI platform that provides a natural language copilot experience. It can help support security professionals in different scenarios, like incident response, threat hunting, and intelligence gathering. For more information about what it can do, go to [What is Microsoft Copilot for Security?](/security-copilot/microsoft-security-copilot)

**Copilot for Security integrates with Microsoft Intune**. If you use [Microsoft Intune](../fundamentals/what-is-intune.md) in the same tenant as Copilot for Security, then you can use Copilot for Security and gets insights about your Intune data.



 to view managed device attributes and configuration data. You can get information about your devices, apps, compliance & configuration policies, and policy assignments managed in Intune.

designed for SOC analysts & security admins, can be used by Intune too. Main thing is separate from embedded experiences
open ended questions, can ask about one specific device, and get all properties about that device

There is Intune data that's important to SOC analysists, including user/device events that happen after a malicious intent, like a new device enrolled after a malicious event.

- get intune device info prompt

- compliance is also helpful to SOC analysts, like a device that's non-compliant, and the reason why it's non-compliant. It can help determine the next steps to take.

- Intune data shows who owns the device. In Defender, the type of device is also helpful. A reaction could be different based on laptop vs mobile phone.

  CfS today does not allow you to take actions through CfS itself. so you can't ask Copilot to go isolate a device. it can give you a link to the device in defender to go perform that action yourself. CfS today can only read stuff

Prompt/response history has a 30 days retention period.

document intune skills/capabilities

include sample intune prompts

Specifically, Copilot for Security gets insights from your Intune data. You can use the system features built into Copilot for Security, and use prompts to get more information. This information can help you understand your security posture and possibly troubleshoot device issues.

This article introduces you to Copilot for Security and includes sample prompts that can help Intune admins.

Copilot is also embedded in the Intune admin center. For more information, go to [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md).



## Standalone in Copilot for Security

Doc needs:

1. cover the feature
1. sample prompts
1. why this data is interesting to SOC analytics

Info important to SOC analytics

device name, ID, compliance status, when it was enrolled, non-compliant reason

was device recently enrolled
is it a hacker using stolen credentials that is trying to enroll and get access


can ask about one speicifc device, and get all properties about that device

what is the device
what is the device manufacturer

## Know before you begin

- Be clear and specific with your prompts. You might get better results if you include specific device IDs/names, app names, or policy names in your prompts.

  It might also help to add **Intune** to your prompt, like:

  - **According to Intune, how many devices were enrolled this week**
  - **Tell me about Intune devices for (user name)**

- Experiment with different prompts and variations to see what works best for your use case. Chat AI models vary, so iterate and refine your prompts based on the results you receive.

- Copilot for Security saves your prompt sessions. To see the previous sessions, in Copilot for Security, go to the menu > **My sessions**:

  :::image type="content" source="./media/security-copilot/security-copilot-menu-my-sessions.png" alt-text="Screenshot that shows the Microsoft Copilot for Security menu and My sessions with previous sessions.":::

  For a walkthrough on Copilot for Security, including the pin and share feature, go to [Navigating Microsoft Copilot for Security](/security-copilot/navigating-security-copilot).

For more information on writing Copilot for Security prompts, go to [Microsoft Copilot for Security - Create effective prompts](/security-copilot/prompting-tips).

## Open Copilot for Security

1. Go to [Microsoft Copilot for Security](https://go.microsoft.com/fwlink/?linkid=2247989) and sign in with your credentials.
2. By default, Intune should be enabled. To confirm, select **plugins** (bottom left corner):

    :::image type="content" source="./media/security-copilot/security-copilot-plugins.png" alt-text="Screenshot that shows the plugins that are available, enabled, and disabled in Microsoft Copilot for Security.":::

    In **Manage plugins**, confirm Microsoft Intune is on. Close **Plugins**.

    :::image type="content" source="./media/security-copilot/intune-plug-in-enabled.png" alt-text="Screenshot that shows the Microsoft Intune plug-in is enabled in Microsoft Copilot for Security.":::

    > [!NOTE]
    > Some roles can enable or disable plugins. For more information, go to [Manage plugins in Microsoft Copilot for Security](/security-copilot/manage-plugins).

3. You can:

    - Select **Promptbooks** to see an existing list of prompts and any saved sessions.
    - In the open prompt, enter your prompt.

## Built-in system features

In Copilot for Security, there are built in system features. These features can get data from the different plugins that are enabled.

To view the list of built-in system capabilities for Intune, use the following steps:

1. In the prompt, select **See all system capabilities**.
2. In the Microsoft Intune section, you can see the built-in capabilities for Intune:

    - Describe device configuration policy
    - Generate an Intune policy from a JSON file
    - Get app configuration policies for a specific device
    - Get an overview of the number of devices enrolled in Intune
    - And more.

## Sample prompts for Intune

There are many prompts you can use to get information about your Intune data. This section lists some ideas and examples.

### General information about your Intune data

Get **general information** about your Intune data, like the number of devices, apps deployed, platform versions of your devices, and more.

**Sample prompts**:

- What apps are added to Intune?
- What Intune apps are assigned the most?
- How many devices were enrolled in Intune in the last 24 hours?
- Tell me about Intune devices for Jon Smith.

### Policy targets

Get details on **policy targets**, like the groups that have a specific app assigned or how many users have a specific app assigned.

**Sample prompts**:

- How many users is ContosoApp assigned to?
- Which groups are ContosoApp assigned to?
- How many apps are assigned to the device ID *Enter the device ID* in Intune?
- Why is "Allow Microsoft Store App to auto update" policy applying to DeviceA?
- Tell me about Intune devices for user UserA.
- Why is PolicyA applying on DeviceB?

### Specific devices

Get information about a **specific device**, like its group memberships and the apps assigned to it.

**Sample prompts**:

- What groups are DeviceA in?
- Tell me about DeviceA.
- Who is the primary user for DeviceA?
- Is ContosoApp installed on DeviceA?
- Show me discovered apps on DeviceA

### Similarities and differences

Get the **similarities and differences** between two devices, like the compliance policies, hardware, and device configurations assigned to both devices.

**Sample prompts**:

- What is the hardware configuration difference between the DeviceA and DeviceB devices?
- What are the similarities in compliance policy between the DeviceA and DeviceB devices?
- What is the difference in device configuration profile between the DeviceA and DeviceB devices?
- Compare installed applications on DeviceA and DeviceB.

## Provide feedback

Your feedback on the Intune integration with Copilot for Security helps with development. To provide feedback, in Copilot for Security, use the feedback buttons at the bottom of each completed prompt:

:::image type="content" source="./media/security-copilot/security-copilot-prompt-feedback.png" alt-text="Screenshot that shows how to submit feedback on the prompt results in Microsoft Copilot for Security.":::

Your options:

- **Confirm**: The results match expectations.
- **Off-target**: The results don't match expectations.
- **Report**: The results are harmful in some way.

Whenever possible, and when the result is **Off-target**, write a few words explaining what can be done to improve the outcome. If you entered Intune-specific prompts and the results aren't Intune related, then include that information.

## Data processing and privacy

When you use Copilot for Security to get Intune data, Copilot for Security has access to the data and permissions defined by the RBAC roles and Scope tags assigned to you. If you want Copilot for Security to access all your Intune data, then use one of the following roles in Microsoft Entra ID:

- Global Administrator
- Intune Service Administrator (also known as Intune Administrator)

For more information about data privacy in Copilot for Security, go to [Privacy and data security in Microsoft Copilot for Security](/security-copilot/privacy-data-security).

## Related articles

- [What is Microsoft Copilot for Security?](/security-copilot/microsoft-security-copilot)
- [Privacy and data security in Microsoft Copilot for Security](/security-copilot/privacy-data-security)
