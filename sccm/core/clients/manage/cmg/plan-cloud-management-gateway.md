---
title: Plan for cloud management gateway
titleSuffix: Configuration Manager
description: Plan and design the cloud management gateway (CMG) to simplify management of internet-based clients.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Plan for the cloud management gateway in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*
 
<!--1101764-->
The cloud management gateway (CMG) provides a simple way to manage Configuration Manager clients on the internet. By deploying the CMG as a cloud service in Microsoft Azure, you can manage traditional clients that roam on the internet without additional infrastructure. You also don't need to expose your on-premises infrastructure to the internet. 

> [!Tip]  
> This feature was first introduced in version 1610 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1802, this feature is no longer a pre-release feature.  


> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


After establishing the prerequisites, creating the CMG consists of the following three steps in the Configuration Manager console:
1. Deploy the CMG cloud service to Azure.
2. Add the CMG connection point role. 
3. Configure the site and site roles for the service. 
Once deployed and configured, clients seamlessly access on-premises site roles regardless of whether they're on the intranet or internet.

This article provides the foundational knowledge to learn about the CMG, design how it fits in your environment, and plan the implementation. 



## Scenarios 

There are several scenarios for which a CMG is beneficial. The following scenarios are some of the more common:  

- Manage traditional Windows clients with Active Directory domain-joined identity. These clients include Windows 7, Windows 8.1, and Windows 10. It uses PKI certificates to secure the communication channel. Management activities include:  
    - Software updates and endpoint protection
    - Inventory and client status
    - Compliance settings
    - Software distribution to the device
    - Windows 10 in-place upgrade task sequence (as of version 1802)

- Manage traditional Windows 10 clients with modern identity, either hybrid or pure cloud domain-joined with Azure Active Directory (Azure AD). Clients use Azure AD to authenticate rather than PKI certificates. Using Azure AD is simpler to set up, configure and maintain than more complex PKI systems. Management activities are the same as the first scenario, as well as:  
    - Software distribution to the user  

- Install the Configuration Manager client on Windows 10 devices over the internet. Using Azure AD allows the device to authenticate to the CMG for client registration and assignment. You can install the client manually, or using another software distribution method, such as Microsoft Intune.  

- New device provisioning with co-management. CMG is not required for co-management. It helps complete an end-to-end scenario for new devices involving Windows AutoPilot, Azure AD, Microsoft Intune, and Configuration Manager.  

### Specific use cases
Across these scenarios the following specific device use cases may apply:

- Roaming devices such as laptops  

- Remote/branch office devices that are less expensive and more efficient to manage over the internet than across a WAN or through a VPN.  

- Mergers and acquisitions, where it may be easiest to join devices to Azure AD and manage through a CMG.  

> [!Important]
> By default all clients receive policy for a CMG, and start using it when they become internet-based. Depending upon the scenario and use case that applies to your organization, you may need to scope usage of the CMG. For more information, see the [Enable clients to use a cloud management gateway](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway) client setting.


## Topology design

### CMG components
Deployment and operation of the CMG includes the following components:  

- The **CMG cloud service** in Azure authenticates and forwards Configuration Manager client requests to the CMG connection point.  
 
- The **CMG connection point** site system role enables a consistent and high-performance connection from the on-premises network to the CMG service in Azure. It also publishes settings to the CMG including connection information and security settings. The CMG connection point forwards client requests from the CMG to on-premises roles according to URL mappings.

- The [**service connection point**](/sccm/core/servers/deploy/configure/about-the-service-connection-point) site system role runs the cloud service manager component, which handles all CMG deployment tasks. Additionally, it monitors and reports service health and logging information from Azure AD. Ensure your service connection point is in [online mode](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).  

- The **management point** site system role services client requests per normal.  

- The **software update point** site system role services client requests per normal.  

- **Internet-based clients** connect to the CMG to access on-premises Configuration Manager components.

