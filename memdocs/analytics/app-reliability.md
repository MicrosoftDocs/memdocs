---
title: Application reliability (preview) in endpoint analytics
titleSuffix: Configuration Manager
description: Get details about application reliability in endpoint analytics
ms.date: 02/24/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 68d07732-421e-40ca-9ee3-f5a856407259
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
---

# Application reliability (preview) in endpoint analytics
<!--IN5653073-->
The application reliability report provides insight into potential issues for desktop applications on managed devices. You can quickly identify the top applications that are impacting end-user productivity, and see aggregate app usage along with app failure metrics for these applications. From the report, drill into specific device data and view a timeline of app reliability events to troubleshoot end-user impacting issues.

:::image type="content" source="media/5659073-application-reliability.png" alt-text="Application reliability report in endpoint analytics" lightbox="media/5659073-application-reliability.png":::

## Prerequisites

- Devices be enrolled in endpoint analytics.
   - [Enroll Configuration Manager devices](enroll-configmgr.md)
   - [Enroll Intune devices](enroll-intune.md)
- Devices enrolled from Configuration Manager need client version 2006, or later installed.

## App reliability score

The **App reliability score** provides a high-level view of desktop application robustness across your environment. As with other endpoint analytics scores, the **App reliability score** is a number between 0 and 100. The score is calculated from the app reliability scores of each desktop application in your environment that's found in the **App performance** tab. 

Each application on the **App performance** tab is assigned an **App reliability score** based on:

- **Total usage duration**: Factoring in the usage duration when calculating an app's reliability score helps ensure the most disruptive application issues are prioritized.
- **Crash frequency**: For each of app, the total number of crashes and the total usage duration over a 14 day rolling window is used to calculate the **Mean time to failure** value. This calculation normalizes the crash rate allowing for direct comparison of the relative frequency of crash events across different applications. This value is the primary contributor to an app's reliability score.

> [!NOTE]
> The **Application reliability** report is currently in preview. While this report is in preview, you'll see your **App reliability score** on the **Overview** page. However, the score won't contribute to your overall endpoint analytics score.
## App performance tab

