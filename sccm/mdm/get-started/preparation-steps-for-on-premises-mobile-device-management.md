---
title: "Preparation steps for On-premises Mobile Device Management in System Center Configuration Manager"
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
caps.latest.revision: 4
author: Mtillman

---
# Preparation steps for On-premises Mobile Device Management in System Center Configuration Manager
Managing devices with System Center Configuration Manager On\-premises Mobile Device Management requires the Configuration Manager infrastructure to be set up so that the required site system roles (enrollment proxy point, enrollment point, device management point, and distribution point) can communicate across a trusted channel with the mobile devices to be managed.  
  
 The following high-level tasks are required to prepare the Configuration Manager system for On\-premises Mobile Device Management:  
  
-   [Set up a Microsoft Intune subscription for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management.md)  
  
     In this task, you sign up for Microsoft Intune, and then add the subscription to Configuration Manager through the Configuration Manager console. This step is required for licensing purposes only. Intune is not used to manage the devices or store management information. All coordination and management of devices is with your organization's enterprise using the on-premises Configuration Manager infrastructure.  
  
-   [Install site system roles for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mobile-device-management.md)  
  
     In this task, you install and configure the site system roles required to manage devices with on-premises Configuration Manager infrastructure. On\-premises Mobile Device Management minimally requires the enrollment proxy point, enrollment point, device management point, and distribution point site system roles.  
  
-   [Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-certificates-for-trusted-communications-for-on-premises-mobile-device-management.md)  
  
     In this task, you configure the on-premises Configuration Manager infrastructure to allow trusted communications (HTTPS) between managed devices and the servers hosting the required site system roles.  
  
-   [Set up device enrollment for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-for-on-premises-mobile-device-management.md)  
  
     In this task, you grant permission to users to enroll computers and devices and you install the trusted root certificate on devices (typically ones that are not domain-joined) to permit HTTPS connections to the site system servers.  
  
## See Also  
 [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)

