---
# required metadata
title: Network requirements for Windows 365
titleSuffix:
description: Learn about the network requirements for using Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 03/10/2022 
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

Windows 365 is a cloud-based service that lets users connect through the internet from any device, from any place, to a Windows Desktop running in Azure. To support these internet connections, you must follow the networking requirements listed below.

Each customer has its specific requirements based on the workload they use to pre-calculate the network requirements of their Cloud PC environment.  

>[!Note]
>This article only applies if you plan on provisioning Cloud PCs on your own Azure virtual network, as opposed to a Microsoft-hosted network.

## General network requirements

To use your own network and provision Azure AD joined Cloud PCs, you must meet the following requirements:

- Azure virtual network: You must have a virtual network (vNET) in your Azure subscription in the same region as where the Windows 365 desktops are created.
- Network bandwidth: See [Azure’s Network guidelines](/windows-server/remote/remote-desktop-services/network-guidance).
- A subnet within the vNet and available IP address space.

To use your own network and provision Hybrid Azure AD joined Cloud PCs, you must meet the above requirements, and the following requirements:

- The Azure virtual network must be able to resolve DNS entries for your Active Directory Domain Services (AD DS) environment. To support this resolution, define your AD DS DNS servers as the DNS servers for the virtual network.
- The Azure vNet must have network access to an enterprise domain controller, either in Azure or on-premises.

## Allow network connectivity

You must allow traffic in your Azure network configuration to the following service URLs and ports:

- [Network endpoints for Microsoft Intune](/mem/intune/fundamentals/intune-endpoints)
- [Azure Virtual Desktop required URL list](/azure/virtual-desktop/safe-url-list)
- rdweb.wvd.microsoft.com
- rdbroker.wvd.microsoft.com
- Provisioning and Azure network connection endpoints:
  - cpcsaamssa1prodprap01.blob.core.windows.net
  - cpcsaamssa1prodprau01.blob.core.windows.net
  - cpcsaamssa1prodpreu01.blob.core.windows.net
  - cpcsaamssa1prodpreu02.blob.core.windows.net
  - cpcsaamssa1prodprna01.blob.core.windows.net
  - cpcsaamssa1prodprna02.blob.core.windows.net
  - cpcsacnrysa1prodprna02.blob.core.windows.net
  - cpcsacnrysa1prodprap01.blob.core.windows.net
  - cpcsacnrysa1prodprau01.blob.core.windows.net
  - cpcsacnrysa1prodpreu01.blob.core.windows.net
  - cpcsacnrysa1prodpreu02.blob.core.windows.net
  - cpcsacnrysa1prodprna01.blob.core.windows.net
  - cpcstcnryprodprap01.blob.core.windows.net
  - cpcstcnryprodprau01.blob.core.windows.net
  - cpcstcnryprodpreu01.blob.core.windows.net
  - cpcstcnryprodprna01.blob.core.windows.net
  - cpcstcnryprodprna02.blob.core.windows.net
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
  - hm-iot-in-prod-preu01.azure-devices.net (443 & 5671 outbound)
  -	hm-iot-in-prod-prap01.azure-devices.net (443 & 5671 outbound)
  -	hm-iot-in-prod-prna01.azure-devices.net (443 & 5671 outbound)
  - hm-iot-in-prod-prau01.azure-devices.net (443 & 5671 outbound)

All endpoints connect over port 443.

### Remote Desktop Protocol (RDP) broker service endpoints

Direct connectivity to Azure Virtual Desktop RDP broker service endpoints is critical for remoting performance to a Cloud PC. These endpoints affect both connectivity and latency. To align with the [Microsoft 365 network connectivity principles](/microsoft-365/enterprise/microsoft-365-network-connectivity-principles#new-office-365-endpoint-categories), you should categorize these endpoints as **Optimize** endpoints. We recommend that you use a direct path from your Azure virtual network to those endpoints.

To make it easier to configure network security controls, use Azure Virtual Desktop service tags to identity those endpoints for direct routing using an [Azure Networking User Defined Route (UDR)](/azure/virtual-network/virtual-networks-udr-overview). A UDR will result in direct routing between your virtual network and the RDP broker for lowest latency. For more information about Azure Service Tags, see [Azure service tags overview](/azure/virtual-desktop/network-connectivity).

Changing the network routes of a Cloud PC (at the network layer or at the Cloud PC layer like VPN) might break the connection between the Cloud PC and the Azure Virtual Desktop RDP broker. If so, the end user will be disconnected from their Cloud PC until a connection be re-established.


## DNS requirements

As part of the Hybrid Azure AD Join requirements, your Cloud PCs must be able to join on-premises Active Directory. That requires that the Cloud PCs be able to resolve DNS records for your on-premises AD environment.

Configure your Azure Virtual Network where the Cloud PCs are provisioned as follows:

1. Make sure that your Azure Virtual Network has network connectivity to DNS servers that can resolve your Active Directory domain.
2. From the Azure Virtual Network's Settings, select DNS Servers and then choose Custom.
3. Enter the IP address of DNS servers that environment that can resolve your AD DS domain.

>[!TIP]
>Adding at least two DNS servers, as you would with a physical PC, helps mitigate the risk of a single point of failure in name resolution.

For more information, see [configuring Azure Virtual Networks settings](/azure/virtual-network/manage-virtual-network#change-dns-servers).

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

The network quality is important per scenario. Make sure that you have the proper bandwidth available for the quality that you want to offer.

Full HD (1920x1080p) isn’t a supported resolution for Microsoft Teams on Cloud PCs.

| Bandwidth (up/down) | Scenarios |
| --- | --- |
| 30 kbps | Peer-to-peer audio calling. |
| 130 kbps | Peer-to-peer audio calling and screen sharing. |
| 500 kbps | Peer-to-peer quality video calling 360p at 30 fps. |
| 1.2 Mbps | Peer-to-peer HD quality video calling with resolution of HD 720p at 30 fps. |
| 500kbps/1Mbps | Group Video calling. |

## Traffic interception technologies

Some enterprise customers use traffic interception, SSL decryption, deep packet inspection, and other similar technologies for security teams to monitor network traffic. Cloud PC provisioning may need direct access to the virtual machine. These traffic interception technologies can cause issues with running Azure network connection checks or Cloud PC provisioning. Make sure no network interception is enforced for Cloud PCs provisioned within the Windows 365 service.

## Bandwidth

Windows 365 uses the Azure network infrastructure. An Azure subscription is required when a virtual network is selected while deploying Windows 365 Enterprise. Bandwidth charges for Cloud PC usage include:

- Network traffic into a Cloud PC is free.
- Outbound (egress) traffic incurs charges against the Azure subscription for the virtual network.
- Office data (like email and OneDrive for Business file sync) incurs egress charges if the Cloud PC and a user’s data reside in different regions.
- RDP networking traffic always incurs egress charges.

If you bring your own network, see [Bandwidth pricing]( https://azure.microsoft.com/pricing/details/bandwidth/).

If you use a Microsoft-hosted network: [!INCLUDE [Outbound data rates](../includes/outbound-data-rates.md)]

<!-- ########################## -->
## Next steps

[Learn about Cloud PC role-based access control](role-based-access.md).
