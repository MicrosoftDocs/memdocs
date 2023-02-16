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


# Anomaly Detection in Endpoint analytics

This article explains how anomaly detection in Endpoint Analytics works as an early warning system.

Anomaly detection monitors the health of devices in your organization for user experience and productivity regressions following configuration changes. When a failure occurs, Anomalies correlates relevant deployment objects to enable rapid troubleshooting, suggest root causes and remediation.

Administrators can rely on anomaly detection to learn about user experience impacting issues before it reaches them through other channels.The initial focus for anomaly detection is on Application hangs/ crashes and Stop Error Restarts.

## Overview

Anomaly detection is used to detect potential problems in a system before they become serious, allowing for proactive measures to be taken to prevent costly damage.

Traditionally, support teams have limited visibility into these potential problems.  

- often, they only get a subset of the issues reported/ escalated through the support channel, which is not truly representative of everything going on in your organization.  

- they must spend countless hours reviewing custom dashboards trying to identify the root cause, troubleshoot, create custom alerts, change thresholds, and tweak parameters.  

Anomaly detection aims at addressing these problems by enabling IT admins with critical information.

## Pre-requisites

- Licensing/Subscriptions: Intune Suite for EA premium offering

- Permissions: Anomaly detection leverages built in [role permissions](overview.md#built-in-role-permissions)  

## Anomalies tab

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Report** > **Endpoint Analytics** > **Overview**.
3. Select **Anomalies** tab. The **Anomalies** tab provides a quick overview of the anomalies detected in your organization.
4. In this example, the **Anomalies** tab shows an *App regression anomaly* with *high severity* impact. Anomalies are listed by severity and you can add filters to refine the list. 
 Image here
5. Select an item from the list and a detailed view is displayed with key information such as App name, affected devices, Date created and Latest occurrence (Initial and latest occurrence of the anomaly), and potential factors influencing the anomaly and suggested remediation.
 image here
6. Select View Affected Devices. A detailed list of devices with other key attributes relevant to the given device is displayed. Additionally, anomalous events can also be seen on the device timeline.  
 Image here

## Analytical or Statistical Models for determining anomalies

The Analytical Model built detects device cohorts facing anomalous set of stop error restarts and application hangs/ crashes that need admin attention to mitigate and resolve. These device cohorts are determined based on the patterns identified from our sensor telemetry and diagnostics logs. 

- Threshold based heuristic model: This technique involves setting one or more threshold values for Application Hangs/Crashes or Stop Error Restarts. Devices are flagged as anomalous if there is a breach in the above set threshold. This model is simple yet effective; it is particularly suited in surfacing prominent or static issues with devices or their apps. Currently, the thresholds are pre-determined without an option to customize.  

- Paired t-tests model: Paired t-tests are a mathematical method that compares pairs of observations in a dataset, looking for a statistically significant distance between their means. These tests are used on datasets that consist of observations that are related to each other in some way, such as count of Stop Error Restarts from the same device before and after a policy change, or app crashes on a device after an OS (operating systems) update.  

- Population Z-score model: Population Z-score based statistical models involve calculating the standard deviation and mean of a dataset, and then using those values to determine which data points are anomalous. The standard deviation and mean are used to calculate the Z-score for each data point, which represents the number of standard deviations away from the mean. Data points that fall outside a certain range are considered anomalous. This model is well suited in highlighting outlier devices or apps from the wider baseline but requires sufficiently large datasets to be accurate. 

- Time Series Z-score model: Time series Z-score models are a variation of the standard Z-score model designed for detecting anomalies in time series data. Time series data is a sequence of data points collected at regular intervals over time, such as aggregate of Stop Error Restarts. In this model, the standard deviation and mean are calculated for a sliding window of time, using aggregated metrics. This allows the model to be sensitive to temporal patterns in the data and adapt to changes in its distribution over time.

## Next steps 

Organizations go through ups and downs, baselines could vary across geographies, user base and so on. Microsoft plans to leverage the power of AI (artificial intelligence) and machine learning models to better understand device cohort and to surface what really matters. 

Over time, Anomaly Detection will monitor the health of devices in your organization for user experience and productivity regressions like Boot and Logon times, App Hangs && || Crashes, Network Connectivity, Battery Health, OS Crashes (Blue Screen) , then help you correlate with any configuration events occurring on the device like an OS upgrade, a Security updates, Driver install/ updates, App Install/ updates to help admins troubleshoot things faster.