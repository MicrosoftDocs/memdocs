---
title: Scores, baselines, and insights in Endpoint Analytics
titleSuffix: Microsoft Endpoint Manager
description: Learn about scores, baselines, and insights in Endpoint Analytics
ms.date: 07/07/2022
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: high
---

# <a name="bkmk_device"></a> Endpoint analytics scores, baselines, and insights

When you first open the **Overview** page in **Endpoint analytics**, you're presented with a few score charts. You'll also notice there's information about what affects the scores and how to improve them if needed. Understanding the following three items are central to understanding each of the reports:

- Scores
- Baselines
- Insights and recommendations

:::image type="content" source="media/8816759-overview-page.png" alt-text="Screenshot of the Endpoint analytics overview page" lightbox="media/8816759-overview-page.png":::

## Understanding scores

**Endpoint analytics** scores range from 0 to 100. Lower scores indicate there's room for improvement. Scores help you understand the relative impact of each metric in your environment. For instance, when reviewing your [startup score](startup-performance.md), you find that overall your score of 61 is higher than the [baseline](#baselines) of 50 for all organizations. When examining the startup score breakdown, you find that your environment excels during the core boot phase with a score of 77. However, based on the average time it takes to get to a responsive desktop, you suspect long running startup processes are lowering the core sign-in score to 46. Reviewing the top [insights and recommendations](#bkmk_insights) entry for the startup score confirms that long running processes are responsible for the impact on the score. 

:::image type="content" source="media/8816759-startup-score.png" alt-text="Screenshot of the startup score page showing an overall startup score of 61 and an all organizations baseline score of 50. Startup subscores are core boot phase at 77 and core sign-in at 46. Under the core sign-in subscore, the average time to responsive desktop is 54 seconds. Insights and recommendations show 40 devices are taking 166 seconds longer than other devices due to startup process delays" lightbox="media/8816759-startup-score.png":::

A status of **insufficient data** means you don't have enough devices reporting to provide a meaningful score. Currently, at least five devices are required.

## Baselines

Baseline scores are shown on charts as triangle markers. There's a built-in baseline for **All organizations (median)**, which allows you to compare your scores to a typical enterprise. You can create new baselines based on your current metrics so you can track progress or view regressions over time. For more information about creating baselines, see [baseline settings](settings.md#bkmk_baselines).

:::image type="content" source="media/8816759-baseline.png" alt-text="Screenshot of Endpoint analytics score chart. A red square outline is around the baseline number and baseline triangle marker" lightbox="media/8816759-baseline.png":::

> [!Important]  
> We anonymize and aggregate the scores from all enrolled organizations to keep the **All organizations (median)** baseline up-to-date. You can [stop gathering data](data-collection.md#bkmk_stop) at any time.

## <a name="bkmk_insights"></a> Insights and recommendations

**Insights and recommendations** is a prioritized list to improve your score. The whole list is displayed on the **Overview** page either beside or below the charts depending on the width of your browser window. **Insights and recommendations** are filtered to the subnode's context when you navigate through reports. The recommendation listed with each insight tells you how to increase the score and how many points the score will gain when the recommendation is complete.
- Selecting the insight link from **Insights and recommendations** provides you with more information on devices and attributes related to the insight. 
- The `Learn more` link takes you to information about how the metric is scored and the recommended course of action is for the insight.  

## <a name="bkmk_per-device"></a> Per device scores
<!--IN8462182-->
To help you identify devices that could be impacting user experience, Endpoint analytics shows some scores per device. Reviewing scores per device may help you find and resolve end-user impacting issues before a call is made to the help desk. From the **Endpoint analytics** main page, select the **Device scores** tab to display individual device scores. Sorting by scores can assist you in finding devices that might need attention.

:::image type="content" source="media/8816759-per-device-scores-chart.png" alt-text="Screenshot of Endpoint analytics device scores chart from the overview page." lightbox="media/8816759-per-device-scores-chart.png":::

Selecting a device from the **Devices scores** tab loads a device page that gives you more information. From the device's **Startup performance** tab, review **Boot history** and **Sign-in history** for experience impacting trends. The **Application reliability** tab provides insight into potential issues for desktop applications on the managed device.

:::image type="content" source="media/8816759-per-device-scores.png" alt-text="Screenshot of a device's Endpoint analytics score with the startup performance and application reliability subscores." lightbox="media/8816759-per-device-scores.png":::

You can also access per device scores on a device's **User experience** page. From the **User experience** page you can review the **Endpoint analytics**, **Startup performance**, and **Application reliability** information for the specific device.

:::image type="content" source="media/user-experience-page.png" alt-text="Screenshot of a device's user experience page displaying the startup performance tab." lightbox="media/user-experience-page.png":::

### <a name="bkmk_drill-in"></a> Device level drill-in from reports

When reviewing your organization's reports, you can display individual device scores. To drill-in to  information for a specific device, select the **Device performance** tab, then choose a device.

:::image type="content" source="media/8816759-per-device-startup-score.png" alt-text="Screenshot of Endpoint analytics startup performance page for a single device." lightbox="media/8816759-per-device-startup-score.png":::

> [!Note]
> You may notice small differences in values when reviewing detailed reporting when compared to overall less granular scores for devices and models.

## <a name="bkmk_model"></a> Per model scores
<!--IN14439211-->
Endpoint analytics shows scores per device model. These scores help admins contextualize the user experience across device models in the environment. Reviewing model scores may help you project and prioritize your next hardware refresh cycle. It can also help you discover devices that no longer meet your organization's current hardware specifications. From the **Endpoint analytics** main page, select the **Model scores** tab to display scores per device model. Scores per device model are available in all Endpoint analytics reports.

## Filter reports
<!--7207888-->
Use the **Add filter** option on tables to display items that match your criteria. You can add more filters to drill further into your data. Using filters enables you to discover trends in your environment or spot potential issues. For instance, in the **Device performance** tab of the **Startup performance** report, you might use a filter to identify devices with a high **Time to responsive desktop**. After reviewing your filtered data, you add another filter to include devices with a high **Group Policy sign-in time**. With the additional filter, you can gauge the impact Group Policy has on the user experience for devices that take a long time to get to a responsive desktop.

:::image type="content" source="media/7207888-filter.png" alt-text="Screenshot of a table filter in Endpoint analytics." lightbox="media/7207888-filter.png":::

> [!NOTE]
> There are currently limitations in the following filters:
> - The **Disk type** filter doesn't support the value **Unknown**<!--12829141-->. 
> - Filtering on **Startup performance score** from **Overview** > **Device Scores** returns devices with a score of "--". <!--12829158-->

## Known issues

[!INCLUDE [Endpoint analytics export to csv value mapping known issue](includes/known-issue-csv-mapping.md)]

## Next steps

- Use [Proactive remediations](proactive-remediations.md) to gather more data and take action on devices