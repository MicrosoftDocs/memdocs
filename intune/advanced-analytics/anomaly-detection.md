---
title: Anomaly Detection in Advanced Analytics
description: Learn how anomaly detection in Microsoft Intune endpoint analytics proactively monitors device health, detects issues, and provides actionable insights for IT admins.
ms.date: 10/09/2025
ms.topic: concept-article
---

# Anomaly detection

[!INCLUDE [intune-add-on-note](../intune-service/includes/intune-add-on-note.md)]

This article explains how anomaly detection in endpoint analytics works as an early warning system.

Anomaly detection monitors the health of devices in your organization for user experience and productivity regressions following configuration changes. When a failure occurs, Anomalies correlates relevant deployment objects to enable rapid troubleshooting, suggest root causes and remediation.

Administrators can rely on anomaly detection to learn about user experience impacting issues before it reaches them through other channels. The initial focus for anomaly detection is on Application hangs/ crashes and Stop Error Restarts.

## Overview

With anomaly detection, you can detect potential problems in a system before they become a serious issue. Traditionally, support teams had limited visibility into potential problems.

- The support channel is only able to report or escalate a subset of the issues. This report isn't truly representative of everything going on in your organization.

- The support channel spends countless hours reviewing custom dashboards trying to identify the root cause, troubleshoot, create custom alerts, change thresholds, and tweak parameters.

Anomaly detection aims at addressing these problems by enabling IT admins with critical information.

In addition to detecting anomalies, you can view device correlation groups to explore potential root causes for medium and high severity anomalies. These device cohorts allow you to view patterns identified among devices. We took a proactive approach to device management by also identifying devices 'at risk' in those cohorts. These 'at risk' devices fall under the identified patterns with high confidence but don't see those anomalies yet.

> [!NOTE]
> Device cohorts are only identified for medium and high severity anomalies.

## Before you begin

Make sure you meet the [requirements](index.md#prerequisites) to confirm your environment meets prerequisites.

## Anomalies tab

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Report** > **Endpoint analytics** > **Overview**.
3. Select **Anomalies** tab. The **Anomalies** tab provides a quick overview of the anomalies detected in your organization.
4. In this example, the **Anomalies** tab shows an *anomaly* with *medium severity* impact. You can add filters to refine the list.

   :::image type="content" source="images/anomaly-detection/anomalies-tab.png" lightbox="images/anomaly-detection/anomalies-tab.png" alt-text="This is a screenshot of the Anomaly tab in Overview section of endpoint analytics":::

5. To see more information about a specific item, choose it from the list. You can see details like the name of the app, which devices are affected, when the issue was first detected and last occurred, and any device groups that might be contributing to the problem.

   :::image type="content" source="images/anomaly-detection/details-of-anomaly.png" lightbox="images/anomaly-detection/details-of-anomaly.png" alt-text="This is a screenshot of details displayed when you select an anomaly displayed in the Anomaly tab ":::

6. Select a device correlation group from the list for a detailed view of the devices' common factors. Devices are correlated based on one or more shared attributes such as app version, driver update, OS version, and device model. You can see the number of devices currently affected by the anomaly and devices at risk of experiencing the anomaly. The prevalence rate also shows you the percentage of affected devices from an anomaly that are members of a correlation group.

   :::image type="content" source="images/anomaly-detection/select-corelation-group.png" lightbox="images/anomaly-detection/select-corelation-group.png" alt-text="This is a screenshot showing Device correlation groups":::

7. Select **View Affected Devices** to display a list of devices with key attributes relevant to each device. You can filter to view devices in specific correlation groups or show all devices affected by that anomaly in your organization. Additionally, the device timeline shows more anomalous events.

   :::image type="content" source="images/anomaly-detection/affected-devices.png" lightbox="images/anomaly-detection/affected-devices.png" alt-text="This is a screenshot showing a list of affected devices":::

## Reviewing Anomaly Detection Data

Investigate flagged Device correlation groups using device timeline and resource reports to determine root cause. Device correlation groups identify root causes for high & medium severity anomalies, along with at risk devices which may be impacted in the future.

- Best practices:
  - IT administrators should periodically review the anomaly detection dashboard, to understand the current baseline and prioritize investigations and resolutions of new issues.
  - Investigate any new reported issues, to identify common factors, as displayed in advanced analytics such as common device hardware.
  - Prioritize the anomalies to investigate based on severity, and internal knowledge like application criticality.
  - Leverage [device timeline](enhanced-device-timeline.md) to review if there is a specific pattern, such as a device restart or update tied to the anomaly.
  - Work with IT teams to understand any other factors that could be impacting this, such as recent application updates.
  - Review possible remediation actions as noted in the Anomaly report (Driver Updates, Application Updates).
  - Integrate the resolution into L1/L2 support, to keep teams aware of current known issues. Consider working with your ITSM team to record known anomalies currently under investigation.
  - Test remediation actions on a subset of devices and monitor before rolling out to wider impacted devices. After remediation has been performed on impacted devices, proactively roll out to at risk devices that may be impacted in the future.
  - Review anomaly detection after any major update or incident to check for possible new issues that need investigation and resolution.
  - To better understand the detection methods, consider reviewing the [Statistical Models](#statistical-models-for-determining-anomalies) used by Anomaly Detection.

## Statistical Models for determining anomalies

The Analytical Model built detects device cohorts facing anomalous set of stop error restarts and application hangs/ crashes that need admin attention to mitigate and resolve. Patterns identified from our sensor telemetry and diagnostics logs determine these device cohorts

- **Threshold based heuristic model**: The heuristic model involves setting one or more threshold values for Application Hangs/Crashes or Stop Error Restarts. Devices are flagged as anomalous if there's a breach in the above set threshold. The model is simple yet effective; it's suited in surfacing prominent or static issues with devices or their apps. Currently, the thresholds are predetermined without an option to customize. 

- **Paired t-tests model**: Paired t-tests are a mathematical method that compares pairs of observations in a dataset, looking for a statistically significant distance between their means. Tests are used on datasets that consist of observations related to each other in some way. For example, count of Stop Error Restarts from the same device before and after a policy change, or app crashes on a device after an OS (operating systems) update.

- **Population Z-score model**: Population Z-score based statistical models involve calculating the standard deviation and mean of a dataset, and then using those values to determine which data points are anomalous.
Standard deviation and mean are used to calculate the Z-score for each data point, which represents the number of standard deviations away from the mean. Data points that fall outside a certain range are anomalous. This model is well suited in highlighting outlier devices or apps from the wider baseline but requires sufficiently large datasets to be accurate.

- **Time Series Z-score model**: Time series Z-score models are a variation of the standard Z-score model designed for detecting anomalies in time series data. Time series data is a sequence of data points collected at regular intervals over time, such as aggregate of Stop Error Restarts.
Standard deviation and mean are calculated for a sliding window of time, using aggregated metrics. This method allows the model to be sensitive to temporal patterns in the data and adapt to changes in its distribution over time.
