---
title: include file
description: include file
author: ErikjeMS  
ms.service: microsoft-intune
ms.topic: include
ms.date: 06/02/2020
ms.author: erikje
ms.custom: include file
---

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