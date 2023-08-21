---
# required metadata
title: Requirements to set up VMware Horizon for Windows 365 Enterprise
titleSuffix:
description: Learn about requirements for using VMware Horizon with Windows 365 Enterprise.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/21/2023
ms.topic: overview
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aradinger    
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Requirements for using VMware Horizon for Windows 365 Enterprise

To use VMware Horizon for Windows 365, you must meet the following requirements:

## VMware requirements

- A VMware Horizon Cloud Service – Next Gen tenant
- A Horizon Cloud Service Subscription that includes:
  - Horizon Universal Licenses for Apps
  - Horizon Universal License for Desktops and Apps support brokering to Windows 365 Cloud PCs
- A VMware Cloud Service Portal (CSP) account
- The same identity provider access being used by your Windows 365 Tenant
- Tenant to tenant connectivity
- Entitle users
- Cloud PC Must have access to the following ports:
  - Agent facing: 8444
  - Client facing: 443 and 8443
- VMware UAG as a Service (Preview) is required for brokering to Windows 365 Cloud PCs. It's enabled by default when you turn on the Windows 365 provider type in Horizon Cloud Service – next-gen.

## Microsoft requirements

- Microsoft Intune entitlement
- Azure Active Directory (Azure AD) domain in the same tenant as Microsoft Intune
- Windows 365 Enterprise licenses in the same tenant as Microsoft Intune
- Azure admin account:
  - Azure AD Global Admin for required authorizations in the VMware Cloud.
  - Intune Admin for enabling the VMware connector in Microsoft Intune.
  - For more information about the Windows 365 requirements, see [Windows 365 requirements](requirements.md).

## Supported configurations

VMware Horizon for Windows 365 supports integrating with Windows 365 deployments with for Azure AD joined Cloud PCs and Hybrid Azure AD joined Cloud PCs.

<!-- ########################## -->
## Next steps

[Set up VMware Horizon for Windows 365 Enterprise](set-up-vmware-horizon.md).
