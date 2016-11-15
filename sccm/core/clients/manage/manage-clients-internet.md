---
title: "Manage clients | Internet | Cloud Management Gateway | System Center Configuration Manager"
description: ""
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
  - configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: Mtillman
ms.author: mtillman
manager: angrobe
---

# Manage clients on the Internet in Configuration Manager

Typically in Configuration Manager, most of the computers and servers that are being managed are physically on the same internal private or corporate network as the site system servers that perform management functions. However, you can manage client computers outside your corporate network if they are connected to the Internet without requiring the clients to connect via virtual private networks to reach the site system servers.

Configuration Manager provides two ways to manage Internet connected clients:

- **Cloud management gateway**

  Beginning in version 1610, Configuration Manager introduces cloud management gateway. This new method provides a way to manage Internet-based clients using a combination of a cloud service deployed to Microsoft Azure and a new site system role that communicates with that service. Clients then use the service to communicate with Configuration Manager. For more information, see [Plan for cloud management gateway](plan-cloud-management-gateway.md).

- **Internet-based client management**

  This legacy method relies on Internet-facing site system servers to which clients communicate for management purposes. This method requires clients and site system servers to be configured for Internet-based management. For more infomation, see [Plan for Internet-based client management](plan-internet-based-client-management.md).
