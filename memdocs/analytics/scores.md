---
title: Scores, baselines, and insights in Endpoint Analytics
titleSuffix: Microsoft Endpoint Manager
description: Learn about scores, baselines, and insights in Endpoint Analytics
ms.date: 07/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: ce1cdea9-b530-4d4d-a01f-aadc42021831
author: mestew
ms.author: mstewart
manager: dougeby

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

**Insights and recommendations** is a prioritized list to improve your score. The whole list is displayed on the **Overview** page either beside or below the charts depending on the width of your browser window. **Insights and recommendations** are filtered to the subnode's context when you navigate through reports. The recommendation listed with each insight tells you how to increase the score and how many points the score will gain when the recommendation is complete. When reviewing **Insights and recommendations**, the `Learn more` link takes you to information about how the metric is scored and the recommended course of action is for the insight.  

## Per device scores

To help you identify devices that could be impacting user experience, Endpoint analytics shows some scores per device. Reviewing scores per device may help you find and resolve end-user impacting issues before a call is made to the help desk.From the **Endpoint analytics** main page, select the **Device scores** tab to display individual device scores. Sorting by scores can assist you in finding devices that might need attention. The following scores are displayed per device:

- [Endpoint analytics score](enroll-intune.md#bkmk_view)
- [Startup performance score](startup-performance.md#bkmk_score)
- [Application reliability score](app-reliability.md#app-reliability-score)

**Placeholder - Insert screenshot of the Device scores tab**

Selecting a device from the **Devices scores** tab loads a device page that gives you more information. From the device's **Startup performance** tab, review **Boot history** and **Sign-in history** for experience impacting trends. The **Application reliability** tab provides insight into potential issues for desktop applications on the managed device.

**Placeholder - Insert screenshot of the device's Endpoint analytics page**

### <a name="bkmk_drill-in"></a> Device level drill-in from reports

When reviewing your organization's **Startup performance** or **Application reliability** reports, you can display individual device scores. To drill-in to  information for a specific device, select the **Device performance** tab, then choose a device.

**Placeholder - Insert screenshot of the device's Startup performance page**

## Next steps

- Use [Proactive remediations](proactive-remediations.md) to gather more data and take action on devices