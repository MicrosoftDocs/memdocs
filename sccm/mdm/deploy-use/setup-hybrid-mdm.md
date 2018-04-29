---
title: Setup hybrid MDM
titleSuffix: "Configuration Manager"
description: "Set up hybrid device enrollment with Configuration Manager and Intune."
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Setup hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*


Before you can manage iOS, Windows, and Android devices with Configuration Manager, they must be enrolled with Intune. Use the following steps to setup hybrid device enrollment with Configuration Manager using Intune. By completing the following steps you will enable "bring your own device" (BYOD) enrollment for your users. These steps are also prerequisites for [enrolling BYOD devices](enroll-hybrid-ios-mac.md) and [enrolling company-owned devices](enroll-company-owned-devices.md).

 |Steps|Details|  
 |-----------|-------------|  
 |**Step 1:** [Create an MDM collection](create-mdm-collection.md)|Create a Configuration Manager user collection with users whose devices can be enrolled|  
 |**Step 2:** [Domain name requirements](confirm-dns.md)|Confirm your organization's domain name service (DNS) and Active Directory user management meets MDM requirements|
 |**Step 3:** [Configure Intune Subscription](configure-intune-subscription.md)|The Intune service lets you manage devices over the Internet.|  
 |**Step 4:** [Add terms and conditions](terms-and-conditions.md)| Create terms and conditions to which users must agree before they can use the Company Portal app|
 |**Step 5:** [Create service connection point](create-service-connection-point.md)|The service connection point sends settings and software deployment information to Configuration Manager and retrieves status and inventory messages from mobile devices. |  
 |**Step 6:** [Enable platform enrollment](enable-platform-enrollment.md)|MDM enrollment for iOS and Windows devices require additional steps for communication between the service and devices. Android requires no additional configuration.|  
 |**Step 7:** [Set up additional management](set-up-additional-management.md)|(Optional) Set up configuration items and conditional access for enrolled devices|
 |**Step 8:** [Verify MDM configuration](verify-mdm-configuration.md)|View log files to confirm that the service connection point was created successfully and user accounts are synchronizing.|

Looking for Intune without Configuration Manager?
> [!div class="button"]
[View Intune docs >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## Enroll devices
After hybrid setup is complete, devices can be enrolled in Configuration Manager in a number of ways:
- **Company-owned (COD) devices:** [Enroll company-owned devices](enroll-company-owned-devices.md) provides guidance on different platform-specific ways to enroll company-owned devices.
- **User-owned (BYOD) devices:** [Enroll user-owned (BYOD) devices](enroll-hybrid-ios-mac.md) provides guidance on ways to enroll user-owned devices.
