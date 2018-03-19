---
title: CMG security and privacy
description: Learn about guidance and recommendations for security and privacy with the cloud management gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/16/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971

---

# Security and privacy for the cloud management gateway

*Applies to: System Center Configuration Manager (Current Branch)*

This article includes security and privacy information for the Configuration Manager cloud management gateway (CMG). For more information, see [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).

## CMG security details
- The CMG accepts and manages connections from CMG connection points. It uses mutual SSL authentication using certificates and connection IDs.
- The CMG accepts and forwards client requests using the following methods:
	- Pre-authenticates connections using mutual SSL with the PKI-based client authentication certificate or Azure AD. 
	  - IIS on the CMG VM instances verifies the certificate path based on the trusted root certificate(s) uploaded to the CMG.
	  - IIS on the VM instance also verifies client certificate revocation, if enabled. For more information, see [Publish the certificate revocation list](#bkmk_crl).
	- The certificate trust list checks the root of the client authentication certificate. It also performs the same validation as the management point for the client. For more information, see [Review entries in the site's certificate trust list](#bkmk_ctl).
	- Validates and filters client requests (URLs) to check if any CMG connection point can service the request.  
	- Checks content length for each publishing endpoint.
	- Uses round-robin behavior to load-balance CMG connection points in the same site.
- The CMG connection point uses the following methods:
	- Builds consistent HTTPS/TCP connections to all VM instances of the CMG. It checks and maintains these connections every minute.
	- Uses mutual SSL authentication with the CMG using certificates.
	- Forwards client requests based on URL mappings.
	- Reports connection status to show service health status in the console.
	- Reports traffic per endpoint every five minutes.

### Configuration Manager client-facing roles
The management point and software update point host endpoints in IIS to service client requests. The CMG doesn't expose all internal endpoints. Every endpoint published to the CMG has an URL mapping.
  - The external URL is the one the client uses to communicate with the CMG.
  - The internal URL is the CMG connection point used to forward requests to the internal server.

#### URL mapping example
When you enable CMG traffic on a management point, Configuration Manager creates an internal set of URL mappings for each management point server. For example: ccm_system, ccm_incoming, and sms_mp. The external URL for the management point ccm_system endpoint might look like:  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
The URL is unique for each management point. The Configuration Manager client then puts the CMG-enabled management point name into its internet management point list. This name looks like:  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
The site automatically uploads all published external URLs to the CMG. This behavior allows the CMG to do URL filtering. All URL mappings replicate to the CMG connection point. It then forwards the communication to internal servers according to the external URL from the client request.



## Security guidance for CMG


<a name="bkmk_crl"></a>

### Publish the certificate revocation list

Publish your PKI's certificate revocation list (CRL) for internet-based clients to access. When deploying a CMG using PKI, configure the service to **verify client certificate revocation** on the Settings tab. This setting configures the service to use a published certificate revocation list (CRL). For more information, see [Plan for PKI certificate revocation](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs).



<a name="bkmk_ctl"></a>

### Review entries in the site's certificate trust list
<!--503739-->
Each Configuration Manager site includes a list of trusted root certification authorities, the certificate trust list (CTL). View and modify the list by going to the Administration workspace, expand Site Configuration, and select Sites. Select a site, and click Properties in the ribbon. Switch to the Client Computer Communication tab, and then click **Set** under Trusted Root Certification Authorities.
 
Use a more restrictive CTL for a site with a CMG using PKI client authentication. Otherwise, clients with client authentication certificates issued by any trusted root that already exists on the management point are automatically accepted for client registration.

This subset provides administrators with more control over security. The CTL restricts the server to only accept client certificates that are issued from the certification authorities in the CTL. For example, Windows ships with a number of well-known third-party certification authority (CA) certificates, such as VeriSign and Thawte. By default, the computer running IIS trusts certificates that chain to these well-known CAs. Without configuring IIS with a CTL, any computer that has a client certificate issued from these CAs are accepted as a valid Configuration Manager client. If you configure IIS with a CTL that didn't include these CAs, client connections are refused if the certificate chained to these CAs. 


<!--486209-->


<!-- ## Privacy information for CMG -->


## Next steps

- [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Set up cloud management gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Frequently asked questions about the cloud management gateway](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Certificates for cloud management gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
