---
title: Plan for cloud management gateway
titleSuffix: Configuration Manager
description: Plan and design the cloud management gateway (CMG) to simplify management of internet-based clients.
ms.date: 04/14/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.custom: contperf-fy21q1
---

# Plan for the cloud management gateway in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article provides information about the cloud management gateway (CMG) to design how it fits in your environment and plan your implementation.

For more foundational knowledge of CMG scenarios and use cases, see [Overview of CMG](overview.md).

> [!NOTE]
> Some sections that were previously in this article have moved:
>
> - **Scenarios**: [CMG overview](overview.md)
> - **Specifications**: [Supported configurations for CMG](supported-configurations.md)
> - **Cost**: [Cost of CMG](cost.md)
> - **Ports and data flow**: [Data flow for CMG](data-flow.md)

## Topology design

### CMG components

Deployment and operation of the CMG includes the following components:

- The **CMG cloud service** in Azure authenticates and forwards Configuration Manager client requests over the internet to the on-premises CMG connection point.

- The **CMG connection point** site system role enables a consistent and high-performance connection from the on-premises network to the CMG service in Azure. It also publishes settings to the CMG including connection information and security settings. The CMG connection point forwards client requests from the CMG to on-premises roles according to URL mappings. For example, the management point and software update point.

- The [**service connection point**](../../../servers/deploy/configure/about-the-service-connection-point.md) site system role runs the cloud service manager component, which handles all CMG deployment tasks. Additionally, it monitors and reports service health and logging information from Azure Active Directory (Azure AD). Make sure your service connection point is in [online mode](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).

- The **management point** and **software update point** site system roles service client requests per normal.

- The CMG uses a **certificate-based HTTPS** web service to help secure network communication with clients.

- **Internet-based clients** connect to the CMG to access on-premises Configuration Manager components. Clients have multiple options for identity and authentication:

  - Azure AD
  - PKI certificates
  - Configuration Manager site-issued tokens

- A content-enabled CMG or a [**cloud distribution point**](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) provides content to internet-based clients, as needed. Using a content-enabled CMG reduces the required certificates and Azure costs.

> [!NOTE]
> When you deploy a CMG, it also creates an Azure storage account. The CMG uses this storage account for its standard operations, and for content distribution if you enable it. This storage account doesn't support customizations, such as virtual network restrictions.

### Azure Resource Manager

