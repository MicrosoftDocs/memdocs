---
title: External notifications
titleSuffix: Configuration Manager
description: Enable the site to send notifications to an external system or application.
ms.date: 09/18/2023
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# External notifications

*Applies to: Configuration Manager (current branch)*

<!--9504414-->

In a complex IT environment, you may have an automation system like [Azure Logic Apps](/azure/logic-apps/logic-apps-overview). Customers use these systems to define and control automated workflows to integrate multiple systems. You could integrate Configuration Manager into a separate automation system through the product's SDK APIs. But this process can be complex and challenging for IT professionals without a software development background.

Starting in version 2107, you can enable the site to send notifications to an external system or application. This feature simplifies the process by using a web service-based method. You configure [subscriptions](configure-alerts.md) to send these notifications. These notifications are in response to specific, defined events as they occur. For example, [status message filter rules](use-status-system.md#manage-status-filter-rules).

> [!NOTE]
> The external system or application defines and provides the methods that this feature calls.

When you set up this feature, the site opens a communication channel with the external system. That system can then start a complex workflow or action that doesn't exist in Configuration Manager.

Starting in version 2111, use the Configuration Manager console to create or edit subscriptions for external notifications. This article now focuses on that experience. If you're using version 2107, see [Configuration Manager version 2107](#configuration-manager-version-2107).<!-- 10615989 -->

## Prerequisites

- Create the subscription on the top-level site of the hierarchy. This site is either a standalone primary site, or a central administration site (CAS). You can view and modify an existing subscription on any site in a hierarchy.<!-- 12510324 -->

- The site's service connection point needs to be in online mode. For more information, see [About the service connection point](../deploy/configure/about-the-service-connection-point.md).

- Currently, this feature only supports Azure Logic Apps as the external system. An active Azure subscription with rights to create a logic app is required.

    The service connection point needs to communicate with the notification service, for example Azure Logic Apps. For more information, see [Internet access requirements](../../plan-design/network/internet-endpoints.md#external-notifications).

- To create an event type for an application approval request, the site needs an app that requires approval and is deployed to a user collection. For more information, see [Deploy applications](../../../apps/deploy-use/deploy-applications.md) and [Approve applications](../../../apps/deploy-use/app-approval.md).

### Permissions

You can configure the following permissions to the **NotificationSubscription** object: Read, Delete, Modify, Create.<!-- 12510324 -->

- The **Full administrator** default security role has these permissions.
- The **Read only analyst** default security role has the **Read** permission.

In version 2107, users also need the **All** security scope. In version 2111 and later, you can't scope the subscription objects. If needed, you can use scopes on the **Site** object, to which users need at least read permission.

Other permissions may be required for custom roles. Use the following table to understand what's needed:

| Action              | Alerts:<br>Read | Site:<br>Read | Notify:<br>Read | Notify:<br>Modify                | Notify:<br>Create                | Notify:<br>Delete | Site:<br>Manage SFR |
|---------------------|-----------------|---------------|-----------------|----------------------------------|----------------------------------|-------------------|---------------------|
| View subscription   | X               |               | X               |                                  |                                  |                   |                     |
| Modify subscription | X               | X             | X               | X                                |                                  |                   |                     |
| Create subscription <sup>[Note 1](#bkmk_note1)</sup> | X               | X             | X               |                                  | X                                |                   |                     |
| Delete subscription | X               |               | X               |                                  |                                  | X                 |                     |
| Create new SFR      | X               | X             | X               | <sup>[Note 2](#bkmk_note2)</sup> | <sup>[Note 2](#bkmk_note2)</sup> |                   | X                   |
| Add existing SFR    | X               | X             | X               | <sup>[Note 2](#bkmk_note2)</sup> | <sup>[Note 2](#bkmk_note2)</sup> |                   |                     |
| Add app approval    | X               | X             | X               | <sup>[Note 2](#bkmk_note2)</sup> | <sup>[Note 2](#bkmk_note2)</sup> |                   |                     |

The above table uses the following shorthand:

- **Notify**: **Notification subscription** objects
- **SFR**: Status filter rule

#### <a name="bkmk_note1"></a> Note 1: Top-level site in hierarchy

Create the subscription on the top-level site of the hierarchy. This site is either a standalone primary site, or a CAS. You can view and modify an existing subscription on any site in a hierarchy.<!-- 12510324 -->

#### <a name="bkmk_note2"></a> Note 2: Modify and Create permissions for event actions

When managing events on the subscription, the permissions to **Modify** or **Create** on the **Notification subscription** object depend upon whether you need to modify or create the event. For example, if you have the **Create** permission, then you can add a status filter rule to the subscription. If you don't have the **Modify** permission, then you can't make changes to the subscription events.

## Create an Azure logic app and workflow

Use the following process to create a sample app in Azure Logic Apps to receive the notification from Configuration Manager.

> [!NOTE]
> This process is provided as an example to help you get started. It's not intended for production use.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the Azure search box, enter `logic apps`, and select **Logic Apps**.

1. Select **Add** and choose **Consumption**. This action creates a new logic app.

1. On the **Basics** tab, specify the project details as necessary for your environment: subscription name, resource group, logic app name, and region.

1. Select **Review + create**. On the validation page, confirm the details that you provided, and select **Create**.

1. Under **Next steps**, select **Go to resource**.

1. Under the section to **Start with a common trigger**, select **When a HTTP request is received**.

1. At the bottom of the trigger editor, select **Use sample payload to generate schema**.

1. Paste the following sample payload:

    ```json
    {
        "EventID":0,
        "EventName":"",
        "SiteCode":"",
        "ServerName":"",
        "MessageID":0,
        "Source":"",
        "EventPayload":""
    }
    ```

1. Select **Done** and then select **Save**.

1. Copy the generated URL for the logic app. You'll use this URL later when you create the subscription in Configuration Manager.

    > [!NOTE]
    > The URL from Azure for the logic app includes the secret key. When saved in Configuration Manager, it's protected the same as any other password or secret key. If your environment uses a proxy server or other network inspection device, there's a risk that it will log this URL and expose the secret key. Control access to such systems, and be prepared to renew the secret key for the logic app in the Azure portal. You can also set an expiration date for the secret key in the Azure portal. For more information, see [Secure your logic apps](/azure/logic-apps/logic-apps-securing-a-logic-app#generate-shared-access-signatures-sas).<!-- 10060737 -->

1. To add a new step in the designer, select **+ New Step**. Choose an appropriate action when it receives a notification from Configuration Manager. For example:

    - To send an email, use the [Office 365 Outlook connector](/azure/connectors/connectors-create-api-office365-outlook).
    - To post a message to Teams, use the [Microsoft Teams connector](/connectors/teams/).

    Sign in if necessary and complete the required information for the action. For more information, see the [Create logic apps](/azure/logic-apps/quickstart-create-first-logic-app-workflow#add-an-action) quickstart in the Azure Logic Apps documentation.

### Notification schema

These notifications use the following standardized schema:

```json
{
    "properties": {
        "EventID": {
            "type": "integer"
        },
        "EventName": {
            "type": "string"
        },
        "EventPayload": {
            "type": "string"
        },
        "MessageID": {
            "type": "string"
        },
        "ServerName": {
            "type": "string"
        },
        "SiteCode": {
            "type": "string"
        },
        "Source": {
            "type": "string"
        }
    },
    "type": "object"
}
```

## Create an event

<!-- 10615989 -->

There are two types of events that are currently supported:

- The site raises a status message that matches conditions specified in a status filter rule for external notification. You can create a new rule or use an existing one.

- A user requests approval for an application in Software Center.

> [!NOTE]
> In a hierarchy, the scope of events depends upon the event type:
>
> - Application approval events only happen at primary sites.
> - Status filter rules apply to the site where you create the rule using the **Create external service notification event wizard**.
>   - If you run the wizard to create the event while connected to the CAS, it only triggers on matching events from the CAS.
>   - To subscribe to events raised by a child primary site, connect to the primary site. Modify the notification subscription to create a new status filter rule for the child primary site.<!-- 12510324 -->

Use the following process to create an event:

1. In the Configuration Manager console, connect to the top-level site of the hierarchy. This site is either a standalone primary site, or a CAS.

1. Go to the **Monitoring** workspace, expand **Alerts**, and select the **External service notifications** node.

1. In the ribbon, select **Create subscription**.

1. In the New Subscription window, specify a **Name** for the subscription to identify it in the Configuration Manager console. The maximum length is 254 characters. Optionally add a **Description**.

1. For the **External service URL** value, paste the URL of the Azure Logic App that you previously copied.

1. Select the gold asterisk :::image type="icon" source="media/new-icon.png" border="false"::: to add a new event to the subscription.

    1. In the Create External Service Notification Event wizard, on the Event type page, select one of the following event types:

        - **New status filter rule**: Create a new status filter rule to use for this event. Specify a name for the status filter rule, and then configure the filter criteria. For more information about criteria for status message rules, see [Use the status system](use-status-system.md).

            > [!IMPORTANT]
            > Be cautious with the type of status filter rule that you create. For external notifications, the site can process 300 status messages every five minutes. If your rule allows more messages than this limit, it will cause a backlog on the site. Create rules with narrow filters for specific scenarios. Avoid generic rules that allow a lot of messages.

        - **Existing status filter rule**: Reuse a status filter rule for external notification that already exists. It doesn't display all status filter rules, only the rules that you created using this wizard.

        - **User submits application request**: Send an external notification for application approval requests.

## Manage events

After you create a subscription, use the **External service notifications** node to do the following actions:

- **Properties**: Edit the name, description, or events for a subscription. You can't edit the external service URL.

- **Delete**: Remove a subscription.

> [!NOTE]
> You can view and modify an existing subscription on any site in a hierarchy.

When you select a subscription, the details pane shows information about the events that have happened.

## Trigger an event

The process to trigger an event depends upon the type of subscription:

- For a status filter rule, trigger an event for the site component. For example, use the [Configuration Manager Service Manager](../deploy/configure/site-components.md#configuration-manager-service-manager) to restart the component.

- For an app approval request, use Software Center to request an app that requires approval. For more information, see [Software Center user guide](../../understand/software-center.md#install-an-application).

## Monitor the workflow

### Configuration Manager Console
Starting in version 2309, when Azure Logic Apps generate notifications or alerts related to specific events or conditions, Configuration Manager can now capture and display these notifications. This integration enables the monitoring of Azure Logic App notifications directly within the Configuration Manager console, providing a centralized location for tracking critical events, taking appropriate actions and maintain a high level of operational efficiency. 

To use this feature a valid **Microsoft Entra Web app** is required. Please deploy the Azure services for **Administration Service Management** under Administration\Overview\Cloud Services\Azure Services. If the service is already deployed, admin can use the existing web application to view **Run details** from Azure logic app.

For more information, see [Configure Azure services for use with Configuration Manager](../deploy/configure/azure-services-wizard.md).

Use the following process to view Run Details of subscription:

1. In the Configuration Manager console  click **Monitoring**.
2. In the Monitoring workspace, click **External Service Notifications** and select the desired subscription.
3. Click on **Show Details**. 
4. In the dialog box, Select the Azure Environment, Microsoft Entra tenant name from the drop down and SignIn using your **Azure Admin Account**. 
5. Select the Subscription ID and enter the **Resource group** name and **Workflow** name.
6. Click on **Get Run Details** button to view the **Run Details**.

 :::image type="content" source="media/17668438-external-service.png" alt-text="Screenshot of the Run Details wizard in Configuration Manager console.":::

### Azure Portal

Within five minutes, the event triggers the logic app workflow. Check the status of the workflow in the Azure portal. Navigate to the **Runs history** page of the logic app.

For more information, see [Monitor run status, review trigger history, and set up alerts for Azure Logic Apps](/azure/logic-apps/monitor-logic-apps).

## Troubleshoot

Use the following Configuration Manager log files on the site server to help troubleshoot this process:

- **ExternalNotificationsWorker.log**: Check if the queue has been processed and notifications are sent to external system.
- **statmgr.log**: Check if the status filter rules have been processed without errors

## Known issues

If you create a status filter rule, you'll see it in the site's list of **Status filter rules** in the Configuration Manager console. If you make a change on the **Actions** tab of the rule properties, the external notification won't work.

After you [recover a central administration site](recover-sites.md) (CAS), delete and recreate the subscription.<!-- 10333966 -->

> [!TIP]
> Before you [remove a CAS](../deploy/install/remove-central-administration-site.md), recreate the subscriptions at the child primary site.

## Configuration Manager version 2107

> [!IMPORTANT]
> This section and the PowerShell script only apply to version 2107. In version 2111 and later, [use the Configuration Manager console](#create-an-event) to create and manage events.

### Other prerequisites for version 2107

To create the objects in Configuration Manager version 2107, you need to use the PowerShell script **SetupExternalServiceNotifications.ps1**. Use the following script sample to properly get the PowerShell script to use for this feature:<!-- 10363343 -->

```powershell
$FileName = ".\SetupExternalServiceNotifications.ps1"
Invoke-WebRequest https://aka.ms/cmextnotificationscript -OutFile $FileName
(Get-Content $FileName -Raw).Replace("`n","`r`n") | Set-Content $FileName -Force
(Get-Content $FileName -Raw).TrimEnd("`r`n") | Set-Content $FileName -Force
```

> [!NOTE]
> **SetupExternalServiceNotifications.ps1** is digitally signed by Microsoft. This script sample downloads the file and fixes the line breaks to preserve the digital signature.

### Create an event in version 2107

There are two types of events that are supported in version 2107:

- The site raises a status message that matches conditions specified in a status filter rule.

- A user requests approval for an application in Software Center.

#### Create a status message event in version 2107

1. On the site server, run **SetupExternalServiceNotifications.ps1**. Since you're running it on the site server, enter `y` to continue.

1. Select option `2` to create a new status filter rule.

1. Specify a name for the new status filter rule.

1. Select message-matching criteria for the rule, and specify values to match. Specify `0` to not use a criterion.

    The following criteria are available:

    - **Source**: Client, SMS Provider, Site Server
    - **Site code**
    - **System**
    - **Component**
    - **Message type**: Milestone, Detail, Audit
    - **Severity**: Informational, Warning, Error
    - **Message ID**
    - **Property**
    - **Property value**

    For more information about criteria for status message rules, see [Use the status system](use-status-system.md).

    > [!IMPORTANT]
    > Be cautious with the type of status filter rule that you create. For external notifications, the site can process 300 status messages every five minutes. If your rule allows more messages than this limit, it will cause a backlog on the site. Create rules with narrow filters for specific scenarios. Avoid generic rules that allow a lot of messages.

1. Rerun the PowerShell script. Select option `3` to create a new subscription.

1. Specify a name and description for the subscription. Then specify the logic app URL that you previously copied from the Azure portal.

1. Select the new status filter rule.

1. Select `0` to exit the script.

#### Create an app approval event in version 2107

> [!NOTE]
> This event type requires an application that requires approval and is deployed to a user collection. For more information, see [Deploy applications](../../../apps/deploy-use/deploy-applications.md) and [Approve applications](../../../apps/deploy-use/app-approval.md).

1. On the site server, run **SetupExternalServiceNotifications.ps1**. Since you're running it on the site server, enter `y` to continue.

1. Select option `3` to create a new subscription.

1. Specify a name and description for the subscription. Then specify the logic app URL that you previously copied from the Azure portal.

1. Select the appropriate event for an application request.

1. Select `0` to exit the script.

### Remove a subscription in version 2107

If you need to delete a subscription, use the following process:

1. Run the **SetupExternalServiceNotifications.ps1** script with option `1` to list the available subscriptions. Note the subscription ID, which is an integer value.

1. Use the **NotificationSubscription** API of the administration service. Make a DELETE call to the URI `https://<SMSProviderFQDN>/AdminService/v1.0/NotificationSubscription/<Subscription_ID>`.

    For more information, see [How to use the administration service in Configuration Manager](../../../develop/adminservice/usage.md).

After you remove the subscription, the site doesn't send notifications to the external system.

### Script usage in version 2107

When you run **SetupExternalServiceNotifications.ps1**, it detects whether it's running on a site server:

- `Y`: Continue on the current server
- `N`: Specify the FQDN of a site server to use

If the script doesn't detect a site server, it prompts for an FQDN.

The following actions are then available:

- `0`: Skip/continue
- `1`: List available subscriptions
- `2`: Create a status filter rule to expose status messages
- `3`: Create a subscription. This option is only available for the top-level site.

> [!NOTE]
> This script is only supported for sites running version 2107 or later.

## Next steps

[Use the status system](use-status-system.md)

[Configure alerts](configure-alerts.md)
