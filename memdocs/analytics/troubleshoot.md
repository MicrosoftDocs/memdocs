---
title: Troubleshooting Endpoint analytics
titleSuffix: Microsoft Endpoint Manager
description: Instructions for troubleshooting Endpoint analytics.
ms.date: 10/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: troubleshooting
author: smritib17
ms.author: smbhardwaj
manager: dougeby
ms.localizationpriority: high
---


# <a name="bkmk_tshoot"></a> Troubleshooting Endpoint analytics

The following sections can be used to help in troubleshooting issues you may come across.

## <a name="bkmk_known"></a> Known issues

### Custom client settings may incorrectly indicate Endpoint analytics data collection is enabled

When you enable Endpoint analytics data upload in Configuration Manager, data collection is automatically enabled in your hierarchy's default client settings. Afterwards, any pre-existing custom [client settings](../configmgr/core/clients/deploy/about-client-settings.md#computer-agent) that include the **Computer Agent** group of settings may appear to have the **Enable Endpoint analytics data collection** set to **Yes** in the Configuration Manager console, but this setting may not have been deployed to targeted devices.

**Impacted devices:**
This issue impacts custom client settings objects that include the **Computer Agent** group of settings and were created and deployed prior to onboarding to Endpoint analytics. If you view Resultant Client Settings for devices targeted by such a custom client setting, you may find that Endpoint analytics data collection is not enabled.

**Mitigation:**
To properly configure devices governed by custom client settings for Endpoint analytics, manually set the **Enable Endpoint analytics data collection** setting to **No** and select **OK** to close the settings. Then, reopen the custom client settings and change the **Enable Endpoint analytics data collection** setting back to **Yes** and select **OK**. This change will force the custom client settings to update on targeted devices.

### <a name="bkmk_2016281112"></a> Error code -2016281112 (Remediation failed)

