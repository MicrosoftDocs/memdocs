---
# required metadata

title:  Windows 10 Delivery Optimization settings for Intune 
titleSuffix: Microsoft Intune
description: Delivery Optimization settings for Windows 10 devices that you can deploy using Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/05/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier3
- M365-identity-device-management
---

# Delivery Optimization settings for Windows devices in Intune

Applies to:  
- Windows 10
- Windows 11

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

This article lists some of the settings for Delivery Optimization that Intune supports for devices that run Windows 10 or later.  

Most options in the Microsoft Intune admin center directly map to Delivery Optimization settings that are covered in-depth in the Windows documentation. These options include links to relevant content.  Settings or options that are specific to Intune don't contain links to additional content.  

The following tables include:  

- **Setting**: The setting as it appears in Intune. Settings that are links open the relevant entry in [Configure Delivery Optimization for Windows updates](/windows/deployment/update/waas-delivery-optimization) in the Windows documentation where you can learn more about the setting.

- **Windows version**: The minimum version of Windows that includes support for this setting.

- **Details**: A brief description of how Intune implements the setting, including the Intune default. When available, there are links to [Delivery Optimization Policy configuration service provider](/windows/client-management/mdm/policy-csp-deliveryoptimization) (CSP) entries.  

To configure Intune to use these settings, see [Deliver updates](delivery-optimization-windows.md).  

## Before you begin

[Create a Windows Delivery Optimization profile](delivery-optimization-windows.md).

## Delivery Optimization  

