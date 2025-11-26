---
title: Configure Endpoint Analytics
description: Step-by-step guide to configure endpoint analytics in Microsoft Intune, enroll devices, and manage data collection policies for device insights.
ms.date: 10/09/2025
ms.topic: how-to
zone_pivot_groups: manage-intune-cm
---

# Configure endpoint analytics

::: zone pivot="intune"

Configure endpoint analytics in Intune by creating a data collection policy and adjusting settings that define your analytics experience.

::: zone-end

::: zone pivot="cm"

Configure endpoint analytics in Configuration Manager by enabling data upload, turning on data collection for devices. Then, adjust settings in the Intune admin center that define your analytics experience.

**Co-managed devices:** We recommend [using Intune for configuration](?pivots=intune). You don't need to shift co-management workloads to Intune. When co-management is enabled, enrolled devices automatically send the required functional data to the Microsoft cloud.

::: zone-end

## Before you begin

Make sure you meet the [requirements](index.md#prerequisites) to confirm your environment meets prerequisites.

::: zone pivot="cm"

## Enable data upload in Configuration Manager

To enable data upload for endpoint analytics in Configuration Manager:

1. In the Configuration Manager console, go to **Administration** > **Cloud Services** > **Cloud Attach**.
1. Select **CoMgmtSettingsProd** then select **Properties**.
1. On the **Configure upload** tab, check the option to **Enable Endpoint analytics for devices uploaded to Microsoft Endpoint Manager**.

> [!IMPORTANT]
> When you enable endpoint analytics data upload, your default client settings are automatically updated to allow managed endpoints to send relevant data to your Configuration Manager site server. If you use custom client settings, you might need to update and re-deploy them for data collection to occur.

   :::image type="content" source="images/6051638-configure-upload-configmgr.png" alt-text="Enable endpoint analytics for devices uploaded to Microsoft Endpoint Manager" lightbox="images/6051638-configure-upload-configmgr.png":::

## Configure data collection client settings

The **Enable Endpoint analytics data collection** client setting lets managed devices send data required for endpoint analytics to your site server. This setting only controls local data collection—it doesn't determine whether data is uploaded to the cloud.

By default, this setting is enabled for devices targeted by the default [client settings](../configmgr/core/clients/deploy/about-client-settings.md). To change this behavior:

1. In the Configuration Manager console, go to **Administration** > **Client Settings** > **Default Client Settings**.
1. Right-click and select **Properties** then select the **Computer Agent** settings.
1. Set **Enable Endpoint analytics data collection** to **Yes** to configure devices for local data collection. Set to **No** to disable local data collection.

You can also modify the **Enable Endpoint analytics data collection** policy in custom client settings to configure a specific set of devices for local data collection. Don't forget to deploy or re-deploy your custom client setting after making changes.

   > [!IMPORTANT]
   > If you have an existing custom client agent setting that is deployed to your devices, you need to update the [**Enable Endpoint analytics data collection**](data-collection.md#data-collection) option in that custom setting and select **Ok** for it to take effect.

::: zone-end

## Enable endpoint analytics

When you open Endpoint analytics for the first time, a guided setup helps you configure data collection. As part of this process, Intune creates a *Windows health monitoring policy* to enable data collection.

1. In the [Microsoft Intune admin center][INT-AC], select **Reports** > **Analytics** > [**Endpoint analytics**][INT-EA].
    :::image type="content" source="images/ea-introduction.png" lightbox="images/ea-introduction.png" alt-text="Endpoint analytics introduction page." border="false":::
1. For **Collect device data from**, choose from the following options:
   - **All cloud-managed devices**: Assigns the policy to all Windows devices that are Intune-managed or co-managed.
   - **Selected devices**: Assigns the policy only to devices you select.
   - **I'll choose later**: Doesn't assign the policy now.
1. Select **Start**.

A configuration profile called *Intune data collection policy* is assigned to the targeted devices, which instructs the devices where to send the data.

::: zone pivot="cm"

> [!NOTE]
> The Intune data collection policy is required for Intune-managed and co-managed devices. Devices managed solely by Configuration Manager don't need this policy assigned because data collection is controlled by Configuration Manager client settings.

::: zone-end

::: zone pivot="intune"

### Change the assignment of the Intune data collection policy

If you want to change which devices contribute data to endpoint analytics, you can change the assignment of the Intune data collection policy.

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Configuration profiles**.
1. Select the profile named **Intune data collection policy**.
1. Select **Properties** > **Assignments** > **Edit**.
1. Change the assignment to include or exclude groups of devices.

You can also create a new profile if you want to target a different set of devices:

1. [Create a Windows health monitoring policy](/intune/intune-service/configuration/windows-health-monitoring).
1. Assign the policy to a group that contains as members the devices that you want to target.

::: zone-end

## General settings

To review the current configuration of endpoint analyticss:

1. In the [Microsoft Intune admin center][INT-AC], select **Reports** > **Analytics** > [**Endpoint analytics**][INT-EA].
    :::image type="content" source="images/ea-settings.png" lightbox="images/ea-settings.png" alt-text="Endpoint analytics general settings page." border="false":::
1. From the **General** pane you can review if the Intune data collection policy is configured and if the Configuration Manager data collection is enabled.

### Consent to share data

When you share anonymized data and aggregate metrics, your organization helps keep the *All organizations (median)* baseline current.

You can revoke consent to share this data at any time. Before revoking consent, consider the impact on your reports and insights:

- Reports that rely on shared data—such as startup performance insights—are disabled.
- Existing report data becomes stale immediately, and no new data is added.
- Historical data remains visible for up to 60 days, after which it's removed.

To revoke consent:

1. Clear the checkbox that states **I consent to share anonymized and aggregate metrics to see updated Endpoint analytics scores and insights**.
1. Select **Yes** to confirm the action.
1. Optionally, [stop gathering data](data-collection.md#stop-gathering-data).

## Configure baselines

Baselines help you compare your performance to industry norms or track progress using your own metrics.

To create a custom baseline and adjust the regression threshold:

1. In the [Microsoft Intune admin center][INT-AC], select **Reports** > **Analytics** > [**Endpoint analytics**][INT-EA].
1. Select **Settings** > **Baseline**.
    :::image type="content" source="images/ea-settings-baseline.png" lightbox="images/ea-settings-baseline.png" alt-text="Endpoint analytics baseline settings page." border="false":::
1. Select **Create new** and enter a name.
    > [!TIP]
    > Include the date in the name for easier selection from the drop-down in reports.
1.  Metrics are flagged red and marked as *regressed* if they fall below the current baseline. Because daily fluctuations are normal, set a **regression threshold** (default is 10%) so metrics are only flagged when they regress by more than the percentage you specify.

You can create up to 20 baselines per tenant. Delete old baselines when they're no longer needed.

## Review collected data

After devices receive the data collection policy, they begin sending data to endpoint analytics. The service processes and calculates the data before displaying results. It can take up to **24 hours after a restart** for data to appear in reports.

For startup performance metrics, devices must restart at least once.

To learn more about how data flows and is collected from devices to the Microsoft cloud, see [Data flow](data-collection.md#data-flow).

When processing is complete, the **Overview** page updates with your organization's data:

- The **Endpoint analytics score** is a weighted average of the [Startup performance](startup-performance.md), [Application reliability](app-reliability.md), and [Work from anywhere](work-from-anywhere.md) scores.
- You can compare your current score to other scores by selecting a baseline.
  - Baseline markers are shown for your overall score and subscores. If any of the scores have regressed by more than the configurable threshold from the selected baseline, the score is displayed in red and the top-level score is flagged as needing attention.
  - A status of **insufficient data** means you don't have enough devices reporting to provide a meaningful score. We currently require at least five devices.
- **Insights and recommendations** is a prioritized list to improve your score. This list is filtered to the subnode's context when you navigate.

:::image type="content" source="images/ea-overview.png" alt-text="Screenshot of the endpoint analytics overview page." lightbox="images/ea-overview.png" border="false":::

## Next Steps

Learn more about endpoint analytics:

- [Scores, baselines, and insights](scores.md)
- Understand the reports:
  - [Startup performance](startup-performance.md)
  - [Restart frequency](restart-frequency.md)
  - [Application reliability](app-reliability.md)
- [Understand data collection](data-collection.md)
- [Microsoft Intune Advanced Analytics](../advanced-analytics/index.md)

<!-- admin center -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-EA]: https://aka.ms/endpointanalytics
[PORTAL-0]: https://aka.ms/uea
[PORTAL]: https://aka.ms/uea_prereq
[PORTAL_1]: https://aka.ms/uea_baselines
[PORTAL_2]: https://aka.ms/uea_prereq_configmgr

<!-- role links -->

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#read-only-operator
[INT-R5]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

[ENT-R1]: /entra/identity/role-based-access-control/permissions-reference#global-administrator
[ENT-R2]: /entra/identity/role-based-access-control/permissions-reference#intune-administrator
[ENT-R3]: /entra/identity/role-based-access-control/permissions-reference#reports-reader
