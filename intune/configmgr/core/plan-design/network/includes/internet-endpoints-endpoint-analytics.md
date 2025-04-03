---
author: banreet
ms.author: banreetkaur
ms.subservice: desktop-analytics
ms.service: configuration-manager
ms.topic: include
ms.date: 08/11/2020
ms.localizationpriority: medium
---

### Endpoints required for Configuration Manager-managed devices

Configuration Manager-managed devices send data to Intune via the connector on the Configuration Manager role and they don't need directly access to the Microsoft public cloud.

| Endpoint  | Function  |
|-----------|-----------|
| `https://graph.windows.net` | Used to automatically retrieve settings when attaching your hierarchy to Endpoint analytics on Configuration Manager server role. For more information, see [Configure the proxy for a site system server](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Used to synch device collection and devices with Endpoint analytics on Configuration Manager server role only. For more information, see [Configure the proxy for a site system server](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### Endpoints required for Intune-managed devices

To enroll devices to Endpoint analytics, they need to send required functional data to Microsoft public cloud. Endpoint Analytics uses the Windows client and Windows Server **Connected User Experiences and Telemetry** component (DiagTrack) to collect the data from Intune-managed devices. Make sure that the **Connected User Experiences and Telemetry** service on the device is running.

| Endpoint  | Function  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Used by Intune-managed devices to send [required functional data](../../../../../analytics/data-collection.md#bkmk_datacollection) to the Intune data collection endpoint. |
