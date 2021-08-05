---
# required metadata
title: Security overview for Windows 365
titleSuffix:
description: Learn about security for Windows 365
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/02/2021
ms.topic: overview
ms.service: cloudpc
ms.subservice: 
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Security guidelines

To help improve security for your Cloud PCs, consider the following general guidelines:

1. Configure multi-factor authentication (MFA) for device enrollment. For more information, see [Require MFA for Intune device enrollments](/mem/intune/enrollment/multi-factor-authentication).
2. Apply Conditional Access policies to control the devices and apps that can connect to your email and company resources. For more information, see [What is Conditional Access in Azure Active Directory?](/azure/active-directory/conditional-access/overview)
3. Use Microsoft Defender ATP to identify threats and set devices as non-compliant. You can easily connect Microsoft Defender ATP to Cloud PC devices, apply device compliance policies to Cloud PCs, and use Conditional Access to identify threats. For more information, see [Enforce compliance for Microsoft Defender ATP with Conditional Access in Intune](/mem/intune/protect/advanced-threat-protection).  
4. Use Intune compliance policies with Conditional Access policies for Cloud PCs. These policies help identify non-compliant devices and users so they can’t access corporate resources until the device risk level is lowered. For more information, see [Windows 10 compliance settings in Microsoft Intune](/mem/intune/protect/compliance-policy-create-windows). Windows health attestation settings cannot be validated on virtual machines including Cloud PCs.
5. One of the most important elements of device security is OS updates. These updates make sure that devices stay up-to-date and secure while delivering new features and defenses against vulnerabilities. For Cloud PCs, Endpoint Manager can be used by IT admins to configure Intune Windows 10 update rings and policies for Windows Update for Business. For more information, see [Manage Windows 10 software updates in Intune](/mem/intune/protect/windows-update-for-business-configure).  
6. Windows 365 integrates with Microsoft Defender for Endpoint. Security and endpoint admins can work together to manage their Cloud PC environment just like they manage a physical endpoint. If subscribed, Cloud PCs will:
    - Send data through to Microsoft 365 Secure Score.
    - Unhealthy PCs will show up on the Microsoft Defender for Endpoint Security Center and threat analysis dashboards.
    - Cloud PCs will respond to remediation measures just like other managed devices.

<!-- ########################## -->
## Next steps

[Deploy security baselines](deploy-security-baselines.md)
