---
title: Associate users with a computer
titleSuffix: Configuration Manager
description: Configure Configuration Manager to associate users with destination computers when deploying operating systems.
ms.date: 08/17/2018
ms.service: configuration-manager
ms.subservice: osd
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Associate users with a destination computer in Configuration Manager

*Applies to: Configuration Manager (current branch)*

When you use Configuration Manager to deploy operating systems, you can associate users with the destination computer. This option works whether a single user or multiple users are the primary users of the destination computer.  

User device affinity supports user-centric management for when you deploy applications. When you associate a user with the destination computer on which to install an OS, you can later deploy applications to that user, and the applications automatically install on the destination computer. While you can configure support for user device affinity during OS deployment, you can't use user device affinity to deploy the OS.  

For more information about user device affinity, see [Link users and devices with user device affinity](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

There are several methods by which you can integrate user device affinity into your OS deployments. You can integrate user device affinity into PXE deployments, bootable media deployments, and pre-staged media deployments.  


### Create a task sequence that includes the **SMSTSAssignUsersMode** variable

Add the **SMSTSAssignUsersMode** variable to the beginning of your task sequence by using the [Set Task Sequence Variable](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) step. This variable specifies how the task sequence handles the user information.

For more information, see [Task sequence variables](../understand/task-sequence-variables.md#SMSTSAssignUsersMode).


### Create a prestart command that gathers the user information

The prestart command can be a VBScript with an input box. It can also be an HTML application (HTA) that validates the user data that they enter. 

This prestart command must set the **SMSTSUDAUsers** variable that's used when the task sequence runs. This variable can be set on a computer, a collection, or a task sequence variable.

For more information, see [Task sequence variables](../understand/task-sequence-variables.md#SMSTSUDAUsers).


### Configure how distribution points and media associate the user with the destination computer

The distribution point or media supports associating users with the destination computer where the OS is deployed. Use one of the following methods: 

- [Configure a distribution point to accept PXE boot requests](prepare-site-system-roles-for-operating-system-deployments.md#configuring-distribution-points-to-accept-pxe-requests)  
- [Create bootable media](../deploy-use/create-bootable-media.md)  
- [Create pre-staged media](../deploy-use/create-prestaged-media.md)  


Configuring user device affinity support doesn't have a built-in method to validate the user identity. This behavior is important when a technician is provisioning the computer and enters the information on behalf of the user. In addition to setting how task sequence handles the user information, configuring these options on the distribution point and media provides the ability to restrict the deployments that are started from a PXE boot or from a specific type of media.
