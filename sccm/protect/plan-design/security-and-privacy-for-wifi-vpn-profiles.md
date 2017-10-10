---
title: "Wi-Fi and VPN profile security and privacy"
description: "Learn about the security best practices for managing Wi-Fi and VPN profiles for devices in System Center Configuration Manager."
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
caps.latest.revision: 4
caps.handback.revision: 0
author: Nbigmanms.author: nbigmanmanager: angrobe

---
# Security and privacy for Wi-Fi and VPN profiles in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
##  Security Best Practices for Wi-Fi  and VPN Profiles  
 Use the following security best practices when you manage Wi-Fi  and VPN profiles for devices.  

|Security best practice|More information|  
|----------------------------|----------------------|  
|Whenever possible, choose the most secure options that your Wi-Fi and VPN infrastructure and client operating systems can support.|Wi-Fi and VPN profiles provide a convenient method to centrally distribute and manage Wi-Fi and VPN settings that your devices already support. Configuration Manager does not add Wi-Fi or VPN functionality.<br /><br /> Identify, implement, and follow any security best practices that have been recommended for your devices and infrastructure.|  

## Privacy Information for Wi-Fi Profiles  
 You can use Wi-Fi and VPN profiles to configure client devices to connect to Wi-Fi and VPN servers, and then evaluate whether those devices become compliant after the profiles are applied. The management point sends compliance information to the site server, and the information is stored in the site database. The information is encrypted when devices send it to the management point, but it is not stored in encrypted format in the site database. The database retains the information until the site maintenance task **Delete Aged Configuration Management Data** deletes it. The default deletion interval is 90 days, but you can change it. Compliance information is not sent to Microsoft.  

 By default, devices do not evaluate Wi-Fi and VPN profiles. In addition, you must configure the profiles, and then deploy them to users.  

 Before you configure Wi-Fi or VPN profiles, consider your privacy requirements.  
