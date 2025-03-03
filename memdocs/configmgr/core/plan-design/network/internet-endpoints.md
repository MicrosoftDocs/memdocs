---
title: Internet access requirements
titleSuffix: Configuration Manager
description: Learn about the internet endpoints to allow for full functionality of Configuration Manager features.
ms.date: 04/08/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: reference
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz
---

# Internet access requirements

Some Configuration Manager features rely on internet connectivity for full functionality. If your organization restricts network communication with the internet using a firewall or proxy device, make sure to allow these endpoints.

<!-- SCCMDocs-pr #3403 -->

Configuration Manager uses the following Microsoft URL forwarding services throughout the product:

- `https://aka.ms`
- `https://go.microsoft.com`

Even if they're not explicitly listed in the following sections, you should always allow these endpoints.

## Service connection point

For more information, see [About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md).

[!INCLUDE [Internet endpoints for service connection point](includes/internet-endpoints-service-connection-point.md)]

## Updates and servicing

For more information, see [Updates and servicing](../../servers/manage/updates.md).

> [!TIP]
> Enable these endpoints for the [management insight](../../servers/manage/management-insights.md) rule, **Connect the site to the Microsoft cloud for Configuration Manager updates**.

- `*.akamaiedge.net`

- `*.akamaitechnologies.com`

- `*.manage.microsoft.com`

- `go.microsoft.com`

- `download.microsoft.com`

- `download.windowsupdate.com`

- `download.visualstudio.microsoft.com`

- `sccmconnected-a01.cloudapp.net`

- `definitionupdates.microsoft.com`

> [!NOTE]
> Starting March 2025, the **configmgrbits.azureedge.net** domain migrates to **configmgrbits.cdn.manage.microsoft.com**. No action is required if *.manage.microsoft.com traffic is already allowed.
- `configmgrbits.azureedge.net`

