---
title: "VPN profiles in System Center Configuration Manager"
description: "Learn how to use VPN profiles in System Center Configuration Manager to deploy VPN settings to users in your organization."
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: 6
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---
# VPN profiles in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


Use VPN profiles in System Center Configuration Manager (also known as ConfigMgr or SCCM) to deploy VPN settings to users in your organization. By deploying these settings, you minimize the end-user effort required to connect to resources on the company network.  

 For example, you want to provision all devices that run the Windows RT operating system with the settings required to connect to a file share on the corporate network. You can create a VPN profile containing the settings necessary to connect to the corporate network and then deploy this profile to all users that have devices that run Windows RT in your hierarchy. Users of Windows RT devices see the VPN connection in the list of available networks and can connect to this network with minimum effort.  

 When you create a VPN profile, you can include a wide range of security settings, including certificates for server validation and client authentication that have been provisioned by using System Center Configuration Manager certificate profiles. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

 The sections below explain what devices you can configure with VPN profiles if you are using Configuration Manager.

 See [VPN profiles on mobile devices](/sccm/mdm/deploy-use/create-vpn-profiles) to review the devices you can configure when using Configuration Manager with Microsoft Intune.  

## VPN profiles when using Configuration Manager  
 The following table describes the VPN profiles you can configure for various device platforms.  

|Connection type|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|No|No|No|No|  
|**Pulse Secure**|Yes|No|Yes|Yes|  
|**F5 Edge Client**|Yes|No|Yes|Yes|  
|**Dell SonicWALL Mobile Connect**|Yes|No|Yes|Yes|  
|**Check Point Mobile VPN**|Yes|No|Yes|Yes|  
|**Microsoft SSL (SSTP)**|Yes|Yes|Yes|No|  
|**Microsoft Automatic**|Yes|Yes|Yes|No|  
|**IKEv2**|Yes|Yes|Yes|No|  
|**PPTP**|Yes|Yes|Yes|No|  
|**L2TP**|Yes|Yes|Yes|No|  

### Next steps  
 Use the following topics to help you plan for, configure, operate, and maintain VPN profiles in Configuration Manager.  

-   [Prerequisites for VPN profiles in System Center Configuration Manager](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Security and privacy for VPN profiles in System Center Configuration Manager](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
