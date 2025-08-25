---
title: Quickstart - Enroll Configuration Manager devices
titleSuffix: Microsoft Intune
description: In this quickstart, you enroll Configuration Manager devices into Endpoint analytics.
ms.date: 04/07/2025
ms.service: microsoft-intune
ms.subservice: endpoint-analytics
ms.topic: quickstart
author: MandiOhlinger
ms.author: mandia
manager: laurawi
# Customer intent: As an administrator, I want to enroll Configuration Manager devices into Endpoint analytics so that I can gain insights into the user experience.
ms.localizationpriority: high
ms.collection: highpri
---

# Quickstart: Enroll Configuration Manager devices into Endpoint analytics

This quickstart outlines prerequisites and instructions for enrolling Configuration Manager managed devices into Endpoint analytics. If your devices are co-managed and meet the [Intune device requirements](enroll-intune.md#intune-device-requirements), we recommend [using Intune to enroll them into Endpoint analytics](enroll-intune.md) instead of following the instructions in this article. You don't need to move any co-management workloads to Intune to enroll a co-managed device to Endpoint analytics via Intune.

## <a name="bkmk_prereq"></a> Prerequisites

Before you start this tutorial, make sure you have the following prerequisites:  

### Configuration Manager requirements

- A minimum of Configuration Manager version 2002 with [KB4560496 - Update rollup for Microsoft Configuration Manager version 2002](https://support.microsoft.com/help/4560496) or later
- The Configuration Manager clients upgraded to version 2002 (including [KB4560496](https://support.microsoft.com/help/4560496)) or later
- [Microsoft Intune tenant attach](../configmgr/tenant-attach/device-sync-actions.md) enabled.

> [!IMPORTANT]  
> If you have co-management enabled, enrolled devices that meet the Intune requirements send required functional data directly to Microsoft public cloud. For more information, see [requirements for devices managed by Intune](overview.md#bkmk_intune_prereq).

### Licensing Prerequisites

Devices enrolled in Endpoint analytics need a valid license for the use of Microsoft Intune. For more information, see [Microsoft Intune licensing](../intune-service/fundamentals/licenses.md) or [Microsoft Configuration Manager licensing](../configmgr/core/understand/learn-more-editions.md). There are some more licensing requirements for Proactive remediations. For more information, see the [Endpoint analytics licensing requirements overview](overview.md#licensing-prerequisites).

## Endpoint analytics permissions

- The [Intune Service Administrator role](../intune-service/fundamentals/role-based-access-control.md) is required to [start gathering data](#bkmk_onboard).
  - After the admin selects **Start** for gathering data, other read-only roles can view the data.

[!INCLUDE [Endpoint analytics permissions information](includes/endpoint-analytics-rbac.md)]

## <a name="bkmk_endpoints"></a> Endpoints required for Configuration Manager-managed devices

Configuration Manager-managed devices send data to Intune via the connector on the Configuration Manager role and they don't need directly access to the Microsoft public cloud. If your environment uses a proxy server, configure your proxy server to allow the following endpoints:

| Endpoint  | Function  |
|-----------|-----------|
| `https://graph.windows.net` | Used to automatically retrieve settings  when attaching your hierarchy to Endpoint analytics on Configuration Manager Server role. For more information, see [Configure the proxy for a site system server](../configmgr/core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Used to synch device collection and devices with Endpoint analytics on Configuration Manager Server role only. For more information, see [Configure the proxy for a site system server](../configmgr/core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

## Limitations

- Endpoint analytics insights aren't available for devices running Windows Server editions.
- Using multiple Configuration Manager hierarchies with a single Endpoint analytics instance isn't currently supported.

## <a name="bkmk_cm_enroll"></a> Enroll devices managed by Configuration Manager
<!--6051638, 5924760-->
Before you enroll Configuration Manager devices, verify the [prerequisites](#bkmk_prereq) including enabling [Microsoft Intune tenant attach](../configmgr/tenant-attach/device-sync-actions.md). Cloud attaching your environment was simplified starting from Configuration Manager 2111. You can use the recommended defaults to enable both Endpoint analytics and tenant attach at the same time. For more information, see [Enable cloud attach](..\configmgr\cloud-attach\enable.md).<!--10964629-->


### <a name="bkmk_cm_upload"></a> Enable data upload in Configuration Manager

1. In the Configuration Manager console, go to **Administration** > **Cloud Services** > **Cloud Attach**.
   - For version 2103 and earlier, select the **Co-management** node.
1. Select **CoMgmtSettingsProd** then select **Properties**.
1. On the **Configure upload** tab, check the option to **Enable Endpoint analytics for devices uploaded to Microsoft Endpoint Manager**

> [!IMPORTANT]
> When you enable Endpoint analytics data upload, your default client settings are automatically updated to allow managed endpoints to send relevant data to your Configuration Manager site server. If you use custom client settings, you may need to update and re-deploy them for data collection to occur. For more information on how to configure data collection, such as to limit collection only to a specific set of devices, see [Configuring Endpoint analytics data collection](#bkmk_cm_enable).

   :::image type="content" source="media/6051638-configure-upload-configmgr.png" alt-text="Enable Endpoint analytics for devices uploaded to Microsoft Endpoint Manager" lightbox="media/6051638-configure-upload-configmgr.png":::

### <a name="bkmk_onboard"></a> Onboard in the Endpoint analytics portal
Onboarding from  the Endpoint analytics portal is required for both  Configuration Manager and Intune managed devices. For more information about common issues, see [Troubleshooting device enrollment and startup performance](troubleshoot.md#bkmk_enrollment_tshooter).

[!INCLUDE [Endpoint analytics overview page information](includes/onboard.md)]

### <a name="bkmk_cm_enable"></a> Configure Endpoint analytics data collection in Configuration Manager

The **Enable Endpoint analytics data collection** client setting allows your managed endpoints to send data necessary for Endpoint analytics to your site server. This setting doesn't control whether data gets uploaded to the Microsoft Intune admin center.

The **Enable Endpoint analytics data collection** setting is enabled by default for devices targeted by only the default [client settings](../configmgr/core/clients/deploy/about-client-settings.md). If you're upgrading to version 2006 from Configuration Manager version 1910 or prior, the Endpoint analytics data collection policy is enabled in your custom client settings upon upgrade. You can enable or disable data collection by following the instructions: <!--7065447, 7741111-->

1. In the Configuration Manager console, go to **Administration** > **Client Settings** > **Default Client Settings**.
1. Right-click and select **Properties** then select the **Computer Agent** settings.
1. Set **Enable Endpoint analytics data collection** to **Yes** to configure devices for local data collection. Set to **No** to disable local data collection.

You can also modify the **Enable Endpoint analytics data collection** policy in custom client settings to configure a specific set of devices for local data collection. Don't forget to deploy or re-deploy your custom client setting after making changes.

   > [!IMPORTANT]
   > If you have an existing custom client agent setting that is deployed to your devices, you need to update the [**Enable Endpoint analytics data collection**](data-collection.md#bkmk_datacollection) option in that custom setting and select **Ok** for it to take effect.

## <a name="bkmk_view"></a> View the Overview page

You can't see your data immediately. The data needs to be gathered and the results calculated. For startup performance, the device must be restarted at least once. After your data is ready, information is updated on the **Overview** page, and is explained here in more detail:

[!INCLUDE [Endpoint analytics overview page information](includes/overview-page.md)]

## Next steps

[Enroll Intune devices](enroll-intune.md)
