---
title: Cloud distribution point
titleSuffix: Configuration Manager
description: Plan and design for distributing software content through Microsoft Azure with cloud distribution points in Configuration Manager.
ms.date: 09/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Use a cloud distribution point in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

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

-   Manage cloud distribution points individually or as members of distribution point groups  

-   Use a cloud distribution point as a fallback content location  

-   Supports both intranet and internet-based clients  


### Benefits

The cloud distribution point provides the following additional benefits:  

-   The site encrypts the content before sending it to the cloud distribution point in Azure.  

-   To meet changing demands for content requests by clients, manually scale the cloud service in Azure. This action doesn't require that you install and provision additional distribution points in Configuration Manager.  

-   Supports content download from clients configured for other content technologies, such as Windows BranchCache and alternate content providers.  

-   Starting in version 1806, use cloud distribution points as source locations for pull-distribution points.  


## <a name="bkmk_topology"></a> Topology design

Deployment and operation of the cloud distribution point includes the following components:  

- A **cloud service** in Azure. The site distributes content to this service, which stores it in Azure cloud storage. The management point provides to clients this content location in the list of available sources as appropriate.  

- A **management point** site system role services client requests per normal.  

    - On-premises clients typically use an on-premises management point.  

    - Internet-based clients either use a [cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway), or an [internet-based management point](/sccm/core/clients/manage/plan-internet-based-client-management).  

- The cloud distribution point uses a **certificate-based HTTPS** web service to help secure network communication with clients. Clients must trust this certificate.  


### Azure Resource Manager
<!--1322209-->
Starting in version 1806, create a cloud distribution point using an **Azure Resource Manager deployment**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) is a modern platform for managing all solution resources as a single entity, called a [resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). When deploying a cloud distribution point with Azure Resource Manager, the site uses Azure Active Directory (Azure AD) to authenticate and create the necessary cloud resources. This modernized deployment doesn't require the classic Azure management certificate.  

The cloud distribution point wizard still provides the option for a **classic service deployment** using an Azure management certificate. To simplify the deployment and management of resources, Microsoft recommends using the Azure Resource Manager deployment model for all new cloud distribution points. If possible, redeploy existing cloud distribution points through Resource Manager.

Configuration Manager doesn't migrate existing classic cloud distribution points to the Azure Resource Manager deployment model. Create new cloud distribution points using Azure Resource Manager deployments, and then remove classic cloud distribution points. 

