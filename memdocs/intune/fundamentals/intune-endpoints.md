---
# required metadata

title: Network endpoints for Microsoft Intune
titleSuffix: 
description: Review endpoints for Intune. This page lists IP addresses and port settings needed for proxy settings in your Intune deployments.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 06/23/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: srink
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# Network endpoints for Microsoft Intune  

This article lists IP addresses and port settings needed for proxy settings in your Microsoft Intune deployments.

As a cloud-only service, Intune doesn't require an on-premises infrastructure such as servers or gateways.

## Access for managed devices  

To manage devices behind firewalls and proxy servers, you must enable communication for Intune.

> [!NOTE]
> The information in this section also applies to the [Microsoft Intune Certificate Connector](../protect/certificate-connector-prerequisites.md). The connector has the same network requirements as managed devices.

- The proxy server must support both **HTTP (80)** and **HTTPS (443)** because Intune clients use both protocols. Windows Information Protection uses port 444.
- For some tasks (like downloading software updates for the classic pc agent), Intune requires unauthenticated proxy server access to manage.microsoft.com

> [!NOTE]
> The inspection of SSL traffic is not supported to 'manage.microsoft.com' endpoint.

You can modify proxy server settings on individual client computers. You can also use Group Policy settings to change settings for all client computers located behind a specified proxy server.


<!--
> [!NOTE] If Windows 8.1 devices haven't cached proxy server credentials, enrollment might fail because the request doesn't prompt for credentials. Enrollment fails without warning as the request wait for a connection. If users might experience this issue, instruct them to open their browser settings and save proxy server settings to enable a connection.   -->

Managed devices require configurations that let **All Users** access services through firewalls.

To make it easier to configure services through firewalls, we have onboarded with the Office 365 Endpoint service. At this time, the Intune services are accessed through a PowerShell script. There are other dependent services for Intune which are already covered as part of the M365 Service and are marked as 'required'. Services already covered by M365 are not included in the script to avoid duplication.
By using the following PowerShell script, you can retrieve the list of IP addresses for the Intune service. This provides the same list as the subnets indicated in the IP address table below.

