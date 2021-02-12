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

- **Crash frequency**: For each of app, the total number of crashes and the total usage duration over a 14 day rolling window is used to calculate the **Mean time to failure** value. This calculation normalizes the crash rate allowing for direct comparison of the relative frequency of crash events across different applications. This value is the primary contributor to an app's reliability score.
- **Total usage duration**: Factoring in the usage duration across all enrolled devices helps ensure the most disruptive application issues are prioritized.

> [!NOTE]
> The **Application reliability** report is currently in preview. While this report is in preview, you'll see your **App reliability score** on the **Overview** page. However, the score won't contribute to your overall endpoint analytics score.
## App performance tab

The **App performance** tab uses data from the past 14 days to show reliability insights for each desktop application in your organization. The following applications are included in the report:

- Foreground applications with a measurable amount of usage in your organization. This ensures that the report is focused on end-user impacting issues.
- Applications with either an active device count that's greater than 5, or a count greater than 2% of the total number of your tenant's enrolled devices, whichever is larger. This helps filter out noise and ensures that calculations are made across a sufficient number of devices to be meaningful.

For each application in the report, the following data is provided:

- **App name**: The app identifier in the file manifest provided by your client devices. The app name is typically in executable (or .exe) format.
- **App display name**: The `friendly name` of the application reported in the file manifest. This column is hidden by default since the data isn't always available.
- **App publisher**: The publisher of the executable reported in the file manifest. Limited cleanup occurs on the app publisher. For instance, `Microsoft Corporation` and `microsoft corporation` are collapsed during cleanup. However, app metadata isn't added or modified in cases where it's unavailable, null, or potentially inaccurate.
- **Active devices (14 days)**: The total number of your tenant's enrolled devices that have launched this app at least once in the past 14 days.
- **Total usage duration (14 days)**: The cumulative usage duration of the application across all your tenant's enrolled devices over the past 14 days. **Engagement time** is used to determine usage duration. **Engagement time** is composed of both:
   -  Interactive time: The time when the user is actively engaging with an application, such as browsing the web
   - Keep-alive time: Time when the application is requesting a keep-alive from the OS, such as when  presenting a PowerPoint or watching a video.
- **Total crashes (14 days)**: The total number of application crash events reported across all enrolled devices in your tenant over the past 14 days.
- **Mean time to failure**: The average amount of engagement time that an end-user is able to use the application before a crash occurs over the past 14 days. This value is calculated by dividing **Total usage duration (14 days)** by **Total crashes (14 days)**. By relating usage duration and crash counts, the frequency of crashes across different applications is normalized. Applications without crash events in your tenant over the past 14 days are given a mean time to failure value of `No crash events`.
- **App reliability score**: A score between 0 and 100 that represents the relative reliability of the application in your tenant. This score is calculated based on **Mean time to failure** and **Total usage duration (14 days)**. A score of 0 represents an unreliable app that is likely hampering end-user productivity. A score of 100 represents a reliable app that is likely contributing to end-user productivity.

> [!NOTE]
> A maximum of 10 application crash events per application, per device, per day is used. This prevents excessive data collections from devices with severe application issues and helps prevent outlier devices from having undue influence over the reliability scores for individual applications.
