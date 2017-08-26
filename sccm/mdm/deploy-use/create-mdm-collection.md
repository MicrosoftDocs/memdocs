---
title: "Create an MDM collection using System Center Configuration Manager | Microsoft Docs"
description: "Create an MDM collection using System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
---
# Create an MDM collection with System Center Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*

A Configuration Manager user collection is required to specify the users who can enroll devices into management. You can only use user collections (instead of device collections) because Intune licenses are assigned by user.

> [!NOTE]
> To enroll devices with Intune, you do not need to assign licenses to users in the Office 365 portal or Azure Active Directory portal. Including the users in a collection that gets associated with the Intune subscription (in a [later step](configure-intune-subscription.md)) is all that's required.

For testing purposes you can set up a **Direct rule** and add specific users who can enroll devices. In the Configuration Manager console, choose, **Assets and Compliance** > **User Collections**, click the **Home** tab > **Create** group, and then click **Create User Collection**. For broader distribution you should use **Query rules** to define users. For more information about collections, see [How to create collections](https://technet.microsoft.com/library/mt629371.aspx).

![Create a user collection for MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
[Next step >](confirm-dns.md)
