---
title: Quickstart - Enroll Configuration Manager devices
titleSuffix: Microsoft Endpoint Manager
description: In this quickstart, you enroll Configuration Manager devices into Endpoint analytics.
ms.date: 10/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: quickstart
ms.assetid: cbdd4a4a-2761-4e66-91eb-8602fb8b4926
author: mestew  
ms.author: mstewart
manager: dougeby

# Customer intent: As a Microsoft Endpoint Manager administrator, I want to enroll Configuration Manager devices into Endpoint analytics so that I can gain insights into the user experience.
---

# Quickstart: Enroll Configuration Manager devices into Endpoint analytics

This quickstart outlines prerequisites and instructions for enrolling Configuration Manager managed devices into Endpoint analytics. If your devices are co-managed and meet the [Intune device requirements](enroll-intune.md#intune-device-requirements), we recommend [using Intune to enroll them into Endpoint analytics](enroll-intune.md) instead of following the instructions in this quickstart. You do not need to move any co-management workloads to Intune to enroll a co-managed device to Endpoint analytics via Intune.

## <a name="bkmk_prereq"></a> Prerequisites

Before you start this tutorial, make sure you have the following prerequisites:  

### Configuration Manager requirements

- A minimum of Configuration Manager version 2002 with [KB4560496 - Update rollup for Microsoft Endpoint Configuration Manager version 2002](https://support.microsoft.com/help/4560496) or later
- The Configuration Manager clients upgraded to version 2002 (including [KB4560496](https://support.microsoft.com/help/4560496)) or later
- [Microsoft Endpoint Manager tenant attach](../configmgr/tenant-attach/device-sync-actions.md) enabled.

> [!Important]  
> If you have co-management enabled, enrolled devices that meet the Intune requirements will send required functional data directly to Microsoft public cloud. For more information, see [requirements for devices managed by Intune](overview.md#bkmk_intune_prereq).

### Licensing Prerequisites

Endpoint analytics is included in the following plans:

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) or higher
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) or higher.

## Endpoint analytics permissions

- The [Intune Service Administrator role](../intune/fundamentals/role-based-access-control.md) is required to [start gathering data](#bkmk_onboard).
   - After clicking **Start** for gathering data, other read-only roles can view the data.

[!INCLUDE [Endpoint analytics permissions information](includes/endpoint-analytics-rbac.md)]

## <a name="bkmk_endpoints"></a> Endpoints required for Configuration Manager-managed devices

Configuration Manager-managed devices send data to Intune via the connector on the Configuration Manager role and they don't need directly access to the Microsoft public cloud. If your environment uses a proxy server, configure your proxy server to allow the following endpoints:

| Endpoint  | Function  |
|-----------|-----------|
| `https://graph.windows.net` | Used to automatically retrieve settings  when attaching your hierarchy to Endpoint analytics on Configuration Manager Server role. For more information, see [Configure the proxy for a site system server](../configmgr/core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Used to synch device collection and devices with Endpoint analytics on Configuration Manager Server role only. For more information, see [Configure the proxy for a site system server](../configmgr/core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

## Limitations

- Endpoint analytics insights are not available for devices running Windows Server editions.
- Using multiple Configuration Manager hierarchies with a single Endpoint analytics instance is not currently supported.

## <a name="bkmk_cm_enroll"></a> Enroll devices managed by Configuration Manager
<!--6051638, 5924760-->
Before you enroll Configuration Manager devices, verify the [prerequisites](#bkmk_prereq) including enabling [Microsoft Endpoint Manager tenant attach](../configmgr/tenant-attach/device-sync-actions.md). 

### <a name="bkmk_cm_upload"></a> Enable data upload in Configuration Manager

1. In the Configuration Manager console, go to **Administration** > **Cloud Services** > **Co-management**.
1. Select **CoMgmtSettingsProd** then click **Properties**.
1. On the **Configure upload** tab, check the option to **Enable Endpoint analytics for devices uploaded to Microsoft Endpoint Manager**

> [!Important]
> When you enable Endpoint analytics data upload, your default client settings will be automatically updated to allow managed endpoints to send relevant data to your Configuration Manager site server. If you use custom client settings, you may need to update and re-deploy them for data collection to occur. For more details on this, as well as how to configure data collection, such as to limit collection only to a specific set of devices, see the section on [Configuring Endpoint analytics data collection](#bkmk_cm_enable).

   :::image type="content" source="media/6051638-configure-upload-configmgr.png" alt-text="Enable Endpoint analytics for devices uploaded to Microsoft Endpoint Manager" lightbox="media/6051638-configure-upload-configmgr.png":::

### <a name="bkmk_onboard"></a> Onboard in the Endpoint analytics portal
Onboarding from  the Endpoint analytics portal is required for both  Configuration Manager and Intune managed devices. For more information about common issues, see [Troubleshooting device enrollment and startup performance](troubleshoot.md#bkmk_enrollment_tshooter).

[!INCLUDE [Endpoint analytics overview page information](includes/onboard.md)]

### <a name="bkmk_cm_enable"></a> Configure Endpoint analytics data collection in Configuration Manager

The **Enable Endpoint analytics data collection** client setting allows your managed endpoints to send data necessary for Endpoint analytics to your site server. This setting does not control whether data gets uploaded to the Microsoft Endpoint Manager admin center.

Starting in Configuration Manager version 2006, the **Enable Endpoint analytics data collection** setting is enabled by default for devices targeted by only the default [client settings](../configmgr/core/clients/deploy/about-client-settings.md). If you're upgrading to version 2006 from Configuration Manager version 1910 or prior, the Endpoint analytics data collection policy will be enabled in your custom client settings upon upgrade. You can enable or disable data collection by following the instructions below: <!--7065447, 7741111-->

1. In the Configuration Manager console, go to **Administration** > **Client Settings** > **Default Client Settings**.
1. Right-click and select **Properties** then select the **Computer Agent** settings.
1. Set **Enable Endpoint analytics data collection** to **Yes** to configure devices for local data collection. Set to **No** to disable local data collection.

You may also modify the **Enable Endpoint analytics data collection** policy in custom client settings to configure a specific set of devices for local data collection. Don't forget to deploy or re-deploy your custom client setting after making changes.

   > [!Important]
   > If you have an existing custom client agent setting that's been deployed to your devices, you'll need to update the [**Enable Endpoint analytics data collection**](data-collection.md#bkmk_datacollection) option in that custom setting and select **Ok** for it to take effect.


## <a name="bkmk_view"></a> View the Overview page

[!INCLUDE [Endpoint analytics overview page information](includes/overview-page.md)]

## Next steps

[Enroll Intune devices](enroll-intune.md)
