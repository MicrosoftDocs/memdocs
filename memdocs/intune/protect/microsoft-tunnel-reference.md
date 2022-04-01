---
title: File and command reference for Microsoft Tunnel Gateway, a VPN solution for Microsoft Intune
description: Find file and command-line references for tools you use to install or manage the Microsoft Tunnel Gateway, a VPN server that runs on Linux.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/11/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
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

# Reference for Microsoft Tunnel Gateway

The information in this reference for Microsoft Tunnel Gateway is provided to support installation and maintenance of the tunnel installation in your environment.

## mst-cli command-line tool for Microsoft Tunnel Gateway

**Mst-cli** is a command-line tool for use with Microsoft Tunnel Gateway. This tool is available on the Linux server after the tunnel completes installation and is found at **/usr/sbin/mst-cli**. Some tasks you can use this tool to complete include:

- Get information about the tunnel server.
- Set or update the configuration of the tunnel server.
- Restart the tunnel server.
- Uninstall the tunnel server.

The following are common command line uses of the tool.

**Command-line interface**:  

- `mst-cli –help` - Usage: **mst-cli [command]**

  Commands:  
  - `agent` - Operate on the agent component.
  - `server` - Operate on the server component.
  - `uninstall` - Uninstall the Microsoft Tunnel.
  - `eula` - Show the EULA.
  - `import_cert` - Import or update the TLS certificate.

- `mst-cli agent –help` - Usage: **mst-cli agent [command]**

  Commands:  
  - `logs` - Show the agent logs (-h for more information).
  - `status` - Show the agent status.
  - `start` - Start the agent service.
  - `stop` - Stop the agent service.
  - `restart` - Restart the agent service.

- `mst-cli agent logs   help` - Usage: **mst-cli agent logs [flags]**

  Flags:
  - `-f, --follow` - Follow log output. The default is false.
  - `--since string` - Show logs since TIMESTAMP.
  - `--tail uint` - Output the specified number of LINES at the end of the logs.  Defaults to zero (0), which prints all lines.
  - `-t, --timestamps` - Output the timestamps in the log.

- `mst-cli agent status` - The following returns are examples of results you might see:  
  - State: running  
  - Health: healthy

- `mst-cli agent start` - Starts the agent if it's stopped.

- `mst-cli agent stop` - Stops the agent.  Must be started manually after stopped.

- `mst-cli agent restart` - Restarts the agent.

- `mst-cli server --help` - Usage: **mst-cli server [command]**

  Commands:
  - `logs` - Show the server logs. Use **-h** for more information.
  - `status` - Show the server status.
  - `start` - Start the server service.
  - `stop` - Stop the server service.
  - `restart` - Restart the server service.
  - `show` - Show various server stats. Use **-h** for more information.

- `mst-cli server logs –help` - Usage: **mst-cli server logs [flags]**

  Flags:
  - `-f, --follow` - Follow log output. The default is false.
  - `--since string` - Show logs since TIMESTAMP
  - `--tail uint` - Output the specified number of LINES at the end of the logs.  Defaults to zero (0), which prints all lines.
  - `-t, --timestamps` - Output the timestamps in the log.

- `mst-cli server status` - The following returns are examples of results you might see:

  - State: running
  - Health: healthy

- `mst-cli server start` - Starts the server if it's stopped.

- `mst-cli server stop` - Stops the server.  Must be started manually after stopped.

- `mst-cli server restart` - Restarts the server.

- `mst-cli server show`
  - `show status` - Prints the status and statistics of the server.
  - `show users` - Prints the connected users.
  - `show ip bans` - Prints the banned IP addresses.
  - `show ip ban points` - Prints all the known IP addresses that have points.
  - `show iroutes` - Prints the routes provided by users of the server.
  - `show sessions all` - Prints all the session IDs.
  - `show sessions valid` - Prints all the valid for reconnection sessions.
  - `show session [SID]` - Prints information on the specified session.
  - `show user [NAME]` - Prints information on the specified user.
  - `show id [ID]` - Prints information on the specified ID.
  - `show events` - Provides information about connecting users.
  - `show cookies all` - Alias for show sessions all.
  - `show cookies valid` - Alias for show sessions valid.

## Environment variables

Following are environment variables you might want to configure when you install the Microsoft Tunnel Gateway software on the Linux server. These variables are found in the environment file **/etc/mstunnel/env.sh**:

- **http_proxy**=[address] - The HTTP address for your proxy server.
- **https_proxy**=[address] - The HTTPs address for your proxy server. 

## Data Paths  

| Path/File                       | Description             | Permissions |
|---------------------------------|-------------------------|------------|
| /…/mstunnel                     | The root directory for all configuration.   | Owner root, Group mstunnel |
| /…/mstunnel/admin-settings.json | Contains the settings for the server install.  *This file is managed by Intune and shouldn't be edited manually*. | |
| /…/mstunnel/certs               | The directory where the TLS certificate is stored.  | Owner root, Group mstunnel |
| /…/mstunnel/private             |The directory where the Intune Agent certificate and the TLS private key are stored. | Owner root, Group mstunnel |

