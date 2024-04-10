---
author: Yusuke Shinoki (HE/HIM)
ms.date: 04/10/2024
---
Delivery Optimization

Windows updates, upgrades, and applications can contain packages with large files. Downloading and distributing updates can consume quite a bit of network resources on the devices receiving them. 

Delivery Optimization is a reliable HTTP downloader with a cloud-managed solution that allows Windows devices to download those packages from peers on the same network.

Additional information:

- [Delivery Optimization reference](https://learn.microsoft.com/windows/deployment/do/waas-delivery-optimization-reference)
- [YouTube: Delivery Optimization](https://www.youtube.com/playlist?list=PLMuDtq95SdKtN9lntgTcuhsYCsSQR4Dyl)

  | **Settings Catalog** | **Value** | **Notes** | **CSP** |
  |---|---|---|---|
  | **DO Delay Background Download From Http** | 3600 | After the max delay has reached, the download will resume using HTTP, either downloading the entire payload or complementing the bytes that couldn't be downloaded from Peers. | [DeliveryOptimization/DODelayBackgroundDownloadFromHttp](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-deliveryoptimization) |
  | **DO Download Mode** | HTTP blended with peering behind the same NAT. | | [DeliveryOptimization/DODownloadMode](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-deliveryoptimization) |
  | **DO Max Cache Age** | 1209600 | | [DeliveryOptimization/DOMaxCacheAge](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-deliveryoptimization) |
  | **DO Min Disk Size Allowed To Peer** | 100 | Specifies the required minimum disk size (capacity in GB) for the device to use Peer Caching.Recommended values: 64 GB to 256 GB.Adjust as necessary according to your hardware. | [DeliveryOptimization/DOMinDiskSizeAllowedToPeer](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-deliveryoptimization) |
  | **DO Min File Size To Cache** | 5 | | [DeliveryOptimization/DOMinFileSizeToCache](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-deliveryoptimization) |
  | **DO Min RAM Allowed To Peer** | 2 | | [DeliveryOptimization/DOMinRAMAllowedToPeer](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-deliveryoptimization) |
  | **DO Restrict Peer selection By** | Subnet mask | | [DeliveryOptimization/DORestrictPeerSelectionBy](https://learn.microsoft.com/windows/client-management/mdm/policy-csp-deliveryoptimization) |

