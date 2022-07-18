---
title: Distribute referenced content
titleSuffix: Configuration Manager
description: Before clients run a task sequence that references content, distribute that content to distribution points.
ms.date: 04/08/2022
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.localizationpriority: medium
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Distribute referenced content

*Applies to: Configuration Manager (current branch)*

Before clients run a task sequence that references content, distribute that content to distribution points. At any time, you can select the task sequence and distribute its content to build a new list of reference packages for distribution. If you make changes to the task sequence with updated content, redistribute the content before it's available to clients.

## Distribute content

Use the following procedure to distribute the content that is referenced by a task sequence:

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Task Sequences** node.

1. In the **Task Sequence** list, select the task sequence that you want to distribute.

1. On the **Home** tab of the ribbon, in the **Deployment** group, select **Distribute Content**. This action starts the Distribute Content Wizard.

1. On the **General** page, verify that the correct task sequence is selected for distribution.

1. On the **Content** page, verify the content to distribute, such as the boot image referenced by the task sequence.

1. On the **Content Destination** page, specify the collections, distribution point, or distribution point group where you want to distribute the task sequence contents.

    > [!IMPORTANT]
    > If the task sequence that you selected references content that's already distributed to a specific distribution point, the wizard doesn't list that distribution point.

1. Complete the wizard.

## Prestage content

You can also prestage the content referenced in the task sequence. Configuration Manager creates a compressed, prestaged content file that contains the files, associated dependencies, and associated metadata for the content that you select. Then you manually import the content at a site server, secondary site, or distribution point. For more information about how to prestage content files, see [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).

## Next steps

[Reduce the size of task sequence policy](reduce-task-sequence-policy-size.md)

[Deploy a task sequence](deploy-a-task-sequence.md)
