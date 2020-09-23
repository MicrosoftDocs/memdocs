---
title: Set up checklist for CMG
titleSuffix: Configuration Manager
description: Get an overview of the cloud management gateway (CMG) setup process and make sure you have all prerequisites ready to start.
ms.date: 09/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: overview
ms.assetid: 8f567343-c235-4a5e-a62b-668f503f2a92
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Set up checklist for cloud management gateway

*Applies to: Configuration Manager (current branch)*

Before you deploy a cloud management gateway (CMG), use this article to understand the setup process. Also make sure you have all of the prerequisites ready to get started.

First, develop your design and plan for implementing a CMG in your environment. For more information, see [Plan for cloud management gateway](plan-cloud-management-gateway.md). Use that section of articles to determine your CMG design.

The overall CMG setup process is divided into the following five main parts:

1. _Get the CMG server authentication certificate_: The CMG uses HTTPS for secure client communication over the public internet. You can get a certificate from a public provider, or issue one from your public key infrastructure (PKI).

1. _Configure CMG authentication_: Because clients communicate across the internet, Configuration Manager requires additional security for this channel. You can use Azure Active Directory (Azure AD), PKI certificates, or token-based authentication from the site server.

1. _Configure Azure AD_: Configuration Manager requires app registrations in Azure AD. You can let Configuration Manager create them, or an Azure administrator can pre-create the registrations.

1. _Set up the CMG_: This step also includes configuring the site, and adding the CMG connection point site system role.

1. _Configure clients to use the CMG_.

The other articles in this section step through each part of the process.

## Terminology

The following terms are used in the context of setting up a CMG. They're defined here for clarity.

- Azure AD _tenant_: The directory of user accounts and app registrations. One tenant can have multiple subscriptions.

- Azure AD _subscription_: A subscription separates billing, resources, and services. It's associated with a single tenant.

- Azure _resource group_: A container that holds related resources for an Azure solution. The resource group includes those resources that you want to manage as a group. You decide which resources belong in a resource group based on what makes the most sense for your organization. For more information, see [Resource groups](/azure/azure-resource-manager/management/overview#resource-groups).

- CMG _service name_: The common name (CN) of the CMG server authentication certificate. Clients and the CMG connection point site system role communicate with this service name. For example, `GraniteFalls.Contoso.Com` or `GraniteFalls.CloudApp.Net`.

- CMG _deployment name_: The first part of the service name plus the Azure location for the cloud service deployment. For example, `GraniteFalls.CloudApp.Net`. The cloud service manager component of the service connection point uses this name when it deploys the CMG in Azure. The deployment name is always in an Azure domain.

## Checklist

Use the following checklist to make sure you have the necessary information and prerequisites to create a CMG:  

- The Azure environment to use. For example, the Azure Public Cloud or the Azure US Government Cloud.  

- The Azure region for this CMG deployment.  

- How many VM instances you need for scale and redundancy.

- You need one or more certificates for CMG, depending upon your design. For more information, see [Certificates for cloud management gateway](certificates-for-cloud-management-gateway.md).  

- You need the following requirements for an [Azure Resource Manager](plan-cloud-management-gateway.md#azure-resource-manager) deployment of CMG:  

  - Integration with [Azure AD](../../../servers/deploy/configure/azure-services-wizard.md) for **Cloud Management**. Azure AD user discovery isn't required. To integrate the site with Azure AD for deploying the CMG using Azure Resource Manager, you need a **Global Admin**.

  - The **Microsoft.ClassicCompute** & **Microsoft.Storage** resource providers must be registered within the Azure subscription. For more information, see [Azure Resource Manager](/azure/azure-resource-manager/resource-manager-supported-services).

  - A **Subscription Owner** needs to sign in to deploy the CMG.

- A globally unique name for the service. This name is from the [CMG server authentication certificate](server-auth-cert.md).  

- If enabling CMG as a cloud distribution point, the same globally unique CMG service name chosen also needs to be available as a globally unique storage account name. This name is from the [CMG server authentication certificate](server-auth-cert.md).

## Next steps

Get started with your CMG setup by getting a server authentication certificate:
  
> [!div class="nextstepaction"]
> [CMG server authentication certificate](server-auth-cert.md)
