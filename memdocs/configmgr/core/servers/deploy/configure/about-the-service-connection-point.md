---
title: Service connection point
titleSuffix: Configuration Manager
description: Learn about this Configuration Manager site system role, and understand and plan for its range of uses.
ms.date: 10/12/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.author: gokarthi
author: gowdhamankarthikeyan
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# About the service connection point in Configuration Manager

*Applies to: Configuration Manager (current branch)*

The service connection point is a site system role that provides several important functions for the hierarchy. Before you set up the service connection point, understand and plan for its range of uses. Planning for usage might affect how you set up this site system role:

- Download updates that apply to your Configuration Manager infrastructure. Only relevant updates for your infrastructure are made available based on usage data you upload.

- Upload usage data from your Configuration Manager infrastructure. You can control the level or amount of detail that you upload. For more information, see [Usage data levels and settings](../install/setup-reference.md#bkmk_usage).

- Deploy a [cloud management gateway](../../../clients/manage/cmg/overview.md) in Azure

- Synchronize apps from the [Microsoft Store for Business and Education](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)

- Discover users and groups in [Azure Active Directory (Azure AD)](about-discovery-methods.md#azureaddisc)

- Use [Desktop Analytics](../../../../desktop-analytics/overview.md) to gain insights on Windows 10 update and app readiness

Each hierarchy supports a single instance of this role. It can only be installed at the top-tier site of your hierarchy, which is a central administration site (CAS) or stand-alone primary site. If you expand a stand-alone primary site to a larger hierarchy, uninstall this role from the primary site, and then install it at the CAS.

## <a name="bkmk_modes"></a> Modes of operation

The service connection point supports two modes of operation:

- **Online**: The service connection point automatically checks every 24 hours for updates. It downloads new updates that are available for your current infrastructure and product version to make them available in the Configuration Manager console.

- **Offline**: The service connection point doesn't connect to the Microsoft cloud service. To manually import available updates, use the [service connection tool](../../manage/use-the-service-connection-tool.md).

### Change mode

If you change between online or offline modes after you install the service connection point, restart the **SMS_DMP_DOWNLOADER** thread of the SMS_Executive service. Restarting this thread makes the change become effective. To restart this thread, use the Configuration Manager Service Manager.

> [!TIP]
> You can also restart the SMS_Executive service for Configuration Manager, which restarts most site components. Alternatively, wait for a scheduled task like a site backup, which stops and restarts the SMS_Executive service for you.

To use the Configuration Manager Service Manager to restart the SMS_DMP_DOWNLOADER thread:

1. In the Configuration Manager console go to the **Monitoring** workspace, expand **System Status**, and select the **Component Status** node. In the ribbon, choose **Start**, and then select **Configuration Manager Service Manager**.

1. In the service manager navigation pane, expand the site, expand **Components**, and then choose the component that you want to restart: **SMS_DMP_DOWNLOADER**.

1. Go to the **Component** menu, and choose **Query**.

1. Confirm the current status of the component. Then go to the **Component** menu, and choose **Stop**.  

1. **Query** the component again to confirm that it stopped. Then choose the **Start** component action to restart it.

## Remote site system requirements

When you install the service connection point on a site system server that's remote from the site server, configure one of the following requirements:

- The computer account of the site server must be a local admin on the computer that hosts a remote service connection point.

  or<!-- MEMDocs#1479 -->

- Set up the site system server that hosts this role with a [site system installation account](../../../plan-design/hierarchy/accounts.md#site-system-installation-account). The distribution manager on the site server uses the site system installation account to transfer updates from the service connection point.

## Internet access requirements

If your organization restricts network communication with the internet using a firewall or proxy device, you need to allow the service connection point to access internet endpoints.

For more information, see [Internet access requirements](../../../plan-design/network/internet-endpoints.md). Other Configuration Manager features may require additional endpoints from the service connection point.

[!INCLUDE [Internet endpoints for service connection point](../../../plan-design/network/includes/internet-endpoints-service-connection-point.md)]

## Validate internet access

<!--8565578-->

If you use Desktop Analytics or tenant attach, starting in version 2010, the service connection point now checks important internet endpoints. These checks help make sure that the cloud-connected services are available. It also helps you troubleshoot issues by quickly determining if network connectivity is a problem.

For the list of internet endpoints, see the following sections of the **Internet access requirements** article:

- [Desktop Analytics](../../../plan-design/network/internet-endpoints.md#desktop-analytics)
- [Tenant attach](../../../plan-design/network/internet-endpoints.md#tenant-attach)

For more details, review the **EndpointConnectivityCheckWorker.log** file on the service connection point.

A failure isn't always determined by the HTTP status code, but if there's network connectivity to an endpoint. The following scenarios can cause a check to fail:

- Network connection timeout
- SSL/TLS failure
- Unexpected status code:

  | Status code | Description | Possible reason |
  |---------|---------|---------|
  | 407 | Proxy authentication required | May indicate a proxy issue |
  | 408 | Request timeout | May indicate a proxy issue |
  | 426 | Upgrade required | May indicate a TLS misconfiguration |
  | 451 | Unavailable for legal reasons | May indicate a proxy issue |
  | 502 | Bad gateway | May indicate a proxy issue |
  | 511 | Network authentication required | May indicate a proxy issue |
  | 598 | Network read timeout error | Not RFC compliant, but used by some proxy servers to indicate a network timeout |
  | 599 | Network connection timeout error | Not RFC compliant, but used by some proxy servers to indicate a network timeout |

There are also the following status messages for the **SMS_SERVICE_CONNECTOR** component:

| Message ID | Severity | Notes |
|---------|---------|---------|
| 11410 | Informational | All checks are successful |
| 11411 | Warning | One or more non-critical failures occurred |
| 11412 | Error | One or more critical failures occurred |

## Install

When you run **Setup** to install the top-tier site of a hierarchy, you can install the service connection point.

After setup runs, or if you're reinstalling the role, use the **Add Site System Roles** wizard or the **Create Site System Server** wizard. (Only install the service connection point on the top-tier site of your hierarchy.) For more information, see [Install site system roles](install-site-system-roles.md).

## <a name="bkmk_move"></a> Move the role

<!-- SCCMDocs#922 -->
There are several scenarios in which you may need to move the service connection point to another server:

- [Recovery](../../manage/recover-sites.md)
- [Site server high availability](site-server-high-availability.md)
- [Site expansion](../install/setup-wizard-central-primary.md#expand-a-stand-alone-primary-site)

After you move the service connection point, check all site functions. For example, you may need to renew the secret key for any connections to Azure Active Directory (Azure AD) tenants. For more information, see [Renew secret key](azure-services-wizard.md#bkmk_renew).

## <a name="bkmk_notifications"></a> Console notifications for the service connection point
<!--11047451-->
Occasionally, the Configuration Manager console may give you a [notification](../../manage/admin-console-notifications.md) about your service connection point. The notification asks you to restart the SMS_EXECUTIVE service on the server that hosts the service connection point. This notification occurs  because a configuration change was made by Microsoft on the services that your service connection point connects to. Features of Configuration Manager that rely on these services may not function for your site properly until the SMS_EXECUTIVE service is restarted.
## Log files

To view information about uploads to Microsoft, view the **Dmpuploader.log** on the server that runs the service connection point. For download progress of updates, view the **Dmpdownloader.log**. For the complete list of logs related to the service connection point, see [Log files - Service connection point](../../../plan-design/hierarchy/log-files.md#BKMK_WITLog).

## Next steps

Use the following flowcharts to understand the process flow and key log entries. This process includes update downloads and replication of updates to other sites.

- [Flowchart - Download updates](../../manage/download-updates-flowchart.md)

- [Flowchart - Update replication](../../manage/update-replication-flowchart.md)
