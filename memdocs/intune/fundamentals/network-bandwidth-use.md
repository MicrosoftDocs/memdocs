---
# required metadata

title: Network requirements and bandwidth details for Microsoft Intune
titleSuffix: Microsoft Intune
description: Review network configuration requirements and bandwidth details for Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/30/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 0f737d48-24bc-44cd-aadd-f0a1d59f6893

# optional metadata
# CustomerIntent: As an  IT admin, I want to gather the network requirements and bandwidth details so that I can understand what is needed for Intune deployments.

#ROBOTS:
#audience:

ms.reviewer: srink
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.collection:
- tier2
- M365-identity-device-management
---

# Intune network configuration requirements and bandwidth

You can use this information to understand bandwidth requirements for your Intune deployments.

## Average network traffic

This table lists the approximate size and frequency of common content that travels across the network for each client.

> [!NOTE]
> To ensure devices receive the updates and content from Intune, they must periodically connect to the Internet. The time required to receive updates or content can vary, but they should remain continuously connected to the Internet for at least one hour each day.

|Content type|Approximate size|Frequency and details|
|----------------|--------------------|-------------------------|
|Intune client installation<br /><br />**The following requirements are in addition to the Intune client installation**|125 MB|**One time**<br /><br />The size of the client download varies depending on the operating system of the client computer.|
|Client enrollment package|15 MB|**One time**<br /><br />Additional downloads are possible when there are updates for this content type.|
|Endpoint Protection agent|65 MB|**One time**<br /><br />Additional downloads are possible when there are updates for this content type.|
|Operations Manager agent|11 MB|**One time**<br /><br />Additional downloads are possible when there are updates for this content type.|
|Policy agent|3 MB|**One time**<br /><br />Additional downloads are possible when there are updates for this content type.|
|Remote Assistance via Microsoft Easy Assist agent|6 MB|**One time**<br /><br />Additional downloads are possible when there are updates for this content type.|
|Daily client operations|6 MB|**Daily**<br /><br />The Intune client regularly communicates with the Intune service to check for updates and policies, and to report the client's status to the service.|
|Endpoint Protection malware definition updates|Varies<br /><br />Typically 40 KB to 2 MB|**Daily**<br /><br />Up to three times a day.|
|Endpoint Protection engine update|5 MB|**Monthly**|
|Software updates|Varies<br /><br />The size depends on the updates you deploy.|**Monthly**<br /><br />Typically, software updates release on the second Tuesday of each month.<br /><br />A newly enrolled or deployed computer can use more network bandwidth while downloading the full set of previously released updates.|
|Service packs|Varies<br /><br />The size varies for each service pack you deploy.|**Varies**<br /><br />Depends on when you deploy service packs.|
|Software distribution|Varies<br /><br />The size depends on the software you deploy.|**Varies**<br /><br />Depends on when you deploy software.|

## Ways to reduce network bandwidth use

You can use one or more of the following methods to reduce network bandwidth use for Intune clients.

### Use a proxy server to cache content requests

A proxy server can cache content to reduce duplicate downloads and reduce network bandwidth from content from the Internet.

A caching proxy server that receives content requests from clients can retrieve that content and cache both web responses and downloads. The server uses cached data to answer subsequent requests from clients.

The following are typical settings to use for a proxy server that caches content for Intune clients.


|          Setting           |           Recommended value           |                                                                                                  Details                                                                                                  |
|----------------------------|---------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         Cache size         |             5 GB to 30 GB             | The value varies based on the number of client computers in your network and the configurations you use. To prevent files from being deleted too soon, adjust the size of the cache for your environment. |
| Individual cache file size |                950 MB                 |                                                                     This setting might not be available in all caching proxy servers.                                                                     |
|   Object types to cache    | HTTP<br/><br />HTTPS<br/><br/>BITS |                                               Intune packages are CAB files retrieved by Background Intelligent Transfer Service (BITS) download over HTTP.                                               |
> [!NOTE]
> If you use a proxy server to cache content requests, communication is only encrypted between the client and the proxy and from the proxy to Intune. The connection from the client to Intune will not be encrypted end-to-end.

For information about using a proxy server to cache content, see the documentation for your proxy server solution.

### Delivery Optimization

Delivery Optimization lets you use Intune to reduce bandwidth consumption when your Windows 10 devices download applications and updates. Use a self-organizing distributed cache to pull downloads from traditional servers, and alternate sources (like network peers).

To see the full list of Windows 10 versions and content types supported by Delivery Optimization, see the [Delivery Optimization for Windows 10 updates article](/windows/deployment/update/waas-delivery-optimization#requirements).

You can [set up Delivery Optimization](../configuration/delivery-optimization-settings.md) as part of your device configuration profiles.

### Background Intelligent Transfer Service (BITS) and BranchCache

You can use Microsoft Intune to manage Windows PCs either [as mobile devices with mobile device management (MDM)](../enrollment/windows-enroll.md) or as computers with the Intune software client. Microsoft recommends that customers [use the MDM management solution](../enrollment/windows-enroll.md) whenever possible. When managed this way, BranchCache and BITS aren't supported. For more information, see [Compare managing Windows PCs as computers or mobile devices](./intune-legacy-pc-client.md).

#### Use (BITS) on computers (requires Intune software client)

During hours that you configure, you can use BITS on a Windows computer to reduce the network bandwidth. You can configure BITS policy on the **Network bandwidth** page of the Intune Agent policy.

> [!NOTE]
> For MDM management on Windows, only the OS's management interface for the MobileMSI app type uses BITS to download. AppX/MsiX use their own non-BITS download stack and Win32 apps via the Intune agent use Delivery Optimization rather than BITS.

To learn more about BITS and Windows computers, see [Background Intelligent Transfer Service](/windows/win32/bits/background-intelligent-transfer-service-portal) in the TechNet Library.

#### Use BranchCache on computers (requires Intune software client)

Intune clients can use BranchCache to reduce wide area network (WAN) traffic. The following operating systems support BranchCache:

- Windows 7
- Windows 8.0
- Windows 8.1
- Windows 10

To use BranchCache, the client computer must have BranchCache enabled, and then be configured for **distributed cache mode**.

When the Intune client is installed on computers, BranchCache and distributed cache mode are enabled by default. However, if Group Policy has disabled BranchCache, Intune doesn't override that policy and BranchCache remains disabled.

If you use BranchCache, work with other administrators in your organization to manage Group Policy and Intune Firewall policy. Ensure they don't deploy policy that disables BranchCache or Firewall exceptions. For more about BranchCache, see [BranchCache Overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831696(v=ws.11)).

## Next steps

[Review endpoints for Intune](intune-endpoints.md)