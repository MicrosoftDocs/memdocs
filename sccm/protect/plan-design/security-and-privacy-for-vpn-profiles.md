---
title: "VPN profile security and privacy | System Center Configuration Manager"
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc78c1a4-d34e-4c7c-9abe-72c5adf073e5
caps.latest.revision: 5
author: Nbigman

---
# Security and privacy for VPN profiles in System Center Configuration Manager
This topic contains security and privacy information for VPN profiles in System Center Configuration Manager.  
  
##  <a name="BKMK_Security_RemoteConnections"></a> Security Best Practices for VPN Profiles  
 Use the following security best practices when you manage VPN profiles for devices.  
  
|Security best practice|More information|  
|----------------------------|----------------------|  
|Whenever possible, choose the most secure options that your VPN infrastructure and client operating systems can support.|VPN profiles provide a convenient method to centrally distribute and manage VPN settings that are already supported by your devices. System Center Configuration Manager does not add VPN functionality.<br /><br /> Identify, implement, and follow any security best practices that have been recommended for your devices and VPN infrastructure.|  
  
## Privacy Information for VPN Profiles  
 You can use VPN profiles to configure client devices to connect to VPN servers and to evaluate whether those devices become compliant after the profiles are applied. Compliance information is sent to the site server by the management point and stored in the site database. The information is encrypted when devices send it to the management point, but it is not stored in encrypted format in the site database. Information is retained in the database until the site maintenance task **Delete Aged Configuration Management Data** deletes it every 90 days. You can configure the deletion interval. Compliance information is not sent to Microsoft.  
  
 By default, devices do not evaluate VPN profiles. In addition, you must configure the VPN profiles, and then deploy them to users.  
  
 Before you configure VPN profiles, consider your privacy requirements.  
  
### See also  

 [VPN profiles in System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md)

