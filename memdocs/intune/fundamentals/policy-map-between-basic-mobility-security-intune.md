---
# required metadata

title: Policy mapping between Basic Mobility and Security and Intune
titleSuffix: Microsoft Intune
description: An overview of the policy map between Basic Mobility and Security and Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 12/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high


# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection:
- tier2
- M365-identity-device-management
- retire
---

# Policy mapping between Basic Mobility and Security and Intune

Both Basic Mobility and Security, formerly Microsoft 365 mobile device management (MDM), and Intune are used to manage mobile devices. Part of this management includes the application of various policies that determine how the mobile devices interact with your company data and security.

If you choose to migrate your MDM from Basic Mobility and Security to Intune, you’ll need to duplicate the policies over to Intune. You can use the [Migration evaluation tool](migrate-to-intune.md) to handle the migration. You can also use the articles in this section to understand the two systems’ policies and how they map to each other.

Depending on the Basic Mobility and Security policy settings, different Intune and Azure AD policies may be needed to duplicate the behavior. Because Intune offers more flexibility, each source policy can translate into multiple Intune and Azure Active Directory (Azure AD) policies to achieve the same effect. Each device security policy can require up to three compliance policies, six configuration profiles, and five global conditional access policies.

## Basic Mobility and Security policies in Office 365 Security and Compliance portal

Basic Mobility and Security uses the Office 365 Security and Compliance portal to manage [device security policies](/microsoft-365/admin/basic-mobility-security/set-up#step-4-recommended-manage-device-security-policies).

## Intune policies in the Microsoft Intune admin center

Intune uses the Microsoft Intune admin center to manage the following policies to achieve similar results as the Office device security policies:

| Intune policy type | Purpose | Intune location |
| --- | --- | --- |
| [Compliance policies](../protect/device-compliance-get-started.md) | Specify the device settings as access requirements. | [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Compliance policies** |
| [Configuration profiles](../configuration/device-profiles.md) | Specify other settings that aren’t part of the access requirements, including email profiles. | [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Configuration profiles** |
| [Conditional access policies]( ../protect/conditional-access.md)| Azure AD conditional access blocks access if the settings aren't compliant. | [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Endpoint security** > **Conditional access** > **Classic policies** |

Intune and Azure AD policies are more powerful than Office MDM policies and have many more settings to achieve more advanced scenarios. Before you change Intune or Azure AD policies not mentioned in these articles, you should first read the relevant Intune or Azure AD documentation.

## Next steps

- [Access requirements policy mapping from Basic Mobility and Security to Intune](policy-map-access-requirements.md)
- [Configurations policy mapping from Basic Mobility and Security to Intune](policy-map-configurations.md)
- [Miscellaneous policy mapping from Basic Mobility and Security to Intune](policy-map-miscellaneous.md)
 