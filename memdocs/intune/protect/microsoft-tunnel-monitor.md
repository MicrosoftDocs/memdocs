---
title: Monitor the status of the Microsoft Tunnel VPN solution for Microsoft Intune
description: Monitor the status of Microsoft Tunnel Gateway, a VPN server that runs on Linux. With the Microsoft Tunnel, cloud-based devices you manage with Intune can reach your on-premises infrastructure. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/23/2021
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

# Monitor Microsoft Tunnel

After installation of Microsoft Tunnel, you can view the server configuration and server health in the Microsoft Endpoint Manager admin center (endpoint.microsoft.com).  

## Use the admin center UI

Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and go to **Tenant administration** > **Microsoft Tunnel Gateway** > **Health status**.

Select a server and then open the **Health check** tab to view that servers health status metrics. By default, each metric uses predefined threshold values that determine the status. The following metrics [support customization of these thresholds](#manage-health-status-thresholds):

- CPU usage
- Memory usage
- Disk space usage
- Latency

Default values for server health metrics:

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

- **Internal network accessibility** – Status from the most recent check of the internal URL. You configure the URL as part of a [Tunnel Site configuration](../protect/microsoft-tunnel-configure.md#to-create-a-site-configuration).
  - **Healthy** - The server can access the URL specified in the site properties.
  - **Unhealthy** - The server can't access the URL specified in the site properties.
  - **Unknown** - This status appears when you haven't set a URL in the site properties. This status doesn’t affect the overall status of the site.

- **Server version** - The status of the Tunnel Gateway Server software, in relation to the most recent version.
  - **Healthy** - Up to date with the most recent software version
  - **Warning** - One version behind
  - **Unhealthy** - Two or more versions behind, and out of support

  When *Server version* isn’t *Healthy*, plan to [install upgrades for Microsoft Tunnel](../protect/microsoft-tunnel-upgrade.md).

## Manage health status thresholds

You can customize the following Microsoft Tunnel health status metrics to change the thresholds each uses to report their status. Customizations are tenant-wide and apply to all Tunnel severs. The health check metrics you can customize include:

- CPU usage
- Memory usage
- Disk space usage
- Latency

**To modify a metrics threshold value**:

:::image type="content" source="./media/microsoft-tunnel-monitor/thresholds.png" alt-text="Screen capture of how to select and configure health status threaholds.":::

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Microsoft Tunnel Gateway** > **Health status**.

2. Select **Configure thresholds**.

3. On the *Configure thresholds* page, set new thresholds for each health check category that you want to customize.
   - Threshold values apply to all servers at all sites.
   - Select **Revert to default** to restore *all* thresholds back to their default values.

4. Select **Save**.

5. On the Health status pane, select **Refresh** to update the status of all servers based on the customized threshold values.

After you modify thresholds, the values on a servers *Health check* tab automatically update to reflect its status, based on the current thresholds.

:::image type="content" source="./media/microsoft-tunnel-monitor/server-health-check.png" alt-text="Screen capture of a servers Health check view.":::
## Health status trends for Tunnel servers

View health status trends Microsoft Tunnel Gateway health metrics in the form of a chart. Data for the charts is averaged over a three-hour block and as such can be delayed up to three hours.

The health status trend charts are available for the following metrics:

- Connections
- CPU usage
- Disk space usage
- Memory usage
- Average latency
- Throughput

To view trend charts:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Tenant administration** > **Microsoft Tunnel Gateway** > **Health status** > *Select a server*, and then select **Trends**

3. Use the **Metric** drop-down to select the metric chart you want to view.

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