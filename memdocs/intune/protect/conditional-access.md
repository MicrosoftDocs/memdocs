---
# required metadata

title: Use Conditional Access with Microsoft Intune compliance policies
titleSuffix: Microsoft Intune
description: Combine Conditional Access with Intune compliance policies to define the requirements that users and devices must meet before gaining access your organizations resources. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby    
ms.date: 04/14/2022
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: a1973f38-ea55-43eb-a151-505fb34a8afb

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Learn about Conditional Access and Intune

Use Conditional Access with Microsoft Intune compliance policies to control the devices and apps that can connect to your email and company resources. When integrated, you can gate access to keep your corporate data secure, while giving users an experience that allows them to do their best work from any device, and from any location.

[Conditional Access](/azure/active-directory/conditional-access/overview) is an Azure Active Directory capability that is included with an Azure Active Directory Premium license. Through Azure Active Directory, Conditional Access brings signals together to make decisions, and enforce organizational policies. Intune enhances this capability by adding mobile device compliance and mobile app management data to the solution. Common signals include:

- User or group membership.
- IP location information.
- Device details, including device compliance or configuration status.
- Application details, including requiring use of managed apps to access corporate data.
- Real-time and calculated risk detection, when you also use a mobile threat defense partner.

:::image type="content" source="./media/conditional-access/ca-diagram-1.png" alt-text="Conceptual Conditional Access process flow.":::

> [!NOTE]
> Conditional Access also extends its capabilities to [Microsoft 365 services](/office365/enterprise/office-365-client-support-conditional-access).

## Ways to use Conditional Access with Intune

Conditional Access works with Intune device configuration and compliance policies, and with Intune Application protection policies.  

- **Device-based Conditional Access**

  Intune and Azure Active Directory work together to make sure only managed and compliant devices can access email, Microsoft 365 services, Software as a service (SaaS) apps, and on-premises apps. Additionally, you can set a policy in Azure Active Directory to enable only domain-joined computers or mobile devices that have enrolled in Intune to access Microsoft 365 services.  Including:

  - Conditional Access based on network access control

  - Conditional Access based on device risk

  - Conditional Access for Windows PCs. Both corporate-owned and bring your own device (BYOD).

  - Conditional Access for Exchange on-premises

  Learn more about [device-based Conditional Access with Intune](../protect/create-conditional-access-intune.md)

- **App-based Conditional Access**

  Intune and Azure Active Directory work together to make sure only managed apps can access corporate e-mail or other Microsoft 365 services.

  Learn more about [app-based Conditional Access with Intune](../protect/app-based-conditional-access-intune.md).

## Next steps

[Common ways to use Conditional Access with Intune](../protect/conditional-access-intune-common-ways-use.md)