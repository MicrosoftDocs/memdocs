---
title: Copilot in Intune shows device information and helps troubleshoot
description: Microsoft Security Copilot in Intune can help you get information about your devices, compare devices, and get error information. Use this information to help you manage and troubleshoot device issues.
ms.date: 09/17/2025
ms.update-cycle: 180-days
ms.topic: how-to
ms.reviewer: ankurgoyal, zadvor, rashok
ms.collection:
- M365-identity-device-management
- msec-ai-copilot
---

# Use Microsoft Copilot in Intune to troubleshoot devices

Microsoft Security Copilot is a generative-AI security analysis tool that can help your organization get information quickly. Copilot is [built into Microsoft Intune](copilot-intune-overview.md). It can help IT admins manage and troubleshoot devices.

Copilot uses your Intune data. Admins can only access the data that they have permissions to, which includes the [role based access control (RBAC) roles](../fundamentals/role-based-access-control.md) and [scope tags](../fundamentals/scope-tags.md) assigned to them. For more information, see [Copilot in Intune FAQ](copilot-intune-faq.md).

With Copilot in Intune, you can:

- Get more information about a specific device, including installed apps, group membership, and more.
- Compare devices to see the similarities and differences between them, like the compliance policies, hardware, and device configurations assigned to both devices.
- Use the error analyzer prompt to enter an error code, get more information about the error, and get a possible resolution.

This article describes how to use Copilot to manage and troubleshoot device issues in Intune.

## Before you begin

- To use Copilot in Intune, make sure Copilot is enabled. For more information, see:

  - [Copilot in Intune](../copilot/copilot-intune-overview.md#before-you-begin)
  - [Get started with Microsoft Security Copilot](/copilot/security/get-started-security-copilot)

- Sign into the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with the **Intune Administrator** Microsoft Entra ID role.

  For more information, see:

  - [Copilot in Intune FAQ - Access to Copilot](copilot-intune-faq.md#access-to-copilot)
  - [Microsoft Security Copilot authentication and roles](/copilot/security/authentication)

## Use a suggested prompt

To troubleshoot devices, you can use Copilot Chat to get more information about a device. For example, you can get a list of installed apps, compare devices, and get information about an error code.

The prompts include:

- Summarize this device.
- Analyze an error code.
- Compare this device with another device.
- Show apps on this device.
- Show policies on this device.
- Show group memberships.
- Show the primary user of this device.

As you type your question in Copilot Chat, an intelligent search matches your request to available prompts built into Intune. These prompts are shown as suggestions that you can select. You can also ask questions about a Microsoft Surface device, or troubleshoot issues in a Windows 365 Cloud PC.

## Get details and troubleshoot a device

This section guides you through some Copilot prompts that you can use.

1. Sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices**.
3. Select **Copilot**:

    :::image type="content" source="./media/copilot-devices/copilot-banner.png" alt-text="Screenshot that shows to select Copilot in the banner in Microsoft Intune or Intune admin center." lightbox="./media/copilot-devices/copilot-banner.png":::

4. Copilot Chat opens and shows some prompts that you can use that apply to all devices. Select a prompt to get more information. For example, select **Show me all non-compliant devices**:

    :::image type="content" source="./media/copilot-devices/all-noncompliant-devices.png" alt-text="Screenshot that shows all noncompliant devices in a Copilot prompt in Microsoft Intune or Intune admin center.":::

    The results show all noncompliant devices in your organization, including the device name, device ID, and more.

Let's walk through some other prompts.

### Summarize a device

In your Copilot Chat session, enter `summarize` and select the **Summarize an Intune device** prompt.

:::image type="content" source="./media/copilot-devices/summarize-intune-device-prompt.png" alt-text="Screenshot that shows the summarize an Intune device Copilot prompt in Microsoft Intune or Intune admin center.":::

When you submit the prompt, it asks for the device name or ID. The summary includes device-specific information, like the operating system, whether the device is registered in Microsoft Entra ID, malware counts, any noncompliant policies, group membership, and more.

### Compare devices

In your Copilot Chat session, enter `compare` and select the **Compare two Intune devices** prompt.

:::image type="content" source="./media/copilot-devices/compare-intune-device-prompt.png" alt-text="Screenshot that shows the compare an Intune device Copilot prompt in Microsoft Intune or Intune admin center.":::

With this prompt, you can compare a working/healthy device with a non-working/unhealthy device. This comparison helps you identify the differences between the two devices and troubleshoot the nonworking device.

When you submit the prompt, it asks for the device names or IDs to compare:

:::image type="content" source="./media/copilot-devices/compare-devices-comparison-type.png" alt-text="Screenshot that shows the Copilot comparing two devices in Microsoft Intune or Intune admin center.":::

The results show the differences and similarities between the two devices.

### Show policies assigned to this device

In the admin center, go to **Devices** > **All devices** and select any device. In your Copilot Chat session, enter `show policies` and select the **Show me device configuration policies assigned to a device** prompt.

:::image type="content" source="./media/copilot-devices/show-policies-prompt.png" alt-text="Screenshot that shows the device configuration policies assigned to a device in Copilot in Microsoft Intune or Intune admin center." lightbox="./media/copilot-devices/show-policies-prompt.png":::

Select the type of policies to show for the device:

:::image type="content" source="./media/copilot-devices/show-policies-type-prompt.png" alt-text="Screenshot that shows the policy types you can choose in a Copilot prompt in Microsoft Intune or Intune admin center." lightbox="./media/copilot-devices/show-policies-type-prompt.png":::

This prompt shows all the policies that are assigned to the device. Use this prompt to show configuration profiles, compliance policies, and app configuration policies.

## Related articles

- [Copilot in Intune](copilot-intune-overview.md)
- [Copilot in Intune FAQ](copilot-intune-faq.md)
