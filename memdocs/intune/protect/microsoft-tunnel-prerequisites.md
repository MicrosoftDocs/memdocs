---
title: Identify the prerequisites to install and use the Microsoft Tunnel VPN solution for Microsoft Intune - Azure | Microsoft Docs
description: Learn what is required to support use of the Microsoft Tunnel Gateway in your environment, including Linux servers, network, and firewall configurations.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/28/2021
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

# Prerequisites for the Microsoft Tunnel in Intune

Before you can install the Microsoft Tunnel VPN gateway for Microsoft Intune, you must configure prerequisites. Prerequisites include use of a Linux server that runs Docker to host the Tunnel server software. You'll also need to configure your network,  firewalls, and proxies to support communications for the Microsoft Tunnel.

*Microsoft Tunnel is in public preview*.

At a high level, you’ll need the following to use the Microsoft Tunnel:

- An Azure subscription
- An Intune subscription
- Linux server that runs Docker. This server can be on-premises or in the cloud
- A Transport Layer Security (TLS) certificate for the Linux server to secure connections from devices to the Tunnel Gateway server
- Devices that run Android or iOS/iPadOS

Prerequisites you’ll configure include preparing your network, firewalls, and proxy to support the use of the Microsoft Tunnel.

After configuring prerequisites, we recommend you then run the [readiness tool](#run-the-readiness-tool) to help validate that your environment is well configured for a successful installation.

The following sections detail the prerequisites for the Microsoft Tunnel, and provide guidance on using the readiness tool.

## Linux server

Set up a Linux based virtual machine or a physical server on which Microsoft Tunnel Gateway will install.

- **Linux distribution** - The following are supported:

  - CentOS 7.4+(CentOS 8+ isn’t supported)
  - Red Hat (RHEL) 7.4+
  - Red Hat (RHEL) 8
  - Ubuntu 18.04
  - Ubuntu 20.04

- **Size the Linux server**: Use the following guidance to meet your expected use:

  |# Devices | # CPUs | Memory GB | # Servers | # Sites | Disk Space GB |
  |----------|--------|-----------|-----------|---------|---------------|
  | 1,000    | 4      | 4         | 1         | 1       | 30            |
  | 2,000    | 4      | 4         | 1         | 1       | 30            |
  | 5,000    | 8      | 8         | 2         | 1       | 30            |
  | 10,000   | 8      | 8         | 3         | 1       | 30            |
  | 20,000   | 8      | 8         | 4         | 1       | 30            |
  | 40,000   | 8      | 8         | 8         | 1       | 30            |

  Support scales linearly. While each Microsoft Tunnel supports up to 64,000 concurrent connections, individual devices can open multiple connections.

- **CPU**: 64-bit AMD/Intel processor.

- **Install Docker**:  Install Docker version 19.03 CE or later.

  Microsoft Tunnel requires Docker on the Linux server to provide support for containers. Containers provide a consistent execution environment, health monitoring and proactive remediation, and a clean upgrade experience.

  For information about installing and configuring Docker, see:

  - [Install Docker Engine on CentOS]( https://docs.docker.com/engine/install/centos/)
  - [Install Docker Engine on Red Hat Enterprise Linux 7]( https://docs.docker.com/engine/install/centos/)
    > [!NOTE]
    > The current version of Docker that’s available for download for Red Hat Enterprise Linux 7 is not supported with Microsoft Tunnel. Therefore, the preceding link directs you to the CentOS download and installation instructions. The CentOS distribution and installation instructions for Docker are supported on Red Hat Enterprise Linux 7 for Microsoft Tunnel and should be used until an updated distribution for Red Hat Enterprise Linux 7 is available.
  - [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

- **Transport Layer Security (TLS) certificate**: The Linux server requires a trusted TLS certificate to secure the connection between devices and the Tunnel Gateway server. You’ll add the TLS certificate, including the full trusted certificate chain, to the server during installation of the Tunnel Gateway.

  - The Subject Alternative Name (SAN) of the TLS certificate you use to secure the Tunnel Gateway endpoint must match the IP address or FQDN of the Tunnel Gateway server.

  - TLS certificate can't have an expiration date longer than two years. If the date is longer than two years, it won't be accepted on iOS devices.

  - Use of wildcards has limited support. For example, **\*.contoso.com** is supported. **cont\*.com** isn’t supported.

  - During installation of the Tunnel Gateway server, you must copy the entire trusted certificate chain to your Linux server. The installation script provides the location where you copy the certificate files and prompts you to do so.

  - If you use a TLS certificate that's not publicly trusted, you must push the entire trust chain to devices using an Intune *Trusted certificate* profile.

  - The TLS certificate can be in **PEM** or **pfx** format.

- **TLS version**: By default, connections between Microsoft Tunnel clients and servers use TLS 1.3. When TLS 1.3 isn’t available, the connection can fall back to use TLS 1.2.

## Network

- **Enable packet forwarding for IPv4**: On  each Linux server that hosts the Tunnel server software, edit the **/etc/sysctl.conf** file and remove the leading hashtag (#) from *#net.ipv4.ip_forward=1* to enable packet forwarding. After your edit, the entry should appear as follows:

  ```
  # Uncomment the next line to enable packet forwarding for IPv4
  net.ipv4.ip_forward=1
  ```

  For this change to take effect, you must either reboot the server or run `sysctl -p`.

- **Configure multiple NICs per server** *(Optional)*: We recommend using two Network Interface controllers (NICs) per Linux server to improve performance, though use of two is optional.

  - **NIC 1** - This NIC handles traffic from your managed devices and should be on a public network with public IP address.  This IP address is the address that you configure in the *Site configuration*. This address can represent a single server or a load balancer.

  - **NIC 2** - This NIC handles traffic to your on-premises resources and should be on your private internal network without network segmentation.

- **Ensure cloud-based Linux VMs can access your on-premises network**: If you run Linux as a VM in a cloud, ensure the server can access your on-premises network. For example, for a VM in Azure, you can use [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) or something similar to provide access. Azure ExpressRoute isn't necessary when you run the server in a VM on-premises.

- **Load balancers** *(Optional)*:  If you choose to add a load balancer, consult your vendors documentation for configuration details. Take into consideration network traffic and firewall ports specific to Intune and the Microsoft Tunnel.

## Firewall

By default, the Microsoft Tunnel and server use the following ports:

**Inbound ports**:

- TCP 443 – Required by Microsoft Tunnel.
- UDP 443 – Required by Microsoft Tunnel.
- TCP 22 – Optional. Used for SSH/SCP to the Linux server.

**Outbound ports**:

- TCP 443 – Required to access Intune services. Required by Docker to pull images.
- TCP – 80 – Required to access Intune services.

When creating the Server configuration for the tunnel, you can specify a different port than the default of 443. If you specify a different port, configure firewalls to support your configuration.

**More requirements**:

- The Tunnel shares the same requirements as [Network endpoints for Microsoft Intune](../fundamentals/intune-endpoints.md), with the addition of port TCP 22.

- Configure firewall rules to support the configurations detailed in  [Microsoft Container Registry (MCR) Client Firewall Rules Configuration](https://github.com/microsoft/containerregistry/blob/master/client-firewall-rules.md).

## Proxy

You can use a proxy server with Microsoft Tunnel. The following considerations can help you configure the Linux server and your environment for success:

- If you use an internal proxy, you might need to configure the Linux host to use your proxy server by using environment variables. To use the variables, edit the **/etc/environment** file on the Linux server, and adding the following lines:

  `http_proxy=[address]`  
  `https_proxy=[address]`

- Authenticated proxies aren't supported.

- The proxy can’t perform break and inspect because the Linux server uses TLS mutual authentication when connecting to Intune.

- Configure Docker to use the proxy to pull images. To do so, edit the **/etc/systemd/system/docker.service.d/http-proxy.conf** file on the Linux server and add the following lines:

  ```
  [Service]
  Environment="HTTP_PROXY=http://your.proxy:8080/"
  Environment="HTTPS_PROXY=https://your.proxy:8080/"
  Environment="NO_PROXY=127.0.0.1,localhost"
  ```

  > [!NOTE]  
  > Microsoft Tunnel doesn’t support Azure AD App Proxy, or similar proxy solutions.

## Platforms

Devices must be enrolled to Intune to be supported with Microsoft Tunnel. Only the following device platforms are supported:

- iOS/iPadOS
- Android Enterprise:
  - Fully Managed
  - Corporate-Owned Work Profile
  - Personally-Owned Work profile

  > [!NOTE]
  > *Android Enterprise dedicated* devices aren't supported by the Microsoft Tunnel.

The following functionality is supported by all platforms:

- Azure Active Directory (Azure AD) authentication to the Tunnel using either username and password, or certificates.
- Per-app support.
- Manual full-device tunnel through a Tunnel app, where the user launches VPN and selects *Connect*.
- Split tunneling. However, on iOS split tunneling rules are ignored when your VPN profile uses *per app VPN*.

Support for a Proxy is limited to the following platforms:

- Android 10 and later
- iOS/iPadOS

## Permissions

To manage the Microsoft Tunnel, users must have permissions that are included in the **Microsoft Tunnel Gateway** permissions group in Intune. By default, Intune Administrators and Azure AD administrators have these permissions. You can also add them to [custom roles you create](../fundamentals/create-custom-role.md) for your Intune tenant.

While configuring a role, on the **Permissions** page, expand **Microsoft Tunnel Gateway** and then select the permissions you want to grant.

:::image type="content" source="./media/microsoft-tunnel-prerequisites/microsoft-tunnel-gateway-permissions.png" alt-text="Screen shot of the tunnel gateway permissions in the Microsoft Endpoint Manager admin center.":::

The Microsoft Tunnel Gateway permissions group grants the following permissions:

- **Create** - Configure Microsoft Tunnel Gateway *Servers* and *Sites*. Server configurations include settings for IP address ranges, DNS servers, ports, and split tunneling rules. Sites are logical groupings of multiple servers that support Microsoft Tunnel.

- **Update** (modify) - Update Microsoft Tunnel Gateway server configurations and sites. Server configurations include settings for IP address ranges, DNS servers, ports, and split tunneling rules. Sites are logical groupings of multiple servers that support Microsoft Tunnel.

- **Delete** - Delete Microsoft Tunnel Gateway server configurations and sites. Server configurations include settings for IP address ranges, DNS servers, ports, and split tunneling rules. Sites are logical groupings of multiple servers that support Microsoft Tunnel.

- **Read** - View Microsoft Tunnel Gateway server configurations and sites. Server configurations include settings for IP address ranges, DNS servers, ports, and split tunneling rules. Sites are logical groupings of multiple servers that support Microsoft Tunnel.


## Run the readiness tool

Before you start a server install, we recommend you download and run the **mst-readiness** tool. The tool is a script that runs on your Linux server and does the following actions:

- Confirms that your network configuration allows Microsoft Tunnel to access the required Microsoft endpoints.  
- Validates that the Azure Active Directory (Azure AD) account you use to install Microsoft Tunnel has the required roles to complete enrollment.

> [!IMPORTANT]
> The readiness tool doesn't validate inbound ports, which is a common misconfiguration. After the readiness tool runs, review the [firewall prerequisites](#firewall) and manually validate your firewalls pass inbound traffic.

The mst-readiness tool has a dependency on **jq**, a command-line JSON processor. Before you run the readiness tool, ensure **jq** is installed. For information about how to get and install **jq**, see the documentation for the version of Linux that you use.

To use the readiness tool:

1. Get the readiness tool by using one of the following methods:
   - Download the tool directly by using a web browser.  Go to https://aka.ms/microsofttunnelready to download a file named **mst-readiness**.
   - Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Microsoft Tunnel Gateway**, select the **Servers** tab, select **Create** to open the *Create a server* pane, and then select **Download readiness tool**.  
   - Use a Linux command to get the readiness tool directly. For example, you can use **wget** or **curl** to open the link https://aka.ms/microsofttunnelready.

      For example, to use **wget** and log details to *mst-readiness* during the download, run `wget --output-document=mst-readiness https://aka.ms/microsofttunnelready`

   You can run the script from any Linux server that is on the same network as the server you plan to install, allowing network admins to run it and troubleshoot network issues independently.

2. To validate your network configuration, run the script with the following commands to first set the execute permissions on the script and then to validate the Tunnel can connect to the correct endpoints:

   - `sudo chmod +x ./mst-readiness`
   - `sudo ./mst-readiness network`

   The second command runs the following actions and reports on success or error for both:

   - Tries to connect to each Microsoft endpoint the tunnel will use.
   - Checks that the required ports are open in your firewall.

3. To validate that the account you’ll use to install Microsoft Tunnel has the required roles and permissions to complete enrollment, run the script with the following command line: `./mst-readiness account`

   The script prompts you to use a different machine with a web browser, which you use to authenticate to Azure AD and to Intune. The tool will report success or an error.

For more information about this tool, see [Reference for mst-cli](../protect/microsoft-tunnel-reference.md#mst-cli-command-line-tool-for-microsoft-tunnel-gateway) in the reference article for Microsoft Tunnel article.

## Next steps

[Configure Microsoft Tunnel](microsoft-tunnel-configure.md)
