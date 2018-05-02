---
title: "Manage the LTSB"
titleSuffix: "Configuration Manager"
description: "Management differences for the LTSB of System Center Configuration Manager."
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Manage the Long Term Servicing Branch of Configuration Manager

*Applies to: System Center Configuration Manager (Long-Term Servicing Branch)*

When you use the Long-Term Servicing Branch (LTSB) of System Center Configuration Manager, the following can help you understand important changes that affect how you manage your infrastructure.

Because the LTSB is equivalent to Current Branch version 1606 (with some exceptions like Intune integration and cloud-related features), most tasks you use for planning, deployment, configuration, and day-to-day management are the same.

For example, the LTSB supports the same number of sites, site types, clients, and general infrastructure as the Current Branch. Therefore, you use the guidance found in the site and hierarchy planning and design topics for the Current Branch. Similarly, for features with the LTSB that are supported by both branches, like Software Updates or Operating System Deployment, use the guidance found in those sections of the Current Branch documentation with the caveats of not having access to feature changes introduced after version 1606 of the Current Branch.

The following sections provide information about manage tasks that are not similar.

## Updates and servicing
Only critical security updates are made available as in-console updates in the LTSB.  

Information about regular updates for the subsequent Current Branch releases are visible in the console, but are not made available to the LTSB. They are not downloaded and cannot be installed.

To support in-console updates for critical security fixes, an LTSB site requires the use of [the service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point). You can configure this site system role in offline or online mode, as is done for the Current Branch. The LTSB collects and submits the same telemetry and usage data as the Current Branch.

The LTSB supports the use of the Hotfix Installer and the Update Registration tool, as documented for the Current Branch.

For general information about updates and servicing, see [Updates for Configuration Manager](/sccm/core/servers/manage/updates).


## Changes for site expansion and the CD.Latest folder
When you run the LTSB and are expanding a stand-alone primary site by installing a new central administration site, you must use Setup and the source files from the version 1606 baseline media. For the Current Branch, you run Setup and use source files from the CD.Latest folder.

Although you do not run Setup for site expansion from the CD.Latest folder, you continue to use the CD.Latest folder for site recovery, and to install a new child primary site when your first LTSB site was a central administration site.

For more information about site expansion, see [Expand a stand-alone primary site](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site). For more information about the CD.Latest folder, see [The CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder).


## Recovery
When you recover a site, you must restore the site or site database to its original branch. You cannot recover a Current Branch site database to a LTSB installation, or vice versa.
