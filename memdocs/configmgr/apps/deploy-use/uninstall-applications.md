---
title: Uninstall applications
titleSuffix: Configuration Manager
description: Uninstall an application by using Configuration Manager
ms.date: 04/06/2022
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Uninstall applications with Configuration Manager

*Applies to: Configuration Manager (current branch)*

Instead of needing to create a separate object to uninstall an application, you can specify uninstall behaviors on the deployment type. Then create a separate deployment with the action to uninstall. You can uninstall an application even if it wasn't previously installed by Configuration Manager.

## Behaviors and limitations

- To deploy an application with the **Uninstall** action, first delete any existing application deployments, simulated deployments, or task sequence deployments that include this application. Otherwise Configuration Manager may reinstall the application.

- Some application types don't support uninstallation.

- When you uninstall an application, Configuration Manager doesn't automatically uninstall dependencies.

- If you deploy to a user an application with the **Uninstall** action, and the application was installed for all users of the computer, the uninstall might fail if the user's account doesn't have permissions to uninstall the application.

- In version 2103 and earlier, if you remove a user or a device from a collection that has an application deployed to it, Configuration Manager doesn't automatically uninstall the application from the device.

    > [!TIP]
    > Version 2107 and later supports [Implicit uninstall](#implicit-uninstall).

- A deployment with the **Uninstall** action doesn't check requirement rules. If the application is installed on the target device, Configuration Manager uninstalls it.

## Process

When you [create the application](create-applications.md), select the option to **Automatically identify information about this deployment type from installation files**. If the information is available in the installation files, the uninstall command line is automatically added to the deployment type properties.

For an existing application, use the following steps to configure its uninstall properties:

1. In the Configuration Manager console, go to the **Software Library** workspace. Expand **Application Management** and select the **Applications** node.

1. Select the application. In the details pane, switch to the **Deployment Types** tab.

1. Select the deployment type. Then in the ribbon, on the **Deployment Type** tab, select **Properties**.

1. Switch to the **Content** tab and configure the following settings:

    - **Uninstall content settings**: Select an option for where Configuration Manager gets the content to uninstall the application:

        - **Same as install content**: The install and uninstall content are the same. This option is the default.

        - **No uninstall content**: Your application doesn't need content for uninstall.

        - **Different from install content**: The uninstall content is different from the install content.

    - **Uninstall content location**: If you select the third option for content settings, specify the network path to the content that's used to uninstall the application.

1. Switch to the **Programs** tab and configure the following settings:

    - **Uninstall program**: Specify the command line and any required parameters to uninstall the application.

    - **Uninstall start in**: Optionally specify the folder that has the uninstall program for the deployment type. This folder can be an absolute path on the client. It can also be a relative path on a distribution point of the folder with the package.

    - **Run installation and uninstall program as 32-bit process on 64-bit clients**: Use the 32-bit file and registry locations on Windows-based computers to run the uninstall program for the deployment type.

Then [deploy the application](deploy-applications.md). On the **Deployment Settings** page of the wizard, select the deployment action to **Uninstall**.

> [!NOTE]
> When you select a deployment action of **Uninstall**, the deployment purpose is automatically configured as **Required**.

## Implicit uninstall

<!--3607457-->

Many customers have lots of collections because for every application they need at least two collections: one for install and another for uninstall. This practice adds overhead of managing more collections, and can reduce site performance for collection evaluation.

Starting in version 2107, you can enable an application deployment to support implicit uninstall. If a resource is in a collection, the application installs. Then when you remove the resource from the collection, the application uninstalls.

Starting in version 2111, this behavior also supports [application groups](create-app-groups.md#app-approval).<!-- 10479618 --> When this article refers to an _application_, it also applies to app groups.

> [!NOTE]
> In version 2111 and later, this behavior applies to deployments to device or user collections.<!--10393847--> In version 2107, this behavior only applies to deployments to device collections.

Starting in version 2203, if you deploy an application or app group to a user collection that's based on a security group, and you enable implicit uninstall, changes to the security group are now honored. When the site discovers the change in group membership, Configuration Manager uninstalls the app for the user that you removed from the security group.<!--12488148-->

### Enable implicit uninstall

When you [deploy the application](deploy-applications.md) to a collection, configure the following settings on the **Deployment Settings** page:

- **Action**: Install

- **Purpose**: Required

- Enable the following option: **When a resource is no longer a member of the collection, uninstall the application**

    > [!TIP]
    > In version 2107, this option is named: **Uninstall this application if the targeted object falls out of the collection**

> [!IMPORTANT]
> Be careful with enabling this option on deployments to large query-based collections. Especially queries to external sources like Active Directory groups. An unexpected external change could automatically trigger a large number of devices to uninstall the application.

### Implicit uninstall process

After you remove the resource from the collection, the following process happens:

- A background worker process runs on the site server every 10 minutes. This task keeps track of apps for which you've enabled this option. It then detects resources that you removed from the target collection. To help you troubleshoot this process, view the **SMS_ImplicitUninstall.log** file on the site server.

- The client needs to download policy. By default, the [client policy polling interval](../../core/clients/deploy/about-client-settings.md#client-policy) client setting is 60 minutes. To accelerate this step, manually [download policy](../../core/clients/manage/manage-clients.md#start-policy-retrieval).

- 15 minutes after the client receives the updated policy, it uninstalls the app.

Depending upon the timing of those steps, the longest time period for the client to uninstall the app is 85 minutes. If the first step happens immediately, and you manually download policy on the device, the overall process is 15 minutes.

> [!NOTE]
> - For this behavior, the site can process up to 1000 collection membership changes every 10 minutes.
> - If the uninstall doesn't occur, it's likely that there's a conflicting install deployment of the same application, application group, or a different application group with the same apps.<!--12618105--> Configuration Manager always honors an install deployment over an uninstall deployment.

### Known issues

You configure an app's installation behavior to **Install for system**, and then deploy it to a user collection. A device has multiple users who are both in the collection, and the app installs on the device. If you then remove _one user_ from the collection, the app is uninstalled from the device for all users.<!-- 11104790 -->

## Next steps

[How to manage collections](../../core/clients/manage/collections/manage-collections.md)

[Monitor applications from the Configuration Manager console](monitor-applications-from-the-console.md)

[Log file reference](../../core/plan-design/hierarchy/log-files.md)
