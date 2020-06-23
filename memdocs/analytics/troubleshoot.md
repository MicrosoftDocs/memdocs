---
title: Troubleshooting Endpoint analytics
titleSuffix: Configuration Manager
description: Instructions for troubleshooting Endpoint analytics.
ms.date: 06/25/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: troubleshooting
ms.assetid: d13ec899-6033-4579-9b80-c9bf755f2f98
author: mestew
ms.author: mstewart
manager: dougeby

---


# <a name="bkmk_tshoot"></a> Troubleshooting Endpoint analytics

The sections below can be used to assist in troubleshooting issues you may come across.

## <a name="bkmk_enrollment_tshooter"></a> Troubleshooting device enrollment and startup performance

If the overview page shows a startup performance score of zero with a banner showing it's waiting for data, or if the startup performance's device performance tab shows fewer devices than you expect, there are some steps you can take to troubleshoot the issue.

First, ensure devices meet the prerequisites:
- [Prerequisites for Intune managed devices](enroll-intune.md#bkmk_prereq)
- [Prerequisites for Configuration Manager managed devices](enroll-configmgr.md#bkmk_prereq)
- [Prerequisites for Proactive remediations](proactive-remediations.md#bkmk_prereq)

For Intune or co-managed devices configured with the Intune data collection policy:
1. Make sure you have the [Intune data collection](settings.md#bkmk_profile) policy is targeting all devices you want to see performance data. Look at the assignment tab to make sure it's assigned to the expected set of devices. 
1. Look for devices that haven't been successfully configured for data collection. You can also see this information in the profiles overview page.  
   - There's a known issue where customers may see profile assignment errors, where affected devices show an error code of `-2016281112 (Remediation failed)`. We're actively investigating this issue.
1. Devices that have been successfully configured for data collection must be restarted after data collection has been enabled, and you must then wait up to 25 hours after for the device to show up in the device performance tab. See [Data flow](data-collection.md#data-flow)
1. If your device has been successfully configured for data collection, has subsequently restarted, and after 25 hours you're still not seeing it, then the device may not be able communicate with the required endpoints. See [Proxy configuration](#bkmk_endpoints).

For Configuration Manager-managed devices:
1. Ensure all devices you want to see performance data are [enrolled](enroll-configmgr.md#bkmk_cm_enroll).
1. Check if the data upload from Configuration Manager to the Gateway Service was successful by looking at the error messages on the **UXAnalyticsUploadWorker.log** file on the site server.
1. Check if an admin has custom overrides for client settings.  In the Configuration Manager console, go to the **Devices** workspace, find the target devices, and in the **Client settings** group, select the **Resultant client settings**. If endpoint analytics is disabled, there's an overriding client setting. Find the overriding client settings and enable endpoint analytics on it.  
1. Check if missing client devices are sending data to the site server by reviewing the **SensorEndpoint.log** file located in `C:\Windows\CCM\Logs\` on client devices. Look for *Message sent* messages.
1. Check and resolve any errors occurring during processing of the boot events by reviewing the **SensorManagedProvider.log** file located in `C:\Windows\CCM\Logs\` on client devices.


## <a name="bkmk_endpoints"></a> Proxy configuration

If your environment uses a proxy server, configure your proxy server to allow the following endpoints:

### Endpoints required for Configuration Manager-managed devices

Configuration Manager-managed devices send data to Intune via the connector on the Configuration Manager role and they don't need directly access to the Microsoft public cloud.

| Endpoint  | Function  |
|-----------|-----------|
| `https://graph.windows.net` | Used to automatically retrieve settings  when attaching your hierarchy to Endpoint analytics on Configuration Manager Server role. For more information, see [Configure the proxy for a site system server](../configmgr/core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Used to synch device collection and devices with Endpoint analytics on Configuration Manager Server role only. For more information, see [Configure the proxy for a site system server](../configmgr/core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### Endpoints required for Intune-managed devices

To enroll devices to Endpoint analytics, they need to send required functional data to Microsoft public cloud. Endpoint Analytics uses the Windows 10 and Windows Server Connected User Experiences and Telemetry component (DiagTrack) to collect the data from Intune-managed devices. Make sure that the **Connected User Experiences and Telemetry** service on the device is running.

| Endpoint  | Function  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Used by Intune-managed devices to send [required functional data](data-collection.md#bkmk_datacollection) to the Intune data collection endpoint. |

> [!Important]  
> For privacy and data integrity, Windows checks for a Microsoft SSL certificate (certificate pinning) when communicating with the required functional data sharing endpoints. SSL interception and inspection aren't possible. To use Endpoint analytics, exclude these endpoints from SSL inspection.<!-- BUG 4647542 -->

### Proxy server authentication

If your organization uses proxy server authentication for internet access, make sure that it doesn't block the data because of authentication. If your proxy doesn't allow devices to send this data, they won't show in Desktop Analytics.

### Bypass (recommended)

Configure your proxy servers to not require proxy authentication for traffic to the data sharing endpoints. This option is the most comprehensive solution. It works for all versions of Windows 10.  

### User proxy authentication

Configure devices to use the signed-in user's context for proxy authentication. This method requires the following configurations:

- Devices have the current quality update for a supported version of Windows

- Configure user-level proxy (WinINET proxy) in **Proxy settings** in the Network & Internet group of Windows Settings. You can also use the legacy Internet Options control panel.

- Make sure that the users have proxy permission to reach the data sharing endpoints. This option requires that the devices have console users with proxy permissions, so you can't use this method with headless devices.

> [!IMPORTANT]
> The user proxy authentication approach is incompatible with the use of Microsoft Defender Advanced Threat Protection. This behavior is because this authentication relies on the **DisableEnterpriseAuthProxy** registry key set to `0`, while Microsoft Defender ATP requires it to be set to `1`. For more information, see [Configure machine proxy and internet connectivity settings in Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

### Device proxy authentication

This approach supports the following scenarios:

- Headless devices, where no user signs in, or users of the device don't have internet access

- Authenticated proxies that don't use Windows Integrated Authentication

- If you also use Microsoft Defender Advanced Threat Protection

This approach is the most complex because it requires the following configurations:

- Make sure devices can reach the proxy server through WinHTTP in local system context. Use one of the following options to configure this behavior:

  - The command line `netsh winhttp set proxy`

  - Web proxy auto-discovery (WPAD) protocol

  - Transparent proxy

  - Configure device-wide WinINET proxy using the following group policy setting: **Make proxy settings per-machine (rather than per-user)** (ProxySettingsPerUser = `1`)

  - Routed connection, or that uses network address translation (NAT)

- Configure proxy servers to allow the computer accounts in Active Directory to access the data endpoints. This configuration requires proxy servers to support Windows Integrated Authentication.  

## <a name="bkmk_faq"></a> Frequently asked questions

### Will my Endpoint analytics data migrate if I move my Intune tenant to a different tenant location?

If you migrate your Intune tenant to a different location, all data in your Endpoint analytics solution at the time of the migration will be lost. Because endpoints report into Endpoint analytics continuously, all events that occur post-migration automatically upload into your new tenant location and reports begin to repopulate, assuming devices remain properly enrolled.

### Why are the scripts exiting with a code of 1?

The scripts exit with a code of 1 to signal to Intune that remediation should occur. In this case, exiting a detection script with 1 means it's true that remediation is needed. Many script packages that run solely in CM may show compliant, but exit with a code of 1. For these scripts, exiting with a code of 1 isn't something alarming but you may want to verify the device remediates properly.

### Why did the Update Stale Group Policies script return with error 0x87D00321?

0x87D00321 is a script execution timeout error. This error typically occurs with machines that are connected remotely. A potential mitigation might be to only deploy to a dynamic collection of machines that have internal network connectivity.

## Next steps

For more information on changes to Endpoint analytics, see [What's new](whats-new.md).
