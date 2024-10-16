---
# required metadata

title: Use Security Copilot to get device and policy information
description: You can use Security Copilot to get information about your Intune data, including devices, apps, policies, and groups managed in Intune. You can also compare policies, get device specific details, and get target info for policies.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/01/2024
ms.topic: concept-article
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
- magic-ai-copilot
---

# Access your Microsoft Intune data in Security Copilot

Security Copilot is a cloud-based AI platform that provides a natural language Copilot experience. It can help support security professionals in different scenarios, like incident response, threat hunting, and intelligence gathering. For more information about what it can do, go to [What is Microsoft Security Copilot?](/security-copilot/microsoft-security-copilot).

**Security Copilot integrates with your Microsoft Intune data**.

If you use [Microsoft Intune](../fundamentals/what-is-intune.md) in the same tenant as Security Copilot, then you can use Security Copilot to get insights about your Intune data.

There are Intune capabilities built into Security Copilot, and you can use prompts to get more information, including:

- Information about your devices, apps, compliance & configuration policies, and policy assignments managed in Intune
- Managed device attributes and hardware details
- Issue with specific devices and compare a working & non-working device

This article shows you how to access your Microsoft Intune data in Security Copilot and includes sample prompts.

## Security admin focus

Security Copilot has a Security Operations Center (SOC) or security admin focus. So, if you're a SOC analyst or security admin, then you can use Security Copilot to get the security posture of devices that Intune manages.

For example, there's a user or device that is showing signs of malicious intent. Also, you notice some events are happening after the malicious intent, like an unknown device enrolling in Intune. Maybe someone is trying to use stolen credentials to enroll and get access. You need to get more information.

In Security Copilot, you can use the Intune capabilities to get more information, like:

- Ask about a specific device, get all the properties about that device, including the device name, device ID, and device manufacturer.
- Determine when the device is enrolled in Intune.
- Find the primary user of a device
- Determine the type of device, like a laptop or mobile phone.
- Check the compliance status, especially if a device is noncompliant, and why it's noncompliant.

In Microsoft Defender, you can use this information, including the device type, to determine your next steps. For example, you might take different actions based on the type of device (laptop vs. mobile phone vs. tablet). Security Copilot can also give you a link to the device in Microsoft Defender, so you can run any Defender actions.

### What you need to know

- When an admin submits a prompt, Copilot can only access the data that the admin has permissions to, which includes the [RBAC roles](../fundamentals/role-based-access-control.md) and [Intune scope tags](../fundamentals/scope-tags.md) assigned to them.

  If you want your admins to access all your Intune data in Security Copilot, then use the following role in Microsoft Entra ID:

  - Intune Service Administrator (also known as Intune Administrator)

  For more information on roles and authentication, go to:

  - [Roles and authentication in Microsoft Security Copilot](/security-copilot/authentication)
  - [Role based access control (RBAC) in Intune](../fundamentals/role-based-access-control.md)
  - [Use RBAC and scope tags for distributed IT in Intune](../fundamentals/scope-tags.md)

- You can access your Intune data in the [Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989) and Copilot in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). For more information on Copilot in Intune vs. Security Copilot, and other common questions, go to the [Microsoft Copilot in Intune FAQ](copilot-intune-faq.md).

## Open Security Copilot and enable Intune

To use the Intune capabilities in Security Copilot, enable the Intune plugin.

1. Go to [Microsoft Security Copilot](https://go.microsoft.com/fwlink/?linkid=2247989) and sign in with your credentials.
2. In the prompt bar, select **Sources** (right corner).

    :::image type="content" source="./media/security-copilot/security-copilot-sources.png" alt-text="Screenshot that shows the plugin sources that are available, enabled, and disabled in Microsoft Security Copilot.":::

3. In **Manage sources**, turn on Microsoft Intune:

    :::image type="content" source="./media/security-copilot/intune-plug-in-enabled.png" alt-text="Screenshot that shows the Microsoft Intune plug-in source is enabled in Microsoft Security Copilot.":::

    > [!NOTE]
    > Some roles can enable or disable plugins. For more information, go to [Manage plugins in Microsoft Security Copilot](/security-copilot/manage-plugins).

## Use the built-in features

In Security Copilot, there are built in system features that are helpful for Intune admins. For a walkthrough of Security Copilot, go to [Navigating Microsoft Security Copilot](/security-copilot/navigating-security-copilot).

This section describes some of the features that are helpful for Intune admins.

### System capabilities

Capabilities are built-in features that can get data from the different plugins that you enable, including Microsoft Intune. When you use a prompt to ask something about your Intune data, like apps assigned to a user or device details, your prompts use these Intune capabilities.

To view the list of Intune built-in system capabilities for Intune, use the following steps:

1. In the [Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989) prompt bar, select the Copilot prompts icon > **See all system capabilities**.

    :::image type="content" source="./media/security-copilot/security-copilot-system-capabilities.png" alt-text="Screenshot that shows how to select the prompts icon and system capabilities in Microsoft Security Copilot.":::

2. In the Microsoft Intune section, there's a list of all the built-in capabilities for Intune. You can select any of the capabilities and get more information about that capability.

### Sessions

When you use prompts in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) or in the Security Copilot portal, the sessions are saved. To see the saved sessions, use the following steps:

