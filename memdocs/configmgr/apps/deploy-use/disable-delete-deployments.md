---
title: Disable and delete app deployments
titleSuffix: Configuration Manager
description: If you want to stop the deployment of an application, you can either disable it temporarily or delete it entirely.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Disable and delete application deployments

*Applies to: Configuration Manager (current branch)*

If you want to stop the deployment of an application, you can either disable it temporarily or delete it entirely.

> [!IMPORTANT]
> Neither of these actions by themselves cause an instant change on the client. You can use [client notifications](../../core/clients/manage/client-notification.md#client-notification) or other automation tools to quickly request that clients refresh policy. But that still doesn't guarantee that a client won't run a deployment.
>
> Make sure you carefully plan app deployments. [Simulate](simulate-application-deployments.md) more complex deployments. When you deploy to a query-based collection, use [query results preview](../../core/clients/manage/collections/create-collections.md#bkmk-query) to make sure you understand the scope of the query.

## Disable

<!--8354812-->

Starting in version 2103, you can disable application deployments. Other objects already have similar behaviors:

- Software update deployments: Disable the deployment
- Phased deployments: Suspend the phase
- Package: Disable the program
- Task sequence: Disable the task sequence
- Configuration baseline: Disable the baseline

For device-based deployments, when you disable the deployment or object, use the client notification action to **Download Computer Policy**. This action immediately tells the client to update its policy from the site. If the deployment hasn't already started, the client receives the updated policy that the object is now disabled.

For user-based deployments, the user needs to sign out of Windows. Policy updates when they sign in to Windows, or every 24 hours by default.

> [!NOTE]
> You can't disable an available deployment of an application to a user collection.<!-- 9390894 --> You can only disable required deployments to user collections, or both type of deployments to device collections. The following table summarizes the supported scenarios to disable app deployments:
>
> |Deployment purpose| Device collection | User collection |
> |---------|---------|---------|
> |Required |  Yes    |  Yes    |
> |Available|  Yes    |  No     |

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node.

1. Select an app that you've deployed. In the details pane, switch to the **Deployment** tab.

1. Select a deployment. In the ribbon, on the **Deployment** tab, select **Disable**.

1. For a device-based deployment, note the name of the collection in **Collection** field of the deployment.

    > [!TIP]
    > When you select the deployment, press **CTRL** + **C**. This keyboard shortcut copies the values of the current columns for the selected deployment.

    <!-- 1. Right-click the deployment and select **Collection**. This action switches the view to the **Assets and Compliance** workspace showing the target collection for the deployment.  Waiting on 8957946 for better end-to-end flow -->

1. Switch to the **Assets and Compliance** workspace, select the **Device Collections** node, and locate the target collection for the deployment. The quickest method is to search for the collection name as previously noted. You may need to select the option in the ribbon to search **All subfolders**.

1. Select the target collection for the deployment. In the ribbon, in the **Collection** group, select **Client Notification** and choose the **Download Computer Policy** action.

To enable the deployment, repeat this process but select the **Enable** action on the application deployment.

> [!NOTE]
> When you select a deployment, you can use the **Collection** action to change to the **Assets and Compliance** workspace. But the current collection view doesn't support client notification actions.<!-- 8957946 -->

## Delete

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select either the **Applications** or **Application Groups** node.

1. Select the application or application group that includes the deployment you want to delete.

1. Switch to the **Deployments** tab of the details pane, and select the deployment.

1. In the ribbon, on the **Deployment** tab in the **Deployment** group, select **Delete**.

When you delete an application deployment, any instances of the application that clients have already installed aren't removed. To remove these applications, deploy the application to computers to **Uninstall**. If you delete an application deployment, the application is no longer visible in Software Center. The same behavior happens when you remove a resource from the target collection for the deployment.

When you delete a deployment, you remove the policy that deploys an application to a specific collection. This action doesn't delete the collection, any deployment types, or the application itself.

## Next steps

[Revise and supersede applications](revise-and-supersede-applications.md)

[Uninstall applications](uninstall-applications.md)
