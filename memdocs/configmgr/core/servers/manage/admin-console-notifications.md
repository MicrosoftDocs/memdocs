---
title: Configuration Manager console notifications
titleSuffix: Configuration Manager
description: Learn about notifications from the Configuration Manager console.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a0d709fa-c4f8-46e1-b432-582cc293be35
author: mestew
ms.author: mstewart
manager: dougeby
---

# Configuration Manager console notifications

*Applies to: Configuration Manager (current branch)*

<!--3556016, fka 1318035-->
Starting in Configuration Manager version 1902, the Configuration Manager console notifies you for specific events that occur. You can configure some of the event notifications for your Configuration Manager sites.

- Non-configurable event notifications:
   - When an update is available for Configuration Manager itself
   - When lifecycle and maintenance events occur in the environment
- Configurable event notifications:
   - [Non-critical site health changes](#bkmk_noncrit)
   - [Messages from Microsoft](#bkmk_msft) (starting in version 2006)

This notification is a bar at the top of the console window below the ribbon. It replaces the previous experience when Configuration Manager updates are available. These in-console notifications still display critical information, but don't interfere with your work in the console. You can't dismiss critical notifications. The console displays all notifications in a new notification area of the title bar.

![Notification bar and flag in console](./media/1318035-notify-eval-version-expired.png)

## <a name="bkmk_noncrit"></a> Configure a site to show non-critical notifications

You can configure each site to show non-critical notifications in the properties of the site.

1. In the **Administration** workspace, expand **Site Configuration**, then select the **Sites** node.
1. Select the site you want to configure for non-critical notifications.
1. In the ribbon, select **Properties**.
1. On the **Alerts** tab, select the option to **Enable console notifications for non-critical site health changes**.
   - If you enable this setting, all console users see critical, warning, and information notifications. This setting is enabled by default.  
   - If you disable this setting, console users only see critical notifications.  

Most console notifications are per session. The console evaluates queries when a user launches it. To see changes in the notifications, restart the console. If a user dismisses a non-critical notification, it notifies again when the console restarts if it's still applicable.

The following notifications reevaluate every five minutes:

- Site is in maintenance mode  
- Site is in recovery mode  
- Site is in upgrade mode  

Notifications follow the permissions of role-based administration. For example, if a user doesn't have permissions to see Configuration Manager updates, they won't see those notifications.

Some notifications have a related action. For example, if the console version doesn't match the site version, select **Install the new console version**. This action launches the console installer.

Starting in version 2006, if you configure Azure services to cloud-attach your site, you'll see notifications with an action to [renew the secret key](../deploy/configure/azure-services-wizard.md#bkmk_renew).<!--6386392--> The site evaluates the state of the following alerts once per hour:

- One or more Azure AD app secret keys will expire soon
- One or more Azure AD app secret keys have expired

The following notifications are most applicable to the technical preview branch:  

- Evaluation version is within 30 days of expiration (Warning): the current date is within 30 days of the expiration date of the evaluation version  
- Evaluation version is expired (Critical): the current date is past the expiration date of the evaluation version  
- Console version mismatch (Critical): the console version doesn't match the site version  
- Site upgrade is available (Warning): there's a new update package available  

For more information and troubleshooting assistance, see the **SmsAdminUI.log** file on the console computer. By default, this log file is at the following path: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log`.

## <a name="bkmk_msft"></a> Configure a site to receive messages from Microsoft
 <!--3953121-->

Starting in version 2006, you can choose to receive notifications from Microsoft in the Configuration Manager console. These notifications help you stay informed about new or updated features, changes to Configuration Manager and attached services, and issues that require action to remediate.

> [!NOTE]
> For push notifications from Microsoft to show in the console, the service connection point needs access to `configmgrbits.azureedge.net`. It also needs access to this endpoint for [updates and servicing](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates), so you may have already allowed it.

### Configure notification settings for Microsoft messages

1. Navigate to **Administration** > **Site Configuration** > **Sites**.

1. Select a site, and then in the ribbon, select **Properties**.

1. In the **Alerts** tab, enable the notifications by selecting **Receive messages from Microsoft**. You can deselect any of the following notifications if you prefer not to receive them:  

   - **Prevent/fix**: Known issues affecting your organization that may require you to take action.

   - **Plan for change**: Changes to Configuration Manager that may require you to take action.

   - **Stay informed**: Informs you of new or updated features that are available.

:::image type="content" source="media/3953121-microsoft-notifications.png" alt-text="Notification from Microsoft options in site properties" lightbox="media/3953121-microsoft-notifications.png":::

## Next steps

- [Use the console](admin-console.md)

- [Console tips](admin-console-tips.md)

- [Accessibility features](../../understand/accessibility-features.md)
