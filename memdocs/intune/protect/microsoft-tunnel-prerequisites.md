---
title: Identify the prerequisites to install and use the Microsoft Tunnel VPN solution for Microsoft Intune
description: Learn what is required to support use of the Microsoft Tunnel Gateway in your environment, including Linux servers, network, and firewall configurations.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/11/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ochukwunyere
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Prerequisites for the Microsoft Tunnel in Intune

Before you can install the Microsoft Tunnel VPN gateway for Microsoft Intune, you must configure prerequisites. Prerequisites include use of a Linux server that runs containers to host the Tunnel server software. You'll also need to configure your network, firewalls, and proxies to support communications for the Microsoft Tunnel.

At a high level, you’ll need the following to use the Microsoft Tunnel:

- An Azure subscription.
- An Intune subscription.
- A Linux server that runs containers. This server can be on-premises or in the cloud:
  - Podman for Red Hat Enterprise Linux (RHEL) 8.4 and later
  - Docker for all other Linux distributions
- A Transport Layer Security (TLS) certificate for the Linux server to secure connections from devices to the Tunnel Gateway server.
- Devices that run Android or iOS/iPadOS.

Prerequisites you’ll configure include preparing your network, firewalls, and proxy to support the use of the Microsoft Tunnel.

After configuring prerequisites, we recommend you then run the [readiness tool](#run-the-readiness-tool) to help validate that your environment is well configured for a successful installation.

The following sections detail the prerequisites for the Microsoft Tunnel, and provide guidance on using the readiness tool.

## Linux server

Set up a Linux based virtual machine or a physical server on which Microsoft Tunnel Gateway will install.

- **Linux distribution** - The following are supported:

  - CentOS 7.4+(CentOS 8+ isn’t supported)
  - Red Hat (RHEL) 7.4+
  - Red Hat (RHEL) 8.4
  - Red Hat (RHEL) 8.5
    > [!NOTE]
    > This version of RHEL doesn't automatically load the ip_tables module into the Linux kernel. When you use this version, plan to [manually load the ip_tables](#manually-load-ip_tables) after the server installs.
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

- **Install Docker CE or Podman**: Install Podman version 3.0 on RHEL 8.4 and later. For all other versions of RHEL or other Linux distributions, install Docker version 19.03 CE or later.
  Microsoft Tunnel requires Docker (or Podman on RHEL 8.4 and later) on the Linux server to provide support for containers. Containers provide a consistent execution environment, health monitoring and proactive remediation, and a clean upgrade experience.

  For information about installing and configuring Docker or Podman, see:

  - [Install Docker Engine on CentOS or Red Hat Enterprise Linux 7]( https://docs.docker.com/engine/install/centos/)
    > [!NOTE]
    > The preceding link directs you to the CentOS download and installation instructions. Use those same instructions for RHEL 7. The version installed on RHEL 7 by default is too old to support Microsoft Tunnel Gateway. Red Hat Enterprise Linux 8 does not support Docker. For RHEL 8.4 and later, install and use Podman instead.
  - [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
  - [Install Podman on Red Hat Enterprise Linux 8.4 and later (scroll down to RHEL8)](https://podman.io/getting-started/installation).  
    Podman is the container solution used on RHEL 8.4, and *podman* is part of a module called "container-tools". In this context, a module is a set of RPM packages that represent a component and are usually installed together. A typical module contains packages with an application, packages with the application-specific dependency libraries, packages
with documentation for the application, and packages with helper utilities. For more information, see [Introduction to modules](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/installing_managing_and_removing_user-space_components/introduction-to-modules_using-appstream) in the Red Hat documentation.

- **Transport Layer Security (TLS) certificate**: The Linux server requires a trusted TLS certificate to secure the connection between devices and the Tunnel Gateway server. You’ll add the TLS certificate, including the full trusted certificate chain, to the server during installation of the Tunnel Gateway.

  - The Subject Alternative Name (SAN) of the TLS certificate you use to secure the Tunnel Gateway endpoint must match the IP address or FQDN of the Tunnel Gateway server.

  - TLS certificate can't have an expiration date longer than two years. If the date is longer than two years, it won't be accepted on iOS devices.

  - Use of wildcards has limited support. For example, **\*.contoso.com** is supported. **cont\*.com** isn’t supported.

  - During installation of the Tunnel Gateway server, you must copy the entire trusted certificate chain to your Linux server. The installation script provides the location where you copy the certificate files and prompts you to do so.

  - If you use a TLS certificate that's not publicly trusted, you must push the entire trust chain to devices using an Intune *Trusted certificate* profile.

  - The TLS certificate can be in **PEM** or **pfx** format.

- **TLS version**: By default, connections between Microsoft Tunnel clients and servers use TLS 1.3. When TLS 1.3 isn’t available, the connection can fall back to use TLS 1.2.

## Network

- **Enable packet forwarding for IPv4**: Each Linux server that hosts the Tunnel server software must have IP forwarding for IPv4 enabled. To check on the status of IP forwarding, on the server run one of the following generic commands as *root* or *sudo*. Both commands return a value of **0** for *disabled* and a value of **1** for *enabled*:
  - `sysctl net.ipv4.ip_forward`
  - `cat /proc/sys/net/ipv4/ip_forward`

  If not enabled, you can temporarily enable IP forwarding by running one of the following generic commands as *root* or *sudo* on the server. These commands can change the IP forwarding configuration until the server restarts. After a restart, the server returns IP forwarding behavior to its previous state. For both commands, use a value of **1** to *enable* forwarding. A value of **0** will disable forwarding. The following command examples use a value of *1* to *enable* forwarding:
  - `sysctl -w net.ipv4.ip_forward=1`
  - `echo 1 > /proc/sys/net/ipv4/ip_forward`

  To make IP forwarding permanent, on each Linux server edit the **/etc/sysctl.conf** file and remove the leading hashtag (#) from *#net.ipv4.ip_forward=1* to enable packet forwarding. After your edit, the entry should appear as follows:

  ```
  # Uncomment the next line to enable packet forwarding for IPv4
  net.ipv4.ip_forward=1
  ```

  For this change to take effect, you must either reboot the server or run `sysctl -p`.

  If the expected entry isn't present in the sysctl.conf file, consult the documentation for the distribution you use for how to enable IP forwarding. Typically, you can edit **sysctl.conf** to add the missing line at the end of the file to permanently enable IP forwarding.

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

- TCP 443 – Required to access Intune services. Required by Docker or Podman to pull images.
- TCP – 80 – Required to access Intune services.

When creating the Server configuration for the tunnel, you can specify a different port than the default of 443. If you specify a different port, configure firewalls to support your configuration.

**More requirements**:

- The Tunnel shares the same requirements as [Network endpoints for Microsoft Intune](../fundamentals/intune-endpoints.md), with the addition of port TCP 22.

- Configure firewall rules to support the configurations detailed in  [Microsoft Container Registry (MCR) Client Firewall Rules Configuration](https://github.com/microsoft/containerregistry/blob/master/client-firewall-rules.md).

## Proxy

You can use a proxy server with Microsoft Tunnel. The following considerations can help you configure the Linux server and your environment for success:

### Configure an outbound proxy for Docker

- If you use an internal proxy, you might need to configure the Linux host to use your proxy server by using environment variables. To use the variables, edit the **/etc/environment** file on the Linux server, and add the following lines:

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

### Configure an outbound proxy for Podman

The following details can help you configure an internal proxy when using RHEL 8.4 and later, and Podman:

- Authenticated proxies aren't supported.

- The proxy can’t perform break and inspect because the Linux server uses TLS mutual authentication when connecting to Intune.

- Podman reads HTTP Proxy information stored in **/etc/profile.d/http_proxy.sh**. If this file doesn't exist on your server, create it. Edit **http_proxy.sh** to add the following two lines. In the following lines, *10.10.10.1:3128* is an example address:port entry. When you add these lines, replace *10.10.10.1:3128* with the values for your proxy IP *address:port*:

  `export HTTP_PROXY=http://10.10.10.1:3128`  
  `export HTTPS_PROXY=http://10.10.10.1:3128`

  If you have access to Red Hat Customer Portal, you can view the knowledge base article associated with this solution. See [Setting up HTTP Proxy variables for Podman - Red Hat Customer Portal](https://access.redhat.com/solutions/3939131).

- When you add those two lines to *http_proxy.sh* before you install Microsoft Tunnel Gateway by running the mstunnel-setup, the script will automatically configure the Tunnel Gateway proxy environment variables in **/etc/mstunnel/env.sh**.

  To configure a proxy after the Microsoft Tunnel Gateway setup has completed, do the following actions:

  1. Modify or create the file **/etc/profile.d/http_proxy.sh** and add the two lines from the previous bullet point.
  2. Edit **/etc/mstunnel/env.sh** and add the following two lines to end of the file. Like the previous lines, replace the example address:port value of *10.10.10.1:3128* with the values for your proxy IP *address:port*:

     `HTTP_PROXY=http://10.10.10.1:3128`  
     `HTTPS_PROXY=http://10.10.10.1:3128`

  3. Restart the Tunnel Gateway server: Run `mst-cli server restart`


  Be aware that RHEL uses SELinux. Because a proxy that doesn't run on a SELinux port for *http_port_t* can require additional configuration, check on the use of SELinux managed ports for http. Run the following command to view the configurations: `sudo semanage port -l | grep “http_port_t” `
  
  Example of the results of the port check command. In this example, the proxy uses 3128 and isn't listed:

  :::image type="content" source="./media/microsoft-tunnel-prerequisites/check-selinux-ports.png" alt-text="Screen shot of the port check.":::

  - If your proxy runs on one of the SELinux ports for **http_port_t**, then you can continue with the Tunnel Gateway  install process.
  - If your proxy does't run on a SELunux port for **http_port_t** as in the preceding example, you'll need to make extra configurations.

    **If your proxy port is not listed for** ***http_port_t***, check if the proxy port is used by another service. Use the *semnage* command to first check the port that your proxy uses and then later if needed, to change it. To check the port your proxy uses, run: `sudo semanage port -l | grep “your proxy port”`
  
    Example of the results of checking for a service that might use the port:

    :::image type="content" source="./media/microsoft-tunnel-prerequisites/check-service.png" alt-text="Screen shot of the service check.":::

    - In the example, the port we expect (3128) is used by *squid*, which happens to be an OSS proxy service. Squid proxy SELinux policies are part of many common distributions. Because *squid* uses port 3128 (our example port), we must modify the **http_port_t** ports and add port 3128 to be allowed via SELinux for the proxy used by Tunnel. To modify the port use, run the following command: `sudo semanage port -m -t http_port_t -p tcp “your proxy port”`

      Example of the command to modify the port:

      :::image type="content" source="./media/microsoft-tunnel-prerequisites/modify-port.png" alt-text="Screen shot of the port modification.":::

      After running the command to change the port, run the following command to check if the port is used by another service: `sudo semanage port -l | grep “your proxy port”`

      Example of the command to check the port after modifying the port:

      :::image type="content" source="./media/microsoft-tunnel-prerequisites/review-results-for-port.png" alt-text="Screen shot of checking the port after modification.":::

      In this example, port 3128 is now associated with both *http_port-t* and *squid_port_t*. That result is expected. If your proxy port isn't listed when running the *sudo semanage port -l | grep "your_proxy_port"* command, then run the command to modify the port again, but the **-m** in the *semanage* command with **-a**: `sudo semanage port -a -t http_port_t -p tcp “your proxy port”`

### Update the proxy server in use by the tunnel server

To change the proxy server configuration that is in use by the Linux host of the tunnel server, use the following procedure:

1. On the tunnel server, edit */etc/mstunnel/env.sh* and specify the new proxy server.
2. Run `mst-cli install`.

   This command rebuilds the containers with the new proxy server details. During this process, you’re asked to verify the contents of */etc/mstunnel/env.h* and to make sure that the certificate is installed. The certificate should already be present from the previous proxy server configuration.

   To confirm both and complete the configuration, enter **yes**.

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

- Azure Active Directory (Azure AD) authentication to the Tunnel using username and password.
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

Before you start a server install, we recommend you download and run the most recent version of the **mst-readiness** tool. The tool is a script that runs on your Linux server and does the following actions:

- Validates that the Azure Active Directory (Azure AD) account you use to install Microsoft Tunnel has the required roles to complete enrollment.

- Confirms that your network configuration allows Microsoft Tunnel to access the required Microsoft endpoints.

- Checks for the presence of the ip_tables module on the Linux server. This check was added to the script on February 11 2022, when support for RHEL 8.5 was added. RHEL 8.5 doesn’t load the ip_tables module by default. If they are missing after the Linux server installs, you must [manually load the ip_tables module](#manually-load-ip_tables).

> [!IMPORTANT]
> The readiness tool doesn't validate inbound ports, which is a common misconfiguration. After the readiness tool runs, review the [firewall prerequisites](#firewall) and manually validate your firewalls pass inbound traffic.

The mst-readiness tool has a dependency on **jq**, a command-line JSON processor. Before you run the readiness tool, ensure **jq** is installed. For information about how to get and install **jq**, see the documentation for the version of Linux that you use.

To use the readiness tool:

1. Get the most recent version of the readiness tool by using one of the following methods:
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

### Manually load ip_tables

While most Linux distributions include the ip_tables module, some distributions might not. For example, REHL 8.5 doesn't load the ip_tables by default.

To check for the presence of this module, run the most recent version of mst-readiness tool on the server to validate its presence. The check for ip_tables was added to the readiness tools script on February 11 2022.

If the module isn’t present, the tool will stop on the ip_tables module check. In this scenario, you can run the following commands to manually load the ip_tables module, and then validate they're now present.

**Manually load the ip_tables module**:

In the context of sudo, run the following commands on your Linux server to validate the presence of the tables, and then to manually load them if necessary:

1. Validate the presence of ip_tables on the server: `lsmod |grep ip_tables`

2. If ip_tables isn't present, run the following to load the module into the kernel immediately, without a restart:  Run `/sbin/modprobe ip_tables`

3. Rerun the validation to confirm the tables are now loaded: `lsmod |grep ip_tables`

**Configure Linux to load ip_tables at boot**:

In the context of sudo, run the following command on your Linux server to create a config file that will load the ip_tables into kernel during boot time: `echo ip_tables > /etc/modules-load.d/mstunnel_iptables.conf`

## Next steps

[Configure Microsoft Tunnel](microsoft-tunnel-configure.md)
