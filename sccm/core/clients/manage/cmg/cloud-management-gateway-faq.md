---
title: CMG FAQ
titleSuffix: Configuration Manager
description: Use this article to answer frequently asked questions regarding the cloud management gateway
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117


---

# Frequently asked questions about the cloud management gateway

*Applies to: Configuration Manager (current branch)*

This article answers your frequently asked questions about the cloud management gateway. For more information, see [plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## Frequently asked questions

### What certificates do I need?

For more detailed information, see [certificates for cloud management gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).


### Do I need Azure ExpressRoute?

No. [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) lets you extend your on-premises network into the Microsoft cloud. ExpressRoute, or other such virtual network connections aren't required for the Configuration Manager cloud management gateway. The design of the cloud management gateway allows internet-based clients to communicate through the Azure service to on-premises site systems with no additional network configuration. For more information, see [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)

<!-- SCCMDocs#1659 -->

### Do I need to maintain the Azure virtual machines?

No maintenance is required. The design of the cloud management gateway uses Azure platform as a service (PaaS). Using the subscription you provide, Configuration Manager creates the necessary virtual machines (VMs), storage, and networking. Azure secures and updates the virtual machine. These VMs aren't a part of your on-premises environment, as is the case with infrastructure as a service (IaaS). The cloud management gateway is a PaaS that extends your Configuration Manager environment into the cloud. For more information, see [Securing PaaS deployments](/azure/security/security-paas-deployments).


### How can I ensure service continuity during service updates?

By scaling CMG to include two or more instances, you automatically benefit from Update Domains in Azure. See [How to update a cloud service](/azure/cloud-services/cloud-services-update-azure-service).


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

### How does CMG affect my clients connected via VPN?

Roaming clients that connect to your environment via a VPN are commonly detected as intranet-facing. They attempt to connect to your on-premises infrastructure such as management points and distribution points. Some customers prefer to have these roaming clients managed by cloud services even when connected via VPN. Starting in version 1902, associate the CMG with a boundary group. This action forces these clients to not use the on-premises site systems. For more information, see [Configure boundary groups](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#configure-boundary-groups).

### If I enable a CMG, will my clients only connect to the CMG-enabled management point when they're connected to the intranet?

In order to secure sensitive traffic sent over a CMG, either configure an HTTPS management point or use Enhanced HTTP.

If you choose to deploy a CMG, and use PKI certificates for HTTPS communication on the CMG-enabled management point, select the option to **Allow internet-only clients** on the management point properties. This setting makes sure that internal clients continue to use HTTP management points in your environment.

If you use Enhanced HTTP, you don't need to configure this setting. Clients continue to use HTTP when communicating directly to the CMG-enabled management point. For more information, see [Enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http).

## Next steps

- [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Set up cloud management gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Certificates for cloud management gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Security and privacy for cloud management gateway](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Cloud management gateway size and scale numbers](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
