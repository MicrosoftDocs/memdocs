---
title: "Use the Configuration Manager extended interoperability client with the Current Branch "
description: "Learn about using the client from the Long-Term Servicing Branch of Configuration Manager with a Current Branch site."
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
---

# Use the Configuration Manager client software for extended interoperability with future versions of a Current Branch site

*Applies to: System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch)*  

In some cases, your company policies might not allow you to regularly update the Configuration Manager client on some PCs. For example, you might need to comply with change management policies, or the device might be mission-critical.

While you should continue to use automatic client upgrade when possible for most of your clients, beginning with Configuration Manager update 1610, you can accommodate these needs by installing a new client for long-term use, called the extended interoperability client (EIC).

The EIC is compatible with Configuration Manager sites running version 1610 or later. The EIC should only be used for specific PCs that cannot be frequently updated, like kiosk, or point-of-sale devices. Use the most recent Configuration Manager client for all other PCs.

## How this scenario works

Typically, when you install a new in-console update for the Current Branch, clients automatically update their client software so they can use those new features.

With this scenario, you use the Current Branch and receive the new features and updates. Most clients run the client software from the Current Branch and can update that client software with each version update you install. However, on a subset of critical systems that you do not want to receive client software updates, you install the extended interoperability client. These clients do not install new client software until you explicitly deploy a new version of the client software to them.

>[!IMPORTANT]
>The Current Branch site must run version 1610 or later.

## How to use the EIC

1. Obtain the EIC (client version 5.00.8412) from the \SMSSETUP\Client folder  of the Configuration Manager 1606 update installation media. Ensure that you copy the entire contents of the folder.
2. Manually install the EIC on those devices. [Read more details about how to manually install the client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).
3. Exclude that collection from client upgrades.

>[!TIP]
>To find System Center Configuration Manager version 1606 in the Volume Licensing Service Center (VLSC), go to the **Downloads and Keys** tab of the [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), search for "system center config," and then select **System Center Config Mgr (current branch and LTSB)**.

## The extended interoperability client software

The current EIC will continue to be supported with updated versions of Configuration Manager Current Branch until at least November 18, 2018. After this time, check this page for details of a new EIC, or an extension of support for the existing EIC.

>[!TIP]
>The EIC is supported for at least two years from the date of release (see [Support for System Center Configuration Manager current branch versions](/sccm/core/servers/manage/current-branch-versions-supported)). For example, support for the current EIC is two years after the release of 1610, which is 18 November 2018.

Plan to update the extended interoperability client on devices that you manage with the Current Branch before support for the client expires. To do so, download a new version of the client from Microsoft and then deploy that updated client software to your devices that use the current extended interoperability client.

## Limitations of the extended interoperability client

- Updates for the extended interoperability client software are not available by using in-console updates. Additional details for deploying an updated client software are provided when an updated client is released.
- The EIC only supports software updates, inventory, and packages and programs.

## Next steps

Use the information in [How to monitor clients](/sccm/core/clients/manage/monitor-clients) to ensure that clients are installed correctly on the devices you want.
