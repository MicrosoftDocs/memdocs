---
title: "Create Exchange ActiveSync email profiles | Microsoft Docs"
description: "Learn how to create and configure email profiles in System Center Configuration Manager that work with Microsoft Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: 4
caps.handback.revision: 0
author: Nbigmanms.author: nbigmanmanager: angrobe

---

# Exchange ActiveSync email profiles in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Email profiles works with  Microsoft Intune to enable you to provision devices with email profiles and restrictions by using Exchange ActiveSync. This enables your users to access corporate email on their devices with minimal setup required on their part.  

 You can configure the following device types with email profiles:  

-   Devices that run Windows Phone 8  

-   Devices that run Windows Phone 8.1  

-   Devices that run Windows  10 Mobile  

-   IPhone devices that run iOS 5, iOS 6, iOS 7 and iOS 8  

-   IPad devices that run iOS 5, iOS 6, iOS 7 and iOS 8  

> [!IMPORTANT]  
>  To deploy profiles to iOS, Android Samsung KNOX Standard, Windows Phone, and Windows 8.1 or Windows 10 devices, these devices must be enrolled into Intune. For information about how to get your devices enrolled, see [Manage mobile devices with Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 In addition to configuring an email account on the device, you can also configure synchronization settings for contacts, calendars and tasks.  

 When you create an email profile, you can include a wide range of security settings, including certificates for identity, encryption and signing that have been provisioned by using System Center Configuration Manager certificate profiles. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](../../protect/deploy-use/introduction-to-certificate-profiles.md).    

For detailed information about creating an email profile, see [Create a New Exchange ActiveSync Email Profile](../../protect/deploy-use/create-exchange-activesync-profiles.md#create-a-new-exchange-activesync-email-profile). For information about how to deploy the Exchange ActiveSync email profiles, see [How to deploy profiles in System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).  
