---
title: "Introduction to Wi-Fi Profiles | System Center Configuration Manager"
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 86725460-c2f3-49ed-90aa-6b2724d34d69
caps.latest.revision: 8
author: Nbigman

---
# Introduction to Wi-Fi Profiles in System Center Configuration Manager
Use Wi-Fi profiles in System Center Configuration Manager to deploy wireless network settings to users in your organization. By deploying these settings, you minimize the end-user effort required to connect to the wireless network.  
  
 For example, you installed a new Wi-Fi network named **Contoso Wi-Fi**. You now want to provision all devices that run the iOS operating system with the settings required to connect to this network. You can create a Wi-Fi profile containing the settings necessary to connect to the **Contoso Wi-Fi** wireless network. Then, you can deploy this profile to all users that have devices that run iOS in your hierarchy. Users of iOS devices see the company network in the list of wireless networks and can readily connect to this network.  
  
 You can configure the following device types with Wi-Fi profiles:  
  
-   Devices that run Windows 8.1 32-bit  
  
-   Devices that run Windows 8.1 64-bit  
  
-   Devices that run Windows RT 8.1  
  
-   Devices that run Windows Phone 8.1  
  
-   Devices that run Windows 10 Desktop or Mobile  
  
-   IPhone devices that run iOS 5, iOS 6, iOS 7 and iOS 8  
  
-   IPad devices that run iOS 5, iOS 6, iOS 7 and iOS 8  
  
-   Android devices that run version 4  
  
> [!IMPORTANT]  
>  To deploy profiles to Android, iOS, Windows Phone, and enrolled Windows 8.1 or later devices, these devices must be enrolled in Microsoft Intune]. For information about how to get your devices enrolled, see [Manage mobile devices with Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx).  
  
 When you create a Wi-Fi profile, you can include a wide range of security settings. These include certificates for server validation and client authentication that have been provisioned by using Configuration Manager certificate profiles. For more information about certificate profiles, see [Certificate profiles in System Center Configuration Manager](../Topic/Certificate%20profiles%20in%20System%20Center%20Configuration%20Manager.md).  
  
## See Also  
 [Wi-Fi Profiles in System Center Configuration Manager](../Topic/Wi-Fi%20Profiles%20in%20System%20Center%20Configuration%20Manager.md)

