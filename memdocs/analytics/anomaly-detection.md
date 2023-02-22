---
title: Anomaly detection in Endpoint Analytics
titleSuffix: Microsoft Endpoint Manager
description: Learn about Anomaly detection in Endpoint Analytics
ms.date: 02/15/2023
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.localizationpriority: high
---


# Anomaly Detection in Endpoint analytics

This article explains how anomaly detection in Endpoint Analytics works as an early warning system.

Anomaly detection monitors the health of devices in your organization for user experience and productivity regressions following configuration changes. When a failure occurs, Anomalies correlates relevant deployment objects to enable rapid troubleshooting, suggest root causes and remediation.

Administrators can rely on anomaly detection to learn about user experience impacting issues before it reaches them through other channels. The initial focus for anomaly detection is on Application hangs/ crashes and Stop Error Restarts.

## Overview

With anomaly detection, you can detect potential problems in a system before they become a serious issue. Traditionally, support teams have limited visibility into potential problems.  

- often, they only get a subset of the issues reported/ escalated through the support channel, which isn't truly representative of everything going on in your organization.  

- they must spend countless hours reviewing custom dashboards trying to identify the root cause, troubleshoot, create custom alerts, change thresholds, and tweak parameters.  

Anomaly detection aims at addressing these problems by enabling IT admins with critical information.

## Pre-requisites

- Licensing/Subscriptions: Intune Suite for EA premium offering

- Permissions: Anomaly detection uses built in [role permissions](overview.md#built-in-role-permissions)  

## Anomalies tab

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Report** > **Endpoint Analytics** > **Overview**.
3. Select **Anomalies** tab. The **Anomalies** tab provides a quick overview of the anomalies detected in your organization.
4. In this example, the **Anomalies** tab shows an *App regression anomaly* with *high severity* impact. You can add filters to refine the list. 

   :::image type="content" source="media/anomaly-detection/anomalies-tab.png" alt-text="This is a screenshot of the Anomaly tab in Overview section of Endpoint Anlaytics":::

5. Select an item from the list to display a detailed view with key information such as App name, affected devices, Date created and Latest occurrence (Initial and latest occurrence of the anomaly), and potential factors influencing the anomaly and suggested remediation.

   :::image type="content" source="media/anomaly-detection/details-of-anomaly.png" alt-text="This is a screenshot of details displayed when you select an anomaly displayed in the Anomaly tab ":::

6. Select **View Affected Devices** to display a list of devices with key attributes relevant to each device. Additionally, the device timeline shows anomalous events.  

   :::image type="content" source="media/anomaly-detection/affected-devices.png" alt-text="This is a screenshot showing a list of affected devices":::

## Statistical Models for determining anomalies

The Analytical Model built detects device cohorts facing anomalous set of stop error restarts and application hangs/ crashes that need admin attention to mitigate and resolve. Patterns identified from our sensor telemetry and diagnostics logs determine these device cohorts

- **Threshold based heuristic model**: The heuristic model involves setting one or more threshold values for Application Hangs/Crashes or Stop Error Restarts. Devices are flagged as anomalous if there's a breach in the above set threshold. The model is simple yet effective; it's suited in surfacing prominent or static issues with devices or their apps. Currently, the thresholds are pre-determined without an option to customize.  

- **Paired t-tests model**: Paired t-tests are a mathematical method that compares pairs of observations in a dataset, looking for a statistically significant distance between their means. Tests are used on datasets that consist of observations related to each other in some way. For example, count of Stop Error Restarts from the same device before and after a policy change, or app crashes on a device after an OS (operating systems) update.  

- **Population Z-score model**: Population Z-score based statistical models involve calculating the standard deviation and mean of a dataset, and then using those values to determine which data points are anomalous. 
Standard deviation and mean are used to calculate the Z-score for each data point, which represents the number of standard deviations away from the mean. Data points that fall outside a certain range are anomalous. This model is well suited in highlighting outlier devices or apps from the wider baseline but requires sufficiently large datasets to be accurate. 

- **Time Series Z-score model**: Time series Z-score models are a variation of the standard Z-score model designed for detecting anomalies in time series data. Time series data is a sequence of data points collected at regular intervals over time, such as aggregate of Stop Error Restarts. 
Standard deviation and mean are calculated for a sliding window of time, using aggregated metrics. This method allows the model to be sensitive to temporal patterns in the data and adapt to changes in its distribution over time.

## Next steps 

For more information, go to:

- Enhanced device timelines
- Device scope  

