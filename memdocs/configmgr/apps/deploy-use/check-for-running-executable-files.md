---
title: Check for running executable files
titleSuffix: Configuration Manager
description: Configure an app deployment to check if certain executable files are running on the client.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Check for running executable files

*Applies to: Configuration Manager (current branch)*

Configure an application deployment to check if certain executable files are running on the client. Use this option to check for processes that might disrupt the installation of the application. If one of these executable files is running, the client blocks the installation of the deployment type. The user must close the running executable file before the client can install the deployment type. For deployments with a purpose of required, the client can automatically close the running executable file.

1. Open the **Properties** for the deployment type.

1. Switch to the **Install Behavior** tab, and select **Add**.

1. In the **Add Executable File** window, enter the name of the target executable file. Optionally, enter a friendly name for the application to help you identify it in the list.

1. Select **OK** to save and close the deployment type properties window.

1. When you deploy the application, select the option to **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**. This option is on the **Deployment Settings** tab of the deployment properties.

> [!NOTE]
> If you configure an application to check for running executable files, and include it in the [Install Application](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) task sequence step, the task sequence will fail to install it. If you don't configure this task sequence step to continue on error, then the entire task sequence fails.

## Client behaviors and user notifications

After clients receive the deployment, the following behavior applies:

- If you deployed the application as **Available**, and a user tries to install it, the client prompts the user to close the specified running executable files before proceeding with the installation.

- If you deployed the application as **Required**, and specified to **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**, then the client displays a notification. It informs the user that the specified executable files are automatically closed when the application installation deadline is reached. If the user tries to install the application before the deadline, the deployment will fail. It notifies the user that the installation couldn't complete because the specified executables are running.

  - Schedule these dialogs in the **Computer Agent** group of client settings. For more information, see [Computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent).

  - If you don't want the user to see these messages, select the option to **Hide in Software Center and all notifications** on the **User Experience** tab of the deployment's properties. For more information, see [User Experience settings](deploy-applications.md#bkmk_deploy-ux).

- If you deployed the application as **Required**, and didn't specify to **Automatically close any running executables you specified on the install behavior tab of the deployment type properties dialog box**, then the installation of the app fails if one or more of the specified applications are running.

## Next steps

- Plan for [user notifications](../plan-design/user-notifications.md) when you deploy applications

- [Create deployment types for an application](create-applications.md#bkmk_create-dt)

- [Deploy applications](deploy-applications.md)
