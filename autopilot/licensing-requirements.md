---
title: Windows Autopilot licensing requirements
description: Inform yourself about licensing requirements for Windows Autopilot deployment.
ms.prod: windows-client
ms.technology: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 11/30/2023
ms.collection: 
  - M365-modern-desktop
  - tier2
ms.topic: conceptual
ms.custom: 
  - CI 116757
  - CSSTroubleshooting
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a> 
---

# Windows Autopilot licensing requirements

Windows Autopilot depends on specific capabilities available in Windows client and Microsoft Entra ID. It also requires an MDM service such as Microsoft Intune. These capabilities can be obtained through various editions and subscription programs:

To provide needed Microsoft Entra ID (automatic MDM enrollment and company branding features) and MDM functionality, one of the following subscriptions is required:

- [Microsoft 365 Business Premium subscription](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 F1 or F3 subscription](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Microsoft 365 Academic A1, A3, or A5 subscription](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 Enterprise E3 or E5 subscription](https://www.microsoft.com/microsoft-365/enterprise), which include all Windows client, Microsoft 365, and EMS features (Microsoft Entra ID and Intune).
- [Enterprise Mobility + Security E3 or E5 subscription](https://www.microsoft.com/cloud-platform/enterprise-mobility-security), which include all needed Microsoft Entra ID and Intune features.
- [Intune for Education subscription](/intune-education/what-is-intune-for-education), which include all needed Microsoft Entra ID and Intune features.
- [Microsoft Entra ID P1 or P2](https://azure.microsoft.com/services/active-directory/) and [Microsoft Intune subscription](https://www.microsoft.com/cloud-platform/microsoft-intune) (or an alternative MDM service).

> [!NOTE]
>
> Even when using Microsoft 365 subscriptions, you still need to [assign Intune licenses to the users](/intune/fundamentals/licenses-assign).

Additionally, the following are also recommended (but not required):

- [Microsoft 365 Apps for enterprise](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0), which can be deployed easily via Intune (or other MDM services).
- [Windows Subscription Activation](/windows/deployment/windows-10-enterprise-subscription-activation), to automatically step up devices from Windows Pro to Windows Enterprise edition.

## Next steps

- [Windows Autopilot configuration requirements](configuration-requirements.md)
