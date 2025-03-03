---
# required metadata

title: What are cloud-native Windows endpoints
titleSuffix: Microsoft Intune
description: Learn more about cloud-native endpoints and what they are. See a list of benefits, and the effect on end users and IT administrators. Cloud-native endpoints help with remote workers and hybrid workers, and use Microsoft Intune to manage devices.
keywords:
author: MandiOhlinger

ms.author: mandia
manager: dougeby
ms.date: 05/30/2024
ms.topic: article
ms.service: microsoft-intune
ms.subservice:
ms.localizationpriority: high
ms.assetid:
# optional metadata

#audience:
#ms.devlang:
ms.reviewer: ahamil, jasandys, wicale
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - intune-scenario
---

# Learn more about cloud-native endpoints

> [!TIP]
> [!INCLUDE [cloud-native-endpoints-definitions](../../includes/cloud-native-endpoints-definitions.md)]

Organizations are focusing on supporting remote and hybrid workers. With cloud-native endpoints, organizations can:

- Ship devices directly to users.
- Automatically configure apps and settings on devices using an internet connection.
- Have users reset their devices and redeploy apps without losing data.
- Allow users to be productive from anywhere, while protecting and securing user and organization data.

In this set of articles, you will:

- ✅ **Learn about cloud-native endpoints** and the benefits to organizations and end users (this article).

- ✅ **Step through a tutorial** that creates a Windows device that's cloud-native:

  - [Tutorial: Get started with cloud-native Windows endpoints with Microsoft Intune](cloud-native-windows-endpoints.md)

- ✅ **Learn more about the Microsoft Entra concepts** that are part of cloud-native endpoints, including accessing on-premises resources:

  - [Entra joined vs. Hybrid Entra joined](azure-ad-joined-hybrid-azure-ad-joined.md)
  - [Cloud-native endpoints and on-premises resources](cloud-native-endpoints-on-premises.md)

- ✅ **Get guidance and advice** on moving your workloads and your organization to become cloud-native:

  - [High level planning guide to move to cloud-native endpoints](cloud-native-endpoints-planning-guide.md)

- ✅ **Read about some scenarios** that can affect your cloud-native migration:

  - [Known issues and important information](cloud-native-endpoints-known-issues.md)

## What are cloud-native endpoints

Cloud-native endpoints are devices that can be deployed from anywhere. They receive their applications and configurations dynamically from the cloud, and can easily be reset or restored.

A cloud-native endpoint doesn't necessarily live exclusively in the cloud. Instead, any endpoint that's cloud-native eliminates hard dependencies to on-premises connectivity and on-premises resources.

These endpoints can be located anywhere that has internet access. They can also be physical devices or virtual machines.

From a technical perspective, cloud-native endpoints are Windows devices that are deployed using [Windows Autopilot](/autopilot/overview), joined to Microsoft Entra ([Microsoft Entra joined devices](/entra/identity/devices/concept-directory-join)), and are automatically enrolled in a Mobile Device Management (MDM) solution, like [Microsoft Intune](../../intune-service/fundamentals/what-is-intune.md).

A cloud-native endpoint has the following characteristics:

- Provisioned and managed from cloud-based services
- Can use and access other cloud-based endpoints from anywhere
- Microsoft Entra joined
- Includes configuration, data, and applications that are portable and roam with the user
- Doesn't generally require a direct connection to any on-premises resources for usability or management

For end users, they only need an internet connection. Their data and critical settings can be automatically preserved and restored using [Enterprise State Roaming](/entra/identity/devices/enterprise-state-roaming-faqs), or similar solutions. If end users experience issues during deployment or at any time, then they can reset and reprovision the device without contacting support.

Microsoft recommends that organizations focus on adopting cloud-native endpoints.

## Benefits for users and IT

Cloud-native endpoints provide many benefits to end users and IT:

- **Best for remote workers**

  End users don't worry about connecting to the VPN or other networks. They sign in to devices from anywhere, and run actions, like password reset, without connecting to on-premises AD.

  Microsoft Entra joined endpoints do the initial sign-in using an internet connection. The Microsoft Entra joined sign-in process doesn't use an on-premises domain controller for connectivity, and is faster than a traditional domain-based sign-in.

  Traditional domain joined PCs require connectivity to domain controllers for initial sign-in.

- **Deploy from anywhere**

  To deploy new devices, administrators can be anywhere with an internet connection. You can provision or reset devices, and have the devices ready quicker than traditional provisioning, possibly in minutes. The reliance on on-premises resources is reduced, which simplifies the endpoint requirements and endpoint management.

- **Simplified management for all platforms**

  Users and administrators get a unified management experience for all platforms, including Android, iOS/iPadOS, macOS, and Windows. With Intune, you can manage mobile and non-mobile devices and operating systems. You don't need to rely on complex group policy management.

- **Provide a secure Single-Sign-On (SSO) experience to cloud and on-premises apps**

  Cloud-native endpoints include native single sign-on (SSO) for cloud and [on-premises resources](/entra/identity/devices/device-sso-to-on-premises-resources), such as file servers, print servers, and web applications.

- **Secure access without passwords**

  With [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-overview), end users can sign in to their device, and access resources without passwords.

  For more specific information, go to [Password-less Strategy](/windows/security/identity-protection/hello-for-business/passwordless-strategy).

- **Seamless experience for documents, settings, and preferences**

  With [OneDrive](/onedrive/plan-onedrive-enterprise), end users automatically gain access to their documents, can restore any previous Office and Windows settings, and avoid spending time recovering data.

  For example, you can store the following user data on OneDrive:

  - Windows wallpaper
  - Automatic sync of documents and desktop files to OneDrive
  - Office settings
  - Outlook email signatures
  - Microsoft Edge settings

  When user data is stored on OneDrive, it can synchronize the data with all user endpoints.

## How to get started

The [High level planning guide to move to cloud-native endpoints](cloud-native-endpoints-planning-guide.md) is a good resource. It covers the following areas:

- **Plan**: When ready to move to cloud-native endpoints, organizations focus on several key areas:

  - Review your existing workloads for modernization, and determine the next steps to support cloud-native.
  - Be prepared to change operational processes and procedures.
  - Get your end users ready for change.

  For more specific information, go to the [High level planning guide to move to cloud-native endpoints](cloud-native-endpoints-planning-guide.md).

- **Create a Proof of Concept**: Do an initial proof of concept (POC). The goal is to understand changes and their impact.

  For more specific information, go to the [High level planning guide to move to cloud-native endpoints](cloud-native-endpoints-planning-guide.md).

## Follow the cloud-native endpoints guidance

1. 🡺 **Overview: What are cloud-native endpoints?** (*You are here*)
2. [Tutorial: Get started with cloud-native Windows endpoints](cloud-native-windows-endpoints.md)
3. [Concept: Entra joined vs. Hybrid Entra joined](azure-ad-joined-hybrid-azure-ad-joined.md)
4. [Concept: Cloud-native endpoints and on-premises resources](cloud-native-endpoints-on-premises.md)
5. [High level planning guide](cloud-native-endpoints-planning-guide.md)
6. [Known issues and important information](cloud-native-endpoints-known-issues.md)