---
title: "Deploy applications"
description: "Create a deployment type or simulate deployment for an application by using System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: 10
caps.handback.revision: 0
author: mattbriggs
ms.author: mabrigg
manager: angrobe

---
# Deploy applications with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Before you can deploy a System Center Configuration Manager application, you must create at least one deployment type for the application. For more information about creating applications and deployment types, see [Create applications](/sccm/apps/deploy-use/create-applications).

 You can also simulate an application deployment. This type of deployment tests the applicability of an application deployment to computers without installing or uninstalling the application. A simulated deployment evaluates the detection method, requirements, and dependencies for a deployment type and reports the results in the **Deployments** node of the **Monitoring** workspace. For more information, see [Simulate application deployments](/sccm/apps/deploy-use/simulate-application-deployments).

> [!IMPORTANT]
>  You can deploy (install or uninstall) required applications, but not packages or software updates. MDM-enrolled devices also do not support simulated deployments, user experience, or scheduling settings.

## Deploy an application

1.  In the Configuration Manager console, go to **Software Library** > **Application Management** > **Applications**.

2.  In the **Applications** list, select the application that you want to deploy. Then, on the **Home** tab, in the **Deployment** group, click **Deploy**.

### Specify general information about the deployment

On the **General** page of the Deploy Software wizard, specify the following information:

- **Software**  
This displays the application to deploy. You can click **Browse** to select a different application.
- **Collection**  
Click **Browse** to select the collection to deploy the application to.
- **Use default distribution point groups associated to this collection**  
Select this option if you want to store the application content on the collection's default distribution point group. If you have not associated the selected collection with a distribution point group, this option is grayed out.
- **Automatically distribute content for dependencies**  
If this is enabled and if any of the deployment types in the application contain dependencies, then the dependent application content is also sent to distribution points.

	>[!IMPORTANT]
	> If you update the dependent application after the primary application has been deployed, any new content for the dependency will not be automatically distributed.

- **Comments (optional)**  
Optionally, enter a description for this deployment.

### Specify content options for the deployment

On the **Content** page, click **Add** to add the content associated with this deployment to distribution points or distribution point groups. If you have selected **Use default distribution points associated to this collection** on the **General** page, then this option is automatically populated and can only be modified by a member of the Application Administrator security role.

### Specify deployment settings

On the **Deployment Settings** page of the Deploy Software wizard, specify the following information:

- **Action**  
From the drop-down list, choose whether this deployment is intended to **Install** or **Uninstall** the application.

	> [!NOTE]
	>  If an application is deployed twice to a device, once with an action of **Install** and once with an action of **Uninstall**, the application deployment with an action of **Install** takes priority.

You cannot change the action of a deployment after it has been created.

- **Purpose**  
From the drop-down list, choose one of the following options:
	- **Available**  
	If the application is deployed to a user, the user sees the published application in Software Center and can install it on demand.
	- **Required**  
	The application is deployed automatically according to the schedule. If the application deployment status is not hidden, anyone using the application can track its deployment status and install the application from Software Center before the deadline.

	> [!NOTE]   
	>  When the deployment action is set to **Uninstall**, the deployment purpose is automatically set to **Required** and cannot be changed.  

- **Deploy automatically according to schedule whether or not a user is logged on**  
If the deployment is to a user, select this option to deploy the application to the user’s primary devices. This setting does not require the user to log on before the deployment runs. Do not select this option if the user must provide input to complete the installation. This option is only available when the deployment has a purpose of **Required**.

