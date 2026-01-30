---
title: Troubleshooting Endpoint Analytics
description: Troubleshoot Microsoft Intune endpoint analytics, including device enrollment issues, startup performance, and data collection problems.
ms.date: 10/09/2025
ms.topic: troubleshooting
---

# Troubleshooting endpoint analytics

The following sections can be used to help in troubleshooting issues you might come across.

## Known issues and limitations

### API operator support limitations

The following APIs support a limited set of OData query operators. If you use unsupported operators in your queries, you might receive unexpected results or errors.

|API|Unsupported operators|Supported operators|
|---|---|---|
|`UserExperienceAnalyticsDeviceStartupHistory`| - `Top`<br>- `Skip`<br>- `Count`<br>- `OrderBy`<br>- `SkipToken`<br>- `Expand`|- `Select`<br>- `Filter`|
|`UserExperienceAnalyticsDeviceStartupProcesses`| - `Top`<br>- `Skip`<br>- `Count`<br>- `SkipToken`<br>- `Expand`|- `Select`<br>- `Filter`<br>- `OrderBy`|
|`SummarizeDevicePerformanceDevices`| - `Top`<br>- `Skip`<br>- `Count`<br>- `OrderBy`<br>- `SkipToken`<br>- `Expand`|- `Select`<br>- `Expand`|

### Exported csv files display numerical values

When reporting data is exported to a `.csv` file, the exported data doesn't use the friendly names you're used to seeing in the online reports. Use the information below to map the data in the exported file into the meaning of the value:

**Application reliability report** </br>

- The `TotalAppUsageDuration` and `MeanTimeToFailure` columns in the `.csv` file are integer values with a unit of **minutes**
- A `MeanTimeToFailure` value of 2147483647 means `No crash events`

**Per device score report** </br>

- A value of `-1` or `-2` in the `EndpointAnalyticsScore`, `StartupPerformanceScore`, and `AppReliabilityScore` columns means the associated score is unavailable
- Health status: </br>

   |HealthStatus `.csv` value| Report value|
   |---|---|
   |0|Unknown|
   |1|Insufficient data|
   |2|Needs attention|
   |3|Meeting goals|

**Startup performance report** </br>

The `CoreBootTime`, `GPBootTime`, `CoreLogonTime`, `GPLogonTime`, `DesktopUsableTime`, `Median`, and `TimePerProcess` columns are integer values with a unit of **seconds**.

**Work from anywhere report** </br>

- Column name in `.csv` file: UpgradeEligibility </br>
Report column name: Windows 11 readiness status </br>

   |`.csv` value| Report value|
   |---|---|
   |0|Upgraded|
   |1|Unknown|
   |2|Not capable|
   |3|Capable|

- Column name in `.csv` file: GraphDeviceIsManaged </br> Report column name: Microsoft Entra registered

### Custom client settings might incorrectly indicate endpoint analytics data collection is enabled

When you enable endpoint analytics data upload in Configuration Manager, data collection is automatically enabled in your hierarchy's default client settings. Afterwards, any pre-existing custom [client settings](../configmgr/core/clients/deploy/about-client-settings.md#computer-agent) that include the **Computer Agent** group of settings might appear to have the **Enable Endpoint analytics data collection** set to **Yes** in the Configuration Manager console, but this setting might not have been deployed to targeted devices.

**Impacted devices:**
This issue impacts custom client settings objects that include the **Computer Agent** group of settings and were created and deployed before onboarding to endpoint analytics. If you view Resultant Client Settings for devices targeted by such a custom client setting, you might find that endpoint analytics data collection isn't enabled.

**Mitigation:**
To properly configure devices governed by custom client settings for endpoint analytics, manually set the **Enable Endpoint analytics data collection** setting to **No** and select **OK** to close the settings. Then, reopen the custom client settings and change the **Enable Endpoint analytics data collection** setting back to **Yes** and select **OK**. This change forces the custom client settings to update on targeted devices.

### Hardware inventory fails to process
<!--7535675-->
Sometimes hardware inventory for devices fails to process after enabling endpoint analytics. Errors similar to the one shown here might be seen in the Dataldr.log file:

```console
Begin transaction: Machine=<machine>
*** [23000][2627][Microsoft][SQL Server Native Client 11.0][SQL Server]Violation of PRIMARY KEY constraint 'BROWSER_USAGE_HIST_PK'. Cannot insert duplicate key in object 'dbo.BROWSER_USAGE_HIST'. The duplicate key value is (XXXX, Y). : dbo.dBROWSER_USAGE_DATA
ERROR - SQL Error in
ERROR - is NOT retryable.
Rollback transaction: XXXX
```

