---
title: Use Software Center to deploy Windows over the network
titleSuffix: "Configuration Manager"
description: "You can deploy an operating system to Software Center to refresh an existing computer with a new version of Windows or to upgrade Windows to the latest version."
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: 5
author: mattbriggs
ms.author: mabrigg
manager: angrobe

---
# Use Software Center to deploy Windows over the network with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You may make the task sequence that installs an operating system in System Center Configuration Manager available in  Software Center. You may deploy an  operating system to Software Center with the following operating system deployment scenarios:

-   [Refresh an existing computer with a new version of Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Upgrade Windows to the latest version](upgrade-windows-to-the-latest-version.md)

Complete the steps in one of the operating system deployment scenarios. Then use the following sections to prepare for deployments that are available in Software Center.

## Configure deployment settings  
To make the operating system deployment available in the Software Center, configure the deployment. You may configure the deployment on the **Deployment Settings** page of the Deploy Software Wizard or the **Deployment Settings** tab in the properties for the deployment. For the **Make available to the following** setting, configure either **Only Configuration Manager Clients** or **Configuration Manager clients, media and PXE**. After the system deploys the operating system, the operating system will be displayed in Software Center for members of the target collection.

##  <a name="BKMK_Deploy"></a> Deploy the task sequence to computers  
Deploy the operating system to a target collection. For more information, see [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). When you deploy operating systems for Software Center, you may configure whether the deployment is required or available.

-   **Required deployment**: Required deployments will make the operating system available in Software Center, but it will be automatically started at the configured assignment schedule.

-   **Available deployment**: The operating system will be available in the Software Center and the user can install it on demand.
