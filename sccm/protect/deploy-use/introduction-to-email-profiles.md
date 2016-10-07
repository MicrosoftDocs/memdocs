---
title: "Introduction to email profiles | System Center Configuration Manager"
description: "Learn how to use email profiles to enable your users to access corporate email on their devices with minimal setup."
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c4e2dc48-91c2-438f-9e1a-947b1125b0e2
caps.latest.revision: 3
caps.handback.revision: 0
author: Nbigmanms.author: nbigmanmanager: angrobe

---
# Introduction to email profiles in System Center Configuration Manager
Email profiles works with  Microsoft Intune to enable you to provision devices with email profiles and restrictions by using Exchange ActiveSync. This enables your users to access corporate email on their devices with minimal setup required on their part.  

 You can configure the following device types with email profiles:  

-   Devices that run Windows Phone 8  

-   Devices that run Windows Phone 8.1  

-   Devices that run Windows  10 Mobile  

-   IPhone devices that run iOS 5, iOS 6, iOS 7 and iOS 8  

-   IPad devices that run iOS 5, iOS 6, iOS 7 and iOS 8  

> [!IMPORTANT]  
>  To deploy profiles to iOS, Android Samsung KNOX, Windows Phone, and Windows 8.1 or Windows 10 devices, these devices must be enrolled into Intune. For information about how to get your devices enrolled, see [Manage mobile devices with Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 In addition to configuring an email account on the device, you can also configure synchronization settings for contacts, calendars and tasks.  

 When you create an email profile, you can include a wide range of security settings, including certificates for identity, encryption and signing that have been provisioned by using System Center Configuration Manager certificate profiles. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md).  
