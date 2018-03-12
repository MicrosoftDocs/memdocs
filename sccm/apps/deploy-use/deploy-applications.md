---
title: Deploy applications
titleSuffix: Configuration Manager
description: Create or simulate a deployment of an application to a device or user collection
ms.custom: na
ms.date: 03/09/2018
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
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Deploy applications with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Create or simulate a deployment of an application to a device or user collection in Configuration Manager. This deployment gives instructions to the Configuration Manager client on how and when to install the software. 

Before you can deploy an application, create at least one deployment type for the application. For more information, see [Create applications](/sccm/apps/deploy-use/create-applications).

 You can also simulate an application deployment. This simulation tests the applicability of a deployment without installing or uninstalling the application. A simulated deployment evaluates the detection method, requirements, and dependencies for a deployment type and reports the results in the **Deployments** node of the **Monitoring** workspace. For more information, see [Simulate application deployments](/sccm/apps/deploy-use/simulate-application-deployments).

> [!IMPORTANT]
>  You can simulate the deployment of required applications, but not packages or software updates.   
>  MDM-enrolled devices don't support simulated deployments, user experience, or scheduling settings.



## Deploy an application

1.  In the Configuration Manager console, go to **Software Library** > **Application Management** > **Applications**.

2.  In the **Applications** list, select the application that you want to deploy. Then, on the **Home** tab, in the **Deployment** group, click **Deploy**.

### Specify general information about the deployment

On the **General** page of the Deploy Software wizard, specify the following information:

- **Software**: This value displays the application to deploy. Click **Browse** to select a different application.
- **Collection**: Click **Browse** to select the collection to deploy the application to.
- **Use default distribution point groups associated to this collection**: Store the application content on the collection's default distribution point group. If you have not associated the selected collection with a distribution point group, this option is grayed out.
- **Automatically distribute content for dependencies**: If any of the deployment types in the application contain dependencies, then the site also sends dependent application content to distribution points.

	>[!IMPORTANT]
	> If you update the dependent application after deploying the primary application, the site doesn't automatically distribute any new content for the dependency.

- **Comments (optional)**: Optionally, enter a description for this deployment.

### Specify content options for the deployment

On the **Content** page, click **Add** to add the content associated with this deployment to distribution points or distribution point groups. If you select **Use default distribution points associated to this collection** on the **General** page, then this option is automatically populated. Only a member of the Application Administrator security role can modify it.

### Specify deployment settings

On the **Deployment Settings** page of the Deploy Software wizard, specify the following information:

- **Action**: From the drop-down list, choose whether this deployment is to **Install** or **Uninstall** the application.

	> [!NOTE]
	>  If an application is deployed twice to a device, once with an action of **Install** and once with an action of **Uninstall**, the application deployment with an action of **Install** takes priority.

  You cannot change the action of a deployment after you create it.

- **Purpose**: From the drop-down list, choose one of the following options:  
	- **Available**: If the application is deployed to a user, the user sees the published application in Software Center and can install it on demand.
	- **Required**: The application is deployed automatically according to the schedule. If the application deployment status is not hidden, anyone using the application can track its deployment status and install the application from Software Center before the deadline.

	> [!NOTE]   
	>  When the deployment action is set to **Uninstall**, the deployment purpose is automatically set to **Required**. You can't change this behavior.  

- **Deploy automatically according to schedule whether or not a user is logged on**: If the deployment is to a user, select this option to deploy the application to the user’s primary devices. This setting does not require the user to log on before the deployment runs. Do not select this option if the user must interact with the installation. This option is only available when the deployment has a purpose of **Required**.

