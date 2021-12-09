---
title: Monitor the CMG
titleSuffix: Configuration Manager
description: Monitor clients and network traffic through the cloud management gateway (CMG).
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Monitor the CMG

*Applies to: Configuration Manager (current branch)*

After the cloud management gateway (CMG) is running and clients are connecting through it, you can monitor clients and network traffic. Monitor the service to make sure its performance is optimal.

## Monitor clients

Clients connected through the CMG appear in the Configuration Manager console the same way on-premises clients do. For more information, see [how to monitor clients](../monitor-clients.md).

## Monitor traffic in the console

Monitor traffic on the CMG using the Configuration Manager console:

1. Go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Management Gateway** node.

1. Select the CMG in the list pane.

1. View the traffic information in the details pane for the CMG connection point and the site system roles it connects to. These statistics show the client requests coming into these roles. The requests include policy, location, registration, content, inventory, and client notifications.<!-- SCCMDocs#1208 -->

## Monitor content

Monitor content that you distribute to a CMG the same as with any other distribution point. For more information, see [Monitor content](../../../servers/deploy/configure/monitor-content-you-have-distributed.md).

When you view the list of CMGs in the console, you can add more columns to the list. For example, the **Storage egress (GB)** column shows the amount of data that clients downloaded from the service in the last 30 days.

## Monitor logs

[!INCLUDE [Logs for cloud management gateway](../../../plan-design/hierarchy/includes/logs-cmg.md)]

## Cloud management dashboard

<!--1358461-->
The cloud management dashboard provides a centralized view for CMG usage. It also displays data about cloud users and devices.

In the Configuration Manager console, go to the **Monitoring** workspace. Select the **Cloud Management** node, and view the dashboard tiles.

The following screenshot shows the section of the cloud management dashboard specific for the CMG:

:::image type="content" source="media/cloud-management-dashboard-cmg.png" alt-text="Cloud management dashboard tiles CMG traffic and Current online clients." lightbox="media/cloud-management-dashboard-cmg.png":::

## Connection analyzer

To aid troubleshooting, use the CMG connection analyzer for real-time verification. The in-console utility checks the current status of the service, and the communication channel through the CMG connection point to any management points that allow CMG traffic.

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Cloud Services** and select the **Cloud management gateway** node.

1. Select the target CMG instance, and then select **Connection analyzer** in the ribbon.

1. In the CMG connection analyzer window, select one of the following options to authenticate with the service:

     1. **Azure AD user**: Use this option to simulate communication the same as a cloud-based user identity signed in to an Azure AD-joined Windows device. Select **Sign In** to securely enter the credentials for an Azure AD user account.

     1. **Client certificate**: Use this option to simulate communication the same as a Configuration Manager client with a [client authentication certificate](configure-authentication.md#pki-certificate).

1. Select **Start** to start the analysis. The analyzer window displays the results. Select an entry to see more details in the Description field.  

:::image type="content" source="media/cmg-connection-analyzer.png" alt-text="Example output for the cloud management gateway (CMG) connection analyzer.":::

## Set up outbound traffic alerts

Outbound traffic alerts help you know when network traffic approaches a 14-day threshold level. When you create the CMG, you can set up traffic alerts. If you skipped that part, you can still set up the alerts after the service is running. Adjust the alert settings at any time.

You can also configure thresholds for the amount of data that you want to store on the CMG and that clients download. Use alerts for these thresholds to help you decide when to stop or delete the cloud service, adjust the content that you store on the CMG, or modify which clients can use the service.

1. Go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Management Gateway** node.

1. Select the CMG in the list pane, and then select **Properties** in the ribbon.

1. Go to the **Alerts** tab to enable the threshold and alerts:

    - Specify the **14-day data threshold for outbound data transfer** in gigabytes (GB). This threshold helps you to monitor the amount of data that transfers from the CMG to clients every two weeks. By default, this threshold is **10 GB**. The site raises warning and critical alerts when transfers reach values that you define. By default, these alerts occur at 50% and 90% of the threshold.

    - If the CMG is content-enabled, also specify a **storage alert threshold**. This threshold sets an upper limit on the amount of content to store on the CMG. By default, this threshold is **2 GB**. Configuration Manager generates warning and critical alerts when the remaining free space reaches the levels that you specify. By default, these alerts occur at 50% and 90% of the threshold.

> [!NOTE]
> Alerts for the CMG depend on usage statistics from Azure, which can take up to 24 hours to become available. For more information about Storage Analytics for Azure, see [Storage Analytics](/azure/storage/common/storage-analytics).
>
> In an hourly cycle, the primary site that monitors the CMG downloads transaction data from Azure. It stores this transaction data in the `CloudDP-<ServiceName>.log` file on the site server. Configuration Manager then evaluates this information against the storage and transfer quotas for each CMG. When the transfer of data reaches or exceeds the specified volume for either warnings or critical alerts, Configuration Manager generates the appropriate alert.
>
> Because the site downloads information about data transfers from Azure every hour, the usage might exceed a warning or critical threshold before Configuration Manager can access the data and raise an alert.

## Stop CMG when it exceeds threshold

<!--3735092-->
Configuration Manager can stop a CMG service when the total data transfer goes over your limit. Use [alerts](#set-up-outbound-traffic-alerts) to trigger notifications when the usage reaches warning or critical levels. To help reduce any unexpected Azure costs because of a spike in usage, this option turns off the cloud service.

> [!IMPORTANT]
> Even if the service isn't running, there are still costs associated with the cloud service. Stopping the service doesn't eliminate all associated Azure costs. To remove all cost for the cloud service, [delete the CMG](modify-cloud-management-gateway.md#delete-the-service).
>
> When you stop the CMG service, internet-based clients can't communicate with Configuration Manager.

The total data transfer (egress) includes data from the cloud service and storage account. This data comes from the following flows:

- CMG to client
- CMG to site, including CMG log files
- If you enable CMG for content, storage account to client

For more information on these data flows, see [CMG ports and data flow](data-flow.md).

The storage alert threshold is separate. That alert monitors the capacity of your Azure storage instance.

When you select the CMG instance in the **Cloud Management Gateway** node in the console, you can see the total data transfer in the details pane.

Configuration Manager checks the threshold value every six minutes. If there's a sudden spike in usage, Configuration Manager can take up to six minutes to detect that it exceeded the threshold and then stop the service.

### Process to stop the cloud service when it exceeds threshold

1. [Set up outbound traffic alerts](#set-up-outbound-traffic-alerts).

2. On the **Alerts** tab of the CMG properties window, enable the option to **Stop this service when the critical threshold is exceeded**.

To test this feature, temporarily reduce one of the following values:

- **14-day threshold for outbound data transfer (GB)**. The default value is `10000`.

- **Percentage of threshold for raising Critical alert**. The default value is `90`.

## Next steps

If you need to change the configuration, you can modify the CMG:
  
> [!div class="nextstepaction"]
> [Modify a CMG](modify-cloud-management-gateway.md)
