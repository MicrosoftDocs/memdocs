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
- [Windows 10 and Windows 8.1 devices](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)
- [Windows Phone devices](/sccm/compliance/deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client)
- [iOS and Mac devices](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)
- [Android and Samsung KNOX Standard devices](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)

**Applications** can be deployed to managed devices:
- [iOS applications](/sccm/apps/get-started/creating-ios-applications)
- [Mac applications](/sccm/apps/get-started/creating-mac-computer-applications)
- [Windows PC applications](/sccm/apps/get-started/creating-windows-applications)
- [Windows Phone applications](/sccm/apps/get-started/creating-windows-phone-applications)
- [Android applications](/sccm/apps/get-started/creating-android-applications)

**Conditional access** lets you manage access to company resources including:  
- [Email access](/sccm/protect/deploy-use/manage-email-access)
- [SharePoint access](/sccm/protect/deploy-use/manage-sharepoint-online-access)
- [Skype for Business access](/sccm/protect/deploy-use/manage-skype-for-business-online-access)
- [Dynamic CRM Online](/sccm/protect/deploy-use/manage-dynamics-crm-online-access)

**Multi-factor Authentication (MFA)** lets you require more than one verification method, which adds a critical second layer of security to user sign-ins and transactions.
Previously, you would go to either the Intune console or the Configuration Manager console to set MFA for Intune enrollments. Now, you login to the [Microsoft Azure portal](https://manage.windowsazure.com) using your Intune credentials and configure MFA settings through Azure AD. To learn more, see [Multi-factor authentication for Microsoft Intune](https://aka.ms/mfa_ad).
