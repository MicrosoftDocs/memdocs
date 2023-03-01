---
title: Data flow for CMG
titleSuffix: Configuration Manager
description: Understand how data flows between components of the cloud management gateway (CMG), including network ports and internet endpoints.
ms.date: 04/08/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: reference
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Data flow for CMG

*Applies to: Configuration Manager (current branch)*

Use this article to understand how data flows between components of the cloud management gateway (CMG). It requires specific network ports and internet endpoints to function. You don't need to open any inbound ports to your on-premises network. The service connection point and CMG connection point site system roles start all communication with Azure and the CMG. These two roles need to create outbound connections to the Microsoft cloud. The service connection point deploys and monitors the service in Azure, so needs to be online. The CMG connection point connects to the CMG to manage communication between the CMG and on-premises site system roles.

## Data flow diagram

The following diagram is a basic, conceptual data flow for the CMG:

:::image type="content" source="media/cmg-data-flow.svg" alt-text="Data flow diagram for cloud management gateway (CMG).":::

1. The service connection point connects to Azure over HTTPS port 443. It authenticates using Azure Active Directory (Azure AD). The service connection point deploys the CMG in Azure. The CMG creates the HTTPS service using the server authentication certificate.

2. The CMG connection point connects to the CMG in Azure. It holds the connection open, and builds the channel for future two-way communication.

    - When you deploy the CMG as a virtual machine scale set, this flow is over HTTPS.

    - If you deploy the CMG as a classic cloud service, it first tries TCP-TLS. If that connection fails, it switches to HTTPS.

    For more information, see [Note 2: CMG connection point HTTPS ports for one VM](#bkmk_port-note2).

3. The client connects to the CMG over HTTPS port 443. It authenticates using Azure AD, the client authentication certificate, or a site-issued token.

    > [!NOTE]
    > If you enable the CMG to serve content, the client connects directly to Azure blob storage over HTTPS port 443. For more information, see [Content data flow](#content-data-flow).

4. The CMG forwards the client communication over the existing connection to the on-premises CMG connection point. You don't need to open any inbound firewall ports.

5. The CMG connection point forwards the client communication to the on-premises management point and software update point.

For more information when you integrate with Azure AD, see [Configure Azure services: Cloud management data flow](../../../servers/deploy/configure/azure-services-wizard.md#cloud-management-data-flow).

### Content data flow

When a client uses a CMG as a content location:

1. The management point gives the client an access token along with the list of content sources. This token is valid for 24 hours, and gives the client access to the cloud-based content source.

1. The management point responds to the client's location request with the _service name_ of the CMG. This property is the same as the common name of the server authentication certificate.

    If you're using your domain name, for example, `WallaceFalls.contoso.com`, then the client first tries to resolve this FQDN. Clients use the CNAME alias in your domain's internet-facing DNS to resolve the Azure deployment name.

1. The client next resolves the _deployment name_ to a valid IP address. This response is handled by Azure's DNS.

1. The client connects to the CMG. Azure load balances the connection to one of the VM instances. The client authenticates itself using the access token.

1. The CMG authenticates the client's access token, and then gives the client the exact content location in Azure storage.

1. If the client trusts the CMG's server authentication certificate, it connects to Azure storage to download the content.

## Required ports

This table lists the required network ports and protocols. The *Client* is the device that starts the connection, requiring an outbound port. The *Server* is the device that accepts the connection, requiring an inbound port.

| Client | Protocol | Port | Server | Description |
|--------|----------|------|--------|-------------|
| Service connection point | HTTPS | 443 | Azure | CMG deployment |
| CMG connection point (virtual machine scale set) | HTTPS | 443 | CMG service | Protocol to build CMG channel to only one VM instance <sup>[Note 2](#bkmk_port-note2)</sup> |
| CMG connection point (virtual machine scale set) | HTTPS | 10124-10139 | CMG service | Protocol to build CMG channel to two or more VM instances <sup>[Note 3](#bkmk_port-note3)</sup> |
| CMG connection point (classic cloud service) | TCP-TLS | 10140-10155 | CMG service | Preferred protocol to build CMG channel <sup>[Note 1](#bkmk_port-note1)</sup> |
| CMG connection point (classic cloud service) | HTTPS | 443 | CMG service | Fall back protocol to build CMG channel to only one VM instance <sup>[Note 2](#bkmk_port-note2)</sup> |
| CMG connection point (classic cloud service) | HTTPS | 10124-10139 | CMG service | Fall back protocol to build CMG channel to two or more VM instances <sup>[Note 3](#bkmk_port-note3)</sup> |
| Client | HTTPS | 443 | CMG | General client communication |
| Client | HTTPS | 443 | Blob storage | Download cloud-based content |
| CMG connection point | HTTPS or HTTP | 443 or 80 | Management point | On-premises traffic, port depends upon management point configuration |
| CMG connection point | HTTPS or HTTP | 443 or 80 / 8530 or 8531 | Software update point | On-premises traffic, port depends upon software update point configuration |

### Notes on ports

#### <a name="bkmk_port-note1"></a> Note 1: CMG connection point TCP-TLS ports

These ports only apply when you deploy the CMG as a **cloud service (classic)**, which was the only method available in version 2006 and earlier.

The CMG connection point first tries to establish a long-lived TCP-TLS connection with each CMG VM instance. It connects to the first VM instance on port 10140. The second VM instance uses port 10141, up to the 16th on port 10155. A TCP-TLS connection has the best performance, but it doesn't support internet proxy. If the CMG connection point can't connect via TCP-TLS, then it falls back to HTTPS<sup>[Note 2](#bkmk_port-note2)</sup>.

#### <a name="bkmk_port-note2"></a> Note 2: CMG connection point HTTPS ports for one VM

If you deploy the CMG in a **virtual machine scale set**, the CMG connection point only communicates with the service in Azure over HTTPS. It doesn't require TCP-TLS ports to build the CMG communication channel.

For a CMG deployed as a classic cloud service, it only uses this port if the TCP-TLS connection fails. If the CMG connection point can't connect to the CMG via TCP-TLS<sup>[Note 1](#bkmk_port-note1)</sup>, it connects to the Azure network load balancer over HTTPS 443. This behavior is only for one VM instance.

#### <a name="bkmk_port-note3"></a> Note 3: CMG connection point HTTPS ports for two or more VMs

If there are two or more VM instances, the CMG connection point uses HTTPS 10124 to the first VM instance, not HTTPS 443. It connects to the second VM instance on HTTPS 10125, up to the 16th on HTTPS port 10139.

## Internet access requirements

If your organization restricts network communication with the internet using a firewall or proxy device, you need to allow the CMG connection point and service connection point to access internet endpoints.

For more information, see [Internet access requirements](../../../plan-design/network/internet-endpoints.md#cloud-services).

[!INCLUDE [Internet endpoints for cloud services](../../../plan-design/network/includes/internet-endpoints-cloud-services.md)]

## HTTP headers and verbs

Any networking device that manages communication between the client, the CMG, and the on-premises site systems has to allow the following HTTP headers and verbs. If these items are blocked, it will affect client communication through the CMG.<!-- MEMDocs#1309 -->

### HTTP headers

- Range:
- CCMClientID:
- CCMClientIDSignature:
- CCMClientTimestamp:
- CCMClientTimestampsSignature:

### HTTP verbs

- HEAD
- CCM_POST
- BITS_POST
- GET
- PROPFIND
