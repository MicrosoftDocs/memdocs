---
title: Monitor the status of the Microsoft Tunnel VPN solution for Microsoft Intune - Azure | Microsoft Docs
description: Monitor the status of Microsoft Tunnel Gateway, a VPN server that runs on Linux. With the Microsoft Tunnel, cloud-based devices you manage with Intune can reach your on-premises infrastructure. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/22/2021
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

# Monitor Microsoft Tunnel

After installation of Microsoft Tunnel, you can view the server configuration and server health in the Microsoft Endpoint Manager admin center (endpoint.microsoft.com).  

## Use the admin center UI

Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and go to *Tenant administration* > *Microsoft Tunnel Gateway*, and select the **Health check** tab.

Select a server to view the following information about it:

- **Last check-in** – When the Tunnel Gateway server last checked in with Intune.
  - *Healthy* – The last check-in was within the last five minutes.
  - *Unhealthy* – More than five minutes have passed since the last check-in.

- **Current connections** – The number of unique connections that were active at the last server check-in.
  - *Healthy* – There were 4,990 or fewer connections
  - *Unhealthy* – There were more than 4,990 active connections

- **Throughput** – The megabits bits per second of traffic passing through the Tunnel Gateway NIC at the last server check-in.

- **CPU usage** – The average CPU use by the Tunnel Gateway server every five minutes.
  - *Healthy* - 95% or less
  - *Warning* - 96% to 99%
  - *Unhealthy* - 100% use
  

- **Memory usage** – The average memory use by the Tunnel Gateway server every 5 minutes.
  - *Healthy* - 95% or less
  - *Warning* - 96% to 99%
  - *Unhealthy* - 100% use

- **Latency** – The average amount of time it takes for IP packets to arrive and then exit the network interface.
  - *Healthy* - Less than 10 milliseconds
  - *Warning* - 10 milliseconds to 20 milliseconds
  - *Unhealthy* - More than 20 milliseconds

- **TLS certificate** - The number of days until the TLS certificate that secures traffic between clients and the Tunnel Gateway server will expire.
  - *Healthy* - More than 30 days
  - *Warning* - 30 days or less
  - *Unhealthy* - The certificate is expired

## Use mst-cli command-line tool

Use the **mst-cli** command-line tool to get information about the Microsoft Tunnel server. This file is added to the Linux server when the Microsoft Tunnel installs. The tool is located at: **/usr/sbin/mst-cli**.

For more information and command-line examples, see [mst-cli command-line tool for Microsoft Tunnel](../protect/microsoft-tunnel-reference.md#mst-cli-command-line-tool-for-microsoft-tunnel-gateway).

## View Microsoft Tunnel logs

Microsoft Tunnel logs information to the Linux server logs in the *syslog* format. To view log entries, use the **journalctl -t** command followed by one or more tags that are specific to Microsoft Tunnel entries:

- **ocserv** -  Display server logs.
- **mstunnel-agent**: Display agent logs.
- **mstunnel_monitor**: Display monitoring task logs.

For example, to view information for only the tunnel server, run `journalctl -t ocserv`.  To view information for all three, you can run `journalctl -t ocserv -t mstunnel-agent -t mstunnel_monitor`.

You can add  `-f` to the command to display an active and continuing view of the log file.   For example, to actively monitor ongoing processes for Microsoft Tunnel, run `journalctl -t mstunnel_monitor -f`.

More options for *journalctl*:

- `journalctl -h` – Display command help for *journalctl*.
- `man journalctl` – Display additional information.
- `man journalctl.conf` Display information on configuration
For more information about *journalctl*, see the documentation for the version of Linux that you use.  

## Next steps

[Reference for Microsoft Tunnel](../protect/microsoft-tunnel-reference.md)
