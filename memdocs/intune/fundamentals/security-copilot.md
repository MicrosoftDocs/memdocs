---
# required metadata

title: Use Security Copilot to get device and policy information
description: You can use Security Copilot to get information about your Intune data, including devices, apps, policies, and groups managed in Intune. You can also compare policies, get device specific details, and get target info for policies.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 10/10/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: scottduf, rashok
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

# Microsoft Security Copilot (preview) and Intune

> [!IMPORTANT]
> The information in this article applies to the Microsoft Security Copilot Early Access Program, which is an invite-only paid preview program. Some information in this article relates to prereleased product, which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided in this article.

Security Copilot is a cloud-based AI platform that provides a natural language copilot experience. It can help support security professionals in different scenarios, like incident response, threat hunting, and intelligence gathering. For more information about what it can do, go to [What is Microsoft Security Copilot?](/security-copilot/microsoft-security-copilot).

**Security Copilot integrates with Microsoft Intune**.

If you use [Microsoft Intune](what-is-intune.md) in the same tenant as Security Copilot, then you can use Security Copilot to view managed device attributes and configuration data. You can get information about your devices, apps, compliance & configuration policies, and policy assignments managed in Intune.

Specifically, Security Copilot gets insights from your Intune data. You can use the system features built into Security Copilot, and use prompts to get more information. This information can help you understand your security posture and possibly troubleshoot device issues.

This article introduces you to Security Copilot and includes sample prompts that can help Intune admins.

## Know before you begin

- Be clear and specific with your prompts. You might get better results if you include specific device IDs/names, app names, or policy names in your prompts.

  It might also help to add **Intune** to your prompt, like:

  - **According to Intune, how many devices were enrolled this week**
  - **Tell me about Intune devices for (user name)**

- Experiment with different prompts and variations to see what works best for your use case. Chat AI models vary, so iterate and refine your prompts based on the results you receive.

- Security Copilot saves your prompt sessions. To see the previous sessions, in Security Copilot, go to the menu > **My investigations**:

  :::image type="content" source="./media/security-copilot/security-copilot-menu-my-investigations.png" alt-text="Screenshot that shows the Microsoft Security Copilot menu and My investigations with previous sessions.":::

  For a walkthrough on Security Copilot, including the pin and share feature, go to [Navigating Microsoft Security Copilot](/security-copilot/navigating-security-copilot).

For more information on writing Security Copilot prompts, go to [Microsoft Security Copilot prompting tips](/security-copilot/prompting-tips).

## Open Security Copilot

1. Go to [Microsoft Security Copilot](https://go.microsoft.com/fwlink/?linkid=2247989) and sign in with your credentials.
2. By default, Intune should be enabled. To confirm, select **plugins** (bottom left corner):

    :::image type="content" source="./media/security-copilot/security-copilot-plugins.png" alt-text="Screenshot that shows the plugins that are available, enabled, and disabled in Microsoft Security Copilot.":::

    In **My plugins**, confirm Microsoft Intune is on. Close **Plugins**.

    > [!NOTE]
    > Some roles can enable or disable plugins, like Microsoft Intune. For more information, go to [Manage plugins in Microsoft Security Copilot](/security-copilot/manage-plugins).

3. Enter your prompt.

## Built-in system features

In Security Copilot, there are built in system features. These features can get data from the different plugins that are enabled.

To view the list of built-in system capabilities for Intune, use the following steps:

1. In the prompt, enter **/**.
2. Select **See all system capabilities**.
3. In the Intune section, you can:

    - Compare different security baselines.
    - Get a summary of an existing policy.
    - Get policy assignment scope.
    - Get the differences or comparisons between two devices.
    - Quickly gather details for a device by asking about it.
    - Get detailed information about a user's device enrollments and device compliance for troubleshooting or a security investigation.
    - And more

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
- Tell me about DeviceA
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

Your feedback on the Intune integration with Security Copilot helps with development. To provide feedback, in Security Copilot, use the feedback buttons at the bottom of each completed prompt:

:::image type="content" source="./media/security-copilot/security-copilot-prompt-feedback.png" alt-text="Screenshot that shows how to submit feedback on the prompt results in Microsoft Security Copilot.":::

Your options:

- **Confirm**: The results match expectations.
- **Off-target**: The results don't match expectations.
- **Report**: The results are harmful in some way.

Whenever possible, and when the result is **Off-target**, write a few words explaining what can be done to improve the outcome. If you entered Intune-specific prompts and the results aren't Intune related, then include that information.

## Data processing and privacy

When you interact with the Security Copilot to get Intune data, Security Copilot pulls that data from Intune. The prompts, the Intune data that's retrieved, and the output shown in the prompt results is processed and stored within the Security Copilot service.

For more information about data privacy in Security Copilot, go to [Privacy and data security in Microsoft Security Copilot](/security-copilot/privacy-data-security).

## Related articles

- [What is Microsoft Security Copilot?](/security-copilot/microsoft-security-copilot)
- [Privacy and data security in Microsoft Security Copilot](/security-copilot/privacy-data-security)
