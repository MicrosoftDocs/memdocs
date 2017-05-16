---
title: "Plan for the cloud management gateway | Microsoft Docs"
description: ""
ms.date: 05/16/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: robstackmsft
ms.author: robstack
manager: angrobe
---

# Plan for the cloud management gateway in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Beginning in version 1610, cloud management gateway provides a simple way to manage Configuration Manager clients on the Internet. The cloud management gateway service is deployed to Microsoft Azure and requires an Azure subscription. It connects to your on-premises Configuration Manager infrastructure using a new role called the cloud management gateway connector point. Once deployed and configured, clients will be able to access on-premises Configuration Manager site system roles regardless of whether they're on the internal private network or on the Internet.

Use the Configuration Manager console to deploy the service to Azure, add the cloud management gateway connector point role, and configure site system roles to allow cloud management gateway traffic. Cloud management gateway currently only supports the management point and software update point roles.

Client certificates and Secure Socket Layer (SSL) certificates are required to authenticate computers and encrypt communications between the different layers of the service. Client computers typically receive a client certificate through group policy enforcement. To encrypt the traffic between clients and site system server hosting the roles, you need to create a custom SSL certificate from the CA. You also need set up a management certificate on Azure that allows Configuration Manager to deploy the cloud management gateway service.

## Requirements for cloud management gateway

-   Client computers and the site system server running the cloud management gateway connector point.

-   Custom SSL certificates from the internal CA - used to encrypt communication from the client computers and authenticate the identity of the cloud management gateway service.

-   Azure subscription for cloud services.

-   Azure management certificate - used to authenticate Configuration Manager with Azure.

## Specifications for cloud management gateway

- Each instance of cloud management gateway supports 4,000 clients.
- We recommend that you create at least two instances of cloud management gateway to improve availability.
- Cloud management gateway only supports the management point and software update point roles.
-   The following features in Configuration Manager are currently unsupported for cloud management gateway:

    -   Client deployment
    -   Automatic site assignment
    -   User policies
    -   Application catalog (including software approval requests)
    -   Full operating system deployment (OSD)
    -   Configuration Manager console
    -   Remote tools
    -   Reporting website
    -   Wake on LAN
    -   Mac, Linux, and UNIX clients
    -   Azure Resource Manager
    -   Peer cache
    -   On-premises Mobile Device Management

## Cost of cloud management gateway

>[!IMPORTANT]
>The cost information provided below is for estimating purposes only. Your environment may have other variables that affect the overall cost of using cloud management gateway.

Cloud management gateway uses the following Microsoft Azure functionality, which incurs charges to the Azure subscription account:

-   Virtual machine

    -   Cloud management gateway currently requires a Standard\_A2 virtual machine. When creating the service, you can select how many VMs to support the service (one is the default).

    -   For estimating purposes only, expect that a single Azure Standard\_A2 virtual machine can support approximately 2,000 simultaneous Internet-based clients.

    -   See the [Azure pricing calculator](https://azure.microsoft.com/en-us/pricing/calculator/) to help determine potential costs.

      >[!NOTE]
      >Virtual machine costs vary by region.

-   Outbound data transfer

    -   Charges are incurred for data flowing out of the service.. See the [Azure bandwidth pricing details](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) to help determine potential costs.

    -   For estimating purposes only, expect approximately 100 MB per client per month for Internet-based clients doing policy refreshes every hour.

    >[!NOTE]
    > Performing other actions supported via the cloud management gateway (for example, deploying software updates or applications) will increase the amount of outbound data transfer from Azure.

-   Content storage

    -   Internet-based clients managed with cloud management gateway will get software update content from Windows Update at no charge.

    -   Any other necessary content (for example, applications) must be distributed to a cloud-based distribution point. Currently, the cloud management gateway supports only Cloud Distribution Point for sending content to clients.

    - See the cost of using a [cloud-based distribution](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution) for more details.

## Next steps

[Set up cloud management gateway](setup-cloud-management-gateway.md)


## Frequently asked questions about the Cloud Management Gateway (CMG)

### Why use the cloud management gateway?

Use this role to simplify Internet-based client management in three steps from the Configuration Manager console.

1. Deploy the CMG to Azure using the [Create Cloud Management Gateway](/sccm/core/clients/manage/setup-cloud-management-gateway) wizard.
2. Configure the [cloud management gateway connection point](/sccm/core/servers/deploy/configure/install-site-system-roles) site system role.
3. [Configure roles for cloud management gateway traffic](/sccm/core/clients/manage/setup-cloud-management-gateway#step-7-configure-roles-for-cloud-management-gateway-traffic), like the management point, and software update point.

### How does the cloud management gateway work?

- The cloud management gateway connection point enables a consistent and high performance connection from the Internet to the cloud management gateway.
- Configuration Manager publishes settings to the CMG including connection information and security settings.
- The CMG authenticates and forwards Configuration Manager client requests to the cloud management gateway connection point. These requests are forwarded to roles in the corporate network according to URL mappings.

### How is the cloud management gateway deployed?

The cloud service manager component on the service connection point handles all CMG deployment tasks. Additionally, it monitors and reports service health and logging information from Azure AD.

#### Certificate requirements

You'll need the following certificates to secure the CMG:

- **Management certificate** - This can be any certificate including self-signed certificates. You can use a public certificate uploaded to Azure AD or a  [PFX with private key](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) imported into Configuration Manager to authenticate with Azure AD. 
- **Web service certificate** -  We recommend that you use a public CA certificate to gain native trust by clients. The CName needs to be created in the public DNS registar. Wild card certificates are not supported.
- **Root/SubCA certificates upload to CMG** - The CMG needs to do full chain validation on client PKI certificates. If you use an enterprise CA for issuing client PKI certificates and their root or subordinate CA is not available on the internet, then you must upload it to the CMG.

#### Deployment process

There two phases to the deployment:

- Deploy the cloud service
	- Upload your [Azure Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) (csdef) file
	- Upload your [Azure Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) (cscfg) file.
- Set up the CMG component on your Azure AD server, and configure endpoints, HTTP handlers, and services in Internet Information Services (IIS)

If you change the configuration of the CMG, a configuration deployment is initiated to the CMG.

### How does the cloud management gateway help ensure security?

The CMG helps ensure security in the following ways:

- Accepts and manages connections from CMG connection points including mutual SSL authentication using internal certificates and connection IDs.
- Accepts and forwards client requests
	- Pre-authenticates connections using mutual SSL on the client PKI certificate.
	- The certificate trust list checks the root of the client PKI certificate. You can specify this setting in the client communicate settings in site properties. Also performs the same validation as the management point for the client.
	- Validates received URLs
	- Filters received URLs to check if any connecting CMG connection point can service the URL request.  
	- Checks content length check for each publishing endpoint.
	- Uses 'round-robin' to load balance between CMG connection points from the same site.

- Secures the CMG connection point
	- Builds consistent HTTP/TCP connections to all virtual instances of the connecting CMG. Checks and maintains connections every minute.
	- Mutually autheticates SSL authentication with CMG using internal certificates.
	- Forwards HTTP requests based on URL mappings.
	- Reports connection status to show admin service health status.
	- Reports endpoint traffic report per endpoint every 5 minutes.

- Secure the publishing endpoint
Configuration Manager client facing roles like the management point, and software update point host endpoints in IIS to service client requests. Every endpoint published to the CMG has an URL mapping.
The external URL is the one the client uses to communicate with the CMG.
The internal URL is the CMG connection point used to forward requests to the internal server. 

#### Example:
When you enable CMG traffic on a management point, Configuration Manager creates a set of URL mappings internally for each management point server, like ccm_system, ccm_incoming, and sms_mp.
The external URL for the management point ccm_system endpoint might look like **https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System**. 
The URL is unique for each management point. The Configuration Manager client then puts the CMG enabled MP name like **<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>** into its internet management point list. 
All published external URLs are uploaded to the CMG automatically then CMG is able to do URL filtering. All URL mapping replicates to CMG connection point so it can forward to internal servers according to client requesting external URL.

### What ports are used by the cloud management gateway? 

- No inbound ports required on premise network. Deployment of CMG will create a bunch on CMG automatically. 
- Besides 443, some outbound ports are required by the CMG connection point.

|||||
|-|-|-|-|
|Data flow|Server|Server ports|Client|
|CMG deployment|Azure|443|Configuration Manager service connection point|
|Build CMG channel|CMG|VM instance: 1 Port: 443<br>VM instance: N (N>=2 and N<= 16) Ports: 10124~N 10140~N|CMG Connection point|
|Client to CMG|CMG|443|Client|
|CMG connector to site role (currently management points and software update points)|Site role|Protocol/Ports configured on the site role|CMG connection point|

### How can you improve performance of the cloud management gateway?

- If possible, configure the CMG, CMG connection point and the Configuration Manager site server in same network region to reduce latency.
- Currently, the connection between the Configuration Manager client and the CMG is not region-aware.
- To gain high availability, we recommend at least 2 virtual instances of the CMG and two CMG connection points per site 
- You can scale the CMG to support more clients by adding more VM instances. They are load balanced by the Azure AD load balancer.
- Create more CMG connection points to distribute the load among them. The CMG will 'round-robin' the traffic to its connecting CMG connection points.
- Support client number per CMG VM instance is 6k in the 1702 release. When the CMG channel is under high load, the request will still be handled but might take longer than normal.

### How can you monitor the cloud management gateway?

For troubleshooting deployment, use **CloudMgr.log** and **CMGSetup.log**.
For troubleshooting service health, use **CMGService.log** and **SMS_CLOUD_PROXYCONNECTOR.log**.
For troubleshooting client traffic, use **CMGHttpHandler.log**, **CMGService.Log**, and **SMS_CLOUD_PROXYCONNECTOR.log**.

For a list of all CMG-related log files, see [Log files in Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)

