---
title: Plan for CMG
titleSuffix: Configuration Manager
description: Plan and design the cloud management gateway (CMG) to simplify management of internet-based clients.
ms.date: 04/08/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
ms.collection: highpri
---

# Plan for the CMG in Configuration Manager

*Applies to: Configuration Manager (current branch)*

To simplify management of internet-based clients, first develop a plan for the cloud management gateway (CMG). Design how it fits in your environment and prepare for your implementation.

For more foundational knowledge of CMG scenarios and use cases, see [Overview of CMG](overview.md).

> [!NOTE]
> Some sections that were previously in this article have moved:
>
> - **Hierarchy design**: [CMG hierarchy design](plan-hierarchy-design.md)
> - **Performance and scale**: [CMG performance and scale](perf-scale.md)

## Planning checklist

The overall CMG planning process is divided into the following parts:

- _Components and requirements_: This article summarizes the components that make up the CMG system. It also lists the system requirements.

- _Client authentication_: Determine which authentication method you'll use for clients from potentially untrusted networks.

- _Hierarchy design_: Plan where to place the CMG in your environment.

- _Supported configurations_: Understand which Configuration Manager features you can support on internet-based clients that connect to the CMG.

- _Performance and scale_: Decide how many service components you'll need to best support your number of clients.

- _Cost_: Understand the cost of the Azure-based components.

## CMG components

Deployment and operation of the CMG includes the following components:

- The **CMG cloud service** in Azure authenticates and forwards Configuration Manager client requests over the internet to the on-premises CMG connection point.

- The **CMG connection point** site system role enables a consistent and high-performance connection from the on-premises network to the CMG service in Azure. It also publishes settings to the CMG including connection information and security settings. The CMG connection point forwards client requests from the CMG to on-premises roles according to URL mappings. For example, the management point and software update point.

- The [**service connection point**](../../../servers/deploy/configure/about-the-service-connection-point.md) site system role runs the cloud service manager component, which handles all CMG deployment tasks. Additionally, it monitors and reports service health and logging information from Azure Active Directory (Azure AD). Make sure your service connection point is in [online mode](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).

- The **management point** and **software update point** site system roles service client requests per normal.

- The CMG uses a **certificate-based HTTPS** web service to help secure network communication with clients.

- **Internet-based clients** connect to the CMG to access on-premises Configuration Manager components. There are multiple options for client identity and authentication:

  - Azure AD
  - PKI certificates
  - Configuration Manager site-issued tokens

  For more information, see [Plan for CMG client authentication](plan-client-authentication.md).

- The CMG creates an **Azure storage account**, which it uses for its standard operations. By default, the CMG is also content-enabled to provide deployment content to internet-based clients. This storage account doesn't support customizations, such as virtual network restrictions.

  > [!NOTE]
  > The cloud-based distribution point (CDP) is deprecated. Starting in version 2107, you can't create new CDP instances. To provide content to internet-based devices, enable the CMG to distribute content.<!-- 10247883 -->

## Azure Resource Manager