|Setting  |Windows version  |Details  |
|---------|-----------------|---------|
| [Download mode](/windows/deployment/update/waas-delivery-optimization-reference#download-mode)     | 1511         | Specify the download method that Delivery Optimization uses to download content.<br><ul><li>**Not configured**: End users update their devices using their own methods, which may be to use the *Windows Updates or Delivery Optimization* settings available with the operating system. </li> <li> **HTTP only, no peering (0)**: Get updates only from the internet. Don't get updates from other computers on your network (peer-to-peer). </li> <li> **HTTP blended with peering behind the same NAT (1)**: Get updates from the internet and from other computers on your network that are behind the same Network Address Translation (NAT) IP addresses. </li> <li> **HTTP blended with peering across a private group (2)**: Peering occurs on devices in the same Active Directory Site (if it exists) or the same domain. When this option is selected, peering crosses your NAT IP addresses. </li> <li> **HTTP blended with Internet peering (3)**: Get updates from the internet and from other computers on your network. </li> <li> **Simple download mode with no peering (99)**: Gets updates from the internet, directly from the update owner, such as Microsoft. It doesn't contact the Delivery Optimization cloud services. </li> <li> **Bypass mode (100)**: Use Background Intelligent Transfer Service (BITS) to get updates. Don't use Delivery Optimization. </li></ul> **Default**: Not configured  <br><br> Policy CSP: [DODownloadMode](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dodownloadmode)  <br><br>  |
| [Restrict Peer Selection](/windows/deployment/update/waas-delivery-optimization-reference#select-a-method-to-restrict-peer-selection)          | 1803        | Requires **Download mode** be set to *HTTP blended with peering behind the same NAT (1)* or *HTTP blended with peering across a private group (2)*.<br/><br/>Restricts peer selection to a specific group of devices.<br/><br/>**Default**: Not configured <br/><br/>Policy CSP: [DORestrictPeerSelectionBy](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dorestrictpeerselectionby)<br><br>      |
| [Group ID source](/windows/deployment/update/waas-delivery-optimization-reference#select-the-source-of-group-ids)     | 1803        | Requires **Download mode** be set to *HTTP blended with peering across a private group*.<br><br>Restricts peer selection to a specific group of devices by source.<br><br>If you select **Custom**, you then configure **Group ID (as GUID)**. Use a GUID as the Group ID if you need to create a single group for Local Network Peering for branches that are on different domains or aren't on the same LAN.<br><br>**Default**: Not configured <br><br>Policy CSP: [DOGroupId](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dogroupid)     |

## Bandwidth  

> [!NOTE]
> **DOMaxDownloadBandwidth** and **DOMaxUploadBandwidth** are [deprecated](/windows/deployment/deploy-whats-new#delivery-optimization) with the Windows 10, version 2004 release. Instead, use **DO Max Foreground Download Bandwidth** and **DO Max Background Download Bandwidth** that can be configured through the Intune [settings catalog](settings-catalog.md).

|Setting  |Windows version  |Details  |
|---------|---------|---------|
|Bandwidth optimization type     | *See details*        | Select how Intune determines the maximum bandwidth that Delivery Optimization can use across all concurrent download activities.<br><br>Options include:<br><ul><li>**Not configured**</li><br><li>**Absolute**– Specify the [Maximum download bandwidth (in KB/s)](/windows/deployment/update/waas-delivery-optimization-reference#maximum-download-bandwidth) and the [Maximum upload bandwidth (in KB/s)](/windows/deployment/update/waas-delivery-optimization-reference#max-upload-bandwidth) that a device can use across all its concurrent Delivery Optimization downloads activities.<br><br>Requires Windows 1607<br><br>Policy CSP: [DOMaxDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-domaxdownloadbandwidth) and [DOMaxUploadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-domaxuploadbandwidth)</li><br><li>**Percent** – Specify the [Maximum foreground download bandwidth (in %)](/windows/deployment/update/waas-delivery-optimization-reference#maximum-foreground-download-bandwidth) and [Maximum background download bandwidth (in %)](/windows/deployment/update/waas-delivery-optimization-reference#maximum-foreground-download-bandwidth) that a device can use across all its concurrent Delivery Optimization downloads activities.<br><br>Requires Windows 1803<br><br>Policy CSP: [DOPercentageMaxForegroundBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dopercentagemaxforegroundbandwidth) and [DOPercentageMaxBackgroundBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dopercentagemaxbackgroundbandwidth)    <br><br><li>**Percent with business hours** – For a maximum [foreground](/windows/deployment/update/waas-delivery-optimization-reference#set-business-hours-to-limit-foreground-download-bandwidth) download bandwidth, and a maximum [background](/windows/deployment/update/waas-delivery-optimization-reference#set-business-hours-to-limit-background-download-bandwidth) download bandwidth, configure business hours start and end times, and then the percentage of bandwidth to use during and outside your business hours. <br><br>Requires Windows 1803 <br><br>Policy CSP: [DOSetHoursToLimitBackgroundDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dosethourstolimitbackgrounddownloadbandwidth) and [DOSetHoursToLimitForegroundDownloadBandwidth](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dosethourstolimitforegrounddownloadbandwidth)<br><br>   |
|[Delay background HTTP download (in seconds)](/windows/deployment/update/waas-delivery-optimization-reference#delay-background-download-from-http-in-secs) | 1803        | Use this setting to configure a maximum time to delay a background download of content over HTTP. This configuration applies only to downloads that support a peer-to-peer download source. During this delay, the device searches for a peer with the content available. While waiting for a peer source, the download appears to be stuck for the end user.   <br><br>**Default**:  *No value is configured*  <br><br>**Recommended**: 60 seconds   <br><br>Policy CSP: [DODelayBackgroundDownloadFromHttp](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dodelaybackgrounddownloadfromhttp) <br><br>    |
| [Delay foreground HTTP download (in seconds)](/windows/deployment/update/waas-delivery-optimization-reference#delay-foreground-download-from-http-in-secs)      | 1803       | Configure a maximum time to delay a foreground (interactive) download of content over HTTP. This configuration applies only to downloads that support a peer-to-peer download source. During this delay, the device searches for a peer with the content available. While waiting for a peer source, the download appears to be stuck for the end user.   <br><br>**Default**:  *No value is configured*  <br><br>**Recommended**: 60 seconds   <br><br>Policy CSP:  [DODelayForegroundDownloadFromHttp](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dodelayforegrounddownloadfromhttp) <br><br>         |


## Caching  

|Setting  |Windows version  |Details  |
|---------|---------|---------|
|[Minimum RAM required for peer caching (in GB)](/windows/deployment/update/waas-delivery-optimization-reference#minimum-ram-inclusive-allowed-to-use-peer-caching)      | 1709        | Specify the minimum RAM size in GBs that a device must have to use peer caching. <br><br>**Default**:   *No value is configured*  <br><br>**Recommended**: 4 GB <br><br>Policy CSP: [DOMinRAMAllowedToPeer](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dominramallowedtopeer) <br><br>        |
|[Minimum disk size required for peer caching (in GB)](/windows/deployment/update/waas-delivery-optimization-reference#minimum-disk-size-allowed-to-use-peer-caching)      | 1709        | Specify the minimum disk size in GBs that a device must have to use peer caching. <br><br>**Default**:  *No value is configured*  <br><br>**Recommended**: 32 GB   <br><br>Policy CSP: [DOMinDiskSizeAllowedToPeer](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-domindisksizeallowedtopeer) <br><br>    |
|[Minimum content file size for peer caching (in MB)](/windows/deployment/update/waas-delivery-optimization-reference#minimum-peer-caching-content-file-size)      | 1709        | Specify the minimum size in MB that a file must meet or exceeded to use peer caching.  <br><br>**Default**:  *No value is configured*  <br><br>**Recommended**: 10 MB   <br><br>Policy CSP: [DOMinFileSizeToCache](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dominfilesizetocache)  <br><br>      |
|[Minimum battery level required to upload (in %)](/windows/deployment/update/waas-delivery-optimization-reference#allow-uploads-while-the-device-is-on-battery-while-under-set-battery-level)      | 1709        | Specify as a percent, the minimum battery level that a device must have to upload data to peers. If the battery level drops to the specified value, any active uploads automatically pause.   <br><br>**Default**:  *No value is configured*  <br><br>**Recommended**:  40%   <br><br>Policy CSP: [DOMinBatteryPercentageAllowedToUpload](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dominbatterypercentageallowedtoupload) <br><br>        |
|[Modify cache drive](/windows/deployment/update/waas-delivery-optimization-reference#modify-cache-drive)        | 1607        | Specify the drive that Delivery Optimization uses for its cache. You can use an environment variable, drive letter, or a full path.  <br><br>**Default**:  %SystemDrive% <br><br>Policy CSP:  [DOModifyCacheDrive](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-domodifycachedrive) <br><br>        |
| [Maximum cache age (in days)](/windows/deployment/update/waas-delivery-optimization-reference#max-cache-age)    | 1511         | Specify for how long after each file successfully downloads that the file is held in the Delivery Optimization cache on a device.   <br><br>With Intune, you configure the cache age in days. The number of days you define is converted into the applicable number of seconds, which is how Windows defines this setting. For example, an Intune configuration of 3 days is converted on the device to 259200 seconds (3 days).  <br><br>**Default**:   *No value is configured*     <br><br>**Recommended**: 7   <br><br>Policy CSP: [DOMaxCacheAge](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-domaxcacheage)  <br><br>          |
| Maximum cache size type  | *See details*    | Select how to manage the amount of disk space on a device that is used by Delivery Optimization. When not configured, cache size defaults to 20% of the free disk space available.  <br><ul><li>**Not configured** (Default)</li><br><li>**Absolute** – Specify the [Absolute maximum cache size (in GB)](/windows/deployment/update/waas-delivery-optimization-reference#absolute-max-cache-size) to configure the maximum amount of drive space a device can use for Delivery Optimization. When set to 0 (zero), the cache size is unlimited, although Delivery Optimization will clear the cache when the device is low on disk space. <br><br>Requires Windows 1607<br><br> Policy CSP: [DOAbsoluteMaxCacheSize](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-doabsolutemaxcachesize) </li><br><li>**Percentage** – Specify the [Maximum cache size (in %)](/windows/deployment/update/waas-delivery-optimization-reference#max-cache-size) to configure the maximum amount of drive space a device can use for Delivery Optimization. The percentage is of the available drive space, and Delivery Optimization constantly assesses the available drive space and will clear the cache to keep the maximum cache size under the set percentage. <br><br>Requires Windows 1511<br><br>Policy CSP: [DOMaxCacheSize](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-domaxcachesize)  |
| [VPN peer caching](/windows/deployment/update/waas-delivery-optimization-reference#enable-peer-caching-while-the-device-connects-via-vpn)  | 1709  | Select **Enabled** to configure a device to participate in Peer Caching while connected by VPN to the domain network. Devices that are enabled can download from or upload to other domain network devices, either on VPN or on the corporate domain network.  <br><br>**Default**: Not configured  <br><br>Policy CSP: [DOAllowVPNPeerCaching](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-domaxcacheage)    |

## Local Server Caching  

|Setting  |Windows version  |Details  |
|---------|-----------------|---------|
|Cache server host names | 1809  |Specify the IP address or FQDN of Network Cache servers that will be used by your devices for Delivery Optimization, and then select **Add** to add that entry to the list.  <br><br>**Default**: Not configured  <br><br>Policy CSP: [DOCacheHost](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-docachehost)  |
|[Delay foreground download Cache Server fallback (in seconds)](/windows/deployment/update/waas-delivery-optimization-reference#delay-foreground-download-cache-server-fallback-in-secs) | 1903    |Specify a time in seconds (0-2592000) to delay the fallback from a Cache server to the HTTP source for a foreground content download. When the [Bandwidth](#bandwidth) setting for *Delay background HTTP download (in seconds)* is configured, that setting applies first to allow downloads from peers. (0-2592000).   <br><br>**Default**: 0  <br><br>Policy CSP [DODelayCacheServerFallbackForeground](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dodelaycacheserverfallbackforeground)  |
|[Delay background download Cache Server fallback (in seconds)](/windows/deployment/update/waas-delivery-optimization-reference#delay-background-download-cache-server-fallback-in-secs) | 1903    |Specify a time in seconds (0-2592000) to delay the fallback from a Cache server to the HTTP source for a background content download. When the [Bandwidth](#bandwidth) setting for *Delay background HTTP download (in seconds)* is configured, that setting applies first to allow downloads from peers.    (0-2592000)   <br><br>**Default**: 0 <br><br>Policy CSP: [DODelayCacheServerFallbackBackground](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-dodelaycacheserverfallbackbackground)  |

> [!NOTE]
> When you install a Microsoft Connected Cache on a Configuration Manager distribution point, cloud-managed devices can use the on-premises cache. As long as the device can communicate with the server, the cache is available to deliver content to these devices. For more information, see [Microsoft Connected Cache in Configuration Manager](../../configmgr/core/plan-design/hierarchy/microsoft-connected-cache.md).<!-- 8827227 -->

## Next steps

[Assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

[Learn more about Delivery Optimization in Intune](delivery-optimization-windows.md).
