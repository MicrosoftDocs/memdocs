---
title: "Certificate Profiles in System Center Configuration Manager | Microsoft Docs"
description: "Certificate Profiles in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be6d8fcf-cad0-43ba-a33e-8fb5fc121312
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillmanms.author: mtillman
manager: angrobe
---
# Certificate Profiles in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Certificate profiles work with Active Directory Certificate Services and the Network Device Enrollment Service role to provision authentication certificates for managed devices so that users can seamlessly access company resources. For example, you can create and deploy certificate profiles to provide the necessary certificates for users to initiate VPN and wireless connections.

[Certificate profiles](../../protect/deploy-use/introduction-to-certificate-profiles.md) provides general information about creating and configuring certificaate profiles. This topic highlights some specific information about certificate profiles related to mobile device management.

- Certificate profiles provide certificate enrollment and renewal from an enterprise certification authority (CA) for devices that run iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop and Mobile, and Android. These certificates can then be used for Wi-Fi and VPN connections.

-  To deploy certificate profiles that use the SCEP, you must install a policy module for NDES on a server that runs Windows Server 2012 R2 with the Active Directory Certificate Services role and a working NDES that is accessible to the devices that require the certificates. For devices that are enrolled by Microsoft Intune, this requires the NDES to be accessible from the Internet, for example, in a screened subnet (also known as a DMZ).

-  Configuration Manager supports deploying certificates to different certificate stores, depending on the requirements, the device type, and  the operating system. The following devices and operating systems are supported:
 -   Windows RT 8.1  
 -   Windows 8.1  
 -   Windows Phone 8.1  
 -   Windows 10 Desktop and Mobile  
 -   iOS  
 -   Android  
 > [!IMPORTANT]  
 >  To deploy profiles to Android, iOS, Windows Phone, and enrolled Windows 8.1 or later devices, these devices must be [enrolled in Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).   

- For other prerequisites, see [Certificate profile prerequisites](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

**Create:** [Create a new certificate profile](../../protect/deploy-use/create-certificate-profiles.md) walks you through the Create Certificate Profile Wizard.


**Deploy:** See [Deploy Wi-Fi, VPN, email, and certificate profiles](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) for information about deploying certificate profiles.
