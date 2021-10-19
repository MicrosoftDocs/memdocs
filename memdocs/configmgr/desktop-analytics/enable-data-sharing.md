---
title: Enable data sharing
titleSuffix: Configuration Manager
description: A reference guide for sharing diagnostics data with Desktop Analytics.
ms.date: 07/07/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.localizationpriority: medium
---

# Enable data sharing for Desktop Analytics

To [enroll devices](enroll-devices.md) to Desktop Analytics, they need to send diagnostic data to Microsoft. Configuration Manager provides an integrated experience for managing and deploying settings to clients. Use Configuration Manager to manage the diagnostic data level and help [configure proxy servers](#proxy-server-authentication). For the best experience, use Configuration Manager.

> [!IMPORTANT]
> In most circumstances, only use Configuration Manager to configure these settings. Don't also apply these settings in domain group policy objects. For more information, see [Conflict resolution](group-policy-settings.md#conflict-resolution).

## Diagnostic data levels

:::image type="content" source="media/diagnostic-data-levels.png" alt-text="Diagram of diagnostic data levels for Desktop Analytics":::

The basic functionality of Desktop Analytics works at the **Required** [diagnostic data level](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels). If you don't configure the **Optional (limited)** level in Configuration Manager, you won't get the following features of Desktop Analytics:

- App usage
- [Additional app insights](compat-assessment.md#additional-insights)
- [Deployment status data](deploy-prod.md#address-deployment-alerts)
- [Health monitoring data](health-status-monitoring.md)

Microsoft recommends that you enable the **Optional (limited)** diagnostic data level with Desktop Analytics to maximize the benefits you get from it.

- The **Optional (Limited)** setting in Configuration Manager is the same setting as **Limit Enhanced diagnostic data to the minimum required by Windows Analytics** policy available on devices running Windows 10, version 1709 and later.

- Devices running Windows 10, version 1703 and earlier, Windows 8.1, or Windows 7 don't have this policy setting. When you configure the **Optional (limited)** setting in Configuration Manager, these devices fall back to the **Required** level.

- Devices running Windows 10, version 1709 have this policy setting. However, when you configure the **Optional (limited)** setting in Configuration Manager, these devices also fall back to the **Required** level.

For more information about diagnostic data shared with Microsoft with **Optional (limited)**, see [Windows 10 enhanced diagnostic data events and fields](/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

When you configure the diagnostic data level, you set the upper boundary for the device. By default in Windows 10, version 1803 and later, users can choose to set a lower level. You can control this behavior using the group policy setting, [Configure telemetry opt-in setting user interface](group-policy-settings.md#group-policy-settings-to-customize-the-user-experience).

> [!IMPORTANT]
> Microsoft has a strong commitment to providing the tools and resources that put you in control of your privacy. As a result, while Desktop Analytics supports Windows 8.1 devices, Microsoft doesn't collect Windows diagnostic data from Windows 8.1 devices located in European countries (European Economic Area [EEA], Switzerland, and the United Kingdom).
>
> Starting in July 2021, Desktop Analytics supports the [Windows diagnostic data processor configuration](/windows/privacy/changes-to-windows-diagnostic-data-collection#new-windows-diagnostic-data-processor-configuration). For more information, see [Support for the Windows diagnostic data processor configuration](whats-new.md#support-for-the-windows-diagnostic-data-processor-configuration).

For more information, see [Desktop Analytics privacy](privacy.md).

The following articles are also good resources for better understanding Windows diagnostic data levels:

- [Windows 10 & privacy compliance: A guide for IT and compliance professionals](/windows/privacy/windows-10-and-privacy-compliance)

- [Configure Windows diagnostic data in your organization](/windows/privacy/configure-windows-diagnostic-data-in-your-organization)

> [!NOTE]
> Clients configured to send **Optional (limited)** diagnostic data will send approximately 2 MB of data to the Microsoft cloud on the initial full scan. The daily delta varies between 250-400 KB per day.
>
> The daily delta scan happens at 3:00 AM (device local time). Some events are sent at the first available time throughout the day. These times aren't configurable.
>
> For more information, see [Configure Windows diagnostic data in your organization](/windows/privacy/configure-windows-diagnostic-data-in-your-organization).  

### Support for new Windows 10 diagnostic data levels

Microsoft is increasing transparency by categorizing the diagnostic data that Windows 10 collects:

- **Basic** diagnostic data is recategorized as **Required**
- **Full** is recategorized as **Optional**

Starting in Configuration Manager current branch version 2006, the **Diagnostic Data** tab of the Desktop Analytics service in the Configuration Manager console uses these new labels. In Configuration Manager version 2002 and earlier, the settings had different names:<!-- 7363467 -->

| Version 2006 and later | Version 2002 and earlier |
|---------|---------|
| Required | Basic |
| Optional (limited) | Enhanced (Limited) |
| N/A | Enhanced |
| Optional | Full |

If you previously configured any devices at the **Enhanced** level, when you upgrade to version 2006, they'll revert to **Optional (limited)**. They'll then send less data to Microsoft. This change shouldn't affect what you see in Desktop Analytics.

In an upcoming release of Windows 10,  devices configured for **Enhanced** or **Enhanced (Limited)** diagnostic data will revert to the **Required** level. This change may affect the functionality of Desktop Analytics. Use Configuration Manager current branch version 2010, <!--6979470--> to properly configure these devices to **Optional (limited)**. If you're using another mechanism to configure these policies on devices, you may need to make changes for the upcoming new behavior. For more information, see [Changes to Windows diagnostic data collection](/windows/privacy/changes-to-windows-diagnostic-data-collection#behaviorial-changes).

You can test the behavioral changes now in Windows 10 Insider Preview build 19577 and later. After you enroll Windows Insider devices to Desktop Analytics, it may take up to 48 hours to appear on the Desktop Analytics portal or the new configurations to take effect. Use the Configuration Manager console to look for issues or configuration alerts as you [Monitor connection health](monitor-connection-health.md).

## Endpoints

To enable data sharing, configure your proxy server to allow the following internet endpoints.

> [!IMPORTANT]
> For privacy and data integrity, Windows checks for a Microsoft SSL certificate (certificate pinning) when communicating with the diagnostic data endpoints. SSL interception and inspection aren't possible. To use Desktop Analytics, exclude these endpoints from SSL inspection.<!-- BUG 4647542 -->

Starting in version 2002, if the Configuration Manager site fails to connect to required endpoints for a cloud service, it raises a critical status message ID 11488. When it can't connect to the service, the SMS_SERVICE_CONNECTOR component status changes to critical. View detailed status in the [Component Status](../core/servers/manage/use-status-system.md#monitor-the-status-system) node of the Configuration Manager console.<!-- 5566763 -->

Starting in version 2010, the service connection point validates important internet endpoints for Desktop Analytics. These checks help make sure that the cloud service is available. It also helps you troubleshoot issues by quickly determining if network connectivity is a problem. For more information, see [Validate internet access](../core/servers/deploy/configure/about-the-service-connection-point.md#validate-internet-access).<!--8565578-->

> [!NOTE]
> For more information on the Microsoft IP address ranges, see [Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602). These addresses update regularly. There's no granularity by service, any IP address in these ranges could be used.

[!INCLUDE [Internet endpoints for Desktop Analytics](../core/plan-design/network/includes/internet-endpoints-desktop-analytics.md)]

## Proxy server authentication

If your organization uses proxy server authentication for internet access, make sure that it doesn't block the diagnostic data because of authentication. If your proxy doesn't allow devices to send this data, they won't show in Desktop Analytics.

### Bypass (recommended)

Configure your proxy servers to not require proxy authentication for traffic to the diagnostic data endpoints. This option is the most comprehensive solution. It works for all versions of Windows 10.  

### User proxy authentication

Configure devices to use the signed-in user's context for proxy authentication. This method requires the following configurations:

- Devices have the current quality update for a supported version of Windows

- Configure user-level proxy (WinINET proxy) in **Proxy settings** in the Network & Internet group of Windows Settings. You can also use the legacy Internet Options control panel.

- Make sure that the users have proxy permission to reach the diagnostic data endpoints. This option requires that the devices have console users with proxy permissions, so you can't use this method with headless devices.

> [!IMPORTANT]
> The user proxy authentication approach is incompatible with the use of Microsoft Defender for Endpoint. This behavior is because this authentication relies on the **DisableEnterpriseAuthProxy** registry key set to `0`, while Microsoft Defender for Endpoint requires it to be set to `1`. For more information, see [Configure machine proxy and internet connectivity settings in Microsoft Defender for Endpoint](/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

### Device proxy authentication

This approach supports the following scenarios:

- Headless devices, where no user signs in, or users of the device don't have internet access

- Authenticated proxies that don't use Windows Integrated Authentication

- If you also use Microsoft Defender for Endpoint

This approach is the most complex because it requires the following configurations:

- Make sure devices can reach the proxy server through WinHTTP in local system context. Use one of the following options to configure this behavior:

  - The command line `netsh winhttp set proxy`

  - Web proxy autodiscovery (WPAD) protocol

  - Transparent proxy

  - Configure device-wide WinINET proxy using the following group policy setting: **Make proxy settings per-machine (rather than per-user)** (ProxySettingsPerUser = `1`)

  - Routed connection, or that uses network address translation (NAT)

- Configure proxy servers to allow the computer accounts in Active Directory to access the diagnostic data endpoints. This configuration requires proxy servers to support Windows Integrated Authentication.

## Next steps

[Desktop Analytics data privacy](privacy.md)
