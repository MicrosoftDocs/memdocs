---
title: "Configure firewalls, ports, and domains for System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
translation.priority.ht: 
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Configure firewalls, ports, and domains for System Center Configuration Manager
To prepare your network to support System Center Configuration Manager, plan to configure infrastructure like firewalls to pass the communications used by Configuration Manager.  
  
|Consideration|Details|  
|-------------------|-------------|  
|**Ports and protocols** used by different Configuration Manager capabilities. Some ports are required, while other **Domains and services** can be customized.|Most Configuration Manager communications use common ports such as port 80 for HTTP or 443 for HTTPS communication. However, [some site system roles support use of custom websites](https://technet.microsoft.com/library/mt426625.aspx) and custom ports.<br /><br /> **Before you deploy Configuration Manager**, identify the ports you plan to use and configure firewalls accordingly.<br /><br /> **Later, if you need to change a port** after you install Configuration Manager, don't forget to update firewalls on devices and the network and also change the configuration of the port from within Configuration Manager.<br /><br /> For more information see, [How to configure client communication ports in System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md) and [Ports used in System Center Configuration Manager](../../../core/plan-design/hierarchy/ports.md).|  
|**Domains and services** that site servers and clients might need to access.|Configuration Manager capabilities can require site servers and clients have access to specific services and Domains on the internet, like Windowsudpate.microsoft.com or the Microsoft Intune service.<br /><br /> If you will use Microsoft Intune to manage mobile devices, you must also configure access to [ports and domains that are required by Intune.](https://technet.microsoft.com/dn646950.aspx)|  
|**Proxy servers** for site system servers and for client communications. You can specify separate proxy servers for different site system servers and clients.|Because these configurations are made at the time you install a site system role or client, you only need to be aware of the proxy server configurations for later reference when you configure site system roles and clients.<br /><br /> If you’re not sure your deployment will need to use proxy servers, review [Proxy server support in System Center Configuration Manager](../../../core/plan-design/network/proxy-server-support.md) to learn about  site system roles and client actions that can use a proxy server.|  
  
## See Also  
 [Prepare your network environment for System Center Configuration Manager](../Topic/Prepare%20your%20network%20environment%20for%20System%20Center%20Configuration%20Manager.md)