---
title: Reduce task sequence policy size
titleSuffix: Configuration Manager
description: When the size of the task sequence policy exceeds 32 MB, the client fails to process the large policy. The client then fails to run the task sequence deployment. Manage the size of task sequence policy to reduce deployment failures.
ms.date: 04/08/2022
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.localizationpriority: medium
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Reduce the size of task sequence policy

*Applies to: Configuration Manager (current branch)*

<!--6982275-->
When the size of the task sequence policy exceeds 32 MB, the client fails to process the large policy. The client then fails to run the task sequence deployment. The size of the task sequence as stored in the site database is smaller, but can still cause problems if too large. When the client processes the entire task sequence policy, the expanded size can cause problems over 32 MB.

To check for the 32-MB task sequence policy size on clients, use [management insights](../../core/servers/manage/management-insights.md#operating-system-deployment).

Configuration Manager restricts the following actions for a task sequence in the site database that's greater than 2 MB in size:<!--6888853-->

- Save changes in the task sequence editor
- Save changes with PowerShell cmdlets
- Import a new task sequence
- Any other change using supported SDK methods

For example, if you try to save changes to a large task sequence, the task sequence editor will display an error.

> [!TIP]
> The behavior in version 2010 and later checks for the 2 MB size limit on the task sequence as stored in the site database. When the client processes the entire task sequence policy, the expanded size can cause problems over 32 MB. The management insights check for the 32 MB task sequence policy size.

When you view the list of task sequences in the Configuration Manager console, add the **Size (KB)** column. Use this column to identify large task sequences that can cause problems.<!--7645732-->

## Actions to reduce task sequence size

To help reduce the size of task sequences and task sequence deployment policies, take the following actions:

- Separate functional segments into child task sequences, and use the [Run Task Sequence](../understand/task-sequence-steps.md#child-task-sequence) step. Keep each task sequence less than 2 MB in the database. Each task sequence has a separate 32-MB limit on its policy size.

    > [!NOTE]
    > Reducing the total number of steps and groups in a task sequence has minimal impact on the policy size. Each step is generally a couple of KB in policy. Moving groups of steps to a child task sequence is more impactful.

- Reduce the number of software updates in deployments to the same collection as the task sequence.

- Instead of entering a script in the [Run PowerShell Script](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript) step, reference it via a package.

- There's an 8-KB limit on the size of the task sequence _environment_ when it runs. Review the usage of custom task sequence variables, which can also contribute to the policy size.

- As a last resort, split a complex, dynamic task sequence into separate task sequences with distinct deployments to different collections.

## Next steps

[Export and import task sequences](export-import-task-sequences.md)