```PowerShell
(invoke-restmethod -Uri ("https://endpoints.office.com/endpoints/WorldWide?ServiceAreas=MEM`&clientrequestid=" + ([GUID]::NewGuid()).Guid)) | ?{$_.ServiceArea -eq "MEM" -and $_.ips} | select -unique -ExpandProperty ips
```

By using the following PowerShell script, you can retrieve the list of FQDNs used by Intune and Autopilot.

```PowerShell
(invoke-restmethod -Uri ("https://endpoints.office.com/endpoints/WorldWide?ServiceAreas=MEM`&clientrequestid=" + ([GUID]::NewGuid()).Guid)) | ?{$_.ServiceArea -eq "MEM" -and $_.urls} | select -unique -ExpandProperty urls
```

This provides a convenient method to list and review all services required by Intune and autopilot in one location. You will also need FQDN's that are covered as part of M365 Requirements. For reference this is the list of URL's returned, and the service they are tied to.

|FQDN    |Associated Service      |
|-----------|----------------|
|*.manage.microsoft.com| Intune Service |
|manage.microsoft.com| Intune Service |
|*.delivery.mp.microsoft.com| Delivery Optimization |
|*.prod.do.dsp.mp.microsoft.com| Delivery Optimization |
|*.update.microsoft.com| Delivery Optimization |
|*.windowsupdate.com| Delivery Optimization |
|emdl.ws.microsoft.com| Delivery Optimization |
|tsfe.trafficshaping.dsp.mp.microsoft.com| Delivery Optimization |
|time.windows.com| NTP Sync |
|www.msftconnecttest.com| NTP Sync |
|www.msftncsi.com| NTP Sync |
|*.s-microsoft.com| Windows Notifications & Store |
|clientconfig.passport.net| Windows Notifications & Store |
|windowsphone.com| Windows Notifications & Store |
|approdimedatahotfix.azureedge.net| Scripts & Win32 Apps |
|approdimedatapri.azureedge.net| Scripts & Win32 Apps |
|approdimedatasec.azureedge.net| Scripts & Win32 Apps |
|euprodimedatahotfix.azureedge.net| Scripts & Win32 Apps |
|euprodimedatapri.azureedge.net| Scripts & Win32 Apps |
|euprodimedatasec.azureedge.net| Scripts & Win32 Apps |
|naprodimedatahotfix.azureedge.net| Scripts & Win32 Apps |
|naprodimedatapri.azureedge.net| Scripts & Win32 Apps |
|swda01-mscdn.azureedge.net| Scripts & Win32 Apps |
|swda02-mscdn.azureedge.net| Scripts & Win32 Apps |
|swdb01-mscdn.azureedge.net| Scripts & Win32 Apps |
|swdb02-mscdn.azureedge.net| Scripts & Win32 Apps |
|swdc01-mscdn.azureedge.net| Scripts & Win32 Apps |
|swdc02-mscdn.azureedge.net| Scripts & Win32 Apps |
|swdd01-mscdn.azureedge.net| Scripts & Win32 Apps |
|swdd02-mscdn.azureedge.net| Scripts & Win32 Apps |
|swdin01-mscdn.azureedge.net| Scripts & Win32 Apps |
|swdin02-mscdn.azureedge.net| Scripts & Win32 Apps |
|*.notify.windows.com| Push Notifications |
|*.wns.windows.com| Push Notifications |
|*.dl.delivery.mp.microsoft.com| Delivery Optimization |
|*.do.dsp.mp.microsoft.com| Delivery Optimization |
|*.emdl.ws.microsoft.com| Delivery Optimization |
|ekcert.spserv.microsoft.com| Autopilot Self-deploy |
|ekop.intel.com| Autopilot Self-deploy |
|ftpm.amd.com| Autopilot Self-deploy |
|*.itunes.apple.com| Apple Device Management |
|*.mzstatic.com| Apple Device Management |
|*.phobos.apple.com| Apple Device Management |
|5-courier.push.apple.com| Apple Device Management |
|ax.itunes.apple.com.edgesuite.net| Apple Device Management |
|itunes.apple.com| Apple Device Management |
|ocsp.apple.com| Apple Device Management |
|phobos.apple.com| Apple Device Management |
|phobos.itunes-apple.com.akadns.net| Apple Device Management |
|intunecdnpeasd.azureedge.net|  |
|*.channelservices.microsoft.com| Remote Help |
|*.go-mpulse.net| Remote Help |
|*.infra.lync.com| Remote Help |
|*.resources.lync.com| Remote Help |
|*.support.services.microsoft.com| Remote Help |
|*.trouter.skype.com| Remote Help |
|*.vortex.data.microsoft.com| Remote Help |
|edge.skype.com| Remote Help |
|remoteassistanceprodacs.communication.azure.com| Remote Help |
|lgmsapeweu.blob.core.windows.net | Collect Diagnostics |

The following tables list the ports and services that the Intune client accesses:

|Domains    |IP address      |
|-----------|----------------|
| login.microsoftonline.com <br> *.officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net <br> enterpriseregistration.windows.net | More information [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) |
|*.manage.microsoft.com <br> manage.microsoft.com <br>|104.46.162.96/27<br>13.67.13.176/28<br>13.67.15.128/27<br>13.69.231.128/28<br>13.69.67.224/28<br>13.70.78.128/28<br>13.70.79.128/27<br>13.71.199.64/28<br>13.73.244.48/28<br>13.74.111.192/27<br>13.77.53.176/28<br>13.86.221.176/28<br>13.89.174.240/28<br>13.89.175.192/28<br>20.189.172.160/27<br>20.189.229.0/25<br>20.191.167.0/25<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>20.44.19.224/27<br>20.49.93.160/27<br>20.192.174.216/29<br>20.192.159.40/29<br>20.204.193.12/30<br>20.204.193.10/31<br>40.119.8.128/25<br>40.67.121.224/27<br>40.70.151.32/28<br>40.71.14.96/28<br>40.74.25.0/24<br>40.78.245.240/28<br>40.78.247.128/27<br>40.79.197.64/27<br>40.79.197.96/28<br>40.80.180.208/28<br>40.80.180.224/27<br>40.80.184.128/25<br>40.82.248.224/28<br>40.82.249.128/25<br>52.150.137.0/25<br>52.162.111.96/28<br>52.168.116.128/27<br>52.182.141.192/27<br>52.236.189.96/27<br>52.240.244.160/27|


## Network requirements for PowerShell scripts and Win32 apps  

If you're using Intune to deploy PowerShell scripts or Win32 apps, you'll also need to grant access to endpoints in which your tenant currently resides.

To find your tenant location (or Azure Scale Unit (ASU)), sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Tenant details**. The location is under **Tenant location** as something like North America 0501 or Europe 0202. Look for the matching number in the following table. That row will tell you which storage name and CDN endpoints to grant access to. The rows are differentiated by geographic region, as indicated by the first two letters in the names (na = North America, eu = Europe, ap = Asia Pacific). Your tenant location will be one of these three regions although your organization’s actual geographic location might be elsewhere.

|Azure Scale Unit (ASU) | Storage name | CDN |
| --- | --- |--- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0601<br>AMSUA0701<br>AMSUA0702<br>AMSUA0801<br>AMSUA0901 | naprodimedatapri<br>naprodimedatasec<br>naprodimedatahotfix | naprodimedatapri.azureedge.net<br>naprodimedatasec.azureedge.net<br>naprodimedatahotfix.azureedge.net |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502<br>AMSUB0601<br>AMSUB0701 | euprodimedatapri<br>euprodimedatasec<br>euprodimedatahotfix | euprodimedatapri.azureedge.net<br>euprodimedatasec.azureedge.net<br>euprodimedatahotfix.azureedge.net |
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

For more information, see [Use Apple products on enterprise networks](https://support.apple.com/HT210060), [TCP and UDP ports used by Apple software products](https://support.apple.com/HT202944), [About macOS, iOS/iPadOS, and iTunes server host connections and iTunes background processes](https://support.apple.com/HT201999), and [If your macOS and iOS/iPadOS clients aren't getting Apple push notifications](https://support.apple.com/HT203609).  

## Android port information

Depending on how you choose to manage Android devices, you may need to open the Google Android Enterprise ports and/or the Android push notification. For more information on Android management methods supported, see the [Android enrollment documentation](../enrollment/android-enroll.md). 

> [!NOTE]
> Because Google Mobile Services isn't available in China, devices in China managed by Intune can't use features that require Google Mobile Services. These features include: Google Play Protect capabilities such as SafetyNet device attestation, Managing apps from the Google Play Store, 
Android Enterprise capabilities (see this [Google documentation](https://support.google.com/work/android/answer/6270910)). Additionally, the Intune Company Portal app for Android uses Google Mobile Services to communicate with the Microsoft Intune service. Because Google Play services isn't available in China, some tasks can require up to 8 hours to finish. For more information, see this [article](../apps/manage-without-gms.md#limitations-of-intune-management-when-gms-is-unavailable).

### Android (AOSP)  

|Used for|Hostname (IP address/subnet)|Protocol|Port|
|-----|--------|------|-------|
|Downloading and installing Microsoft Intune and Microsoft Authenticator apps|intunecdnpeasd.azureedge.net|    HTTPS    |      443      |

### Google Android Enterprise 

Google provides documentation of required network ports and destination host names in their [Android Enterprise Bluebook](https://static.googleusercontent.com/media/www.android.com/en//static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf), under the **Firewall** section of that document. 

### Android push notification

Intune leverages Google Firebase Cloud Messaging (FCM) for push notification to trigger device actions and check-ins. This is required by both Android Device Administrator and Android Enterprise. For information on FCM network requirements, see Google's [FCM ports and your firewall](https://firebase.google.com/docs/cloud-messaging/concept-options#messaging-ports-and-your-firewall).

## Endpoint analytics

For more information on the required endpoints for endpoint analytics, see [Endpoint analytics proxy configuration](../../analytics/troubleshoot.md#bkmk_endpoints).

## Microsoft Defender for Endpoint

For more information about configuring Defender for Endpoint connectivity, see [Connectivity Requirements](../protect/mde-security-integration.md#connectivity-requirements)

Allow the following hostnames through your firewall to support Security Management for Defender for Endpoint.
For communication between clients and the cloud service:
- \*.dm.microsoft.com - The use of a wildcard supports the cloud-service endpoints that are used for enrollment, check-in, and reporting, and which can change as the service scales.

## Related topics

[Office 365 URLs and IP address ranges](/microsoft-365/enterprise/urls-and-ip-address-ranges)

[Microsoft 365 network connectivity overview](https://support.office.com/article/client-connectivity-4232abcf-4ae5-43aa-bfa1-9a078a99c78b)

[Content delivery networks (CDNs)](https://support.office.com/article/content-delivery-networks-0140f704-6614-49bb-aa6c-89b75dcd7f1f)

[Other endpoints not included in the Office 365 IP Address and URL Web service](/microsoft-365/enterprise/additional-office365-ip-addresses-and-urls)

[Managing Office 365 endpoints](/microsoft-365/enterprise/managing-office-365-endpoints)

