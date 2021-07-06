---
title: Plan for cloud management gateway
titleSuffix: Configuration Manager
description: Plan and design the cloud management gateway (CMG) to simplify management of internet-based clients.
ms.date: 07/16/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.custom: contperf-fy21q1
---

# Plan for the cloud management gateway in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article provides information about the cloud management gateway (CMG) to design how it fits in your environment and plan your implementation.

For more foundational knowledge of CMG scenarios and use cases, see [Overview of CMG](overview.md).

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

  For more information, see [Client authentication methods](#client-authentication-methods).

- The CMG creates an **Azure storage account**, which it uses for its standard operations. By default, the CMG is also content-enabled to provide deployment content to internet-based clients. This storage account doesn't support customizations, such as virtual network restrictions.

  > [!NOTE]
  > The cloud-based distribution point (CDP) is deprecated. Starting in version 2107, you can't create new CDP instances. To provide content to internet-based devices, enable the CMG to distribute content.<!-- 10247883 -->

### Azure Resource Manager

<!-- 1324735 -->
You create the CMG using an **Azure Resource Manager deployment**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) is a modern platform for managing all solution resources as a single entity, called a [resource group](/azure/azure-resource-manager/resource-group-overview#resource-groups). When you deploy a CMG with Azure Resource Manager, the site uses Azure Active Directory (Azure AD) to authenticate and create the necessary cloud resources.

> [!NOTE]
> CMG deployments with the **cloud service (classic)** method don't support subscriptions for Azure Cloud Service Providers (CSP). The CMG deployment with Azure Resource Manager continues to use the classic cloud service, which the CSP doesn't support. For more information, see [Azure services available in the Azure CSP program](/partner-center/azure-plan-available). In version 2006 and earlier, this deployment method is the only option.

### Virtual machine scale sets

> [!NOTE]
> This feature was first introduced in version 2010 as a [pre-release feature](../../../servers/manage/pre-release-features.md). Starting in version 2107, it's no longer a pre-release feature.

<!--3601040-->
Starting in version 2010, customers with a Cloud Solution Provider (CSP) subscription can deploy the CMG with a **virtual machine scale set** in Azure. This support is only if they don't currently have a CMG deployed using classic cloud services to another subscription.

Starting in version 2107, all customers can deploy a CMG with a virtual machine scale set. If you have an existing CMG deployed with the classic cloud service, **convert** the CMG to use a virtual machine scale set.<!-- 8959690 -->

With a few exceptions, the configuration, operation, and functionality of the CMG remains the same.

- Other [Azure resource providers](configure-azure-ad.md#configure-azure-resource-providers) in your Azure subscription.

- Different deployment names, for example, **GraniteFalls.EastUS.CloudApp.Azure.Com** for a deployment in the **East US** Azure region. This name change can affect how you create and manage the [CMG server authentication certificate](server-auth-cert.md).

- The CMG connection point only communicates with the virtual machine scale set in Azure over HTTPS. It doesn't require TCP-TLS ports.

#### Limitations for a CMG with a virtual machine scale set

##### Limitations with versions 2010 and 2103

- If you require more than one CMG instance, they all have to use the same deployment method.
- The supported number of concurrent client connections is 2,000 per VM instance. For more information, see [Performance and scale](#performance-and-scale).
- It's only supported with a standalone primary site.
- It doesn't support Azure US Government Cloud environments.
- Users may experience a delay of up to three seconds for actions in Software Center.
- Configuration Manager currently creates the Azure storage container based on the name of the resource group. Azure has different naming requirements for resource groups and storage containers. Make sure the name of the resource group for this service only has lowercase letters, numbers, and hyphens. If you have an existing resource group that doesn't work, rename it in the Azure portal, or create a new resource group.<!-- 8888841 -->
- If you have more than one HTTPS management point, then you can't install the Configuration Manager client on devices over the internet. If you need to [Install off-premises clients using a CMG](configure-clients.md#install-off-premises-clients-using-a-cmg), then you can only have one HTTPS management point. You also need to enable the CMG for content.<!-- 9760068 -->

##### Limitations with versions 2107

- It doesn't support Azure US Government Cloud environments.
- Users may experience a delay of up to three seconds for actions in Software Center.
- Configuration Manager currently creates the Azure storage container based on the name of the resource group. Azure has different naming requirements for resource groups and storage containers. Make sure the name of the resource group for this service only has lowercase letters, numbers, and hyphens. If you have an existing resource group that doesn't work, rename it in the Azure portal, or create a new resource group.<!-- 8888841 -->
- If you have more than one HTTPS management point, then you can't install the Configuration Manager client on devices over the internet. If you need to [Install off-premises clients using a CMG](configure-clients.md#install-off-premises-clients-using-a-cmg), then you can only have one HTTPS management point. You also need to enable the CMG for content.<!-- 9760068 -->

### Client authentication methods

Because these clients are potentially connecting to the service from the untrusted public internet, they have a higher authentication requirement. There are three options for identity and authentication:

- Azure AD
- PKI certificates
- Configuration Manager site-issued tokens

The following table summarizes the key factors for each method:

|         | Azure AD | PKI certificate | Site token |
|---------|---------|---------|---------|
| **ConfigMgr version** | All supported | All supported | All supported |
| **Windows client version** | Windows 10 | All supported | All supported |
| **Scenario support** | User and device | Device-only | Device-only |
| **Management point** | E-HTTP or HTTPS | E-HTTP or HTTPS | E-HTTP or HTTPS |

Microsoft recommends joining devices to Azure AD. Internet-based devices can use Azure AD modern authentication with Configuration Manager. It also enables both device and user scenarios whether the device is on the internet or connected to the internal network.

You can use one or more methods. All clients don't have to use the same method.

Which ever method you choose, you may also need to reconfigure one or more management points. For more information, see [Configure client authentication for CMG](configure-authentication.md#enable-management-point-for-https).

#### Azure AD

If your internet-based devices are running Windows 10, consider using Azure AD modern authentication with the CMG. This authentication method is the only one that enables user-centric scenarios. For example, deploying apps to a user collection.

First, the devices need to be either cloud domain-joined or hybrid Azure AD-joined, and the user also needs an Azure AD identity. If your organization is already using Azure AD identities, then you should be set with this prerequisite. If not, talk with your Azure administrator to plan for cloud-based identities. For more information, see [Azure AD device identity](/azure/active-directory/devices/). Until that process is complete, consider [token-based authentication](#site-token) for internet-based clients with your CMG.

There are a few other requirements, depending upon your environment:

- Enable user discovery methods for hybrid identities
- Enable ASP.NET 4.5 on the management point
- Configure client settings

For more information on these prerequisites, see [Install clients using Azure AD](../../deploy/deploy-clients-cmg-azure.md).

> [!NOTE]
> If your devices are in an Azure AD tenant that's separate from the tenant with a subscription for the CMG compute resources, starting in version 2010 you can disable authentication for tenants not associated with users and devices. For more information, see [Configure Azure services](../../../servers/deploy/configure/azure-services-wizard.md#disable-authentication).<!--8537319-->

#### PKI certificate

If you have a public key infrastructure (PKI) that can issue client authentication certificates to devices, then consider this authentication method for internet-based devices with your CMG. It doesn't support user-centric scenarios, but supports devices running Windows 8.1 or Windows 10.

> [!TIP]
> Windows 10 devices that are hybrid or cloud domain-joined don't require this certificate because they use [Azure AD](#azure-ad) to authenticate.

This certificate may also be required on the CMG connection point.

#### Site token

If you can't join devices to Azure AD or use PKI client authentication certificates, then use Configuration Manager token-based authentication. Site-issued client authentication tokens work on all supported client OS versions, but only support device scenarios.

If clients occasionally connect to your internal network, they're automatically issued a token. They need to communicate directly with an on-premises management point to register with the site and get this client token.

If you can't register clients on the internal network, you can create and deploy a bulk registration token. The bulk registration token enables the client to initially install and communicate with the site. This initial communication is long enough for the site to issue the client its own, unique client authentication token. The client then uses its authentication token for all communication with the site while it's on the internet.

## Hierarchy design

Create the CMG at the top-tier site of your hierarchy. If that's a central administration site (CAS), then create CMG connection points at child primary sites. The cloud service manager component is on the service connection point, which is also on the CAS. This design can share the service across different primary sites if needed.

You can create multiple CMG services in Azure, and you can create multiple CMG connection points. Multiple CMG connection points provide load balancing of client traffic from the CMG to the on-premises roles.

You can associate a CMG with a boundary group. This configuration allows clients to default or fall back to the CMG for client communication according to [boundary group relationships](../../../servers/deploy/configure/boundary-groups.md). This behavior is especially useful in branch office and VPN scenarios. You can direct client traffic away from expensive and slow WAN links to instead use faster services in Microsoft Azure.<!--3640932-->

Starting in version 2006, intranet clients can access a CMG-enabled software update point when it's assigned to a boundary group. For more information, see [Configure boundary groups](../../../servers/deploy/configure/boundary-groups.md#bkmk_cmg-sup). <!--7102873-->

> [!NOTE]
> Internet-based clients don't fall into any boundary group.

Other factors, such as the number of clients to manage, also affect your CMG design. For more information, see [Performance and scale](#performance-and-scale).

### Design examples

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

For more information, see the following FAQ: [Do the user accounts have to be in the same Azure AD tenant as the tenant associated with the subscription that hosts the CMG cloud service?](./cloud-management-gateway-faq.yml#do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service-)

## Requirements

> [!TIP]
> To clarify some Azure terminology:
>
> - The _tenant_ is the directory of user accounts and app registrations. One tenant can have multiple subscriptions.
> - A _subscription_ separates billing, resources, and services. It's associated with a single tenant.

- An **Azure subscription** to host the CMG. This subscription can be in one of the following environments:

  - Global Azure cloud
  - Azure US Government cloud

  Customers with a Cloud Service Provider (CSP) subscription need to use version 2010 or later with a **virtual machine scale set** deployment.<!--3601040-->

- Integrate the site with **Azure AD** to deploy the service with Azure Resource Manager. For more information, see [Configure Azure AD for CMG](configure-azure-ad.md).

  When you onboard the site to Azure AD, you can optionally enable **Azure AD user discovery**. It isn't required to create the CMG, but required if you plan to use Azure AD authentication with hybrid identities. For more information, see [Install clients using Azure AD](../../deploy/deploy-clients-cmg-azure.md) and see [About Azure AD user discovery](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc).

- An **Azure administrator** needs to participate in the initial creation of certain components. This persona can be the same as the Configuration Manager administrator, or separate. If separate, they don't require permissions in Configuration Manager.

  - When you integrate the site with Azure AD for deploying the CMG using Azure Resource Manager, you need a **Global Administrator**.

  - When you create the CMG, you need a **Subscription Owner**.

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

## Performance and scale

> [!NOTE]
> Sizing guidance for management points and software update points doesn't change whether they service on-premises or internet-based clients. For more information, see [Size and scale numbers](../../../plan-design/configs/size-and-scale-numbers.md).

### Size and scale for cloud management gateway

[!INCLUDE [Size and scale for cloud management gateway](../../../plan-design/configs/includes/scale-cmg.md)]

### Size and scale for cloud management gateway connection point

[!INCLUDE [Size and scale for cloud management gateway connection point](../../../plan-design/configs/includes/scale-cmgcp.md)]

### Improve CMG performance

The following recommendations can help you improve CMG performance:

- The connection between the Configuration Manager client and the CMG isn't region-aware. Client communication is largely unaffected by latency and geographic separation. It's generally not necessary to deploy multiple CMG for the purposes of geo-proximity. Deploy the CMG at the top-level site in your hierarchy. To increase scale, add VM instances.

- For high availability of the service, create a CMG with at least two VM instances and two CMG connection points per site.

- Scale the CMG to support more clients by adding more VM instances. The Azure load balancer controls client connections to the service.

- Create more CMG connection points to distribute the load among them. The CMG distributes the traffic to its connecting CMG connection points in a round-robin fashion.

> [!NOTE]
> The CMG connection point creates a TCP connection to the management point for each client. While Configuration Manager has no hard limit on the number of clients for a CMG connection point, Windows Server has a default maximum TCP dynamic port range of 16,384. If a Configuration Manager site manages more than 16,384 clients with a single CMG connection point, add another site system or increase the Windows Server limit. All clients maintain a channel for client notifications, which holds a port open on the CMG connection point. For more information on how to increase this limit, see [Microsoft Support article 929851](https://support.microsoft.com/help/929851).

## Next steps

Next, review the features and configurations that the CMG supports:
  
> [!div class="nextstepaction"]
> [Supported configurations for CMG](supported-configurations.md)
