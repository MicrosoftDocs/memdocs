---
# required metadata

title: Network endpoints for Microsoft Intune
titleSuffix: 
description: Review endpoints for Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/30/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: b8d9aef2-8757-4e22-9b24-a0833d27304c

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: srink
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
---

# Network endpoints for Microsoft Intune  

This page lists IP addresses and port settings needed for proxy settings in your Intune deployments.

As a cloud-only service, Intune doesn't require on-premises infrastructure such as servers or gateways.

## Access for managed devices  

To manage devices behind firewalls and proxy servers, you must enable communication for Intune.

> [!NOTE]
> The information in section also applies to the Microsoft Intune Certificate Connector. The connector has the same network requirements as managed devices.

- The proxy server must support both **HTTP (80)** and **HTTPS (443)** because Intune clients use both protocols. Windows Information Protection uses port 444.
- For some tasks (like downloading software updates for the classic pc agent), Intune requires unauthenticated proxy server access to manage.microsoft.com

You can modify proxy server settings on individual client computers. You can also use Group Policy settings to change settings for all client computers located behind a specified proxy server.


<!--
> [!NOTE] If Windows 8.1 devices haven't cached proxy server credentials, enrollment might fail because the request doesn't prompt for credentials. Enrollment fails without warning as the request wait for a connection. If users might experience this issue, instruct them to open their browser settings and save proxy server settings to enable a connection.   -->

Managed devices require configurations that let **All Users** access services through firewalls.


The following tables list the ports and services that the Intune client accesses:

|Domains    |IP address      |
|-----------|----------------|
| login.microsoftonline.com <br> *.officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net <br> enterpriseregistration.windows.net | More information [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) |
|portal.manage.microsoft.com<br> m.manage.microsoft.com |52.175.12.209<br>20.188.107.228<br>52.138.193.149<br>51.144.161.187<br>52.160.70.20<br>52.168.54.64 <br>13.72.226.202<br>52.189.220.232|
|fef.msuc03.manage.microsoft.com|23.101.0.100|
|wip.mam.manage.microsoft.com|52.187.76.84<br>13.76.5.121<br>52.165.160.237<br>40.86.82.163<br>52.233.168.142<br>168.63.101.57<br>52.187.196.98<br>52.237.196.51|
|mam.manage.microsoft.com|104.40.69.125<br>13.90.192.78<br>40.85.174.177<br>40.85.77.31<br>137.116.229.43<br>52.163.215.232<br>52.174.102.180<br>52.187.196.173<br>52.156.162.48|
|*.manage.microsoft.com|13.67.13.176/28<br>13.69.231.128/28<br>13.69.67.224/28<br>13.70.78.128/28<br>13.71.199.64/28<br>13.73.244.48/28<br>13.75.39.208/28<br>13.77.53.176/28<br>13.86.221.176/28<br>13.89.174.240/28<br>13.89.175.192/28<br>40.82.248.224/28<br>20.189.105.0/24<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>40.70.151.32/28<br>40.71.14.96/28<br>40.119.8.128/25<br>40.74.25.0/24<br>40.82.249.128/25<br>40.80.184.128/25<br>52.150.137.0/25<br>52.162.111.96/28|


## Network requirements for PowerShell scripts and Win32 apps  

If you're using Intune to deploy PowerShell scripts or Win32 apps, you'll also need to grant access to endpoints in which your tenant currently resides.

To find your tenant location (or Azure Scale Unit (ASU)), sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Tenant details**. The location is under **Tenant location** as something like North America 0501 or Europe 0202. Look for the matching number in the following table. That row will tell you which storage name and CDN endpoints to grant access to. The rows are differentiated by geographic region, as indicated by the first two letters in the names (na = North America, eu = Europe, ap = Asia Pacific). Your tenant location will be one of these three regions although your organization’s actual geographic location might be elsewhere.

