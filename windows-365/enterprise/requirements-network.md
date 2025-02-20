---
# required metadata
title: Network requirements for Windows 365
titleSuffix:
description: Learn about the network requirements for using Windows 365.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/31/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chbrinkh
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Network requirements

Windows 365 is a cloud-based service that lets users connect through the internet from any device, from any place, to a Windows Desktop running in Azure. To support these internet connections, you must follow the networking requirements listed in this article.

Each customer has its specific requirements based on the workload they use to calculate the network requirements of their Cloud PC environment.

>[!Note]
>This article only applies if you plan on provisioning Cloud PCs on your own Azure virtual network, as opposed to a Microsoft-hosted network.

## General network requirements

### [Windows 365 Enterprise](#tab/enterprise)

To use your own network and provision Microsoft Entra joined Cloud PCs, you must meet the following requirements:

- Azure virtual network: You must have a virtual network (vNET) in your Azure subscription in the same region as where the Windows 365 desktops are created.
- Network bandwidth: See [Azure’s Network guidelines](/windows-server/remote/remote-desktop-services/network-guidance).
- A subnet within the vNet and available IP address space.

To use your own network and provision Microsoft Entra hybrid joined Cloud PCs, you must meet the above requirements, and the following requirements:

- The Azure virtual network must be able to resolve DNS entries for your Active Directory Domain Services (AD DS) environment. To support this resolution, define your AD DS DNS servers as the DNS servers for the virtual network.
- The Azure vNet must have network access to an enterprise domain controller, either in Azure or on-premises.

### [Windows 365 Government](#tab/government)

All of the Windows 365 Enterprise **General network requirements** apply to [Windows 365 Government](introduction-windows-365-government.md) with the following additions:

<a name='azure-active-directory-joined-cloud-pcs'></a>

#### Microsoft Entra joined Cloud PCs

To use your own network and provision Microsoft Entra joined Cloud PCs, you must meet the following requirements:

- The customer must have a subscription in the Azure Government environment.
- Azure virtual network: You must have a virtual network (vNET) in your Azure Government subscription in the same region as where the Windows 365 Cloud PCs are created. For Government Community Cloud (GCC) and Government Community Cloud High (GCCH), this network is a US Gov region.
- Network bandwidth: See [Azure’s Network guidelines](/windows-server/remote/remote-desktop-services/network-guidance).
- A subnet within the vNet and available IP address space.

<a name='hybrid-azure-ad-joined-cloud-pcs'></a>

#### Microsoft Entra hybrid joined Cloud PCs

To use your own network and provision Microsoft Entra hybrid joined Cloud PCs, you must meet the above requirements, and the following requirements:

- The customer must have a subscription in the Azure Government environment.
- The Azure virtual network must be able to resolve DNS entries for your Active Directory Domain Services (AD DS) environment. To support this resolution, define your AD DS DNS servers as the DNS servers for the virtual network.
- The Azure vNet must have network access to an enterprise domain controller, either in Azure or on-premises.

---

## Allow network connectivity

### [Windows 365 Enterprise](#tab/ent)

You must allow traffic in your network configuration to the following service URLs and ports to support provisioning and management of Cloud PCs and for remote connectivity with Cloud PCs. Although most of the configuration is for the Cloud PC network, end user connectivity occurs from a physical device. Therefore, you must also follow the connectivity guidelines on the physical device network.

