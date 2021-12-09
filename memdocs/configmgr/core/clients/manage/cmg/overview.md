---
title: Cloud management gateway overview
titleSuffix: Configuration Manager
description: Learn about managing internet-based clients with Configuration Manager by using the cloud management gateway (CMG) service in Azure.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: overview
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
ms.collection: highpri
---

# Cloud management gateway overview

*Applies to: Configuration Manager (current branch)*

<!--1101764-->
The cloud management gateway (CMG) provides a simple way to manage Configuration Manager clients over the internet. You deploy CMG as a cloud service in Microsoft Azure. Then without more on-premises infrastructure, you can manage clients that roam on the internet or are in branch offices across the WAN. You also don't need to expose your on-premises infrastructure to the internet.

:::image type="content" source="media/cmg-basic-architecture.svg" alt-text="Diagram of cloud management gateway (CMG) basic architecture.":::

After establishing the prerequisites, creating the CMG consists of the following three steps in the Configuration Manager console:

1. Deploy the CMG cloud service to Azure.
2. Add the CMG connection point role.
3. Configure the site and site roles for the service.

Once deployed and configured, clients seamlessly access on-premises site roles whether they're on the intranet or internet.

This article provides the foundational knowledge to learn about the CMG and the scenarios where you can use it.

## Scenarios

There are several scenarios for which a CMG is beneficial. The following scenarios are some of the more common:  

- Manage traditional Windows clients with Active Directory domain-joined identity. These clients include any supported version of Windows. It uses PKI certificates to secure the communication channel. Management activities include:  

  - Software updates and endpoint protection
  - Inventory and client status
  - Compliance settings
  - Software distribution to the device
  - Windows in-place upgrade task sequence

- Manage traditional Windows 10 or later clients with modern identity, either hybrid or pure cloud domain-joined with Azure Active Directory (Azure AD). Clients use Azure AD to authenticate rather than PKI certificates. Using Azure AD is simpler to set up, configure and maintain than more complex PKI systems. Management activities are the same as the first scenario plus:

  - Software distribution to the user  

- Install the Configuration Manager client on Windows 10 or later devices over the internet. Using Azure AD allows the device to authenticate to the CMG for client registration and assignment. You can install the client manually, or using another software distribution method, such as Microsoft Intune.  

- New device provisioning with co-management. When auto-enrolling existing clients, CMG isn't required for co-management. It's required for new devices involving Windows Autopilot, Azure AD, Microsoft Intune, and Configuration Manager. For more information, see [Paths to co-management](../../../../comanage/quickstart-paths.md).

## Specific use cases

Across these scenarios, the following specific device use cases may apply:

- Roaming devices such as laptops  

- Remote/branch office devices that are less expensive and more efficient to manage over the internet than across a WAN or through a VPN.  

- Mergers and acquisitions, where it may be easiest to join devices to Azure AD and manage through a CMG.  

- Workgroup clients. These devices may require other configurations, such as certificates.<!-- SCCMDocs#1925 -->

    To help with management of remote workgroup clients, use Configuration Manager token-based authentication. For more information, see [Token-based authentication for CMG](../../deploy/deploy-clients-cmg-token.md).

> [!IMPORTANT]
> By default all clients receive policy for a CMG, and start using it when they become internet-based. Depending upon the scenario and use case that applies to your organization, you may need to scope usage of the CMG. For more information, see the [Enable clients to use a cloud management gateway](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway) client setting.

## Next steps

Develop your design and plan for implementing a CMG in your environment:
  
> [!div class="nextstepaction"]
> [Plan for the CMG](plan-cloud-management-gateway.md)
