---
title: "Firewalls and domains"
titleSuffix: "Configuration Manager"
description: "Set up firewalls, ports, and domains to prepare for System Center Configuration Manager communications."
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Set up firewalls, ports, and domains for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

To prepare your network to support System Center Configuration Manager, plan to set up infrastructure like firewalls to pass the communications used by Configuration Manager.  

|Consideration|Details|  
|-------------------|-------------|  
|**Ports and protocols** that different Configuration Manager capabilities use. Some ports are required, and you can customize other **domains and services**.|Most Configuration Manager communications use common ports like port 80 for HTTP or 443 for HTTPS communication. However, [some site system roles support the use of custom websites](/sccm/core/plan-design/network/websites-for-site-system-servers) and custom ports.<br /><br /> **Before you deploy Configuration Manager**, identify the ports that you plan to use and set up firewalls accordingly.<br /><br /> **If you need to change a port** after you install Configuration Manager, don't forget to update firewalls on devices and the network and also change the configuration of the port from within Configuration Manager.<br /><br /> For more information see: </br>- [How to configure client communication ports](../../../core/clients/deploy/configure-client-communication-ports.md) </br>- [Ports used in Configuration Manager](../../../core/plan-design/hierarchy/ports.md) </br>- [Internet access requirements for the service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)|  
|**Domains and services** that site servers and clients might need to use.|Configuration Manager capabilities can require site servers and clients to have access to specific services and domains on the Internet, like Windowsudpate.microsoft.com or the Microsoft Intune service.<br /><br /> If you will use Microsoft Intune to manage mobile devices, you must also set up access to [ports and domains that Intune requires.](https://docs.microsoft.com/intune/get-started/network-infrastructure-requirements-for-microsoft-intune)|  
|**Proxy servers** for site system servers and for client communications. You can specify separate proxy servers for different site system servers and clients.|Because these configurations are made at the time you install a site system role or client, you only need to be aware of the proxy server configurations for later reference when you configure site system roles and clients.<br /><br /> If you're not sure your deployment will need to use proxy servers, review [Proxy server support in System Center Configuration Manager](../../../core/plan-design/network/proxy-server-support.md) to learn about  site system roles and client actions that can use a proxy server.|   
|  
