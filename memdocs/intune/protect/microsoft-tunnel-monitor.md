---
title: Monitor the status of the Microsoft Tunnel VPN solution for Microsoft Intune
description: Monitor the status of Microsoft Tunnel Gateway, a VPN server that runs on Linux. With the Microsoft Tunnel, cloud-based devices you manage with Intune can reach your on-premises infrastructure. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/17/2022
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
ms.collection:
- tier2
- M365-identity-device-management
---

# Monitor Microsoft Tunnel

After installation of Microsoft Tunnel, you can view the server configuration and server health in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

## Use the admin center UI

Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and go to **Tenant administration** > **Microsoft Tunnel Gateway** > **Health status**.

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

:::image type="content" source="./media/microsoft-tunnel-monitor/thresholds.png" alt-text="Screen capture of how to select and configure health status thresholds.":::

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Tenant administration** > **Microsoft Tunnel Gateway** > **Health status**.

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

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Tenant administration** > **Microsoft Tunnel Gateway** > **Health status** > *Select a server*, and then select **Trends**

3. Use the **Metric** drop-down to select the metric chart you want to view.

## Use mst-cli command-line tool

Use the **mst-cli** command-line tool to get information about the Microsoft Tunnel server. This file is added to the Linux server when the Microsoft Tunnel installs. The tool is located at: **/usr/sbin/mst-cli**.

