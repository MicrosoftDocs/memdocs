---
title: "Set up additional management using System Center Configuration Manager | Microsoft Docs"
description: "Set up additional management using System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillmanms.author: mtillman
manager: angrobe
---
# Set up additional management with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
(Optional) You can set up additional management before devices are enrolled. These management solutions can be created and deployed after devices are enrolled, although many organizations prefer to deploy them as devices are brought into management.

**Configuration items** let you manage settings such as requiring a PIN or requiring encryption on enrolled devices based on device platform:
- [Windows 10 and Windows 8.1 devices](emm-create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Windows Phone devices](emm-create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [iOS and Mac devices](emm-create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Android and Samsung KNOX Standard devices](emm-create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

**Applications** can be deployed to managed devices:
- [iOS applications](emm-creating-ios-applications.md)
- [Mac applications](../../apps/get-started/creating-mac-computer-applications.md)
- [Windows PC applications](../../apps/get-started/creating-windows-applications.md)
- [Windows Phone applications](emm-creating-windows-phone-applications.md)
- [Android applications](emm-creating-android-applications.md)

**Conditional access** lets you manage access to company resources including:  
- [Email access](emm-manage-email-access.md)
- [SharePoint access](emm-manage-sharepoint-online-access.md)
- [Skype for Business access](emm-manage-skype-for-business-online-access.md)
- [Dynamic CRM Online](emm-manage-dynamics-crm-online-access.md)

**Multi-factor Authentication (MFA)** lets you require more than one verification method, which adds a critical second layer of security to user sign-ins and transactions.
Previously, you would go to either the Intune console or the Configuration Manager console to set MFA for Intune enrollments. Now, you login to the [Microsoft Azure portal](https://manage.windowsazure.com) using your Intune credentials and configure MFA settings through Azure AD. To learn more, see [Multi-factor authentication for Microsoft Intune](https://aka.ms/mfa_ad).
