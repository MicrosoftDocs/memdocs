---
# required metadata

title: Copilot in Intune shows device information and errors
description: Microsoft Copilot in Intune can help you get information about your devices, compare devices, and get error information. Use this information to help you manage and troubleshoot device issues.
keywords: security copilot, intune, microsoft intune, copilot, device information, device errors, device troubleshooting, analyze error code, compare devices, AI, generative-AI
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/01/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice:
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: zadvor, rashok
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- magic-ai-copilot
---

# Use Microsoft Copilot in Intune to troubleshoot devices (public preview)

Microsoft Copilot for Security is a generative-AI security analysis tool that can help your organization get information quickly. Copilot is [built into Microsoft Intune](copilot-intune-overview.md). It can help IT admins manage and troubleshoot devices.

Copilot uses your Intune data. Admins can only access the data that they have permissions to, which includes the [RBAC roles](../fundamentals/role-based-access-control.md) and [scope tags](../fundamentals/scope-tags.md) assigned to them. For more information, see [Microsoft Copilot in Intune FAQ](copilot-intune-faq.md).

With Copilot in Intune, you can:

- Get more information about a specific device, including installed apps, group membership, and more.
- Compare devices to see the similarities and differences between them, like the compliance policies, hardware, and device configurations assigned to both devices.
- Use the error analyzer prompt to enter an error code, get more information about the error, and get a possible resolution.

This article describes how to use Copilot to manage and troubleshoot device issues in Intune.

## Before you begin

- Copilot in Intune is in [public preview](../fundamentals/public-preview.md).

- To use Copilot in Intune, make sure Copilot is enabled. For more information, see:

  - [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md#before-you-begin)
  - [Get started with Microsoft Copilot for Security](/security-copilot/get-started-security-copilot)

- When you use the Copilot prompts to troubleshoot your devices, you are within the scope of the device you select.

## Use a suggested prompt

To troubleshoot devices, you can use Copilot with an existing set of prompts to get more information about the device. For example, you can get a list of installed apps, compare devices, and get information about an error code.

The guided prompts include:

- Summarize this device.
- Analyze an error code.
- Compare this device with another device.
- Show apps on this device.
- Show policies on this device.
- Show group memberships.
- Show the primary user of this device.

## Get details and troubleshoot a device

This section guides you through some Copilot prompts that you can use.

1. Sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices**, and then select any device.
3. Select **Explore with Copilot**:

    :::image type="content" source="./media/copilot-devices/explore-with-copilot.png" alt-text="Screenshot that shows where you select a device and then select Explore with Copilot in Microsoft Intune or Intune admin center.":::

4. In Copilot, there are prompts for you to choose from. Select a prompt to get more information about the device.

Let's walk through some of the prompts.

### Summarize this device

Select the **Summarize this device** prompt:

:::image type="content" source="./media/copilot-devices/sample-prompts.png" alt-text="Screenshot that shows the Copilot sample prompts after you select a device in Microsoft Intune or Intune admin center.":::

The **Summarize this device** prompt shows more information about the device. The summary includes device-specific information, like the operating system, whether the device is registered in Microsoft Entra ID, malware counts, any noncompliant policies, group membership, and more.

Remember, these prompts and their results are within the scope of the device you select.

### Compare this device

When you use the **Compare this device with another device** prompt, you compare a working/healthy device with a non-working/unhealthy device. This comparison helps you identify the differences between the two devices and troubleshoot the nonworking device.

Select the prompt guide and select **Compare this device with another device**.

:::image type="content" source="./media/copilot-devices/prompt-guide.png" alt-text="Screenshot that shows the Copilot prompt guide after you select a device in Microsoft Intune or Intune admin center.":::

In the compare device prompt, enter another device name or Intune device ID to compare, select the comparison type > **Submit**:

:::image type="content" source="./media/copilot-devices/compare-devices-comparison-type.png" alt-text="Screenshot that shows the Copilot comparison prompt after you select a device in Microsoft Intune or Intune admin center.":::

The results show the differences and similarities between the two devices.

### Analyze an error code

Select the prompt guide and select > **Analyze an error code**.

This prompt can help you troubleshoot an error code that you see in Intune, including error codes from a device configuration profile, compliance policy, app installation, and more. The error doesn't have to be scoped to the device you select.

For example, enter `90` > **Submit**.

The results show the error code and a description of the error. The description includes the error type, the error message, and  more information about the error. This information can help you troubleshoot the error.

:::image type="content" source="./media/copilot-devices/analyze-error-example.png" alt-text="Screenshot that shows the Analyze an error code feature in Copilot after you select a device in Microsoft Intune or Intune admin center.":::

For a list of common errors in Intune, see [Common error codes and descriptions in Microsoft Intune](/troubleshoot/mem/intune/general/troubleshoot-company-resource-access-problems).

## Related articles

- [Microsoft Copilot in Intune](copilot-intune-overview.md)
- [Microsoft Copilot in Intune FAQ](copilot-intune-faq.md)
