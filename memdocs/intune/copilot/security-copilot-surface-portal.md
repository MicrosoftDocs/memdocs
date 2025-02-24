---
# required metadata

title: Security Copilot in Microsoft Surface Management Portal
description: You can use Security Copilot to help you manage and monitor Surface devices at scale.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/18/2025
ms.topic: concept-article
ms.service: microsoft-intune
ms.subservice:
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: zadvor
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

# Security Copilot in Microsoft Surface Management Portal (Public Preview)

Microsoft Security Copilot is a cloud-based AI platform that provides a natural language Copilot experience that can be used to provide information and resolve issues. [Surface Management Portal](/surface/surface-management-portal) provides a centralized platform to manage and monitor Surface devices at scale. Surface Management Portal integration with Microsoft Copilot for Security helps Surface device administrators be more efficient, and resolve hardware issues faster and at scale. 

Copilot for Surface Management Portal provides visibility into your environment's warranty coverage landscape, and end-of-servicing timelines. Additionally, it offers insights into various aspects of device management, including compliance policies, malware protection, and other threats to reduce risks.

## Know before you begin

If you're new to Security Copilot, you should familiarize yourself with it by reading these articles:

- [What is Microsoft Security Copilot?](/copilot/security/microsoft-security-copilot)
- [Microsoft Security Copilot experiences](/copilot/security/experiences-security-copilot)
- [Get started with Microsoft Security Copilot](/copilot/security/get-started-security-copilot)
- [Understand authentication in Microsoft Security Copilot](/copilot/security/authentication)
- [Prompting in Microsoft Security Copilot](/copilot/security/prompting-security-copilot)

## Security Copilot integration in Microsoft Surface Management Portal

If you use [Microsoft Surface Management Portal](/surface/surface-management-portal) in the same tenant as Security Copilot, then you can use Security Copilot to get insights from your Surface Management Portal data.

There are Surface Management Portal capabilities built into Security Copilot, and you can use prompts to get more information, including:

- Information about your device fleet, including summary on warranties, and end of service and support.
-	Details about issues with specific devices, so you can troubleshoot more quickly and easily.
-	Information to help you learn about safeguarding and improving the lifetime of your Surface devices.

This article shows you how to access your [Microsoft Surface Management Portal data in Security Copilot](#enable-the-security-copilot-integration-in-surface-management-portal).

## Key features

Copilot for Surface Management Portal brings the capabilities of Security Copilot to the Microsoft Surface Management Portal admin center, enabling you to respond to Surface device issues and escalations quickly. Bringing AI to Surface Management Portal allows teams to immediately understand warranty coverage of their device fleet and determine remediation steps in a timely manner. As an administrator, you can compare the latest Surface for Business devices with their current Surface devices. You can also learn more about protecting your organizations devices from malware and other threats, so that you can reduce risks.

:::image type="content" source="./media/security-copilot-surface-portal/surface-management-portal-01.png" lightbox="./media/security-copilot-surface-portal/surface-management-portal-01.png" alt-text="Screenshot that shows Copilot in the Surface Management Portal.":::

## Enable the Security Copilot Integration in Surface Management Portal

Copilot for Surface Management Portal is included with Security Copilot. There aren't any other licensing requirements needed to use Copilot for Surface Management Portal. Ensure that you have provisioned sufficient **security compute units** to leverage this capability. For more information, see [Get started with Microsoft Security Copilot](/copilot/security/get-started-security-copilot) and [Manage usage of security compute units in Security Copilot](/copilot/security/manage-usage).

Enable integration of Security Copilot:

1. Sign in to the [Security Copilot portal](https://go.microsoft.com/fwlink/?linkid=2247989).
2. In the prompt bar, select **Sources** at the right corner.

    :::image type="content" source="./media/security-copilot-surface-portal/surface-management-portal-02.png" alt-text="Screenshot that shows the Sources icon.":::

3. In **Manage Sources**, activate the **Surface Management Portal** plugin.

    :::image type="content" source="./media/security-copilot-surface-portal/surface-management-portal-03.png" alt-text="Screenshot that shows the select for **Surface Management Portal** plugin.":::

4. Close the plugin pane.

> [!NOTE]
> Only certain roles can enable or disable plugins. For more information, see [Manage plugins in Microsoft Security Copilot](/copilot/security/manage-plugins?tabs=securitycopilotplugin).

## Sample Surface Management Portal prompts

Once you have set up Security Copilot, you can start using Copilot for Surface Management Portal by selecting one of the available prompts.

**Sample prompts**:
- Troubleshoot Surface devices.
- List all my Surface device models' end of service date.
- Compare technical specifications of two Surface devices.
- Generate a warranty coverage report for all devices.
- What are the best practices for protecting Surface devices?

> [!NOTE]
> These capabilities are available for public preview.

## Provide feedback

Your feedback is vital to guide the current and planned development of the product. The best way to provide feedback is to use the feedback buttons at the bottom of each completed prompt, directly within the product.

:::image type="content" source="./media/security-copilot-surface-portal/surface-management-portal-04.png" alt-text="Screenshot that shows the Feeback prompt.":::

## Privacy and data security in Security Copilot

To understand how Security Copilot handles your prompts and the output data that it retrieves from the service, see [Privacy and data security in Microsoft Security Copilot](/copilot/security/privacy-data-security).

## Responsible AI FAQ in Microsoft Security Copilot

At Microsoft, we take our commitment to responsible AI seriously. Security Copilot is being developed in accordance with our [AI principles](https://go.microsoft.com/fwlink/?linkid=2304711). To learn more about how Microsoft approaches responsible AI for Security Copilot, see [Responsible AI FAQ](/copilot/security/rai-faqs-security-copilot?source=recommendations).