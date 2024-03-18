---
# required metadata

title: Secure your corporate data using Microsoft Edge for Business
titleSuffix:
description: Secure your corporate data in Microsoft Intune with Microsoft Edge for Business.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/04/2024
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high

# optional metadata

#audience:
#ROBOTS: 
ms.reviewer: samarti
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier1
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Secure your corporate data in Intune with Microsoft Edge for Business

**Authors:**

Martinez, S., , Wu, I., Emerson, D., Turner, R., Lin, C., Askilsrud, C., Southgate, R., Kunze, C., Osorio, C., Poehlman, J., Hamilton, A.

**Applies to:**
- Mobile App Management (MAM) 
- Microsoft Edge for Business

This content is a guide that provides valuable insights into secure enterprise browser configuration and implementation related to Mobile App Management and Microsoft Edge for Business.

## Target Audience

The target audience for this content primarily includes:

- **Intune Administrators:** This content provides detailed guidance about configuring and managing Microsoft Edge for Business in Microsoft Intune.
- **Security Professionals:** This content focus on security related areas, such as the [data protection framework using app protection policies](../apps/app-protection-framework.md), [app configuration policies](../apps/app-configuration-policies-overview.md), data encryption, and [conditional access policies](../apps/app-protection-framework.md#conditional-access-policies). This content is also beneficial for security professionals looking to enhance their organization's security posture.
- **Decision Makers:** This content can help decision makers understand the security, productivity, and manageability benefits of Microsoft Edge for Business. In addition,this content will help decision makers make informed decisions about browser choice for their organization.

> [!NOTE]
> This content is designed to empower and encourage you to leverage the full potential of Microsoft Edge for Business and Microsoft Application Management.

## Overview

This guide provides the following content:

1. **Understanding Microsoft Edge for Business** - This content explains what Microsoft Edge for Business and Microsoft Application Management is, its importance in today's digital landscape, and how it can be used to protect your organization from various cyber threats.
2. **Creating Microsoft Edge for Business Mobile Application Management for Windows Policy** - This content guides you when implementing an App Protection policy for Windows, ensuring secure access and usage of enterprise applications.
3. **Mobile Application Management for Mobile Policy** - This content covers the creation of an App Protection policy for mobile devices, which is crucial in an era where mobile devices are extensively used for business purposes.
4. **Microsoft Entra Conditional Access Policy** - This content shows how to create a conditional access policy, which is a critical aspect of modern security frameworks. It helps control who or what can access your business data under specific conditions.
5. **End User Experience** - This content provides insights into the end user experience, helping you understand how security measures impact the user interaction with the system.
6. **Windows Security Center Integration** - This content explains how the secure enterprise browser integrates with the Windows Security Center, enhancing the overall security posture of your organization.

For more information about Microsoft Edge Security content, see [Microsoft Edge for Business: AI and protection in one secure enterprise browser](https://aka.ms/EdgeSecuritywhitepaper).

### What is Microsoft Edge for Business?

Microsoft Edge for Business is secure by default. It provides a dedicated Microsoft Edge experience built for work. It enables admins in organizations to give their users a productive and secure work-browser across managed and unmanaged devices. In addition, Microsoft Edge for Business has the same rich set of enterprise controls, security, and productivity features that you're already familiar with in Microsoft Edge, but it's built to help meet the evolving needs of businesses and organizations.

Microsoft Edge for Business aims to address the needs of both end users and IT Pros by automatically separating work and personal browsing. Microsoft Edge for Business does this using dedicated browser windows with their own favorites, separate caches, and storage locations. This separation ensures that work related content doesn't get intermingled with personal browsing. In addition, it helps to prevent cognitive overload where end users accidentally share sensitive information with unintended audiences. 

> [!NOTE]
> When Microsoft Edge for Business is gnerally available, it would act as the standard browser experience for organizations, activated by a Microsoft Entra entity (formerly Azure Active Directory) sign in. For more information, see the [build announcement](https://blogs.windows.com/msedgedev/2023/05/23/microsoft-edge-build-2023-innovations-in-AI-productivity-management-sidebar-apps/#business). 

### Is this a new browser?

No, this isn't a new browser. This is a new, dedicated Microsoft Edge experience built for work that enables organizations to configure it to maximize productivity and security. It has the same functionality that you're already familiar with in Microsoft Edge plus the optional automatic switching built to help meet the evolving needs of users and businesses. Signing in with Microsoft Entra will automatically enable Microsoft Edge for Business.  

### Benefits

Microsoft Edge for Business has several benefits. For IT, Microsoft Edge for Business can reduce the cyber-attack surface area and heighten your organization's security posture because it can streamline down to one browser for all use cases. For end users who are signed in with work and personal profiles, Microsoft Edge for Business can provide a better browsing experience with automatic switching, which has security and privacy benefits.

- **Work Browser (Visual Refresh):** The Microsoft Edge for Business icon replaces the existing Microsoft Edge icon in the taskbar and other shortcuts:

    :::image type="content" alt-text="Work Browser (Visual Refresh)" source="./media/securing-data-edge-for-business/securing_data_edge_for_business0.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business0.png":::

- **Enhanced Security:** By using app protection policies, Microsoft Edge for Business ensures a more secure and protected browsing experience by ensuring enterprise data remain secured.

- **Centralized Management:** Microsoft Intune provides a management experience that simplifies the process of managing a Microsoft Edge for Business policy experience.

In addition to the above benefits, you can enable protected Mobile Application Management access to org data on personal devices. This capability uses the following functionality:
- Intune application configuration policies to customize the org user experience.
- Intune application protection policies to secure org data and ensure the client device is healthy.
- Windows Security Center client threat defense integrated with Intune APP to detect local health threats on personal Windows devices.
- Microsoft Entra Conditional Access to ensure the device is protected and healthy before granting protected services access via Microsoft Entra.

## Zero Trust Methodology

The Zero Trust methodology aims to bring a new way of thinking to how an organization should approach security and is increasingly becoming the standard for security strategy. Prior best practices revolved around the model of "trust but verify," however attacks in today's landscape can take advantage of the trust inherent in that model, driving a need for change in tackling this challenge. As a result, organizations are changing their security strategy to align with three principles based on the concept of "never trust, always verify":

**Verify explicitly** - Always authenticate and authorize based on all available data points, including user identity, location, device health, service or workload, data classification, and anomalies.

**Use least-privilege access** - Limiting user access via just-in-time and just-enough-access (JIT/JEA), risk-based adaptive policies, and data protection to help secure both data and productivity.

**Assume breach** - Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses.

#### Complements Zero Trust

Microsoft Edge for Business is built with Chromium, giving it the well-engineered and tested security architecture design at its foundation. Because of this foundation, Microsoft Edge releases security updates and patches quickly to help stay ahead of security threats, such as zero-day exploits, to minimize the impact of compromise. Additionally, Microsoft Edge is built with its own unique protection features on top of Chromium and supports the following technologies:
- Microsoft Security solutions from Microsoft Defender
- Microsoft Entra (formerly known as Azure Active Directory)
- Microsoft Intune
- Microsoft Purview
 
Microsoft Edge for Business offers the following features that support the Zero Trust methodology:
- Microsoft Purview Data Loss Prevention (DLP)
- Microsoft Defender SmartScreen
- Enhanced security mode (ESM)
- Website typo protection
- Native support for Microsoft Entra Conditional Access
- Password Monitoring and Generator
- Microsoft Edge management service (EMS)
- Unmanaged device support with Microsoft Intune Mobile Application Management

