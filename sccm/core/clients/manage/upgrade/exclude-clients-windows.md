---
title: "Exclude client upgrades for Windows"
description: "Learn how to exclude Windows clients from getting upgraded in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: arob98
ms.author: angrobe
manager: angrobe

---
# How to exclude upgrading clients for Windows computers in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Beginning in version 1610, you can exclude a collection of clients from automatically installing updated client versions. This applies to automatic upgrade as well as other methods such as software update-based upgrade, logon scripts, and group policy. You can use this for a collection of computers that need greater care when upgrading the client. A client that is in an excluded collection ignores requests to install updated client software.

## Configure exclusion for automatic upgrades

1. In the Configuration Manager console, go to **Administration** > **Site Configuration** > **Sites**, and then click **Hierarchy Settings**.

2. Click the **Client Upgrade** tab.

3. Click the checkbox for **Exclude specified clients from upgrade**, and then for Exclusion collection, select the collection you want to exclude. You can only select a single collection for exclusion.

4.  Click **OK** to close and save the configuration. Then, after clients update policy, clients in the excluded collection will no longer automatically install updates to the client software. For more information, see [How to upgrade clients for Windows computers](upgrade-clients-for-windows-computers.md).

![Settings for automatic upgrade exclusion](media/automatic_upgrade_exclusion.png)



>[!NOTE]
>Although the user interface states that clients will not be upgraded via any method, there are two methods you can use to override these settings. Client push installation and a manual client installation can be used to override this configuration. For more details, see the following section.

## How to upgrade a client that is in an excluded collection

So long as a collection is configured to be excluded, members of that collection can only have their client software upgraded by one of two methods, which override the exclusion:
 - **Client Push Installation** – You can use client push installation to upgrade a client that is in an excluded collection. This is allowed as it is considered to be the intent of the administrator and enables you to upgrade clients without removing the entire collection from exclusion.       

 - **Manual client installation** – You can manually upgrade clients that are in an excluded collection when you use the following command line switch with ccmsetup:  ***/ignoreskipupgrade***

  If you attempt to manually upgrade a client that is a member of the excluded collection and do not use this switch, the client will not install the new client software. For more information see [How to install Configuration Manager Clients Manually](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).

For more information on client installation methods, see [How to deploy clients to Windows computers in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).
