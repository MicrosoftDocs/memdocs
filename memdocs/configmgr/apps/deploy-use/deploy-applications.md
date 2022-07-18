---
title: Deploy applications
titleSuffix: Configuration Manager
description: Create or simulate a deployment of an application to a device or user collection
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Deploy applications with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Create or simulate a deployment of an application to a device or user collection in Configuration Manager. This deployment gives instructions to the Configuration Manager client on how and when to install or uninstall the software.

Before you can deploy an application, create at least one _deployment type_ for the application. For more information, see [Create deployment types for the application](create-applications.md#bkmk_create-dt).

In some situations, consider another feature as a better solution:

- If you have several applications that you need to deploy together, instead of creating multiple deployments, create an _application group_. You can send the app group to a user or device collection as a single deployment. For more information, see [Create application groups](create-app-groups.md).

- For more complex deployments, first test it with a _simulated deployment_. This simulation tests the applicability of a deployment without installing or uninstalling the application. A simulated deployment evaluates the detection method, requirements, and dependencies for a deployment type and reports the results in the **Deployments** node of the **Monitoring** workspace. For more information, see [Simulate application deployments](simulate-application-deployments.md).

    > [!NOTE]
    > You can only simulate the deployment of required applications, but not packages or software updates.
    >
    > On-prem MDM-enrolled devices don't support simulated deployments, user experience, or scheduling settings.

- _Phased deployments_ allow you to orchestrate a coordinated, sequenced rollout of software based on customizable criteria and groups. For example, deploy the application to a pilot collection, and then automatically continue the rollout based on success criteria. For more information, see [Create a phased deployment](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json).<!--1358147-->

## <a name="bkmk_deploy"></a> Start the deployment wizard

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select either the **Applications** or **Application Groups** node.

1. Select an application or application group from the list to deploy. In the ribbon, select **Deploy**.  

> [!NOTE]
> When you view the properties of an existing deployment, the following sections correspond to tabs of the deployment properties window:  
>
> - [General](#bkmk_deploy-general)
> - [Content](#bkmk_deploy-content)
> - [Deployment Settings](#bkmk_deploy-settings)
> - [Scheduling](#bkmk_deploy-sched)
> - [User Experience](#bkmk_deploy-ux)
> - [Alerts](#bkmk_deploy-alerts)

## <a name="bkmk_deploy-general"></a> General information

On the **General** page of the Deploy Software wizard, specify the following information:  

- **Software**: This value displays the application to deploy. Select **Browse** to choose a different application.  

- **Collection**: Select **Browse** to choose the target collection for this application deployment.

- **Use default distribution point groups associated to this collection**: Store the application content on the collection's default distribution point group. If you haven't associated the selected collection with a distribution point group, this option is grayed out.  

- **Automatically distribute content for dependencies**: If any of the deployment types in the application have dependencies, then the site also sends dependent application content to distribution points.  

    >[!NOTE]
    > If you update the dependent application after deploying the primary application, the site doesn't automatically distribute any new content for the dependency.

- **Comments (optional)**: Optionally, enter a description for this deployment.

## <a name="bkmk_deploy-content"></a> Content options

On the **Content** page, select **Add** to distribute the content for this application to a distribution point or a distribution point group.

If you selected the option to **Use default distribution points associated to this collection** on the General page, then this option is automatically populated. Only a member of the **Application Administrator** security role can modify it.

If the application content is already distributed, then they appear here.

## <a name="bkmk_deploy-settings"></a> Deployment settings

On the **Deployment Settings** page, specify the following information:

- **Action**: From the drop-down list, choose whether this deployment is to **Install** or **Uninstall** the application.

    > [!NOTE]
    > If you create a deployment to **Install** an app and another deployment to **Uninstall** the same app on the same device, the **Install** deployment takes priority.

    You can't change the action of a deployment after you create it.

- **Purpose**: From the drop-down list, choose one of the following options:

  - **Available**: The user sees the application in Software Center. They can install it on demand.

    > [!NOTE]
    > When you deploy apps as available to user collections, there are other requirements for some types of clients. For more information, see [Prerequisites to deploy user-available apps](../plan-design/prerequisites-deploy-user-available-apps.md).

  - **Required**: The client automatically installs the app according to the schedule that you set. If the application isn't hidden, a user can track its deployment status. They can also use Software Center to install the application before the deadline.

    > [!NOTE]
    > When you set the deployment action to **Uninstall**, the deployment purpose is automatically set to **Required**. You can't change this behavior.

- **Allow end users to attempt to repair this application**: If you created the application with a repair command line, enable this option. Users see an option in Software Center to **Repair** the application.<!--1357866-->

- **Uninstall this application if the targeted object falls out of the collection**: Starting in version 2107, when you remove the device from the target collection, Configuration Manager runs the uninstall program on that device. For more information, see [Implicit uninstall](uninstall-applications.md#implicit-uninstall). This option is only available for device-targeted deployments and when the deployment is **Required**.<!--3607457-->

- **Pre-deploy software to the user's primary device**: If the deployment is to a user, select this option to deploy the application to the user's primary device. This setting doesn't require the user to sign in before the deployment runs. If the user must interact with the installation, don't select this option. This option is only available when the deployment is **Required**.

- **Send wake-up packets**: If the deployment is **Required**, Configuration Manager sends a wake-up packet to computers before the client runs the deployment. This packet wakes the computers at the installation deadline time. Before using this option, computers and networks must be configured for Wake On LAN. For more information, see [Plan how to wake up clients](../../core/clients/deploy/plan/plan-wake-up-clients.md).

- **Allow clients on a metered Internet connection to download content after the installation deadline, which might incur additional costs**: This option is only available for deployments with a purpose of **Required**.

- **Automatically upgrade any superseded versions of this application**: The client upgrades any superseded version of the application with the superseding application.

    > [!NOTE]
    > This option works regardless of administrator approval. If an administrator already approved the superseded version, they don't need to also approve the superseding version. Approval is only for new requests, not superseding upgrades.<!--515824-->
    >
    > For **Available** install purpose, you can enable or disable this option. <!--1351266-->

### <a name="bkmk_approval"></a> Approval settings

The application approval behavior depends upon whether you enable the recommended optional feature, **Approve application requests for users per device**.

- **An administrator must approve a request for this application on the device**: If you enable the optional feature, the administrator approves any user requests for the application before the user can install it on the requested device. If the administrator approves the request, the user is only able to install the application on that device. The user must submit another request to install the application on another device. This option is grayed out when the deployment purpose is **Required**, or when you deploy the application to a device collection.

- **Require administrator approval if users request this application**: If you don't enable the optional feature, the administrator approves any user requests for the application before the user can install it. This option is grayed out when the deployment purpose is **Required**, or when you deploy the application to a device collection.  

For more information, see [Approve applications](app-approval.md).

### Deployment properties: Deployment settings

When you view the properties of a deployment, if supported by the deployment type technology, the following option appears on the **Deployment Settings** tab:

**Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**. For more information, see [check for running executable files before installing an application](check-for-running-executable-files.md).

## <a name="bkmk_deploy-sched"></a> Scheduling settings

On the **Scheduling** page, set the time when this application is deployed or available to client devices.

By default, Configuration Manager makes the deployment policy available to clients right away. If you want to create the deployment, but not make it available to clients until a later date, configure the option to **Schedule the application to be available**. Then select the date and time, including whether that's based on UTC or the client's local time.

If the deployment is **Required**, also specify the **Installation deadline**. By default this deadline is as soon as possible.

For example, you need to deploy a new line-of-business application. All users need to install it by a certain time, but you want to give them the option to opt in early. You also need to make sure that the site has distributed the content to all distribution points. You schedule the application to be available in five days from today. This schedule gives you time to distribute the content and confirm its status. You then set the installation deadline for one month from today. Users see the application in Software Center when it's available in five days. If they do nothing, the client automatically installs the application at the installation deadline.

If the application you're deploying supersedes another application, set the installation deadline when users receive the new application. Set the **Installation Deadline** to upgrade users with the superseded application.

### Delay enforcement with a grace period

You might want to give users more time to install required applications *beyond* any deadlines you set. This behavior is typically required when a computer is turned off for a long time, and needs to install many applications. For example, when a user returns from vacation, they have to wait for a long time as the client installs overdue deployments. To help solve this problem, define an enforcement grace period.

- First, configure this grace period with the property **Grace period for enforcement after deployment deadline (hours)** in client settings. For more information, see the [Computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent) group. Specify a value between **1** and **120** hours.  

- On the **Scheduling** page of a required application deployment, enable the option to **Delay enforcement of this deployment according to user preferences, up to the grace period defined in client settings**. The enforcement grace period applies to all deployments with this option enabled and targeted to devices to which you also deployed the client setting.

After the deadline, the client installs the application in the first non-business window, which the user configured, up to this grace period. However, the user can still open Software Center and install the application at any time. Once the grace period expires, enforcement reverts to normal behavior for overdue deployments.

:::image type="content" source="media/grace-period.svg" alt-text="DIagram of grace period timeline":::

<!-- SCCMDocs issue #1599 -->

> [!NOTE]
> Most of the time, this feature addresses the scenario when the device is powered off while the user is out of the office. Technically, the grace period starts when the client gets policy after the deployment deadline. The same behavior happens if you stop the Configuration Manager client service (CcmExec), and then restart it at some time after the deployment deadline.

## <a name="bkmk_deploy-ux"></a> User experience settings

On the **User Experience** page, specify information about how users can interact with the application installation.

- **User notifications**: Specify whether to display notification in Software Center at the configured available time. This setting also controls whether to notify users on the client computers. For available deployments, you can't select the option to **Hide in Software Center and all notifications**.  

  - **When software changes are required, show a dialog window to the user instead of a toast notification**<!--3555947-->: Select this option to change the user experience to be more intrusive. It only applies to required deployments. For more information, see [User notifications](../plan-design/user-notifications.md#replace-toast-notifications-with-dialog-window).

- **Software Installation** and **System restart**: Only configure these settings for required deployments. They specify the behaviors when the deployment reaches the deadline outside of any defined maintenance windows. For more information about maintenance windows, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).  

- **Write filter handling for Windows Embedded devices**: This setting controls the installation behavior on Windows Embedded devices that are enabled with a write filter. Choose the option to commit changes at the installation deadline or during a maintenance window. When you select this option, a restart is required and the changes persist on the device. Otherwise, the application is installed to the temporary overlay, and committed later.  

  - When you deploy a software update to a Windows Embedded device, make sure the device is a member of a collection that has a configured maintenance window. For more information about maintenance windows and Windows Embedded devices, see [Create Windows Embedded applications](../get-started/creating-windows-embedded-applications.md).  

## <a name="bkmk_deploy-alerts"></a> Alerts

On the **Alerts** page, configure how Configuration Manager generates alerts for this deployment. If you're also using System Center Operations Manager, configure its alerts as well. You can only configure some alerts for required deployments.

## Next steps

- [Monitor applications](monitor-applications-from-the-console.md)
- [Disable and delete application deployments](disable-delete-deployments.md)
- [Troubleshoot application deployments](/troubleshoot/mem/configmgr/troubleshoot-application-deployment?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)
- [Common error codes for app installation](../../tenant-attach/app-install-error-reference.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)
- [Management tasks for applications](management-tasks-applications.md)
- [Software Center user guide](../../core/understand/software-center.md)

> [!NOTE]
> This article used to include more sections, which have moved to the following articles:
>
> - [Delete a deployment](disable-delete-deployments.md)
> - [User notifications for required deployments](../plan-design/user-notifications.md)
> - [Check for running executable files](check-for-running-executable-files.md)
> - [Deploy user-available apps](../plan-design/prerequisites-deploy-user-available-apps.md)
