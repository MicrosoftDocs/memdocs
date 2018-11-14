---
title: Enable data sharing
titleSuffix: Configuration Manager
description: A how-to guide for sharing diagnostics data with Desktop Analytics.
ms.date: 12/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
---

# How to enable data sharing for Desktop Analytics 

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

To enroll devices to Desktop Analytics, they need to send diagnostic data to Microsoft. If your environment uses a proxy server, use the following information to help configure the proxy. 


## Endpoints

To enable data sharing, configure your proxy server to whitelist the following endpoints:

| Endpoint  | Function  |
|-----------|-----------|
| `https://v10.events.data.microsoft.com` | Connected user experience and diagnostic component endpoint for use with Windows 10, version 1803, or later |
| `https://v10.vortex-win.data.microsoft.com` | Connected user experience and diagnostic component endpoint for Windows 10, version 1709 or earlier |
| `https://vortex-win.data.microsoft.com` | Connected user experience and diagnostic component endpoint for Windows 7 and Windows 8.1 |
| `https://settings-win.data.microsoft.com` | Enables the compatibility update to send data to Microsoft. |
| `http://adl.windows.com` | Allows the compatibility update to receive the latest compatibility data from Microsoft. |
| `https://watson.telemetry.microsoft.com` | Windows Error Reporting (WER). Required for device health and update compliance antivirus reports. Not used by Desktop Analytics. |<!--then why is it here?-->
| `https://oca.telemetry.microsoft.com`  | Online Crash Analysis (OCA). Required for device health and update compliance antivirus reports. Not used by Desktop Analytics. |<!--then why is it here?-->
| `https://login.live.com` | Windows Error Reporting (WER). Required to obtain a unique device ID. <br>**Note:** WER doesn't use this endpoint to access Microsoft account consumer services such as Xbox Live. WER uses an anti-spoofing API at that address to enhance the integrity of error reports. |
| `https://nexusrules.officeapps.live.com` | Used to request dynamic diagnostic data events from Office clients. This data is useful for drill-down and diagnostics purposes in the Desktop Analytics portal |
| `https://nexus.officeapps.live.com` | Used by Office clients to send diagnostic data events from Office 14, Office 15, and versions of Office 16 prior to 16.0.8702. It's used to collect usage and reliability signals events for Desktop Analytics. |
| `https://mobile.pipe.aria.microsoft.com/Collector/3.0/` | Used by Office clients to send diagnostic data events from universal/modern Office apps, and Win32 Office 16 versions later than 16.0.8702. It's used to collect usage and reliability signals events for Desktop Analytics. |
| `https://browser.pipe.aria.microsoft.com/Collector/3.0` | Used by Office web clients to send diagnostic data events. This endpoint is also used by Office add-ins and other extensions within Office clients. |



## SSL inspection

To ensure privacy and data integrity, Windows checks for a Microsoft SSL certificate when communicating with the diagnostic data endpoints. SSL interception and inspection isn't possible. To use Desktop Analytics, exclude the above endpoints from SSL inspection.



## Proxy server authentication

Make sure that a proxy doesn't block the diagnostic data because of authentication. If your organization uses proxy server authentication for outbound traffic, use one or more of the following approaches:

- **Bypass** (recommended): Configure your proxy servers to not require proxy authentication for traffic to the diagnostic data endpoints. This option is the most comprehensive solution. It works for all versions of Windows 10.  

- **User proxy authentication**: Configure devices to use the signed-in user's context for proxy authentication. This method requires the devices to run Windows 10, version 1703 or later. Make sure that the users have proxy permission to reach the diagnostic data endpoints. This option requires that the devices have console users with proxy permissions, so you can't use this method with headless devices.  

- **Device proxy authentication**: 
    - Configure a system-level proxy server on the devices.  
    - Configure these devices to use device-based outbound proxy authentication.  
    - Configure proxy servers to allow the machine accounts to access the diagnostic data endpoints.  



## Diagnostic data levels

When you integrate Configuration Manager with Desktop Analytics, you also use it to manage the diagnostic data level on devices. For the best experience, use Configuration Manager. 

You can also set the diagnostic data level on devices with the Desktop Analytics deployment script, by group policy, or Microsoft Intune. For more information, see [Methods to enroll devices](/sccm/desktop-analytics/set-up#methods-to-enroll-devices). 

The basic functionality of Desktop Analytics works at the **Basic** diagnostic data level. You won't get usage or health data for your updated devices without enabling the **Enhanced** level. Microsoft recommends that you enable the **Enhanced** diagnostic data level. 

On devices running Windows 10, version 1709 (or later), the Enhanced diagnostic data setting includes the **Limited enhanced** data level. For more information, see [Windows 10 enhanced diagnostic data events and fields used by Windows Analytics](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)). 

For more information, see [Windows Analytics and privacy](https://docs.microsoft.com/windows/deployment/update/windows-analytics-privacy).

<!--{DO WE NEED TO ADDRESS PRIVACY ISSUES IN SOME WAY ANALOGOUS TO THE WA PRIVACY TOPIC?}-->