Customers may see profile assignment errors, where affected devices show an error code of `-2016281112 (Remediation failed)` if they can't correctly be assigned the [Intune data collection](settings.md#bkmk_profile) policy. Startup performance insights are only available for devices running Windows 10 version 1903 or later Enterprise, Education, or Pro. Long-term servicing channel (LTSC) isn't supported.
  - Windows 10 Pro versions 1903 and 1909 require [KB4577062](https://support.microsoft.com/help/4577062/windows-10-update-kb4577062). <!--8392089, 8389021-->
  - Windows 10 Pro versions 2004 and 20H2 require [KB4577063](https://support.microsoft.com/help/4577063/windows-10-update-kb4577063).<!--8392089, 8389021-->

### Hardware inventory may fail to process
<!--7535675-->
Hardware inventory for devices may fail to process after enabling endpoint analytics. Errors similar to the one below may be seen in the Dataldr.log file:

```text
Begin transaction: Machine=<machine>
*** [23000][2627][Microsoft][SQL Server Native Client 11.0][SQL Server]Violation of PRIMARY KEY constraint 'BROWSER_USAGE_HIST_PK'. Cannot insert duplicate key in object 'dbo.BROWSER_USAGE_HIST'. The duplicate key value is (XXXX, Y). : dbo.dBROWSER_USAGE_DATA
ERROR - SQL Error in
ERROR - is NOT retyrable.
Rollback transaction: XXXX
```

**Mitigation:** To work around this issue, disable the collection of the [Browser Usage (SMS_BrowerUsage)](../configmgr/apps/deploy-use/deploy-edge.md#prerequisites-for-the-dashboard) hardware inventory class. This class isn't currently used by Endpoint analytics and isn't transmitted to Microsoft.

### Script requirements for Remediations

If the option **Enforce script signature check** is enabled in the [Settings](remediations.md#bkmk_prs_deploy) page of creating a script package, then make sure that the scripts are encoded in UTF-8 not UTF-8 BOM.

## <a name="bkmk_enrollment_tshooter"></a> Troubleshooting device enrollment and startup performance

If the overview page shows a startup performance score of zero with a banner showing it's waiting for data, or if the startup performance's device performance tab shows fewer devices than you expect, there are some steps you can take to troubleshoot the issue.

First, ensure devices meet the prerequisites:
- [Prerequisites for Intune managed devices](enroll-intune.md#bkmk_prereq)
- [Prerequisites for Configuration Manager managed devices](enroll-configmgr.md#bkmk_prereq)
- [Prerequisites for Remediations](remediations.md#bkmk_prereq)

For Intune or co-managed devices configured with the Intune data collection policy:
1. Make sure you have the [Intune data collection](settings.md#bkmk_profile) policy is targeting all devices you want to see performance data. Look at the assignment tab to make sure it's assigned to the expected set of devices. 
1. Look for devices that haven't been successfully configured for data collection. You can also see this information in the profiles overview page.  
   - There's a known issue where customers may see profile assignment errors, where affected devices show an error code of `-2016281112 (Remediation failed)`. For more information, see the [Error code -2016281112](#bkmk_2016281112) section.
1. Devices that have been successfully configured for data collection must be restarted after data collection has been enabled, and you must then wait up to 25 hours after for the device to show up in the device performance tab. See [Data flow](data-collection.md#bkmk_flow)
1. If your device has been successfully configured for data collection, has later restarted, and after 25 hours you're still not seeing it, then the device may not be able communicate with the required endpoints. See [Proxy configuration](#bkmk_endpoints).

For Configuration Manager-managed devices:
1. Ensure all devices you want to see performance data are [enrolled](enroll-configmgr.md#bkmk_cm_enroll).
1. Check if the data upload from Configuration Manager to the Gateway Service was successful by looking at the error messages on the **UXAnalyticsUploadWorker.log** file on the site system hosting Service Connection Point role.
1. Check if an admin has custom overrides for client settings.  In the Configuration Manager console, go to the **Devices** workspace, find the target devices, and in the **Client settings** group, select the **Resultant client settings**. If endpoint analytics is disabled, there's an overriding client setting. Find the overriding client settings and enable endpoint analytics on it.  
1. Check if missing client devices are sending data to the site server by reviewing the **SensorEndpoint.log** file located in `C:\Windows\CCM\Logs\` on client devices. Look for *Message sent* messages.
1. Check and resolve any errors occurring during processing of the boot events by reviewing the **SensorManagedProvider.log** file located in `C:\Windows\CCM\Logs\` on client devices.
1. Client devices require a restart to fully enable all analytics. <!--7698085-->

## <a name="bkmk_endpoints"></a> Proxy configuration

If your environment uses a proxy server, configure your proxy server to allow the following endpoints:

> [!Important]  
> For privacy and data integrity, Windows checks for a Microsoft SSL certificate (certificate pinning) when communicating with the required functional data sharing endpoints. SSL interception and inspection aren't possible. To use Endpoint analytics, exclude these endpoints from SSL inspection.<!-- BUG 4647542 -->

[!INCLUDE [Internet endpoints for Endpoint analytics](../configmgr/core/plan-design/network/includes/internet-endpoints-endpoint-analytics.md)]

### Proxy server authentication

If your organization uses proxy server authentication for internet access, make sure that it doesn't block the data because of authentication. If your proxy doesn't allow devices to send this data, they won't show in Desktop Analytics.

### Bypass (recommended)

Configure your proxy servers to not require proxy authentication for traffic to the data sharing endpoints. This option is the most comprehensive solution. It works for all versions of Windows 10 or later.  

### User proxy authentication

Configure devices to use the signed-in user's context for proxy authentication. This method requires the following configurations:

- Devices have the current quality update for a supported version of Windows

- Configure user-level proxy (WinINET proxy) in **Proxy settings** in the Network & Internet group of Windows Settings. You can also use the legacy Internet Options control panel.

- Make sure that the users have proxy permission to reach the data sharing endpoints. This option requires that the devices have console users with proxy permissions, so you can't use this method with headless devices.

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

- Configure proxy servers to allow the computer accounts in Active Directory to access the data endpoints. This configuration requires proxy servers to support Windows-Integrated Authentication.  

## <a name="bkmk_faq"></a> Frequently asked questions

### If my devices are co-managed, should I enroll them via Intune, Configuration Manager, or both?

We recommend using Intune to enroll eligible co-managed devices. Devices that do not meet the device requirements for Intune enrollment (such as Windows Home devices or devices running older versions of Windows) can be enrolled via Configuration Manager. Deduplication logic in our back end prevents devices enrolled via both Intune and Configuration Manager from appearing multiple times in the Endpoint analytics portal.

### Will my Endpoint analytics data migrate if I move my Intune tenant to a different tenant location?

If you migrate your Intune tenant to a different location, all data in your Endpoint analytics solution at the time of the migration will be lost. Because endpoints report into Endpoint analytics continuously, all events that occur post-migration automatically upload into your new tenant location and reports begin to repopulate, assuming devices remain properly enrolled.

### Why are the scripts exiting with a code of 1?

The scripts exit with a code of 1 to signal to Intune that remediation should occur. In this case, exiting a detection script with 1 means it's true that remediation is needed. Many script packages that run solely in CM may show compliant, but exit with a code of 1. For these scripts, exiting with a code of 1 isn't something alarming but you may want to verify the device remediates properly.

### Why did the Update Stale Group Policies script return with error 0x87D00321?

0x87D00321 is a script execution timeout error. This error typically occurs with machines that are connected remotely. A potential mitigation might be to only deploy to a dynamic collection of machines that have internal network connectivity.

### What is the output size limit for remediation scripts?

The maximum allowed output size limit for Remediation scripts is 2048 characters.

## Next steps

Use [Remediations](remediations.md) to help fix common support issues before end-users notice issues.
