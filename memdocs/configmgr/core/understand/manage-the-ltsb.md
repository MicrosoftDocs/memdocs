---
title: Manage the LTSB
titleSuffix: Configuration Manager
description: Management differences for the LTSB of Configuration Manager.
ms.date: 03/24/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Manage the long term servicing branch of Configuration Manager

*Applies to: System Center Configuration Manager (long term servicing branch)*

When you use the long term servicing branch (LTSB) of Configuration Manager, there are important changes that affect how you manage your infrastructure.

The LTSB is generally the same as current branch version 1606, with some exceptions like cloud-attached features. Most tasks you use for planning, deployment, configuration, and day-to-day management are the same.

For example, the LTSB supports the same number of sites, site types, clients, and general infrastructure as the current branch. Use the same guidance for site and hierarchy planning and design as the current branch. Some features are supported by both branches, like software updates or OS deployment. Use the same guidance as the current branch, with the understanding that there were feature changes since version 1606 of the current branch.

The following sections provide information about tasks that aren't similar between the long term servicing branch and the current branch.

## Updates and servicing

Only critical security updates are made available as in-console updates in the LTSB.  

Regular updates for the current branch are visible in the console, but aren't made available to the LTSB. They aren't downloaded and can't be installed.

To support in-console updates for critical security fixes, an LTSB site requires the use of the [service connection point](../servers/deploy/configure/about-the-service-connection-point.md). You can configure this site system role in offline or online mode, the same as for the current branch. The LTSB collects and submits the same diagnostic and usage data as the current branch.

The LTSB supports the use of the hotfix installer and the update registration tool, as documented for the current branch.

For general information about updates and servicing, see [Updates for Configuration Manager](../servers/manage/updates.md).

## Changes for site expansion and the `CD.Latest` folder

When you use the LTSB, and expand a stand-alone primary site with a new central administration site (CAS), run setup and the source files from the version 1606 baseline media. For the current branch, you run setup and use source files from the `CD.Latest` folder.

Although you don't run setup for site expansion from the `CD.Latest` folder, continue to use the `CD.Latest` folder for the following actions:

- Site recovery
- Install a new child primary site when your first LTSB site was a CAS

For more information about site expansion, see [Expand a stand-alone primary site](../servers/deploy/install/setup-wizard-central-primary.md#expand-a-stand-alone-primary-site). For more information about the `CD.Latest` folder, see [The `CD.Latest` folder](../servers/manage/the-cd.latest-folder.md).

## Recovery

When you recover a site, you must restore the site or site database to its original branch. You can't recover a current branch site database to an LTSB installation, or an LTSB site to a current branch installation.

## Next steps

[Upgrade the long-term servicing branch to the current branch](convert-to-current-branch.md)