1. In the [Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989), go to the menu > **My sessions**.

    :::image type="content" source="./media/security-copilot/security-copilot-menu-my-sessions.png" alt-text="Screenshot that shows the Microsoft Security Copilot menu and My sessions with previous sessions in Security Copilot portal.":::

2. When you select a session, your previous prompts and results are shown. Every session also has a session ID in the URL. You can share this session ID with others to review the same prompt session.

    For example, your session ID is something like `https://securitycopilot.microsoft.com/sessions/023d1c61-f3c7-4702-8924-075a1058900d`.

## Sample prompts for Intune

You can create your own prompts in Security Copilot to get information about your Intune data. This section lists some ideas and examples.

### Before you begin

- Be clear and specific with your prompts. You might get better results if you include specific device IDs or names, app names, or policy names in your prompts.

  It might also help to add **Intune** to your prompt, like:

  - **According to Intune, how many devices were enrolled this week?**
  - **Tell me about Intune devices for (user name).**

- Experiment with different prompts and variations to see what works best for your use case. Chat AI models vary, so iterate and refine your prompts based on the results you receive.  

  You can also save your prompts in a promptbook for future use. For more information, go to:

  - [Prompting in Microsoft Security Copilot](/security-copilot/prompting-security-copilot)
  - [Using promptbooks in Microsoft Security Copilot](/security-copilot/using-promptbooks)

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
- Why is the "Allow Microsoft Store App to auto update" policy applying to DeviceA?
- Tell me about Intune devices for user UserA.
- Why is PolicyA applying on DeviceB?

### Specific devices

Get information about a **specific device**, like its group memberships and the apps assigned to it.

**Sample prompts**:

- What devices are used by UserA@contoso.com?
- What groups is DeviceA in?
- Tell me about DeviceA.
- Who is the primary user for DeviceA?
- Is ContosoApp installed on DeviceA?
- Show me discovered apps on DeviceA.

### Similarities and differences

Get the **similarities and differences** between two devices, like the compliance policies, hardware, and device configurations assigned to both devices.

**Sample prompts**:

- What is the hardware configuration difference between the DeviceA and DeviceB devices?
- What are the similarities in compliance policies between the DeviceA and DeviceB devices?
- What is the difference in device configuration profile between the DeviceA and DeviceB devices?
- Compare installed applications on DeviceA and DeviceB.

## Provide feedback

Your feedback on the Intune integration with Security Copilot helps with development. To provide feedback, in Security Copilot, use the feedback buttons at the bottom of each completed prompt.

:::image type="content" source="./media/security-copilot/security-copilot-prompt-feedback.png" alt-text="Screenshot that shows how to submit feedback on the prompt results in Microsoft Security Copilot.":::

Whenever possible, and when the result isn't what you expect, write a few words explaining what can be done to improve the outcome. If you entered Intune-specific prompts and the results aren't Intune related, then include that information.

## Data processing and privacy

For more information about data privacy in Security Copilot, go to [Privacy and data security in Microsoft Security Copilot](/security-copilot/privacy-data-security).

When you interact with the Security Copilot to get Intune data, the Security Copilot pulls that data from Intune. The prompts, the Intune data that's retrieved, and the output shown in the prompt results is processed and stored within the Security Copilot service.

When you use Security Copilot to get Intune data, Security Copilot also has access to the data and permissions defined by the [RBAC roles](../fundamentals/role-based-access-control.md) and [Intune scope tags](../fundamentals/scope-tags.md) assigned to you.

## Related articles

- [What is Microsoft Security Copilot?](/security-copilot/microsoft-security-copilot)
- [Privacy and data security in Microsoft Security Copilot](/security-copilot/privacy-data-security)
- [Use Microsoft Copilot in Intune](copilot-intune-overview.md)