- **Send wake-up packets**: If the deployment purpose is **Required**, a wake-up packet is sent to computers before the client runs the deployment. This packet wakes the computers at the installation deadline time. Before using this option, computers and networks must be configured for Wake On LAN.
- **Allow clients on a metered Internet connection to download content after the installation deadline, which might incur additional costs**: This option is only available for deployments with a purpose of **Required**.
- **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**: For more information, see [check for running executable files before installing an application](#how-to-check-for-running-executable-files-before-installing-an-application).

- **Require administrator approval if users request this application**: For versions 1710 and prior, the administrator approves any user requests for the application before the user can install it. This option is grayed out when the deployment purpose is **Required**, or when the application is deployed to a device collection.  

	> [!NOTE]
	>  Application approval requests are displayed in the **Approval Requests** node, under **Application Management** in the **Software Library** workspace. If a request isn't approved within 45 days, it's removed. Reinstalling the client might cancel any pending approval requests.  
	>  After you've approved an application for installation, you can **Deny** the request in the Configuration Manager console. This action doesn't cause the client to uninstall the application from any devices, but it does stop users from installing new copies of the application from Software Center.

- **An administrator must approve a request for this application on the device**: Starting in version 1802, the administrator approves any user requests for the application before the user can install it on the requested device. If the administrator approves the request, the user is only able to install the application on that device. The user must submit another request to install the application on another device. This option is grayed out when the deployment purpose is **Required**, or when the application is deployed to a device collection. <!--1357015-->  

    > [!Important]
    > The Configuration Manager client must be on version 1802 as well. You must also be using the new Software Center.  

    > [!Note]
    > View **Approval Requests** under **Application Management** in the **Software Library** workspace of the Configuration Manager console. There is now a **Device** column in the list for each request. When you take action on the request, the Application Request dialog also includes the device name from which the user submitted the request.  
    >  If a request isn't approved within 45 days, it's removed. Reinstalling the client might cancel any pending approval requests.  
	>  After you've approved an application for installation, you can **Deny** the request in the Configuration Manager console. This action doesn't cause the client to uninstall the application from any devices, but it does stop users from installing new copies of the application from Software Center.

- **Automatically upgrade any superseded version of this application**: The client upgrades any superseded version of the application with the superseding application.    

    > [!NOTE]  
    > Starting in version 1802, for either **Available** or **Required** install purpose, you can enable or disable this option. <!--1351266--> 


### Specify scheduling settings for the deployment

On the **Scheduling** page of the Deploy Software wizard, set the time when this application is deployed or available to client devices.
The options on this page differ depending on whether the deployment action is set to **Available** or **Required**.

In some cases, you might want to give users more time to install required application deployments or software updates beyond any deadlines you set up. This behavior is typically required when a computer has been turned off for long time and needs to install many applications. For example, if a user has returned from vacation, they might have to wait for a long time as overdue application deployments are installed. To help solve this problem, you can now define an enforcement grace period by deploying Configuration Manager client settings to a collection.

To configure the grace period, take the following actions:

- On the **Computer Agent** page of client settings, configure the new property **Grace period for enforcement after deployment deadline (hours)** with a value between **1** and **120** hours.
- On the **Scheduling** page of a required application deployment, choose to **Delay enforcement of this deployment according to user preferences, up to the grace period defined in client settings**. The enforcement grace period applies to all deployments with this option enabled and targeted to devices to which you also deployed the client setting.

After the application install deadline is reached, the client installs the application in the first non-business window, which the user configured, up to that grace period. However, the user can still open Software Center and install the application at any time they want. Once the grace period expires, enforcement reverts to normal behavior for overdue deployments.

If the application you're deploying supersedes another application, you can set the installation deadline when users receive the new application. Set the **Installation Deadline** to upgrade users with the superseded application.

### Specify user experience settings for the deployment

On the **User Experience** page of the Deploy Software wizard, specify information about how users can interact with the application installation.

When you deploy applications to write-filter enabled Windows Embedded devices, you can specify to install the application on the temporary overlay and commit changes later. You can also specify to commit the changes at the installation deadline or during a maintenance window. If you commit changes at the installation deadline or during a maintenance window, you must restart the device. The changes persist on the device.

>[!NOTE]
	>  When you deploy an application to a Windows Embedded device, make sure it's a member of a collection with a maintenance window. For more information about maintenance windows and Windows Embedded devices, see [Create Windows Embedded applications](../../apps/get-started/creating-windows-embedded-applications.md).
	>  The options **Software Installation** and **System restart (if required to complete the installation)** are not used if the deployment purpose is set to **Available**. You can also configure the level of notification a user sees when the application is installed.

### Specify alert options for the deployment

On the **Alerts** page of the Deploy Software wizard, set up how Configuration Manager and System Center Operations Manager generate alerts for this deployment. You can configure thresholds for reporting alerts and turn off reporting for the duration of the deployment.

### Associate the deployment with an iOS app configuration policy

On the **App Configuration Policies** page, click **New** to associate this deployment with an iOS app configuration policy (if you have created one). For more information about this type of policy, see [Configure iOS apps with app configuration policies](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).

### Deployment properties

Find the new deployment in the **Deployments** node of the **Monitoring** workspace. You can edit the properties of this deployment or delete the deployment from the **Deployments** tab of the application detail pane.



## Delete an application deployment

1.  In the Configuration Manager console, go to **Software Library** > **Application Management** > **Applications**.
3.  In the **Applications** list, select the application that includes the deployment you delete.
4.  In the **Deployments** tab of the *<application name\>* list, select the application deployment to delete. Then on the **Deployment** tab, in the **Deployment** group, click **Delete**.

When you delete an application deployment, any instances of the application that have already been installed aren't removed. To remove these applications, you must deploy the application to computers with **Uninstall**. If you delete an application deployment, or remove a resource from the collection you're deploying to, the application is no longer visible in Software Center.



## User notifications for required deployments
When you receive required software from the **Snooze and remind me** setting, you can select from the following drop-down list of values:
- **Later**: Specifies that notifications are scheduled based on the notification settings configured in client settings.
- **Fixed time**: Specifies that the notification is scheduled to display again after the selected time. For example, if you select 30 minutes, the notification displays again in 30 minutes.

![Computer Agent group in default client settings](media/ComputerAgentSettings.png)

The maximum snooze time is always based on the notification values configured in the client settings at every time along the deployment timeline. For example:
- You configure the **Deployment deadline greater than 24 hours, remind users every (hours)** setting on the **Computer Agent** page for 10 hours.
- The client displays the notification dialog more than 24 hours before the deployment deadline.
- The dialog shows snooze options up to but never greater than 10 hours. 
- As the deployment deadline approaches, the dialog shows fewer options. These options are consistent with the relevant client settings for each component of the deployment timeline.

For a high-risk deployment, such as a task sequence that deploys an operating system, the user notification experience is more intrusive. Instead of a transient taskbar notification, a dialog box like the following displays each time you're notified that critical software maintenance is required:

![Required software dialog notifies you of critical software maintenance](media/client-toast-notification.png)



## How to check for running executable files before installing an application

In the **Properties** dialog box of a deployment type, on the **Install Behavior** tab, specify one or more executable files. If one of these executable files is running on the client, it blocks the installation of the deployment type. The user must close the running executable file before the client can install the deployment type. For deployments with a purpose of required, the client can automatically close the running executable file.

1. Open the **Properties** dialog box for any deployment type.
2. On the **Install Behavior** tab of the *<deployment type name>* **Properties** dialog box, click **Add**.
3. In the **Add or Edit Executable File** dialog box, enter the name of the executable file that, if running, blocks install of the application. Optionally, you can also enter a friendly name for the application to help you identify it in the list.
4. Click **OK**, then close the *<deployment type name>* **Properties** dialog box.
5. When you deploy the application, on the **Deployment Settings** page of the Deploy Software Wizard, select **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**.

After clients receive the deployment, the following behavior applies:

- If you deployed the application as **Available**, and an end user tries to install it, the client prompts the user to close the specified running executable files before proceeding with the installation.

- If you deployed the application as **Required**, and specified to **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**, then the user sees a dialog box informing them that the specified executable files are automatically closed when the application installation deadline is reached. You can schedule these dialogs in **Client Settings** > **Computer Agent**. If you don’t want the end user to see these messages, select **Hide in Software Center and all notifications** on the **User Experience** tab of the deployment’s properties.

- If you deployed the application as **Required**, and didn't specify to **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**, then the installation of the app fails if one or more of the specified applications are running.



## Next steps

   -  [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md)  
   -  [How to configure client settings](../../core/clients/deploy/configure-client-settings.md)
   -  [Software Center user guide](/sccm/core/understand/software-center)