<!-- 1324735 -->
You create the CMG using an **Azure Resource Manager deployment**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) is a modern platform for managing all solution resources as a single entity, called a [resource group](/azure/azure-resource-manager/resource-group-overview#resource-groups). When you deploy CMG with Azure Resource Manager, the site uses Azure Active Directory (Azure AD) to authenticate and create the necessary cloud resources.

> [!NOTE]
> CMG deployments with the **cloud service (classic)** method don't support subscriptions for Azure Cloud Service Providers (CSP). The CMG deployment with Azure Resource Manager continues to use the classic cloud service, which the CSP doesn't support. For more information, see [Azure services available in the Azure CSP program](/partner-center/azure-plan-available). In version 2006 and earlier, this deployment method is the only option.

### Virtual machine scale sets

> [!NOTE]
> In this version of Configuration Manager, a CMG with a virtual machine scale set is a pre-release feature. To enable it, see [Pre-release features](../../../servers/manage/pre-release-features.md).

<!--3601040-->
Starting in version 2010, customers with a Cloud Solution Provider (CSP) subscription can deploy the CMG with a **virtual machine scale set** in Azure. This support is only if they don't currently have a CMG deployed using classic cloud services to another subscription. With a few exceptions, the configuration, operation, and functionality of the CMG remains the same.

- Additional [Azure resource providers](configure-azure-ad.md#configure-azure-resource-providers) in your Azure subscription.

- Different deployment names, for example, **GraniteFalls.EastUS.CloudApp.Azure.Com** for a deployment in the **East US** Azure region. For more information, see [CMG server authentication certificate](server-auth-cert.md).

- The CMG connection point only communicates with the virtual machine scale set in Azure over HTTPS. It doesn't require TCP-TLS ports. For more information, see [Ports and data flow](data-flow.md).

> [!IMPORTANT]
> If you've already deployed a CMG, you don't need to make any change at this time.

#### Current limitations for a CMG with a virtual machine scale set

- If you require more than one CMG instance, they all have to use the same deployment method.
- The supported number of concurrent client connections is 2,000 per VM instance. For more information, see [Performance and scale](#performance-and-scale).
- It's only supported with a standalone primary site.
- It doesn't support Azure US Government Cloud environments.
- Users may experience a delay of up to three seconds for actions in Software Center.
- Configuration Manager currently creates the Azure storage container based on the name of the resource group. Azure has different naming requirements for resource groups and storage containers. Make sure the name of the resource group for this service only has lowercase letters, numbers, and hyphens. If you have an existing resource group that doesn't work, rename it in the Azure portal, or create a new resource group.<!-- 8888841 -->

### Hierarchy design

Create the CMG at the top-tier site of your hierarchy. If that's a central administration site (CAS), then create CMG connection points at child primary sites. The cloud service manager component is on the service connection point, which is also on the CAS. This design can share the service across different primary sites if needed.

You can create multiple CMG services in Azure, and you can create multiple CMG connection points. Multiple CMG connection points provide load balancing of client traffic from the CMG to the on-premises roles.

You can associate a CMG with a boundary group. This configuration allows clients to default or fall back to the CMG for client communication according to [boundary group relationships](../../../servers/deploy/configure/boundary-groups.md). This behavior is especially useful in branch office and VPN scenarios. You can direct client traffic away from expensive and slow WAN links to instead use faster services in Microsoft Azure.<!--3640932-->

Starting in version 2006, intranet clients can access a CMG-enabled software update point when it's assigned to a boundary group. For more information, see [Configure boundary groups](../../../servers/deploy/configure/boundary-groups.md#bkmk_cmg-sup). <!--7102873-->

> [!NOTE]
> Internet-based clients don't fall into any boundary group.

Other factors, such as the number of clients to manage, also impact your CMG design. For more information, see [Performance and scale](#performance-and-scale).

#### Example 1: Standalone primary site

Contoso has a standalone primary site in an on-premises datacenter at their headquarters in New York City.

- They create a CMG in the East US Azure region to reduce network latency.
- They create two CMG connection points, both linked to the single CMG service.

As clients roam onto the internet, they communicate with the CMG in the East US Azure region. The CMG forwards this communication through both of the CMG connection points.

#### Example 2: Hierarchy

Fourth Coffee has a CAS in an on-premises datacenter at their headquarters in Seattle. One primary site is in the same datacenter, and the other primary site is in their main European office in Paris.

- On the CAS, they create a CMG service in the West US Azure region. They scale the number of VMs for the expected load of roaming clients in the entire hierarchy.
- On the Seattle-based primary site, they create a CMG connection point linked to the single CMG.
- On the Paris-based primary site, they create a CMG connection point linked to the single CMG.

As clients roam onto the internet, they communicate with the CMG in the West US Azure region. The CMG forwards this communication to the CMG connection point in the client's assigned primary site.

> [!TIP]
> You don't need to deploy more than one CMG for the purposes of geolocation. The Configuration Manager client is mostly unaffected by the slight latency that can occur with the cloud service, even when geographically distant.

### Test environments
<!-- SCCMDocs#1225 -->
Many organizations have separate environments for production, test, development, or quality assurance. When you plan your CMG deployment, consider the following questions:

- How many Azure AD tenants does your organization have?
  - Is there a separate tenant for testing?
  - Are user and device identities in the same tenant?

- How many subscriptions are in each tenant?
  - Are there subscriptions that are specific for testing?

Configuration Manager's Azure service for **Cloud management** supports multiple tenants. Multiple Configuration Manager sites can connect to the same tenant. A single site can deploy multiple CMG services into different subscriptions. Multiple sites can deploy CMG services into the same subscription. Configuration Manager provides flexibility depending upon your environment and business requirements.

For more information, see the following FAQ: [Do the user accounts have to be in the same Azure AD tenant as the tenant associated with the subscription that hosts the CMG cloud service?](cloud-management-gateway-faq.md#bkmk_tenant)

## Requirements

> [!TIP]
> To clarify some Azure terminology:
>
> - The _tenant_ is the directory of user accounts and app registrations. One tenant can have multiple subscriptions.
> - A _subscription_ separates billing, resources, and services. It's associated with a single tenant.

- An **Azure subscription** to host the CMG.

    > [!IMPORTANT]
    > CMG deployments with the **cloud service (classic)** method don't support subscriptions with an Azure Cloud Service Provider (CSP).<!-- MEMDocs#320 --> In version 2006 and earlier, this deployment method is the only option.
    >
    > Starting in version 2010, customers with a Cloud Solution Provider (CSP) subscription can deploy the CMG with a **virtual machine scale set** in Azure.<!--3601040--> For more information, see [Topology design: Virtual machine scale sets](#virtual-machine-scale-sets).

- Your user account needs to be a **Full administrator** or **Infrastructure administrator** in Configuration Manager.<!-- SCCMDocs#2146 -->

- An **Azure administrator** needs to participate in the initial creation of certain components. This persona can be the same as the Configuration Manager administrator, or separate. If separate, they don't require permissions in Configuration Manager.

  - When you integrate the site with Azure AD for deploying the CMG using Azure Resource Manager, you need a **Global Administrator**.

  - When you create the CMG, you need a **Subscription Owner**.

- At least one on-premises Windows server to host the **CMG connection point**. You can colocate this role with other Configuration Manager site system roles.

- The **service connection point** must be in [online mode](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).

- A [**server authentication certificate**](server-auth-cert.md) for the CMG.

- Integrate the site with **Azure AD** to deploy the service with Azure Resource Manager. For more information, see [Configure Azure AD for CMG](configure-azure-ad.md).

- **Other certificates** may be required, depending upon your client OS version and authentication model. For more information, see [Configure client authentication](configure-authentication.md).

- Clients must use **IPv4**.

## Performance and scale

> [!NOTE]
> Sizing guidance for management points and software update points doesn't change whether they service on-premises or internet-based clients. For more information, see [Size and scale numbers](../../../plan-design/configs/size-and-scale-numbers.md).

### Size and scale for cloud management gateway

[!INCLUDE [Size and scale for cloud management gateway](../../../plan-design/configs/includes/scale-cmg.md)]

### Size and scale for cloud management gateway connection point

[!INCLUDE [Size and scale for cloud management gateway connection point](../../../plan-design/configs/includes/scale-cmgcp.md)]

### Improve CMG performance

The following recommendations can help you improve CMG performance:

- The connection between the Configuration Manager client and the CMG isn't region-aware. Client communication is largely unaffected by latency and geographic separation. It's not necessary to deploy multiple CMG for the purposes of geo-proximity. Deploy the CMG at the top-level site in your hierarchy. To increase scale, add VM instances.

- For high availability of the service, create a CMG with at least two VM instances and two CMG connection points per site.

- Scale the CMG to support more clients by adding more VM instances. The Azure load balancer controls client connections to the service.

- Create more CMG connection points to distribute the load among them. The CMG distributes the traffic to its connecting CMG connection points in a round-robin fashion.

> [!NOTE]
> While Configuration Manager has no hard limit on the number of clients for a CMG connection point, Windows Server has a default maximum TCP dynamic port range of 16,384. If a Configuration Manager site manages more than 16,384 clients with a single CMG connection point, increase the Windows Server limit. All clients maintain a channel for client notifications, which holds a port open on the CMG connection point. For more information on how to increase this limit, see [Microsoft Support article 929851](https://support.microsoft.com/help/929851).

## Next steps

Next, review the features and configurations that the CMG supports:
  
> [!div class="nextstepaction"]
> [Supported configurations for CMG](supported-configurations.md)