- **Send wake-up packets**  
If the deployment purpose is set to **Required** and this option is selected, a wake-up packet is sent to computers before the deployment is installed. This packet wakes the computers at the installation deadline time. Before you can use this option, computers and networks must be configured for Wake On LAN.
- **Allow clients on a metered Internet connection to download content after the installation deadline, which might incur additional costs**  
This option is only available for deployments with a purpose of **Required**.
- **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**  
For more information about how to configure a list of executables that can prevent an application from installing, see **How to check for running executable files before installing an application** later in this topic.
- **Require administrator approval if users request this application**  
If this option is selected, the administrator must approve any user requests for the application before it can be installed. This option is grayed out when the deployment purpose is **Required** or when the application is deployed to a device collection.

	> [!NOTE]
	>  Application approval requests are displayed in the **Approval Requests** node, under **Application Management** in the **Software Library** workspace. If a request is not approved within 45 days, it is removed. Additionally, reinstalling the Configuration Manager client might cancel any pending approval requests.
	>  After you have approved an application for installation, you can subsequently choose to deny the request by clicking **Deny** in the Configuration Manager console (previously, this button was grayed out after approval).
	>  This action does not cause the application to be uninstalled from any devices, but it does stop users from installing new copies of the application from Software Center.

- **Automatically upgrade any superseded version of this application**  
If this option is selected, any superseded version of the application is upgraded with the superseding application.

### Specify scheduling settings for the deployment

On the **Scheduling** page of the Deploy Software wizard, set the time when this application is deployed or available to client devices.
The options on this page differ depending on whether the deployment action is set to **Available** or **Required**.

In some cases, you might want to give users more time to install required application deployments or software updates beyond any deadlines you set up. This is typically required when a computer has been turned off for an extended period of time and needs to install a large number of updates or application deployments. For example, if a user has returned from vacation, they might have to wait for a long time as overdue application deployments are installed. To help solve this problem, you can now define an enforcement grace period by deploying Configuration Manager client settings to a collection.

To configure the grace period, take the following actions:

- On the **Computer Agent** page of client settings, configure the new property **Grace period for enforcement after deployment deadline (hours)** with a value between **1** and **120** hours.
- On the **Scheduling** page in a new required application deployment, or in the properties of an existing deployment, select the box **Delay enforcement of this deployment according to user preferences, up to the grace period defined in client settings**. The enforcement grace period is used by all deployments that have this box selected and are targeted to devices to which you also deployed the client setting.

After the application install deadline is reached, the application will be installed in the first non-business window that the user configured up to that grace period. However, the user can still open Software Center and install the application at any time they want. Once the grace period expires, enforcement reverts to normal behavior for overdue deployments.

If the application you are deploying supersedes another application, you can set the installation deadline when users receive the new application. Do this by using the setting **Installation Deadline** to upgrade users with the superseded application.

### Specify user experience settings for the deployment


On the **User Experience** page of the Deploy Software wizard, specify information about how users can interact with the application installation.

When you deploy applications to Windows Embedded devices that are write-filter enabled, you can specify to install the application on the temporary overlay and commit changes later, or to commit the changes at the installation deadline or during a maintenance window. When you commit changes at the installation deadline or during a maintenance window, you must restart the device. The changes persist on the device.

>[!NOTE]
	>  When you deploy an application to a Windows Embedded device, make sure that the device is a member of a collection that has a configured maintenance window. For more information about how maintenance windows are used when you deploy applications to Windows Embedded devices, see [Create Windows Embedded applications](../../apps/get-started/creating-windows-embedded-applications.md).
	>  The options **Software Installation** and **System restart (if required to complete the installation)** are not used if the deployment purpose is set to **Available**. You can also configure the level of notification a user sees when the application is installed.

### Specify alert options for the deployment

On the **Alerts** page of the Deploy Software wizard, set up how Configuration Manager and System Center Operations Manager generate alerts for this deployment. You can configure thresholds for reporting alerts and turn off reporting for the duration of the deployment.

### Associate the deployment with an iOS app configuration policy

On the **App Configuration Policies** page, click **New** to associate this deployment with an iOS app configuration policy (if you have created one). For more information about this type of policy, see [Configure iOS apps with app configuration policies](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).

### Finish up

On the **Summary** page of the Deploy Software wizard, review the actions that are taken by this deployment, and then click **Next** to finish the wizard.

