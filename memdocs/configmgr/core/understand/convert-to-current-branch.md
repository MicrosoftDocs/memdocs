---
title: Upgrade the LTSB to current branch
titleSuffix: Configuration Manager
description: Learn how to convert a long-term servicing branch (LTSB) site to a current branch site.
ms.date: 02/8/2017
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: upgrade-and-migration-article
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Upgrade the long-term servicing branch to the current branch

*Applies to: System Center Configuration Manager (Long-Term Servicing Branch)*

Use this topic to learn how to upgrade (convert) a site and hierarchy that runs the Long-Term Servicing Branch (LTSB) of Configuration Manager to the Current Branch.

When you have a current Software Assurance agreement (or similar licensing rights) that grants you rights to use the Current Branch, you can convert your installation from the LTSB to the Current Branch.  This is a one-way conversion because there is no support for converting a Current Branch site to the LTSB.

If you have multiple sites, you only need to convert the top-tier site of your hierarchy. After the top-tier site is converted:
- Child primary sites automatically convert.
- You must manually update secondary sites from within the Configuration Manager console.

## Run setup to convert the Long-Term Servicing Branch
On the top-tier site of your hierarchy, you can run Configuration Manager setup from qualifying baseline media and select **Site maintenance**.  Then, when presented with the licensing page, select the option for the Current Branch and complete the wizard.

When your site has converted to the Current Branch, previously unavailable features and capabilities will be available for use.

> [!NOTE]  
> Qualifying baseline media is a media that has a version that is equal to or later than your LTSB installation.

For example, because the LTSB is based on version 1606, you cannot use the baseline 1511 media to convert to the Current Branch. Instead, you run setup from the same version 1606 baseline media that you used to install the LTSB site, and choose the licensing option for the Current Branch.  Alternately, if a later baseline of the Current Branch has been released, you can run setup from that baseline media.

For a list of baseline versions, see **Baseline and update versions** in [Updates for Configuration Manager](../servers/manage/updates.md).

## Use the Configuration Manager console to convert the long-term servicing branch
If your site runs the LTSB, you can use the following option in the Configuration Manager console to convert to the Current Branch:

 1. In the console, go to **Administration** > **Site Configuration** > **Sites**, and then open **Hierarchy Settings**.  

 2. In **Hierarchy Settings**, switch to the **Licensing** tab. Select the option to **Convert to Current Branch**, and then choose **Apply**.  

When your site has converted to the Current Branch, previously unavailable features and capabilities will be available for use.
