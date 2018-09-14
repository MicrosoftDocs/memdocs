---
title: CMG FAQ
description: Use this article to answer frequently asked questions regarding the cloud management gateway
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
---

# Frequently asked questions about the cloud management gateway

*Applies to: System Center Configuration Manager (Current Branch)*

This article answers your frequently asked questions about the cloud management gateway. For more information, see [plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## Frequently asked questions

### What certificates do I need?

For more detailed information, see [certificates for cloud management gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).


### Do I need Azure ExpressRoute?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) lets you extend your on-premises network into the Microsoft cloud. ExpressRoute, or other such virtual network connections aren't required for the Configuration Manager cloud management gateway. The design of the cloud management gateway allows internet-based clients to communicate through the Azure service to on-premises site systems with no additional network configuration. For more information, see [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)

If your organization uses ExpressRoute, a security best practice is to isolate the Azure subscription for the cloud management gateway. This configuration makes sure that the cloud management gateway service isn't accidentally connected in this manner. For more information, see [Security and privacy for cloud management gateway](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway).


### Do I need to maintain the Azure virtual machines?

No maintenance is required. The design of the cloud management gateway uses Azure platform as a service (PaaS). Using the subscription you provide, Configuration Manager creates the necessary virtual machines (VMs), storage, and networking. Azure secures and updates the virtual machine. These VMs aren't a part of your on-premises environment, as is the case with infrastructure as a service (IaaS). The cloud management gateway is a PaaS that extends your Configuration Manager environment into the cloud. 


### I'm already using IBCM. If I add CMG, how do clients behave?

If you already deployed [internet-based client management](/sccm/core/clients/manage/plan-internet-based-client-management) (IBCM), you can also deploy the cloud management gateway. Clients receive policy for both services. As they roam onto the internet, they randomly select and use one of these internet-based services.


### Do the user accounts have to be in the same Azure subscription as the subscription that hosts the CMG cloud service?
<!--SCCMDocs-pr issue #2873-->
If your environment has more than one subscription, you can deploy CMG into any subscription that can host Azure cloud services. 

This question is common in the following scenarios:  

- When you have distinct test and production Active Directory and Azure AD environments, but one single, centralized Azure hosting subscription  

- Your use of Azure has grown organically across different teams  

When you're using a Resource Manager deployment, onboard the associated Azure AD tenant. This connection allows Configuration Manager to authenticate to Azure to create, deploy, and manage the CMG.  

If you're using Azure AD authentication for the users and devices managed over the CMG, onboard that Azure AD tenant. For more information on Azure services for cloud management, see [Configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard). When you onboard each Azure AD tenant, a single CMG can provide Azure AD authentication for multiple tenants, regardless of the hosting location.



## Next steps

- [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Set up cloud management gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Certificates for cloud management gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Security and privacy for cloud management gateway](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Cloud management gateway size and scale numbers](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)