The new deployment is displayed in the **Deployments** list in the **Deployments** node of the **Monitoring** workspace. You can edit the properties of this deployment or delete the deployment from the **Deployments** tab of the application detail pane.

## Delete an application deployment

1.  In the Configuration Manager console, go to **Software Library** > **Application Management** > **Applications**.
3.  In the **Applications** list, select the application that includes the deployment you delete.
4.  In the **Deployments** tab of the *<application name\>* list, select the application deployment to delete. Then on the **Deployment** tab, in the **Deployment** group, click **Delete**.

When you delete an application deployment, any instances of the application that have already been installed are not removed. To remove these applications, you must deploy the application to computers with **Uninstall**. If you delete an application deployment, or remove a resource from the collection you are deploying to, the application will no longer be visible in Software Center.

## User notifications for required deployments
When you receive required software from the **Snooze and remind me** setting, you can select from the following drop-down list of values:
- **Later**  
Specifies that notifications are scheduled based on the notification settings configured in Client Agent settings.
- **Fixed time**  
Specifies that the notification will be scheduled to display again after the selected time. For example, if you select 30 minutes, the notification displays again in 30 minutes.

![Computer Agent page in Client Agent settings](media/ComputerAgentSettings.png)

The maximum snooze time is always based on the notification values configured in the Client Agent settings at every time along the deployment timeline. For example, if the **Deployment deadline greater than 24 hours, remind users every (hours)** setting on the **Computer Agent** page is configured for 10 hours, and it is more than 24 hours before the deadline when the dialog is launched, you would be presented with a set of snooze options up to but never greater than 10 hours. As the deadline approaches, the dialog shows fewer options, consistent with the relevant Client Agent settings for each component of the deployment timeline.

Additionally, for a high-risk deployment, such as a task sequence that deploys an operating system, the user notification experience is now more intrusive. Instead of a transient taskbar notification, a dialog box like the following displays on your computer each time you are notified that critical software maintenance is required:

![Required Software dialog](media/client-toast-notification.png)

## How to check for running executable files before installing an application

>[!Tip]
>Introduced with version 1702, this is a pre-release feature. To enable it, see [Pre-release features in System Center Configuration Manager](https://docs.microsoft.com/sccm/core/servers/manage/pre-release-features).

In the **Properties** dialog box of a deployment type, on the **Install Behavior** tab, you can specify one or more executable files that, if running, block the installation of the deployment type. The user must close the running executable file (or it can be closed automatically for deployments with a purpose of required) before the deployment type can be installed. To configure this:

1. Open the **Properties** dialog box for any deployment type.
2. On the **Install Behavior** tab of the *<deployment type name>* **Properties** dialog box, click **Add**.
3. In the **Add or Edit Executable File** dialog box, enter the name of the executable file that, if running, blocks install of the application. Optionally, you can also enter a friendly name for the application to help you identify it in the list.
4. Click **OK**, then close the *<deployment type name>* **Properties** dialog box.
5. Next, when you deploy an application, on the **Deployment Settings** page of the Deploy Software Wizard, select **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**, then continue to deploy the application.

After the application reaches client PCs, the following behavior applies:

- If the application was deployed as **Available**, and an end user tries to install it, they are prompted to close any running executables you specified before they can proceed with the installation.

- If the application was deployed as **Required**, and the option **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box** is selected, they see a dialog box that informs them that executables you specified are automatically closed when the application installation deadline is reached. You can schedule these dialogs in **Client Settings** > **Computer Agent**. If you don’t want the end user to see these messages, select **Hide in Software Center and all notifications** on the **User Experience** tab of the deployment’s properties.

- If the application was deployed as **Required** and the option **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box** is not selected, then the installation of the app fails if one or more of the specified applications are running.

## For more information

   -  [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md)  
   -  [How to configure client settings](../../core/clients/deploy/configure-client-settings.md)
