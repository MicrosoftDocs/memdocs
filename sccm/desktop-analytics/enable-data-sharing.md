---
title: Enable data sharing
titleSuffix: Configuration Manager
description: A reference guide for sharing diagnostics data with Desktop Analytics.
ms.date: 10/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Enable data sharing for Desktop Analytics

To enroll devices to Desktop Analytics, they need to send diagnostic data to Microsoft. If your environment uses a proxy server, use this information to help configure the proxy.


## Diagnostic data levels

![Diagram of diagnostic data levels for Desktop Analytics](media/diagnostic-data-levels.png)

When you integrate Configuration Manager with Desktop Analytics, you also use it to manage the diagnostic data level on devices. For the best experience, use Configuration Manager.

The basic functionality of Desktop Analytics works at the **Basic** [diagnostic data level](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels). You won't get usage or health data for your updated devices without configuring the **Enhanced (Limited)** level in Configuration Manager. 

> [!TIP]
> The **Enhanced (Limited)** setting in Configuration Manager is the **Limit Enhanced diagnostic data to the minimum required by Windows Analytics** policy on devices running Windows 10, version 1709 and later. Microsoft recommends that you enable the **Enhanced (Limited)** diagnostic data level with Desktop Analytics.
>
> Devices running Windows 10, version 1703 and earlier don't have this policy setting. When you configure the **Enhanced (Limited)** setting in Configuration Manager, these devices fall back to the **Basic** level.

For more information, see [Windows 10 enhanced diagnostic data events and fields](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!Important]   
> Microsoft has a strong commitment to providing the tools and resources that put you in control of your privacy. As a result, Microsoft doesn't collect the following data from devices located in European countries (EEA and Switzerland):
>
> - Windows diagnostic data from Windows 8.1 devices
> - App usage data for Windows 7

For more information, see [Desktop Analytics privacy](/sccm/desktop-analytics/privacy).

The following articles are also good resources for better understanding Windows diagnostic data levels:

- [Windows 10 and the GDPR for IT Decision Makers](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> Clients configured to Limit Enhanced diagnostic data will send approximately 2 MB of data to the Microsoft cloud on the initial full scan. The daily delta varies between 250-400 KB per day.
>
> The daily delta scan happens at 3:00 AM (device local time). Some events are sent at the first available time throughout the day. These times aren't configurable.
>
> For more information, see [Configure Windows diagnostic data in your organization](https://aka.ms/enterprisetelemetry).  



## Endpoints

To enable data sharing, configure your proxy server to allow the following endpoints:

> [!Important]  
> For privacy and data integrity, Windows checks for a Microsoft SSL certificate when communicating with the diagnostic data endpoints. SSL interception and inspection aren't possible. To use Desktop Analytics, exclude these endpoints from SSL inspection.<!-- BUG 4647542 -->

| Endpoint  | Function  |
|-----------|-----------|
| `https://aka.ms` | Used to locate the service |
| `https://v10c.events.data.microsoft.com` | Connected user experience and diagnostic component endpoint. Used by devices running Windows 10, version 1809 or later, or version 1803 with the 2018-09 cumulative update or later installed. |
| `https://v10.events.data.microsoft.com` | Connected user experience and diagnostic component endpoint. Used by devices running Windows 10, version 1803 _without_ the 2018-09 cumulative update installed. |
| `https://v10.vortex-win.data.microsoft.com` | Connected user experience and diagnostic component endpoint. Used by devices running Windows 10, version 1709 or earlier. |
| `https://vortex-win.data.microsoft.com` | Connected user experience and diagnostic component endpoint. Used by devices running Windows 7 and Windows 8.1 |
| `https://settings-win.data.microsoft.com` | Enables the compatibility update to send data to Microsoft. |
| `http://adl.windows.com` | Allows the compatibility update to receive the latest compatibility data from Microsoft. |
| `https://watson.telemetry.microsoft.com` | Windows Error Reporting (WER). Required to monitor deployment health in Windows 10, version 1803 or earlier. |
| `https://umwatsonc.events.data.microsoft.com` | Windows Error Reporting (WER). Required for device health reports in Windows 10, version 1809 or later. |
| `https://ceuswatcab01.blob.core.windows.net`<br> `https://ceuswatcab02.blob.core.windows.net`<br> `https://eaus2watcab01.blob.core.windows.net`<br> `https://eaus2watcab02.blob.core.windows.net`<br> `https://weus2watcab01.blob.core.windows.net`<br> `https://weus2watcab02.blob.core.windows.net` | Windows Error Reporting (WER). Required to monitor deployment health in Windows 10, version 1809 or later. |
| `https://kmwatsonc.events.data.microsoft.com` | Online Crash Analysis. Required for device health reports in Windows 10, version 1809 or later. |
| `https://oca.telemetry.microsoft.com`  | Online Crash Analysis (OCA). Required to monitor deployment health in Windows 10, version 1803 or earlier. |
| `https://login.live.com` | Required to provide a more reliable device identity for Desktop Analytics. <br> <br>To disable end-user Microsoft account access, use policy settings instead of blocking this endpoint. For more information, see [The Microsoft account in the enterprise](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| `https://graph.windows.net` | Used to automatically retrieve settings like CommercialId when attaching your hierarchy to Desktop Analytics (on Configuration Manager Server role). For more information, see [Configure the proxy for a site system server
](/sccm/core/plan-design/network/proxy-server-support#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Used to synch device collection memberships, deployment plans, and device readiness status with Desktop Analytics (on Configuration Manager Server role only). For more information, see [Configure the proxy for a site system server
](/sccm/core/plan-design/network/proxy-server-support#configure-the-proxy-for-a-site-system-server). |


## Proxy server authentication

Make sure that a proxy doesn't block the diagnostic data because of authentication. If your organization uses proxy server authentication for outbound traffic, use one or more of the following approaches:

- **Bypass** (recommended): Configure your proxy servers to not require proxy authentication for traffic to the diagnostic data endpoints. This option is the most comprehensive solution. It works for all versions of Windows 10.  

- **User proxy authentication**: Configure devices to use the signed-in user's context for proxy authentication. This method requires the devices to run Windows 10, version 1703 or later, and have user-level proxy configured (WinINET proxy), typically in Internet Explorer or Windows Settings app (Network & Internet / Proxy). Make sure that the users have proxy permission to reach the diagnostic data endpoints. This option requires that the devices have console users with proxy permissions, so you can't use this method with headless devices.

> [!IMPORTANT]
> The user proxy authentication approach is incompatible with the use of Microsoft Defender Advanced Threat Protection. This is because it relies on **DisableEnterpriseAuthProxy = 0** registry key, while Microsoft Defender ATP requires it to be set to 1.(Read more here)[<https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection>]

- **Device proxy authentication**: This is the most complex approach, requiring:
    - Ensure devices can reach proxy server through WinHTTP in local system context, configured either through 'netsh winhttp set proxy' command, WPAD, transparent proxy, routed/NATted connection, etc.
    - Configure proxy servers to allow the computer accounts in Active Directory to access the diagnostic data endpoints. This requires proxy servers to support Windows Integrated Authentication.  


