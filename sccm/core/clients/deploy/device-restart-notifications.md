---
title: Device restart notifications
titleSuffix: Configuration Manager
description: Learn about restart notification behavior for various client settings
ms.date: 07/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# About device restart notifications in Configuration Manager

*Applies to: System Center Configuration Manager (current branch)*

The notifications a user receives for a pending device restart can vary depending on [Computer restart client settings](/sccm/core/clients/deploy/about-client-settings#computer-restart) and which version of Configuration Manager is being used. This article helps admins determine what the user experience is for pending device restart notifications.

>[!NOTE]
>This article focuses on client settings found in Configuration Manager version 1902 and version 1906.

## Understanding restart notification types

The [Computer restart client settings](/sccm/core/clients/deploy/about-client-settings#computer-restart) change the user experience for all required deployments that require a restart of the following types:

- [Application](/sccm/apps/deploy-use/deploy-applications)
- [Task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)
- [Software update](/sccm/sum/deploy-use/deploy-software-updates)

There are three types of notifications users can receive.

## Device restart notifications in version 1902

## Device restart notifications starting in version 1906

Some admins prefer frequent restart notifications and a short time frame for allowing restarts to be postponed. Other admins allow users to postpone a restart for longer periods of time and want users to be notified of the pending restart infrequently. Configuration Manager version 1906 gives an admin additional control over the timing and frequency of restart notifications.

## Next steps

- [Introduction application management](/sccm/apps/understand/introduction-to-application-management)
- [Introduction to operating system deployment](/sccm/osd/understand/introduction-to-operating-system-deployment)
- [Introduction to software updates management](/sccm/sum/understand/software-updates-introduction)