> [!IMPORTANT]  
> This feature doesn't enable support for Azure Cloud Service Providers (CSP). The cloud distribution point deployment with Azure Resource Manager continues to use the classic cloud service, which the CSP doesn't support. For more information, see [available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### Hierarchy design

Where you create the cloud distribution point depends upon which clients need to access the content. Starting in version 1806, there are three types of cloud distribution points:  

- Classic service deployment: Create this type only at a primary site.  

- Azure Resource Manager deployment: Create this type at a primary site or the central administration site.  

- The cloud management gateway can also serve content to clients. This functionality reduces the required certificates and cost of Azure VMs. For more information, see [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).<!--1358651-->  


To determine whether to include cloud distribution points in boundary groups, consider the following behaviors:  

- Internet-based clients don't rely on boundary groups. They only use internet-facing distribution points or cloud distribution points. If you're only using cloud distribution points to service these types of clients, then you don't need to include them in boundary groups.  

- If you want clients on your internal network to use a cloud distribution point, then it needs to be in the same boundary group as the clients. Clients prioritize cloud distribution points last in their list of content sources, because there's a cost associated with downloading content out of Azure. So a cloud distribution point is typically used as a fallback source for intranet-based clients. If you want a cloud-first design, then design your boundary groups to meet this business requirement. For more information, see [Configure boundary groups](/sccm/core/servers/deploy/configure/boundary-groups).  


Even though you install cloud distribution points in specific regions of Azure, clients aren't aware of the Azure regions. They randomly select a cloud distribution point. If you install cloud distribution points in multiple regions, and a client receives more than one in the content location list, the client might not use a cloud distribution point from the same Azure region.  


### Backup and recovery  

When you use a cloud distribution point in your hierarchy, use the following information to help you plan for backup and recovery:  

- When you use the **Backup Site Server** maintenance task, Configuration Manager automatically includes the configurations for the cloud distribution point.  

- Back up and save a copy of the server authentication certificate. If you use the classic service deployment in Azure, also back up and save a copy of the Azure management certificate. When you restore the Configuration Manager primary site to a different server, you must reimport the certificates.  



##  <a name="bkmk_requirements"></a> Requirements

- You need an **Azure subscription** to host the service.  

    - An **Azure administrator** needs to participate in the initial creation of certain components, depending upon your design. This persona doesn't require permissions in Configuration Manager.  

- The site server requires **internet access** to deploy and manage the cloud service.  

- If using the Azure classic deployment method, you need an **Azure management certificate**. For more information, see the [Certificates](#bkmk_certs) section below.   

    > [!TIP]  
    > Starting with Configuration Manager version 1806, use the **Azure Resource Manager** deployment model. It doesn't require this management certificate.  

- If using the **Azure Resource Manager** deployment method, integrate Configuration Manager with [Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Azure AD user discovery isn't required.  

- A **server authentication certificate**. For more information, see the [Certificates](#bkmk_certs) section below.  

    - To reduce complexity, Microsoft recommends using a public certificate provider for the server authentication certificate. When doing so, you also need a **DNS CNAME alias** for clients to resolve the name of the cloud service.  

- Set the client setting, **Allow access to cloud distribution points**, to **Yes** in the **Cloud Services** group. By default, this value is set to **No**.  

- Client devices require **internet connectivity**, and must use **IPv4**.  



## <a name="bkmk_spec"></a> Specifications

- The cloud distribution point supports all Windows versions listed in [Supported operating systems for clients and devices](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

- An administrator distributes the following types of supported software content:  
    - Applications
    - Packages
    - OS upgrade packages
    - Third-party software updates  

    > [!Important]  
    > While the Configuration Manager console doesn't block the distribution of Microsoft software updates to a cloud distribution point, you're paying Azure costs to store content that clients don't use. Internet-based clients always get Microsoft software update content from the Microsoft Update cloud service. Don't distribute Microsoft software updates to a cloud distribution point.    

- Starting in version 1806, configure a pull-distribution point to use a cloud distribution point as a source. For more information, see [About source distribution points](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point#about-source-distribution-points).<!--1321554-->  


### Deployment settings

- When you deploy a task sequence with the option to **Download content locally when needed by running task sequence**, the management point doesn't include a cloud distribution point as a content location. Deploy the task sequence with the option to **Download all content locally before starting task sequence** for clients to use a cloud distribution point.  

- A cloud distribution point doesn't support package deployments with the option to **Run program from distribution point**. Use the deployment option to **Download content from distribution point and run locally**.  


### Limitations  

- You can't use a cloud distribution point for PXE or multicast-enabled deployments.  

- A cloud distribution point doesn't support App-V streaming applications.  

- You can't [prestage content](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent) on a cloud distribution point. The distribution manager of the primary site that manages the cloud distribution point transfers all content.  

- You can't configure a cloud distribution point as a pull-distribution point.  



##  <a name="bkmk_cost"></a> Cost   
<!--501018-->
> [!IMPORTANT]  
> The following cost information is for estimating purposes only. Your environment may have other variables that affect the overall cost of using a cloud distribution point.  

Configuration Manager includes the following options to help control costs and monitor data access:  

- Control and monitor the amount of content that you store in a cloud service. For more information, see [Monitor cloud distribution points](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_monitor).  

- Configure Configuration Manager to alert you when thresholds for client downloads meet or exceed monthly limits. For more information, see [Data transfer threshold alerts](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_alerts).   

- To help reduce the number of data transfers from cloud distribution points by clients, use one of the following peer caching technologies:  
    - Configuration Manager peer cache
    - Windows BranchCache
    - Windows 10 Delivery Optimization  

   For more information, see [Fundamental concepts for content management](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).   


### Components

A cloud distribution point uses the following Azure components, which incur charges to the Azure subscription account:  

> [!Tip]  
> Starting in version 1806, the cloud management gateway can also serve content to clients. This functionality reduces the cost by consolidating the Azure VMs. For more information, see [Cost for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#cost).  

#### Virtual machine
- The cloud distribution point uses Azure Cloud Services as platform as a service (PaaS). This service uses virtual machines (VMs) that incur compute costs.  

- Each cloud distribution point service uses two Standard A0 VMs.  

- See the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/) to help determine potential costs.

    > [!NOTE]  
    > Virtual machine costs vary by region.

#### Outbound data transfer
- Any dataflows into Azure are free (ingress or upload). Distributing content from the site to the cloud distribution point is uploading to Azure.  

- Charges are based on data flowing out of Azure (egress or download). Cloud distribution point dataflows out of Azure consist of the software content that clients download.  

- For more information, see [Monitor cloud distribution points](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_monitor).  

- See the [Azure bandwidth pricing details](https://azure.microsoft.com/pricing/details/bandwidth/) to help determine potential costs. Pricing for data transfer is tiered. The more you use, the less you pay per gigabyte.  

#### Content storage
- Internet-based clients get Microsoft software update content from the Microsoft Update cloud service at no charge. Don't distribute software update deployment packages with Microsoft software updates to a cloud distribution point. Otherwise, you'll incur data storage costs for content that clients never use.  

- Cloud distribution points use the following standard blob storage depending upon the deployment model:  

    - A classic deployment uses Azure geo-redundant storage (GRS). For more information, see [Geo-redundant storage](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs).  

    - An Azure Resource Manager deployment use Azure locally-redundant storage (LRS). This change reduces the cost of the storage account. The classic deployment wasn't using the additional features of GRS. For more information, see [Locally-redundant storage](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

#### Other costs
- Each cloud service has a dynamic IP address. Each distinct cloud distribution point uses a new dynamic IP address. Adding additional VMs per cloud service doesn't increase these addresses.  



##  <a name="bkmk_dataflow"></a> Ports and data flow   

There are two primary data flows for the cloud distribution point:  

- The site server connects to Azure to set up the cloud distribution point service  

- A client connects to the cloud distribution point to download content  


### Site server to Azure

You don't need to open any inbound ports to your on-premises network. The site server initiates all communication with Azure and the cloud distribution point to deploy, update, and manage the cloud service. The site server must be able to create outbound connections to the Microsoft cloud. This action is equivalent to installing the distribution point site system role on a specific site.  


### Client to cloud distribution point

You don't need to open any inbound ports to your on-premises network. Internet-based clients communicate directly with the Azure service. Clients on your internal network that use a cloud distribution point must be able to connect the Microsoft cloud. 

For more information on content location priority and when intranet-based clients use a cloud distribution point, see [Content source priority](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#content-source-priority).

When a client uses a cloud distribution point as a content location:  

1. The management point gives the client an access token along with the list of content sources. This token is valid for 24 hours, and gives the client access to the cloud distribution point.  

2. The management point responds to the client's location request with the **Service FQDN** of the cloud distribution point. This property is the same as the common name of the server authentication certificate.  

    If you're using your domain name, for example, WallaceFalls.contoso.com, then the client first tries to resolve this FQDN. You need a CNAME alias in your domain's internet-facing DNS for clients to resolve the Azure service name, for example: WallaceFalls.cloudapp.net.  

3. The client next resolves the Azure service name, for example, WallaceFalls.cloudapp.net, to a valid IP address. This response should be handled by Azure's DNS.  

4. The client connects to the cloud distribution point. Azure load balances the connection to one of the VM instances. The client authenticates itself using the access token.  

5. The cloud distribution point authenticates the client's access token, and then gives the client the exact content location in Azure storage.  

6. If the client trusts the cloud distribution point's server authentication certificate, it connects to Azure storage to download the content. 



##  <a name="bkmk_perf"></a> Performance and scale   
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



##  <a name="bkmk_certs"></a> Certificates  

Depending upon your cloud distribution point design, you need one or more digital certificates.  


### General information
<!--SCCMDocs issue #779-->
Certificates for cloud distribution points support the following configurations:  

- **4096 bit key length**  

- Starting in version 1710, support for **Version 3** certificates. For more information, see [CNG certificates overview](/sccm/core/plan-design/network/cng-certificates-overview).  

- Starting in version 1802, when you configure Windows with the following policy: **System cryptography: Use FIPS compliant algorithms for encryption, hashing, and signing**  

- Starting in version 1802, support for **TLS 1.2**. For more information, see [Cryptographic controls technical reference](/sccm/core/plan-design/security/cryptographic-controls-technical-reference#about-ssl-vulnerabilities).  


### Azure management certificate

*This certificate is required for classic service deployments. It isn't required for Azure Resource Manager deployments.*

If using the Azure classic deployment method, you need an **Azure management certificate**. For more information, see the [Azure management certificate](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#azure-management-certificate) section of the cloud management gateway certificates article. The Configuration Manager site server uses this certificate to authenticate with Azure to create and manage the classic deployment.  

> [!TIP]  
> Starting with Configuration Manager version 1806, use the **Azure Resource Manager** deployment model. It doesn't require this management certificate.  

To reduce complexity, use the same Azure management certificate for all classic deployments of cloud distribution points and cloud management gateways, across all Azure subscriptions and all Configuration Manager sites.


### Server authentication certificate

*This certificate is required for all cloud distribution point deployments.*

For more information, see [CMG server authentication certificate](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate), and the following subsections, as necessary:  
- CMG trusted root certificate to clients
- Server authentication certificate issued by public provider
- Server authentication certificate issued from enterprise PKI

The cloud distribution point uses this type of certificate in the same way as the cloud management gateway. Clients also need to trust this certificate. To reduce complexity, Microsoft recommends using a certificate issued by a public provider. 

Unless you use a wildcard certificate, don't reuse the same certificate. Each instance of the cloud distribution point and cloud management gateway requires a unique server authentication certificate. 

For more information on creating this certificate from a PKI, see [Deploy the service certificate for cloud distribution points](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012).  



##  <a name="bkmk_faq"></a> Frequently asked questions (FAQ)   

### Does a client need a certificate to download content from a cloud distribution point?

A client authentication certificate isn't required. The client does need to trust the server authentication certificate used by the cloud distribution point. If this certificate is issued by a public certificate provider, then most Windows devices already include trusted root certificates for these providers. If you issued a server authentication certificate from your organization's PKI, then your clients need to trust the issuing certificates in the entire chain. This chain includes the root certificate authority, and any intermediate certificate authorities. Depending upon your PKI design, this certificate can introduce additional complexity to the deployment of the cloud distribution point. To avoid this complexity, Microsoft recommends using a public certificate provider that your clients already trust.  


### Can my on-premises clients use a cloud distribution point?

Yes. If you want clients on your internal network to use a cloud distribution point, then it needs to be in the same boundary group as the clients. Clients prioritize cloud distribution points last in their list of content sources, because there's a cost associated with downloading content out of Azure. Thus, a cloud distribution point is typically used as a fallback source for intranet-based clients. If you want a cloud-first design, then design your boundary groups accordingly. For more information, see [Configure boundary groups](/sccm/core/servers/deploy/configure/boundary-groups).  


### Do I need Azure ExpressRoute?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) lets you extend your on-premises network into the Microsoft cloud. ExpressRoute, or other such virtual network connections aren't required for the Configuration Manager cloud distribution point.  

If your organization uses ExpressRoute, isolate the Azure subscription for the cloud distribution point from the subscription that uses ExpressRoute. This configuration ensures that the cloud distribution point isn't accidentally connected in this manner.  


### Do I need to maintain the Azure virtual machines?

No maintenance is required. The design of the cloud distribution point uses Azure platform as a service (PaaS). Using the subscription you provide, Configuration Manager creates the necessary VMs, storage, and networking. Azure secures and updates the virtual machines. These VMs aren't a part of your on-premises environment, as is the case with infrastructure as a service (IaaS). The cloud distribution point is a PaaS that extends your Configuration Manager environment into the cloud. For more information, see [Security advantages of a PaaS cloud service model](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model).  


### Does the cloud distribution point use Azure CDN?

The Azure Content Delivery Network (CDN) is a global solution for rapidly delivering high-bandwidth content by caching the content at strategically placed physical nodes across the world. For more information, see [What is Azure CDN?](https://docs.microsoft.com/azure/cdn/cdn-overview).

The Configuration Manager cloud distribution point currently doesn't support Azure CDN.



## Next steps
[Install cloud distribution points](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)