## Files add during server installation

**/etc/mstunnel**:

- **admin-settings.json**:
  - Contains the serialized *Server configuration* from Intune.
  - Created after the server has enrolled.

- **agent-info.json**:
  - Created when the enrollment is complete.
  - AgentId, IntuneTenantId, AADTenantId, and the agent certificate RenewalDate.
  - Updated on agent certificate renewal.

- **private/agent.p12**:
  - PFX certificate used for agent authentication to Intune.
  - Automatically renewed.

- **version-info.json**:
  - Contains version information for the various components.
  - ConfigVersion, DockerVersion, AgentImageHash, AgentCreateDate, ServerImageHash, ServerCreateDate.

- **ocserv.conf**:
  - Server configuration

- **Images_configured**

**The Docker images used to create the containers**:

- agentImageDigest
- serverImageDigest

### Example of admin-settings.json

``` JSON
{
"PolicyName": "Auto Generated Policy for rh7vm",
   "DisplayName": "rh7vm Policy",
   "Description": "This policy was auto generated for rh7vm",  
   "Network": "169.100.0.0/16",
   "DNSServers": ["168.63.129.16"],
   "DefaultDomainSuffix": "nmqjwlanybmubp4imht0k2b4qd.xx.internal.cloudapp.net",
   "RoutesInclude": ["default"],
   "RoutesExclude": [],
   "ListenPort": 443
}
```

| Admin Setting     | Description                           |
|-------------------|---------------------------------------|
| PolicyName          |The name of the settings policy. You can choose the name.       |
| DisplayName         |  The short display name. You can choose the name.              |
| Description        | The description of the policy. You can choose the description. |
| Network             | The network with mask that will be used to assign clients virtual addresses. This doesn't need to change unless you have a conflict. This setting will support 64,000 clients. |
| DNSServers          | The list of DNS servers that the client should use.  These servers can resolve the addresses of internal resources. |
| DefaultDomainSuffix | The Domain suffix that a client appends to the host name when trying to resolve resources. |
| RoutesInclude       | The list of routes that will be routed via the VPN.  The default is all routes. |
| RoutesExclude       | The list of routes that should bypass the VPN.                 |
| ListenPort          | The port that the VPN server will receive traffic on.          |

## Docker commands

The following are common commands for Docker that can be of use if you must investigate problems on a tunnel server.

> [!NOTE]
> Most Linux distributions use Docker. However, some like *Red Hat Enterprise Linux (RHEL) 8.4* do not support Docker. Instead, these distributions use Podman. See [Linxu servers](../protect/microsoft-tunnel-prerequisites.md#linux-server) in the prerequisites for more details about supported distributions and the Docker or Podman requirements of each.
>
> The references and command lines that are written for Docker can be used with Podman by replacing *docker* with *podman*.

Command-line interface:

- `docker ps –a` – See all containers.
  - *mstunnel-server* – This container runs the **ocserv** server components, and uses inbound Port 443 *(default)*, or a custom port configuration.
  - *mstunnel-agent* - This container runs the Intune connector and uses outbound Port 443.

- **To restart Docker**:  
  - `systemctl restart docker`

- **To run something in a container**:
  - `docker exec –it mstunnel-server bash`
  - `docker exec –it mstunnel-agent bash`

## Podman commands

The following are commands for Podman that can be of use if you must investigate problems on a tunnel server. For additional commands you can use with Podman, see [Docker commands](#docker-commands).

- `sudo podman images` - List all running containers.
- `sudo podman stats` - Display container CPU utilization, MEM usage, Network and Block IO.
- `sudo podman port mstunnel-server` - List the port mappings from tunnel-server to the local Linux host.

## Linux commands

The following are common Linux commands you might use with a tunnel server.

- `sudo su` – Makes you root on the box.  Use this command before running the following commands, and before you run mstunnel-setup.

- `ls` – list contents of the directory.

- `ls – l` – List contents of directory including timestamps.

- `cd` – change to another directory. For example, `cd /etc/test/stuff` changes you from the *root* directory to the *etc* subfolder > to the *test* subfolder > and then to the *stuff* folder.

- `cp <source> <destination>` - Useful for copying the certs to the right location.

- `ln –s <source> <target>` - Create a softlink.

- `curl <URL>` – Checks access to a website. For example: `curl https://microsoft.com`

- `./<filename>` -  Run a script.

### Manually load ip_tables

Use the following commands to check for, and manually load if necessary, ip_tables in the Linux server kernel. Use the sudo context:

- Validate the presence of ip_tables on the server: `lsmod |grep ip_tables`

- Create a config file that will load the ip_tables into kernel when the server boots: `echo ip_tables > /etc/modules-load.d/mstunnel_iptables.conf`

- To load ip_tables into the kernel immediately: `/sbin/modprobe ip_tables`