|Azure Scale Unit (ASU) | Storage name | CDN |
| --- | --- |--- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0701<br>AMSUA0702<br>AMSUA0801 | naprodimedatapri<br>naprodimedatasec<br>naprodimedatahotfix | naprodimedatapri.azureedge.net<br>naprodimedatasec.azureedge.net<br>naprodimedatahotfix.azureedge.net |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502<br>AMSUB0601 | euprodimedatapri<br>euprodimedatasec<br>euprodimedatahotfix | euprodimedatapri.azureedge.net<br>euprodimedatasec.azureedge.net<br>euprodimedatahotfix.azureedge.net |
| AMSUC0101<br>AMSUC0201<br>AMSUC0301<br>AMSUC0501<br>AMSUD0101| approdimedatapri<br>approdimedatasec<br>approdimedatahotifx | approdimedatapri.azureedge.net<br>approdimedatasec.azureedge.net<br>approdimedatahotfix.azureedge.net |

## Windows Push Notification Services (WNS)  

For Intune-managed Windows devices managed using Mobile Device Management (MDM), device actions and other immediate activities require the use of Windows Push Notification Services (WNS). For more information, see [Allowing Windows Notification traffic through enterprise firewalls](/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config).  

## Delivery Optimization port requirements  

### Port requirements  

For peer-to-peer traffic, Delivery Optimization uses 7680 for TCP/IP or 3544 for NAT traversal (optionally Teredo). 
For client-service communication, it uses HTTP or HTTPS over port 80/443.

### Proxy requirements  

To use Delivery Optimization, you must allow Byte Range requests. For more information, see [Proxy requirements for Windows Update](/windows/deployment/update/windows-update-troubleshooting).

### Firewall requirements  

Allow the following hostnames through your firewall to support Delivery Optimization.
For communication between clients and the Delivery Optimization cloud service:
- \*.do.dsp.mp.microsoft.com

For Delivery Optimization metadata:
- \*.dl.delivery.mp.microsoft.com
- \*.emdl.ws.microsoft.com

## Apple device network information  

|Used for|Hostname (IP address/subnet)|Protocol|Port|
|-----|--------|------|-------|
|Retrieving and displaying content from Apple servers|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br> \*.phobos.itunes-apple.com.akadns.net |    HTTP    |      80      |
|Communications with APNS servers|#-courier.push.apple.com<br>'#' is a random number from 0 to 50.|    TCP     |  5223 and 443  |
|Various functionalities including accessing the World Wide Web, iTunes store, macOS app store, iCloud, messaging, etc. |phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net| HTTP/HTTPS |  80 or 443   |

For more information, see Apple's [TCP and UDP ports used by Apple software products](https://support.apple.com/HT202944), [About macOS, iOS/iPadOS, and iTunes server host connections and iTunes background processes](https://support.apple.com/HT201999), and [If your macOS and iOS/iPadOS clients aren't getting Apple push notifications](https://support.apple.com/HT203609).  

## Android port information

Depending on how you choose to manage Android devices, you may need to open the Google Android Enterprise ports and/or the Android push notification. For more information on Android management methods supported, see the [Android enrollment documentation](../enrollment/android-enroll.md). 

> [!NOTE]
> Because Google Mobile Services isn't available in China, devices in China managed by Intune can't use features that require Google Mobile Services. These features include: Google Play Protect capabilities such as SafetyNet device attestation, Managing apps from the Google Play Store, 
Android Enterprise capabilities (see this [Google documentation](https://support.google.com/work/android/answer/6270910)). Additionally, the Intune Company Portal app for Android uses Google Mobile Services to communicate with the Microsoft Intune service. Because Google Play services isn't available in China, some tasks can require up to 8 hours to finish. For more information, see this [article](../apps/manage-without-gms.md#limitations-of-intune-device-administrator-management-when-gms-is-unavailable).

### Google Android Enterprise 

Google provides documentation of required network ports and destination host names in their [Android Enterprise Bluebook](https://static.googleusercontent.com/media/www.android.com/en//static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf), under the **Firewall** section of that document. 

### Android push notification

Intune leverages Google Firebase Cloud Messaging (FCM) for push notification to trigger device actions and check-ins. This is required by both Android Device Administrator and Android Enterprise. For information on FCM network requirements, see Google's [FCM ports and your firewall](https://firebase.google.com/docs/cloud-messaging/concept-options#messaging-ports-and-your-firewall).

## Endpoint analytics

For more information on the required endpoints for endpoint analytics, see [Endpoint analytics proxy configuration](../../analytics/troubleshoot.md#bkmk_endpoints).
