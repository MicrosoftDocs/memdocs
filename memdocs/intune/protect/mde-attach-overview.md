---
# required metadata

title: Use Intune to manage Microsoft Defender for Endpoint on supported devices
description: Use Intune profiles to manage security settings for Microsoft Defender for Endpoint for devices that register in your Azure Active Directory. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/20/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata
 
#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattcall


---
<!-- Release branch: release-mde-integration. Draft and scope in progress. Place images in ./media/mde-attach-overview folder.  -->


# Use MDE-Attach to manage security with or without MDM enrollment

<!-- alternate title ideas?  Maybe:  # Manage Microsoft Defender for Endpoint on devices with or without MDM enrollment -->

When you use Microsoft Endpoint Manager (MEM) and Microsoft Defender for Endpoint (MDE) in the same Azure Active Directory (Azure AD) tenant, you can use the Microsoft Endpoint Manager to deploy security configurations of devices in your environment. This capability is known as *Security Management for Microsoft Defender for Endpoint*. With this functionality, devices receive security configurations directly from Endpoint Manager without requiring the device to be fully enrolled.

When devices are managed through this capability, endpoint security policies are sent directly to devices. Devices are targeted with policy using their Azure Active Directory device object, in the same way that all other Intune devices are targeted. Once policy is deployed to the device, the *Defender for Endpoint* components on the device enforce the policy. The device (through the Defender for Endpoint component) then reports the policy status, which is available in the Microsoft Endpoint Manager admin center.

<!-- Placeholder image follows :: Updated by MC on 10/06 -->
:::image type="content" source="./media/mde-overview/endpoint-security-overview.png" alt-text="Conceptual diagram of the MDE-Attach solution.":::

## Prerequisites

The security management functionality for Microsoft Defender for Endpoint clients has the following requirements:

- Microsoft Defender for Endpoint license
- The platform is in the list of supported platforms
- The devices meets the minimum requirements for the platform
- (Active Directory Devices) Hybrid Azure Active Directory join is configured
- The required endpoints are accessible from the endpoint


## Supported platforms

MDE-Attach policies are supported for the following device platforms:

- Windows 10 Professional/Enterprise (With KB999999)
- Windows 11 Professional/Enterprise (With KB999999)
- Windows Server 2012 R2 with Microsoft Defender for Down-Level Devices
- Windows Server 2019 with Microsoft Defender for Down-Level Devices
- Windows Server 2022 (with KB999999)

> [!TIP]
> Mobile devices (iOS/Android) that are not enrolled in Endpoint Manager can leverage Mobile Application Management for security configurations. Learn more on securing your corporate data with Mobile Application Management [here](Link to MAM Docs))

## Architecture
<!-- Placeholder image follows. Use of AAD and MEM for Azure AD and Microsoft Endpoint Manager must be fixed for use in docs -->
:::image type="content" source="./media/mde-overview/mde-architecture.png" alt-text="Conceptual representation of the MDE-Attach solution.":::

1. Blah
2. Blah
<!-- for Localization, the more text we can add outside the image, the better --> 

## Next steps

