---
# required metadata
title: Windows 365 architecture
titleSuffix:
description: Windows 365 architecture
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

ms.reviewer: saudm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Windows 365 architecture

Windows 365 provides a per-user per-month license model by hosting Cloud PCs on behalf of customers in Microsoft Azure. In this model, there’s no need to consider storage, compute infrastructure architecture, or costs. The Windows 365 architecture also lets you use your existing investments in Azure networking and security. Each Cloud PC is connected to an Azure virtual network that you configure in the Windows 365 section of the Microsoft Endpoint Manager admin center.

## Virtual network connectivity

Each Cloud PC has a virtual network interface card (NIC) in Microsoft Azure. The virtual NICs are created by Windows 365 in your Azure subscription. They’re attached to an Azure Virtual Network based on your on-premises network connection (OPNC) configuration.

Windows 365 is [supported in a number of Azure regions](requirements.md#supported-azure-regions-for-cloud-pc-provisioning). You can leverage Azure [virtual network peering](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) or [Virtual WAN](/azure/architecture/networking/hub-spoke-vwan-architecture) to extend access between Azure regions you currently use to one or more Windows 365 supported Azure regions.

By using Azure Networking, Windows 365 lets you use Virtual Network security and routing features, including:

- [Azure Network Security Groups](/azure/virtual-network/network-security-groups-overview)
- [User Defined Routing](/en-us/azure/virtual-network/virtual-networks-udr-overview)
- [Azure Firewall](/azure/firewall/overview)
- [Network virtual appliances](https://azure.microsoft.com/blog/best-practices-to-consider-before-deploying-a-network-virtual-appliance/) (NVAs)

However, for web filtering and network protection for Cloud PCs, consider using the [Network Protection](/microsoft-365/security/defender-endpoint/network-protection) and [Web Protection](/microsoft-365/security/defender-endpoint/web-protection-overview) features of Microsoft Defender for Endpoint. These features can be deployed across both physical and virtual endpoints by using the Microsoft Endpoint Manager admin center.

## Microsoft Endpoint Manager integration

Microsoft Endpoint Manager is used to manage all of your Cloud PCs. Microsoft Endpoint Manager and associated Windows components have a variety of [network endpoints that must be allowed](/mem/intune/fundamentals/intune-endpoints) through the Virtual Network. Apple and Android endpoints may be safely ignored if you don’t use Microsoft Endpoint Manager for managing those device types.

Be sure to allow access to [Windows Notification Services (WNS)](/mem/intune/fundamentals/intune-endpoints#windows-push-notification-services-wns). You might not immediately notice an impact if access is blocked. However, WNS enables Microsoft Endpoint Manager to trigger actions on Windows endpoints immediately instead of waiting for normal policy polling intervals on those devices or policy polling at startup/logon behavior. WNS [recommends](/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config) direct connectivity from the Windows client to WNS.

You’ll only need to grant access to a subset of endpoints based on your Microsoft Endpoint Manager tenant location. To find your tenant location (or Azure Scale Unit (ASU)), sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Tenant details**. Under **Tenant location**, you’ll see something similar to "North America 0501" or "Europe 0202". The rows in the Microsoft Endpoint Manager documentation are differentiated by geographic region, as indicated by the first two letters in the names (na = North America, eu = Europe, ap = Asia Pacific). Because tenants may be relocated within a region, it’s best to allow access to an entire region rather than a specific endpoint in that region.

For more information about Microsoft Endpoint Manager service regions and data location information, see [Data storage and processing in Intune](/mem/intune/protect/privacy-data-store-process).

## Identity services

Windows 365 uses both Microsoft Azure Active Directory (Azure AD) and on-premises Active Directory Domain Services (AD DS). Azure AD provides user authentication for Windows 365 (as with any other Microsoft 365 service), along with device identity services for Microsoft Endpoint Manager through Hybrid Azure AD Join. AD DS  provides on-premises domain join for the Cloud PCs along with user authentication for the Remote Desktop Protocol (RDP) connection.

### Azure AD

Azure AD provides user authentication and authorization for both the Windows 365 web portal and for the Remote Desktop client apps. Both support modern authentication, which means Azure AD Conditional Access can be integrated to provide:

- multi-factor authentication
- location-based restrictions
- sign-in risk management
- session limits, including:
  - sign-in frequency for Remote Desktop clients and the Windows 365 web portal
  - cookie persistence for the Windows 365 web portal
- device compliance controls

### Active Directory Domain Services

Windows 365 requires that Cloud PCs be joined to an AD DS domain. This domain must be synchronized with Azure AD. The domain’s domain controllers may be hosted in Azure or on-premises. If hosted on-premises, connectivity must be established from Azure to the on-premises environment. The connectivity can be in the form of [Azure Express Route](/azure/architecture/reference-architectures/hybrid-networking/expressroute) or a [site-to-site VPN](/azure/architecture/reference-architectures/hybrid-networking/vpn). For more information on establish hybrid network connectivity, see [implement a secure hybrid network](/azure/architecture/reference-architectures/dmz/secure-vnet-dmz). The connectivity must allow communication from the Cloud PCs to the domain controllers required by Active Directory. For more information see, [Configure firewall for AD domain and trusts](/troubleshoot/windows-server/identity/config-firewall-for-ad-domains-and-trusts).

## "Hosted on behalf of" connectivity

The "hosted on behalf of" connectivity lets Microsoft services, after they’re delegated appropriate and scoped permissions to a virtual network, attach hosted Azure services to a customer subscription. This lets a Microsoft service provide software-as-a-service and user licensed services as opposed to standard consumption-based services.

All Cloud PC connectivity is provided by the virtual network interface card. The "hosted on behalf of" architecture means that the Cloud PCs exists in the subscription owned by Microsoft. Therefore, Microsoft incurs the costs for running and managing this infrastructure.

Windows 365 aligns with Microsoft 365 data protection policies and provisions. Customer data within Microsoft's enterprise cloud services is protected by a variety of technologies and processes:

- Various forms of encryption.
- Isolated logically from other tenants.
- Accessible to a limited, controlled, and secured set of users, from specific clients.
- Secured for access using role-based access controls.
- Replicated to multiple servers, storage endpoints, and data centers for redundancy.
- Monitored for unauthorized access, excessive resource consumption, and availability.

## Azure Virtual Desktop connectivity

Cloud PC connectivity is provided by the Azure Virtual Desktop platform. Connectivity occurs from the Cloud PC to the Azure Virtual Desktop endpoints. No inbound connections direct from the Internet are made to the Cloud PC. Instead, Windows 365 seamlessly integrates Azure Virtual Desktop connectivity components into gallery or custom images. For more information on these ports, see [Azure Virtual Desktop required URL list](/azure/virtual-desktop/safe-url-list).

Service Tags are listed in the Azure Virtual Desktop documentation to ease the configuration of Azure Networking security controls. For more information on Azure Service Tags and their use in simplifying virtual network configuration, see [Azure service tags overview](/azure/virtual-network/service-tags-overview).

<!-- ########################## -->
## Next steps

[Learn about the Cloud PC lifecycle](lifecycle.md).