- The CMG uses a **certificate-based HTTPS** web service to help secure network communication with clients.  

- Internet-based clients use **PKI certificates or Azure AD** for identity and authentication.  

- A [**cloud distribution point**](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) provides content to internet-based clients, as needed.  


### Azure Resource Manager
<!-- 1324735 -->
Starting in version 1802, you can create the CMG using an **Azure Resource Manager deployment**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) is a modern platform for managing all solution resources as a single entity, called a [resource group](/azure/azure-resource-manager/resource-group-overview#resource-groups). When deploying CMG with Azure Resource Manager, the site uses Azure Active Directory (Azure AD) to authenticate and create the necessary cloud resources. This modernized deployment does not require the classic Azure management certificate.  

The CMG wizard still provides the option for a **classic service deployment** using an Azure management certificate. To simplify the deployment and management of resources, using the Azure Resource Manager deployment model is recommended for all new CMG instances. If possible, redeploy existing CMG instances through Resource Manager. For more information, see [Modify a CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).

> [!IMPORTANT]  
> This capability does not enable support for Azure Cloud Service Providers (CSP). The CMG deployment with Azure Resource Manager continues to use the classic cloud service, which the CSP does not support. For more information, see [available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services). 


### Hierarchy design

Create the CMG at the top-tier site of your hierarchy. If that is a central administration site, then create CMG connection points at child primary sites. The cloud service manager component is on the service connection point, which is also on the central administration site. This design can share the service across different primary sites if needed.

You can create multiple CMG services in Azure, and you can create multiple CMG connection points. Multiple CMG connection points provide load balancing of client traffic from the CMG to the on-premises roles. To reduce network latency, assign the associated CMG to the same geographical region as the primary site.

 > [!Note]  
 > Internet-based clients and the CMG do not fall into any boundary group.

Other factors, such as the number of clients to manage, also impact your CMG design. For more information, see [Performance and scale](#performance-and-scale).

#### Example 1: standalone primary site

Contoso has a standalone primary site in an on-premises datacenter at their headquarters in New York City. 
- They create a CMG in the East US Azure region to reduce network latency. 
- They create two CMG connection points, both linked to the single CMG service.  

As clients roam onto the internet, they communicate with the CMG in the East US Azure region. The CMG forwards this communication through both of the CMG connection points.

#### Example 2: hierarchy with site-specific CMG

Fourth Coffee has a central administration site in an on-premises datacenter at their headquarters in Seattle. One primary site is in the same datacenter, and the other primary site is in their main European office in Paris. 
- On the central administration site, they create two CMG services:
     - One CMG in the West US Azure region.
     - One CMG in the West Europe Azure region.
- On the Seattle-based primary site, they create a CMG connection point linked to the West US CMG.
- On the Paris-based primary site, they create a CMG connection point linked to the West Europe CMG.

As Seattle-based clients roam onto the internet, they communicate with the CMG in the West US Azure region. The CMG forwards this communication to the Seattle-based CMG connection point.

Similarly, as Paris-based clients roam onto the internet, they communicate with the CMG in the West Europe Azure region. The CMG forwards this communication to the Paris-based CMG connection point. When Paris-based users travel to the company headquarters in Seattle, their computers continue to communicate with the CMG in the West Europe Azure region. 

 > [!Note]  
 > Fourth Coffee considered creating another CMG connection point on the Paris-based primary site linked to the West US CMG. Paris-based clients would then use both CMGs, regardless of their location. While this configuration helps load balance traffic and provide service redundancy, it can also cause delays when Paris-based clients communicate with the US-based CMG. Configuration Manager clients are not currently aware of their geographical region, so do not prefer a CMG that is geographically closer. Clients randomly use an available CMG.



## Requirements

- An **Azure subscription** to host the CMG.  

    - An **Azure administrator** needs to participate in the initial creation of certain components, depending upon your design. This persona does not require permissions in Configuration Manager.  

- At least one on-premises Windows server to host the **CMG connection point**. You can co-locate this role with other Configuration Manager site system roles.  

- The **service connection point** must be in [online mode](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).   

- A [**server authentication certificate**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate) for the CMG.  

- If using the Azure classic deployment method, you must use an [**Azure management certificate**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#azure-management-certificate).  

    > [!TIP]  
    > Starting with Configuration Manager version 1802, using the **Azure Resource Manager** deployment model is recommended. It does not require this management certificate.  

- **Other certificates** may be required, depending upon your client OS version and authentication model. For more information, see [CMG certificates](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).  

    - Starting in version 1802, you must configure all CMG-enabled [**management points to use HTTPS**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https).  

- Integration with **Azure AD** may be required for Windows 10 clients. For more information, see [Configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- Clients must use **IPv4**.  



## Specifications

- All Windows versions listed in [Supported operating systems for clients and devices](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) are supported for CMG.  

- CMG only supports the management point and software update point roles.  

- CMG does not support clients that only communicate with IPv6 addresses.<!--495606-->  

- Software update points using a network load balancer do not work with CMG. <!--505311-->  

- Starting in version 1802, CMG deployments using the Azure Resource Model do not enable support for Azure Cloud Service Providers (CSP). The CMG deployment with Azure Resource Manager continues to use the classic cloud service, which the CSP does not support. For more information, see [available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)  


### Support for Configuration Manager features
The following table lists CMG support for Configuration Manager features:


|Feature  |Support  |
|---------|---------|
| Software updates     | ![Supported](media/green_check.png) |
| Endpoint protection     | ![Supported](media/green_check.png) |
| Hardware and software inventory     | ![Supported](media/green_check.png) |
| Client status and notifications     | ![Supported](media/green_check.png) |
| Run scripts     | ![Supported](media/green_check.png) |
| Compliance settings     | ![Supported](media/green_check.png) |
| Client install</br>(with Azure AD integration)     | ![Supported](media/green_check.png)  (1706) |
| Software distribution (device-targeted)     | ![Supported](media/green_check.png) |
| Software distribution (user-targeted, required)</br>(with Azure AD integration)     | ![Supported](media/green_check.png)  (1710) |
| Software distribution (user-targeted, available)</br>([all requirements](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)) | ![Supported](media/green_check.png)  (1802) |
| Windows 10 in-place upgrade task sequence     | ![Supported](media/green_check.png)  (1802) |
| Any other task sequence scenario     | ![Not supported](media/Red_X.png) |
| Client push     | ![Not supported](media/Red_X.png) |
| Automatic site assignment     | ![Not supported](media/Red_X.png) |
| Application catalog     | ![Not supported](media/Red_X.png) |
| Software approval requests     | ![Not supported](media/Red_X.png) |
| Configuration Manager console     | ![Not supported](media/Red_X.png) |
| Remote tools     | ![Not supported](media/Red_X.png) |
| Reporting website     | ![Not supported](media/Red_X.png) |
| Wake on LAN     | ![Not supported](media/Red_X.png) |
| Mac, Linux, and UNIX clients     | ![Not supported](media/Red_X.png) |
| Peer cache     | ![Not supported](media/Red_X.png) |
| On-premises MDM     | ![Not supported](media/Red_X.png) |


|Key|
|--|
|![Supported](media/green_check.png) = This feature is supported with CMG by all supported versions of Configuration Manager  |
|![Supported](media/green_check.png) (*YYMM*) = This feature is supported with CMG starting with version *YYMM* of Configuration Manager  |
|![Not supported](media/Red_X.png) = This feature is not supported with CMG |



## Cost

>[!IMPORTANT]  
>The following cost information is for estimating purposes only. Your environment may have other variables that affect the overall cost of using CMG.

CMG uses the following Azure components, which incur charges to the Azure subscription account:

#### Virtual machine

- CMG uses Azure Cloud Services as platform as a service (PaaS). This service uses virtual machines (VMs) that incur compute costs.  

- In Configuration Manager version 1706, CMG uses a Standard A2 VM.  

- Starting in Configuration Manager version 1710, CMG uses a Standard A2 V2 VM.  

- You select how many VM instances support the CMG. One is the default, and 16 is the maximum. This number is set when creating the CMG, and can be changed afterwards to scale the service as needed.

- For more information on how many VMs you need to support your clients, see [Performance and scale](#performance-and-scale).

- See the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/) to help determine potential costs.

    > [!NOTE]  
    > Virtual machine costs vary by region.

#### Outbound data transfer

- Charges are based on data flowing out of Azure (egress or download). Any data flows into Azure are free (ingress or upload). CMG data flows out of Azure include policy to the client, client notifications, and client responses forwarded by the CMG to the site. These responses include inventory reports, status messages, and compliance status.  

- Even without any clients communicating with a CMG, some background communication causes network traffic between the CMG and the on-premises site.  

- View the **Outbound data transfer (GB)** in the Configuration Manager console. For more information, see [Monitor clients on CMG](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway).  

- See the [Azure bandwidth pricing details](https://azure.microsoft.com/pricing/details/bandwidth/) to help determine potential costs. Pricing for data transfer is tiered. The more you use, the less you pay per gigabyte.  

- *For estimating purposes only*, expect approximately 100-300 MB per client per month for internet-based clients. The lower estimate is for a default client configuration. The upper estimate is for a more aggressive client configuration. Your actual usage may vary depending upon how you configure client settings.  

   > [!NOTE]  
   > Performing other actions, such as deploying software updates or applications, increases the amount of outbound data transfer from Azure.

#### Content storage

- Internet-based clients get Microsoft software update content from Windows Update at no charge. Do not distribute update packages with Microsoft update content to a cloud distribution point, otherwise you may incur storage and data egress costs.  

- For any other necessary content, such as applications or third-party software updates, you must distribute to a cloud distribution point. Currently, the CMG supports only the cloud distribution point for sending content to clients.  

- For more information, see the cost of using [cloud distribution points](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_cost).  

#### Other costs

- Each cloud service has a dynamic IP address. Each distinct CMG uses a new dynamic IP address. Adding additional VMs per CMG doesn't increase these addresses.  



## Performance and scale

For more information on CMG scale, see [Size and scale numbers](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg).

The following recommendations can help you improve CMG performance:

- If possible, configure the CMG, CMG connection point, and the Configuration Manager site server in same network region to reduce latency.  

- Currently, the connection between the Configuration Manager client and the CMG is not region-aware.  

- For high availability of the service, create at least two CMG services and two CMG connection points per site.  

- Scale the CMG to support more clients by adding more VM instances. The Azure load balancer controls client connections to the service.  

- Create more CMG connection points to distribute the load among them. The CMG distributes the traffic to its connecting CMG connection points in a round-robin fashion.  

- When the CMG is under high load due to more than the supported number of clients, it still handles requests but there may be delay.  


> [!Note]  
> While Configuration Manager has no hard limit on the number of clients for a CMG connection point, Windows Server has a default maximum TCP dynamic port range of 16,384. If a Configuration Manager site manages more than 16,384 clients with a single CMG connection point, you must increase the Windows Server limit. All clients maintain a channel for client notifications, which holds a port open on the CMG connection point. For more information on how to use the netsh command to increase this limit, see [Microsoft Support article 929851](https://support.microsoft.com/help/929851).



## Ports and data flow

You do not need to open any inbound ports to your on-premises network. The service connection point and CMG connection point initiate all communication with Azure and the CMG. These two site system roles must be able to create outbound connections to the Microsoft cloud. The service connection point deploys and monitors the service in Azure, thus must be online mode. The CMG connection point connects to the CMG to manage communication between the CMG and on-premises site system roles.

The following diagram is a basic, conceptual data flow for the CMG: 
![CMG data flow](media/cmg-data-flow.png)
   1. The service connection point connects to Azure over HTTPS port 443. It authenticates using Azure AD or the Azure management certificate. The service connection point deploys the CMG in Azure. The CMG creates the HTTPS cloud service using the server authentication certificate.  

   2. The CMG connection point connects to the CMG in Azure over TCP-TLS or HTTPS. It holds the connection open, and builds the channel for future two-way communication.   

   3. The client connects to the CMG over HTTPS port 443. It authenticates using Azure AD or the client authentication certificate.  

   4. The CMG forwards the client communication over the existing connection to the on-premises CMG connection point. You don't need to open any inbound firewall ports.  

   5. The CMG connection point forwards the client communication to the on-premises management point and software update point.  

### Required ports
This table lists the required network ports and protocols. The *Client* is the device initiating the connection, requiring an outbound port. The *Server* is the device accepting the connection, requiring an inbound port. 

| Client  | Protocol | Port  | Server  | Description  |
|---------|---------|---------|---------|---------|
| Service connection point     | HTTPS | 443        | Azure        | CMG deployment |
| CMG connection point     |  TCP-TLS | 10140-10155        | CMG service        | Preferred protocol to build CMG channel <sup>1</sup> |
| CMG connection point     | HTTPS | 443        | CMG service       | Fallback to build CMG channel to only one VM instance<sup>2</sup> |
| CMG connection point     |  HTTPS   | 10124-10139     | CMG service       | Fallback to build CMG channel to two or more VM instances<sup>3</sup> |
| Client     |  HTTPS | 443         | CMG        | General client communication |
| CMG connection point      | HTTPS or HTTP | 443 or 80         | Management point</br>(version 1706 or 1710) | On-premises traffic, port depends upon management point configuration |
| CMG connection point      | HTTPS | 443      | Management point</br>(version 1802) | On-premises traffic must be HTTPS |
| CMG connection point      | HTTPS or HTTP | 443 or 80         | Software update point | On-premises traffic, port depends upon software update point configuration |

<sup>1</sup> The CMG connection point first tries to establish a long-lived TCP-TLS connection with each CMG VM instance. It connects to the first VM instance on port 10140. The second VM instance uses port 10141, up to the sixteenth on port 10155. A TCP-TLS connection performs the best, but it doesn’t support internet proxy. If the CMG connection point can’t connect via TCP-TLS, then it falls back to HTTPS<sup>2</sup>.  

<sup>2</sup> If the CMG connection point can’t connect to the CMG via TCP-TLS<sup>1</sup>, it connects to the Azure network load balancer over HTTPS 443 only for one VM instance.  

<sup>3</sup> If there are two or more VM instances, the CMG connection point uses HTTPS 10124 to the first VM instance, not HTTPS 443. It connects to the second VM instance on HTTPS 10125, up to the sixteenth on HTTPS port 10139.


### Internet access requirements

The CMG connection point site system supports using a web proxy. For more information on configuring this role for a proxy, see [Proxy server support](/sccm/core/plan-design/network/proxy-server-support#to-set-up-the-proxy-server-for-a-site-system-server). The CMG connection point requires connectivity to the following endpoints:  

- Specific Azure endpoints are different per environment depending upon the configuration. Configuration Manager stores these endpoints in the site database. Query the **AzureEnvironments** table in SQL Server for the list of Azure endpoints.  

- ServiceManagementEndpoint (https://management.core.windows.net/)  

- StorageEndpoint (core.windows.net)  

- For Azure AD token retrieval by the Configuration Manager console and client: ActiveDirectoryEndpoint (https://login.microsoftonline.com/)  

- For Azure AD user discovery: AAD Graph endpoint (https://graph.windows.net/)  



## Next steps

- [Certificates for cloud management gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Security and privacy for cloud management gateway](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Cloud management gateway size and scale numbers](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
- [Frequently asked questions about the cloud management gateway](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Set up cloud management gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
