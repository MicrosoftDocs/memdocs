---
title: Manage clients over the internet
titleSuffix: Configuration Manager
description: Learn about managing clients with cloud management gateway and internet-based client management in Configuration Manager.
ms.date: 08/02/2021
ms.subservice: client-mgt
ms.topic: conceptual
ms.service: configuration-manager
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Manage clients over the internet with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Typically in Configuration Manager, most of the managed computers and servers are physically on the same internal network as the site system servers that perform management functions. However, you can manage clients outside your internal network when they are connected to the internet. This ability doesn't require the clients to connect via VPN to reach the site system servers.

Configuration Manager provides two ways to manage internet-connected clients:

- Cloud management gateway

- Internet-based client management

> [!NOTE]
> You can have a combination of both services for a single site. If a device gets policy from the site for both IBCM and CMG, then it randomizes between them for communication. The only mechanism available to control communication is client authentication. For example, if a Microsoft Entra joined client doesn't trust the server authentication certificate of the internet-based management point, it can only use the CMG. If a domain-joined client doesn't trust the server authentication certificate of the CMG, it can only use the internet-based management point.<!-- SCCMDocs#1541 -->

## Cloud management gateway

The cloud management gateway provides management of internet-based clients. It uses a combination of a Microsoft Azure cloud service, and an on-premises site system role that communicates with that service. Internet-based clients use the cloud service to communicate with the on-premises Configuration Manager.

### CMG advantages

- No additional on-premises infrastructure investment required.  

- Does not expose on-premises infrastructure to the internet.  

- Cloud virtual machines that run the service are fully managed by Azure and require no maintenance.  

- Easily set up and configured in the Configuration Manager console.  

### CMG disadvantages  

- Cloud subscription cost.  

- Management data sent through cloud service.  

## Internet-based client management

This method relies on internet-facing site system servers to which clients directly communicate for management purposes. It requires clients and site system servers to be configured for internet-based client management (IBCM).

### IBCM advantages

- No cloud service dependency.  

- No additional cost associated with a cloud subscription.  

- Full control of servers and roles providing the service.  

### IBCM disadvantages

- Require additional infrastructure investment.  

- Overhead and operational cost of additional infrastructure.  

- Infrastructure must be exposed to the internet.  

## Next steps

[Overview of cloud management gateway](cmg/overview.md)

[Plan for internet-based client management](plan-internet-based-client-management.md)
