---
# required metadata
title: Requirements to set up Citrix HDX Plus for Windows 365 Enterprise
titleSuffix:
description: Learn about requirements for using Citrix HDX Plus with Windows 365 Enterprise.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/21/2023
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

# Requirements for using Citrix HDX Plus for Windows 365 Enterprise

To use Citrix HDX Plus for Windows 365, you must meet the following requirements:

## Citrix requirements

- Citrix Cloud tenant with HDX Plus for Windows 365 entitlement
  - DaaS Standard for Azure
  - DaaS Advanced Plus
  - DaaS Premium
  - DaaS Premium Plus
- Citrix admin account with full admin rights
- Cloud PCs must have access to:
  - https://*.*.nssvc.net on TCP 443 and UDP 443 for HDX sessions over TCP and EDT, respectively. If you can’t allow all subdomains in that manner, you can instead use https://*.c.nssvc.net and https://*.g.nssvc.net. For more information, see the [Citrix Support Knowledge Center article CTX270584](https://support.citrix.com/article/CTX270584/citrix-gateway-service-pointsofpresence-pops).
  - https://*.xendesktop.net on TCP 443. If you can’t allow all subdomains in that manner, you can use https://<customer_ID>.xendesktop.net, where customer_ID is your Citrix Cloud customer ID as shown in the Citrix Cloud administrator portal.
- For Microsoft Entra hybrid joined deployments:
  - The Microsoft Entra domain must be synchronized from the Microsoft Entra domain that the Cloud PCs belong to.
  - Cloud Connectors to allow Citrix Cloud to connect to your Active Directory domain. For more information, see [Citrix Cloud Connector](https://docs.citrix.com/en-us/citrix-cloud/citrix-cloud-resource-locations/citrix-cloud-connector.html).
- Allowlist endpoint required for VDA registration: \*.apps.cloud.com

## Microsoft requirements

- Microsoft Intune entitlement
- Microsoft Entra domain in the same tenant as Microsoft Intune
- Windows 365 Enterprise licenses in the same tenant as Microsoft Intune
- Azure admin account:
  - Intune Administrator for required authorizations in Citrix Cloud.
  - Intune Administrator for enabling Citrix connector in Microsoft Intune.
  - For more information about the Windows 365 requirements, see [Windows 365 requirements](requirements.md).

Citrix HDX Plus doesn't currently support Windows 365 Frontline.

## Supported configurations

Citrix HDX Plus for Windows 365 supports integrating with Windows 365 deployments with for Microsoft Entra joined Cloud PCs and Microsoft Entra hybrid joined Cloud PCs. The following tables detail the configurations for each scenario.

### Supported infrastructures

| Identity | Citrix Cloud | CVAD (on-premises) | Citrix Workspace | Citrix Storefront | Citrix Gateway Service | Citrix Gateway |
| --- | --- | --- | --- | --- | --- | --- |
| Microsoft Entra joined | Yes | No | Yes | No | Yes | No |
| Microsoft Entra hybrid joined | Yes | No | Yes | No | Yes | No |

### Supported identity providers

| Identity | Microsoft Entra ID | Active Directory | Active Directory + Token | Okta | SAML | Citrix Gateway | Adaptive Authentication |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Microsoft Entra joined | Yes | No | No | No | No | No | No |
| Microsoft Entra hybrid joined | Yes | Yes | Yes | Yes | Yes | Yes | Yes |

> [!NOTE]  
> For Hybrid AD joined deployments, if you're using an IdP other than Active Directory or Active Directory + Token, you'll need Citrix Federated Authentication Service (FAS). If you don't use FAS, you won't be able to use single sign-on (SSO) to the Cloud PC. For more information, see the [FAS documentation](https://docs.citrix.com/en-us/federated-authentication-service).  

<!-- ########################## -->
## Next steps

[Set up Citrix HDX Plus for Windows 365 Enterprise](set-up-citrix.md).
