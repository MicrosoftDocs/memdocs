---
# required metadata

title: Use Intune to manage Microsoft Defender for Endpoint on supported devices
description: Use Intune profiles to manage security settings for Microsoft Defender for Endpoint for devices that register in your Azure Active Directory. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 9/26/2021
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

When you use Microsoft Intune and Microsoft Defender for Endpoint (MDE) in the same Azure Active Directory (Azure AD) tenant, you can use the Microsoft Endpoint Manager admin center to manage and report on the MDE configurations of devices in your environment. This capability is known as *MDE-Attach*. With MDE-Attach, you manage the settings for Microsoft Defender for Endpoint directly on devices, and not the device itself.

To manage a device through MDE-Attach, the Intune policies for MDE settings are sent directly to devices through their Azure AD membership. On each device, it’s the MDE Sense agent that reads the policy and then configures security settings. The agent then reports on the device status, which is available in the Microsoft Endpoint Manager admin center.

<!-- Placeholder image follows -->
:::image type="content" source="./media/mde-attach-overview/endpoint-security-overview.png" alt-text="Conceptual diagram of the MDE-Attach solution.":::

Because the MDE Sense agent receives and acts on the policy, the MDE-Attach solutions primary requirements are:

- You have subscriptions for both Intune and Microsoft Defender for Endpoint
- Supported devices run the MDE agent
- Devices register in the same Azure AD environment as your Intune and Defender subscriptions

That's it! Your devices don't need to enroll with Intune or Configuration manager. Instead, they can enroll with a third-party MDM, or not enroll with any MDM service.

## Supported platforms

MDE-Attach policies are supported for the following device platforms:

- Linux
- macOS
- Windows 10
- Windows 11
- Windows Server

> [!TIP]
> Support for MDE on devices that run Android and iOS/iPadOS are not supported through MDM-Attach but remain supported through existing solutions like mobile application management.

## How MDE-Attach works

With a subscription for both Intune and MDE in the same Azure AD environment, you can use MDE-Attach. When you use MDE-Attach, Microsoft Endpoint Manager becomes the umbrella for policy management and reporting on your devices that use MDE for security.

## Architecture
<!-- Placeholder image follows. Use of AAD and MEM for Azure AD and Microsoft Endpoint Manager must be fixed for use in docs -->
:::image type="content" source="./media/mde-attach-overview/pending-mde-attach-architecture.png" alt-text="Conceptual representation of the MDE-Attach solution.":::

1. Blah
2. Blah
<!-- for Localization, the more text we can add outside the image, the better --> 

## Next steps

