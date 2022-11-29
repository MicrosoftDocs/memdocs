---
title: Cloud distribution point
titleSuffix: Configuration Manager
description: Plan and design for distributing software content through Microsoft Azure with cloud distribution points in Configuration Manager.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Use a cloud distribution point in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!WARNING]
> The implementation for sharing content from Azure has changed. Use a content-enabled cloud management gateway by enabling the option to **Allow CMG to function as a cloud distribution point and serve content from Azure storage**. For more information, see [Modify a CMG](../../clients/manage/cmg/modify-cloud-management-gateway.md).
>
> Starting in version 2107, you can't create a traditional cloud distribution point (CDP).<!-- 10247883 -->

A cloud distribution point is a Configuration Manager distribution point that is hosted as Platform-as-a-Service (PaaS) in Microsoft Azure. This service supports the following scenarios:  

- Provide software content to internet-based clients without additional on-premises infrastructure  

- Cloud-enable your content distribution system  

- Reduce the need for traditional distribution points  

This article helps you learn about the cloud distribution point, plan for its use, and design your implementation. It includes the following sections:

- [Features and benefits](#bkmk_features)
- [Topology design](#bkmk_topology)
- [Requirements](#bkmk_requirements)
- [Specifications](#bkmk_spec)
- [Cost](#bkmk_cost)
- [Performance and scale](#bkmk_perf)
- [Ports and data flow](#bkmk_dataflow)
- [Certificates](#bkmk_certs)
- [Frequently asked questions (FAQ)](#bkmk_faq)


## <a name="bkmk_features"></a> Features and benefits

### Features

The cloud distribution point supports several features that are also offered by on-premises distribution points:  

- Manage cloud distribution points individually or as members of distribution point groups  

- Use a cloud distribution point as a fallback content location  

- Supports both intranet and internet-based clients  

### Benefits

The cloud distribution point provides the following additional benefits:  

- The site encrypts the content before sending it to the cloud distribution point in Azure.  

- To meet changing demands for content requests by clients, manually scale the cloud service in Azure. This action doesn't require that you install and provision additional distribution points in Configuration Manager.  

- Supports content download from clients configured for other content technologies, such as Windows BranchCache.  

- Use cloud distribution points as source locations for pull-distribution points.  


## <a name="bkmk_topology"></a> Topology design

Deployment and operation of the cloud distribution point includes the following components:  

- A **cloud service** in Azure. The site distributes content to this service, which stores it in Azure cloud storage. The management point provides to clients this content location in the list of available sources as appropriate.  

- A **management point** site system role services client requests per normal.  

    - On-premises clients typically use an on-premises management point.  

    - Internet-based clients either use a [cloud management gateway](../../clients/manage/cmg/overview.md), or an [internet-based management point](../../clients/manage/plan-internet-based-client-management.md).  

- The cloud distribution point uses a **certificate-based HTTPS** web service to help secure network communication with clients. Clients must trust this certificate.  

### Azure Resource Manager

<!--1322209-->
Create a cloud distribution point using an **Azure Resource Manager deployment**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) is a modern platform for managing all solution resources as a single entity, called a [resource group](/azure/azure-resource-manager/resource-group-overview#resource-groups). When deploying a cloud distribution point with Azure Resource Manager, the site uses Azure Active Directory (Azure AD) to authenticate and create the necessary cloud resources.

> [!Note]  
> This feature doesn't enable support for Azure Cloud Service Providers (CSP). The cloud distribution point deployment with Azure Resource Manager continues to use the classic cloud service, which the CSP doesn't support. For more information, see [available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

Azure Resource Manager is the only deployment mechanism for new instances of the cloud distribution point. Existing deployments continue to work.<!-- 3605704 -->

### Hierarchy design

Where you create the cloud distribution point depends upon which clients need to access the content.

- Azure Resource Manager deployment: Create this type at a primary site or the central administration site.  

- The cloud management gateway (CMG) can also serve content to clients. This functionality reduces the required certificates and cost of Azure VMs. For more information, see [Overview of cloud management gateway](../../clients/manage/cmg/overview.md).<!--1358651-->  

To determine whether to include cloud distribution points in boundary groups, consider the following behaviors:  

- Internet-based clients don't rely on boundary groups. They only use internet-facing distribution points or cloud distribution points. If you're only using cloud distribution points to service these types of clients, then you don't need to include them in boundary groups.  

- If you want clients on your internal network to use a cloud distribution point, then it needs to be in the same boundary group as the clients. Clients prioritize cloud distribution points last in their list of content sources, because there's a cost associated with downloading content out of Azure. So a cloud distribution point is typically used as a fallback source for intranet-based clients. If you want a cloud-first design, then design your boundary groups to meet this business requirement. For more information, see [Configure boundary groups](../../servers/deploy/configure/boundary-groups.md).  

Even though you install cloud distribution points in specific regions of Azure, clients aren't aware of the Azure regions. They randomly select a cloud distribution point. If you install cloud distribution points in multiple regions, and a client receives more than one in the content location list, the client might not use a cloud distribution point from the same Azure region.  

### Backup and recovery  

When you use a cloud distribution point in your hierarchy, use the following information to help you plan for backup and recovery:  

- When you use the **Backup Site Server** maintenance task, Configuration Manager automatically includes the configurations for the cloud distribution point.  

- Back up and save a copy of the server authentication certificate. When you restore the Configuration Manager primary site to a different server, reimport the certificate.


## <a name="bkmk_requirements"></a> Requirements

- You need an **Azure subscription** to host the service.  

    - An **Azure administrator** needs to participate in the initial creation of certain components, depending upon your design. This persona doesn't require permissions in Configuration Manager.  

- The site server requires **internet access** to deploy and manage the cloud service.  

- When using the **Azure Resource Manager** deployment method, integrate Configuration Manager with [Azure AD](../../servers/deploy/configure/azure-services-wizard.md) for **Cloud Management**. Azure AD *user discovery* isn't required.  

- A **server authentication certificate**. For more information, see the [Certificates](#bkmk_certs) section below.  

    - To reduce complexity, use a public certificate provider for the server authentication certificate. When doing so, you also need a **DNS CNAME alias** for clients to resolve the name of the cloud service.  

- Set the client setting, **Allow access to cloud distribution points**, to **Yes** in the **Cloud Services** group. By default, this value is set to **No**.  

- Client devices require **internet connectivity**, and must use **IPv4**.  


## <a name="bkmk_spec"></a> Specifications

- The cloud distribution point supports all Windows versions listed in [Supported operating systems for clients and devices](../configs/supported-operating-systems-for-clients-and-devices.md).  

- An administrator distributes the following types of supported software content:  
  - Applications
  - Packages
  - OS upgrade packages
  - Third-party software updates  

    > [!Important]  
    > - While the Configuration Manager console doesn't block the distribution of Microsoft software updates to a cloud distribution point, you're paying Azure costs to store content that clients don't use. Internet-based clients always get Microsoft software update content from the Microsoft Update cloud service. Don't distribute Microsoft software updates to a cloud distribution point.
    > - When using a CMG for content storage, the content for third-party updates won't download to clients if the **Download delta content when available** [client setting](../../clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) is enabled. <!--6598587--> 

- Configure a pull-distribution point to use a cloud distribution point as a source. For more information, see [About source distribution points](use-a-pull-distribution-point.md#about-source-distribution-points).<!--1321554-->  

### Deployment settings

- **Download content locally when needed by the running task sequence**. The task sequence engine can download packages on-demand from a content-enabled CMG or a cloud distribution point. This option provides additional flexibility with your Windows in-place upgrade deployments to internet-based devices.

- **Download all content locally before starting task sequence**. With this option, the Configuration Manager client downloads the content from the cloud source before starting the task sequence.

- A cloud distribution point doesn't support package deployments with the option to **Run program from distribution point**. Use the deployment option to **Download content from distribution point and run locally**.  

### Limitations  

- You can't use a cloud distribution point for PXE or multicast-enabled deployments.  

- A cloud distribution point doesn't support App-V streaming applications.  

- A cloud distribution point doesn't support content for Microsoft 365 Apps updates. <!--7366753-->

- You can't [prestage content](manage-network-bandwidth.md#BKMK_PrestagingContent) on a cloud distribution point. The distribution manager of the primary site that manages the cloud distribution point transfers all content.  

- You can't configure a cloud distribution point as a pull-distribution point.  


## <a name="bkmk_cost"></a> Cost

<!--501018-->
> [!IMPORTANT]  
> The following cost information is for estimating purposes only. Your environment may have other variables that affect the overall cost of using a cloud distribution point.  

Configuration Manager includes the following options to help control costs and monitor data access:  

- Control and monitor the amount of content that you store in a cloud service. For more information, see [Monitor cloud distribution points](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- Configure Configuration Manager to alert you when thresholds for client downloads meet or exceed monthly limits. For more information, see [Data transfer threshold alerts](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_alerts).

- To help reduce the number of data transfers from cloud distribution points by clients, use one of the following peer caching technologies:  
  - Configuration Manager peer cache
  - Windows BranchCache
  - Windows Delivery Optimization  

    For more information, see [Fundamental concepts for content management](fundamental-concepts-for-content-management.md).  

### Components

A cloud distribution point uses the following Azure components, which incur charges to the Azure subscription account:  

> [!Tip]  
> The cloud management gateway can also serve content to clients. This functionality reduces the cost by consolidating the Azure VMs. For more information, see [Cost for cloud management gateway](../../clients/manage/cmg/cost.md).  

#### Virtual machine

- The cloud distribution point uses Azure Cloud Services as platform as a service (PaaS). This service uses virtual machines (VMs) that incur compute costs.  

- Each cloud distribution point service uses two Standard A0 VMs.  

- See the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/) to help determine potential costs.

    > [!NOTE]  
    > Virtual machine costs vary by region.

#### Outbound data transfer

- Any dataflows into Azure are free (ingress or upload). Distributing content from the site to the cloud distribution point is uploading to Azure.  

- Charges are based on data flowing out of Azure (egress or download). Cloud distribution point dataflows out of Azure consist of the software content that clients download.  

- For more information, see [Monitor cloud distribution points](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- See the [Azure bandwidth pricing details](https://azure.microsoft.com/pricing/details/bandwidth/) to help determine potential costs. Pricing for data transfer is tiered. The more you use, the less you pay per gigabyte.  

#### Content storage

- Internet-based clients get Microsoft software update content from the Microsoft Update cloud service at no charge. Don't distribute software update deployment packages with Microsoft software updates to a cloud distribution point. Otherwise, you'll incur data storage costs for content that clients never use.  

- Cloud distribution points with an Azure Resource Manager deployment use Azure locally redundant storage (LRS). For more information, see [Locally redundant storage](/azure/storage/common/storage-redundancy-lrs).

#### Other costs

- Each cloud service has a dynamic IP address. Each distinct cloud distribution point uses a new dynamic IP address. Adding additional VMs per cloud service doesn't increase these addresses.  


## <a name="bkmk_dataflow"></a> Ports and data flow

There are two primary data flows for the cloud distribution point:  

- The site server connects to Azure to set up the cloud distribution point service  

- A client connects to the cloud distribution point to download content  

### Site server to Azure

You don't need to open any inbound ports to your on-premises network. The site server initiates all communication with Azure and the cloud distribution point to deploy, update, and manage the cloud service. The site server needs to create outbound connections to the Microsoft cloud. This action is equivalent to installing the distribution point site system role on a specific site.  

### Client to cloud distribution point

You don't need to open any inbound ports to your on-premises network. Internet-based clients communicate directly with the Azure service. Clients on your internal network that use a cloud distribution point need to connect to the Microsoft cloud.

For more information on content location priority and when intranet-based clients use a cloud distribution point, see [Content source priority](fundamental-concepts-for-content-management.md#content-source-priority).

When a client uses a cloud distribution point as a content location:  

1. The management point gives the client an access token along with the list of content sources. This token is valid for 24 hours, and gives the client access to the cloud distribution point.  

2. The management point responds to the client's location request with the **Service FQDN** of the cloud distribution point. This property is the same as the common name of the server authentication certificate.  

    If you're using your domain name, for example, WallaceFalls.contoso.com, then the client first tries to resolve this FQDN. You need a CNAME alias in your domain's internet-facing DNS for clients to resolve the Azure service name, for example: WallaceFalls.cloudapp.net.  

3. The client next resolves the Azure service name, for example, WallaceFalls.cloudapp.net, to a valid IP address. This response should be handled by Azure's DNS.  

4. The client connects to the cloud distribution point. Azure load balances the connection to one of the VM instances. The client authenticates itself using the access token.  

5. The cloud distribution point authenticates the client's access token, and then gives the client the exact content location in Azure storage.  

6. If the client trusts the cloud distribution point's server authentication certificate, it connects to Azure storage to download the content.


## <a name="bkmk_perf"></a> Performance and scale

<!--494872-->

As with any distribution point design, consider the following factors:  

- Number of concurrent client connections
- The size of the content that clients download
- The length of time allowed to meet your business requirements

Depending upon your [topology design](#bkmk_topology), if clients have the option of more than one cloud distribution point for any given content, then they naturally randomize across those cloud services. If you only distribute a certain piece of content to a single cloud distribution point, and a large number of clients try to download this content at the same time, this activity puts higher load on that single cloud distribution point. Adding an additional cloud distribution point also includes a separate Azure storage service. For more information on how the client communicates with the cloud distribution point components and downloads content, see [Ports and data flow](#bkmk_dataflow).  

The cloud distribution point uses two Azure VMs as the front end to the Azure storage. This default deployment meets most customer's needs. In some extreme circumstances, with a large number of concurrent client connections (for example, 150,000 clients), the processing capacity of the Azure VMs can't keep up with the client requests. You can't resize the Azure VMs used for the cloud distribution point. While you can't configure the number of VM instances for the cloud distribution point in Configuration Manager, if necessary, reconfigure the cloud service in the Azure portal. Either manually add more VM instances, or configure the service to automatically scale.

> [!Important]  
> When you update Configuration Manager, the site redeploys the cloud service. If you manually reconfigure the cloud service in the Azure portal, the number of instances resets to the default of two.  

The Azure storage service supports 500 requests per second for a single file. Performance testing of a single cloud distribution point supported distribution of a single 100-MB file to 50,000 clients in 24 hours.<!--512106-->  


## <a name="bkmk_certs"></a> Certificates  

Depending upon your cloud distribution point design, you need one or more digital certificates.  

### General information

<!--SCCMDocs issue #779-->
Certificates for cloud distribution points support the following configurations:  

- 4096-bit key length

- Version 3 certificates. For more information, see [CNG certificates overview](../network/cng-certificates-overview.md).  

- When you configure Windows with the following policy: **System cryptography: Use FIPS compliant algorithms for encryption, hashing, and signing**  

- Support for TLS 1.2. For more information, see [Cryptographic controls technical reference](../security/cryptographic-controls-technical-reference.md#about-ssl-vulnerabilities).  

### Server authentication certificate

*This certificate is required for all cloud distribution point deployments.*

For more information, see [CMG server authentication certificate](../../clients/manage/cmg/server-auth-cert.md), and the following subsections, as necessary:  

- CMG trusted root certificate to clients
- Server authentication certificate issued by public provider
- Server authentication certificate issued from enterprise PKI

The cloud distribution point uses this type of certificate in the same way as the cloud management gateway. Clients also need to trust this certificate. To reduce complexity, Microsoft recommends using a certificate issued by a public provider.

Unless you use a wildcard certificate, don't reuse the same certificate. Each instance of the cloud distribution point and cloud management gateway requires a unique server authentication certificate.

For more information on creating this certificate from a PKI, see [Deploy the service certificate for cloud distribution points](../network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).  

## <a name="bkmk_faq"></a> Frequently asked questions (FAQ)

### Does a client need a certificate to download content from a cloud distribution point?

A client authentication certificate isn't required. The client does need to trust the server authentication certificate used by the cloud distribution point. If this certificate is issued by a public certificate provider, then most Windows devices already include trusted root certificates for these providers. If you issued a server authentication certificate from your organization's PKI, then your clients need to trust the issuing certificates in the entire chain. This chain includes the root certificate authority, and any intermediate certificate authorities. Depending upon your PKI design, this certificate can introduce additional complexity to the deployment of the cloud distribution point. To avoid this complexity, Microsoft recommends using a public certificate provider that your clients already trust.  

### Can my on-premises clients use a cloud distribution point?

Yes. If you want clients on your internal network to use a cloud distribution point, then it needs to be in the same boundary group as the clients. Clients prioritize cloud distribution points last in their list of content sources, because there's a cost associated with downloading content out of Azure. Thus, a cloud distribution point is typically used as a fallback source for intranet-based clients. If you want a cloud-first design, then design your boundary groups accordingly. For more information, see [Configure boundary groups](../../servers/deploy/configure/boundary-groups.md).  

### Do I need Azure ExpressRoute?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) lets you extend your on-premises network into the Microsoft cloud. ExpressRoute, or other such virtual network connections aren't required for the Configuration Manager cloud distribution point.  

If your organization uses ExpressRoute, isolate the Azure subscription for the cloud distribution point from the subscription that uses ExpressRoute. This configuration ensures that the cloud distribution point isn't accidentally connected in this manner.  

### Do I need to maintain the Azure virtual machines?

No maintenance is required. The design of the cloud distribution point uses Azure platform as a service (PaaS). Using the subscription you provide, Configuration Manager creates the necessary VMs, storage, and networking. Azure secures and updates the virtual machines. These VMs aren't a part of your on-premises environment, as is the case with infrastructure as a service (IaaS). The cloud distribution point is a PaaS that extends your Configuration Manager environment into the cloud. For more information, see [Security advantages of a PaaS cloud service model](/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model).  

### Does the cloud distribution point use Azure CDN?

The Azure Content Delivery Network (CDN) is a global solution for rapidly delivering high-bandwidth content by caching the content at strategically placed physical nodes across the world. For more information, see [What is Azure CDN?](/azure/cdn/cdn-overview).

The Configuration Manager cloud distribution point currently doesn't support Azure CDN.


## Next steps

[Install cloud distribution points](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)