For more information and command-line examples, see [mst-cli command-line tool for Microsoft Tunnel](../protect/microsoft-tunnel-reference.md#mst-cli-command-line-tool-for-microsoft-tunnel-gateway).

## View Microsoft Tunnel logs

Microsoft Tunnel logs information to the Linux server logs in the *syslog* format. To view log entries, use the **journalctl -t** command followed by one or more tags that are specific to Microsoft Tunnel entries:

- **mstunnel-agent**: Display agent logs.
- **mstunnel_monitor**: Display monitoring task logs.
- **ocserv** -  Display server logs.
- **ocserv-access** - Display access logs.

  By default, access logging is disabled. Enabling access logs can reduce performance, depending on the number of active connections and usage patterns on the server. Logging for DNS connections increases the verbosity of the logs, which can become noisy.

  Access logs have the following format: `<Server timestamp><Server Name><ProcessID on Server><userId><deviceId><protocol><src IP and port><dst IP and port><bytes sent><bytes received><connection time in seconds>` For example:

  - *Feb 25 16:37:56 MSTunnelTest-VM ocserv-access[9528]: ACCESS_LOG,41150dc4-238x-4dwv-9q89-55e987f30c32,f5132455-ef2dd-225a-a693-afbbqed482dce,tcp,169.254.54.149:49462,10.88.0.5:80,112,60,10*

  > [!IMPORTANT]
  > In **ocserv-access**, the *deviceId* value identifies the unique installation instance of Microsoft Defender that runs on a device, and does not identify either the Intune device ID or Azure AD device ID. If Defender is uninstalled and then reinstalled on a device, a new instance for the *DeviceId** is generated.

  To enable access logging:

  1. set TRACE_SESSIONS=1 in /etc/mstunnel/env.sh
  2. set TRACE_SESSIONS=2 to include logging for DNS connections
  3. Run `mst-cli server restart` to restart the server.

  If access logs are too noisy, you can turn off DNS connection logging by setting TRACE_SESSIONS=1 and restarting the server.

- **OCSERV_TELEMETRY** - Display telemetry details for connections to Tunnel.

  Telemetry logs have the following format, with the values for *bytes_in*, *bytes_out*, and *duration* being used only for disconnect operations: `<operation><client_ip><server_ip><gateway_ip><assigned_ip><user_id><device_id><user_agent><bytes_in><bytes_out><duration>` For example:  

  - *Oct 20 19:32:15 mstunnel ocserv[4806]: OCSERV_TELEMETRY,connect,31258,73.20.85.75,172.17.0.3,169.254.0.1,169.254.107.209,3780e1fc-3ac2-4268-a1fd-dd910ca8c13c,5A683ECC-D909-4E5F-9C67-C0F595A4A70E,MobileAccess iOS 1.1.34040102*

  > [!IMPORTANT]
  > In **OCSERV_TELEMETRY**, the *deviceId* value identifies the unique installation instance of Microsoft Defender that runs on a device, and does not identify either the Intune device ID or Azure AD device ID. If Defender is uninstalled and then reinstalled on a device, a new instance for the *DeviceId** is generated.

Command line examples for *journalctl*:

- To view information for only the tunnel server, run `journalctl -t ocserv`.
- To view the telemetry log, run `journalctl -t ocserv | grep TELEMETRY`
- To view information for all log options, you can run `journalctl -t ocserv -t ocserv-access -t mstunnel-agent -t mstunnel_monitor`.
- Add `-f` to the command to display an active and continuing view of the log file. For example, to actively monitor ongoing processes for Microsoft Tunnel, run `journalctl -t mstunnel_monitor -f`.

More options for *journalctl*:

- `journalctl -h` – Display command help for *journalctl*.
- `man journalctl` – Display additional information.
- `man journalctl.conf` Display information on configuration
For more information about *journalctl*, see the documentation for the version of Linux that you use.

## Known issues

The following are known issues for Microsoft Tunnel.

### Server health

#### Clients can successfully use the Tunnel when Server health status shows as offline<!-- 14878305 -->

**Issue**: On the [Tunnel *Health status* tab](../protect/microsoft-tunnel-monitor.md), a server’s health status reports as offline indicating it's disconnected, even though users can reach the tunnel server and connect to the organization’s resources.  

**Solution**: To resolve this issue, you must reinstall Microsoft Tunnel, which re-enrolls the Tunnel server agent with Intune. To prevent this issue, install updates for the Tunnel agent and server soon after they're released. Use the Tunnel server health metrics in the Microsoft Intune admin center to monitor server health.

#### With Podman, you see “Error executing checkup” in the mstunnel_monitor log<!-- 14878316 -->

**Issue**: Podman fails to identify or see the active containers are running, and reports “Error executing checkup” in the [mstunnel_monitor log](../protect/microsoft-tunnel-monitor.md#view-microsoft-tunnel-logs) of the Tunnel server.  The following are examples of the errors: 

- Agent:  
  ```
  Error executing Checkup
  Error details
  \tscript: 561 /usr/sbin/mst-cli
  \t\tcommand: $ctr_cli exec $agent_name mstunnel checkup 2> >(FailLogger)
  \tstack:
  \t\t<> Checkup /usr/sbin/mst-cli Message: NA
  \t\t<> MonitorServices /usr/sbin/mst-cli Message: Failure starting service mstunnel-agent
  \t\t<> main /usr/sbin/mstunnel_monitor Message: NA
  ```

- Server:  
  ```
  Error executing Checkup
  Error details
  \tscript: 649 /usr/sbin/mst-cli
  \t\tcommand: $ctr_cli exec $agent_name mstunnel checkup 2> >(FailLogger)
  \tstack:
  \t\t<> Checkup /usr/sbin/mst-cli Message: NA
  \t\t<> MonitorServices /usr/sbin/mst-cli Message: Failure starting service mstunnel-server
  \t\t<> main /usr/sbin/mstunnel_monitor Message: NA
  ```

**Solution**: To resolve this issue, manually [restart the Podman containers](https://docs.podman.io/en/latest/markdown/podman-restart.1.html). Podman should then be able to identify the containers. If the problem persists, or returns, consider using ***cron*** to create a job that automatically restarts the containers when this issue is seen.

#### With Podman, you see System.DateTime errors in the mstunnel-agent log<!-- 14878334  -->

**Issue**: When you use Podman, the mstunnel-agent log might contain errors similar to the following entries:

- `Failed to parse version-info.json for version information.`
- `System.Text.Json.JsonException: The JSON value could not be converted to System.DateTime`

This issue occurs due to differences in formatting dates between Podman and Tunnel Agent. These errors don't indicate a fatal issue or prevent connectivity.  Beginning with containers released after October 2022, the formatting issues should be resolved.  

**Solution**: To resolve these issues, update the agent container (Podman or Docker) to the latest version. As new sources of these errors are discovered, we’ll continue to fix them in subsequent version updates.

### Connectivity to Tunnel

#### Devices fail to connect to the Tunnel server

**Issue**: Devices fail to connect to the server, and the Tunnel server *ocserv* log file contains an entry similar to the following entry: `main: tun.c:655: Can't open /dev/net/tun: Operation not permitted`

For guidance on viewing Tunnel logs, see [View Microsoft Tunnel logs](#view-microsoft-tunnel-logs) in this article.

**Solution**: Restart the server using `mst-cli server restart` after the Linux server reboots.

If this issue persists, consider automating the restart command by using the cron scheduling utility. See [How to use cron on Linux](https://opensource.com/article/21/7/cron-linux) at *opensource.com*.

#### Users can't connect to resources while using Microsoft Edge<!-- 13119847 -->

**Issue**: After you've [migrated from the stand-alone tunnel client app to Microsoft Defender for Endpoint](../protect/microsoft-tunnel-migrate-app.md) and are then using Microsoft Edge, users are unable to access any internal or external websites. Users might also see a message similar to: `You’re not Connected`.

**Solution**: This issue can occur when the standalone Tunnel client app remains installed while the Microsoft Defender for Endpoint app is in use. To resolve this issue, uninstall the standalone Tunnel client app. It's also possible to uninstall the standalone client app prior to installing Microsoft Defender for Endpoint, but doing so might leave your devices unable to use Microsoft Tunnel until the new Tunnel app is in place and fully configured.  

## Next steps

[Reference for Microsoft Tunnel](../protect/microsoft-tunnel-reference.md)
