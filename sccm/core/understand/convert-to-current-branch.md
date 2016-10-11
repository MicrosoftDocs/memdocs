---
title: "Upgrade the Long-Term Servicing Branch to the Current Branch  | System Center Configuration Manager"
description: "Learn how to convert a Long-Term Servicing Branch site to a Current Branch site."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
caps.latest.revision: 0
author: Brendunsms.author: brendunsmanager: angrobe
---


# Upgrade the Long-Term Servicing Branch to the Current Branch*Applies to: System Center Configuration Manager (Current Branch)*


Use this topic to learn how to upgrade (convert) a site and hierarchy that runs the Long-Term Servicing Branch (LTSB) of Configuration Manager to the Current Branch.

When you have a current Software Assurance agreement (or similar licensing rights) that grants you rights to use the Current Branch, you can convert your installation from the LTSB to the Current Branch.  This is a one-way conversion as there is no support to convert a Current Branch site to the LTSB.

If you have multiple sites, you only need to convert the top-tier site of your hierarchy. After the top-tier site is converted:
- Child primary sites automatically convert.
-	You must manually update secondary sites from within the Configuration Manager console.

## Run Setup to convert
On the top-tier site of your hierarchy, you can run Configuration Manager Setup from qualifying baseline media and select **Site maintenance**.  Then, when presented with the licensing page, select the option for Current Branch, and complete the wizard.

When completed, your site is converted to the Current Branch, and previously unavailable features and capabilities will be available for use.

> [!NOTE]  
> Qualifying baseline media is a media that has a version that is equal to or later than your LTSB installation.

For example, because the LTSB is based on version 1606, you cannot use the baseline 1511 media to convert to the Current Branch. Instead, you run Setup from the same version 1606 baseline media you used to install the LTSB site, and choose the licensing option for the Current Branch.  Alternately, if a later baseline of the Current Branch has been released, you can run Setup from that baseline media.

For a list of baseline versions, see **Baseline and update versions** in [Updates for Configuration Manager](/sccm/core/servers/manage/updates).

## Use the Configuration Manager Console to convert
If your site runs the LTSB, you can use the following option in the Configuration Manager console to convert to the Current Branch:

 1. In the console go to **Administration** > **Site Configuration** > **Sites**, and open **Hierarchy Settings**.  
 2. Select the option to convert to the Current Branch, and then click **Apply**.  

When completed, your site is converted to the Current Branch, and previously unavailable features and capabilities will be available for use.
