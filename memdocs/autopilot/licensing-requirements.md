---
title: Windows Autopilot licensing requirements
description: Inform yourself about licensing requirements for Windows Autopilot deployment.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, Autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: aczechowski
ms.author: aaroncz
ms.reviewer: jubaptis
manager: dougeby
ms.date: 12/16/2020
ms.collection:
  - M365-modern-desktop
  - highpri
ms.topic: conceptual
ms.custom: 
- CI 116757
- CSSTroubleshooting
---

# Windows Autopilot licensing requirements

**Applies to**

- Windows 11
- Windows 10
- Windows Holographic, version 2004 or later

Windows Autopilot depends on specific capabilities available in Windows client and Azure Active Directory (Azure AD). It also requires an MDM service such as Microsoft Intune. These capabilities can be obtained through various editions and subscription programs:

To provide needed Azure Active Directory (automatic MDM enrollment and company branding features) and MDM functionality, one of the following subscriptions is required:
- [Microsoft 365 Business Premium subscription](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 F1 or F3 subscription](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Microsoft 365 Academic A1, A3, or A5 subscription](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 Enterprise E3 or E5 subscription](https://www.microsoft.com/microsoft-365/enterprise), which include all Windows client, Microsoft 365, and EMS features (Azure AD and Intune).
- [Enterprise Mobility + Security E3 or E5 subscription](https://www.microsoft.com/cloud-platform/enterprise-mobility-security), which include all needed Azure AD and Intune features.
- [Intune for Education subscription](/intune-education/what-is-intune-for-education), which include all needed Azure AD and Intune features.
- [Azure Active Directory Premium P1 or P2](https://azure.microsoft.com/services/active-directory/) and [Microsoft Intune subscription](https://www.microsoft.com/cloud-platform/microsoft-intune) (or an alternative MDM service).

> [!NOTE]
> Even when using Microsoft 365 subscriptions, you still need to [assign Intune licenses to the users](/intune/fundamentals/licenses-assign).

Additionally, the following are also recommended (but not required):
- [Microsoft 365 Apps for enterprise](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0), which can be deployed easily via Intune (or other MDM services).
- [Windows Subscription Activation](/windows/deployment/windows-10-enterprise-subscription-activation), to automatically step up devices from Windows Pro to Windows Enterprise edition.

**Next steps**

[Windows Autopilot configuration requirements](configuration-requirements.md)
