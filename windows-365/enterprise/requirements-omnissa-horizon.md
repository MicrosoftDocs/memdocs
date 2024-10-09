---
# required metadata
title: Requirements to set up Omnissa Horizon for Windows 365 Enterprise
titleSuffix:
description: Learn about requirements for using Omnissa Horizon with Windows 365 Enterprise.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/21/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
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

# Requirements for using Omnissa Horizon for Windows 365 Enterprise

To use Omnissa Horizon for Windows 365, you must meet the following requirements:

## Omnissa requirements

- An Omnissa Horizon Cloud Service – Next Gen tenant
- A Horizon Cloud Service Subscription that includes:
  - Horizon Universal Licenses for Apps
  - Horizon Universal License for Desktops and Apps support brokering to Windows 365 Cloud PCs
- An Omnissa Cloud Service Portal (CSP) account
- The same identity provider access being used by your Windows 365 Tenant
- Tenant to tenant connectivity
- Entitle users
- Cloud PC Must have access to the following ports:
  - Agent facing: 8444
  - Client facing: 443 and 8443
- Omnissa UAG as a Service (Preview) is required for brokering to Windows 365 Cloud PCs. It's enabled by default when you turn on the Windows 365 provider type in Horizon Cloud Service – next-gen.

## Microsoft requirements

- Microsoft Intune entitlement
- Microsoft Entra domain in the same tenant as Microsoft Intune
- Windows 365 Enterprise licenses in the same tenant as Microsoft Intune
- Azure admin account:
  - Intune Administrator for required authorizations in the Omnissa Cloud.
  - Intune Administrator for enabling the Omnissa connector in Microsoft Intune.
  - For more information about the Windows 365 requirements, see [Windows 365 requirements](requirements.md).

## Supported configurations

Omnissa Horizon for Windows 365 supports integrating with Windows 365 deployments with for Microsoft Entra joined Cloud PCs and Microsoft Entra hybrid joined Cloud PCs.

<!-- ########################## -->
## Next steps

[Set up Omnissa Horizon for Windows 365 Enterprise](set-up-omnissa-horizon.md).
