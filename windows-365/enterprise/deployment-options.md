---
# required metadata
title: Windows 365 deployment options
titleSuffix:
description: Learn about Windows 365 deployment options.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 12/10/2022
ms.topic: how-to
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: feadebay
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Windows 365 deployment options

You have two options for network deployment of the Windows 365 service:

- Microsoft-hosted network (Recommended)
- Azure Network Connection (ANC)

## Microsoft-hosted network

With this option, Windows 365 is delivered as a SaaS solution. Microsoft fully manages the infrastructure and related services required to deliver functional Cloud PCs to your users. Microsoft also manages the network that the Cloud PCs occupy.

The customer’s only responsibility is the configuration and management of the Cloud PCs. Microsoft doesn’t configure anything within the Cloud PC itself.

Microsoft recommends that customers use this option for their Windows 365 deployment.

### Azure Active Directory join

The simplest method to deploy Windows 365 in your environment is to use the Azure Active Directory join (Azure AD join) identity model in combination with the Microsoft hosted network. With this option, Microsoft:

- Sets up and manages the underlying infrastructure.
- Provides a Zero Trust Framework-aligned model of an End User Computing (EUC) environment.

You don’t have to bring in your own Azure subscription(s), plan, design, deploy, or manage the infrastructure. Customers can dedicate their EUC team to focus on managing Cloud PC configurations and security from a single management console provided by Intune.

This option is analogous to providing an employee with a laptop to use at home. You as an organization don’t control the network the device sits on. You do fully control how the Windows device is configured, secured, and how it connects to your on-premises network. With Windows 365, this control is possible thanks to the end-to-end Zero Trust Security Framework-aligned adaptive security controls and configurations.

For example, users can be authenticated with adaptive controls of Azure Conditional Access. Corporate connectivity can be delivered by using VPN. Internet security can use a cloud-based secure web gateway (SWG). The advantage is that devices can be deployed at scale in a very short timeframe whenever needed on an extremely high bandwidth, resilient network.

The diagram below shows the Microsoft hosted network with the Cloud PC and Virtual Network card within a subscription managed by Microsoft.

IMAGE

### Benefits of this Model

- No Azure subscription is required. Microsoft provides and fully manages the infrastructure required for the Cloud PC to operate. All you need is the required licenses.
- No additional costs for network infrastructure. The Azure costs of operating your own Virtual Network (VNet) and virtual appliances don’t apply. Microsoft takes care of the network infrastructure.
- No Azure networking expertise or management is required. The virtual network is fully managed by Microsoft.
- Low complexity and rapid deployment. There is low complexity in deploying because of minimal dependencies on customer-side elements.
- Zero trust alignment. The Zero Trust model of operation for user, endpoint, workload, and data signals is used for verification rather than applying trust to the network location.
- Simpler troubleshooting and operations. It’s easier to troubleshoot and pinpoint networking issues and adopt modern device management based on Intune policies, security controls, and built-in reporting capabilities.

### Considerations

Before using the Microsoft-hosted network option, review these considerations:

- This option isn’t compatible with the Hybrid Azure AD join model. This is a Cloud-only deployment with no connectivity to on-premises Active Directory Domain Services infrastructure. If you have Group Policy Object-based management policies that can’t be converted to Intune, then this is not the right option for you.
- No control of the VNet. The virtual NIC is Microsoft-managed. Therefore, all network controls must be implemented on the Cloud PC itself, similar to physical devices in a work-from-home scenario.
- No direct access to on-premises resources. A VPN or private access solution is required to access these resources. When using VPNs with a Cloud PC, use [split tunneling]( https://techcommunity.microsoft.com/t5/windows-365/optimizing-rdp-connectivity-for-windows-365/m-p/3554327) to make sure that RDP traffic isn’t routed through the VPN.
- Requires a cloud native management operation model like Intune.
- Port 25 is blocked.
- Ping/ICMP is blocked.
- Local network communications between Cloud PCs are blocked.
- No direct inbound connectivity is possible to Cloud PCS.
- Admins can’t reliably connect from one Cloud PC to another Cloud PC. The underlying VNET could be different. Cross Vnet communications are blocked.
- There is no way for admins to control the IP address ranges and/or address space assigned to the Cloud PCs. Windows 365 handles the IP addresses automatically.

<!-- ########################## -->
## Next steps


