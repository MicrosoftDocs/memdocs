---
title: Deploy a task sequence
titleSuffix: Configuration Manager
description: Use this information to deploy a task sequence to the computers in a collection.
ms.date: 04/05/2021
ms.service: configuration-manager
ms.subservice: osd
ms.topic: how-to
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Deploy a task sequence

*Applies to: Configuration Manager (current branch)*

After you create a task sequence, and distribute the referenced content, deploy it to a device collection. This action allows the task sequence to run on a device. A deployed task sequence can run automatically, or when installed by a user of the device.

> [!WARNING]
> You can manage the behavior for high-risk task sequence deployments. A high-risk deployment is a deployment that is automatically installed and has the potential to cause unwanted results. For example, a task sequence that has a purpose of **Required** that deploys an OS is considered a high-risk deployment. For more information, see [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

## Process

Use the following procedure to deploy a task sequence to the computers in a collection.

> [!NOTE]
> The status messages for the task sequence deployment are displayed in the message window on a primary site, but they aren't displayed on a central administration site.

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Operating Systems**, and then select the **Task Sequences** node.

1. In the **Task Sequence** list, select the task sequence that you want to deploy.

1. On the **Home** tab of the ribbon, in the **Deployment** group, select **Deploy**.

    > [!NOTE]
    > If **Deploy** isn't available, the task sequence has a reference that's not valid. Correct the reference and then try to deploy the task sequence again.

1. On the **General** page, specify the following information.

    - **Task sequence**: Specify the task sequence to deploy. By default, this box displays the selected task sequence.

    - **Collection**: Select the collection that contains the computers to run the task sequence.

        Don't deploy a task sequence that installs an OS to inappropriate collections, such as a collection of all your data center servers. Be sure that the selected collection contains only those computers that you want to run the task sequence.

        For more information about high-risk deployments, see [High-risk deployments](#bkmk_high-risk).

    - **Use default distribution point groups associated to this collection**: Store the task sequence content on the collection's default distribution point group. If you haven't associated the selected collection with a distribution point group, this option is grayed out.

    - **Automatically distribute content for dependencies**: If any referenced content has dependencies, then the site also sends dependent content to distribution points.

    - **Pre-download content for this task sequence**: For more information, see [Configure pre-cache content](configure-precache-content.md).

    - **Select Deployment Template**: Save and specify a deployment template for a task sequence.<!--1357391-->

        > [!IMPORTANT]
        > Some items aren't saved in the template.<!--510610--> Make sure you apply the following items when you run the deployment wizard:
        >
        > - Software Installation
        > - Scheduling
        > - Pre-download content

    - **Comments (optional)**: Specify additional information that describes this deployment of the task sequence.

1. On the **Deployment Settings** page, specify the following information:

    - **Purpose**: From the drop-down list, choose one of the following options:

        - **Available**: The user sees the task sequence in Software Center and can install it on demand.

        - **Required**: Configuration Manager automatically runs the task sequence according to the configured schedule. If the task sequence isn't hidden, a user can still track its deployment status. They can also use Software Center to install the task sequence before the deadline.

        > [!NOTE]
        > If multiple users are signed into the device, package and task sequence deployments may not appear in Software Center.

    - **Make available to the following**: Specify whether the task sequence is available to one of the following types:

        - Only Configuration Manager clients
        - Configuration Manager clients, media, and PXE
        - Only media and PXE
        - Only media and PXE (hidden)

        > [!IMPORTANT]
        > Use the **Only media and PXE (hidden)** setting for automated task sequence deployments. To have the computer automatically boot to the deployment with no user interaction, select **Allow unattended operating system deployment** and set the **SMSTSPreferredAdvertID** variable as part of the media. For more information about task sequence variables, see [Task sequence variables](../understand/task-sequence-variables.md#SMSTSPreferredAdvertID).

    - **Send wake-up packets**: If the deployment is **Required** and you select this option, the site sends a wake-up packet to computers before the client runs the deployment. This packet wakes the computer from sleep at the installation deadline time. Before using this option, computers and networks must be configured for Wake On LAN. For more information, see [Plan how to wake up clients](../../core/clients/deploy/plan/plan-wake-up-clients.md).

    - **Allow clients on a metered Internet connection to download content after the installation deadline, which might incur additional costs**: This option is only available for **Required** deployments. When you have a custom task sequence that installs an application but doesn't deploy an OS, you can specify whether to allow clients to download content after an installation deadline when they use metered internet connections. Internet providers sometimes charge by the amount of data that you use when you're on a metered internet connection.

        > [!NOTE]
        > While using a metered internet connection might work for task sequences that don't deploy an OS, it's not supported.

1. On the **Scheduling** page, specify the following information:

    > [!IMPORTANT]
    > When a Windows PE client starts from PXE or boot media, the client doesn't evaluate deployment schedules. These schedules include start, expire, and deadline times. Only configure schedules in deployments to clients that start from the full Windows OS. Consider using other methods, such as maintenance windows, to control active task sequences deployed to clients that start from Windows PE.

    - **Schedule when this deployment will become available**: Specify the date and time when the task sequence is available to run on the destination computer. When you select the **UTC** option, the task sequence is available for multiple computers at the same time. Otherwise the deployment is available at different times, according to the local time on each computer.

        If the start time is earlier than the required time, the client downloads the task sequence content at the start time.

    - **Schedule when this deployment will expire**: Specify the date and time when the task sequence expires on the destination computer. When you select the **UTC** option, the task sequence expires on multiple destination computers at the same time. Otherwise the deployment expires at different times, according to the local time on each computer.

    - **Assignment schedule**: For a **Required** deployment, specify when the client runs the task sequence. You can add multiple schedules. The assignment schedule can have one of the following configurations:

        - A specific date and time
        - Monthly, weekly, or custom recurrence pattern
        - As soon as possible
        - Log on or log off events

        > [!NOTE]
        > If you schedule a start time for a required deployment that's earlier than the date and time when the task sequence is available, the Configuration Manager client downloads the content at the assigned start time. This behavior occurs even though you scheduled the task sequence to be available at a later time.<!--SCCMDocs issue 777-->

    - **Rerun behavior**: Specify when the task sequence reruns. Select one of the following options:

        - **Never rerun deployed program**: If the client has previously run the task sequence, it doesn't rerun. The task sequence doesn't rerun even if it originally failed or the task sequence files have changed.

        - **Always rerun program**: The task sequence always reruns on the client when the deployment is scheduled. It reruns even if the task sequence has already run successfully. This setting is useful when you use recurring deployments in which the task sequence is routinely updated.

            > [!IMPORTANT]
            > This option is selected by default. However, it has no effect until you assign a required deployment. A user can always rerun available deployments.

        - **Rerun if failed previous attempt**: The task sequence reruns when the deployment is scheduled, only if it previously failed to run. This setting is useful for a required deployment. If the last attempt to run was unsuccessful, it automatically tries to rerun according to the assignment schedule.

        - **Rerun if succeeded on previous attempt**: The task sequence reruns only if it previously ran successfully on the client. This setting is useful when you use recurring deployments in which the task sequence is routinely updated, and each update requires that the previous update is installed successfully.

        > [!NOTE]
        > A user can rerun an available task sequence deployment. Before you deploy an available task sequence in a production environment, first test what happens if a user reruns the task sequence multiple times.

1. On the **User Experience** page, specify the following information:

    - **Allow user to run the program independently of assignments**: Specify whether a user can run a required deployment outside of the assignment schedule. This option is always enabled for available deployments.

    - **Show Task Sequence progress**: Specify whether the Configuration Manager client displays the progress of the task sequence.

    - **Software installation**: Specify whether the user is allowed to install software outside a configured maintenance window after the scheduled time.

    - **System restart (if required to complete the installation)**: Specify whether the user is allowed to restart the computer after a software installation outside a configured maintenance window after the assignment time.

    - **Write filter handling for Windows Embedded devices**: This setting controls the installation behavior on Windows Embedded devices that are enabled with a write filter. Choose the option to commit changes at the installation deadline or during a maintenance window. When you select this option, a restart is required and the changes persist on the device. Otherwise, the application is installed to the temporary overlay, and committed later. When you deploy a task sequence to a Windows Embedded device, make sure the device is a member of a collection that has a configured maintenance window.

    - **Allow task sequence to run for client on the Internet**: Specify whether the task sequence is allowed to run on an internet-based client. For more information, see [Deploy a task sequence over the internet](deploy-task-sequence-over-internet.md#allow-task-sequence-to-run-on-internet).

1. On the **Alerts** page, specify the alert settings that you want for this task sequence deployment.

1. On the **Distribution Points** page, specify the following information:

    - **Deployment options**: For more information, see [Deployment options](#bkmk_deploy-options).

    - **Allow clients to use distribution points from the neighbor boundary group**: Specify whether clients can use distribution points from a neighbor boundary group to download the content that's required by the task sequence.

    - **Allow clients to use distribution points from the default site boundary group**: Specify if clients should download content from a distribution point in the site default boundary group, when it isn't available from a distribution point in the current or neighbor boundary groups.

        > [!NOTE]
        > When a device runs a task sequence and needs to acquire content, it uses boundary group behaviors similar to the Configuration Manager client. For more information, see [Task sequence support for boundary groups](../../core/servers/deploy/configure/boundary-groups-distribution-points.md#task-sequence-support).<!--1359025-->

1. Starting in version 2103, if you use a feature update with the **Upgrade OS** task sequence step, the wizard also includes the **Deployment Package** page.<!--3555906--> Select one of the following options:

    - **Select a deployment package**: Add the feature updates to an existing deployment package.

    - **Create a new deployment package**: Add the feature updates to a new deployment package.

    - **No deployment package**: When clients run the task sequence, they download the feature update from peers or the Microsoft cloud.

    For more information on these options, see step 11 for the **Deployment Package** page when you [Create an automatic deployment rule (ADR)](../../sum/deploy-use/automatically-deploy-software-updates.md).

1. To save these settings to use again, on the **Summary** tab select **Save As Template**. Supply a name for the template and select the settings to save.

1. Complete the wizard.

### <a name="bkmk_deploy-options"></a> Deployment options

<!-- MEMDocs#328, SCCMDocs#2114 -->

These options are on the **Distribution Points** tab of the task sequence deployment. They're dynamic based upon other selections in the deployment and attributes of the task sequence. You may not always see all options.

> [!NOTE]  
> When you use multicast to deploy an OS, download the content to the computers either as needed or before the task sequence runs.  

- **Download content locally when needed by the running task sequence**: Specify that clients download content from the distribution point as it's needed by the task sequence. The client starts the task sequence. When a step in the task sequence requires content, it's downloaded before the step runs.  

- **Download all content locally before starting task sequence**: Specify that clients download all the content from the distribution point before the task sequence runs. If you make the task sequence available to PXE and boot media deployments on the **Deployment Settings** page, this option isn't shown.  

- **Access content directly from a distribution point when needed by the running task sequence**: Specify that clients run the content from the distribution point. This option is only available when you enable all packages associated with the task sequence to use a package share on the distribution point. To enable content to use a package share, see the **Data Access** tab in the **Properties** for each package.  

> [!IMPORTANT]  
> For greatest security, select the options to **Download content locally when needed by the running task sequence** or **Download all content locally before starting task sequence**. When you select either of these options, Configuration Manager hashes the package, so that it can ensure package integrity. When you select the option to **Access content directly from a distribution point when needed by the running task sequence**, Configuration Manager doesn't verify the package hash prior to running the specified program. Because the site can't ensure package integrity, it's possible for users with administrative rights to alter or tamper with package contents.  

#### Example 1: One deployment option

You deploy an OS deployment task sequence that wipes the disk and applies an image. On the **Deployment Settings** page, you make it available to an option that includes media and PXE:

:::image type="content" source="media/deploy-setting-make-available.png" alt-text="Deploy task sequence, make available to the following":::

On the **Distribution Points** page, there's only one deployment option:

- **Download content locally when needed by the running task sequence**

:::image type="content" source="media/deploy-option-1.png" alt-text="Deploy task sequence, one deployment option":::

The option to **Download all content locally before starting task sequence** isn't available because the deployment is made available to media and PXE.

The option to **Access content directly from a distribution point when needed by the running task sequence** isn't available. Not all of the referenced content uses a package share.

#### Example 2: Two deployment options

You deploy an OS deployment task sequence that wipes the disk and applies an image. On the **Deployment Settings** page, you make it available to **Only Configuration Manager clients**. On the **Distribution Points** page, there are two deployment options available:

- **Download content locally when needed by the running task sequence**
- **Download all content locally before starting task sequence**

:::image type="content" source="media/deploy-option-2.png" alt-text="Deploy task sequence, two deployment options":::

The option to **Access content directly from a distribution point when needed by the running task sequence** isn't available. Not all of the referenced content uses a package share.

#### Example 3: Three deployment options

You have several packages with administrative scripts and associated content. On the **Data Access** tab of the package properties, you configure all of them to **Copy the content in this package to a package share on distribution points**.

You create a task sequence that only has several **Install Package** steps for these script packages, and the deploy it. On the **Deployment Settings** page, the only option is to make available to **Only Configuration Manager clients**. This option is the only available. The task sequence isn't for OS deployment, because it doesn't have a boot image associated with it. On the **Distribution Points** page, there are three deployment options available:

- **Download content locally when needed by the running task sequence**
- **Download all content locally before starting task sequence**
- **Access content directly from a distribution point when needed by the running task sequence**

:::image type="content" source="media/deploy-option-3.png" alt-text="Deploy task sequence, three deployment options":::

## Deploy Windows in-place upgrade via CMG

<!-- 1357149 -->
The Windows in-place upgrade task sequence supports deployment to internet-based clients managed through the [cloud management gateway](../../core/clients/manage/cmg/overview.md) (CMG). This ability allows remote users to more easily upgrade Windows without needing to connect to the intranet.

For more information, see [Deploy a task sequence over the internet](deploy-task-sequence-over-internet.md#deploy-windows-in-place-upgrade-via-cmg).

## <a name="bkmk_high-risk"></a> High-risk deployments

When you deploy a high-risk deployment, such as an OS, the **Select Collection** window displays only the custom collections that meet the deployment verification settings that are configured in the site's properties. High-risk deployments are always limited to custom collections, collections that you create, and the built-in **Unknown Computers** collection. When you create a high-risk deployment, you can't select a built-in collection such as **All Systems**. To see all custom collections that contain fewer clients than the configured maximum size, disable the option to **Hide collections with a member count greater than the site's minimum size configuration**. For more information, see [Settings to manage high-risk deployments](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

The deployment verification settings are based on the current membership of the collection. After you deploy the task sequence, Configuration Manager doesn't reevaluate the collection membership for the high-risk deployment settings.  

For example, let's say you set **Default size** to 100 and the **Maximum size** to 1000. When you create a high risk deployment, the **Select Collection** window only displays collections that contain fewer than 100 clients. If you clear the **Hide collections with a member count greater than the site's minimum size configuration** setting, the window displays collections that contain fewer than 1000 clients.  

When you select a collection that contains a site role, the following behavior applies:  

- If the collection contains a site system server, and you configured the deployment verification settings to block collections with site system servers, then an error occurs. You can't continue creating the deployment.  

- If one of the following criteria applies, then the Deploy Software Wizard displays a high-risk warning. To continue, you need to agree to create a high-risk deployment. The site generates an audit status message.  

  - If the collection contains a site system server, and you configured the deployment verification settings to warn on collections with site system servers  

  - If the collection exceeds the default size value

  - If the collection contains a server  

## Next steps

[Monitor OS deployments](monitor-operating-system-deployments.md)

[Debug a task sequence](debug-task-sequence.md)