<!-- 1324735 -->
You create the CMG using an **Azure Resource Manager deployment**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) is a modern platform for managing all solution resources as a single entity, called a [resource group](/azure/azure-resource-manager/resource-group-overview#resource-groups). When you deploy a CMG with Azure Resource Manager, the site uses Azure Active Directory (Azure AD) to authenticate and create the necessary cloud resources.

> [!IMPORTANT]
> Starting in version 2203, the option to deploy a CMG as a **cloud service (classic)** is removed.<!-- 13235079 --> All CMG deployments should use a [virtual machine scale set](#virtual-machine-scale-sets).<!--10966586--> For more information, see [Removed and deprecated features](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

## Virtual machine scale sets

> [!NOTE]
> This feature was first introduced in version 2010 as a [pre-release feature](../../../servers/manage/pre-release-features.md). Starting in version 2107, it's no longer a pre-release feature.<!-- 8959690 -->
>
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](../../../servers/manage/optional-features.md).

<!--3601040-->
Starting in version 2010, customers with a Cloud Solution Provider (CSP) subscription can deploy the CMG with a **virtual machine scale set** in Azure. This support is only if they don't currently have a CMG deployed using classic cloud services to another subscription.

Starting in version 2107, all customers can deploy a CMG with a virtual machine scale set. If you have an existing CMG deployed with the classic cloud service, **convert** the CMG to use a virtual machine scale set.<!-- 8959690 -->

With a few exceptions, the configuration, operation, and functionality of the CMG remains the same.

- Other [Azure resource providers](configure-azure-ad.md#configure-azure-resource-providers) in your Azure subscription.

- Different deployment names, for example, **GraniteFalls.EastUS.CloudApp.Azure.Com** for a deployment in the **East US** Azure region. This name change can affect how you create and manage the [CMG server authentication certificate](server-auth-cert.md).

- The CMG connection point only communicates with the virtual machine scale set in Azure over HTTPS. It doesn't require TCP-TLS ports.

### Limitations for a CMG with a virtual machine scale set

#### Limitations with versions 2107 and later

> [!NOTE]
> Starting in version 2111, CMG deployments with a virtual machine scale set support Azure US Government cloud environments.<!--12141235-->

- Users may experience a delay of up to three seconds for actions in Software Center.
- You can't approve/deny application requests through the CMG.<!-- 10023094 -->
- Version 2107 doesn't support Azure US Government cloud environments.

#### Limitations with versions 2010 and 2103

- If you require more than one CMG instance, they all have to use the same deployment method.
- The supported number of concurrent client connections is 2,000 per VM instance. For more information, see [CMG performance and scale](perf-scale.md).
- It's only supported with a standalone primary site.
- It doesn't support Azure US Government cloud environments.
- Users may experience a delay of up to three seconds for actions in Software Center.
- Configuration Manager currently creates the Azure storage container based on the name of the resource group. Azure has different naming requirements for resource groups and storage containers. Make sure the name of the resource group for this service only has lowercase letters, numbers, and hyphens. If you have an existing resource group that doesn't work, rename it in the Azure portal, or create a new resource group.<!-- 8888841 -->
- If you have more than one HTTPS management point, then you can't install the Configuration Manager client on devices over the internet. If you need to [Install off-premises clients using a CMG](configure-clients.md#install-off-premises-clients-using-a-cmg), then you can only have one HTTPS management point. You also need to enable the CMG for content.<!-- 9760068 -->
- You can't approve/deny application requests through the CMG.<!-- 10023094 -->

## Requirements

> [!TIP]
> To clarify some Azure terminology:
>
> - The Azure AD _tenant_ is the directory of user accounts and app registrations. One tenant can have multiple subscriptions.
> - An Azure _subscription_ separates billing, resources, and services. It's associated with a single tenant.
>
> For more information, see [Subscriptions, licenses, accounts, and tenants for Microsoft's cloud offerings](/microsoft-365/enterprise/subscriptions-licenses-accounts-and-tenants-for-microsoft-cloud-offerings).

- An **Azure subscription** to host the CMG. This subscription can be in one of the following environments:

  - Global Azure cloud
  - Azure US Government cloud

  Customers with a Cloud Service Provider (CSP) subscription need to use version 2010 or later with a **virtual machine scale set** deployment.<!--3601040-->

- Integrate the site with **Azure AD** to deploy the service with Azure Resource Manager. For more information, see [Configure Azure AD for CMG](configure-azure-ad.md).

  When you onboard the site to Azure AD, you can optionally enable **Azure AD user discovery**. It isn't required to create the CMG, but required if you plan to use Azure AD authentication with hybrid identities. For more information, see [Install clients using Azure AD](../../deploy/deploy-clients-cmg-azure.md) and see [About Azure AD user discovery](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc).

- An **Azure administrator** needs to participate in the initial creation of certain components. This persona can be the same as the Configuration Manager administrator, or separate. If separate, they don't require permissions in Configuration Manager.

  - When you integrate the site with Azure AD for deploying the CMG using Azure Resource Manager, you need a **Global Administrator**.

  - When you create the CMG, you need an account that is an Azure **Subscription Owner** and an Azure AD **Global Administrator**.

- Your user account needs to be a **Full administrator** or **Infrastructure administrator** in Configuration Manager.<!-- SCCMDocs#2146 -->

- At least one on-premises Windows server to host the **CMG connection point**. You can colocate this role with other Configuration Manager site system roles.

- The **service connection point** must be in [online mode](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).

- Configure the **management point** to allow traffic from the CMG. It also needs to require HTTPS, or configure the site for [Enhanced HTTP](../../../plan-design/hierarchy/enhanced-http.md).

- A [**server authentication certificate**](server-auth-cert.md) for the CMG.

- **Other certificates** may be required, depending upon your client OS version and authentication model. For more information, see [Configure client authentication](configure-authentication.md).

- Clients must use **IPv4**.

- Make sure the following [client settings](../../deploy/about-client-settings.md#cloud-services) in the **Cloud services** group are enabled for devices that will use the CMG:

  - **Enable clients to use a cloud management gateway**
  - **Allow access to cloud distribution point**

  > [!NOTE]
  > If you enable the client setting to [Download delta content when available](../../deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available), the content for third-party updates won't download to clients.<!--6598587-->

## Next steps

Next, determine how clients will authenticate with the CMG:
  
> [!div class="nextstepaction"]
> [Plan for CMG client authentication](plan-client-authentication.md)
