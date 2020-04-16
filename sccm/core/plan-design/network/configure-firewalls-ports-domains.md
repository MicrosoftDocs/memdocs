---
title: Network infrastructure
titleSuffix: Configuration Manager
description: Set up firewalls, ports, and domains to prepare for Configuration Manager communications.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby


---

# Network infrastructure considerations for Configuration Manager

*Applies to: Configuration Manager (current branch)*

To prepare your network to support Configuration Manager, you may need to configure some infrastructure components. For example, open firewall ports to pass the communications used by Configuration Manager.  

## Ports and protocols

Different Configuration Manager features use different network ports. Some ports are required, and some you can customize.

Most Configuration Manager communications use common ports like port 80 for HTTP or 443 for HTTPS. Some site system roles support the use of custom websites and custom ports. For more information, see [Websites for site system servers](/sccm/core/plan-design/network/websites-for-site-system-servers).

Before you deploy Configuration Manager, identify the ports that you plan to use, and set up firewalls as needed.

After you install Configuration Manager, if you need to change a port, don't forget to update firewalls on devices and the network. Also change the configuration of the port in Configuration Manager.

For more information, see the following articles:

- [How to configure client communication ports](/sccm/core/clients/deploy/configure-client-communication-ports)
- [Ports used in Configuration Manager](/sccm/core/plan-design/hierarchy/ports)


## Internet access requirements

Some Configuration Manager features rely on internet connectivity for full functionality. If your organization restricts network communication with the internet using a firewall or proxy device, make sure to allow the necessary endpoints.

For more information, see [Internet access requirements](/sccm/core/plan-design/network/internet-endpoints)


## Proxy servers

You can specify separate proxy servers for different site system servers and clients. You make these configurations when you install a site system role or client, or change them later as needed.

For more information, see [Proxy server support](/sccm/core/plan-design/network/proxy-server-support).
