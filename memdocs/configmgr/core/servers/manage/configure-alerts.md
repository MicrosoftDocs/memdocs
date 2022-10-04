---
title: Configure alerts
titleSuffix: Configuration Manager
description: Configure alerts to understand the state of your Configuration Manager environment.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Configure alerts in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configure alerts to understand the state of your Configuration Manager environment. Configuration Manager generates alerts by some operations when a specific condition occurs:

- Typically, when an error occurs that you need to resolve.

- To warn you that a condition exists, so that you can continue to monitor the situation.

Some alerts you configure, such as alerts for endpoint protection and client status. Configuration Manager automatically configures other alerts.

You can configure subscriptions to alerts. Subscriptions can send details by email, which increases your awareness of key issues.

## Manage general alerts

In the Configuration Manager console, go to the **Monitoring** workspace, expand **Alerts**, and then select **Active Alerts** or **All Alerts**.

The following actions are available on alerts in these nodes:

- **Postpone**: Suspend monitoring this alert until the specified date is reached. At that time, the site updates the state of the alert. You can only postpone an enabled alert. When you postpone an alert, you can also add a comment.

- **Edit Comments**: Enter a comment for the selected alerts. These comments display with the alert in the Configuration Manager console.

- **Configure**: Modify the name, severity, and definition for the selected alert. If you change the severity of the alert, this configuration affects how the alerts are displayed in the Configuration Manager console.

- **Create subscription**: Create an email subscription to the selected alert. For more information, see [Email alerts](#email-alerts).

## Configure client status alerts

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Device Collections** node.

1. Select the collection for which you want to configure alerts. In the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

    > [!NOTE]
    > You can't configure alerts for user collections.

1. Switch to the **Alerts** tab, and select **Add**.

    > [!NOTE]
    > The **Alerts** tab is only visible if your security role has permissions for alerts.

1. Choose the alerts that you want the site to generate when client status thresholds fall below a specific value:

    - Client check pass or no results for active clients falls below threshold (%)
    - Client remediation success falls below the threshold (%)
    - Client activity falls below threshold (%)

1. In the **Conditions** list of the **Alerts** tab, select each client status alert, and then specify the following information:

    - **Alert Name**: Accept the default name or enter a new name for the alert.

    - **Alert Severity**: Choose the alert level that displays in the Configuration Manager console: Information, Warning, or Critical.

    - **Raise alert if...**: Specify the threshold percentage for the alert.

1. Select **OK** to save the alerts and close the collection properties.

## Email alerts

You can create an email subscription for alerts. When the site triggers an alert, it can then send you email notification.

### Configure email notification for alerts  

Before you can subscribe to email alerts, you need to configure the site to send email notifications. You'll need information about an SMTP email server.

> [!TIP]
> If you use Microsoft 365, use the following information:
>
> - **SMTP server**: `smtp.office365.com`
> - **Port**: `587`
> - **This server requires an encrypted connection (SSL)**

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand **Alerts**, and select the **Subscriptions** node.

1. On the **Home** tab of the ribbon, in the **Create** group, select **Configure Email Notification**.

1. Specify the following information:

    - **Enable email notification for alerts**: Allow Configuration Manager to use an SMTP server to send email alerts.

    - **FQDN or IP Address of the SMTP server to send email alerts**: Enter the fully qualified domain name (FQDN) or IP address for the email server to use for these alerts.

    - **Port**: Specify the SMTP port for the email server to use for these alerts. For example, `587`.

    - **This server requires an encrypted connection (SSL)**: Require that the site creates an encrypted connection with the SMTP server.

    - **SMTP Server Connection Account**: Specify the authentication method for Configuration Manager to use to connect the email server.

        > [!IMPORTANT]
        > Specify an account that has the least possible permissions to send emails.

    - **Sender address for email alerts**: Specify the email address from which alert emails are sent.

    - **Test SMTP Server**: Sends a test email to the email address specified in **Sender address for email alerts**.

1. Select **OK** to save the settings and to close the window.

### Subscribe to email alerts  

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand **Alerts**, and select either **Active Alerts** or **All Alerts**.

1. Select an alert. On the **Home** tab of the ribbon, in the **Subscription** group, select **Create subscription**.

1. In the **New Subscription** window, specify the following information:

    - **Subscription name**: Enter a name to identify the email subscription. You can use up to 255 characters.

    - **Email address**: Enter the recipient email addresses to get this alert. Separate multiple email addresses with a semicolon (`;`).

    - **Email language**: Select the language for the email.

1. Select **OK** to close the **New Subscription** window and to create the email subscription.

To edit or delete a subscription, select the **Subscriptions** node under **Alerts**.

## Monitor alerts

You can view alerts in one of the **Alerts** node of the **Monitoring** workspace. Alerts have one of the following alert states:

- **Never triggered**: The component hasn't met the condition of the alert.

- **Active**: The site triggered the alert when the component met the condition.

- **Canceled**: The condition that caused the alert is now resolved.

- **Postponed**: An administrator suspended monitoring of the alert. Configuration Manager will evaluate the state of the alert at a later time.

- **Disabled**: An administrator disabled the alert. Configuration Manager doesn't update the alert even if the state of the alert changes.

When Configuration Manager generates an alert, you can take one of the following actions:

- Resolve the condition that caused the alert. For example, you resolve a network issue. After Configuration Manager detects that the issue no longer exists, the alert state changes to **Cancel**.

- If the alert is a known issue, postpone the alert until a specific time. At that later time, Configuration Manager updates the alert to its current state.

   You can only postpone an alert when it's active.

- Edit the **Comment** of an alert. This action informs other administrators that you're aware of the alert. For example, in the comment you can identify how to resolve the condition, provide information about the current status of the condition, or explain why you postponed the alert.

## External notifications

Starting in version 2107, you can enable the site to send notifications to an external system or application.<!--9504414--> This capability simplifies the process by using a web service-based method. You configure subscriptions to send these notifications. These notifications are in response to specific, defined events as they occur. For example, status message filter rules. For more information, see [External notifications](external-notifications.md).

## Next steps

[Configure endpoint protection alerts for a collection](../../../protect/deploy-use/endpoint-protection-configure.md)

[Configure client status alerts for a collection](../../../core/clients/deploy/configure-client-status.md)
