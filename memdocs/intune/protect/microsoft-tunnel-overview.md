---
title: Learn about the Microsoft Tunnel VPN solution for Microsoft Intune - Azure | Microsoft Docs
description: Learn about the Microsoft Tunnel Gateway, a VPN server for Intune that runs on Linux. With the Microsoft Tunnel, cloud-based devices you manage with Intune can reach your on-premises infrastructure. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/01/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Microsoft Tunnel for Microsoft Intune

Microsoft Tunnel is a VPN gateway solution for Microsoft Intune that runs in a Docker container on Linux and allows access to on-premises resources from iOS/iPadOS and Android Enterprise devices using modern authentication and Conditional Access.

This article introduces the tunnel, how it works, and its architecture.

If your ready to deploy the Microsoft Tunnel, see [Prerequisites for the Microsoft Tunnel](microsoft-tunnel-prerequisites.md), and then Configure the Microsoft Tunnel

## Overview of Microsoft Tunnel

Microsoft Tunnel Gateway installs to a Docker container that runs on a Linux server. The Linux server can be a physical box in your on-premises environment or a virtual machine that runs on-premises or in the cloud. You'll deploy the Microsoft tunnel app and Intune VPN profiles to your iOS and Android devices to enable them to use the tunnel to connect to corporate resources. When the tunnel is hosted in the cloud, you’ll need to use a solution like Azure ExpressRoute to extend your on-premises network to the cloud.

Through the Microsoft Endpoint Manager admin center, you’ll:

- Download the Microsoft Tunnel installation script that you’ll run on the Linux servers.
- Configure aspects of Microsoft Tunnel Gateway like IP addresses, DNS servers, and ports.
- Deploy VPN profiles to devices to direct them to use the tunnel.
- Deploy the Microsoft Tunnel apps to your devices.

Through the Microsoft Tunnel app, iOS/iPadOS and Android Enterprise devices:

- Use Azure Active Directory (Azure AD) to authenticate to the tunnel.
- Are evaluated against your Conditional Access policies. If the device isn’t compliant, then it won’t have access to your VPN server or your on-premises network.

To connect to the tunnel, devices use the Microsoft Tunnel standalone app, which is available from the iOS/iPadOS or Android app stores.

You can install multiple Linux servers to support Microsoft Tunnel, and combine servers into logical groups called *Sites*. Each server can join a single Site. When you configure a Site, you’re defining a connection point for devices to use when they access the tunnel. Sites require a *Server configuration* that you’ll define and assign to the Site. The Server configuration is applied to each server you add to that Site, simplifying the configuration of more servers.

To direct devices to use the tunnel, you create and deploy a VPN policy for Microsoft Tunnel. This policy is a device configuration VPN profile that uses the Microsoft Tunnel standalone client for its connection type.  

  > [!Important]
  > In preparation for the [public preview of Tunnel client functionality in the Microsoft Defender for Endpoint app](https://aka.ms/defendertunnel), the VPN profile connection type for the Microsoft Tunnel client app has been renamed to **Microsoft Tunnel (standalone client)**. At this time, you should use the **Microsoft Tunnel (standalone client)** connection type, not the **Microsoft Tunnel** connection type.   

Features of the VPN profiles for the tunnel include:

- A friendly name for the VPN connection that your end users will see.
- The site that the VPN client connects to.
- Per-app VPN configurations that define which apps the VPN profile is used for, and if it's always-on or not. When always-on, the VPN will automatically connect and is used only for the apps you define. If no apps are defined, the always-on connection provides tunnel access for all network traffic from the device.
- Manual connections to the tunnel when a user launches the VPN and selects *Connect*.
- On-demand VPN rules that allow use of the VPN when conditions are met for specific FQDNs or IP addresses. (iOS/iPadOS)
- Proxy support (iOS/iPadOS, Android 10+)

Server configurations include:

- IP address range – The IP addresses that are assigned to devices that connect to a Microsoft Tunnel.
- DNS servers – The DNS server devices should use when they connect to the server.
- DNS suffix search.
- Split tunneling rules – Up to 500 rules shared across include and exclude routes. For example, if you create 300 include rules, you can then have up to 200 exclude rules.
- Port – The port that Microsoft Tunnel Gateway listens on.

Site configuration includes:

- A public IP address or FQDN, which is the connection point for devices that use the tunnel. This address can be for an individual server or the IP or FQDN of a load-balancing server.
- The Server configuration that is applied to each server in the Site.

You assign a server to a Site at the time you install the tunnel software on the Linux server. The installation uses a script that you can download from within the admin center. After starting the script, you’ll be prompted to configure its operation for your environment, which includes specifying the Site the server will join.

To use the Microsoft Tunnel, devices will need to install the Microsoft Tunnel app. You get the app from the iOS/iPadOS or Android app stores and deploy it to users.

## Architecture

The Microsoft Tunnel Gateway runs in Docker containers that run on Linux servers.  

![Drawing of the Microsoft Tunnel Gateway architecture](./media/microsoft-tunnel-overview/tunnel-architecture.png)
  
**Components**:  
- **A** – Microsoft Intune.
- **B**- Azure Active Directory (AD).
- **C** – Linux server with Docker.
  - **C.1** - Microsoft Tunnel Gateway.
  - **C.2** – Management Agent.
  - **C.3** – Authentication plugin – Authorization plugin, which authenticates with Azure AD.
- **D** – Public facing IP or FQDN of the Microsoft Tunnel, which can represent a load balancer.
- **E** – Mobile Device Management (MDM) enrolled device.
- **F** – Firewall
- **G** – Internal Proxy Server (optional).
- **H** – Corporate Network.
- **I** – Public internet.

**Actions**:  
- **1** - Intune administrator configures *Server configurations* and *Sites*, Server configurations are associated with Sites.
- **2** - Intune administrator installs Microsoft Tunnel Gateway and the authentication plugin authenticates Microsoft Tunnel Gateway with Azure AD. Microsoft Tunnel Gateway server is assigned to a site.
- **3** - Management Agent communicates to Intune to retrieve your server configuration policies, and to send telemetry logs to Intune.  
- **4** - Intune administrator creates and deploys VPN profiles and the Tunnel app to devices.  
- **5** - Device authenticates to Azure AD. Conditional Access policies are evaluated.  
- **6** - With split tunnel:  
  - **6a** - Some traffic goes directly to the public internet.  
  - **6b** - Some traffic goes to your public facing IP address for the Tunnel.  
- **7** - The Tunnel routes traffic to your internal proxy (optional) and your corporate network.

**Additional details**:

- Conditional Access is done in the VPN client and based on the cloud app *Microsoft Tunnel Gateway*. Non-compliant devices won’t receive an access token from Azure AD and can't access the VPN server. For more information about using Conditional Access with Microsoft Tunnel, see [Use Conditional Access with the Microsoft Tunnel](microsoft-tunnel-conditional-access.md).

- The Management Agent is authorized against Azure AD using Azure app ID/secret keys.

- The Tunnel Gateway server uses NAT to provide addresses to VPN clients that are connecting to the corporate network.
  
## Next steps

[Prerequisites for the Microsoft Tunnel in Intune](microsoft-tunnel-prerequisites.md)
