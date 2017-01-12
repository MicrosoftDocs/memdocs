---
title: Setup hybrid MDM  | Microsoft Docs
description: "Set up hybrid device enrollment with Configuration Manager and Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
---

# Setup hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*


Before you can manage iOS, Windows, and Android devices with Configuration Manager, they must be enrolled with Intune. Use the following steps to setup hybrid device enrollment with Configuration Manager using Intune. By completing the following steps you will enable "bring your own device" (BYOD) enrollment for your users. These steps are also prerequisites for [enrolling BYOD devices](deploy-use/enroll-hybrid-ios-mac.md) and [enrolling company-owned devices](enroll-company-owned-devices.md).

 |Steps|Details|  
 |-----------|-------------|  
 |**Step 1:** [Create an MDM collection](deploy-use/create-mdm-collection.md)|Create a Configuration Manager user collection with users whose devices can be enrolled|  
 |**Step 2:** [Domain name requirements](deploy-use/confirm-dns.md)|Confirm your organization's domain name service (DNS) and Active Directory user management meets MDM requirements|
 |**Step 3:** [Configure Intune Subscription](deploy-use/configure-intune-subscription.md)|The Intune service lets you manage devices over the Internet.|  
 |**Step 4:** [Add terms and conditions](deploy-use/terms-and-conditions.md)| Create terms and conditions to which users must agree before they can use the Company Portal app|
 |**Step 5:** [Create service connection point](deploy-use/create-service-connection-point.md)|The service connection point sends settings and software deployment information to Configuration Manager and retrieves status and inventory messages from mobile devices. |  
 |**Step 6:** [Enable platform enrollment](deploy-use/enable-platform-enrollment.md)|MDM enrollment for [iOS](#ios-and-mac-enrollment-setup) and [Windows](#windows-enrollment-setup) devices require additional steps for communication between the service and devices. Android requires no additional configuration.|  
 |**Step 7:** [Set up additional management](deploy-use/set-up-additional-management.md)|(Optional) Set up configuration items and conditional access for enrolled devices|
 |**Step 8:** [Verify MDM configuration](deploy-use/verify-mdm-configuration.md)|View log files to confirm that the service connection point was created successfully and user accounts are synchronizing.|
 |**Step 9:** [Brand company portal](deploy-use/company-portal-branding.md)|Customize the appearance of the portal with your company logo and custom color schemes.|

Looking for Intune without Configuration Manager?
> [!div class="button"]
[View Intune docs >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## Enroll devices
After hybrid setup is complete, devices can be enrolled in Configuration Manager in a number of ways:
- Company-owned (COD) devices: [Enroll company-owned devices](enroll-company-owned-devices.md) provides guidance on different platform-specific ways to enroll company-owned devices.
- User-owned (BYOD) devices: [Enroll user-owned (BYOD) devices](deploy-use/enroll-hybrid-ios-mac.md) provides guidance on ways to enroll user-owned devices.
