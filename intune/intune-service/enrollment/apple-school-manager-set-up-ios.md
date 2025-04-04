---
# required metadata

title: Apple School Manager Program enrollment for iOS/iPadOS devices
titleSuffix: Microsoft Intune
description: Learn how to set up Microsoft Intune with Apple School Manager for corporate-owned iOS/iPadOS devices. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/06/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 4c35a23e-0c61-11e8-ba89-0ed5f89f718b

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
---

# Set up iOS/iPadOS device enrollment with Apple School Manager

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Set up Microsoft Intune to enroll iOS/iPadOS devices purchased through [Apple School Manager](https://school.apple.com/). Using Intune with Apple School Manager, you can enroll large numbers of iOS/iPadOS devices without ever touching them. When a student or teacher turns on the device, Apple Setup Assistant runs with preconfigured settings and the device enrolls into management. 


## Prerequisites  

To enable Apple School Manager enrollment, you use both the Microsoft Intune admin center and Apple School Manager portal. You need a list of serial numbers or a purchase order number so that you can assign devices to Intune.  

- Get an [Apple mobile device management (MDM) push certificate](apple-mdm-push-certificate-get.md).  
- Set up the [MDM Authority](../fundamentals/mdm-authority-set.md).  
- If using Active Directory Federation Services (AD FS), user affinity requires [WS-Trust 1.3 Username/Mixed endpoint](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)). For more information, see [Get ADFS endpoint](/powershell/module/adfs/get-adfsendpoint).
- Devices must be purchased from [Apple School Manager](http://school.apple.com).  

Apple School Manager enrollment can't be used with the [device enrollment manager](device-enrollment-manager-enroll.md) account.  

## Next steps    

This series of articles describes how to set up Microsoft Intune for devices purchased through Apple School Manager. 

1. 🡺 Prerequisites (*You are here*)  
1. [Get an Apple token for school devices](apple-school-manager-step-1.md)  
1. [Create an Apple enrollment profile](apple-school-manager-step-2.md)  
1. [Sync and distribute devices](apple-school-manager-step-3.md) 
