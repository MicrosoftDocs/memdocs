---
# required metadata
title: Requirements to set up HP Anyware for Windows 365 Enterprise
titleSuffix:
description: Learn about requirements for using HP Anyware with Windows 365 Enterprise.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 10/09/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: elaineyou    
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Requirements for using HP Anyware for Windows 365 Enterprise (preview)

To use HP Anyware for Windows 365, you must meet the following requirements:

## HP Anyware requirements

- HP Anyware Standard license
- Cloud PCs must have access to:
  - https://cas.teradici.com on TCP 443 for Broker connectivity.
- Consult [Anyware Session Planning Guide](https://www.teradici.com/web-help/pcoip/session_planning_guide/2023.12/network/network_requirements/) for more requirements.

## Microsoft requirements

- Microsoft Intune entitlement
- Microsoft Entra domain in the same tenant as Microsoft Intune
- Windows 365 Enterprise licenses in the same tenant as Microsoft Intune
- Azure admin account:
  - Intune Administrator for required authorizations in HP Anyware Service.
  - Intune Administrator for enabling the HP Anyware connector in Microsoft Intune.
  - For more information about the Windows 365 requirements, see [Windows 365 requirements](requirements.md).

## Supported configurations

HP Anyware for Windows 365 supports integrating with Windows 365 deployments for Microsoft Entra joined Cloud PCs and Microsoft Entra hybrid joined Cloud PCs. Also, the supported identity providers include Microsoft Entra ID and Okta. 

<!-- ########################## -->
## Next steps

[Set up HP AnyWare for Windows 365 Enterprise](hp-anyware-set-up.md).