| Device or service | Network connectivity required URLs and ports | Notes |
| --- | --- | --- |
| Physical device | [Link](/azure/virtual-desktop/safe-url-list?tabs=azure#remote-desktop-clients) | For Remote Desktop client connectivity and updates. |
| Microsoft Intune service | [Link](/mem/intune-service/fundamentals/intune-endpoints) | For Intune cloud services like device management, application delivery, and endpoint analytics. |
| Azure Virtual Desktop session host virtual machine | [Link](/azure/virtual-desktop/safe-url-list?tabs=azure#session-host-virtual-machines) | For remote connectivity between Cloud PCs and the backend Azure Virtual Desktop service. |
| Windows 365 service | [Link](#windows-365-service) | For provisioning and health checks. |

#### Windows 365 service

The following URLs and ports are required for the provisioning of Cloud PCs and the Azure Network Connection (ANC) health checks:

- \*.infra.windows365.microsoft.com
- *.cmdagent.trafficmanager.net
- Registration endpoints
  - login.microsoftonline.com
  - login.live.com
  - enterpriseregistration.windows.net
  - global.azure-devices-provisioning.net (443 & 5671 outbound)
  - hm-iot-in-prod-prap01.azure-devices.net (443 & 5671 outbound)
  - hm-iot-in-prod-prau01.azure-devices.net (443 & 5671 outbound)
  - hm-iot-in-prod-preu01.azure-devices.net (443 & 5671 outbound)
  - hm-iot-in-prod-prna01.azure-devices.net (443 & 5671 outbound)
  - hm-iot-in-prod-prna02.azure-devices.net (443 & 5671 outbound)
  - hm-iot-in-2-prod-preu01.azure-devices.net (443 & 5671 outbound)
  - hm-iot-in-2-prod-prna01.azure-devices.net (443 & 5671 outbound)
  - hm-iot-in-3-prod-preu01.azure-devices.net (443 & 5671 outbound)
  - hm-iot-in-3-prod-prna01.azure-devices.net (443 & 5671 outbound)
  - hm-iot-in-4-prod-prna01.azure-devices.net (443 & 5671 outbound)

All endpoints connect over port 443 unless otherwise specified.

##### Port 3389

Port 3389 is disabled by default for all newly provisioned Cloud PCs. Microsoft recommends that you keep port 3389 closed. However, if you need port 3389 to be open for any reprovisioned or newly provisioned Cloud PCs using the Azure Network Connection (ANC) deployment option, you can review the following options:

- [Windows 365 Security Baselines](deploy-security-baselines.md). Customers can use the Windows 365 Security Baselines to effectively manage port 3389 for Windows 365 Cloud PCs. These baselines provide comprehensive tools and configurations designed to enhance security measures while allowing necessary access. By adjusting Firewall Settings and setting the **Default Inbound Action for Public Profile** to *Allow*, organizations can make sure that port 3389 is appropriately configured to meet operational needs. Review and customize these settings according to your specific organizational requirements.
- [Create a custom Firewall rule in Microsoft Intune](/mem/intune-service/protect/endpoint-security-firewall-policy). Customers can use custom Firewall rules in Microsoft Intune to configure port 3389 for Windows 365 Cloud PCs. This option involves creating a custom rule within Intune's security policies tailored to allow inbound traffic on port 3389, which is used for access to Cloud PCs. By defining the rule parameters such as port number, protocol (TCP), and restricting specific IP addresses or networks, you can make sure that access to port 3389 is tightly controlled and limited to authorized entities only.

These options aren't applicable for customers using a Microsoft-hosted network.

### [Windows 365 Government](#tab/gov)

You must allow traffic in your Azure network configuration to:

- The service URLs and ports listed in this section.
- The endpoints for Microsoft Intune and Azure Virtual Desktop.

All endpoints connect over port 443 unless specified otherwise.

- GCC: [Network endpoints for Microsoft Intune](/mem/intune-service/fundamentals/intune-endpoints).
- GCC: [Azure Virtual Desktop required URL list](/azure/virtual-desktop/safe-url-list).
- GCCH: [Microsoft Intune network endpoints for US government deployments](/mem/intune-service/fundamentals/intune-us-government-endpoints).
- GCCH: [Required URLs for Azure Virtual Desktop for US government deployments](/azure/virtual-desktop/safe-url-list?tabs=azure-for-us-government).

#### Cloud PC required URLs

| Address:Port | Required for |
| --- | --- | --- |
| *.infra.windows365.microsoft.us | GCC, GCCH |
| *.cmdagent.usgovtrafficmanager.net | GCC, GCCH |

#### Intune-dependent URLs

| Address:Port | Required for |
| --- | --- | --- |
| portal.manage.microsoft.us:443 | GCCH |
|m.manage.microsoft.us:443 | GCCH |
| mam.manage.microsoft.us:443 | GCCH |
| wip.mam.manage.microsoft.us:443 | GCCH |
| Fef.FXPASU01.manage.microsoft.us:443 | GCCH |
| portal.manage.microsoft.com:443 | GCC |
| m.manage.microsoft.com:443 | GCC |
| fef.msuc03.manage.microsoft.com:443 | GCC |
| mam.manage.microsoft.com:443 | GCC |
| wip.mam.manage.microsoft.com:443 | GCC |

<a name='azure-active-directory-dependent-urls'></a>

#### Microsoft Entra ID-dependent URLs

| Address:Port | Required for |
| --- | --- |
| login.microsoftonline.us | GCCH |
| login.live.com:443 | GCCH, GCC |
| login.microsoftonline.com:443 | GCC |
| global.azure-devices-provisioning.us (port 443 and 5671) | GCC, GCCH |
| hm-iot-in-ghp-ghp01.azure-devices.us (port 443 and 5671) | GCCH |
| hm-iot-in-gcp-gcp01.azure-devices.us (port 443 and 5671) | GCC |
| hm-iot-in-gcb-gcb01.azure-devices.us (port 443 and 5671) |GCC |
| hm-iot-in-ghb-ghb01.azure-devices.us (port 443 and 5671) |GCCH |
| enterpriseregistration.windows.net | GCCH |
| enterpriseregistration.microsoftonline.us | GCCH |

#### Azure Virtual Device-dependent URLs

| Address:Port | Required for |
| --- | --- | --- |
| rdweb.wvd.azure.us:443 | GCCH |
| rdbroker.wvd.azure.us:443 | GCCH |
| rdweb.wvd.microsoft.com:443 | GCC |
| rdbroker.wvd.microsoft.com:443 | GCC |

#### Localization package

| Address:Port | Required for |
| --- | --- | --- |
| download.microsoft.com:443 | GCCH, GCC |
| software-download.microsoft.com:443 | GCCH, GCC |

---

### Use FQDN tags for endpoints through Azure Firewall

Windows 365 fully qualified domain name (FQDN) tags make it easier to grant access to Windows 365 required service endpoints through an Azure firewall. For more information, see [Use Azure Firewall to manage and secure Windows 365 environments](azure-firewall-windows-365.md).

### Remote Desktop Protocol (RDP) broker service endpoints

Direct connectivity to Azure Virtual Desktop RDP broker service endpoints is critical for remoting performance to a Cloud PC. These endpoints affect both connectivity and latency. To align with the [Microsoft 365 network connectivity principles](/microsoft-365/enterprise/microsoft-365-network-connectivity-principles#new-office-365-endpoint-categories), you should categorize these endpoints as **Optimize** endpoints. We recommend that you use a direct path from your Azure virtual network to those endpoints.

To make it easier to configure network security controls, use Azure Virtual Desktop service tags to identity those endpoints for direct routing using an [Azure Networking User Defined Route (UDR)](/azure/virtual-network/virtual-networks-udr-overview). A UDR results in direct routing between your virtual network and the RDP broker for lowest latency. For more information about Azure Service Tags, see [Azure service tags overview](/azure/virtual-desktop/network-connectivity).

Changing the network routes of a Cloud PC (at the network layer or at the Cloud PC layer like VPN) might break the connection between the Cloud PC and the Azure Virtual Desktop RDP broker. If so, the end user is disconnected from their Cloud PC until a connection be re-established.

## DNS requirements

As part of the Microsoft Entra hybrid join requirements, your Cloud PCs must be able to join on-premises Active Directory. That requires that the Cloud PCs be able to resolve DNS records for your on-premises AD environment.

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
| Idle | 0.3 Kbps | 0.3 Kbps | User paused their work and there are no active screen updates. |
| Microsoft Word | 100-150 Kbps | 200-300 Kbps | User is actively working with Microsoft Word: typing, pasting graphics, and switching between documents. |
| Microsoft Excel | 150-200 Kbps | 400-500 Kbps | User is actively working with Microsoft Excel: multiple cells with formulas and charts are updated simultaneously |
| Microsoft PowerPoint | 4-4.5 Mbps | 1.6-1.8 Mbps | User is actively working with Microsoft PowerPoint: typing, pasting, modifying rich graphics, and using slide transition effects. |
| Web Browsing | 6-6.5 Mbps | 0.9-1 Mbps | User is actively working with a graphically rich website that contains multiple static and animated images. User scrolls the pages both horizontally and vertically |
| Image Gallery | 3.3-3.6 Mbps | 0.7-0.8 Mbps | User is actively working with the image gallery application: browsing, zooming, resizing, and rotating images |
| Video playback | 8.5-9.5 Mbps | 2.5-2.8 Mbps | User is watching a 30 FPS video that consumes 1/2 of the screen. |
| Fullscreen Video playback | 7.5-8.5 Mbps | 2.5-3.1 Mbps | User is watching a 30 FPS video maximized to a full screen. |

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

For more information on Microsoft Teams networking requirements, see [Networking considerations](/MicrosoftTeams/vdi-2#networking-considerations).

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
