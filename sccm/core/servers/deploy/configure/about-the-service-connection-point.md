---
title: Service connection point
titleSuffix: Configuration Manager
description: Learn about this Configuration Manager site system role, and understand and plan for its range of uses.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby


---

# About the service connection point in Configuration Manager

*Applies to: Configuration Manager (current branch)*

The service connection point is a site system role that provides several important functions for the hierarchy. Before you set up the service connection point, understand and plan for its range of uses. Planning for usage might affect how you set up this site system role:

- Download updates that apply to your Configuration Manager infrastructure. Only relevant updates for your infrastructure are made available based on usage data you upload.

- Upload usage data from your Configuration Manager infrastructure. You can control the level or amount of detail that you upload. For more information, see [Usage data levels and settings](/configmgr/core/servers/deploy/install/setup-reference#bkmk_usage).

- Deploy a [cloud management gateway](/configmgr/core/clients/manage/cmg/plan-cloud-management-gateway) in Azure

- Synchronize apps from the [Microsoft Store for Business and Education](/configmgr/apps/deploy-use/manage-apps-from-the-windows-store-for-business)

- Discover users and groups in [Azure Active Directory (Azure AD)](/configmgr/core/servers/deploy/configure/about-discovery-methods#azureaddisc)

- Use [Desktop Analytics](/configmgr/desktop-analytics/overview) to gain insights on Windows 10 update and app readiness

Each hierarchy supports a single instance of this role. It can only be installed at the top-tier site of your hierarchy, which is a central administration site (CAS) or stand-alone primary site. If you expand a stand-alone primary site to a larger hierarchy, uninstall this role from the primary site, and then install it at the CAS.

## <a name="bkmk_modes"></a> Modes of operation

The service connection point supports two modes of operation:

- **Online**: The service connection point automatically checks every 24 hours for updates. It downloads new updates that are available for your current infrastructure and product version to make them available in the Configuration Manager console.

- **Offline**: The service connection point doesn't connect to the Microsoft cloud service. To manually import available updates, use the [service connection tool](/configmgr/core/servers/manage/use-the-service-connection-tool).

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

When you install the service connection point on a site system server that's remote from the site server, configure the following requirements:

- The computer account of the site server must be a local admin on the computer that hosts a remote service connection point.

- Set up the site system server that hosts this role with a [site system installation account](/configmgr/core/plan-design/hierarchy/accounts#site-system-installation-account). The distribution manager on the site server uses the site system installation account to transfer updates from the service connection point.

## <a name="bkmk_urls"></a> Internet access requirements

If your organization restricts network communication with the internet using a firewall or proxy device, you need to allow the service connection point to access internet endpoints.

For more information, see [Internet access requirements](/configmgr/core/plan-design/network/internet-endpoints#bkmk_scp).

## Install

When you run **Setup** to install the top-tier site of a hierarchy, you can install the service connection point.

After setup runs, or if you're reinstalling the role, use the **Add Site System Roles** wizard or the **Create Site System Server** wizard. (Only install the service connection point on the top-tier site of your hierarchy.) For more information, see [Install site system roles](/configmgr/core/servers/deploy/configure/install-site-system-roles).

## <a name="bkmk_move"></a> Move the role

<!-- SCCMDocs#922 -->
There are several scenarios in which you may need to move the service connection point to another server:

- [Recovery](/configmgr/core/servers/manage/recover-sites)
- [Site server high availability](/configmgr/core/servers/deploy/configure/site-server-high-availability)
- [Site expansion](/configmgr/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand)

After you move the service connection point, check all site functions. For example, you may need to renew the secret key for any connections to Azure Active Directory (Azure AD) tenants. For more information, see [Renew secret key](/sccm/core/servers/deploy/configure/azure-services-wizard#bkmk_renew).

## Log files

To view information about uploads to Microsoft, view the **Dmpuploader.log** on the server that runs the service connection point. For download progress of updates, view the **Dmpdownloader.log**. For the complete list of logs related to the service connection point, see [Log files - Service connection point](/configmgr/core/plan-design/hierarchy/log-files#BKMK_WITLog).

## Next steps

Use the following flowcharts to understand the process flow and key log entries. This process includes update downloads and replication of updates to other sites.

- [Flowchart - Download updates](/configmgr/core/servers/manage/download-updates-flowchart)

- [Flowchart - Update replication](/configmgr/core/servers/manage/update-replication-flowchart)
