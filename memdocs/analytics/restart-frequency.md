---
title: Restart frequency in Endpoint Analytics
titleSuffix: Configuration Manager
description: Get details about device restart frequency in Endpoint Analytics
ms.date: 02/2\4/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 9fe09e0a-f8ff-4714-8cf9-453e3197760d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX,NOFOLLOW
---

# Overview
In endpoint analytics [startup performance](startup-performance.md), we've provided insights into PC boot times, and how to improve the reboot times of poorly performing devices. But reboot frequency can be just as impactful to the user experience, as a device that reboots daily due to blue screens will have a poor user experience even if the boot times are fast. We've recently added insights into restart frequencies within your org to help you identify problem devices.

This initial release is focused on providing restart frequency metrics within your tenant. Deeper insights to help reduce excess restarts will be added at a later date. For more information, see the [Known issues](#known-issues) section.

There are no additional prerequisites for using this feature beyond what is already required for endpoint analytics startup performance. This feature doesn't have a dependency on Windows Diagnostics data, so will work regardless of how you have configured the telemetry level or Windows Error Reporting.

## Restart categories

Each restart is categorized into one of six categories. They are described as either abnormal shutdowns or normal shutdowns.
- **Abnormal shutdowns**: Where the shutdown or restart did not go through the normal Windows shutdown process
- **Normal shutdowns**: Where the shutdown or restart went through the normal Windows shutdown process

### Abnormal shutdowns

There are three categories for different types of abnormal shutdowns:
- **Stop errors**: You may also know these as blue screens. Stop errors should be infrequent, less than 2 per device per year is typical.
- **Long power button press**: When an end-user holds the power button down to force a restart. These should be less frequent than stop errors.
- **Unknown**: Any abnormal shutdown that isn't one of the above shutdowns. Over time we'll be refining this list as we isolate issues in this category.

### Normal shutdowns

There are three categories for different types of normal shutdowns:
- **Update**: The restart was done in order to finish install of a Windows update. Ideally there should be around one of these per device per month. Less than once per month is problematic since it indicates devices are not getting patched. More than once per month is also problematic as it indicates users are enduring more update restarts than is typically necessary.
- **Shutdown (no update)**: Typically means someone is trying to save battery or power and isn't indicative of a poor user experience.
- **Restart (no update)**: Ideally this should be close to zero since there shouldn't be a reason to restart a device beyond monthly patching.

To clarify, the difference between **Shutdown (no update)** and **Restart (no update)** is the user's action. A shutdown or restart doesn't have to be initiated through the start menu, it could be initiated other ways too.
:::image type="content" source="media/shutdown-restart.png" alt-text="Shutdown and restart in the Windows Start menu":::

## Device performance tab

In the device performance tab, two default columns have been added at the end so you can review the total number of restarts and the number of stop errors each device had in the last 14 days. Sort by these columns to find problematic devices. You can also use this tab to review the total number of devices that have sent restart records For example, the screenshot below has 31 records, meaning 31 devices  have sent restart data.

