---
# required metadata

title: Network endpoints for Microsoft Intune
titleSuffix: 
description: Review endpoints for Intune. This page lists IP addresses and port settings needed for proxy settings in your Intune deployments.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 01/09/2025
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: davidra
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

- The endpoints in this article allow access to the ports identified in the following tables.
- For some tasks, Intune requires unauthenticated proxy server access to manage.microsoft.com, *.azureedge.net, and graph.microsoft.com.

  > [!NOTE]
  > SSL traffic inspection is not supported for '\*.manage.microsoft.com', '\*.dm.microsoft.com', or the [Device Health Attestation (DHA) endpoints listed in the compliance section](#migrating-device-health-attestation-compliance-policies-to-microsoft-azure-attestation).

You can modify proxy server settings on individual client computers. You can also use Group Policy settings to change settings for all client computers located behind a specified proxy server.

Managed devices require configurations that let **All Users** access services through firewalls.

## PowerShell script

To make it easier to configure services through firewalls, we onboarded with the Office 365 Endpoint service. At this time, the Intune endpoint information is accessed through a PowerShell script. There are other dependent services for Intune that are already covered as part of the Microsoft 365 Service and are marked as 'required'. Services already covered by Microsoft 365 aren't included in the script to avoid duplication.

By using the following PowerShell script, you can retrieve the list of IP addresses for the Intune service.

```PowerShell
(invoke-restmethod -Uri ("https://endpoints.office.com/endpoints/WorldWide?ServiceAreas=MEM`&`clientrequestid=" + ([GUID]::NewGuid()).Guid)) | ?{$_.ServiceArea -eq "MEM" -and $_.ips} | select -unique -ExpandProperty ips
```

By using the following PowerShell script, you can retrieve the list of FQDNs used by Intune and dependent services. When you run the script, the URLs in the script output may be different than the URLs in the following tables. At a minimum, make sure you include the URLs in the tables.

```PowerShell
(invoke-restmethod -Uri ("https://endpoints.office.com/endpoints/WorldWide?ServiceAreas=MEM`&`clientrequestid=" + ([GUID]::NewGuid()).Guid)) | ?{$_.ServiceArea -eq "MEM" -and $_.urls} | select -unique -ExpandProperty urls
```

The script provides a convenient method to list and review all services required by Intune and Autopilot in one location. Additional properties can be returned from the endpoint service such as the category property, which indicates whether the FQDN or IP should be configured as **Allow**, **Optimize** or **Default**.

## Endpoints
 
You also need FQDNs that are covered as part of Microsoft 365 Requirements. For reference, the following tables show the service they're tied to, and the list of URLs returned.

The data columns shown in the tables are:

- **ID**: The ID number of the row, also known as an endpoint set. This ID is the same as is returned by the web service for the endpoint set.

- **Category**: Shows whether the endpoint set is categorized as **Optimize**, **Allow**, or **Default**. This column also lists which endpoint sets are required to have network connectivity. For endpoint sets that aren't required to have network connectivity, we provide notes in this field to indicate what functionality would be missing if the endpoint set is blocked. If you're excluding an entire service area, the endpoint sets listed as required don't require connectivity.

  You can read about these categories and guidance for their management in [New Microsoft 365 endpoint categories](/microsoft-365/enterprise/microsoft-365-network-connectivity-principles?#new-office-365-endpoint-categories).

- **ER**: This is Yes/True if the endpoint set is supported over Azure ExpressRoute with Microsoft 365 route prefixes. The BGP community that includes the route prefixes shown aligns with the service area listed. When ER is No / False, then ExpressRoute isn't supported for this endpoint set.

- **Addresses**: Lists the FQDNs or wildcard domain names and IP address ranges for the endpoint set. Note that an IP address range is in CIDR format and may include many individual IP addresses in the specified network.

- **Ports**: Lists the TCP or UDP ports that are combined with listed IP addresses to form the network endpoint. You may notice some duplication in IP address ranges where there are different ports listed.

### Intune core service

>[!NOTE]
> If the firewall that you are using allows you to create firewall rules using a domain name, then use the *.manage.microsoft.com and manage.microsoft.com domain. However, if the firewall provider that you are using, does not allow you to create a firewall rule using a domain name, we recommend that you use the approved list of all subnets in this section.

ID |Desc |Category |ER |Addresses |Ports
-- |---------------------------------------------------------------- |---------------------|--- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------|
163 | Intune client and host service| Allow<BR>Required | False | `*.manage.microsoft.com`<BR>`manage.microsoft.com`<BR>`EnterpriseEnrollment.manage.microsoft.com`<BR>`104.46.162.96/27, 13.67.13.176/28, 13.67.15.128/27, 13.69.231.128/28, 13.69.67.224/28, 13.70.78.128/28, 13.70.79.128/27, 13.74.111.192/27, 13.77.53.176/28, 13.86.221.176/28,13.89.174.240/28, 13.89.175.192/28, 20.189.229.0/25, 20.191.167.0/25, 20.37.153.0/24, 20.37.192.128/25, 20.38.81.0/24, 20.41.1.0/24, 20.42.1.0/24, 20.42.130.0/24, 20.42.224.128/25, 20.43.129.0/24, 20.44.19.224/27, 40.119.8.128/25, 40.67.121.224/27, 40.70.151.32/28, 40.71.14.96/28, 40.74.25.0/24, 40.78.245.240/28, 40.78.247.128/27, 40.79.197.64/27, 40.79.197.96/28, 40.80.180.208/28, 40.80.180.224/27, 40.80.184.128/25, 40.82.248.224/28, 40.82.249.128/25, 52.150.137.0/25, 52.162.111.96/28, 52.168.116.128/27, 52.182.141.192/27, 52.236.189.96/27, 52.240.244.160/27, 20.204.193.12/30, 20.204.193.10/31, 20.192.174.216/29, 20.192.159.40/29, 104.208.197.64/27, 172.160.217.160/27, 172.201.237.160/27, 172.202.86.192/27, 172.205.63.0/25, 172.212.214.0/25, 172.215.131.0/27, 20.168.189.128/27, 20.199.207.192/28, 20.204.194.128/31, 20.208.149.192/27, 20.208.157.128/27, 20.214.131.176/29, 20.43.129.0/24, 20.91.147.72/29, 4.145.74.224/27, 4.150.254.64/27, 4.154.145.224/27, 4.200.254.32/27, 4.207.244.0/27, 4.213.25.64/27, 4.213.86.128/25, 4.216.205.32/27, 4.237.143.128/25, 40.84.70.128/25, 48.218.252.128/25, 57.151.0.192/27, 57.153.235.0/25, 57.154.140.128/25, 57.154.195.0/25, 57.155.45.128/25, 68.218.134.96/27, 74.224.214.64/27, 74.242.35.0/25, 172.208.170.0/25, 74.241.231.0/25, 74.242.184.128/25` | **TCP:** 80, 443|
172 | MDM Delivery Optimization | Default<BR>Required | False | `*.do.dsp.mp.microsoft.com`<BR> `*.dl.delivery.mp.microsoft.com`<BR> | **TCP:** 80, 443|
170 | MEM - Win32Apps| Default<BR>Required | False | `swda01-mscdn.manage.microsoft.com`<br>`swda02-mscdn.manage.microsoft.com`<br>`swdb01-mscdn.manage.microsoft.com`<br>`swdb02-mscdn.manage.microsoft.com`<br>`swdc01-mscdn.manage.microsoft.com`<br>`swdc02-mscdn.manage.microsoft.com`<br>`swdd01-mscdn.manage.microsoft.com`<br>`swdd02-mscdn.manage.microsoft.com`<br>`swdin01-mscdn.manage.microsoft.com`<BR>`swdin02-mscdn.manage.microsoft.com` | **TCP:** 443|
97 | Consumer Outlook.com, OneDrive, Device authentication and Microsoft account | Default<BR>Required | False | `account.live.com`<BR>`login.live.com`<BR> |**TCP:** 443  |
190 | Endpoint discovery | Default<BR>Required | False | `go.microsoft.com` | **TCP:** 80, 443|
189 | Dependency - Feature Deployment| Default<BR>Required | False |`config.edge.skype.com`<BR> | **TCP:** 443|
<!--170 | Organizational messages| Default<BR>Required | False | `fd.api.orgmsg.microsoft.com`<BR>`ris.prod.api.personalization.ideas.microsoft.com`<BR>`contentauthassetscdn-prod.azureedge.net`<BR>`contentauthassetscdn-prodeur.azureedge.net`<BR>`contentauthrafcontentcdn-prod.azureedge.net`<BR>`contentauthrafcontentcdn-prodeur.azureedge.net`<BR> | **TCP:** 443|check if it's been added by 27th March in the tool-->

### Autopilot dependencies

ID |Desc |Category |ER |Addresses |Ports|
-- |-- |-----|--- |--------------|--------------------------------|
164 | Autopilot - Windows Update| Default<BR>Required | False | `*.windowsupdate.com`<BR>`*.dl.delivery.mp.microsoft.com`<BR>`*.prod.do.dsp.mp.microsoft.com`<BR>`*.delivery.mp.microsoft.com`<BR>`*.update.microsoft.com`<BR>`tsfe.trafficshaping.dsp.mp.microsoft.com`<BR>`adl.windows.com`<BR> | **TCP:** 80, 443|
165 | Autopilot - NTP Sync | Default<BR>Required | False | `time.windows.com` |**UDP:** 123|
169 | Autopilot - WNS Dependencies| Default<BR>Required | False | `clientconfig.passport.net`<BR>`windowsphone.com`<BR>`*.s-microsoft.com`<BR>`c.s-microsoft.com` | **TCP:** 443 |
173 | Autopilot - Third party deployment dependencies| Default<BR>Required | False | `ekop.intel.com`<BR>`ekcert.spserv.microsoft.com`<BR>`ftpm.amd.com`<BR> | **TCP:** 443|
182 | Autopilot - Diagnostics upload | Default<BR>Required | False | `lgmsapeweu.blob.core.windows.net`<BR>`lgmsapewus2.blob.core.windows.net`<BR>`lgmsapesea.blob.core.windows.net`<BR>`lgmsapeaus.blob.core.windows.net`<BR>`lgmsapeind.blob.core.windows.net`<BR> | **TCP:** 443|

### Remote Help

ID |Desc |Category |ER |Addresses |Ports|Notes|
-- |-- |-----|--- | --------------| --------------------------------|------------|
181 | MEM - Remote Help Feature| Default<BR>Required | False |`*.support.services.microsoft.com`<BR>`remoteassistance.support.services.microsoft.com`<BR>`rdprelayv3eastusprod-0.support.services.microsoft.com`<BR>`*.trouter.skype.com`<BR>`remoteassistanceprodacs.communication.azure.com`<BR>`edge.skype.com`<BR>`aadcdn.msftauth.net`<BR>`aadcdn.msauth.net`<BR>`alcdn.msauth.net`<BR>`wcpstatic.microsoft.com`<BR>`*.aria.microsoft.com`<BR>`browser.pipe.aria.microsoft.com`<BR>`*.events.data.microsoft.com`<BR>`v10.events.data.microsoft.com`<BR>`*.monitor.azure.com`<BR>`js.monitor.azure.com`<BR>`edge.microsoft.com`<BR>`*.trouter.communication.microsoft.com`<BR>`go.trouter.communication.microsoft.com`<BR>`*.trouter.teams.microsoft.com`<BR>`trouter2-usce-1-a.trouter.teams.microsoft.com`<BR>`api.flightproxy.skype.com`<BR>`ecs.communication.microsoft.com`<BR>`remotehelp.microsoft.com`<BR>`trouter-azsc-usea-0-a.trouter.skype.com`<BR> | **TCP:** 443|
187 | Dependency - Remote Help web pubsub | Default<BR>Required | False | `*.webpubsub.azure.com`<BR> `AMSUA0101-RemoteAssistService-pubsub.webpubsub.azure.com`<BR>| **TCP:** 443|
188 | Remote Help Dependency for GCC customers| Default<BR>Required | False |`remoteassistanceweb-gcc.usgov.communication.azure.us`<BR>`gcc.remotehelp.microsoft.com`<BR>`gcc.relay.remotehelp.microsoft.com`<BR>`*.gov.teams.microsoft.us` | **TCP:** 443|

<!--### Windows update for Business deployment service

ID |Desc |Category |ER |Addresses |Ports|Notes|
-- |-- |-----|--- | --------------| --------------------------------|------------|
181 | Need to add| Default<BR>Required | False |`devicelistenerprod.microsoft.com`<BR>`devicelistenerprod.eudb.microsoft.com`<BR>`login.windows.net`<BR>`payloadprod*.blob.core.windows.net`<BR> | **TCP:** 443|
187 | need to add | Default<BR>Required | False | `*.webpubsub.azure.com`<BR> `AMSUA0101-RemoteAssistService-pubsub.webpubsub.azure.com`<BR>| **TCP:** 443| -->

### Intune dependencies

In this section, the following tables list the Intune dependencies and the ports and services that the Intune client accesses.

- [Windows Push Notification Services dependencies](#windows-push-notification-services-wns-dependencies)
- [Delivery optimization dependencies](#delivery-optimization-dependencies)
- [Apple dependencies](#apple-dependencies)
- [Android AOSP dependencies](#android-aosp-dependencies)

#### Windows Push Notification Services (WNS) dependencies

| ID  | Desc | Category | ER    | Addresses | Ports |
| --- | ---- | -------- | ----- | --------- | ----- |
| 171 | MEM - WNS Dependencies | Default<BR>Required | False | `*.notify.windows.com`<BR>`*.wns.windows.com`<BR>`sinwns1011421.wns.windows.com`<BR>`sin.notify.windows.com`<BR> | **TCP:** 443 |

For Intune-managed Windows devices managed using Mobile Device Management (MDM), device actions and other immediate activities require the use of Windows Push Notification Services (WNS). For more information, see [Allowing Windows Notification traffic through enterprise firewalls](/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config).

#### Delivery optimization dependencies

| ID  | Desc | Category | ER    | Addresses | Ports |
| --- | ---- | -------- | ----- | --------- | ----- |
| 172 | MDM - Delivery Optimization Dependencies | Default<BR>Required | False | `*.do.dsp.mp.microsoft.com`<BR>`*.dl.delivery.mp.microsoft.com`<BR> | **TCP:** 80, 443 |

**Port requirements** - For client-service communication, it uses HTTP or HTTPS over port 80/443. Optionally, for peer-to-peer traffic, Delivery Optimization uses 7680 for TCP/IP and Teredo on port 3544 for NAT traversal. For more information, see [Delivery Optimization documentation](/windows/deployment/do/)

**Proxy requirements** - To use Delivery Optimization, you must allow Byte Range requests. For more information, see [Proxy requirements for Delivery Optimization](/windows/deployment/do/waas-delivery-optimization-faq#what-are-the-requirements-if-i-use-a-proxy).

**Firewall requirements** - Allow the following hostnames through your firewall to support Delivery Optimization. For communication between clients and the Delivery Optimization cloud service:

- \*.do.dsp.mp.microsoft.com

For Delivery Optimization metadata:

- \*.dl.delivery.mp.microsoft.com

#### Apple dependencies

| ID  | Desc | Category | ER    | Addresses | Ports |
| --- | ---- | -------- | ----- | --------- | ----- |
| 178 | MEM - Apple Dependencies | Default<BR>Required | False | `itunes.apple.com`<BR>`*.itunes.apple.com`<BR>`*.mzstatic.com`<BR>`*.phobos.apple.com`<BR>`phobos.itunes-apple.com.akadns.net`<BR>`*.push.apple.com`<BR>`phobos.apple.com`<BR>`ocsp.apple.com`<BR>`ax.itunes.apple.com`<BR>`ax.itunes.apple.com.edgesuite.net`<BR>`s.mzstatic.com`<BR>`a1165.phobos.apple.com`<BR> |**TCP:** 80, 443, 5223|

For more information, see the following resources:

- [Use Apple products on enterprise networks](https://support.apple.com/HT210060)
- [TCP and UDP ports used by Apple software products](https://support.apple.com/HT202944)
- [About macOS, iOS/iPadOS, and iTunes server host connections and iTunes background processes](https://support.apple.com/HT201999)
- [If your macOS and iOS/iPadOS clients aren't getting Apple push notifications](https://support.apple.com/HT203609)

#### Android AOSP dependencies

| ID  | Desc | Category | ER    | Addresses | Ports |
| --- | ---- | -------- | ----- | --------- | ----- |
| 179 | MEM - Android AOSP Dependency | Default<BR>Required | False | `intunecdnpeasd.azureedge.net`<BR> | **TCP:** 443 |

> [!NOTE]
> Because Google Mobile Services isn't available in China, devices in China managed by Intune can't use features that require Google Mobile Services. These features include: Google Play Protect capabilities such as Play Integrity Verdict, Managing apps from the Google Play Store, 
Android Enterprise capabilities (see this [Google documentation](https://support.google.com/work/android/answer/6270910)). Additionally, the Intune Company Portal app for Android uses Google Mobile Services to communicate with the Microsoft Intune service. Because Google Play services isn't available in China, some tasks can require up to 8 hours to finish. For more information, see [Limitations of Intune management when GMS is unavailable](../apps/manage-without-gms.md#limitations-of-intune-management-when-gms-is-unavailable).

**Android port information** - Depending on how you choose to manage Android devices, you may need to open the Google Android Enterprise ports and/or the Android push notification. For more information on Android management methods supported, see the [Android enrollment documentation](deployment-guide-enrollment-android.md).

#### Android Enterprise dependencies

**Google Android Enterprise** - Google provides documentation of required network ports and destination host names in their [Android Enterprise Bluebook](https://static.googleusercontent.com/media/www.android.com/en//static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf), under the **Firewall** section of that document.

**Android push notification** - Intune uses Google Firebase Cloud Messaging (FCM) for push notification to trigger device actions and check-ins. This is required by both Android Device Administrator and Android Enterprise. For information on FCM network requirements, see Google's [FCM ports and your firewall](https://firebase.google.com/docs/cloud-messaging/concept-options#messaging-ports-and-your-firewall).

### Authentication dependencies

ID |Desc |Category |ER |Addresses |Ports|
-- |-- |-----|--- | --------------| --------------------------------|
56 | Authentication and Identity, includes Azure Active Directory and Azure AD related services.| Allow<BR>Required | True |`login.microsoftonline.com`<BR>`graph.windows.net` | **TCP:** 80, 443|
150 | Office Customization Service provides Office 365 ProPlus deployment configuration, application settings, and cloud based policy management. | Default | False |`*.officeconfig.msocdn.com`<BR>`config.office.com`| **TCP:** 443|
59 | Identity supporting services & CDNs. | Default<BR>Required | False |`enterpriseregistration.windows.net`<BR>| **TCP:** 80, 443|

For more information, go to [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

<!-- Older table. Will be removed soon after all the other new tables are finalized. This may take until April 2024
You'll also need FQDNs that are covered as part of Microsoft 365 Requirements. For reference, the following table is the list of URLs returned, and the service they're tied to. When you run the script, the URL list in the script output can be different then the URLs in the following table. At a minimum, make sure you include the URLs in the following table.

|FQDN    |Associated Service      |
|-----------|----------------|
|*.manage.microsoft.com| Intune Service |
|manage.microsoft.com| Intune Service |
|*.prod.do.dsp.mp.microsoft.com| Windows Update and Delivery Optimization |
|*.windowsupdate.com| Windows Update and Delivery Optimization |
|*.dl.delivery.mp.microsoft.com| Windows Update and Delivery Optimization |
|*.update.microsoft.com| Windows Update and Delivery Optimization |
|*.delivery.mp.microsoft.com| Windows Update and Delivery Optimization |
|tsfe.trafficshaping.dsp.mp.microsoft.com| Windows Update and Delivery Optimization |
|*.do.dsp.mp.microsoft.com| Delivery Optimization |
|*.notify.windows.com| Push Notifications |
|*.wns.windows.com| Push Notifications |
|devicelistenerprod.microsoft.com| Windows Update for Business deployment service |
|devicelistenerprod.eudb.microsoft.com| Windows Update for Business deployment service |
|login.windows.net| Windows Update for Business deployment service |
|payloadprod*.blob.core.windows.net| Windows Update for Business deployment service |
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
|fd.api.orgmsg.microsoft.com | Organizational messages |
|ris.prod.api.personalization.ideas.microsoft.com | Organizational messages |
|contentauthassetscdn-prod.azureedge.net | Organizational messages |
|contentauthassetscdn-prodeur.azureedge.net | Organizational messages |
|contentauthrafcontentcdn-prod.azureedge.net | Organizational messages |
|contentauthrafcontentcdn-prodeur.azureedge.net | Organizational messages |
|config.edge.skype.com | Feature Deployment |
|go.microsoft.com | Endpoint discovery |


The following tables list the ports and services that the Intune client accesses:

|Domains    |IP address      |
|-----------|----------------|
| login.microsoftonline.com <br> *.officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net <br> enterpriseregistration.windows.net | More information [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) |
|*.manage.microsoft.com <br> manage.microsoft.com <br>|104.46.162.96/27<br>13.67.13.176/28<br>13.67.15.128/27<br>13.69.231.128/28<br>13.69.67.224/28<br>13.70.78.128/28<br>13.70.79.128/27<br>13.74.111.192/27<br>13.77.53.176/28<br>13.86.221.176/28<br>13.89.174.240/28<br>13.89.175.192/28<br>20.189.172.160/27<br>20.189.229.0/25<br>20.191.167.0/25<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>20.44.19.224/27<br>20.192.174.216/29<br>20.192.159.40/29<br>20.204.193.12/30<br>20.204.193.10/31<br>40.119.8.128/25<br>40.67.121.224/27<br>40.70.151.32/28<br>40.71.14.96/28<br>40.74.25.0/24<br>40.78.245.240/28<br>40.78.247.128/27<br>40.79.197.64/27<br>40.79.197.96/28<br>40.80.180.208/28<br>40.80.180.224/27<br>40.80.184.128/25<br>40.82.248.224/28<br>40.82.249.128/25<br>52.150.137.0/25<br>52.162.111.96/28<br>52.168.116.128/27<br>52.182.141.192/27<br>52.236.189.96/27<br>52.240.244.160/27|
-->

## Network requirements for PowerShell scripts and Win32 apps  

If you are using Intune for scenarios that use the Intune management extension, like deploying [Win32 apps](../apps/apps-win32-app-management.md), [Powershell scripts](../apps/intune-management-extension.md), [Remediations](../fundamentals/remediations.md), [Endpoint analytics](../../analytics/overview.md), [Custom compliance policies](../protect/compliance-use-custom-settings.md) or [BIOS configuration profiles](../configuration/bios-configuration.md), you also need to grant access to endpoints in which your tenant currently resides.

To find your tenant location or Azure Scale Unit (ASU), sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Tenant details**. The location is under **Tenant location** as something like North America 0501 or Europe 0202. Look for the matching number in the following table. That row tells you which storage name and CDN endpoints to grant access to. The rows are differentiated by geographic region, as indicated by the first two letters in the names (na = North America, eu = Europe, ap = Asia Pacific). Your tenant location is one of these three regions although your organization's actual geographic location might be elsewhere.

> [!NOTE]
> **Allow HTTP Partial response** is required for Scripts & Win32 Apps endpoints.

|Azure Scale Unit (ASU) | Storage name | CDN | Port |
| --- | --- |------------- | --- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0601<br>AMSUA0701<br>AMSUA0702<br>AMSUA0801<br>AMSUA0901 | naprodimedatapri<br>naprodimedatasec<br>naprodimedatahotfix | naprodimedatapri.azureedge.net<br>naprodimedatasec.azureedge.net<br>naprodimedatahotfix.azureedge.net<br>imeswda-afd-primary.manage.microsoft.com<br>imeswda-afd-secondary.manage.microsoft.com<br>imeswda-afd-hotfix.manage.microsoft.com | **TCP:** 443 |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502<br>AMSUB0601<br>AMSUB0701 | euprodimedatapri<br>euprodimedatasec<br>euprodimedatahotfix | euprodimedatapri.azureedge.net<br>euprodimedatasec.azureedge.net<br>euprodimedatahotfix.azureedge.net<br>imeswdb-afd-primary.manage.microsoft.com<br>imeswdb-afd-secondary.manage.microsoft.com<br>imeswdb-afd-hotfix.manage.microsoft.com | **TCP:** 443 |
| AMSUC0101<br>AMSUC0201<br>AMSUC0301<br>AMSUC0501<br>AMSUC0601<br>AMSUD0101| approdimedatapri<br>approdimedatasec<br>approdimedatahotifx | approdimedatapri.azureedge.net<br>approdimedatasec.azureedge.net<br>approdimedatahotfix.azureedge.net<br>imeswdc-afd-primary.manage.microsoft.com<br>imeswdc-afd-secondary.manage.microsoft.com<br>imeswdc-afd-hotfix.manage.microsoft.com |**TCP:** 443 |

## Network requirements for macOS app and script deployments

If you're using Intune to deploy apps or scripts on macOS, you also need to grant access to endpoints in which your tenant currently resides.

To find your tenant location or Azure Scale Unit (ASU), sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Tenant details**. The location is under Tenant location as something like North America 0501 or Europe 0202. Look for the matching number in the following table. That row tells you which storage name and CDN endpoints to grant access to. The rows are differentiated by geographic region, as indicated by the first two letters in the names (na = North America, eu = Europe, ap = Asia Pacific). Your tenant location is one of these three regions although your organization's actual geographic location might be elsewhere.

|Azure Scale Unit (ASU) | CDN | Port |
| --- |------------- | --- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0601<br>AMSUA0701<br>AMSUA0702<br>AMSUA0801<br>AMSUA0901 | macsidecar.manage.microsoft.com<br>macsidecarprod.azureedge.net (azureedge.net domains will be disabled after 3/31/2025) | **TCP:** 443 |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502<br>AMSUB0601<br>AMSUB0701 | macsidecareu.manage.microsoft.com<br>macsidecarprodeu.azureedge.net (azureedge.net domains will be disabled after 3/31/2025) | **TCP:** 443 |
| AMSUC0101<br>AMSUC0201<br>AMSUC0301<br>AMSUC0501<br>AMSUC0601<br>AMSUD0101| macsidecarap.manage.microsoft.com<br>macsidecarprodap.azureedge.net (azureedge.net domains will be disabled after 3/31/2025) |**TCP:** 443 |

## Microsoft Store

Managed Windows devices using the Microsoft Store – either to acquire, install, or update apps – need access to these endpoints.

**Microsoft Store API (AppInstallManager):**

- displaycatalog.mp.microsoft.com
- purchase.md.mp.microsoft.com
- licensing.mp.microsoft.com
- storeedgefd.dsx.mp.microsoft.com

**Windows Update Agent:**

For details, see the following resources:

- [Manage connection endpoints for Windows 11 Enterprise](/windows/privacy/manage-windows-11-endpoints)
- [Manage connection endpoints for Windows 10 Enterprise, version 21H2](/windows/privacy/manage-windows-21h2-endpoints)

**Win32 content download:**

Win32 content download locations and endpoints are unique per application and are provided by the external publisher. You can find the location for each Win32 Store app using the following command on a test system (you can obtain the [PackageId] for a Store app by referencing the **Package Identifier** property of the app after adding it to Microsoft Intune):

`winget show [PackageId]`

The **Installer Url** property either shows the external download location or the region-based (Microsoft-hosted) fallback cache based on whether the cache is in-use. Note that the content download location can change between the cache and external location.

**Microsoft-hosted Win32 app fallback cache:**

- Varies by region, example: *sparkcdneus2.azureedge.net, sparkcdnwus2.azureedge.net*

**Delivery Optimization (optional, required for peering):**

For details, see the following resource:

- [Microsoft Connected Cache content and services endpoints](/windows/deployment/do/delivery-optimization-endpoints)

## Migrating device health attestation compliance policies to Microsoft Azure attestation

If a customer enables any of the Windows 10/11 Compliance policy - Device Health settings, then Windows 11 devices will begin to use a Microsoft Azure Attestation (MAA) service based on their Intune tenant location.
However, Windows 10 and GCCH/DOD environments will continue to use the existing Device Health Attestation DHA endpoint 'has.spserv.microsoft.com' for device health attestation reporting and isn't impacted by this change.  

If a customer has firewall policies that prevent access to the new Intune MAA service for Windows 11, then Windows 11 devices with assigned compliance policies using any of the device health settings (BitLocker, Secure Boot, Code Integrity) will fall out of compliance as they're unable to reach the MAA attestation endpoints for their location.

Ensure that there are no firewall rules blocking outbound HTTPS/443 traffic, and that SSL Traffic inspection isn't in place for the endpoints listed in this section, based on your Intune tenant's location.

To find your tenant location navigate to the Intune admin center > **Tenant administration** > **Tenant status** > **Tenant details**, see Tenant location.

# [North America](#tab/north-america)

- 'https://intunemaape1.eus.attest.azure.net'

- 'https://intunemaape2.eus2.attest.azure.net'

- 'https://intunemaape3.cus.attest.azure.net'

- 'https://intunemaape4.wus.attest.azure.net'

- 'https://intunemaape5.scus.attest.azure.net'

- 'https://intunemaape6.ncus.attest.azure.net'

# [Europe](#tab/europe)

- 'https://intunemaape7.neu.attest.azure.net'

- 'https://intunemaape8.neu.attest.azure.net'

- 'https://intunemaape9.neu.attest.azure.net'

- 'https://intunemaape10.weu.attest.azure.net'

- 'https://intunemaape11.weu.attest.azure.net'

- 'https://intunemaape12.weu.attest.azure.net'

# [Asia Pacific](#tab/asia-pacific)

- 'https://intunemaape13.jpe.attest.azure.net'

- 'https://intunemaape17.jpe.attest.azure.net'

- 'https://intunemaape18.jpe.attest.azure.net'

- 'https://intunemaape19.jpe.attest.azure.net'

---

## Windows Update for Business deployment service

For more information on the required endpoints for Windows Update for Business deployment service, see [Windows Update for Business deployment service prerequisites](/windows/deployment/update/deployment-service-prerequisites#required-endpoints).

## Endpoint analytics

For more information on the required endpoints for Endpoint analytics, see [Endpoint analytics proxy configuration](../../analytics/troubleshoot.md#bkmk_endpoints).

## Microsoft Defender for Endpoint

For more information about configuring Defender for Endpoint connectivity, see [Connectivity Requirements](../protect/mde-security-integration.md#connectivity-requirements).

To support Defender for Endpoint security settings management, allow the following hostnames through your firewall.
For communication between clients and the cloud service:

- \*.dm.microsoft.com - The use of a wildcard supports the cloud-service endpoints that are used for enrollment, check-in, and reporting, and which can change as the service scales.

  > [!IMPORTANT]
  > SSL Inspection is not supported on endpoints required for Microsoft Defender for Endpoint.

## Microsoft Intune Endpoint Privilege Management

To support Endpoint Privilege Management, allow the following hostnames on tcp port 443 through your firewall 

For communication between clients and the cloud service:

- \*.dm.microsoft.com - The use of a wildcard supports the cloud-service endpoints that are used for enrollment, check-in, and reporting, and which can change as the service scales.
- \*.events.data.microsoft.com - Used by Intune-managed devices to send [optional reporting data](../protect/epm-data-collection.md) to the Intune data collection endpoint.

  > [!IMPORTANT]
  > SSL Inspection is not supported on endpoints required for Endpoint Privilege Management.

For more information, see the [Overview of Endpoint Privilege Management](../protect/epm-overview.md).

## Related topics

[Office 365 URLs and IP address ranges](/microsoft-365/enterprise/urls-and-ip-address-ranges)

[Microsoft 365 network connectivity overview](https://support.office.com/article/client-connectivity-4232abcf-4ae5-43aa-bfa1-9a078a99c78b)

[Content delivery networks (CDNs)](https://support.office.com/article/content-delivery-networks-0140f704-6614-49bb-aa6c-89b75dcd7f1f)

[Other endpoints not included in the Office 365 IP Address and URL Web service](/microsoft-365/enterprise/additional-office365-ip-addresses-and-urls)

[Managing Office 365 endpoints](/microsoft-365/enterprise/managing-office-365-endpoints)

