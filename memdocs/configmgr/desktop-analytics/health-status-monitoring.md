---
title: Health status monitoring
titleSuffix: Configuration Manager
description: Learn about how health status monitoring works in Desktop Analytics.
ms.date: 06/23/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
ms.localizationpriority: medium
ms.collection: tier3
---

# Health status monitoring in Desktop Analytics

As you [deploy an update to production](deploy-prod.md), use Desktop Analytics to help monitor the health state of your devices. This article explains in detail how health monitoring works.

For more information on how to use this feature, see [Monitor the health of updated devices](deploy-prod.md#bkmk_monitor).

:::image type="content" source="media/monitor-health.png" alt-text="Screenshot of the Monitor Health page of Desktop Analytics." lightbox="media/monitor-health.png":::

> [!NOTE]  
> Desktop Analytics only collects health data from devices that provide usage data it can use as a denominator. This means it doesn't include devices running Windows 7 and Windows 10 that aren't set to share diagnostic data at the Optional (limited) level. If more than 10% of devices running Windows 10 are set to share diagnostic data at levels other than Optional (limited), the **Monitor health** page displays a warning in the banner area.  

To view more information about a specific app, select it in the list.

## Apps

### Health status factors

:::image type="content" source="media/monitor-health-status-factors.png" alt-text="Health status factors for an app in Desktop Analytics.":::

Desktop Analytics monitors the following health status factors for apps:

- **% Devices with crashes**: For the last two weeks, the number of devices on which this particular app has crashed divided by the number of devices on which the app has been used. This view lets you see whether the app stability has increased or decreased on the new OS version. Desktop Analytics calculates this percentage for the following sets:  

  - **After update**: Devices that have updated to the target OS version specified in the deployment plan. To reduce the number of assets with insufficient data, Desktop Analytics collects this data for all of your updated devices. This set includes those devices not in the deployment plan.  

  - **Before update**: Devices that are on an OS version earlier than what's specified in the deployment plan. This list doesn't include devices running Windows 7.  

  - **Commercial avg**: The average (avg) crash rate across all commercial devices. This average is calculated across *all* versions of the app. If your version shows a crash rate above the commercial average, there may be a more stable version available.  

- **Mean time to failure**: Similar to the preceding, but counts the average elapsed time between crashes in the last two weeks.<!-- 7226213 -->

To determine the health status of an app, Desktop Analytics requires data from at least 20 devices. Otherwise it reports **Insufficient data** for the app. The service calculates the health status based on the *mean time to failure* from these devices. The device crash rate is provided for information only. It isn't used in the health status calculation.

### Usage

<!-- 5533890 -->

- **Active devices (last 2 weeks)**: This value is the count of devices where a user launched the selected app within the last two weeks. It's based on devices in the selected deployment plan running the targeted version of Windows 10.

- **Total usage duration**: This value is the total usage duration for the selected app on the targeted version of Windows.

### Troubleshooting info

At the bottom of the app details page, use **Recent crashes** to identify devices on which the app recently crashed. Use this information to troubleshoot the issue by gathering logs or trying fixes on specific devices before trying a broader deployment.

If you find a serious health regression that you're unable to fix, change the app's **Upgrade decision** to **Unable**. This action prevents future deployment of the update to devices with this asset.

## See also

- [Compatibility assessment in Desktop Analytics](compat-assessment.md)  

- [How to deploy to production with Desktop Analytics](deploy-prod.md)  
