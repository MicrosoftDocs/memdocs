---
# required metadata

title: Settings insight
description: The Settings insight feature adds insights giving you confidence in configurations that are successfully adopted by similar organizations.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 7/31/2024
ms.topic: article
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: Lavanya.lakshman
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Settings insight

Settings insight is tailored insights powered by a Machine Learning model. This article explains how Settings insight works. Settings insight is currently available within Intune security baselines.

A security baseline comprises a set of expert recommended configurations to secure devices, apps, and services. Settings insight adds insights to security baselines giving you confidence in configurations that are successfully adopted by similar organizations.

## Overview

The Settings insight feature provides confidence in configurations by adding insights that similar organizations have successfully adopted. This article explains how Settings insight can be accessed or viewed for policies that are created or that exist in Microsoft security baselines.

For example, if an organization is in the manufacturing industry, we'll look at what similar organizations with similar profiles are doing, and prepare a plan tailored to their specific situation.

This feature is now generally available.

## Prerequisites

- **Licensing/Subscriptions**: You must have a Microsoft Intune Plan 1 license to use Settings insight. For more information, see [Licenses available for Microsoft Intune](../fundamentals/licenses.md)
- **Permissions**: Global Admins or Endpoint Security Administrators can create a profile using Baselines.  

## Viewing insights

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Security baselines** to view the list of available baselines.

3. Select one of the following baselines you'd like to use, and then select **Create profile**.
    - Microsoft Edge Baseline
    - Microsoft 365 Apps for Enterprise Security Baseline

4. On the **Basics** tab, specify the **Name**, and **Description** properties.

5. Select **Next** to go to the next tab.

6. On the **Configuration settings** tab, view the groups of **Settings** that are available. You can expand a group to view the settings in that group, and the default values for those settings. Insights are available beside some settings with a light bulb icon.

    :::image type="content" source="./media/settings-insight/createprofile-settingsinsight.png" alt-text="Settings insight shown while creating a profile" lightbox="./media/settings-insight/createprofile-settingsinsight.png":::

7. You can also view these insights while editing a Profile.

    :::image type="content" source="./media/settings-insight/editprofile-settingsinsight.png" alt-text="Settings insight shown while editing a profile" lightbox="./media/settings-insight/editprofile-settingsinsight.png":::

## Models used to categorize organizations

Similar organizations are identified using a K-means clustering model based on customer attributes, such as industry, organization size, etc. Clustering algorithms and key attributes are selected through experiments so that customers are grouped appropriately. The model determines the optimal number of clusters at runtime based on clustering performance.

Setting value recommendations are then made for similar organizations categorized in the same cluster. Healthy organizations within a cluster are first identified based on Endpoint analytic scores. For a common setting, the setting value used by most of the organizations is recommended to other similar organizations within the same cluster. The recommended setting value is only suggested if it aligns with the default setting value that Microsoft baseline selects and functions as a positive reinforcement.

> [!IMPORTANT]
> Customer Data is not being used in the model. Usage data is aggregated at organization level and is converted to categorical format when possible.
> For example, a Boolean attribute is used to reflect whether the customer has Microsoft Exchange in use and categorical data is used to show the range of deployment ratio rather than the actual deployment ratio. Data in use is signed off via privacy and security reviews to ensure compliance and is securely stored with appropriate protection and retention management.

Other safeguard measures are also applied to inhibit individual customer inference. For example, no recommendation is made if the number of similar customers within one cluster is below a given threshold or when the setting isn't adopted by the required minimum number of organizations. Data aggregation and a set of thresholds are applied to protect the confidentiality of individual organizations.  

Model execution and performance are actively monitored to ensure quality and reliability. A series of live monitors is set up to closely watch execution anomalies and key performance metrics. Prompt investigation and regular maintenance are in place to provide valuable recommendations to customers.

## Why some settings may not have insights

Settings insight is powered by machine learning and heavily relies on underlying data used to make recommendations. For reliable recommendations, we have set considerable guardrails in place to only show recommendations when we have sufficient data to support them. If the admin doesn't see recommendations for certain settings, it could mean we didn't have sufficient data to provide an insight. However, this could change over a period as more data becomes available.  

## Next steps

For more information about security baselines, go to:

- [Security baselines](../protect/security-baselines.md)
- [Create security baseline profiles in Microsoft Intune](../protect/security-baselines-configure.md)
