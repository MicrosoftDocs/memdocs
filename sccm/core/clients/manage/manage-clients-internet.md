---
title: Manage clients on the internet
titleSuffix: Configuration Manager
description: Learn about managing clients with cloud management gateway and internet-based client management in Configuration Manager.
ms.date: 03/21/2018
ms.prod: configuration-manager
ms.technology:
  - configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Manage clients on the internet with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Typically in Configuration Manager, most of the managed computers and servers are physically on the same internal network as the site system servers that perform management functions. However, you can manage clients outside your internal network when they are connected to the internet. This ability doesn't require the clients to connect via VPN to reach the site system servers.

Configuration Manager provides two ways to manage internet-connected clients:

-   Cloud management gateway

-   Internet-based client management


## Cloud management gateway

The cloud management gateway provides management of internet-based clients. It uses a combination of a Microsoft Azure cloud service, and a new site system role that communicates with that service. Internet-based clients use the cloud service to communicate with the on-premises Configuration Manager.

#### Advantages  

-   No additional infrastructure investment required.  

-   Does not expose on-premises infrastructure to the internet.  

-   Cloud virtual machines that run the service are fully managed by Azure and require no maintenance.  

-   Easily set up and configured in the Configuration Manager console.  

#### Disadvantages  

-   Cloud subscription cost.  

-   Management data sent through cloud service.  

For more information, see [Plan for cloud management gateway](plan-cloud-management-gateway.md).  



## Internet-based client management

This method relies on internet-facing site system servers to which clients communicate for management purposes. It requires clients and site system servers to be configured for internet-based management.

#### Advantages  

-   No cloud service dependency.  

-   No additional cost associated with a cloud subscription.  

-   Full control of servers and roles providing the service.  

#### Disadvantages  

-   Require additional infrastructure investment.  

-   Overhead and operational cost of additional infrastructure.  

-   Infrastructure must be exposed to the internet.  

For more information, see [Plan for internet-based client management](plan-internet-based-client-management.md).  
