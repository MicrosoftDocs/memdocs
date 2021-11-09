---
title: Use Software Center to deploy Windows over the network
titleSuffix: Configuration Manager
description: Deploy an OS from Software Center to refresh an existing computer with a new version of Windows or to upgrade Windows to the latest version.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Use Software Center to deploy Windows over the network with Configuration Manager

*Applies to: Configuration Manager (current branch)*

You can make a task sequence that installs an OS available in Software Center. A user can run a task sequence from Software Center for the following OS deployment scenarios:

- [Refresh an existing computer with a new version of Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Upgrade Windows to the latest version](upgrade-windows-to-the-latest-version.md)

- [Create a task sequence for non-OS deployments](create-a-task-sequence-for-non-operating-system-deployments.md)

Complete the steps in one of those OS deployment scenarios. Then use the following sections to prepare for deployments that are available in Software Center.

## <a name="BKMK_Deploy"></a> Deploy the task sequence

Deploy the task sequence to a target collection. For more information, see [Deploy a task sequence](deploy-a-task-sequence.md).

On the **Deployment Settings** page of the deployment, for the **Make available to the following** setting, select one of the following options:

- Only Configuration Manager Clients

- Configuration Manager clients, media and PXE

Also configure whether the deployment is required or available:

- Required deployment: Required deployments make the task sequence available in Software Center. It automatically starts at the configured deadline.

- Available deployment: The task sequence is available in Software Center, and a user can install it on demand.

After you create the deployment, clients in the target collection will show the task sequence in Software Center.
    
> [!NOTE]
> If multiple users are signed in on the device, task sequence deployments might not appear in Software Center until other users are signed out.

## Next steps

[User experiences for OS deployment](../understand/user-experience.md#software-center)
