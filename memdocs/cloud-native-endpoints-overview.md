---
# required metadata

title: What are cloud native Windows endpoints 
titleSuffix: Microsoft Endpoint Manager
description: Learn more about cloud native endpoints and what they are. See a list of benefits, and the impact on end users and IT administrators. Cloud native endpoints help with remote workers and hybrid workers.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 03/29/2022
ms.topic: conceptual
ms.service: mem
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
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
---

# Get started with cloud native endpoints and Microsoft Endpoint Manager

Organizations are focusing on supporting remote or hybrid workers. Many organizations want to:

- Ship devices directly to users.
- Automatically configure apps and settings on devices using an internet connection.
- Have users reset their devices and redeploy apps without losing data.
- Allow users to be productive from anywhere, while protecting and securing user and organization data.

## What are cloud native endpoints

Cloud native endpoints are devices that can be deployed from anywhere. They receive their applications and configurations dynamically from the cloud, and can easily be reset or restored.

A cloud native endpoint doesn't necessarily live exclusively in the cloud. Instead, any endpoint that's cloud native eliminates hard dependencies to on-premises connectivity and on-premises resources.

These endpoints can be located anywhere that has internet access. They can also be physical devices or virtual machines.

From a technical perspective, cloud native endpoints are Windows devices that are deployed using [Windows Autopilot](/mem/autopilot/windows-autopilot), joined to Azure Active Directory ([Azure AD joined](/azure/active-directory/devices/concept-azure-ad-join)), and are automatically enrolled in a Mobile Device Management (MDM) solution, like [Microsoft Endpoint Manager](/mem/endpoint-manager-overview).

A cloud native endpoint has the following characteristics:

- Provisioned and managed from cloud-based services
- Can use and access other cloud-based endpoints from anywhere
- Azure Active Directory (AD) joined
- Includes configuration, data, and applications that are portable and roam with the user
- Doesn't generally require a direct connection to any on-premises resources for usability or management

For end users, they only need an internet connection. Their data and critical settings can be automatically preserved and restored using [Enterprise State Roaming](/azure/active-directory/devices/enterprise-state-roaming-faqs), or similar solutions. If end users experience issues during deployment or at any time, then they can reset and reprovision the device without contacting support.

Microsoft recommends customers focus on adopting cloud native endpoints.

In this article, **Azure AD joined** and **cloud native endpoints** are used interchangeably.

## Benefits for users and IT

Cloud native endpoints provide many benefits to end users and IT:

- **Best for remote workers**

  End users don't worry about connecting to the VPN or other networks. They sign in to devices from anywhere, and run actions, like password reset, without connecting to on-premises Active Directory.

  Azure AD joined (also known as AADJ) endpoints do the initial sign in using an internet connection. The Azure AD joined sign in process doesn't use on-premises domain controller connectivity, and is faster than a traditional domain-based sign in.

  Traditional domain joined PCs require connectivity to domain controllers for initial sign in.

- **Deploy from anywhere**

  To deploy new devices, administrators can be anywhere with an internet connection. You can provision or reset devices, and have the devices ready much quicker than traditional provisioning, possibly in minutes. The reliance on on-premises resources is reduced, which simplifies the endpoint requirements and endpoint management.

- **Simplified management for all platforms**

  Users and administrators get a unified management experience for all platforms, including Android, iOS/iPadOS, macOS, and Windows. With Endpoint Manager, you can manage mobile and non-mobile devices and operating systems. You don't need to rely on complex group policy management.

- **Provide a secure Single-Sign-On (SSO) experience to cloud and on-premises apps**

  Cloud native endpoints include native single sign-on (SSO) for cloud and [on-premises resources](/azure/active-directory/devices/azuread-join-sso), such as file servers, print servers, and web applications.

- **Secure access without passwords**

  With [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-overview), end users can sign in to their device, and access resources without passwords.

- **Seamless experience for documents, settings, and preferences**

  With [One Drive for Business](/onedrive/), end users automatically gain access to their documents, can restore any previous Office and Windows settings, and avoid spending time recovering data.

  For example, you can store the following user data on One Drive for Business:

  - Windows wallpaper
  - Automatic sync of documents and desktop files to OneDrive
  - Office settings
  - Outlook email signatures
  - Microsoft Edge settings

  When user data is stored on One Drive for Business, it can synchronize the data with all user endpoints.

## How to get started

- **Plan**: In adopting cloud native endpoints, organizations focus on several key areas:

  - Review your existing workloads for modernization, and determine the next steps to support cloud native.
  - Be prepared to change operational processes and procedures.
  - Get your end users ready for change.

  For more specific information, see the [High level planning guide to move to cloud native endpoints](cloud-native-endpoints-planning-guide.md).

- **Create a Proof of Concept**: Do an initial proof of concept (POC) using a lab environment. The goal is to understand changes and their impact.

  As part of the POC, identify a set of users and devices to run a production pilot. In many organizations, there's a role or business group that will be easier to migrate.

  For example, target the following scenarios for migration to cloud management:

  - Highly mobile sales team whose primary requirements are productivity tools and an online customer relationship management solution
  - Knowledge workers who primarily access content that’s already in the cloud and rely heavily on Microsoft 365 apps
  - Frontline worker devices that are highly mobile, or are in environments where they don't have access to the organization network

  For these groups, use the [high level planning guide](cloud-native-endpoints-planning-guide.md) to review their workloads. Determine how these workloads can move to modern management, including identity, software distribution, device management, and more. For each of the areas in your pilot, the number of items or tasks should be low.

  This initial pilot helps you develop the processes and procedures required for more groups. It also helps develop your long term strategy.

## Next steps

- [Tutorial: Get started with cloud native Windows endpoints with Microsoft Endpoint Manager](cloud-native-windows-endpoints.md)
- [Azure AD joined vs. Hybrid Azure AD joined](azure-ad-joined-hybrid-azure-ad-joined.md)
- [Cloud native endpoints and on-premises resources](cloud-native-endpoints-on-premises.md)
- [High level planning guide to move to cloud native endpoints](cloud-native-endpoints-planning-guide.md)
- [Known issues](cloud-native-endpoints-known-issues.md)
