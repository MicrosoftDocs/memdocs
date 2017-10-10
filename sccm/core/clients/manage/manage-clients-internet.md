---
title: "Manage clients on the Internet "
description: "Learn about managing clients with cloud management gateway and Internet-based client management in Configuration Manager."
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: arob98
ms.author: angrobe
manager: angrobe
---

# Manage clients on the Internet with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Typically in Configuration Manager, most of the computers and servers that are being managed are physically on the same internal private or corporate network as the site system servers that perform management functions. However, you can manage client computers outside your corporate network if they are connected to the Internet without requiring the clients to connect via virtual private networks to reach the site system servers.

Configuration Manager provides two ways to manage Internet connected clients:

-   Cloud management gateway

-   Internet-based client management

## Cloud management gateway

Beginning in version 1610, Configuration Manager introduces cloud management gateway. This new method provides a way to manage Internet-based clients using a combination of a cloud service deployed to Microsoft Azure and a new site system role that communicates with that service. Clients then use the service to communicate with Configuration Manager.

Advantages:

-   No additional infrastructure investment required.

-   Does not expose on-premises infrastructure to the Internet.

-   Cloud virtual machines that run the service are fully managed by Azure and require no maintenance.

-   Easily set up and configured in the Configuration Manager console.

Disadvantages:

-   Cloud subscription cost.

-   Management data sent through cloud service.

For more information, see [Plan for cloud management gateway](plan-cloud-management-gateway.md).

## Internet-based client management

This method relies on Internet-facing site system servers to which clients communicate for management purposes. This method requires clients and site system servers to be configured for Internet-based management.

Advantages:

-   No cloud service dependency.

-   No additional cost associated with a cloud subscription.

-   Full control of servers and roles providing the service.

Disadvantages:

-   Require additional infrastructure investment.

-   Overhead and operational cost of additional infrastructure.

-   Infrastructure must be exposed to the Internet.

For more information, see [Plan for Internet-based client management](plan-internet-based-client-management.md).
