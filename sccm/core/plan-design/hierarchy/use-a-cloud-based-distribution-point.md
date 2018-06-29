---
title: Cloud distribution point
titleSuffix: Configuration Manager
description: Plan and design for distributing software content through Microsoft Azure with cloud distribution points in Configuration Manager.
ms.date: 07/13/2018
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

- Reduce the need for traditional distribution points at remote offices  


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

-   To meet changing demands for content requests by clients, manually scale the cloud service in Azure. This action doesn't require that you install and provision additional distribution points in Configuration Manager. When you update the site, it resets the VM count for the cloud service to the default of two. 

-   Supports content download from clients configured for Windows BranchCache.



## <a name="bkmk_topology"></a> Topology design

Deployment and operation of the cloud distribution point includes the following components:  

- A **cloud service** in Azure. The site distributes content to this service, which stores it in cloud storage. The management point provides to clients this content location in the list of available sources as appropriate.  

- A **management point** site system role services client requests per normal.  

    - On-premises clients typically use an on-premises management point.  

    - Internet-based clients either use a [cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway), or an [internet-based management point](/sccm/core/clients/manage/plan-internet-based-client-management).  

- The cloud distribution point uses a **certificate-based HTTPS** web service to help secure network communication with clients.  

- Internet-based clients use **PKI certificates or Azure AD** for identity and authentication.  


### Azure Resource Manager
<!--1322209-->
Starting in version 1806, create a cloud distribution point using an **Azure Resource Manager deployment**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) is a modern platform for managing all solution resources as a single entity, called a [resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). When deploying a cloud distribution point with Azure Resource Manager, the site uses Azure Active Directory (Azure AD) to authenticate and create the necessary cloud resources. This modernized deployment doesn't require the classic Azure management certificate.  

The cloud distribution point wizard still provides the option for a **classic service deployment** using an Azure management certificate. To simplify the deployment and management of resources, we recommend using the Azure Resource Manager deployment model for all new cloud distribution points. If possible, redeploy existing cloud distribution points through Resource Manager.

Configuration Manager doesn't migrate existing classic cloud distribution points to the Azure Resource Manager deployment model. Create new cloud distribution points using Azure Resource Manager deployments, and then remove classic cloud distribution points. 

