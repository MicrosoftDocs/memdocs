---
title: Test client upgrades
titleSuffix: Configuration Manager
description: Test client upgrades in a pre-production collection in Configuration Manager.
ms.date: 04/12/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: how-to
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to test client upgrades in a pre-production collection

*Applies to: Configuration Manager (current branch)*

You can test a new Configuration Manager client version in a pre-production collection before upgrading the rest of the site with it. When you do this process, the site only updates devices that are part of the test collection. Once you've had a chance to test the client, you can promote the client. Client promotion makes the new version of the client software available to the rest of the site.

> [!NOTE]
> Only a user with the **Full Administrator** security role and the **All** security scope can promote a test client to production. For more information, see [Fundamentals of role-based administration](../../../understand/fundamentals-of-role-based-administration.md). This action is only available when connected to the central administration site (CAS) or a standalone primary site.

There are three steps to test clients in pre-production:

1. Configure automatic client upgrades to use a pre-production collection.

2. Install a Configuration Manager update that includes a new version of the client.

3. Promote the new client to production.

## Configure automatic client upgrades to use a pre-production collection

> [!IMPORTANT]
> Pre-production client deployment isn't supported for workgroup computers. They can't use the authentication required for the distribution point to access the pre-production client package. They'll receive the latest client when it's promoted to be the production client.

1. [Set up a collection](../collections/create-collections.md) that contains the computers to which you want to deploy the pre-production client.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. In the ribbon, select **Hierarchy Settings**.

1. Switch to the **Client Upgrade** tab, and configure the following settings:

    - Select **Upgrade all clients in the pre-production collection automatically using pre-production client**.

    - Select a collection to use as the **Pre-production collection**.

:::image type="content" source="media/test-client-upgrades.png" alt-text="Hierarchy settings window, client upgrade tab, highlighting pre-production collection.":::

> [!NOTE]
> Only a user with the **Full Administrator** security role and the **All** security scope can change these settings.

## Configure client upgrades during site update

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Updates and Servicing** node. Select an available update, and then in the ribbon select **Install Update Pack**.

    For more information on installing updates, see [Updates for Configuration Manager](../../../servers/manage/updates.md).

1. During installation of the update, on the **Client Options** page of the wizard, select **Test in pre-production collection**.

1. Complete the rest of the wizard and install the update pack.

After the wizard complete, clients in the pre-production collection will begin to deploy the updated client. You can monitor the deployment of upgraded clients in the console. Go to the **Monitoring** workspace, expand **Client Status**, and select the **Pre-production Client Deployment** node. For more information, see [How to monitor client deployment status](../../deploy/monitor-client-deployment-status.md).

> [!NOTE]
> For computers in a pre-production collection that also host site system roles, their deployment status may report as **Not compliant**. This state may show even when the client was successfully updated. When you promote the client to production, the deployment status reports correctly.

## Promote a new client to production

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Updates and Servicing** node. In the ribbon, select **Promote Pre-production Client**.

    > [!TIP]
    > The **Promote Pre-production Client** action is also available when you monitor client deployments in the console at **Monitoring** > **Client Status** > **Pre-production Client Deployment**.

1. Review the client versions in production and pre-production, and make sure the correct pre-production collection is specified. When ready, select **Promote**, and then select **Yes** to confirm.

The updated client version now replaces the client version in use in your hierarchy. You can then upgrade the clients for your whole site. For more information, see [How to upgrade clients for Windows computers](upgrade-clients-for-windows-computers.md).

> [!NOTE]
> To enable the pre-production client, or to promote a pre-production client to a production client, your account must be a member of a security role that has **Read** and **Modify** permissions for the **Update Packages** object.
>
> Client upgrades honor any Configuration Manager maintenance windows you configure. For more information on a known issue, see [Client upgrade and maintenance windows](upgrade-clients-for-windows-computers.md#client-upgrade-and-maintenance-windows).

## Known issues

### Pre-production client and site server high availability

<!-- 13846674 -->
Consider the following scenario:

- You enable the pre-production client.
- The site has a [site server in passive mode](../../../servers/deploy/configure/site-server-high-availability.md).
- You update the site to the latest version.
- You promote the passive mode site server to the active site server.

After you promote the site server, the pre-production client version shows as the production version. Depending on your configuration, it may automatically deploy to all systems.

When you install an update, Configuration Manager currently updates the **Client** folder of the site server in passive mode with the pre-production client version.

To work around this issue:

- Wait to promote the site server in passive mode until after you promote the pre-production client version to production version.

- If you have to fail over for high availability, manually correct the client version in the **Client** folder.

## Next steps

[How to exclude clients from upgrade](exclude-clients-windows.md)

[How to upgrade clients for Windows computers](upgrade-clients-for-windows-computers.md)
