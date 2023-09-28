---
# required metadata

title: Use Security Copilot to get device and policy information
description: You can use Security Copilot to get information about your devices, apps, policy assignments, and groups managed in Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/27/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: copilot
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: scottduf
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

Security Copilot is a cloud-based AI platform that provides a natural language copilot experience. It can help support security professionals and IT admins in different scenarios, like incident response, threat hunting, and intelligence gathering. For more information, go to [What is Microsoft Security Copilot?](/security-copilot/microsoft-security-copilot).

If you use Intune in the same tenant as Security Copilot, then you can use Security Copilot to get information about your devices, apps, and policy assignments managed in Intune. Specifically, Security Copilot gets insights from your Intune data. You can use prompts to get more information about specific devices, app usage & assignments, user and group membership, and more.

This article introduces you to Security Copilot and includes sample prompts that can help Intune admins.

## Before you begin

- Be clear and specific with your prompts. You may get better results if you include specific device IDs/names, app names, or policy names in your prompts.

  It may also help to add **Intune** to your prompt, like **What are the Windows device names managed by Intune?** or **How many Android devices are managed by Intune?**.

- Experiment with different prompts and variations to see what works best for your use case. Chat AI models vary, so iterate and refine your prompts based on the results you receive.

- When you have a good prompt, save the text for future use. When you close the Security Copilot session, your prompts and answers aren't saved.

For more information on writing Security Copilot prompts, go to [Microsoft Security Copilot prompting tips](/security-copilot/prompting-tips).

## Open Security Copilot

1. Go to `https://securitycopilot.microsoft.com` and sign in with your credentials.
2. Enter your prompt.

## Sample prompts for Intune admins

There are many prompts you can use to get information about your Intune data. Here are some ideas and examples:

### General information about your Intune data

Get **general information** about your Intune data, like the number of devices, apps deployed, platform versions of your devices, and more.

**Sample prompts**:

- What apps are added to Intune?
- What Intune apps are assigned the most?
- How many devices are managed by Intune?
- What are the device names managed by Intune?
- What are the Android device IDs managed by Intune?
- What are the versions of the iOS and iPadOS devices in Intune?
- How many macOS devices are enrolled in Intune?

### Policy targets

Get details on **policy targets**, like the groups that have a specific app assigned or how many users have a specific app assigned.

**Sample prompts**:

- How many users is appX assigned to?
- Which groups are appX assigned to?
- How many apps are assigned to the device ID *Enter the device ID* in Intune?
- Why is "Allow Microsoft Store App to auto update" policy applying to DeviceX?

### Specific devices

Get information about a **specific device**, like its group memberships and the apps assigned to it.

**Sample prompts**:

- What groups are DeviceX in?
- Tell me about DeviceX
- Who is the primary user for DeviceX?
- Is appX installed on DeviceX?
- Show me discovered apps on DeviceX

### Similarities and differences

Get the **similarities and differences** between two devices, like the compliance policies, hardware, and device configurations assigned to both devices.

**Sample prompts**:

- What is the hardware configuration difference between the DeviceX and DeviceZ devices?
- What are the similarities in compliance policy between the DeviceX and DeviceZ devices?
- What is the difference in device configuration profile between the DeviceX and DeviceZ devices?

## Related articles

- [What is Microsoft Security Copilot?](/security-copilot/microsoft-security-copilot)