> [!IMPORTANT]  
> This feature doesn't enable support for Azure Cloud Service Providers (CSP). The cloud distribution point deployment with Azure Resource Manager continues to use the classic cloud service, which the CSP doesn't support. For more information, see [available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### Hierarchy design
<!--parking lot with KerimH & BruceAms-->

<!--483583-->

Even though you install cloud distribution points in specific regions of Azure, clients aren't aware of the Azure regions. They randomly select a cloud distribution point. If you install cloud distribution points in multiple regions, and a client receives more than one in the content location list, the client might not use a cloud distribution point from the same Azure region.  


Starting in version 1806, the cloud management gateway can also serve content to clients. This functionality reduces the required certificates and cost of Azure VMs. For more information, see [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).<!--1358651-->  


### Backup and recovery  

When you use a cloud distribution point in your hierarchy, use the following information to help you plan for backup and recovery:  

- When you use the **Backup Site Server** maintenance task, Configuration Manager automatically includes the configurations for the cloud distribution point.  

- Back up and save a copy of the server authentication certificate. If you use the classic service deployment in Azure, also back up and save a copy of the Azure management certificate. When you restore the Configuration Manager primary site to a different server, you must reimport the certificates.  



##  <a name="bkmk_requirements"></a> Requirements

- An **Azure subscription** to host the service.  

    - An **Azure administrator** needs to participate in the initial creation of certain component, depending upon your design. This persona doesn't require permissions in Configuration Manager.  

- The site server requires **internet access** to deploy and manage the cloud service. 

- If using the Azure classic deployment method, an **Azure management certificate**. For more information, see the [Azure management certificate](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#azure-management-certificate) section of the cloud management gateway certificates article.   

    > [!TIP]  
    > Starting with Configuration Manager version 1806, use the **Azure Resource Manager** deployment model. It doesn't require this management certificate.  

- If using the **Azure Resource Manager** deployment method, integration with [Azure Active Directory](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Azure AD user discovery isn't required.  

- A **server authentication certificate**. <!--Link to same in CMG, new in CMG, or something within this article?-->  

- Set the client setting, **Allow access to cloud distribution points**, to **Yes** in the **Cloud Services** group. By default, this value is set to **No**.  

- A **DNS CNAME alias** for clients to resolve the name of the cloud service.  

- Clients devices require **internet connectivity**, and must use **IPv4**.  



## <a name="bkmk_spec"></a> Specifications

- All Windows versions listed in [Supported operating systems for clients and devices](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) are supported for the cloud distribution point.  

- An administrator distributes the following types of supported **software content**:  
    - Applications
    - Packages
    - OS upgrade packages
    - Third-party software updates  

    > [!Note]  
    > While the Configuration Manager console doesn't block the distribution of Microsoft software updates to a cloud distribution point, you're paying Azure costs to store content that clients don't use. Internet-based clients always get Microsoft software update content from the Microsoft Update cloud service.  

- Starting in version 1806, configure a pull-distribution point to use a cloud distribution point as a source. For more information, see [About source distribution points](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point#about-source-distribution-points).<!--1321554-->  


### Deployment settings

- When you deploy a task sequence with the option to **Download content locally when needed by running task sequence**, the management point doesn't include a cloud distribution point as a content location. Deploy the task sequence with the option to **Download all content locally before starting task sequence** for clients to use a cloud distribution point.  

- A cloud distribution point doesn't support package deployments with the option to **Run program from distribution point**. Use the deployment option to **Download content from distribution point and run locally**.  

<!--483583: what deployment settings are needed to use CDP?-->


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

- Control and monitor the amount of content that you store in a cloud service. For more information, see [LINK]()<!--NEED LINK-->.  

- Configure Configuration Manager to alert you when thresholds for client downloads meet or exceed monthly limits. For more information, see [LINK]()<!--NEED LINK-->.   

- To help reduce the number of data transfers from cloud distribution points by clients, use one of the following peer caching technologies:  
    - Configuration Manager peer cache
    - Windows BranchCache
    - Windows 10 Delivery Optimization  

    For more information, see [Fundamental concepts for content management](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).   


### Components

A cloud distribution point uses the following Azure components, which incur charges to the Azure subscription account:  

#### Virtual machine
- The cloud distribution point uses Azure Cloud Services as platform as a service (PaaS). This service uses virtual machines (VMs) that incur compute costs.  

- Each cloud distribution point service uses two Standard A0 VMs.  

- See the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/) to help determine potential costs.

    > [!NOTE]  
    > Virtual machine costs vary by region.

#### Outbound data transfer
- Any dataflows into Azure are free (ingress or upload). Distributing content from the site to the cloud distribution point is uploading to Azure.  

- Charges are based on data flowing out of Azure (egress or download). Cloud distribution point dataflows out of Azure consist of the software content that clients download.  

- For more information, see [LINK]()<!--NEED LINK, something on how to monitor CDP?-->.  

- See the [Azure bandwidth pricing details](https://azure.microsoft.com/pricing/details/bandwidth/) to help determine potential costs. Pricing for data transfer is tiered. The more you use, the less you pay per gigabyte.  

#### Content storage
- Internet-based clients get Microsoft software update content from the Microsoft Update cloud service at no charge. Don't distribute software update deployment packages with Microsoft software update content to a cloud distribution point. Otherwise, you'll incur data storage costs.  

- Cloud distribution points use Azure geo-redundant storage (GRS) standard blob storage. For more information, see [Geo-redundant storage](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs).  

#### Other costs
- Each cloud service has a dynamic IP address. Each distinct cloud distribution point uses a new dynamic IP address. Adding additional VMs per cloud service doesn't increase these addresses.  



##  <a name="bkmk_perf"></a> Performance and scale   
<!--parking lot with KerimH & BruceAms-->

<!--494872
    - How to add more capacity?
    - More nodes
    - Auto scaling
-->

<!--512106
    - From TFS 1357349:
        > Azure supports 500 requests/sec for single file (60mb/s).  We calculated we should be able to support distribution of a single 100MB file to 50K clients in 24hrs with 1 Cloud DP.
    - Remi's comment "i can't brake it."
-->



##  <a name="bkmk_dataflow"></a> Ports and data flow   
<!--parking lot with KerimH & BruceAms-->


### Site sets up cloud distribution point

-   **Site server to cloud distribution point communication**: When you install a cloud distribution point, you must assign one primary site to manage the transfer of content to the cloud service. This action is equivalent to installing the distribution point site system role on a specific site.  


### Client communicates with cloud distribution point

-   **Client to cloud distribution point communication**: When a device or user of a device is configured with the client setting that enables the use of a cloud distribution point, the device can receive the cloud distribution point as a valid content location:  

    -   The cloud distribution point is considered a remote distribution point when a client evaluates available content locations.  

    -   Clients on the intranet only use cloud distribution points as a fallback option if on-premises distribution points aren't available.  

Clients that use cloud distribution points use the following sequence for content location requests:  

1.  A client that is configured to use cloud distribution points always attempts to obtain content from a preferred distribution point first.  

2.  When a preferred distribution point isn't available, the client uses a remote distribution point, if the deployment supports this option and if a remote distribution point is available.  

3.  When a preferred distribution point or remote distribution point isn't available, the client can then fall back to obtain the content from a cloud distribution point.  

When a client uses a cloud distribution point as a content location, the client authenticates itself to the cloud distribution point by using a Configuration Manager access token. If the client trusts the Configuration Manager cloud distribution point certificate, the client can then download the requested content.  

<!-- 483583
    - When is CDP returned to client as content location?
    - How does CDP work with boundary groups?
    - How does CDP work with intranet vs internet clients?
-->



##  <a name="bkmk_certs"></a> Certificates  

Cloud distribution points require certificates to enable Configuration Manager to manage the cloud service that hosts the distribution point, and for clients to access content from the distribution point. 


### Azure management certificate

-   **Management certificate for site server to distribution point communication**: The management certificate establishes trust between the Azure management API and Configuration Manager. This authentication enables Configuration Manager to call on the Azure API when you perform tasks such as deploying content or starting and stopping the cloud service. By using  Azure, you can create your own management certificates, which can be either self-signed certificates or certificates that are issued by a certification authority (CA):  

    -   Provide the .cer file of the management certificate to Azure when you configure Azure for Configuration Manager. The .cer file contains the public key for the management certificate. Upload this certificate to Azure before you install a cloud distribution point. This certificate enables Configuration Manager to access the Azure API.  

    -   Provide the .pfx file of the management certificate to Configuration Manager when you install the cloud distribution point. The .pfx file contains the private key for the management certificate. Configuration Manager stores this certificate in the site database. Because the .pfx file contains the private key, you must provide the password to import this certificate file into the Configuration Manager database.  

    If you create a self-signed certificate, you must first export the certificate as a .cer file and then export it again as a .pfx file.  

    Optionally, you can specify a version one **.publishsettings** file from the Azure SDK 1.7. For information about .publishsettings files, refer to the Azure documentation.  

    For more information, see [How to create a management certificate](http://go.microsoft.com/fwlink/p/?LinkId=220281) and [How to add a management certificate to an Azure subscription](http://go.microsoft.com/fwlink/p/?LinkId=241722) in the Azure platform section of the MSDN Library.  


### Server authentication certificate

-   **Service certificate for client communication to the distribution point**: The Configuration Manager cloud distribution point service certificate establishes trust between the Configuration Manager clients and the cloud distribution point, and secures the data that clients download from it by using Secure Socket Layer (SSL) over HTTPS.  

    > [!IMPORTANT]  
    >  The common name in the certificate subject box of the service certificate must be unique in your domain and not match any domain-joined device.  

   For an example deployment of this certificate, see the section **Deploying the service certificate for cloud distribution points** in the article [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

<!-- pulled over from setup article, worth noting somewhere here?

        >  The **Service FQDN** box is automatically populated from the certificate subject name. In most cases, you do not have to edit it. The exception is if you are using a wildcard certificate in a testing environment. For example, in this case you might not specify the host name, so that multiple computers that have the same DNS suffix can use the certificate. In this scenario, the certificate subject contains a value similar to **CN=\*.contoso.com**, and Configuration Manager displays a message that you must specify the correct FQDN. Click **OK** to close the message, and then enter a specific name before the DNS suffix to provide a complete FQDN. For example, you might add **clouddp1** to specify the complete service FQDN of **clouddp1.contoso.com**. The Service FQDN must be unique in your domain and not match any domain-joined device.  
        >   
        >  Wildcard certificates are supported for testing environments only.  
-->

### When certificates expire
<!--512106-->



##  <a name="bkmk_faq"></a> Frequently asked questions (FAQ)   

### Does a client need a certificate to download content from a cloud distribution point?

No?  


### Can my on-premises clients use a cloud distribution point?

Yes!  


### What certificates do I need?

For more detailed information, see [LINK]()<!--NEED Link, to same in CMG, new in CMG, or something within this article?-->.  


### Do I need Azure ExpressRoute?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) lets you extend your on-premises network into the Microsoft cloud. ExpressRoute, or other such virtual network connections aren't required for the Configuration Manager cloud distribution point.  

If your organization uses ExpressRoute, isolate the Azure subscription for the cloud distribution point from the subscription that uses ExpressRoute. This configuration ensures that the cloud distribution point isn't accidentally connected in this manner.  


### Do I need to maintain the Azure virtual machines?

No maintenance is required. The design of the cloud distribution point uses Azure platform as a service (PaaS). Using the subscription you provide, Configuration Manager creates the necessary virtual machines (VMs), storage, and networking. Azure secures and updates the virtual machines. These VMs aren't a part of your on-premises environment, as is the case with infrastructure as a service (IaaS). The cloud distribution point is a PaaS that extends your Configuration Manager environment into the cloud. For more information, see [Security advantages of a PaaS cloud service model](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model).  


### Does the cloud distribution point use Azure CDN?

The Azure Content Delivery Network (CDN) is a global solution for rapidly delivering high-bandwidth content by caching the content at strategically placed physical nodes across the world. For more information, see [What is Azure CDN?](https://docs.microsoft.com/azure/cdn/cdn-overview).

The Configuration Manager cloud distribution point currently doesn't support Azure CDN.



## Next steps
[Install cloud distribution points](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)
