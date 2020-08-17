---
title: Deploy applications
titleSuffix: Configuration Manager
description: Create or simulate a deployment of an application to a device or user collection
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: how-to
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Deploy applications with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Create or simulate a deployment of an application to a device or user collection in Configuration Manager. This deployment gives instructions to the Configuration Manager client on how and when to install the software.

Before you can deploy an application, create at least one deployment type for the application. For more information, see [Create applications](create-applications.md).

Starting in version 1906, you can create a group of applications that you can send to a user or device collection as a single deployment. For more information, see [Create application groups](create-app-groups.md).

You can also simulate an application deployment. This simulation tests the applicability of a deployment without installing or uninstalling the application. A simulated deployment evaluates the detection method, requirements, and dependencies for a deployment type and reports the results in the **Deployments** node of the **Monitoring** workspace. For more information, see [Simulate application deployments](simulate-application-deployments.md).

> [!NOTE]
> You can only simulate the deployment of required applications, but not packages or software updates.
>
> MDM-enrolled devices don't support simulated deployments, user experience, or scheduling settings.

## <a name="bkmk_deploy"></a> Deploy an application

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

### <a name="bkmk_deploy-general"></a> Deployment **General** information

On the **General** page of the Deploy Software wizard, specify the following information:  

- **Software**: This value displays the application to deploy. Select **Browse** to choose a different application.  

- **Collection**: Select **Browse** to choose the target collection for this application deployment.

- **Use default distribution point groups associated to this collection**: Store the application content on the collection's default distribution point group. If you haven't associated the selected collection with a distribution point group, this option is grayed out.  

- **Automatically distribute content for dependencies**: If any of the deployment types in the application have dependencies, then the site also sends dependent application content to distribution points.  

    >[!NOTE]
    > If you update the dependent application after deploying the primary application, the site doesn't automatically distribute any new content for the dependency.

- **Comments (optional)**: Optionally, enter a description for this deployment.

### <a name="bkmk_deploy-content"></a> Deployment **Content** options

On the **Content** page, select **Add** to distribute the content for this application to a distribution point or a distribution point group.

If you selected the option to **Use default distribution points associated to this collection** on the General page, then this option is automatically populated. Only a member of the **Application Administrator** security role can modify it.

If the application content is already distributed, then they appear here.

### <a name="bkmk_deploy-settings"></a> **Deployment Settings**

On the **Deployment Settings** page, specify the following information:  

- **Action**: From the drop-down list, choose whether this deployment is to **Install** or **Uninstall** the application.  

    > [!NOTE]  
    > If you create a deployment to **Install** an app and another deployment to **Uninstall** the same app on the same device, the **Install** deployment takes priority.  

    You can't change the action of a deployment after you create it.  

- **Purpose**: From the drop-down list, choose one of the following options:  

  - **Available**: The user sees the application in Software Center. They can install it on demand.  

  - **Required**: The client automatically installs the app according to the schedule that you set. If the application isn't hidden, a user can track its deployment status. They can also use Software Center to install the application before the deadline.  

    > [!NOTE]  
    > When you set the deployment action to **Uninstall**, the deployment purpose is automatically set to **Required**. You can't change this behavior.  

- **Allow end users to attempt to repair this application**: Starting in version 1810, if you created the application with a repair command line, enable this option. Users see an option in Software Center to **Repair** the application.<!--1357866-->  

- **Pre-deploy software to the user's primary device**: If the deployment is to a user, select this option to deploy the application to the user's primary device. This setting doesn't require the user to sign in before the deployment runs. If the user must interact with the installation, don't select this option. This option is only available when the deployment is **Required**.  

- **Send wake-up packets**: If the deployment is **Required**, Configuration Manager sends a wake-up packet to computers before the client runs the deployment. This packet wakes the computers at the installation deadline time. Before using this option, computers and networks must be configured for Wake On LAN. For more information, see [Plan how to wake up clients](../../core/clients/deploy/plan/plan-wake-up-clients.md).  

