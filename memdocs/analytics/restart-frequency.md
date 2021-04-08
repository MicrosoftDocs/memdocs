---
title: Restart frequency (preview) in endpoint analytics
titleSuffix: Microsoft Endpoint Manager
description: Get details about device restart frequency in endpoint analytics
ms.date: 03/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 9fe09e0a-f8ff-4714-8cf9-453e3197760d
author: mestew
ms.author: mstewart
manager: dougeby
---

# Restart frequency (preview) in endpoint analytics
<!--IN6225459-->
In endpoint analytics [startup performance](startup-performance.md), we've provided insights into PC boot times, and how to improve the reboot times of poorly performing devices. Reboot frequency can be just as impactful to the user experience since a device that reboots daily because of blue screens will have a poor user experience even if the boot times are fast. We've recently added insights into restart frequencies within your organization to help you identify problematic devices.

## Prerequisites

- Devices are enrolled in endpoint analytics.
   - [Enroll Configuration Manager devices](enroll-configmgr.md)
   - [Enroll Intune devices](enroll-intune.md)
   - After enrollment, client devices require a restart to fully enable all analytics. <!--7698085-->
- Devices meet the endpoint analytics [startup performance](startup-performance.md) requirements.
- Devices enrolled from Configuration Manager need client version 2006, or later installed

## Restart categories

Each restart is categorized into one of six categories. They're described as either abnormal shutdowns or normal shutdowns.

**Abnormal shutdowns**: Where the shutdown or restart didn't go through the normal Windows shutdown process. There are three categories for different types of abnormal shutdowns:
- **Blue screens**: You may also know these as stop errors. Stop errors should be infrequent, less than 2 per device per year is typical.
- **Long power button press**: When an end user holds the power button down to force a restart. These shutdowns should be less frequent than stop errors (blue screens).
- **Unknown**: Any abnormal shutdown that isn't one of the above shutdowns. Over time we'll be refining this list as we isolate issues in this category.

**Normal shutdowns**: Where the shutdown or restart went through the normal Windows shutdown process. There are three categories for different types of normal shutdowns:

- **Update**: The restart was done to finish installation of a Windows update. Ideally there should be around one of these restarts per device per month. Less than once per month is problematic since it indicates devices aren't getting patched. More than once per month is also problematic as it indicates users are enduring more update restarts than is typically necessary.
- **Shutdown (no update)**: Typically means someone is trying to save battery or power and isn't indicative of a poor user experience.
- **Restart (no update)**: Ideally this should be close to zero since there shouldn't be a reason to restart a device beyond monthly patching.

The difference between **Shutdown (no update)** and **Restart (no update)** is the user's action. A shutdown or restart doesn't have to be initiated through the start menu, it could be initiated other ways too.

:::image type="content" source="media/shutdown-restart.png" alt-text="Shutdown and restart in the Windows Start menu":::

## Device performance tab

In the device performance tab, two default columns have been added so you can review the total number of restarts and the number of blue screens (stop errors) each device had in the last 14 days. Sort by these columns to find problematic devices. You can also use this tab to review the total number of devices that have sent restart records. For example, the screenshot below has 31 records, meaning 31 devices have sent restart data.

:::image type="content" source="media/device-performance-tab.png" alt-text="Device performance tab under Startup Performance" lightbox="media/device-performance-tab.png":::

## Model performance tab

In the model performance tab, two default columns have been added so you can review both the average number of restarts and the average number of blue screens (stop errors) per model over the last 14 days. Sort by these columns to find problematic device models. Only models with at least 10 devices are shown to ensure the averages are done across enough devices to be meaningful.

:::image type="content" source="media/model-performance-tab.png" alt-text="Model performance tab under Startup Performance" lightbox="media/model-performance-tab.png":::

## Restart frequency tab

The new restart frequency tab shows aggregates of restart frequency counts for each of the [restart categories](#restart-categories) over the last 14 days. For each restart category, the following information is displayed:

- Number of devices that have had at least one restart in that category
- The average number of restarts per device across all devices, to understand the total impact.
  - This average is all devices, not just the ones that had at least one restart in the category.

The trend chart indicates how the rolling 14-day average changes over time. If there is a regression you'll be able to see it and identify when it started. Clicking through the metrics table will take you to the [**Device performance** tab](#device-performance-tab), sorted by number of restarts, so you can quickly identify the devices with the most restarts.

:::image type="content" source="media/restart-frequency-tab.png" alt-text="Restart frequency tab under Startup Performance" lightbox="media/restart-frequency-tab.png":::

## Devices page

Clicking through to a particular device in the [**Device performance** tab](#device-performance-tab), takes you to the device's **Startup performance** tab. The table called **OS version history** was renamed to **OS restart history**. 

The **OS restart history** table has the following information:
-  The **Restart category** for each reboot
- For blue screens (stop errors), the following additional information is available: 
   - The [stop code](/windows-hardware/drivers/debugger/bug-check-code-reference2), also called the bug check code
   - A **Failure bucket ID** that can be used for diagnostics when working with Microsoft support

:::image type="content" source="media/device-page-os-restart-history.png" alt-text="OS restart history under the Device page" lightbox="media/device-page-os-restart-history.png":::

The **OS restart history** table is truncated to the 10 most recent restarts that occurred in the last 2 months. The table is low latency, so new restarts typically show up here before they appear in the daily aggregates shown in the **Device performance** tab.

## Known issues

- Currently, only snapshot baselines are supported. You can compare the current metrics within your tenant to a set of metrics you took a snapshot of previously. An **All organizations (median)** baseline isn't available.

- The count of restarts in a device's restart history in the [**Devices page**](#devices-page) may not match the count shown in the **Device performance** tab. This is by design. The differences are: 
   - The aggregates in the [**Device performance** tab](#device-performance-tab) are computed daily to show counts for the last 14 days
	- The restart history in the [**Devices page**](#devices-page) is truncated to the 10 most recent restarts and goes back up to the last 2 months. This page also has low latency, so new restarts will typically show up here before they make their way into the daily aggregates shown in the **Device performance** tab. The [**Device performance** tab](#device-performance-tab) doesn't have that truncation and goes back for the last 14 days.

- Currently, there isn't an aggregation of blue screens by *driver* or *failure bucket ID*.

