---
# required metadata
title: Security overview for Windows 365
titleSuffix:
description: Learn about security for Windows 365
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 06/15/2023
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Security guidelines

To help improve security for your Cloud PCs, consider the following general guidelines:

1. Apply Conditional Access policies to control the devices and apps that can connect to your email and company resources. Use Conditional Access to secure access end user access to Windows 365.Specifically, considering using Microsoft Entra multifactor authentication to authenticate users. For more information, see [What is Conditional Access in Microsoft Entra ID?](/azure/active-directory/conditional-access/overview)
2. Use Microsoft Defender for Endpoint to identify threats and set devices as non-compliant. You can easily connect Microsoft Defender for Endpoint to Cloud PC devices, apply device compliance policies to Cloud PCs, and use Conditional Access to identify threats. For more information, see [Enforce compliance for Microsoft Defender for Endpoint with Conditional Access in Intune](/mem/intune/protect/advanced-threat-protection).  
3. Use Intune compliance policies with Conditional Access policies for Cloud PCs. These policies help identify non-compliant devices and users so they can’t access corporate resources until the device risk level is lowered. For more information, see [Windows 10/11 compliance settings in Microsoft Intune](/mem/intune/protect/compliance-policy-create-windows).

    >[!Note]
    >Cloud PCs don't support BitLocker. We recommend excluding this setting from compliance policies targeting Cloud PCs.

4. One of the most important elements of device security is OS updates. These updates make sure that devices stay up-to-date and secure while delivering new features and defenses against vulnerabilities. For Cloud PCs, Endpoint Manager can be used by IT admins to configure Intune Windows 10/11 update rings and policies for Windows Update for Business. For more information, see [Manage Windows 10/11 software updates in Intune](/mem/intune/protect/windows-update-for-business-configure).  
5. By default Windows 365 Enterprise, end users aren't administrators of their Cloud PCs. This policy aligns with Windows 10/11 security guidance. For more information about this guidance, see [Local Accounts](/windows/security/identity-protection/access-control/local-accounts#sec-restrict-protect-accounts) in the Windows documentation.
6. Windows 365 integrates with Microsoft Defender for Endpoint. Learn why [Microsoft Defender Antivirus and Microsoft Defender for Endpoint are better together](/microsoft-365/security/defender-endpoint/why-use-microsoft-defender-antivirus). Security and endpoint admins can work together to manage their Cloud PC environment just like they manage a physical endpoint. If subscribed, Cloud PCs will:
    - Send data through to Microsoft 365 Secure Score.
    - Unhealthy PCs will show up on the Microsoft Defender for Endpoint Security Center and threat analysis dashboards.
    - Respond to remediation measures just like other managed devices.
    - Support tamper protection management using [Defender](/microsoft-365/security/defender-endpoint/manage-tamper-protection-microsoft-365-defender) or [Intune](/microsoft-365/security/defender-endpoint/manage-tamper-protection-intune)  
7. Windows 365 integrates with Microsoft Purview. Onboarding to Defender for Endpoint includes [Purview Endpoint Data Loss Protection (DLP)](/purview/endpoint-dlp-getting-started). DLP detects when sensitive items are used and shared. This gives you the visibility and control you need to make sure that data is used and protected properly, and to help prevent risky behavior that might compromise them. [Configure endpoint data loss prevention settings](/purview/dlp-configure-endpoint-settings) to prevent data from getting:
    - Copied from a Cloud PC clipboard/drive to unauthorized devices.
    - Printed to unauthorized printers.
    
<!-- ########################## -->
## Next steps

[Deploy security baselines](deploy-security-baselines.md)
