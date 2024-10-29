---
title: Set up checklist for CMG
titleSuffix: Configuration Manager
description: Get an overview of the cloud management gateway (CMG) setup process and make sure you have all prerequisites ready to start.
ms.date: 04/08/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: overview
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Set up checklist for CMG

*Applies to: Configuration Manager (current branch)*

Before you deploy a cloud management gateway (CMG), use this article to understand the setup process. Also make sure you have all of the prerequisites ready to get started.

First, develop your design and plan for implementing a CMG in your environment. For more information, see [Plan for cloud management gateway](plan-cloud-management-gateway.md). Use that section of articles to determine your CMG design.

The overall CMG setup process is divided into the following five main parts:

1. _Get the CMG server authentication certificate_: The CMG uses HTTPS for secure client communication over the public internet. You can get a certificate from a public provider, or issue one from your public key infrastructure (PKI).

1. _Configure Microsoft Entra ID_: Configuration Manager requires app registrations in Microsoft Entra ID. You can let Configuration Manager create them, or an Azure administrator can pre-create the registrations.

1. _Configure client authentication_: Because clients communicate across the internet, Configuration Manager requires more security for this channel. You can use Microsoft Entra ID, PKI certificates, or token-based authentication from the site server.

1. _Set up the CMG_: This step also includes configuring the site, and adding the CMG connection point site system role.

1. _Configure clients to use the CMG_.

The other articles in this section step through each part of the process.

## Terminology

The following terms are used in the context of setting up a CMG. They're defined here for clarity.

- Microsoft Entra ID _tenant_: The directory of user accounts and app registrations. One tenant can have multiple subscriptions.

- Azure _subscription_: A subscription separates billing, resources, and services. It's associated with a single tenant.

  > [!TIP]
  > For more information, see [Subscriptions, licenses, accounts, and tenants for Microsoft's cloud offerings](/microsoft-365/enterprise/subscriptions-licenses-accounts-and-tenants-for-microsoft-cloud-offerings).

- Azure _resource group_: A container that holds related resources for an Azure solution. The resource group includes those resources that you want to manage as a group. You decide which resources belong in a resource group based on what makes the most sense for your organization. For more information, see [Resource groups](/azure/azure-resource-manager/management/overview#resource-groups).

- CMG _service name_: The common name (CN) of the CMG server authentication certificate. Clients and the CMG connection point site system role communicate with this service name. For example, `GraniteFalls.Contoso.Com` or `GraniteFalls.WestUS.CloudApp.Azure.Com`.

- CMG _deployment name_: The first part of the service name plus the Azure location for the cloud service deployment. The cloud service manager component of the service connection point uses this name when it deploys the CMG in Azure. The deployment name is always in an Azure domain. The Azure location depends upon the deployment method, for example:

  - Virtual machine scale set: `GraniteFalls.WestUS.CloudApp.Azure.Com`
  - Classic deployment: `GraniteFalls.CloudApp.Net`

## Checklist

Use the following checklist to make sure you have the necessary information and prerequisites to create a CMG:

- The Azure environment to use. For example, the Azure Public Cloud or the Azure US Government Cloud.

- The Azure region for this CMG deployment.

- How many VM instances you need for scale and redundancy.

- An Azure **application developer**, **cloud application administrator**, **application administrator**, or **global administrator** role to register apps in Microsoft Entra ID.

- An Azure **subscription owner** role for when you create the CMG in Azure.

- At least one existing site system server on which you plan to add the **CMG connection point** role.

- Review the [internet access requirements](data-flow.md#internet-access-requirements) to make sure each required services can be reached.

- [Enable this optional feature](../../../servers/manage/optional-features.md).

You'll set up other prerequisite components during the next steps in the process.

## Automate with PowerShell

<!--6978300-->
Optionally, you can automate aspects of the CMG setup using PowerShell. While some cmdlets were available in earlier versions, version 2010 includes new cmdlets and significant improvements to existing cmdlets.

For example, an Azure administrator first creates the two required apps in Microsoft Entra ID. Then you write a script that uses the following cmdlets to deploy a CMG:

1. **Import-CMAADServerApplication**: Create the Microsoft Entra server app definition in Configuration Manager.
1. **Import-CMAADClientApplication**: Create the Microsoft Entra client app definition in Configuration Manager.
1. Use **Get-CMAADApplication** to get the app objects, and then pass to **New-CMCloudManagementAzureService** to create the Azure service connection in Configuration Manager.
1. **New-CMCloudManagementGateway**: Create the CMG service in Azure.
1. **Add-CMCloudManagementGatewayConnectionPoint**: Create the CMG connection point site system.

You can use these cmdlets to automate the creation, configuration, and management of the CMG service and Microsoft Entra requirements.

Microsoft Entra app definitions in Configuration Manager:

- [Get-CMAADApplication](/powershell/module/configurationmanager/Get-CMAADApplication)
- [Import-CMAADClientApplication](/powershell/module/configurationmanager/Import-CMAADClientApplication)
- [Import-CMAADServerApplication](/powershell/module/configurationmanager/Import-CMAADServerApplication)

The **Cloud Management** Azure service in Configuration Manager:

- [New-CMCloudManagementAzureService](/powershell/module/configurationmanager/New-CMCloudManagementAzureService)
- [Set-CMCloudManagementAzureService](/powershell/module/configurationmanager/Set-CMCloudManagementAzureService)
- [Get-CMAzureService](/powershell/module/configurationmanager/Get-CMAzureService)
- [Remove-CMAzureService](/powershell/module/configurationmanager/Remove-CMAzureService)

The cloud management gateway service in Configuration Manager:

- [Get-CMCloudManagementGateway](/powershell/module/configurationmanager/Get-CMCloudManagementGateway)
- [New-CMCloudManagementGateway](/powershell/module/configurationmanager/New-CMCloudManagementGateway)
- [Remove-CMCloudManagementGateway](/powershell/module/configurationmanager/Remove-CMCloudManagementGateway)
- [Set-CMCloudManagementGateway](/powershell/module/configurationmanager/Set-CMCloudManagementGateway)
- [Start-CMCloudManagementGateway](/powershell/module/configurationmanager/Start-CMCloudManagementGateway)
- [Stop-CMCloudManagementGateway](/powershell/module/configurationmanager/Stop-CMCloudManagementGateway)

The CMG connection point site system role:

- [Add-CMCloudManagementGatewayConnectionPoint](/powershell/module/configurationmanager/Add-CMCloudManagementGatewayConnectionPoint)
- [Get-CMCloudManagementGatewayConnectionPoint](/powershell/module/configurationmanager/Get-CMCloudManagementGatewayConnectionPoint)
- [Remove-CMCloudManagementGatewayConnectionPoint](/powershell/module/configurationmanager/Remove-CMCloudManagementGatewayConnectionPoint)
- [Set-CMCloudManagementGatewayConnectionPoint](/powershell/module/configurationmanager/Set-CMCloudManagementGatewayConnectionPoint)

## Next steps

Get started with your CMG setup by getting a server authentication certificate:

> [!div class="nextstepaction"]
> [CMG server authentication certificate](server-auth-cert.md)
