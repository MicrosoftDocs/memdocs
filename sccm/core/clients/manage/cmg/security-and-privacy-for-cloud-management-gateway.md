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

This article includes security and privacy information for the Configuration Manager cloud management gateway. For more information, see [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## Security guidance for cloud management gateway

### Publish the certificate revocation list

When deploying a cloud management gateway using PKI, configure the service to **verify client certificate revocation** on the Settings tab. This setting configures the service to use a published certificate revocation list (CRL). For more information, see [Plan for PKI certificate revocation](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs).

### Review entries in the site's certificate trust list
<!--503739-->
Each Configuration Manager site includes a list of trusted root certification authorities, the certificate trust list (CTL). View and modify the list by going to the Administration workspace, expand Site Configuration, and select Sites. Select a site, and click Properties in the ribbon. Switch to the Client Computer Communication tab, and then click **Set** under Trusted Root Certification Authorities.
 
Use a more restrictive CTL for a site with a cloud management gateway deployment using PKI client authentication. Otherwise, clients with client authentication certificates issued by any trusted root that already exists on the management point are automatically accepted for client registration.

This subset provides administrators with more control over security. The CTL restricts the server to only accept client certificates that are issued from the certification authorities in the CTL. For example, Windows ships with a number of well-known third-party certification authority (CA) certificates, such as VeriSign and Thawte. By default, the computer running IIS trusts certificates that chain to these well-known CAs. Without configuring IIS with a CTL, any computer that has a client certificate issued from these CAs are accepted as a valid Configuration Manager client. If you configure IIS with a CTL that didn't include these CAs, client connections are refused if the certificate chained to these CAs. 


<!--486209-->


<!-- ## Privacy information for cloud management gateway -->


## Next steps

- [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Set up cloud management gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Frequently asked questions about the cloud management gateway](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Certificates for cloud management gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
