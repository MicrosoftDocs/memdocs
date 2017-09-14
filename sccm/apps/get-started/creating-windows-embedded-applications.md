---
title: "Create Windows Embedded applications | Microsoft Docs"
description: "See which considerations you must take into account when you create and deploy applications for Windows Embedded devices."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
caps.latest.revision: 7
author: mattbriggsms.author: mabriggmanager: angrobe

---
# Create Windows Embedded applications with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
In addition to the other System Center Configuration Manager requirements and procedures for creating an application, you must also take the following considerations into account when you create and deploy applications for Windows Embedded devices.  

## General considerations  

-   When you deploy applications to Windows Embedded devices that are enabled for write filtering, you can specify whether to disable the write filter on the device during the app deployment. You can then choose to restart the write filter after the app deployment. If the write filter is not disabled, the software is deployed to a temporary overlay. This means that unless another deployment forces changes to persist, the software will no longer be installed when the device restarts.  

-   When you deploy an application to a Windows Embedded device, make sure that the device is a member of a collection that has a configured maintenance window. This lets you manage when the write filter is disabled and enabled, and when the device restarts.  

-   The setting that controls the write filter behavior is a check box named **Commit changes at deadline or during a maintenance window (requires restarts)**.  

## Tips for deploying applications  

**Use required applications rather than available applications for Windows Embedded devices that have write filters enabled.** Because users cannot install apps from Software Center on a Windows Embedded device that has write filters enabled, always deploy applications with a deployment purpose of **required** rather than **available** to these devices. Typically, this isn't a problem because computers that run a Windows Embedded operating system often run a single application that must run in the same way for multiple users. Because of this, these devices are highly managed and locked down by the IT department. Required applications are well-suited to this scenario.

 However, if users do run more than one application on embedded devices when write filters are enabled, educate these users about the following limitations:  

-   Users cannot install required software from Software Center.  

-   Users cannot change their business hours in the Options tab of Software Center.  

-   Users cannot postpone the installation of a required application.  

In addition, low-rights users cannot log on during a maintenance period if Configuration Manager is committing changes for software installations and updates. During this period, users see a message informing them that the device is unavailable because it is being serviced.  

**Do not deploy applications to Windows Embedded devices that have write filters enabled if the applications require the user to accept the license terms.** When write filters are disabled so that Configuration Manager can install software on embedded devices, low-rights users cannot log on to the device. If the installation requires the user to accept the license terms, this will not be possible and the installation will fail. Make sure that you do not deploy software to Windows Embedded devices if the installation requires user interaction. You can use the Applicable Platforms list to filter these operating systems.  
