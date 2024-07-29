---
title: Use cloud services
titleSuffix: Configuration Manager
description: Provision cloud resources for Configuration Manager to supplement your on-premises infrastructure.
ms.date: 07/15/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz
---

# Use cloud services with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager supports several cloud-based options. These can supplement your on-premises infrastructure, and can help solve business problems like:

- How to manage clients that roam onto the internet.

- How to provide content resources to isolated clients or resources on the intranet, outside your firewall.

- How to scale out infrastructure when physical hardware isn't available, or isn't logically placed to support your needs.

Provisioning cloud resources isn't something you have to do before you deploy Configuration Manager. It can be beneficial to understand these options before progressing too far in a hierarchy design plan. The use of cloud resources might save you money and time, while solving business problems that on-premises infrastructure can't.

## Cloud-based resources

Each option has different requirements. Investigate each in greater depth to understand the unique prerequisites, limitations, and potential for additional costs based on use.

### Azure virtual machines for cloud-based infrastructure

Configuration Manager supports using computers that run in virtual machines in Azure. You can use Azure virtual machines in the following scenarios:

- Run Configuration Manager in a virtual machine and use it to manage clients installed in other cloud-based virtual machines.

- Run Configuration Manager in a virtual machine and use it to manage clients that aren't in Azure.

- Run different Configuration Manager site system roles in Azure virtual machines. Run other roles in your on-premises network. Configure appropriate network connectivity for communications.

The same requirements for networks, operating systems, and hardware requirements that apply to installing the Configuration Manager on your on-premises network also apply to the installation of Configuration Manager in Azure.

An Azure subscription is required to use Azure virtual machines. You incur charges based on the number of virtual machines you use, their configuration, and use of cloud-based resources.

Additionally, Configuration Manager sites and clients that run in Azure virtual machines are subject to the same license requirements as on-premises installations.

For more information, see [Configuration Manager on Azure FAQ](configuration-manager-on-azure.yml).

### Azure services

You can connect the site to Azure for several scenarios:

- Microsoft Entra authentication and discovery. For more information, see [Configure Azure services](../servers/deploy/configure/azure-services-wizard.md).
- Cloud management gateway to manage internet-based clients. For more information, see [Cloud management gateway overview](../clients/manage/cmg/overview.md).
- Deploy apps from the Microsoft Store for Business and Education. For more information, see [Manage apps from the Microsoft Store for Business and Education](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).
- [Microsoft Intune tenant attach](../../tenant-attach/device-sync-actions.md)

These are different than using an Azure virtual machine, on which you deploy a site system role.

- Run as a service in Azure, not on a virtual machine.

- Automatically scale to meet increased content requests from clients.

- Support clients on the internet and the intranet.

An Azure subscription is required for these scenarios. You incur charges based on the amount of data that transfers to and from the service.

### Additional Configuration Manager capabilities

Some Configuration Manager capabilities can connect to cloud-based services, like:

- Windows Server Update Services (WSUS)

- Download updates for Configuration Manager

These additional capabilities don't require you to have an Azure subscription. You don't have to set up specific connections, certificates, or services in the cloud. Instead, they are automatically managed by Configuration Manager for you. All you need to do is ensure applicable site systems and devices can access the internet-based URLs.

## Security for cloud-based services

Configuration Manager uses certificates to provision and access your content in Azure, and to manage the services that you use. Configuration Manager encrypts the data that you store in Azure, but doesn't introduce additional security or data controls beyond those that Azure provides.

For more information, see the details for the different cloud-based resource scenarios. Also see an [Introduction to Azure security](/azure/security/fundamentals/overview).
