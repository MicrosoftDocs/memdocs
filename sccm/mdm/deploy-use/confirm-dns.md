---
title: "Confirm domain name requirements"
titleSuffix: "Configuration Manager"
description: "Confirm domain name requirements using System Center Configuration Manager."
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 522c2e82-20eb-4f38-859b-d55640b24e32
caps.latest.revision: 18
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
---
# Confirm domain name requirements with System Center Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*

If necessary, take the following steps to satisfy any dependencies external to Configuration Manager:

1. Each user must have an Intune license assigned to enroll devices. To associate Intune licenses to users, each user must have a user principal name (UPN) that can be publicly resolved (for example, johndoe@contoso.com) or an alternate login ID configured in Azure Active Directory. Configuring an alternate login ID allows users to sign in with an email address, for example, even if their UPN is in a NetBIOS format (for example, CONTOSO\johndoe).

  - If your company uses publicly resolvable UPNs (i.e. johndoe@contoso.com), no further configuration is required.
  - If your company uses a non-resolvable UPN (i.e. CONTOSO\johndoe), you must [configure an alternate ID in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2.  Deploy and configure Active Directory Federation Services (AD FS). (Optional)

     When you set up single sign-on, your users can sign in with their corporate credentials to access the services in Intune.

     For more information, see the following topics:
    -   [Prepare for single sign-on](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [Plan for and deploy AD FS 2.0 for use with single sign-on](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  Deploy and configure directory synchronization.

     Directory synchronization lets you populate Intune with synchronized user accounts. The synchronized user accounts and security groups are added to Intune. Failure to enable Directory Synchronization is a common cause of devices not being able to enroll when setting up Configuration Manager MDM with Microsoft Intune.

     For more information, see [Directory integration](http://go.microsoft.com/fwlink/?LinkID=271120) in the Active Directory documentation library.

4.  Optional, not recommended: If you are not using Active Directory Federation Services, reset users' Microsoft Online passwords.

     If you are not using AD FS, you must set a Microsoft Online password for each user.

> [!div class="button"]
[< Previous step](create-mdm-collection.md)  [Next step >](configure-intune-subscription.md)