- `configmgrbits.cdn.manage.microsoft.com`

    > [!IMPORTANT]
    > This Azure endpoint only supports TLS 1.2 with specific cipher suites.<!-- 10424111 --> Make sure your environment supports these Azure configurations. For more information, see [Azure Front Door: TLS configuration FAQ](/azure/frontdoor/front-door-faq#tls-configuration).

- `cmbitsstore.blob.core.windows.net`

- `ceuswatcab01.blob.core.windows.net`

- `ceuswatcab02.blob.core.windows.net`

- `eaus2watcab01.blob.core.windows.net`

- `eaus2watcab02.blob.core.windows.net`

- `weus2watcab01.blob.core.windows.net`

- `weus2watcab02.blob.core.windows.net`

- `cmbitsstore.blob.core.windows.net`

- `umwatsonc.events.data.microsoft.com`

- `*-umwatsonc.events.data.microsoft.com`

## Windows servicing

For more information, see [Manage Windows as a service](../../../osd/deploy-use/manage-windows-as-a-service.md).

- `download.microsoft.com`

- `https://go.microsoft.com/fwlink/?LinkID=619849`

- `dl.delivery.mp.microsoft.com`

## Azure services

For more information, see [Configure Azure services for use with Configuration Manager](../../servers/deploy/configure/azure-services-wizard.md).

- `management.azure.com` (Azure public cloud)
- `management.usgovcloudapi.net` (Azure US Government cloud)

## Co-management

If you enroll Windows devices to Microsoft Intune for co-management, make sure those devices can access the endpoints required by Intune. For more information, see [Network endpoints for Microsoft Intune](/mem/intune-service/fundamentals/intune-endpoints).

## Microsoft Store for Business

If you integrate Configuration Manager with the [Microsoft Store for Business](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md), make sure the service connection point and targeted devices can access the cloud service. For more information, see [Microsoft Store for Business proxy configuration](/mem/intune-service/fundamentals/intune-endpoints).

## Delivery optimization

If you use delivery optimization, clients need to communicate with its cloud service: `*.do.dsp.mp.microsoft.com`

Distribution points that support Microsoft Connected Cache also require these endpoints.

For more information, see the following articles:

- [Delivery optimization FAQ](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)
- [Fundamental concepts for content management in Configuration Manager](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)
- [Microsoft Connected Cache with Configuration Manager](../hierarchy/microsoft-connected-cache.md)

## Cloud services

<!-- SCCMDocs-pr #3402 -->

For more information on the cloud management gateway (CMG), see [Plan for CMG](../../clients/manage/cmg/data-flow.md).

[!INCLUDE [Internet endpoints for cloud services](includes/internet-endpoints-cloud-services.md)]

## Software updates

Allow the active software update point to access the following endpoints so that WSUS and Automatic Updates can communicate with the Microsoft Update cloud service:

- `http://windowsupdate.microsoft.com`

- `http://*.windowsupdate.microsoft.com`

- `https://*.windowsupdate.microsoft.com`

- `http://*.update.microsoft.com`

- `https://*.update.microsoft.com`

- `http://*.windowsupdate.com`

- `http://download.windowsupdate.com`

- `http://download.microsoft.com`

- `http://*.download.windowsupdate.com`

- `http://ntservicepack.microsoft.com`

For more information on software updates, see [Plan for software updates](../../../sum/plan-design/plan-for-software-updates.md).

### Intranet firewall

You might need to add endpoints to a firewall that's between two site systems in the following cases:

- If child sites have a software update point
- If there's a remote active internet-based software update point at a site

#### Software update point on the child site

- `http://<FQDN for software update point on child site>`

- `https://<FQDN for software update point on child site>`

- `http://<FQDN for software update point on parent site>`

- `https://<FQDN for software update point on parent site>`

## Manage Microsoft 365 Apps

> [!NOTE]
> On April 21, 2020, Office 365 ProPlus was renamed to **Microsoft 365 Apps for enterprise**. For more information, see [Name change for Office 365 ProPlus](/deployoffice/name-change). You might still see references to the old name in the Configuration Manager console and supporting documentation while the console is being updated.

If you use Configuration Manager to deploy and update Microsoft 365 Apps for enterprise, allow the following endpoints:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` to synchronize the software update point for Microsoft 365 Apps for enterprise client updates

- `config.office.com` to create custom configurations for Microsoft 365 Apps for enterprise deployments

-  `https://clients.config.office.net` and `https://go.microsoft.com/fwlink/?linkid=2190568` to support deploying updates for Microsoft 365 Apps for enterprise

- `contentstorage.osi.office.net` to support the evaluation of Office add-in readiness<!-- MEMDocs#410 -->

- `clients.config.office.net` to retrieve the names of the files needed for a particular Microsoft 365 Apps update. For more information, see [Using the Microsoft 365 Apps file list API](/office/client-developer/shared/manageability-applications-with-the-office-365-click-to-run-installer#using-the-microsoft-365-apps-file-list-api).

Your top-level site server needs access to the following endpoint to download the Microsoft Apps 365 readiness file:

- Starting March 2, 2021: `https://omex.cdn.office.net/mirrored/sccmreadiness/SOT_SCCM_AddinReadiness.CAB`
   - Location before March 2, 2021: `https://contentstorage.osi.office.net/sccmreadinessppe/sot_sccm_addinreadiness.cab`

> [!NOTE]
> The location of this file is changing *March 2, 2021*.<!--edit this, placeholder line--> For more information, see [Download location change for Microsoft 365 Apps readiness file](https://techcommunity.microsoft.com/t5/configuration-manager-blog/download-location-change-for-microsoft-365-apps-readiness-file/ba-p/2110282).

## Configuration Manager console

Computers with the Configuration Manager console require access to the following internet endpoints for specific features:

> [!NOTE]
> For push notifications from Microsoft to show in the console, the service connection point needs access to `Configmgrbits.cdn.manage.microsoft.com`. It also needs access to this endpoint for [updates and servicing](#updates-and-servicing).

### In-console feedback

[!INCLUDE [Internet endpoints for product feedback](includes/internet-endpoints-product-feedback.md)]

For more information on this feature, see [Product feedback](../../understand/product-feedback.md).

### Community workspace

#### Documentation node

For more information on this console node, see [Using the Configuration Manager console](../../servers/manage/admin-console.md).

- `https://aka.ms`

- `https://raw.githubusercontent.com`

#### Community hub

For more information on this feature, see [Community hub](../../servers/manage/community-hub.md).

- `https://github.com`

- `https://communityhub.microsoft.com`

## Tenant attach

For more information, see [Enable tenant attach](../../../tenant-attach/device-sync-actions.md).

[!INCLUDE [Internet endpoints for tenant attach](includes/internet-endpoints-tenant-attach.md)]

## Endpoint analytics

For more information, see [Endpoint analytics proxy configuration](../../../../analytics/troubleshoot.md#bkmk_endpoints).

[!INCLUDE [Internet endpoints for Endpoint analytics](includes/internet-endpoints-endpoint-analytics.md)]

## Asset intelligence

<!-- memdocs#470 -->
If you use [asset intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md), allow the following endpoints for the service to synchronize:

- `https://sc.microsoft.com`
- `https://ssu2.manage.microsoft.com`

## Deploy Microsoft Edge

[!INCLUDE [Internet endpoints for deploying Microsoft Edge](includes/internet-endpoints-deploy-microsoft-edge.md)]

## External notifications

For more information, see [External notifications](../../servers/manage/external-notifications.md).

The service connection point needs to communicate with the notification service, for example Azure Logic Apps. The access endpoint for the logic app typically has the following format: `https://*.<RegionName>.logic.azure.com:443`. For example: `https://prod1.westus2.logic.azure.com:443`

To get the access endpoint for the logic app, and the associated IP addresses, use the following process:

1. In the Azure portal, under **Logic Apps**, select the logic app for your notification. For more information, see [Manage logic apps in the Azure portal](/azure/logic-apps/manage-logic-apps-with-azure-portal).
1. In the app's menu, in the **Settings** section, select **Properties**.
1. View or copy the values for the **Access endpoint** and the **Access endpoint IP addresses**.

## Microsoft public IP addresses

For more information on the Microsoft IP address ranges, see [Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602). These addresses update regularly. There's no granularity by service; Any IP address in these ranges could be used.

## Next steps

- [Ports used in Configuration Manager](../hierarchy/ports.md)

- [Proxy server support in Configuration Manager](proxy-server-support.md)
