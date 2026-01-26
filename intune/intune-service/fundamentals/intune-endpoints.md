---
title: Network endpoints for Microsoft Intune
description: Review endpoints for Intune. This page lists IP addresses and port settings needed for proxy settings in your Intune deployments.
author: brenduns
ms.author: brenduns
ms.date: 08/21/2025
ms.topic: reference
ms.reviewer: angrobe
ms.collection:
- M365-identity-device-management
- highpri
- highseo
---

# Network endpoints for Microsoft Intune

This article lists IP addresses and port settings needed for proxy settings in your Microsoft Intune deployments. A consolidated list is at the end of this page.  [Consolidated endpoint list](#consolidated-endpoint-list)

 > [!CAUTION]
 >
 > The previously available PowerShell scripts for retrieving Microsoft Intune endpoint IP addresses and FQDNs no longer return accurate data from the Office 365 Endpoint service. Instead, use the consolidated list provided in this article. Using the original scripts or endpoint lists from the Office 365 Endpoint service is insufficient and may lead to incorrect configurations.

As a cloud-only service, Intune doesn't require an on-premises infrastructure such as servers or gateways.

## Access for managed devices

To manage devices behind firewalls and proxy servers, you must enable communication for Intune.

> [!NOTE]
> The information in this section also applies to the [Microsoft Intune Certificate Connector](../protect/certificate-connector-prerequisites.md). The connector has the same network requirements as managed devices.

- The endpoints in this article allow access to the ports identified in the following tables.
- For some tasks, Intune requires unauthenticated proxy server access to manage.microsoft.com, *.azureedge.net, and graph.microsoft.com.

  > [!NOTE]
  > SSL traffic inspection isn't supported for '\*.manage.microsoft.com', '\*.dm.microsoft.com', or the [Device Health Attestation (DHA) endpoints listed in the compliance section](#migrating-device-health-attestation-compliance-policies-to-microsoft-azure-attestation).

You can modify proxy server settings on individual client computers. You can also use Group Policy settings to change settings for all client computers located behind a specified proxy server.

Managed devices require configurations that let **All Users** access services through firewalls.

## Endpoints

You also need FQDNs that are covered as part of Microsoft 365 Requirements. For reference, the following tables show the service they're tied to, and the list of URLs returned.

The data columns shown in the tables are:

- **ID**: The ID number of the row, also known as an endpoint set. This ID is the same as is returned by the web service for the endpoint set.

- **Category**: Shows whether the endpoint set is categorized as **Optimize**, **Allow**, or **Default**. This column also lists which endpoint sets are required to have network connectivity. For endpoint sets that aren't required to have network connectivity, we provide notes in this field to indicate what functionality would be missing if the endpoint set is blocked. If you're excluding an entire service area, the endpoint sets listed as required don't require connectivity.

  You can read about these categories and guidance for their management in [New Microsoft 365 endpoint categories](/microsoft-365/enterprise/microsoft-365-network-connectivity-principles?#new-office-365-endpoint-categories).

- **ER**: This is Yes/True if the endpoint set is supported over Azure ExpressRoute with Microsoft 365 route prefixes. The BGP community that includes the route prefixes shown aligns with the service area listed. When ER is No / False, then ExpressRoute isn't supported for this endpoint set.

- **Addresses**: Lists the FQDNs or wildcard domain names and IP address ranges for the endpoint set. Be aware that an IP address range is in CIDR format and might include many individual IP addresses in the specified network.

- **Ports**: Lists the TCP or UDP ports that are combined with listed IP addresses to form the network endpoint. You might notice some duplication in IP address ranges where there are different ports listed.

### Intune core service

> [!NOTE]
> If the firewall that you're using allows you to create firewall rules using a domain name, then use the `*.manage.microsoft.com` and `manage.microsoft.com` domain. However, if the firewall provider that you're using, doesn't allow you to create a firewall rule using a domain name, we recommend that you use the approved list of all subnets in this section.

> [!NOTE]
> Intune endpoints also use *Azure Front Door* for communicating with the Intune service. The IP ranges for Intune (part of Microsoft Security) are added to the following table.  Intune specific endpoints are referenced in the JSON file by the name `AzureFrontDoor.MicrosoftSecurity`. Refer to the Azure Front Door and Service Tags documentation for the complete list of all services that utilize Azure Front Door and instructions for using the JSON file. [Azure Front Door IP Ranges and Service Tags](https://www.microsoft.com/download/details.aspx?id=56519)

| ID | Desc | Category | ER | Addresses | Ports |
|----|------|----------|----|-----------|-------|
| 163 | Intune client and host service| Allow<BR>Required | False | `*.manage.microsoft.com`<BR>`manage.microsoft.com`<BR>`*.dm.microsoft.com`<BR>`EnterpriseEnrollment.manage.microsoft.com`<BR>`104.46.162.96/27, 13.67.13.176/28, 13.67.15.128/27, 13.69.231.128/28, 13.69.67.224/28, 13.70.78.128/28, 13.70.79.128/27, 13.74.111.192/27, 13.77.53.176/28, 13.86.221.176/28,13.89.174.240/28, 13.89.175.192/28, 20.189.229.0/25, 20.191.167.0/25, 20.37.153.0/24, 20.37.192.128/25, 20.38.81.0/24, 20.41.1.0/24, 20.42.1.0/24, 20.42.130.0/24, 20.42.224.128/25, 20.43.129.0/24, 20.44.19.224/27, 40.119.8.128/25, 40.67.121.224/27, 40.70.151.32/28, 40.71.14.96/28, 40.74.25.0/24, 40.78.245.240/28, 40.78.247.128/27, 40.79.197.64/27, 40.79.197.96/28, 40.80.180.208/28, 40.80.180.224/27, 40.80.184.128/25, 40.82.248.224/28, 40.82.249.128/25, 52.150.137.0/25, 52.162.111.96/28, 52.168.116.128/27, 52.182.141.192/27, 52.236.189.96/27, 52.240.244.160/27, 20.204.193.12/30, 20.204.193.10/31, 20.192.174.216/29, 20.192.159.40/29, 104.208.197.64/27, 172.160.217.160/27, 172.201.237.160/27, 172.202.86.192/27, 172.205.63.0/25, 172.212.214.0/25, 172.215.131.0/27, 20.168.189.128/27, 20.199.207.192/28, 20.204.194.128/31, 20.208.149.192/27, 20.208.157.128/27, 20.214.131.176/29, 20.43.129.0/24, 20.91.147.72/29, 4.145.74.224/27, 4.150.254.64/27, 4.154.145.224/27, 4.200.254.32/27, 4.207.244.0/27, 4.213.25.64/27, 4.213.86.128/25, 4.216.205.32/27, 4.237.143.128/25, 40.84.70.128/25, 48.218.252.128/25, 57.151.0.192/27, 57.153.235.0/25, 57.154.140.128/25, 57.154.195.0/25, 57.155.45.128/25, 68.218.134.96/27, 74.224.214.64/27, 74.242.35.0/25, 172.208.170.0/25, 74.241.231.0/25, 74.242.184.128/25`<br><br>`Azure Front Door Endpoints:`<br>` 13.107.219.0/24, 13.107.227.0/24, 13.107.228.0/23, 150.171.97.0/24, 2620:1ec:40::/48, 2620:1ec:49::/48, 2620:1ec:4a::/47` | **TCP:** 80, 443 |
| 172 | MDM Delivery Optimization | Default<BR>Required | False | `*.do.dsp.mp.microsoft.com`<BR> `*.dl.delivery.mp.microsoft.com`<BR> | **TCP:** 80, 443 |
| 170 | MEM - Win32Apps | Default<BR>Required | False | `swda01-mscdn.manage.microsoft.com`<br>`swda02-mscdn.manage.microsoft.com`<br>`swdb01-mscdn.manage.microsoft.com`<br>`swdb02-mscdn.manage.microsoft.com`<br>`swdc01-mscdn.manage.microsoft.com`<br>`swdc02-mscdn.manage.microsoft.com`<br>`swdd01-mscdn.manage.microsoft.com`<br>`swdd02-mscdn.manage.microsoft.com`<br>`swdin01-mscdn.manage.microsoft.com`<BR>`swdin02-mscdn.manage.microsoft.com` | **TCP:** 80, 443 |
| 97 | Consumer Outlook.com, OneDrive, Device authentication, and Microsoft account | Default<BR>Required | False | `account.live.com`<BR>`login.live.com`<BR> | **TCP:** 443 |
| 190 | Endpoint discovery | Default<BR>Required | False | `go.microsoft.com` | **TCP:** 80, 443 |
| 189 | Dependency - Feature Deployment | Default<BR>Required | False |`config.edge.skype.com`<BR>`ecs.office.com`<BR> | **TCP:** 443 |
| 192 | Organizational messages | Default<BR>Required | False | `fd.api.orgmsg.microsoft.com`<BR>`ris.prod.api.personalization.ideas.microsoft.com`<BR>` | **TCP:** 443|

### Authentication dependencies

| ID | Desc | Category | ER | Addresses | Ports |
|----|------|----------|----|-----------|-------|
| 56 | Authentication and Identity, includes Microsoft Entra ID and Entra ID related services.| Allow<BR>Required | True | `login.microsoftonline.com`<BR>`graph.windows.net` | **TCP:** 80, 443 |
| 150 | Office Customization Service provides Office 365 ProPlus deployment configuration, application settings, and cloud based policy management. | Default | False | `*.officeconfig.msocdn.com`<BR>`config.office.com` | **TCP:** 443 |
| 59 | Identity supporting services & CDNs. | Default<BR>Required | False |`enterpriseregistration.windows.net`<BR>`certauth.enterpriseregistration.windows.net` | **TCP:** 80, 443 |

For more information, go to [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

### Intune dependencies

In this section, the following tables list the Intune dependencies and the ports and services that the Intune client accesses.

- [Windows Push Notification Services dependencies](#windows-push-notification-services-wns-dependencies)
- [Delivery optimization dependencies](#delivery-optimization-dependencies)
- [Apple dependencies](#apple-dependencies)
- [Android AOSP dependencies](#android-aosp-dependencies)

#### Android Enterprise dependencies

**Google Android Enterprise** - Google provides documentation of required network ports and destination host names in the [Android Enterprise Help Center](https://support.google.com/work/android/answer/10513641?hl=en).

**Android push notification** - Intune uses Google Firebase Cloud Messaging (FCM) for push notification to trigger device actions and check-ins. Both Android Device Administrator and Android Enterprise require this. For information on FCM network requirements, see Google's [FCM ports and your firewall](https://firebase.google.com/docs/cloud-messaging/).

#### Android AOSP dependencies

| ID  | Desc | Category | ER    | Addresses | Ports |
|-----|------|----------|-------|-----------|-------|
| 179 | MEM - Android AOSP Dependency | Default<BR>Required | False | `intunecdnpeasd.azureedge.net`<BR>`intunecdnpeasd.manage.microsoft.com`<BR>(Starting March 2025, azureedge.net domains will migrate to manage.microsoft.com)<br> | **TCP:** 443 |

> [!NOTE]
> Because Google Mobile Services isn't available in China, devices in China managed by Intune can't use features that require Google Mobile Services. These features include: Google Play Protect capabilities such as Play Integrity Verdict, Managing apps from the Google Play Store, Android Enterprise capabilities (see this [Google documentation](https://support.google.com/work/android/answer/6270910)). Additionally, the Intune Company Portal app for Android uses Google Mobile Services to communicate with the Microsoft Intune service. Because Google Play services isn't available in China, some tasks can require up to 8 hours to finish. For more information, see [Limitations of Intune management when GMS is unavailable](../apps/manage-without-gms.md#limitations-of-intune-management-when-gms-is-unavailable).

**Android port information** - Depending on how you choose to manage Android devices, you might need to open the Google Android Enterprise ports and/or the Android push notification. For more information on Android management methods supported, see the [Android enrollment documentation](deployment-guide-enrollment-android.md).

#### Apple dependencies

For information about Apple specific endpoints, see the following resources:

- [Use Apple products on enterprise networks](https://support.apple.com/HT210060)
- [TCP and UDP ports used by Apple software products](https://support.apple.com/HT202944)
- [About macOS, iOS/iPadOS, and iTunes server host connections and iTunes background processes](https://support.apple.com/HT201999)
- [If your macOS and iOS/iPadOS clients aren't getting Apple push notifications](https://support.apple.com/HT203609)


#### Delivery optimization dependencies

| ID  | Desc | Category | ER    | Addresses | Ports |
|-----|------|----------|-------|-----------|-------|
| 172 | MDM - Delivery Optimization Dependencies | Default<BR>Required | False | `*.do.dsp.mp.microsoft.com`<BR>`*.dl.delivery.mp.microsoft.com`<BR> | **TCP:** 80, 443 |

**Port requirements** - For client-service communication, it uses HTTP or HTTPS over port 80/443. Optionally, for peer-to-peer traffic, Delivery Optimization uses 7680 for TCP/IP and Teredo on port 3544 for NAT traversal. For more information, see [Delivery Optimization documentation](/windows/deployment/do/)

**Proxy requirements** - To use Delivery Optimization, you must allow Byte Range requests. For more information, see [Proxy requirements for Delivery Optimization](/windows/deployment/do/waas-delivery-optimization-faq#what-are-the-requirements-if-i-use-a-proxy).

**Firewall requirements** - Allow the following hostnames through your firewall to support Delivery Optimization. For communication between clients and the Delivery Optimization cloud service:

- `*.do.dsp.mp.microsoft.com`

For Delivery Optimization metadata:

- `*.dl.delivery.mp.microsoft.com`

> [!TIP]
> Review dependencies for client-service peer-to-peer solutions that you use to help ensure support for cloud-based management. For example, Windows BranchCache relies on locally available groups that might not be available through Microsoft Entra ID, which is Intune's identity solution.

#### Windows Push Notification Services (WNS) dependencies

| ID  | Desc | Category | ER    | Addresses | Ports |
|-----|------|----------|-------|-----------|-------|
| 171 | MEM - WNS Dependencies | Default<BR>Required | False | `*.notify.windows.com`<BR>`*.wns.windows.com`<BR>`sinwns1011421.wns.windows.com`<BR>`sin.notify.windows.com`<BR> | **TCP:** 443 |

For Intune-managed Windows devices managed using Mobile Device Management (MDM), device actions and other immediate activities require the use of Windows Push Notification Services (WNS). For more information, see [Allowing Windows Notification traffic through enterprise firewalls](/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config).

### Remote Help

In addition to configuring the network requirements listed in the following table, you need to configure the network requirements for Azure communication services as well. For more information, see [Azure communication services network requirements](/azure/communication-services/concepts/voice-video-calling/network-requirements).

| ID |Desc |Category |ER |Addresses |Ports|Notes|
|----|-----|---------|---|----------|-----|-----|
181 | MEM - Remote Help Feature| Default<BR>Required | False |`*.support.services.microsoft.com`<BR>`remoteassistance.support.services.microsoft.com`<BR>`teams.microsoft.com`<BR>`remoteassistanceprodacs.communication.azure.com`<BR>`edge.skype.com`<BR>`aadcdn.msftauth.net`<BR>`aadcdn.msauth.net`<BR>`alcdn.msauth.net`<BR>`wcpstatic.microsoft.com`<BR>`*.aria.microsoft.com`<BR>`browser.pipe.aria.microsoft.com`<BR>`*.events.data.microsoft.com`<BR>`v10c.events.data.microsoft.com`<BR>`*.monitor.azure.com`<BR>`js.monitor.azure.com`<BR>`edge.microsoft.com`<BR>`*.trouter.communication.microsoft.com`<BR>`*.trouter.teams.microsoft.com`<BR>`api.flightproxy.skype.com`<BR>`ecs.communication.microsoft.com`<BR>`remotehelp.microsoft.com`<BR>`remoteassistanceprodacseu.communication.azure.com`(this endpoint is only for EU customers)<BR> | **TCP:** 443 |
187 | Dependency - Remote Help web pubsub | Default<BR>Required | False | `*.webpubsub.azure.com`<BR> `AMSUA0101-RemoteAssistService-pubsub.webpubsub.azure.com`<BR>| **TCP:** 443 |
188 | Remote Help Dependency for GCC customers| Default<BR>Required | False |`remoteassistanceweb-gcc.usgov.communication.azure.us`<BR>`gcc.remotehelp.microsoft.com`<BR>`gcc.relay.remotehelp.microsoft.com`<BR>`*.gov.teams.microsoft.us` | **TCP:** 443 |

### Windows Autopilot dependencies

| ID | Desc | Category | ER | Addresses | Ports |
|----|------|----------|----|-----------|-------|
| 164 | Windows Autopilot - Windows Update| Default<BR>Required | False | `*.windowsupdate.com`<BR>`*.dl.delivery.mp.microsoft.com`<BR>`*.prod.do.dsp.mp.microsoft.com`<BR>`*.delivery.mp.microsoft.com`<BR>`*.update.microsoft.com`<BR>`tsfe.trafficshaping.dsp.mp.microsoft.com`<BR>`adl.windows.com`<BR> | **TCP:** 80, 443 |
| 165 | Windows Autopilot - NTP Sync | Default<BR>Required | False | `time.windows.com` | **UDP:** 123 |
| 169 | Windows Autopilot - WNS Dependencies| Default<BR>Required | False | `clientconfig.passport.net`<BR>`windowsphone.com`<BR>`*.s-microsoft.com`<BR>`c.s-microsoft.com` | **TCP:** 443 |
| 173 | Windows Autopilot - Third-party deployment dependencies| Default<BR>Required | False | `ekop.intel.com`<BR>`ekcert.spserv.microsoft.com`<BR>`ftpm.amd.com`<BR> | **TCP:** 443 |
| 182 | Windows Autopilot - Diagnostics upload | Default<BR>Required | False | `lgmsapeweu.blob.core.windows.net`<BR>`lgmsapewus2.blob.core.windows.net`<BR>`lgmsapesea.blob.core.windows.net`<BR>`lgmsapeaus.blob.core.windows.net`<BR>`lgmsapeind.blob.core.windows.net`<BR> | **TCP:** 443 |

## Endpoint analytics

For more information on the required endpoints for endpoint analytics, see [Network and connectivity requirements](../../endpoint-analytics/index.md#prerequisites).

## Microsoft Defender for Endpoint

For more information about configuring Defender for Endpoint connectivity, see [Connectivity Requirements](../protect/mde-security-integration.md#connectivity-requirements).

To support Defender for Endpoint security settings management, allow the following hostnames through your firewall.
For communication between clients and the cloud service:

- `*.dm.microsoft.com` - The use of a wildcard supports the cloud-service endpoints that are used for enrollment, check-in, and reporting, and which can change as the service scales.

  > [!IMPORTANT]
  > SSL Inspection isn't supported on endpoints required for Microsoft Defender for Endpoint.

## Microsoft Intune Endpoint Privilege Management

To support Endpoint Privilege Management, allow the following hostnames on tcp port 443 through your firewall

For communication between clients and the cloud service:

- `*.dm.microsoft.com` - The use of a wildcard supports the cloud-service endpoints that are used for enrollment, check-in, and reporting, and which can change as the service scales.
- `*.events.data.microsoft.com` - Used by Intune-managed devices to send [optional reporting data](../protect/epm-data-collection.md) to the Intune data collection endpoint.

  > [!IMPORTANT]
  > SSL Inspection isn't supported on endpoints required for Endpoint Privilege Management.

For more information, see the [Overview of Endpoint Privilege Management](../protect/epm-overview.md).

## Microsoft Security Copilot

To ensure communication between Security Copilot and certain security solutions, you must allow Security Copilot's egress IPs to contact the solution.
For information on the required endpoints, see [Microsoft Security Copilot egress IPs](/copilot/security/plugin-ip-address) in the Security Copilot documentation.

## Microsoft Store

Managed Windows devices that use the Microsoft Store either to acquire, install, or update apps need access to these endpoints on tcp ports 80 and 443 through your firewall.

**Microsoft Store API (AppInstallManager):**

- `displaycatalog.mp.microsoft.com`
- `purchase.md.mp.microsoft.com`
- `licensing.mp.microsoft.com`
- `storeedgefd.dsx.mp.microsoft.com`

 > [!IMPORTANT]
 > SSL Inspection isn't supported on endpoints required for Microsoft Store API.

**Windows Update Agent:**

For details, see the following resources:

- [Manage connection endpoints for Windows 11 Enterprise](/windows/privacy/manage-windows-11-endpoints)
- [Manage connection endpoints for Windows 10 Enterprise, version 21H2](/windows/privacy/manage-windows-21h2-endpoints)

  > [!NOTE]
  > [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

**Win32 content download:**

Win32 content download locations and endpoints are unique per application and are provided by the external publisher. You can find the location for each Win32 Store app using the following command on a test system (you can obtain the [PackageId] for a Store app by referencing the **Package Identifier** property of the app after adding it to Microsoft Intune):

- `winget show [PackageId]`

The **Installer Url** property either shows the external download location or the region-based (Microsoft-hosted) fallback cache based on whether the cache is in-use. The content download location can change between the cache and external location.

**Microsoft-hosted Win32 app fallback cache:**

- `cdn.storeedgefd.dsx.mp.microsoft.com`

**Delivery Optimization (optional, required for peering):**

For details, see the following resource:

- [Microsoft Connected Cache content and services endpoints](/windows/deployment/do/delivery-optimization-endpoints)

## Migrating device health attestation compliance policies to Microsoft Azure attestation

If a customer enables any of the Windows Compliance policy - Device Health settings, then Windows 11 devices begin to use a Microsoft Azure Attestation (MAA) service based on their Intune tenant location.
However, Windows 10 and GCCH/DOD environments continue to use the existing Device Health Attestation DHA endpoint 'has.spserv.microsoft.com' for device health attestation reporting and isn't impacted by this change.

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

## Network requirements for macOS app and script deployments

If you're using Intune to deploy apps or scripts on macOS, you also need to grant access to endpoints in which your tenant currently resides.

Different endpoints are used depending on your tenant location. To find your tenant location, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Tenant details** > **Tenant location** with a value of *North America 0501* or similar. Using the region in the location (North America in *North America 0501*), review the following table for the CDN endpoints and ports required:

|Region | CDN | Port |
|-------|-----|------|
|North America | `macsidecar.manage.microsoft.com`<br>`macsidecarprod.azureedge.net`<br>(Starting March 2025, azureedge.net domains will migrate to manage.microsoft.com) | **TCP:** 443 |
|Europe | `macsidecareu.manage.microsoft.com`<br>`macsidecarprodeu.azureedge.net`<br>(Starting March 2025, azureedge.net domains will migrate to manage.microsoft.com) | **TCP:** 443 |
|Asia Pacific| `macsidecarap.manage.microsoft.com`<br>`macsidecarprodap.azureedge.net`<br>(Starting March 2025, azureedge.net domains will migrate to manage.microsoft.com) |**TCP:** 443 |

## Network requirements for PowerShell scripts and Win32 apps

If you're using Intune for scenarios that use the Intune management extension, like deploying [Win32 apps](../apps/apps-win32-app-management.md), [PowerShell scripts](../apps/powershell-scripts.md), [remediations](../fundamentals/remediations.md), [endpoint analytics](../../endpoint-analytics/index.md), [custom compliance policies](../protect/compliance-use-custom-settings.md) or [BIOS configuration profiles](../configuration/bios-configuration.md), you also need to grant access to endpoints in which your tenant currently resides.

Different endpoints are used depending on your tenant location. To find your tenant location, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Tenant details** > **Tenant location** with a value of *North America 0501* or similar. Using the region in the location (North America in *North America 0501*), review the following table for the CDN endpoints and ports required:

> [!NOTE]
> **Allow HTTP Partial response** is required for Scripts & Win32 Apps endpoints.

|Region | CDN | Port |
|-----|--------------|-----|
| North America | `naprodimedatapri.azureedge.net`<br>`naprodimedatasec.azureedge.net`<br>`naprodimedatahotfix.azureedge.net`<br>`imeswda-afd-primary.manage.microsoft.com`<br>`imeswda-afd-secondary.manage.microsoft.com`<br>`imeswda-afd-hotfix.manage.microsoft.com`<br>(Starting March 2025, azureedge.net domains will migrate to manage.microsoft.com) | **TCP:** 443 |
|Europe | `euprodimedatapri.azureedge.net`<br>`euprodimedatasec.azureedge.net`<br>`euprodimedatahotfix.azureedge.net`<br>`imeswdb-afd-primary.manage.microsoft.com`<br>`imeswdb-afd-secondary.manage.microsoft.com`<br>`imeswdb-afd-hotfix.manage.microsoft.com`<br>(Starting March 2025, azureedge.net domains will migrate to manage.microsoft.com) | **TCP:** 443 |
| Asia Pacific | `approdimedatapri.azureedge.net`<br>`approdimedatasec.azureedge.net`<br>`approdimedatahotfix.azureedge.net`<br>`imeswdc-afd-primary.manage.microsoft.com`<br>`imeswdc-afd-secondary.manage.microsoft.com`<br>`imeswdc-afd-hotfix.manage.microsoft.com`<br>(Starting March 2025, azureedge.net domains will migrate to manage.microsoft.com) | **TCP:** 443 |

For diagnostic data used to monitor the health of the client side components:

- `*.events.data.microsoft.com`

## Windows Autopatch

<a name="windows-update-for-business-deployment-service"></a>

For more information on the required endpoints for Windows Autopatch, see [Windows Autopatch prerequisites](/windows/deployment/windows-autopatch/prepare/windows-autopatch-configure-network#required-microsoft-product-endpoints).

## Azure Front Door Connectivity Diagnostics Tool

To help with validating connectivity to the Azure Front Door (AFD) IP addresses used by Intune, the [Test-IntuneAFDConnectivity.ps1](https://download.microsoft.com/download/52de3524-4108-47e5-acda-5cc820107759/Test-IntuneAFDConnectivity.ps1) script can be used to test connectivity to the required AFD IP address ranges and service endpoints.

This diagnostics tool includes checks for:

- DNS Resolution of Intune service endpoints
- Outbound TCP Connectivity on ports 80 and 443 to AFD IP addresses
- HTTPS validation to the Intune cloud service

### Prerequisites

Before running the script, ensure you have:

- PowerShell 5.1 or later
- Connectivity to Network endpoints for Microsoft Intune, as defined in this article.
  
### Usage

Run the script from an Intune-managed device to test connectivity to the Intune network endpoints using Azure Front Door. The script can be run in the context of the logged-on user or as the Local System account (Device context).

#### Script Execution

**Option 1: Run as Current User**

Open **PowerShell** as the current user, navigate to the directory containing the script and run with the following command: 

```powershell
.\Test-IntuneAFDConnectivity.ps1
```

**Option 2: Run as System (Device Context)**

To test connectivity as the device itself, use [PsExec](/sysinternals/downloads/psexec) from [Microsoft Sysinternals](/sysinternals/downloads/pstools).

1. Download [PsExec](/sysinternals/downloads/psexec)

2. Open a **PowerShell** as an Administrator. Navigate to the directory containing **PsExec**.

3. Run the following command to run the script as SYSTEM:

```powershell
.\psexec.exe -accepteula -i -s powershell.exe
```

1. In the new PowerShell window, navigate to the directory containing the script and run with the following command:

```powershell
.\Test-IntuneAFDConnectivity.ps1
```

### Options and Commands

Use the following options based on your environment:

|Cloud|Command|Notes|
| -------- | -------- | -------- |
|Public Cloud (Default)|`.\Test-IntuneAFDConnectivity.ps1`|Tests connectivity to Public Cloud environments|
|Government Cloud|`.\Test-IntuneAFDConnectivity.ps1 -CloudType gov`|Tests connectivity to US Government, GCC High, and DoD environments|
|Export Results with Detailed Logging|`.\Test-IntuneAFDConnectivity.ps1 -LogLevel Detailed -OutputPath "C:\Logs" -Verbose`|Runs tests with detailed logging and saves results to the specified output directory|

### Troubleshooting

If the script reports a failure (Exit Code 1):

- **If the Azure Front Door IP Address tests show failed IPs or IP ranges:** Your firewall, proxy, or VPN may be blocking outbound connections on ports **443** or **80** to those Azure Front Door IPs.

- **If the Service Endpoint test shows “HTTPS endpoint unreachable”:** The required Intune service FQDNs or Azure Front Door IPs may not be reachable, or a DNS, proxy, or HTTPS inspection issue is preventing connection to the Intune service FQDN.

- **Review the network endpoints for Microsoft Intune** (as detailed in this article) and ensure your firewall, VPN, or proxy allows all required Intune service FQDNs, Azure Front Door IP ranges, and ports.

- **Check detailed results** in the saved output file, or run the script with detailed logging (-LogLevel Detailed and -Verbose) to capture more diagnostic information.

## Consolidated Endpoint List

To make it easier to configure services through firewalls, the following is a consolidated list of the FQDNs and IP Subnets used by Intune managed devices. 

These lists include only those endpoints that that are used by Intune managed devices. These lists do not include additional endpoints that were provided by the Office 365 Endpoint service but not used by Intune.

FQDNs
```
*.manage.microsoft.com
manage.microsoft.com
*.dl.delivery.mp.microsoft.com
*.do.dsp.mp.microsoft.com
*.update.microsoft.com
*.windowsupdate.com
adl.windows.com
dl.delivery.mp.microsoft.com
tsfe.trafficshaping.dsp.mp.microsoft.com
time.windows.com
*.s-microsoft.com
clientconfig.passport.net
windowsphone.com
approdimedatahotfix.azureedge.net
approdimedatapri.azureedge.net
approdimedatasec.azureedge.net
euprodimedatahotfix.azureedge.net
euprodimedatapri.azureedge.net
euprodimedatasec.azureedge.net
naprodimedatahotfix.azureedge.net
naprodimedatapri.azureedge.net
naprodimedatasec.azureedge.net
swda01-mscdn.azureedge.net
swda02-mscdn.azureedge.net
swdb01-mscdn.azureedge.net
swdb02-mscdn.azureedge.net
swdc01-mscdn.azureedge.net
swdc02-mscdn.azureedge.net
swdd01-mscdn.azureedge.net
swdd02-mscdn.azureedge.net
swdin01-mscdn.azureedge.net
swdin02-mscdn.azureedge.net
*.notify.windows.com
*.wns.windows.com
ekcert.spserv.microsoft.com
ekop.intel.com
ftpm.amd.com
intunecdnpeasd.azureedge.net
*.monitor.azure.com
*.support.services.microsoft.com
*.trouter.communication.microsoft.com
*.trouter.skype.com
*.trouter.teams.microsoft.com
api.flightproxy.skype.com
ecs.communication.microsoft.com
edge.microsoft.com
edge.skype.com
remoteassistanceprodacs.communication.azure.com
remoteassistanceprodacseu.communication.azure.com
remotehelp.microsoft.com
wcpstatic.microsoft.com
lgmsapeweu.blob.core.windows.net
intunemaape1.eus.attest.azure.net
intunemaape10.weu.attest.azure.net
intunemaape11.weu.attest.azure.net
intunemaape12.weu.attest.azure.net
intunemaape13.jpe.attest.azure.net
intunemaape17.jpe.attest.azure.net
intunemaape18.jpe.attest.azure.net
intunemaape19.jpe.attest.azure.net
intunemaape2.eus2.attest.azure.net
intunemaape3.cus.attest.azure.net
intunemaape4.wus.attest.azure.net
intunemaape5.scus.attest.azure.net
intunemaape7.neu.attest.azure.net
intunemaape8.neu.attest.azure.net
intunemaape9.neu.attest.azure.net
*.webpubsub.azure.com
*.gov.teams.microsoft.us
remoteassistanceweb.usgov.communication.azure.us
config.edge.skype.com
contentauthassetscdn-prod.azureedge.net
contentauthassetscdn-prodeur.azureedge.net
contentauthrafcontentcdn-prod.azureedge.net
contentauthrafcontentcdn-prodeur.azureedge.net
fd.api.orgmsg.microsoft.com
ris.prod.api.personalization.ideas.microsoft.com

```

IP Subnets
```
4.145.74.224/27
4.150.254.64/27
4.154.145.224/27
4.200.254.32/27
4.207.244.0/27
4.213.25.64/27
4.213.86.128/25
4.216.205.32/27
4.237.143.128/25
13.67.13.176/28
13.67.15.128/27
13.69.67.224/28
13.69.231.128/28
13.70.78.128/28
13.70.79.128/27
13.74.111.192/27
13.77.53.176/28
13.86.221.176/28
13.89.174.240/28
13.89.175.192/28
20.37.153.0/24
20.37.192.128/25
20.38.81.0/24
20.41.1.0/24
20.42.1.0/24
20.42.130.0/24
20.42.224.128/25
20.43.129.0/24
20.44.19.224/27
20.91.147.72/29
20.168.189.128/27
20.189.172.160/27
20.189.229.0/25
20.191.167.0/25
20.192.159.40/29
20.192.174.216/29
20.199.207.192/28
20.204.193.10/31
20.204.193.12/30
20.204.194.128/31
20.208.149.192/27
20.208.157.128/27
20.214.131.176/29
40.67.121.224/27
40.70.151.32/28
40.71.14.96/28
40.74.25.0/24
40.78.245.240/28
40.78.247.128/27
40.79.197.64/27
40.79.197.96/28
40.80.180.208/28
40.80.180.224/27
40.80.184.128/25
40.82.248.224/28
40.82.249.128/25
40.84.70.128/25
40.119.8.128/25
48.218.252.128/25
52.150.137.0/25
52.162.111.96/28
52.168.116.128/27
52.182.141.192/27
52.236.189.96/27
52.240.244.160/27
57.151.0.192/27
57.153.235.0/25
57.154.140.128/25
57.154.195.0/25
57.155.45.128/25
68.218.134.96/27
74.224.214.64/27
74.242.35.0/25
104.46.162.96/27
104.208.197.64/27
172.160.217.160/27
172.201.237.160/27
172.202.86.192/27
172.205.63.0/25
172.212.214.0/25
172.215.131.0/27
13.107.219.0/24
13.107.227.0/24
13.107.228.0/23
150.171.97.0/24
2620:1ec:40::/48
2620:1ec:49::/48
2620:1ec:4a::/47
```


## Related content

[Office 365 URLs and IP address ranges](/microsoft-365/enterprise/urls-and-ip-address-ranges)

[Microsoft 365 network connectivity overview](https://support.office.com/article/client-connectivity-4232abcf-4ae5-43aa-bfa1-9a078a99c78b)

[Content delivery networks (CDNs)](https://support.office.com/article/content-delivery-networks-0140f704-6614-49bb-aa6c-89b75dcd7f1f)

[Other endpoints not included in the Office 365 IP Address and URL Web service](/microsoft-365/enterprise/additional-office365-ip-addresses-and-urls)

[Managing Office 365 endpoints](/microsoft-365/enterprise/managing-office-365-endpoints)

<!-- Older table. Will be removed soon after all the other new tables are finalized. This table is for reference only
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
|devicelistenerprod.microsoft.com| Windows Autopatch |
|devicelistenerprod.eudb.microsoft.com| Windows Autopatch |
|login.windows.net| Windows Autopatch |
|payloadprod*.blob.core.windows.net| Windows Autopatch |
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
|ekcert.spserv.microsoft.com| Windows Autopilot Self-deploy |
|ekop.intel.com| Windows Autopilot Self-deploy |
|ftpm.amd.com| Windows Autopilot Self-deploy |
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
|config.edge.skype.com | Feature Deployment |
|go.microsoft.com | Endpoint discovery |


The following tables list the ports and services that the Intune client accesses:

|Domains    |IP address      |
|-----------|----------------|
| login.microsoftonline.com <br> *.officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net <br> enterpriseregistration.windows.net | More information [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) |
|*.manage.microsoft.com <br> manage.microsoft.com <br>|104.46.162.96/27<br>13.67.13.176/28<br>13.67.15.128/27<br>13.69.231.128/28<br>13.69.67.224/28<br>13.70.78.128/28<br>13.70.79.128/27<br>13.74.111.192/27<br>13.77.53.176/28<br>13.86.221.176/28<br>13.89.174.240/28<br>13.89.175.192/28<br>20.189.172.160/27<br>20.189.229.0/25<br>20.191.167.0/25<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>20.44.19.224/27<br>20.192.174.216/29<br>20.192.159.40/29<br>20.204.193.12/30<br>20.204.193.10/31<br>40.119.8.128/25<br>40.67.121.224/27<br>40.70.151.32/28<br>40.71.14.96/28<br>40.74.25.0/24<br>40.78.245.240/28<br>40.78.247.128/27<br>40.79.197.64/27<br>40.79.197.96/28<br>40.80.180.208/28<br>40.80.180.224/27<br>40.80.184.128/25<br>40.82.248.224/28<br>40.82.249.128/25<br>52.150.137.0/25<br>52.162.111.96/28<br>52.168.116.128/27<br>52.182.141.192/27<br>52.236.189.96/27<br>52.240.244.160/27|
-->