**Mitigation:** To work around this issue, disable the collection of the [Browser Usage (SMS_BrowerUsage)](../configmgr/apps/deploy-use/deploy-edge.md#prerequisites-for-the-dashboard) hardware inventory class. This class isn't currently used by endpoint analytics and isn't transmitted to Microsoft.

## Troubleshooting device enrollment and startup performance

If the overview page shows a startup performance score of zero with a banner showing it's waiting for data, or if the startup performance's device performance tab shows fewer devices than you expect, there are some steps you can take to troubleshoot the issue.

First, ensure devices meet the prerequisites:

- [Prerequisites for Intune managed devices](index.md?pivots=intune#prerequisites)
- [Prerequisites for Configuration Manager managed devices](index.md?pivots=cm#prerequisites)

For Intune or co-managed devices configured with the Intune data collection policy:

1. Make sure you have the [Intune data collection](configure.md) policy is targeting all devices you want to see performance data. Look at the assignment tab to make sure it's assigned to the expected set of devices.
1. Look for devices that aren't successfully configured for data collection. You can also see this information in the profiles overview page.
1. Devices that are successfully configured for data collection must be restarted after data collection is enabled, and you must then wait up to 25 hours after for the device to show up in the device performance tab. See [Data flow](data-collection.md#data-flow)
1. If your device is successfully configured for data collection, restarted, and after 25 hours you're still not seeing it, then the device might not be able communicate with the required endpoints. See [Proxy configuration](#proxy-server-authentication).

For Configuration Manager-managed devices:

1. Ensure all devices you want to see performance data are [enrolled in endpoint analytics](configure.md).
1. Check if the data upload from Configuration Manager to the Gateway Service was successful by looking at the error messages on the **UXAnalyticsUploadWorker.log** file on the site system hosting Service Connection Point role.
1. Check if an admin has custom overrides for client settings. In the Configuration Manager console, go to the **Devices** workspace, find the target devices, and in the **Client settings** group, select the **Resultant client settings**. If endpoint analytics is disabled, there's an overriding client setting. Find the overriding client settings and enable endpoint analytics on it.
1. Check if missing client devices are sending data to the site server by reviewing the **SensorEndpoint.log** file located in `C:\Windows\CCM\Logs\` on client devices. Look for *Message sent* messages.
1. Check and resolve any errors occurring during processing of the boot events by reviewing the **SensorManagedProvider.log** file located in `C:\Windows\CCM\Logs\` on client devices.
1. Client devices require a restart to fully enable all analytics. <!--7698085-->

## Proxy server authentication

If your environment uses a proxy server, configure your proxy server to allow the endpoints listed under [network and connectivity requirements](index.md?pivots=intune#prerequisites).

Ensure that the proxy server doesn't block the data because of authentication. If your proxy doesn't allow devices to send this data, they won't show in endpoint analytics.

> [!IMPORTANT]
> For privacy and data integrity, Windows checks for a Microsoft SSL certificate (certificate pinning) when communicating with the required functional data sharing endpoints. SSL interception and inspection aren't possible. To use endpoint analytics, exclude these endpoints from SSL inspection.

### Bypass (recommended)

The recommended approach is to bypass the proxy for traffic to the data sharing endpoints.

### User proxy authentication

Configure devices to use the signed-in user's context for proxy authentication. This method requires the following configurations:

- Configure user-level proxy (WinINET proxy) in **Proxy settings** in the Network & Internet group of Windows Settings. You can also use the legacy Internet Options control panel.
- Ensure that the users have proxy permission to reach the data sharing endpoints. This option requires that devices have signed-in users with proxy permissions. It isn't suitable for headless devices.

> [!IMPORTANT]
> The user proxy authentication approach is incompatible with the use of Microsoft Defender for Endpoint. This behavior is because this authentication relies on the **DisableEnterpriseAuthProxy** registry key set to `0`, while Microsoft Defender for Endpoint requires it to be set to `1`. For more information, see [Configure machine proxy and internet connectivity settings in Microsoft Defender for Endpoint](/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

### Device proxy authentication

This approach supports the following scenarios:

- Headless devices, where no user signs in, or users of the device don't have internet access
- Authenticated proxies that don't use Windows-Integrated Authentication
- If you also use Microsoft Defender for Endpoint

This approach is the most complex because it requires the following configurations:

- Make sure devices can reach the proxy server through WinHTTP in local system context. Use one of the following options to configure this behavior:
  - The command line `netsh winhttp set proxy`
  - Web proxy autodiscovery (WPAD) protocol
  - Transparent proxy
  - Configure device-wide WinINET proxy using the following group policy setting: **Make proxy settings per-machine (rather than per-user)** (ProxySettingsPerUser = `1`)
  - Routed connection, or that uses network address translation (NAT)
- Configure proxy servers to authenticate computer accounts in Active Directory, allowing them to access the data endpoints.This configuration requires proxy servers to support Windows-Integrated Authentication.

## Frequently asked questions

### If my devices are co-managed, should I enroll them via Intune, Configuration Manager, or both?

We recommend using Intune to enroll eligible co-managed devices. Devices that don't meet the device requirements for Intune enrollment (such as Windows Home devices or devices running older versions of Windows) can be enrolled via Configuration Manager. Deduplication logic in our back end prevents devices enrolled via both Intune and Configuration Manager from appearing multiple times in the endpoint analytics portal.

### Will my endpoint analytics data migrate if I move my Intune tenant to a different tenant location?

If you migrate your Intune tenant to a different location, all data in your endpoint analytics solution at the time of the migration is lost. Because endpoints report into endpoint analytics continuously, all events that occur post-migration automatically upload into your new tenant location and reports begin to repopulate, assuming devices remain properly enrolled.

### Why did the Update Stale Group Policies script return with error 0x87D00321?

0x87D00321 is a script execution timeout error. This error typically occurs with machines that are connected remotely. A potential mitigation might be to only deploy to a dynamic collection of machines that have internal network connectivity.

