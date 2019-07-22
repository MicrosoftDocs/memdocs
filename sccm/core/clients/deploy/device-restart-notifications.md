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

## Deployment types for restart notifications

The [Computer restart client settings](/sccm/core/clients/deploy/about-client-settings#computer-restart) change the user experience for all required deployments that require a restart of the following types:

- [Application](/sccm/apps/deploy-use/deploy-applications)
- [Task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)
- [Software update](/sccm/sum/deploy-use/deploy-software-updates)

## Restart notification types

When a restart is required, the end user is is given notification of the upcoming restart. There are three general notifications users can receive:

**Toast notification** informing you a restart is needed. The information in the toast notification can be different depending on which version of Configuration Manager you are running. This type of notification is native to the Windows OS and you may also see third party software using this type of notification.

![Toast notification of pending restart](media/3976435-toast-restart-countdown.png)

Software Center notification with a snooze option showing time remaining before a restart is enforced. Your snooze option may look different depending on your version of Configuration Manager.

![Pending restart Software Center notification with snooze button](media/3976435-snooze-restart-countdown.png)

Software Center final countdown notification that can't be closed by the user. The snooze button is grayed out.

![Software Center final countdown notification](media/3976435-final-restart-countdown.png)

## Device restart notifications in version 1902

<!--3555947-->
Sometimes users don't see the Windows toast notification about a restart or required deployment. Then they don't see the experience to snooze the reminder. This behavior can lead to a poor user experience when the client reaches a deadline.

Starting in version 1902, when software changes are required or deployments need a restart, you have the option of using a more intrusive dialog window.

In the [Computer Restart](/sccm/core/clients/deploy/about-client-settings#computer-restart) group of client settings, enable the following option: **When a deployment requires a restart, show a dialog window to the user instead of a toast notification**.  

Configuring this client setting changes the user experience for all required deployments that require a restart from the following toast notification:

![Toast notification that Restart required](media/3555947-restart-toast.png)  

To the following dialog window:

![Dialog window to Restart your computer](media/3555947-restart-dialog.png)


## Device restart notifications starting in version 1906
<!--3976435-->
Some admins prefer frequent restart notifications and a short time frame for allowing restarts to be postponed. Other admins allow users to postpone a restart for longer periods of time and want users to be notified of the pending restart infrequently. Configuration Manager version 1906 gives an admin additional control over the timing and frequency of restart notifications.







## Log files


## Next steps

- [Introduction application management](/sccm/apps/understand/introduction-to-application-management)
- [Introduction to operating system deployment](/sccm/osd/understand/introduction-to-operating-system-deployment)
- [Introduction to software updates management](/sccm/sum/understand/software-updates-introduction)
