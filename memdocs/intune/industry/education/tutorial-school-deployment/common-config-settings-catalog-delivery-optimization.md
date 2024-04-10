---
title: Common Education Windows Delivery Optimization configuration
description: Learn about common Windows Delivery Optimization configuration used by Education organizations in Intune.
ms.date: 4/9/2024
ms.topic: windows-deliveryoptimization
author: yegor-a
ms.author: egorabr
---

# Delivery Optimization

Windows updates, upgrades, and applications can contain packages with large files. Downloading and distributing updates can consume quite a bit of network resources on the devices receiving them.

Delivery Optimization is a reliable HTTP downloader with a cloud-managed solution that allows Windows devices to download those packages from peers on the same network.

#### Additional information

- [Delivery Optimization reference](/windows/deployment/do/waas-delivery-optimization-reference)
- [YouTube: Delivery Optimization](https://www.youtube.com/playlist?list=PLMuDtq95SdKtN9lntgTcuhsYCsSQR4Dyl)

## Settings Catalog Policies

  | **Settings Catalog** | **Value** | **Notes** | **CSP** |
  |---|---|---|---|
  | **DO Delay Background Download From Http** | 3600 | After the max delay has reached, the download will resume using HTTP, either downloading the entire payload or complementing the bytes that couldn't be downloaded from Peers. | [DODelayBackgroundDownloadFromHttp](/windows/client-management/mdm/policy-csp-deliveryoptimization#DODelayBackgroundDownloadFromHttp) |
  | **DO Download Mode** | HTTP blended with peering behind the same NAT. | | [DODownloadMode](/windows/client-management/mdm/policy-csp-deliveryoptimization#DODownloadMode#DODownloadMode) |
  | **DO Max Cache Age** | 1209600 | 14 days in seconds | [DOMaxCacheAge](/windows/client-management/mdm/policy-csp-deliveryoptimization#DOMaxCacheAge) |
  | **DO Min Disk Size Allowed To Peer** | 100 | Specifies the required minimum disk size (capacity in GB) for the device to use Peer Caching. Recommended values: 64 GB to 256 GB.Adjust as necessary according to your hardware. | [DOMinDiskSizeAllowedToPeer](/windows/client-management/mdm/policy-csp-deliveryoptimization#DOMinDiskSizeAllowedToPeer) |
  | **DO Min File Size To Cache** | 5 | | [DOMinFileSizeToCache](/windows/client-management/mdm/policy-csp-deliveryoptimization#DOMinFileSizeToCache) |
  | **DO Min RAM Allowed To Peer** | 2 | | [DOMinRAMAllowedToPeer](/windows/client-management/mdm/policy-csp-deliveryoptimization#DOMinRAMAllowedToPeer) |
  | **DO Restrict Peer selection By** | Subnet mask | | [DORestrictPeerSelectionBy](/windows/client-management/mdm/policy-csp-deliveryoptimization#DORestrictPeerSelectionBy) |
