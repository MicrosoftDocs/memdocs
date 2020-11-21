---
title: Data flow for cloud management gateway
titleSuffix: Configuration Manager
description: Understand how data flows between components of the cloud management gateway (CMG), including network ports and internet endpoints.
ms.date: 09/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: reference
ms.assetid: 2c82c162-d35d-4659-bbe9-1479a16976fd
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Data flow for cloud management gateway

*Applies to: Configuration Manager (current branch)*

Use this article to understand how data flows between components of the cloud management gateway (CMG). It requires specific network ports and internet endpoints to function. You don't need to open any inbound ports to your on-premises network. The service connection point and CMG connection point site system roles start all communication with Azure and the CMG. These two roles need to create outbound connections to the Microsoft cloud. The service connection point deploys and monitors the service in Azure, so needs to be online. The CMG connection point connects to the CMG to manage communication between the CMG and on-premises site system roles.

## Data flow diagram

The following diagram is a basic, conceptual data flow for the CMG:

:::image type="content" source="media/cmg-data-flow.png" alt-text="Data flow diagram for cloud management gateway (CMG)" lightbox="media/cmg-data-flow.png":::

1. The service connection point connects to Azure over HTTPS port 443. It authenticates using Azure AD or the Azure management certificate. The service connection point deploys the CMG in Azure. The CMG creates the HTTPS cloud service using the server authentication certificate.

2. The CMG connection point connects to the CMG in Azure over TCP-TLS or HTTPS. It holds the connection open, and builds the channel for future two-way communication.

3. The client connects to the CMG over HTTPS port 443. It authenticates using Azure AD, the client authentication certificate, or a site-issued token.

    > [!NOTE]
    > If you enable the CMG to serve content or use a cloud distribution point, the client connects directly to Azure blob storage over HTTPS port 443. For more information, see [Use a cloud-based distribution point](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow).<!-- SCCMDocs#2332 -->

4. The CMG forwards the client communication over the existing connection to the on-premises CMG connection point. You don't need to open any inbound firewall ports.

5. The CMG connection point forwards the client communication to the on-premises management point and software update point.

For more information when you store content in Azure, see [Use a cloud-based distribution point](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow).

For more information when you integrate with Azure Active Directory (Azure AD), see [Configure Azure services: Cloud management data flow](../../../servers/deploy/configure/azure-services-wizard.md#cloud-management-data-flow).

## Required ports

This table lists the required network ports and protocols. The *Client* is the device that starts the connection, requiring an outbound port. The *Server* is the device that accepts the connection, requiring an inbound port.

| Client | Protocol | Port | Server | Description |
|--------|----------|------|--------|-------------|
| Service connection point | HTTPS | 443 | Azure | CMG deployment |
| CMG connection point | TCP-TLS | 10140-10155 | CMG service | Preferred protocol to build CMG channel <sup>[Note 1](#bkmk_port-note1)</sup> |
| CMG connection point | HTTPS | 443 | CMG service | Fall back protocol to build CMG channel to only one VM instance <sup>[Note 2](#bkmk_port-note2)</sup> |
| CMG connection point | HTTPS | 10124-10139 | CMG service | Fall back protocol to build CMG channel to two or more VM instances <sup>[Note 3](#bkmk_port-note3)</sup> |
| Client | HTTPS | 443 | CMG | General client communication |
| Client | HTTPS | 443 | Blob storage | Download cloud-based content |
| CMG connection point | HTTPS or HTTP | 443 or 80 | Management point | On-premises traffic, port depends upon management point configuration |
| CMG connection point | HTTPS or HTTP | 443 or 80 / 8530 or 8531 | Software update point | On-premises traffic, port depends upon software update point configuration |

When you allow the CMG to function as a cloud distribution point and serve content from Azure storage, some additional requirements apply. For more information, see [Use a cloud distribution point: Ports and data flow](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### Notes on ports

#### <a name="bkmk_port-note1"></a> Note 1: CMG connection point TCP-TLS ports

The CMG connection point first tries to establish a long-lived TCP-TLS connection with each CMG VM instance. It connects to the first VM instance on port 10140. The second VM instance uses port 10141, up to the 16th on port 10155. A TCP-TLS connection has the best performance, but it doesn't support internet proxy. If the CMG connection point can't connect via TCP-TLS, then it falls back to HTTPS<sup>[Note 2](#bkmk_port-note2)</sup>.

#### <a name="bkmk_port-note2"></a> Note 2: CMG connection point HTTPS ports for one VM

If the CMG connection point can't connect to the CMG via TCP-TLS<sup>[Note 1](#bkmk_port-note1)</sup>, it connects to the Azure network load balancer over HTTPS 443 only for one VM instance.  

#### <a name="bkmk_port-note3"></a> Note 3: CMG connection point HTTPS ports for two or more VMs

If there are two or more VM instances, the CMG connection point uses HTTPS 10124 to the first VM instance, not HTTPS 443. It connects to the second VM instance on HTTPS 10125, up to the 16th on HTTPS port 10139.

## Internet access requirements

If your organization restricts network communication with the internet using a firewall or proxy device, you need to allow the CMG connection point and service connection point to access internet endpoints.

For more information, see [Internet access requirements](../../../plan-design/network/internet-endpoints.md#bkmk_cloud).

[!INCLUDE [Internet endpoints for cloud services](../../../plan-design/network/includes/internet-endpoints-cloud-services.md)]
