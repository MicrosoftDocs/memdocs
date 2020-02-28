---
# required metadata

title: Network endpoints for US government deployments - Microsoft Intune
titleSuffix: 
description: Review US government endpoints for Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/30/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 5f6682cb-5fcd-4018-b7f7-71768ad3152e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
---

# US government endpoints for Microsoft Intune

This page lists the US government endpoints needed for proxy settings in your Intune deployments.

To manage devices behind firewalls and proxy servers, you must enable communication for Intune.

- The proxy server must support both **HTTP (80)** and **HTTPS (443)** because Intune clients use both protocols
- For some tasks (like downloading software updates), Intune requires unauthenticated proxy server access to manage.microsoft.com

You can modify proxy server settings on individual client computers. You can also use Group Policy settings to change settings for all client computers located behind a specified proxy server.

Managed devices require configurations that let **All Users** access services through firewalls.

For more information about Windows 10 auto-enrollment and device registration for US government customers, see [Set up enrollment for Windows devices](../intune/enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration).

The following tables list the ports and services that the Intune client accesses:

|**Endpoint**|**IP address**|
|---------------------|-----------|
|*.manage.microsoft.us | 52.243.26.209 <br> 52.247.173.11 <br> 52.227.183.12 <br>52.227.180.205 <br> 52.227.178.107 <br> 13.72.185.168 <br> 52.227.173.179 <br> 52.227.175.242 <br> 13.72.39.209 <br> 52.243.26.209 <br> 52.247.173.11 |
| enterpriseregistration.microsoftonline.us | 13.72.188.239 <br> 13.72.55.179 |

## US Government customer designated endpoints:
- Azure portal: https:\//portal.azure.us/ 
- Office 365: https:\//portal.office365.us/ 
- Intune Company Portal: https:\//portal.manage.microsoft.us/ 

## Partner service endpoints that Intune depends on:
- AAD Sync service: https:\//syncservice.gov.us.microsoftonline.com/DirectoryService.svc
- Evo STS: https:\//login.microsoftonline.us
- Directory Proxy: https:\//directoryproxy.microsoftazure.us/DirectoryProxy.svc
- AAD Graph: https:\//directory.microsoftazure.us and https:\//graph.microsoftazure.us
- MS Graph: https:\//graph.microsoft.us
- ADRS: https:\//enterpriseregistration.microsoftonline.us

## Windows Push Notification Services
On Intune-managed devices managed by using Mobile Device Management (MDM), Windows Push Notification Services (WNS) is required for device actions and other immediate activities. For more information, see [Enterprise Firewall and Proxy Configurations to Support WNS Traffic](https://docs.microsoft.com/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config)

## Apple device network information

|**Used for**|**Hostname (IP address/subnet)**|**Protocol**|**Port**|
|------------|-----------|------------|-----------|
|Retrieving and displaying content from Apple servers|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br>\*.phobos.itunes-apple.com.akadns.net|HTTP|80|
|Communication with APNS servers|#-courier.push.apple.com<br>'#' is a random number from 0 to 50.|TCP|5223 and 443|
|Various functions including accessing the internet, iTunes store, macOS app store, iCloud, messaging, etc.|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 or 443|

For more information, see:

- [TCP and UDP ports used by Apple software products](https://support.apple.com/HT202944)
- [About macOS, iOS/iPadOS, and iTunes server host connections and iTunes background processes](https://support.apple.com/HT201999)
- [If your macOS and iOS/iPadOS clients aren't getting Apple push notifications](https://support.apple.com/HT203609)

## Next steps
[Network endpoints for Microsoft Intune](intune-endpoints.md)

