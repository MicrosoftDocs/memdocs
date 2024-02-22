---
# required metadata

title: Copilot in Intune shows device information and errors
description: Microsoft Copilot in Intune can help you get information about your devices, compare devices, and get error information. Use this information to help you manage and troubleshoot device issues.
keywords: security copilot, intune, microsoft intune, copilot, device information, device errors, device troubleshooting
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/20/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

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
---

# Use Microsoft Copilot for Security to troubleshoot devices in Microsoft Intune

> [!WARNING]
> This article is being written.

This feature is in [public preview](public-preview.md).

Microsoft Copilot for Security is a generative-AI security analysis tool that can help your organization get information quickly. Copilot is built into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and is available to help troubleshoot your devices.

With Copilot in Intune, you can:

- Get more information about a specific device, including installed apps, group membership, and more.
- Compare devices to see the similarities and differences between them, like the compliance policies, hardware, and device configurations assigned to both devices.
- Enter an error code to get more about information about the error and how to resolve it.

This article describes how to use Copilot to manage and troubleshoot device issues in Intune.

## Before you begin

- Copilot in Intune is licensed and managed with Microsoft Copilot for Security. To use Copilot in Intune, make sure your organization completed the setup steps for Copilot for Security.

  For more information, go to:

  - [Microsoft Copilot in Intune](../fundamentals/copilot-intune-overview.md#prerequisites)
  - [Get started with Microsoft Copilot](/security-copilot/get-started-security-copilot)

- When you use this Copilot feature for your devices, you are in the scope of the device you select.

## Devices embedded



1. Sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices** > Select any device.
3. Select **Copilot** and choose **Explore device** from the drop-down list:

    :::image type="content" source="./media/copilot-intune-overview/copilot-select-device.png" alt-text="Screenshot that shows selecting any device and then select Copilot in Microsoft Intune and Intune admin center.":::

4. In Copilot, there are existing prompts for you to choose from. Select a prompt to get more information about the device. For example, select **Summarize device**:

    INSERT SCREENSHOT

    The summary shows policies assigned, the primary user of the device, a list of installed apps, and more.

    Remember, these prompts and their results are in the scope of the device you select.

5. Select **Copilot** again and choose **Compare device** from the drop-down list:

    INSERT SCREENSHOT

    In the compare device prompt, enter another device ID or device name to compare. The results show the differences and similarities between the two devices.

    INSERT SCREENSHOT of an example of the results

    With **Compare device**, you can compare a working/healthy device with a non-working/unhealthy device. This comparison can help you identify the differences between the two devices and troubleshoot the non-working device.

6. Select **Copilot** again and choose **Ask about errors** from the drop-down list:

    INSERT SCREENSHOT

## Available prompts

In Copilot, there are existing prompts that guide you to get more information about the device. The guided prompts include:

- compare two devices: with compare, user enters device to compare with
- analyze an error code
- summarize device
- show device policies
- who is the device's primary user
- show applications
- show me app install failure
- show group membership


these are already docs in original article
need to move this info to new article:

starter prompts show, no input box
user must select an existing prompt

analyze error code shows input box. user enters error code.

behind the scenes, intune writes the prompt for the user, and submits to copilot. 

## Related articles

