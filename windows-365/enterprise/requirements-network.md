---
# required metadata
title: Network requirements for Windows 365
titleSuffix:
description: Learn about the network requirements for using Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/02/2021 
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chbrinkh
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Network requirements

Windows 365 is a cloud-based service that lets users connect through the internet from any device, from any place, to a Windows Desktop running in Azure. To support these internet connections, you must comply with the networking requirements listed below.

Each customer has its specific requirements based on the workload they use to pre-calculate the network requirements of their Cloud PC environment.  

## General network requirements

To use Cloud PCs, you must meet the following requirements:

- Azure virtual network: You must have a virtual network (vNET) in your Azure subscription in the same region as where the Windows 365 desktops are created.
- The Azure virtual network must be able to resolve DNS entries for your Active Directory Domain Services (AD DS) environment. To do this is, define your AD DS DNS servers as the DNS servers for the virtual network.
- The Azure vNet must have network access to an enterprise domain controller, either in Azure or on-premises.
- Network bandwidth: See [Azure’s Network guidelines](/windows-server/remote/remote-desktop-services/network-guidance).
- A subnet within the vNet and available IP address space.

## Allow network connectivity

You must allow traffic in your Azure network configuration to the following service URLs and ports:

- [Network endpoints for Microsoft Intune](/mem/intune/fundamentals/intune-endpoints)
- [Azure Virtual Desktop required URL list](/azure/virtual-desktop/safe-url-list)
- rdweb.wvd.microsoft.com
- rdbroker.wvd.microsoft.com
- Provisioning and on-premises network connection endpoints:
  - cpcsacnrysa1prodprna02.blob.core.windows.net
  - cpcsacnrysa1prodprap01.blob.core.windows.net
  - cpcsacnrysa1prodprau01.blob.core.windows.net
  - cpcsacnrysa1prodpreu01.blob.core.windows.net
  - cpcsacnrysa1prodpreu02.blob.core.windows.net
  - cpcsacnrysa1prodprna01.blob.core.windows.net
  - cpcstprovprodpreu01.blob.core.windows.net
  - cpcstprovprodpreu02.blob.core.windows.net
  - cpcstprovprodprna01.blob.core.windows.net
  - cpcstprovprodprna02.blob.core.windows.net
  - cpcstprovprodprap01.blob.core.windows.net
  - cpcstprovprodprau01.blob.core.windows.net
  - prna01.prod.cpcgateway.trafficmanager.net
  - prna02.prod.cpcgateway.trafficmanager.net
  - preu01.prod.cpcgateway.trafficmanager.net
  - preu02.prod.cpcgateway.trafficmanager.net
  - prap01.prod.cpcgateway.trafficmanager.net
  - prau01.prod.cpcgateway.trafficmanager.net
- Cloud PC communication endpoints
  - endpointdiscovery.cmdagent.trafficmanager.net
  - registration.prna01.cmdagent.trafficmanager.net
  - registration.preu01.cmdagent.trafficmanager.net
  - registration.prap01.cmdagent.trafficmanager.net
  - registration.prau01.cmdagent.trafficmanager.net
- Registration endpoints
  - login.microsoftonline.com
  - login.live.com
  - enterpriseregistration.windows.net
  - global.azure-devices-provisioning.net (443 & 5671 outbound)
  - hm-iot-in-*._azure-devices.net (443 & 5671 outbound)



All endpoints connect over port 443.

## DNS requirements

As part of the Hybrid Azure AD Join requirements, your Cloud PCs must be able to join on-prem Active Directory. That requires that the Cloud PCs be able to resolve DNS records for your on-prem AD environment. 

Configure your Azure Virtual Network where the Cloud PCs are provisioned as follows:

1. Make sure that your Azure Virtual Network has network connectivity to DNS servers that can resolve your Active Directory domain.
2. From the Azure Virtual Network's Settings, select DNS Servers and then choose Custom.
3. Enter the IP address of DNS servers that environment that can resolve your AD DS domain.

>[!TIP]
>Adding at least two DNS servers, as you would with a physical PC, helps mitigate the risk of a single point of failure in name resolution.

See the Azure docs for more information on [configuring Azure Virtual Networks settings](/azure/virtual-network/manage-virtual-network#change-dns-servers). 

## Remote Desktop Protocol requirements

Windows 365 uses the Remote Desktop Protocol (RDP).

| Scenario | Default mode | H.264/AVC 444 mode | Description |
| --- | --- | --- | --- |
| Idle | 0.3 Kbps | 0.3 Kbps | User has paused their work and there are no active screen updates. |
| Microsoft Word | 100-150 Kbps | 200-300 Kbps | User is actively working with Microsoft Word: typing, pasting graphics, and switching between documents. |
| Microsoft Excel | 150-200 Kbps | 400-500 Kbps | User is actively working with Microsoft Excel: multiple cells with formulas and charts are updated simultaneously |
| Microsoft PowerPoint | 4-4.5 Mbps | 1.6-1.8 Mbps | User is actively working with Microsoft PowerPoint: typing, pasting, modifying rich graphics, and using slide transition effects. |
| Web Browsing | 6-6.5 Mbps | 0.9-1 Mbps | User is actively working with a graphically rich website that contains multiple static and animated images. User scrolls the pages both horizontally and vertically |
| Image Gallery | 3.3-3.6 Mbps | 0.7-0.8 Mbps | User is actively working with the image gallery application: browsing, zooming, resizing, and rotating images |
| Video playback | 8.5-9.5 Mbps | 2.5-2.8 Mbps | User is watching a 30 FPS video that consumes 1/2 of the screen. |
| Fullscreen Video playback | 7.5-8.5 Mbps | 2.5-3.1 Mbps | User is watching a 30 FPS video that’s maximized to a full screen. |

## Microsoft Teams requirements

Microsoft Teams is one of the core Microsoft 365 services within Cloud PC. Windows 365 offloads the audio and video traffic to your endpoint to make the video experience like Teams on a physical PC.

The network quality is very important per scenario. Make sure that you have the proper bandwidth available for the quality that you want to offer.

Full HD (1920x1080p) isn’t a supported resolution for Microsoft Teams on Cloud PCs.

| Bandwidth (up/down) | Scenarios |
| --- | --- |
| 30 kbps | Peer-to-peer audio calling. |
| 130 kbps | Peer-to-peer audio calling and screen sharing. |
| 500 kbps | Peer-to-peer quality video calling 360p at 30 fps. |
| 1.2 Mbps | Peer-to-peer HD quality video calling with resolution of HD 720p at 30 fps. |
| 500kbps/1Mbps | Group Video calling. |

## Traffic interception technologies

Some enterprise customers use traffic interception, SSL decryption, deep packet inspection, and other similar technologies for security teams to monitor network traffic. Cloud PC provisioning may need direct access to the virtual machine. These traffic interception technologies can causes issues with running on-premises network connection checks or Cloud PC provisioning. Make sure no network interception is enforced for Cloud PCs provisioned within the Windows 365 service.

<!-- ########################## -->
## Next steps

[Learn about Cloud PC role-based access control](role-based-access.md).
