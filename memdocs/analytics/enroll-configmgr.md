---
title: Quickstart - Enroll Configuration Manager devices
titleSuffix: Microsoft Endpoint Manager
description: In this quickstart, you enroll Configuration Manager devices into Endpoint analytics.
ms.date: 06/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: quickstart
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew  
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW 
# Customer intent: As a Microsoft Endpoint Manager administrator, I want to enroll Configuration Manager devices into Endpoint analytics so that I can gain insights into the user experience.
---

# Quickstart: Enroll Configuration Manager devices into Endpoint analytics

This quickstart outlines prerequisites and instructions for enrolling Configuration Manager devices into Endpoint analytics.

## <a name="bkmk_uea_prereq"></a> Prerequisites

Before you start this tutorial, make sure you have the following prerequisites:  

### Enrolling Configuration Manager devices requires:

- Configuration Manager version 2002 or newer
- Clients upgraded to version 2002 or newer
- [Microsoft Endpoint Manager tenant attach](../configmgr/tenant-attach/device-sync-actions.md) enabled.

### <a name="bkmk_uea_endpoints"></a> Endpoints required for Configuration Manager-managed devices

Configuration Manager-managed devices send data to Intune via the connector on the Configuration Manager role and they do not need directly access to the Microsoft public cloud. If your environment uses a proxy server, configure your proxy server to allow the following endpoints:

| Endpoint  | Function  |
|-----------|-----------|
| `https://graph.windows.net` | Used to automatically retrieve settings  when attaching your hierarchy to Endpoint analytics on Configuration Manager Server role. For more information, see [Configure the proxy for a site system server](../configmgr/core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Used to synch device collection and devices with Endpoint analytics on Configuration Manager Server role only. For more information, see [Configure the proxy for a site system server](../configmgr/core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### Licensing Prerequisites

Endpoint analytics is included in the following plans:

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) or higher
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) or higher.

### Endpoint analytics permissions

- The [Intune Service Administrator role](../intune/fundamentals/role-based-access-control.md) is required to [start gathering data](#bkmk_uea_start).
   - By clicking **Start**, you agree to and acknowledge that your customer data may be stored outside the location you selected when you provisioned your Microsoft Intune tenant.
   - After clicking **Start** for gathering data, other read-only roles can view the data.

- The following permissions are used for Endpoint analytics:
   - **Read** under the **Device configurations** category.
   - **Read** under the **Organization** category. <!--temporary for pp-->
   - Permissions appropriate to the user's role under the **Endpoint Analytics** category.

A read-only user would only need the **Read** permission under both the **Device configurations** and **Endpoint Analytics** categories. An Intune administrator would typically need all permissions.

## <a name="bkmk_uea_cm_enroll"></a> Enroll devices managed by Configuration Manager
<!--6051638, 5924760-->
Before you enroll Configuration Manager devices, verify the [prerequisites](#bkmk_uea_prereq) including enabling [Microsoft Endpoint Manager tenant attach](../configmgr/tenant-attach/device-sync-actions.md). 

#### <a name="bkmk_uea_cm_enable"></a> Enable Endpoint analytics data collection in Configuration Manager

1. In the Configuration Manager console, go to **Administration** > **Client Settings** > **Default Client Settings**.
1. Right-click and select **Properties** then select the **Computer Agent** settings.
1. Set **Enable Endpoint analytics data collection** to **Yes**.
   > [!Important] 
   > If you have an existing custom client agent setting that's been deployed to your devices, you'll need to update the **Enable Endpoint analytics data collection** option in that custom setting then redeploy it to your machines for it to take effect.

#### <a name="bkmk_uea_cm_upload"></a> Enable data upload in Configuration Manager

1. In the Configuration Manager console, go to **Administration** > **Cloud Services** > **Co-management**.
1. Select **CoMgmtSettingsProd** then click **Properties**.
1. On the **Configure upload** tab, check the option to **Enable Endpoint analytics for devices uploaded to Microsoft Endpoint Manager**

   :::image type="content" source="media/6051638-configure-upload-configmgr.png" alt-text="Enable Endpoint analytics for devices uploaded to Microsoft Endpoint Manager" lightbox="media/6051638-configure-upload-configmgr.png":::

### <a name="bkmk_uea_onboard"></a> Onboard in the Endpoint analytics portal
Onboarding from  the Endpoint analytics portal is required for both  Configuration Manager and Intune managed devices.

1. Go to `https://aka.ms/endpointanalytics`
1. Click **Start**. This will automatically assign a configuration profile to collect boot performance data from all eligible devices. You can [change assigned devices](#bkmk_uea_profile) later. It may take up to 24 hours for startup performance data to populate from your Intune enrolled devices after they reboot.

> [!Important]  
> We anonymize and aggregate the scores from all enrolled organizations to keep the **All organizations (median)** baseline up-to-date. You can [stop gathering data](#bkmk_uea_stop) at any time.

   - For more information about common issues, see [Troubleshooting device enrollment and startup performance](#bkmk_uea_enrollment_tshooter).


## View the Overview page

Once your data is ready, you'll notice some information on the **Overview** page, explained in more detail below:

- The **User experience score** is a 50/50 weighted average of the **Recommended software** and **Startup performance scores**. We'll be expanding the set of subscores over time.

- You can compare your current score to other scores by setting a baseline.
  - As described in the [baseline](#bkmk_uea_baselines) section, there's a built-in baseline for *Commercial median* to see how you compare to a typical enterprise. You can create new baselines based on your current metrics so you can track progress or view regressions over time.
   - Baseline markers are shown for your overall score and subscores. If any of the scores have regressed by more than the configurable threshold from the selected baseline, the score is displayed in red and the top-level score is flagged as needing attention.
  - A status of **insufficient data** means you don't have enough devices reporting to provide a meaningful score. We currently require at least five devices.

- **Insights and recommendations** is a prioritized list to improve your score. This list is filtered to the subnode's context when you navigate to **Best practices** or **Recommended software**.

[![Endpoint analytics overview page](media/overview-page.png)](media/overview-page.png#lightbox)

## Next steps

[Enroll Intune devices](enroll-intune.md)