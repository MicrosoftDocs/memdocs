---
title: Manage user state
titleSuffix: Configuration Manager
description: Configuration Manager uses the User State Migration Tool to capture and restore user state data in OS deployment scenarios.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Manage user state in Configuration Manager

*Applies to: Configuration Manager (current branch)*

You can use Configuration Manager task sequences to capture and restore the user state data in OS deployment scenarios where you want to keep the user state of the current OS. For example:

- Deployments where you want to capture the user state from one computer to restore it on another computer.

- Update deployments where you want to capture and restore the user state on the same computer.

Configuration Manager uses the User State Migration Tool (USMT) 10.0 to manage the migration of user state data from a source computer to a destination computer after the operating system installation completes. For more information about common migration scenarios for the USMT 10.0, see  [Common Migration Scenarios](/windows/deployment/usmt/usmt-common-migration-scenarios).

## Capture user state data

When you capture user state, you can store the user state data on the destination computer or on a state migration point. To store the user state on a state migration point, first configure a site system server to host the role. To store the user state on the destination computer, configure the task sequence to store the data locally using links.

> [!NOTE]
> The links that Windows uses to store the user state locally are referred to as _hard-links_. A hard-link migration store is a USMT 10.0 feature. It scans the computer for user files and settings and then creates a directory of hard-links to those files. USMT then uses the hard-links to restore the user data after the task sequence deploys the new OS.

> [!IMPORTANT]
> You can't use a state migration point and use hard-links to store the user state data at the same time.

When USMT captures the user state, it can store the information in one of the following ways:

- Store the data remotely on a state migration point. The **Capture User State** task sequence step sends the data to the server. After the task sequence deploys the OS, the **Restore User State** step downloads the data from the server and restores the user state on the destination computer.

- Store the data locally to a specific location. In this scenario, the **Capture User State** step copies the user data to a specific location on the destination computer. After the task sequence deploys the OS, the **Restore User State** step gets the user data from that local location.

- Use hard-links. In this scenario, the user state data remains on the drive when the task sequence removes the old OS. After the task sequence deploys the OS, the **Restore User State** step uses the hard-links to restore the user state data to its original location.

### Store user state data on a state migration point

To store the user state data on a state migration point, use the following steps:

1. Configure a [state migration point](#the-state-migration-point) to store the user state data.

1. Create a [computer association](#computer-associations) between the source computer and the destination computer. Create this association before you capture the user state on the source computer.

1. [Create a task sequence to capture and restore user state](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Specifically, add the following task sequence steps to capture user data from a computer, store the user date on a state migration point, and restore the user data to a computer:

    - [Request State Store](../understand/task-sequence-steps.md#BKMK_RequestStateStore): Requests access to a state migration point when capturing state from a computer or restoring state to a computer.

    - [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState): Runs USMT to capture and store the user state data on the state migration point.

    - [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState): Runs USMT to restore the data from a state migration point to the destination computer.

    - [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore): Notifies the state migration point that the capture or restore action is complete.

### Store user data locally

To store the user state data locally, [create a task sequence to capture and restore user state](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Specifically, add the following task sequence steps to capture user data from a computer and restore it:

- [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState): Run USMT to capture and store the user state to a local folder, with or without hard-links.

- [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState): Run USMT to restore the data from the local store to the destination computer.

  > [!NOTE]
  > The user state data that the hard-links reference remains on the computer after the task sequence removes the old OS.

## The state migration point

The state migration point stores user state data. The task sequence captures it from one computer and then restores it on another computer. When you capture user settings for an OS deployment on the same computer, you can store the data on the same computer by using hard-links or you can use a state migration point. For some deployments, when you create the state store, Configuration Manager automatically creates an association between the state store and the destination computer.

For more information about the state migration point and the steps to configure it, see [State migration point](prepare-site-system-roles-for-operating-system-deployments.md#state-migration-point).

## Computer associations

You use a computer association when you install an OS on new hardware and restore user data settings from another computer. The association defines the relationship between the source and destination computers. The source computer is an existing computer that Configuration Manager manages. It has the original user state. The destination computer is a new computer with a new OS. You restore the user state to the destination computer.

> [!NOTE]
> It's not supported to create a computer association between computers located in a Configuration Manager parent site with computers located in a child site. Computer associations are site specific and don't replicate.

### Create a computer association

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **User State Migration** node.

1. On the **Home** tab, in the **Create** group, select **Create Computer Association**.

1. On the **Computer Association** tab:

    1. For the **Source computer**, select **Search**. Locate and select the existing computer that has the user state.

    1. Repeat this process for the **Destination computer**. You may need to [Import computer information](../../core/clients/manage/manage-clients.md#import-computer-information) to predefine the device record.

1. Switch to the **User Accounts** tab to specify the user accounts to migrate to the destination computer. Select one of the following migration behaviors:

    - **Capture and restore all user accounts**: Use this option to create multiple associations to the same source computer.

    - **Capture all user accounts and restore specified accounts**: This option captures all user accounts from the source computer and only restores the accounts that you specify to the destination computer. You can also use this setting to create multiple associations to the same source computer.

    - **Capture and restore specified user accounts**: This option captures and restores only the accounts that you specify. When you select this option, you can't create multiple associations to the same source computer. This value is the default option.

    Select the new button (gold asterisk) to add user accounts from Active Directory.

## When a deployment fails

If the OS deployment fails, use the USMT 10.0 LoadState tool to manually get the user state data that the task sequence captured. Use this process for data stored on a state migration point or saved locally on the computer. For more information on command-line options, see [LoadState Syntax](/windows/deployment/usmt/usmt-loadstate-syntax).

## Next steps

[State migration point](prepare-site-system-roles-for-operating-system-deployments.md#state-migration-point)

[Create a task sequence to capture and restore user state](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)
