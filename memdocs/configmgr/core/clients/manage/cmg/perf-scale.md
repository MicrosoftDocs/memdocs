---
title: CMG performance and scale
titleSuffix: Configuration Manager
description: Plan how the design the cloud management gateway (CMG) for the best performance at the appropriate scale.
ms.date: 07/16/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# CMG performance and scale

*Applies to: Configuration Manager (current branch)*

The supported scale and performance of the cloud management gateway (CMG) is based on the number of devices that you expect to simultaneously connect to the service. Use the information in this article to determine how many of the following components you need in your environment for the best performance at the appropriate scale:

- CMG cloud service
- Virtual machine instances for each CMG
- CMG connection point site system on your internal network

> [!NOTE]
> Sizing guidance for management points and software update points doesn't change whether they service on-premises or internet-based clients. For more information, see [Size and scale numbers](../../../plan-design/configs/size-and-scale-numbers.md).

## Size and scale for CMG

[!INCLUDE [Size and scale for cloud management gateway](../../../plan-design/configs/includes/scale-cmg.md)]

## Size and scale for CMG connection point

[!INCLUDE [Size and scale for cloud management gateway connection point](../../../plan-design/configs/includes/scale-cmgcp.md)]

## Improve performance

The following recommendations can help you improve CMG performance:

- The connection between the Configuration Manager client and the CMG isn't region-aware. Client communication is largely unaffected by latency and geographic separation. It's generally not necessary to deploy multiple CMG for the purposes of geo-proximity. Deploy the CMG at the top-level site in your hierarchy. To increase scale, add VM instances.

- For high availability of the service, create a CMG with at least two VM instances and two CMG connection points per site.

- Scale the CMG to support more clients by adding more VM instances. The Azure load balancer controls client connections to the service.

- Create more CMG connection points to distribute the load among them. The CMG distributes the traffic to its connecting CMG connection points in a round-robin fashion.

> [!NOTE]
> The CMG connection point creates a TCP connection to the management point for each client. While Configuration Manager has no hard limit on the number of clients for a CMG connection point, Windows Server has a default maximum TCP dynamic port range of 16,384. If a Configuration Manager site manages more than 16,384 clients with a single CMG connection point, add another site system or increase the Windows Server limit. All clients maintain a channel for client notifications, which holds a port open on the CMG connection point. For more information on how to increase this limit, see [Microsoft Support article 929851](https://support.microsoft.com/help/929851).

## Next steps

Next, understand the costs associated with operating an Azure service for the CMG:
  
> [!div class="nextstepaction"]
> [Cost of cloud management gateway](cost.md)
