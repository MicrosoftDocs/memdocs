---
title: "Manage an Intune subscription"
titleSuffix: "Configuration Manager"
description: "Manage an Intune subscription associated with System Center Configuration Manager."
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b494767-68c1-47b1-9a86-591bff0ad491
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
---
# Manage an Intune subscription associated with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

If you add a Microsoft Intune (either a trial subscription or paid subscription) to Configuration Manager, and then need to switch to a different Intune subscription, you must delete both the  **Microsoft Intune Subscription** and the **Service connection point** from the Configuration Manager console before you can add a new subscription.

> [!NOTE]
> You can configure only one Intune subscription at a time in hybrid mobile device management.

## How to delete an Intune subscription from Configuration Manager

> [!IMPORTANT]
>  All content including user enrollments, policies, and app deployments configured for devices managed by the Intune subscription are removed when you delete the subscription.

1.  In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Microsoft Intune Subscriptions**.

2.  Right-click the listed **Microsoft Intune Subscription**, and then click **Delete**.

3.   In the wizard, click **Remove Microsoft Intune Subscription from Configuration Manager**, click **Next**, and then click **Next** again to remove the subscription.


## How to remove the service connection point role

1.  Go to **Administration** > **Overview** > **Site Configuration** > **Servers and Site System Roles**.

2.  Select the server that hosts the **Service connection point** role.

3.  In the **Site System Roles** list, select **Service connection point** and then click **Remove Role** in the ribbon. Confirm you want to remove the role. The service connection point is deleted.

You can now create a new service connection point, add a new Intune subscription to Configuration Manager, and set Configuration Manager as the MDM Authority.

## How to change MDM authority to Intune
Beginning in Configuration Manager version 1610 and Microsoft Intune version 1705, you can change your MDM authority without having to contact Microsoft Support, and without having to unenroll and reenroll your existing managed devices. For details, see [Change your MDM authority](/sccm/mdm/deploy-use/change-mdm-authority).
