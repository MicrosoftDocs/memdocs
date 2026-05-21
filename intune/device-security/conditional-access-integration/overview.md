---
title: Use Conditional Access with Microsoft Intune compliance policies
description: Combine Conditional Access with Intune compliance policies to define the requirements that users and devices must meet before gaining access to your organization's resources.
ms.date: 04/25/2024
ms.topic: overview
ms.reviewer: ilwu
ms.collection:
- M365-identity-device-management
- conditional-access
- sub-device-compliance
---

# Learn about Conditional Access and Intune

Use Conditional Access with Microsoft Intune compliance policies to control the devices and apps that can connect to your email and company resources. When integrated, you can gate access to keep your corporate data secure, while giving users an experience that allows them to do their best work from any device, and from any location.

[Conditional Access](/entra/identity/conditional-access/overview) is a Microsoft Entra capability that is included with a Microsoft Entra ID P1 or P2 license. Through Microsoft Entra ID, Conditional Access brings signals together to make decisions, and enforce organizational policies. Intune enhances this capability by adding mobile device compliance and mobile app management data as signals for Conditional Access decisions. For a full list of supported signals, see [What is Conditional Access?](/entra/identity/conditional-access/overview) in the Microsoft Entra documentation.

You configure Conditional Access policies from the Microsoft Intune admin center. The Conditional Access node in the Microsoft Intune admin center is the same node as in Microsoft Entra ID, so you don't need to switch between them.

:::image type="content" source="./media/scenarios/ca-diagram-1.png" alt-text="Conceptual Conditional Access process flow.":::

> [!NOTE]
> Conditional Access also extends its capabilities to [Microsoft 365 services](/office365/enterprise/office-365-client-support-conditional-access).

## Ways to use Conditional Access with Intune

Conditional Access works with Intune device configuration and compliance policies, and with Intune app protection policies.

- **Device-based Conditional Access**

  Intune and Microsoft Entra ID work together to make sure only managed and compliant devices can access email, Microsoft 365 services, software as a service (SaaS) apps, and on-premises apps.

  Learn more about [device-based Conditional Access with Intune](./device-based-policies.md).

- **App-based Conditional Access**

  Intune and Microsoft Entra ID work together to make sure only managed apps can access corporate email or other Microsoft 365 services.

  Learn more about [app-based Conditional Access with Intune](./app-based-policies.md).

## Known limitations
The compliant network location condition is only supported for devices enrolled in mobile device management (MDM). If you configure a Conditional Access policy using the compliant network location condition, users with devices that aren't yet MDM-enrolled might be affected. Users on these devices might fail the Conditional Access policy check, and be blocked. Ensure that you exclude the affected users or devices when using the compliant network location condition.

## Next steps

[Common ways to use Conditional Access with Intune](./scenarios.md)