- **Allow clients on a metered Internet connection to download content after the installation deadline, which might incur additional costs**: This option is only available for deployments with a purpose of **Required**.  

- **Automatically upgrade any superseded version of this application**: The client upgrades any superseded version of the application with the superseding application.

    > [!NOTE]
    > This option works regardless of administrator approval. If an administrator already approved the superseded version, they don't need to also approve the superseding version. Approval is only for new requests, not superseding upgrades.<!--515824-->  
    >
    > For **Available** install purpose, you can enable or disable this option. <!--1351266-->

#### <a name="bkmk_approval"></a> Approval settings

The application approval behavior depends upon whether you enable the recommended optional feature, **Approve application requests for users per device**.

- **An administrator must approve a request for this application on the device**: If you enable the optional feature, the administrator approves any user requests for the application before the user can install it on the requested device. If the administrator approves the request, the user is only able to install the application on that device. The user must submit another request to install the application on another device. This option is grayed out when the deployment purpose is **Required**, or when you deploy the application to a device collection.

- **Require administrator approval if users request this application**: If you don't enable the optional feature, the administrator approves any user requests for the application before the user can install it. This option is grayed out when the deployment purpose is **Required**, or when you deploy the application to a device collection.  

For more information, see [Approve applications](app-approval.md).

#### Deployment properties **Deployment Settings**

When you view the properties of a deployment, if supported by the deployment type technology, the following option appears on the **Deployment Settings** tab:

**Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**. For more information, see [check for running executable files before installing an application](#bkmk_exe-check).

### <a name="bkmk_deploy-sched"></a> Deployment **Scheduling** settings

On the **Scheduling** page, set the time when this application is deployed or available to client devices.

By default, Configuration Manager makes the deployment policy available to clients right away. If you want to create the deployment, but not make it available to clients until a later date, configure the option to **Schedule the application to be available**. Then select the date and time, including whether that's based on UTC or the client's local time.

If the deployment is **Required**, also specify the **Installation deadline**. By default this deadline is as soon as possible.

For example, you need to deploy a new line-of-business application. All users need to install it by a certain time, but you want to give them the option to opt in early. You also need to make sure that the site has distributed the content to all distribution points. You schedule the application to be available in five days from today. This schedule gives you time to distribute the content and confirm its status. You then set the installation deadline for one month from today. Users see the application in Software Center when it's available in five days. If they do nothing, the client automatically installs the application at the installation deadline.

If the application you're deploying supersedes another application, set the installation deadline when users receive the new application. Set the **Installation Deadline** to upgrade users with the superseded application.

#### Delay enforcement with a grace period

You might want to give users more time to install required applications *beyond* any deadlines you set. This behavior is typically required when a computer is turned off for a long time, and needs to install many applications. For example, when a user returns from vacation, they have to wait for a long time as the client installs overdue deployments. To help solve this problem, define an enforcement grace period.

- First, configure this grace period with the property **Grace period for enforcement after deployment deadline (hours)** in client settings. For more information, see the [Computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent) group. Specify a value between **1** and **120** hours.  

- On the **Scheduling** page of a required application deployment, enable the option to **Delay enforcement of this deployment according to user preferences, up to the grace period defined in client settings**. The enforcement grace period applies to all deployments with this option enabled and targeted to devices to which you also deployed the client setting.

After the deadline, the client installs the application in the first non-business window, which the user configured, up to this grace period. However, the user can still open Software Center and install the application at any time. Once the grace period expires, enforcement reverts to normal behavior for overdue deployments.

:::image type="content" source="media/grace-period.svg" alt-text="DIagram of grace period timeline":::

<!-- SCCMDocs issue #1599 -->

> [!NOTE]
> Most of the time, this feature addresses the scenario when the device is powered off while the user is out of the office. Technically, the grace period starts when the client gets policy after the deployment deadline. The same behavior happens if you stop the Configuration Manager client service (CcmExec), and then restart it at some time after the deployment deadline.

### <a name="bkmk_deploy-ux"></a> Deployment **User Experience** settings

On the **User Experience** page, specify information about how users can interact with the application installation.

- **User notifications**: Specify whether to display notification in Software Center at the configured available time. This setting also controls whether to notify users on the client computers. For available deployments, you can't select the option to **Hide in Software Center and all notifications**.  

  - **When software changes are required, show a dialog window to the user instead of a toast notification**<!--3555947-->: Starting in version 1902, select this option to change the user experience to be more intrusive. It only applies to required deployments. For more information, see [Plan for Software Center](../plan-design/plan-for-software-center.md#bkmk_impact).

- **Software Installation** and **System restart**: Only configure these settings for required deployments. They specify the behaviors when the deployment reaches the deadline outside of any defined maintenance windows. For more information about maintenance windows, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).  

- **Write filter handling for Windows Embedded devices**: This setting controls the installation behavior on Windows Embedded devices that are enabled with a write filter. Choose the option to commit changes at the installation deadline or during a maintenance window. When you select this option, a restart is required and the changes persist on the device. Otherwise, the application is installed to the temporary overlay, and committed later.  

  - When you deploy a software update to a Windows Embedded device, make sure the device is a member of a collection that has a configured maintenance window. For more information about maintenance windows and Windows Embedded devices, see [Create Windows Embedded applications](../get-started/creating-windows-embedded-applications.md).  

### <a name="bkmk_deploy-alerts"></a> Deployment **Alerts**

On the **Alerts** page, configure how Configuration Manager generates alerts for this deployment. If you're also using System Center Operations Manager, configure its alerts as well. You can only configure some alerts for required deployments.

## <a name="bkmk_phased"></a> Create a phased deployment

<!--1358147-->
Phased deployments allow you to orchestrate a coordinated, sequenced rollout of software based on customizable criteria and groups. For example, deploy the application to a pilot collection, and then automatically continue the rollout based on success criteria.

For more information, see the following articles:  

- [Create a phased deployment](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Manage and monitor phased deployments](../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

## <a name="bkmk_delete"></a> Delete a deployment

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select either the **Applications** or **Application Groups** node.  

1. Select the application or application group that includes the deployment you want to delete.  

1. Switch to the **Deployments** tab of the details pane, and select the deployment.  

1. In the ribbon, on the **Deployment** tab in the **Deployment** group, select **Delete**.  

When you delete an application deployment, any instances of the application that clients have already installed aren't removed. To remove these applications, deploy the application to computers to **Uninstall**. If you delete an application deployment, the application is no longer visible in Software Center. The same behavior happens when you remove a resource from the target collection for the deployment.

## <a name="bkmk_notify"></a> User notifications for required deployments

When users receive required software, and select the **Snooze and remind me** setting, they can choose from the following options:  

- **Later**: Specifies that notifications are scheduled based on the notification settings configured in client settings.  

- **Fixed time**: Specifies that the notification is scheduled to display again after the selected time. For example, if you select 30 minutes, the notification displays again in 30 minutes.  

:::image type="content" source="media/ComputerAgentSettings.png" alt-text="Computer Agent group in default client settings":::

The maximum snooze time is always based on the notification values configured in the client settings at every time along the deployment timeline. For example:  

- You configure the **Deployment deadline greater than 24 hours, remind users every (hours)** setting on the **Computer Agent** page for 10 hours.  

- The client displays the notification dialog more than 24 hours before the deployment deadline.  

- The dialog shows snooze options up to but never greater than 10 hours.  

- As the deployment deadline approaches, the dialog shows fewer options. These options are consistent with the relevant client settings for each component of the deployment timeline.  

For a high-risk deployment, such as a task sequence that deploys an OS, the user notification experience is more intrusive. Instead of a transient taskbar notification, a dialog box like the following displays each time you're notified that critical software maintenance is required:

:::image type="content" source="media/client-toast-notification.png" alt-text="Required software dialog notifies you of critical software maintenance":::

## <a name="bkmk_exe-check"></a> Check for running executable files

Configure a deployment to check if certain executable files are running on the client. Use this option to check for processes that might disrupt the installation of the application. If one of these executable files is running, the client blocks the installation of the deployment type. The user must close the running executable file before the client can install the deployment type. For deployments with a purpose of required, the client can automatically close the running executable file.

1. Open the **Properties** for the deployment type.

1. Switch to the **Install Behavior** tab, and select **Add**.

1. In the **Add Executable File** window, enter the name of the target executable file. Optionally, enter a friendly name for the application to help you identify it in the list.

1. Select **OK** to save and close the deployment type properties window.

1. When you deploy the application, select the option to **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**. This option is on the **Deployment Settings** tab of the deployment properties.  

> [!NOTE]
> If you configure an application to check for running executable files, and include it in the [Install Application](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) task sequence step, the task sequence will fail to install it. If you don't configure this task sequence step to continue on error, then the entire task sequence fails.

### Client behaviors and user notifications

After clients receive the deployment, the following behavior applies:  

- If you deployed the application as **Available**, and a user tries to install it, the client prompts the user to close the specified running executable files before proceeding with the installation.  

- If you deployed the application as **Required**, and specified to **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**, then the client displays a notification. It informs the user that the specified executable files are automatically closed when the application installation deadline is reached.  

  - Schedule these dialogs in the **Computer Agent** group of client settings. For more information, see [Computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

  - If you don't want the user to see these messages, select the option to **Hide in Software Center and all notifications** on the **User Experience** tab of the deployment's properties. For more information, see [Deployment User Experience settings](#bkmk_deploy-ux).  

- If you deployed the application as **Required**, and didn't specify to **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**, then the installation of the app fails if one or more of the specified applications are running.  

## Deploy user-available applications

When you deploy applications as **Available** to user collections, then users can browse Software Center and install the apps they need. For on-premises domain-joined clients, Software Center uses the user's domain credentials to get the list of available applications from the management point.

There are additional requirements for clients that are internet-based, joined to Azure Active Directory (Azure AD), or both.

### Azure AD-joined devices
<!-- 1322613 -->

If you deploy applications as available to users, they can browse and install them through Software Center on Azure AD devices. Configure the following prerequisites to enable this scenario:

- Enable HTTPS on the management point  

- Integrate the site with [Azure AD](../../core/servers/deploy/configure/azure-services-wizard.md) for **Cloud Management**  

  - Configure [Azure AD User Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  

- Deploy an application as available to a collection of users from Azure AD  

- Enable the client setting **Use new Software Center** in the [Computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent) group  

- The client OS must be Windows 10, and joined to Azure AD. Either as purely cloud domain-joined, or hybrid Azure AD-joined.  

- To support internet-based clients:  

  - [Cloud management gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG)

  - Distribute any application content to a content-enabled CMG or a [cloud distribution point](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

  - Enable the client setting: **Enable user policy requests from Internet clients** in the [Client Policy](../../core/clients/deploy/about-client-settings.md#client-policy) group  

- To support clients on the intranet:  

  - Add the content-enabled CMG or cloud distribution point to a boundary group used by the clients  

  - Clients must resolve the fully qualified domain name (FQDN) of the HTTPS-enabled management point  

  > [!NOTE]
  > For a client detected as on the intranet, but communicating via the cloud management gateway (CMG), in Configuration Manager version 2002 and earlier, Software Center uses Windows authentication. When it tried to get the list of user-available apps via CMG, it would fail. Starting in version 2006, it uses Azure Active Directory (Azure AD) identity for devices joined to Azure AD. These devices can be cloud-joined or hybrid-joined.<!--6935376-->

## Next steps

- [Monitor applications](monitor-applications-from-the-console.md)
- [Troubleshoot application deployments](troubleshoot-application-deployment.md)
- [Management tasks for applications](management-tasks-applications.md)
- [Software Center user guide](../../core/understand/software-center.md)
